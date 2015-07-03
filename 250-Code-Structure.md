---
layout: post
title:  "Code & Packet structure"
date:   2015-07-03 17:10:00
categories: open-fpga-nvm manual
permalink: /code-structure/
---

# Code

1. State Machines
    - Main Loop States
    
    ```verilog
    parameter
        INIT_0     = 30, INIT_1     = 29, INIT_2     = 28,
        LOOP_ADDR_0= 01, LOOP_ADDR_1= 02, LOOP_ADDR_2= 03, LOOP_ADDR_3= 04, LOOP_ADDR_4= 05,
        RS_0       = 06, RS_1       = 07, RS_2       = 08, //RS_3       = 09,
        WR_0       = 09, WR_1       = 10, //WR_2       = 12,
        RD_0       = 11, RD_1       = 12, //RD_2       = 15,
        ER_0       = 13, ER_1       = 14, //ER_2       = 18,
        UART_0     = 15, UART_1     = 16, UART_2     = 17, UART_3     = 18,
        INIT_FULL_LOOP = 19,
        LOOP_END   = 31;    
    ```
    - NVM-specific Loop States

    ```verilog
    parameter
        INIT       = 30, INIT_T     = 31, STOP       = 00,
        CMDA_0     = 01, CMDA_1     = 02, CMDA_2     = 03,
        ADDR_0     = 04, ADDR_1     = 05, ADDR_2     = 06, ADDR_3     = 07,
        CMDB_0     = 08, CMDB_1     = 09, CMDB_2     = 10,
        WAIT_CYL   = 11,
        WAIT_RB_0  = 12, WAIT_RB_1  = 13,
        DATA_IN_0  = 14, DATA_IN_1  = 15, DATA_IN_2  = 16, DATA_IN_3  = 17, DATA_IN_4  = 18,  //WRITE
        DATA_OUT_0 = 19, DATA_OUT_1 = 20, DATA_OUT_2 = 21, DATA_OUT_3 = 22, DATA_OUT_4 = 23, DATA_OUT_5 = 24,  //READ
        RESET_0    = 25, RESET_1    = 26, RESET_2    = 27, RESET_3    = 28, RESET_4    = 29;    
    ```
    - Serial Loop
        - TX
        - RX
    - Debug Loop
        - There is a state machine for displaying all of 4 digits of 7-Segments
        - ( FYI, LEDs are not in loop, just shows state number of NVM state machine. )

2. Physical pin definition
    - In Verilog code, _.ucf_ file defines which pins are connected to which pin.
    - PIN names are described in _Nexys 3_ manual.
    - Regarding pinout of PCB design, simply matching the pins definition on _.ucf_ file makes it connection.
    
        - TLC NAND pin-connection

            <img src="https://raw.githubusercontent.com/open-fpga-nvm/open-nvm-hardware/master/pic/tlcNand_VHDCI_conn.png" width="350">

        - MRAM pin-connection

            <img src="https://raw.githubusercontent.com/open-fpga-nvm/open-nvm-hardware/master/pic/MRAM_VHDCI_conn.png" width="400">

# Packet Structure
1. Common characteristics
    - Baud-rate: 1152000 bps
    - Using Big-Endian for data values
        - In-code pySerial initialization
        
            ```python
            self.sp = serial.Serial(com_port_num, 115200, timeout=3)
            ```
        - In-code Verilog timer definition
        
            ```verilog
            `define BIT_TMR_MAX 10'd869
            ```
            - How to calculate the counter number _869_:
                - Current FPGA Clock = 100Mhz ( 1tick = 10ns ), target baud-rate = 1152000bps
                - (100,000,000ticks/s) / (115200bits/s) = 869ticks/bit

1. PC → Board (FPGA - RX)
    - Configuration
    - Start/Stop
    - 12 bytes per each packet
    - RAW Packet Structure
    ![](/resource/image/packet-rx.png)
    - In-code implementation (Python part)
    
    ```python
    def uADDR(addr1, addr2):
        return struct.pack('>BIIHB', 0x00, addr1, addr2, 0, 0xEE)

    def uOPER(oWR, oRD, oER, oRST):
        mOPER = 0x0
        if oWR : mOPER |= 0x01
        if oRD : mOPER |= 0x02
        if oER : mOPER |= 0x04
        if oRST: mOPER |= 0x08
        return struct.pack('>BBBBBIHB', 0x01, mOPER,0,0,0, 0, 0, 0xEE)

    def uLOOP(loop_count):
        return struct.pack('>BIIHB', 0x02, loop_count, 0, 0, 0xEE)

    def uLOG(log_freq2):
        return struct.pack('>BIIHB', 0x03, log_freq2, 0, 0, 0xEE)

    def uNAND(pLSB, pCSB, pMSB, ptrn_usr0=0, ptrn_usr1=0, ptrn0=0, ptrn1=0xFF):
        mPAGETYPE = 0
        if pLSB : mPAGETYPE |= 0x01
        if pCSB : mPAGETYPE |= 0x02
        if pMSB : mPAGETYPE |= 0x04
        return struct.pack('>BBBBBHHHB', 0x04, mPAGETYPE, 0, ptrn_usr0,ptrn_usr1, ptrn0,ptrn1, 0, 0xEE)

    def uMRAM(addr1, addr2):
        return struct.pack('>BIIHB', 0x05, addr1, addr2, 0, 0xEE)

    def uSTART():
        return struct.pack('>BIIHB', 0xF0, 0, 0, 0, 0xEE)

    def uHALT():
        return struct.pack('>BIIHB', 0xF1, 0, 0, 0, 0xEE)    
    ```
    
    
2. Board → PC (FPGA - TX)
    - Result
    - 14 bytes per each packet
    - This data is captured/saved into log file and processed with _parser_.
    - RAW Packet Structure
    ![](/resource/image/packet-tx.png)
    - In-code implementation (Verilog part)
    
    ```verilog
    assign tx_data[7:0]=(           (tx_idx ==  0) ? { 6'h0, Oper[1:0] } :                  //Oper
                         (          (tx_idx ==  1) ? { 8'h0 } :                             //ADDR[3]
                          (         (tx_idx ==  2) ? { 3'h0, addr_block[11:7]} :            //ADDR[2]
                           (        (tx_idx ==  3) ? { addr_block[6:0], addr_page[8] } :    //ADDR[1]
                            (       (tx_idx ==  4) ? { addr_page[7:0] } :                   //ADDR[0]
                             (      (tx_idx ==  5) ? { latency[31:24] } :
                              (     (tx_idx ==  6) ? { latency[23:16] } :
                               (    (tx_idx ==  7) ? { latency[15: 8] } :
                                (   (tx_idx ==  8) ? { latency[ 7: 0] } :
                                 (  (tx_idx ==  9) ? { badbits_wire[31:24] } :
                                  ( (tx_idx == 10) ? { badbits_wire[23:16] } :
                                    (tx_idx == 11) ? { badbits_wire[15: 8] } :
                                    (tx_idx == 12) ? { badbits_wire[ 7: 0] } :
                                                     { 8'hEE }
                                  )
                                 )
                                )
                               )
                              )
                             )
                            )
                           )
                          )
                         )
                        );    
    ```

