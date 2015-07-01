---
layout: post
title:  "How-to"
date:   2015-06-29 12:10:00
categories: open-fpga-nvm manual
permalink: /how-to/
---

# How to use the repository code

* **Commandline commands are base on Windows environment.**

## FPGA Code
1. Required Tools
    - Xilinx ISE: For using with Nexys 3 board. In our case, we install with webpack edition.
    - Digilent Adept: For downloading Verilog compiled(synthesized) binary image to Nexys 3 board

1. Usage
    1. Open _Project Navigator_
	2. Create a project with Nexys 3 configuration
	3. Add verilog (.v) files to project
	4. Build Program file
	5. Download Program file (.bit) to Nexys 3 board by using Digilent Adept
    6. Use the host controller application


## Controller Code
1. Required Tools
    - Python 2.7.x: Python interpreter
    - pySerial: Serial port library for Python
	- tk: tk library is already included in Python 2.7, used for simple GUI

1. Usage
    1. Edit **ofserial.cfg** for serial port# and script file name.
    
        ```python
        global_config = {
            'COM_PORT' : 'COM5',
            'CMD_FILE' : 'POWER_ER.act'
        }
        ```
		   
	1. Edit script file for operation
           
        ```python
        actions = [
            {
                'NAME' : 'cap_0E-ALL',
                'CMDS' : [
                            uADDR(0x0F8,0x0FF),
                            uOPER(oWR=False, oRD=False, oER=True, oRST=True),
                            uLOOP(1),
                            uLOG(0),
                            uNAND(pLSB=True, pCSB=True, pMSB=True),
                            uSTART() ]
            },
            {
                'NAME' : 'cap_0R-FF-ALL',
                'CMDS' : [
                            uADDR(0x0F8,0x0FF),
                            uOPER(oWR=False, oRD=True, oER=False, oRST=True),
                            uLOOP(1),
                            uLOG(0),
                            uNAND(pLSB=True, pCSB=True, pMSB=True, ptrn_usr0=1, ptrn_usr1=1, ptrn0=0xFF, ptrn1=0xFF),
                            uSTART() ]
            },
        ]
        ```
		
	1. Run - GUI version
    
        ```
	    python ofserial_tk.py
        ```
		
	1. There is also command line based source file _ofserial.py_
    
1. Script file grammar
    - 'NAME': Log file name for capture result
    - 'CMDS': Series of actions for setting configuration and doing action

        | Type   | Description      | Parameters |
        | ------ | ---------------- | ---------- |
        | uADDR  | Address Range    | NAND: Block Address, MRAM: Byte Address, Start Address and End Address |
        | uOPER  | Operation Filter | oWR: Write, oRD: Read, oER:Erase, oRST:Reset |
        | uLOOP  | Loop Count       | NAND: Block Address |
        | uLOG   | Log Frequency    | NAND: Block Address |
        | uNAND  | NAND Options     | NAND: Block Address |
        | uSTART | Start Testing    | Start the testing with above settings |


##Log Parser
1. Required Tools
    - Python 2.7.x: Python interpreter
1. Usage
    1. run
    
        ```
        python log_parser.py log_file.bin
        ```
			
	2. We also attached a sample batch file(parse.bat) for windows. You can easily parse the files by dragging logfiles onto this batch file.
	    - Edit the path in batchfile before using it.
        
            ```
            C:\Python27\python.exe D:\MyProject\log_parse.py %*
            ```
				
				
				
				