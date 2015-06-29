---
layout: post
title:  "Setup Manual"
date:   2015-06-29 12:10:00
categories: open-fpga-nvm manual
permalink: /setup/
---


**@Gieseo: This section should include the step by step guideline instructing interested user how to recreate the Open-NVM platform.**


## Apparatus
The whole scheme has been evolved with the main apparatus of: 
 
1. FPGA Development Boards: Configured for NVM Memory Controller.  
1. Daughter Board: PCB to Connect NVM with Controller.   
1. PC/Laptop: i) For Configuring FPGA ii) Providing Host-Apps for User-interactive-mode.   
Not to mention, we will also need:
* Accessories (PC-peripherrals)
* Connectors (USB, VHDCI etc)

##Scheme Development
Before we go through hardware set-up & steps, it is advisable to understand the whole scheme first.
Please go through scheme development page first for better understanding of the scheme.  

- **FPGA Based NVM Controller**

The main object of this project is to design a NVM-controller for Emerging NVM, such as: MRAM, Nand-Flash, PCM; that can extract all the characteristics of NVM those determine their performance and quality, and then provide a user-friendly-testablle platform. The whole scheme is developed mainly by designing one universal NVM controller by configuring same FPGA which serve this purpose. Please go thorough next link for detail visualization of this FPGA based memory controller design.  
* [FPGA Based NVM Controller](FPGA Configuration)

- **NVM Daughter Board in PCB**

Custom Printed Circuit Daughter Boards for proper connection with memory controller have been made for each of NVM type. You may Go thorough next link if you have interest in PCB design or required for your own PCB design.  
* [NVM Daughter Board in PCB](PCB Design)

- **Software Development for Application Host**
.... Under Development .....   
* [Software Development for Application Host](Parse Writing) 

##Prerequisite
1. Kernel for required Tools: [Window7]()
1. Download Simulator: [Modelsim]()
1. Download Synthesize tool: [ISE]()
1. Hardware Synthesis Language: [Verilog]()

##Set-up and Steps

1. Power up
1. FPGA Configuration
1. Test FPGA
1. Connect FPGA with NVM-daughter-board
1. Run Test
1. Collect Data
 
 
# Experiment
1. Button A = reset
1. Button B = pause

# Serial communication
    * MRAM
    * TLC-NAND

#Table of contents
* Home
* [Scheme Structure](Structure)
 - [FPGA Based NVM Controller](FPGA Configuration)
 - [NVM Daughter Board in PCB](PCB Design)
 - [Software Development for Application Host](Parse Writing) 
* [Hardware Setup](Setup)
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