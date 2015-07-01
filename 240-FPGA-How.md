---
layout: post
title:  "How-to"
date:   2015-06-29 12:10:00
categories: open-fpga-nvm manual
permalink: /how-to/
---

# How to use the repository code

## FPGA Code
1. Required Tools
    - Xilinx ISE: For using with Nexys 3 board. In our case, we install with webpack edition.
    - Digilent Adept: For downloading compiled image to Nexys 3 board

1. Usage
    1. Open _Project Navigator_
	2. Create a project with Nexys 3 configuration
	3. Add verilog (.v) files to project
	4. Build Program file
	5. Download Program file (.bit) to Nexys 3 board by using Digilent Adept


## Controller Code
1. Required Tools
    - Python 2.7.x: Python interpreter
    - pySerial: python serial library
1. Usage
    1. edit _ofserial.cfg_ for serial port and script file
	
	        global_config = {
                'COM_PORT' : 'COM5',
                'CMD_FILE' : 'POWER_ER.act'
            }
		
	1. run
	
	        python ofserial_tk.py
		
	1. there is also command line based source file _ofserial.py_

1. Script File

##Log Parser
1. Required Tools
    - Python 2.7.x: Python interpreter
1. Usage
    1. run
	
	        python log_parser.py log_file.bin
			
	2. We also attached a sample batch file(parse.bat) for windows. You can easily parse the files by dragging logfiles onto this batch file.
	    - Edit the path in batchfile before using it.
		
                c:\Python27\python.exe d:\MyProject\log_parse.py %*
				
				
				
				