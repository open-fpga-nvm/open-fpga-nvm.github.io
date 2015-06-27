---
layout: post
title:  "FPGA Configuration"
date:   2015-06-26 17:18:00
categories: open-fpga-nvm manual
permalink: /fpga-configuration/
---

#FPGA

_FPGA Based Hardware Prototype: NVM Controller ! ! !_

Our specific goal is to design a NVM controller with FPGA. In this section we will learn to deal with FPGA underlining our goal. Here are the main topics what we are covering in this section:

- **Deal with FPGA:** Generic description on FPGA and the board is exploited. 
- **NVM-Controller Requirement:** Briefly description on system requirement analysis for the board we have chosen, hardware design requirement for the specific FPGA that comes with the board. 
- **NVM-Controller Design:** Procedure for configuring FPGA for our design with emphasis on system design and architecture.   


For Hardware-set-up tasks and connection go to the [Hardware Setup](Setup) section, and for evaluation of the system performance go to the [NVM Test and Result](NVM Test Result) section.


##Deal with FPGA

Before Start with our NVM Controller Design, we will go through a smart overview on FPGA primitive. In this part, we will get a comprehensive perception on FPGA. This part is for newcomer in FPGA-field. You may like to skip this part if you are previously experienced.

+ **Pre-requisite**
  - Digital Design
  - Hardware Description Language
+ **Basic Blocks**
+ **FPGA-Synthesisable Code**
+ **Generic Synthesis Step**
+ **Spartan6**
+ **FPGA Development Board : Nexys-3**

The Nexys3 is a ready-to-use digital circuit development platform based on the Xilinx Spartan-6 LX16 FPGA.  In addition it also have relevant peripherals including 32Mbytes Phase Change nonvolatile memory, a 10/100 Ethernet PHY, 16Mbytes of Cellular RAM, **USB-UART**, USB host port for mice and keyboards, and **high-speed expansion connector**, **4-digit seven-segment display**, **100MHz CMOS oscillator**, **Adept USB port**, power jacks and so on; but only bolded ones are used in our particular case. Nexys-3 board was exploited in order to design the distinct memory controller for the purpose to extract the device characteristic in an optimized efficient way. For more information on nexys3 please visit: http://www.digilentinc.com/Data/Products/NEXYS3/
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


______________________________________________________________________________________________

______________________________________________________________________________________________

#Helpful Tools and Tutorials

**Download**

1. [Install Window-7]()
1. [Install Modelsim]()
1. [Install ISE]()
1. Verilog files
  -  [MRAM]()
  -  [TLC_Nand]()

**Tutorials**

1. [FPGA Basic]()
1. [Verilog](http://vol.verilog.com/VOL/main.htm)
1. [Memory Controller Design](http://www.xilinx.com/support/documentation/sw_manuals/xilinx13_1/ug818_ddr2_mem_tutorial.pdf)
1. [SPARTAN-6](http://www.xilinx.com/support/documentation/data_sheets/ds160.pdf)
1. [Nexys-3](http://www.digilentinc.com/Products/Detail.cfm?NavPath=2,400,897&Prod=NEXYS3&CFID=10336466&CFTOKEN=3e92e68541112146-1076C0E1-5056-0201-02AC30B00D2F84F6)
1. [Using ISE ]()


#Table of contents
* [Home](Home)
* [Scheme Structure](Structure)
 - [FPGA Based NVM Controller](FPGA Configuration)
 - [NVM Daughter Board in PCB](PCB Design)
 - [Software Development for Application Host](Parse Writing) 
*  [Hardware Setup](Setup)
 - [Apparatus](Setup)
 - [Scheme](Structure)
 - [Prerequisite](Setup)
 - [Step by Step Set up](Setup)
 - [Test Procedure](NVM Test Result)
* [NVM Test and Result](NVM Test Result) 
* [Tutorial](Tutorial)
* [Resources](Resources)
* [Appendix](Appendix)
* [Contact](Contact)
* [Disclaimer](Disclaimer)