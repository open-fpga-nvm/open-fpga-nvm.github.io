---
layout: post
title:  "How-to"
date:   2015-06-29 12:10:00
categories: open-fpga-nvm manual
permalink: /how-to/
---

# How to use the repository code

* **Environment is base on _Windows 7_.**

## FPGA Code
1. Required Tools
    - Xilinx ISE: For using with Nexys 3 board. In our case, we've developed with WebPACK edition.
    - Digilent Adept: For downloading Verilog compiled(synthesized) binary image to _Nexys 3_ board.

1. Connection of the _Nexys 3_ board
    - Connect both of USB connectors to PC.
        - JTAG download port
        - USB-to-Serial port
    - Note the COM port number of USB-to-Serial from 'Device Manager' of your system.
    
1. Usage
    1. Launch the _Project Navigator_ tool.
	2. Create a project for _Nexys 3_ board configuration.
        ![](/resource/image/fpga-how-project-setting.png)
	3. Add Verilog source files(.v) into the project.
	4. Execute _Generate Program file_ in 'Design' window.
	5. Download Program file (.bit) to Nexys 3 board by using Digilent Adept.
        - 7-segment will show the number after downloading.
    6. Use the host controller application.


## Controller Code
1. Required Tools
    - Python 2.7.x: Python interpreter
    - pySerial: Serial port library for Python
	- tk: tk library is already included in Python 2.7, used for simple GUI

1. Usage
    1. Edit **ofserial.cfg** for serial COM port number and script file name.
    
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
		
    1. GUI Usage
    ![](/resource/image/fpga-how-host-control.png)
        - **COM PORT**: COM port selection and OPEN/CLOSE the port. If port is available, it is automatically opened on launch.
        - **LOG**: Log window. After running the full script, [Finish] is shown here. This is different from the output log file.
        - **FILES**: (not yet implemented) Script file selection.
        - **CMDS**: (not yet implemented) Script editor.
        - **CONTROL**
            - START: Start the script.
            - STOP: (not working yet) Terminate the current running.
            - TEST: (just testing button for GUI development)
        
	1. Tips
        - There is also command line based script file _ofserial.py_ which we used in initial stage of development.
        - For debugging for serial communication, we used a serial port monitoring tool [_Realterm_](http://realterm.sourceforge.net) which is also an open sourced project.
    
1. Script file grammar
    - Every dictionary in **actions** array are executed and result are saved to log files.
    - **'NAME'**: _Log file name_ for saving capture result
    - **'CMDS'**: Series of actions for setting the configuration or doing action

        | Type         | Description      | Parameters |
        | ------------ | ---------------- | ---------- |
        | **uADDR()**  | Address Range    | (_Start_Address_, _End_Address_) <br> NAND: Block Address <br> MRAM: Byte Address|
        | **uOPER()**  | Operation Filter | _oWR_: Write <br> _oRD_: Read <br> _oER_:Erase <br> _oRST_:Reset |
        | **uLOOP()**  | Loop Count       | NAND: Block Address |
        | **uLOG()**   | Log Frequency    | How frequently FPGA will return result <br> 0=return every result |
        | **uNAND()**  | NAND Options     | _pLSB/pCSB/pMSB_: Filter page type for doing operations <br> _ptrn_usrX_: True=(user data pattern), False=(column address as data pattern) <br> _ptrn_usr0_ is applied to even page, and _ptrn_usr1_ is applied to odd page |
        | **uSTART()** | Start Testing    | Start the testing with above settings |


##Log Parser
1. Required Tools
    - Python 2.7.x: Python interpreter
1. Usage
    1. Run the parser for log file(s).
    
        ```
        python log_parser.py log_file.bin
        ```
			
	2. We also attached a sample batch file(parse.bat) for windows. You can easily parse the files by dragging logfiles onto this batch file.
	    - Edit the path in batchfile before using it.
        
            ```
            C:\Python27\python.exe D:\MyProject\log_parse.py %*
            ```
	
    3. Log file
        - After parsing, log file is saved as _.csv_ format.
        - Basically, we used the _Microsoft Excel_ for further analysis of parsed data.
				
				
				