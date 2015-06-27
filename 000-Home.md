---
layout: post
title:  "Home"
date:   2015-06-26 17:10:00
categories: open-fpga-nvm manual
permalink: /home/
---

#Open-FPGA-NVM
Welcome to the open-fpga-nvm wiki! 

To evaluate the impact of the emerging nonvolatile memory technologies in applications or in system structure, the imperative requirement is to obtain the empirical parametric data and its dependencies. This vast inquiry of NVM into a number of materials and technologies requires a characteristic scheme with wide electric range, with flexible parameter regulation and often with packed fan-out control; whereas, as a new technology this information is not fully available in product specification. Researcher spends protracted terms and funds to build this kind of scheme only for each particular test case on specific material, which is not trivial anymore.  Here we have developed, for the first time of our knowledge, a FPGA based hardware prototype in order to characterize various critical parameters of different materials in one single set up.

This wiki is full step by step tour, so that one can easily mimic this to build their own FPGA scheme, as a memory-controller either to characterize NVM or build any new NVM-system. This will also help in directing many FPGA based IC test and building any FPGA based prototype.

If you feel that **Open-FPGA-NVM** is supportive to your own work, please refer our [NVM-FPGA]() paper. 

##Overview
Open-FPGA-NVM is a FPGA based hardware prototype as a NVM controller, designed to serve the purpose to collect Empirical Data of new generation memory chip such as Everspin’s MRAM, Numonyx PCM, Micron’s Nand-Flash and so on. This wiki is for a complete navigated guidance, from set up to data-collection. This precedent work is developing under Computer Architecture Memory system LAB (CAMELAB) of Dr. Jung at University of Texas at Dallas to establish a comprehensive scheme to test, characterize and evaluate the emerging memory technologies, which will serve in anticipated research to build model as well as system in order to leverage the advantages of different memory technologies for particular or universal application.
##Objective
This open scheme has been developed to generate exhaustive, empirical data of emerging non-volatile memory in a configured, programmable FPGA based hardware prototype in order to serve the area in research on memories especially non-volatile type. This memory-characterizing platform is able to provide the prescribed archive to extract the intrinsic **parameters** of various Nonvolatile memories; Such as:
+ [Latency](Appendix)
+ [Power Consumption](Appendix)
+ [Retention time](Appendix)
+ [Non-Volatility](Appendix)
+ [Endurance](Appendix)
     

##Features 
CAMELAB Memory Empirical Data Generator **NVM-CHARADE** is targeting to achieve the features of 

1. MRAM, PCM and Nand-flash-TLC Characterization
1. Option to test access speed, non-volatility, standby or active power, retention time and endurance.
1. Synchronous, single, burst or chunk DUT access with adjustable read or write latency @ 500MHz clock speed.
1. Able to Process 40 high speed I/O control to the DUT
1. 2nS precision in timing measurement
1. 10 mWatt on 1ms time elapse precision in power measurement
1. Full access to Memory-DUT, 100% place and pattern checkable 
1. Test time: 1K data /sec
1. Controller size <10K gates
1. 7-segment LED displaying test status
1. Auto characteristic plot extraction according to user’s instruction
1. Hardware Prototype: Configurable controller design in Verilog HDL, easily reconfigurable for system level analysis or mimic any issues
1. Auto Latency detection
1. Auto power measurement
1. Operable in two practical mode

  * User interactive mode 
  * Speed-test Mode 

## Project Achievement
* Emerging NVM quality and performance verification
* Platform for NVM research support
* Academic platform in Memory, Memory Hierarchy, Computer Architecture, FPGA, System board design, VLSI-design etc.
* Academic platform in programming language application: C, VHDL, VERILOG etc 
* Academic platform in Hardware Software co-design
* Hardware Support in FPGA
* Hardware Support in PCB
* Application/Tool Support: PCB-Artist, XIINX-ISE, Modelsim
* IC Test Support
* Memory/NVM test Support 
* Build your own SoC(for future project) 
 
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