---
layout: post
title:  "FPGA Configuration"
date:   2015-06-29 12:10:00
categories: open-fpga-nvm manual
permalink: /fpga-config/
---


#FPGA Configuration

**@Gieseo: please complete the blank subsections or remove them as per your judgment**


##FPGA Development Board: Nexys 3

The Nexys 3 is a digital circuit development platform based on the Xilinx Spartan-6 LX16 FPGA. It includes a wide range of required peripherals - 10/100 Ethernet connection, 16MB of embedded RAM, USB-UART, USB host port for mice and keyboards, high-speed expansion connector, 4-digit seven-segment display, 100MHz CMOS oscillator, and and 32MB PCM memory. Nexys-3 board is utilized in order to design our  NVM controller for extracting performance characteristics in an optimized and efficient way. For more information on  the Nexys 3 product please visit: http://www.digilentinc.com/Data/Products/NEXYS3/

A General purpose Computer with keyboard, mouse and monitor is used for user application to serve the purpose of both configuring FPGA and for providing the test instruction for the memory device under test and also collecting all the DUT characteristic data to save into it. A total customized host application has been build into it so that the programmable directed data can be collected depending on the DUT type and test category.
Customized Daughter board has been designed depending on the memory type so that it can be accordingly connected to the memory controller, built in Spartan-6 FPGA through nexys-3 development board’s high-speed expansion connector. 

1. [Manual](http://www.digilentinc.com/Data/Products/NEXYS3/Nexys3_rm_V2.pdf)
1. [Schematic](http://www.digilentinc.com/Data/Products/NEXYS3/NEXYS3_sch.pdf)


##NVM-Controller Requirement:

To decide on FPGA and the board have to be done according to the design/system requirement cost effectively.

**System Requirement**: Determined by board and FPGA

1. One single Controller that may control all (at least): MRAM, TLC-Nand, PCM etc.
1. Number of I/O control signals = 40
1. Vcc range 1.5V-->3.3V
1. Oscillator range 500M
1. Variable system clock requirement: May be
1. May provide the Maximum current consumption from board = ~300mA
1. Separate Vdd and Vddq requirement: May be
1. I/O speed ~500MHz
1. I/O Current density not significant
1. I/O static-shock protection requirement: no
1. Flexible Debug Facility: should

**Controller Design Requirement**: Depends only on FPGA

1. Number of gates need to design this kind of controller ~5K
1. Number of SRAM ~2K
1. Number of Register ~2K
1. Clock management availability: Required 

______________________________________________________________________________________________

______________________________________________________________________________________________


#NVM Controller Design

##**Design Primitive**

   - **Function**
   - **Black Box**
   - **Basic Blocks**

##**Board Deployment**
   
   - **Power Up**
   - **UART**
   - **Clocking**
   - **Spartan-6**  
      * Memory controller State M/C
      * Queue Register
      * Debug controller 
   - **I/O Assignment**
   - **Debug Auxiliaries**

###MRAM Controller Mapping
 
- Memory Map
- Instruction Set
- Time Control Signal
- Operation Mode
- Source Code

###TLC-Nand Controller Mapping
 
- Memory Map
- Instruction Set
- Time Control Signal
- Operation Mode
- Source Code


###**Configuration with ISE**
- **ISE OS requirement:** windows7, Linux. [(Problems with Windows8)](http://www.eevblog.com/forum/microcontrollers/guide-getting-xilinx-ise-to-work-with-windows-8-64-bit/msg479087/?PHPSESSID=d60f5ba67c76d757fe50e0f103c42e27#msg479087), [(Problems with Window-server)]().
- **Download ISE:**[(Download ISE)]
- **Open ISE:** 

  + Start Project
  + Add Source code
  + I/O implementation
  + Generate Programming File
  + Configure Target Device
  + Analyze Design



Hardware set-up and connection details are provided in [Hardware Implementation](Setup). In addition, for sample evaluation of NVM products with the Open-NVM platform, please refer to [NVM Test and Result](NVM Test Result) section.