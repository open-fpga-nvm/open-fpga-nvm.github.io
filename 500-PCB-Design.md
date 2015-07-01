---
layout: post
title:  "PCB Design"
date:   2015-06-29 12:10:00
categories: open-fpga-nvm manual
permalink: /pcb-design/
---


##NVM Daughter Board

The daughter board in our Open-NVM is a custom printed circuit board (PCB) designed to work as a pedestal for the NVM chip under test, and provide the required connectivity between the chip and the FPGA board. 
This short guidance will direct you from selecting the right vendor for PCB to assembling it. In this case, the purpose of our PCB is to connect NVM  to memory controller development board. 

If you are using same development board and NVM like ours:

* Nexys-3 FPGA development board to build the memory controller and its VHDCI expansion for connecting NVM  
* [MRAM-MR2A16A](http://www.everspin.com/family/mr2a16a), TLC-NandFlash-MT29F64G08EBAA as for NVM
 
You may directly use our [gerber files](https://github.com/lubmn/PCB/tree/master/design) and components for PCB order and assembly. And when you do so, it is assumed that you have clear understanding about purpose and type of each I/O, PCB Layout, components etc. Either-way steps and procedures are common.  

#Steps and Procedures
This demonstration is for the PCB-beginners, who have PCB-basics and complete understanding of system-schematic; If you are not a beginner you may like to skip this part and directly

1. Download PCB tool
1. Select components
1. Produce PCB and
1. Assemble it.
	
The whole design cycle may take as long as couple of weeks or as short as couple of days depending on designer's expert level and manufacturer's turnaround time plus shipping and handling delay.....  

For beginners like me I got to go through following questions, procedures, steps and have learnt from my own mistake.  

##1. Why we need PCB 
Well, our purpose is simply to connect the NVM to the controller, simple breadboard could serve the purpose. And you may use breadboard or universal board, but it will make the connections, debug process complex and harden more with number of I/O's and density of the pin. For example, think about you are connecting 8 MR2A16A MRAMs, which means 8x40=320 I/O's. In our case, we are using VHDCI and SATA connectors which is almost impossible to connect in regular breadboard, whereas PCB has made our life simpler and easier. 
 
##2. PCB Manufacturer to choose
In case you are not making your own PCB, you should decide on the PCB manufacturing company. Here I consider four main 'P's i) Precision, ii) Pace, ii) Pricing and iii)Production Delay. For example, we are using VHDCI connectors of 0.8 mm pitch, our circuit may run at 500 MHz, therefore who can serve these with minimum pricing and considerable turnaround time. As a beginner I also wanted to work with a company who can provide high level of customer support with quick response. We go with [Advance Circuits](http://www.4pcb.com), I recommend them for their unbroken assistance; and guess what, we have 1p0 success. One more thing I like to mention, if you like to get rid of shipping and handling cost, you may like to find some company in town. And I would like to try to manufacture it our own, and will give you update later on if we get success.


##3. Choose the right PCB Tools
For chosing PCB tools you may look for 
  
 * Required PCB laout-precision and speed compatibility 
 * Easy LVS and DRC debug and fixing ability 
 * Footprint wizard availability 
 * Efficient Auto-routing and Autoplacement  
 * Easy to remember hotkeys 
 * Smooth learning curve
 * Manageable libraries and files 
 * kernel compatibility  
 * 3D view etc, and last but not the least 
 * Pricing  

The most popular today's PCB layout tools are Cadence Allegro, Mentor Graphics Pads,  Altium designer, Eagle etc. While only Eagle is Mac-compitible; only Allegro is guarantied for design of 10GHz range. Each may have its own unique advantages and limitations. But all of them are kind of pricy for a student like me. Though they are advanced enough to design any kind of board, it doesn’t mean you should chose that for a beginner project. Choosing the right tool for the layout should be decided at the very beginning. I got to chose PCB-Artist the one offered by the same vendor we have chosen ['Advance Circuits'](http://www.4pcb.com) in order to make order placement straight-forward and this do meet all our criteria like precision and speed. And top of everything it is free.


##4. Select Components
Before designing the PCB you have to decide on your components, because that's the particular footprint You will be drawing. Some are pretty specific you may not have much option to chose from. While same kind of components may be offered from various vendors with different footprint. Decision should have been done depending on 
 * Price
 * Footprint
 * Electrical property
 * Minimum quantity to order and number of quantity you like to have
 
There are various reliable websites you can search and order your components, like [Digikey](http://www.digikey.com/), [Amazon](http://www.amazon.com/). You may like to order in bunches for common components like pin-headers or sockets, while any particular pricy one should be ordered the amount you need. Sometimes to get specific research components, could be challenging, as they may not be in production or distributor would only agree to supply in gigantic amount. We get little dilemma to find out Micron TLC-NandFlash for small-quantity of 20pcs; whereas distributor don't agree to sell or send even samples, if it is less than 2000 pcs. I like to thank [America II Electronics](http://www.americaii.com) to help us for solving this issue by supplying 20 pcs of TLC-NandFlash. You should prepare complete [_BOM_](Appendix) at this point. 

In our case, for each TLC-NandFlash PCB we required

 * One [VHDCI-68 connector](http://www.digikey.com/product-detail/en/0714300008/WM7303-ND/572157) in order to connect our FPGA development board
 * One [SATA connector](http://www.digikey.com/product-detail/en/0877030001/WM19111-ND/1499168) to connect our power measurement board
 * Two 24-0.1"pitch DIP socket strips(breakable) to plug in 48 pin DIP sockets for TLC-Nand
 * Bunches of pin headers (>50 counts) for alternate line option and debug/probing.   
We also used [VHDCI cable connector](https://www.digilentinc.com/Products/Catalog.cfm?NavPath=2,393&Cat=3#VHDCI-M2M-CABLE) (male to male type, as both of our development board and PCB has male type VHDCI), and [header-jumper](http://www.amazon.com/2-54mm-Standard-Circuit-Shunts-Jumper/dp/B00HR8DGZO) for line selection.
  
##5. Produce PCB

As you have already known the system you are building, and have chosen your components, now you are ready to layout the PCB. For successful PCB production and avoiding trial and error repetition, if you are building the system for the first time, either you should develop your system and test it using breadboard, or build and test it with schematic. All the renowned PCB tools offer schematic along with it but not testability. You may use Verilog-A/VHDL-AMS to perform any system level testing, incase you are building a complicated, zero tolerance and 1st part success; but that is an another story and has not been followed here, as ours is a simple straightforward case. We have tested partly with breadboard and layout ours using PCB Artist. As an advanced designer, you may directly layout your PCB without component and schematic, still here I am including the steps I have followed (but not detail procedure of PCB-artist-tool: go through PCB-artist-help wizard for that) which is kind of typical and some additional tips those were taken in account to:

1. [Know your tools](http://www.4pcb.com/pcb-software-tips-tools.html): If you are a first time PCB designer you go through PCB artist's [video tutorial](http://www.4pcb.com/pcb-software-tips-tools.html). You should be familiar with the file-structure, location, hot keys, terms, rules, co-ordinate-system, grids etc. you may like to go through once 'PCB-Artist Help->Contents', when you open PCB-Artist first. 
  
1. [Create Component:](http://www.4pcb.com/downloads/pcbartist/PCBArtistLibraryTutorial.pdf) For this, three basic steps you will do: 
  1.  Create schematic symbol: for using it in your PCB schematic, 
  1.  Create PCB symbol: This is the physical footprint your are laying-out that will be used in you PCB, and 
  1.  Create Component: for making consistency between your schematic and layout.                                
  There are thousands of components available and ready to use from millions/billions of components in the market. Don't spend any time to look for available library to your tool. Rather build your own, that will take much more shorter time than you could imagine; once you are familiar with the tools and PCB-basic, it won't take more than 10-20 mins with a regular footprint one. But some tricky one like [VHDCI-68](http://www.molex.com/pdm_docs/sd/714300008_sd.pdf) could take longer time. Whatever the time it may take, you have to have 100% precisely-accurate footprint period. Your selected-component-vendor is supposed to provide every information for the footprint, like in our case we use [VHDCI](http://www.molex.com/pdm_docs/sd/714300008_sd.pdf), and [SATA](http://www.molex.com/pdm_docs/sd/877030001_sd.pdf) connector.

  For creating footprint/PCB Symbol here what I will recommend:
 - Take a look at the physical Component, this 3D understanding will really help you to realize every perspective of the [_footprint_](Appendix). 
 - Always keep record your helpful/required dimension using text(using [_documentation layer_](Appendix) may be) in your component's footprint file; you may need to check it later. 
 - It is handy to put any useful information like Manufacture# in [_silkscreen_](Appendix). 
 - To make hole, I used through-hole pads with hole size greater than pad size, which will show warning while [_DRC_](Appendix)-checking but save money and time for assemble.
 - When you reach to the [_critical dimensional range_](Appendix) of your manufacture, for assuring higher possibility of success you may need to take special modification which may result in conflicting [_DRC_](Appendix), yet you know will cause no error. 

1. [PCB Schematic](http://www.4pcb.com/pcb-software-tips-tools.html): If you are a pro, you may like to avoid creating schematic for a trivial case and can directly layout PCB. I highly recommend to create Schematic, review once more your system, go through specification of each part you are using, know about any development board you are connecting, know about your power supply, consider rating of each pin of every component etc, consider the speed that each pin may get or provide; you should also know if you have any [_static-sensitive_](Appendix) pin in your electronic component, calculate values for any passive elements like capacitor/resistor/inductor if you may require. For e.g. for our TLC-NandFlash we need pull up resistors for ready/busy pin. I have simply chosen its value of 2.2 K-ohm, from Resistor-Current curve provided in the product specification, so that current to that node would remain less than 2mA and assuming Cout<10pF which means RC-time constant is faster than 22ns. I found the next link good enough for having detail conception of [Pull-Up-Resistor Calculation](http://www.edn.com/design/analog/4371297/Design-calculations-for-robust-I2C-communications). 
 
1. [PCB Layout](http://www.4pcb.com/pcb-software-tips-tools.html): So this is the main thing for what we are talking all these. Procedures and steps are mentioned well enough in [advanced circuit's web](http://www.4pcb.com/pcb-software-tips-tools.html). Here I will mention the art and agony of this:  

    **Art**
	
    * Build it for minimum cost with optimum requirements
    * The art of this is to build it for minimum area.
    * Start placing with main components, i.e. mostly your traces would run between.
    * If the connectors or headers possess symmetric pin-out, place the main component that would be connected to it symmetric with respect to it.
    * Calculate your trace width for power bus for maximum possible current. The beautiful art is, current cannot escape through the shortest resistive path but divide into all possible path according to their conductance. Its important you know the worst current density of your trace. 
    * Start with laying-out power and ground trace.
    * Put all the info for PCB-designer (i.e. you) to review with document layer.
    * Put all the info for System-builder or PCB-user to review with silk-screen Layer.
	
    **Agony**
	
    * Auto-placement and Auto-routing may not do the art of layout. 
    * PCB-Artist auto-routes failed for highly dense footprints like 'VHDCI'.   
    * Never put Text with metal (when you have option).
    * No point to put silk-screen text beneath the component.
    * Don't skip drawing ['_keep-out_'](Appendix) e.g. your components body that are touching PCB; and then check manually, if it has anything on its way. PCB Artist don't have the brain yet to check keep-out.
    * Don't forget to put assembling-holes of your component.   
 
1. [Placing Order](http://www.4pcb.com/media/basic-design-requirement-order-process.pdf): After you are done with your layout, when place the order by 'order now' button at menu-bar, it will automatically check DRC, LVS and produce gerber.  Always remember LVS, DRC are formal procedure for creating gerber, and definitely help you for debug and make success, but they are not any substitute of your intellectual visualization or depth in knowledge about your circuit.  

##Assemble
Place the components onto right position/holes, and solder it!

##NVM-PCB FootPrints, Files and Figures
* NVM Spec
  + [MRAM](http://www.everspin.com/family/mr2a16a)
  + [TLC-Nand](http://www.micron.com/parts/nand-flash/mass-storage/mt29f64g08ebaaawp?pc={9E356F28-3F5E-4FF7-A8D5-657A26EC58BE})
  + [PCM](http://webcache.googleusercontent.com/search?q=cache:GwWMtaLG7oMJ:https://www.micron.com/~/media/Documents/Products/Data%2520Sheet/PCM/p8p_parallel_pcm_ds.pdf+&cd=3&hl=en&ct=clnk&gl=us&client=safari)
* PCB Component Footprints 
  + [DIP-Socket](http://www.precidip.com/eMagStudio/2012-12-12/DIL_SIL_TO_SOCKETS/index.html#/1/)
  + [Pin Header](http://www.digikey.com/product-detail/en/350-10-132-00-001101/1212-1139-ND/3757389)
  + [VHDCI Connectors](http://www.molex.com/pdm_docs/sd/714300008_sd.pdf)
  + [SATA Connectors](http://www.molex.com/pdm_docs/sd/877030001_sd.pdf)
* Gerber Files
  + [MRAM](https://github.com/lubmn/PCB/tree/master/design)
  + [TLC-Nand](https://github.com/lubmn/PCB/tree/master/design)
  + [PCM]()
* NVM : FPGA-board-VHDCI connection
  + [MRAM](https://github.com/lubmn/PCB/blob/master/pic/MRAM_VHDCI_conn.png)
  + [TLC-Nand](hhttps://github.com/lubmn/PCB/blob/master/pic/tlcNand_VHDCI_conn.png)
  + [PCM]()
  
##Helpful Tools and Tutorials
* PCB Tools
  + [Install PCB Artist](http://www.4pcb.com/free-pcb-layout-software/?gclid=COGniuG9j8UCFQopaQodQUgAnw)
  + [Link to Eagle](http://www.cadsoftusa.com/download-eagle/)
  + [Link to Allegro](http://www.cadence.com/products/pcb/pages/downloads.aspx)

* Helpful Tutorials for PCB
  + [PCB basic](http://en.wikipedia.org/wiki/Printed_circuit_board)
  + [How to build your board schematic](http://www.frontdoor.biz/HowToPCB/HowToPCB-Schematics.html)
  + [Best Practices for PCB](http://www.edn.com/electronics-blogs/all-aboard-/4429390/Ten-best-practices-of-PCB-design)
  + [David's](http://en.wikipedia.org/wiki/David_L._Jones)--> [PCB tutorial](http://server.ibfriedrich.com/wiki/ibfwikien/images/d/da/PCB_Layout_Tutorial_e.pdf)

* PCB Artist Tutorials
  + [Component Creation with PCB Artist](http://www.4pcb.com/downloads/pcbartist/PCBArtistLibraryTutorial.pdf)
  + [Building Schematic for PCB with PCB Artist](http://www.4pcb.com/media/PCBArtistLibraryTutorial.pdf)
  + [PCB Layout with PCB Artist](http://www.4pcb.com/media/PCBArtistLibraryTutorial.pdf)
  + [Placing order with PCB Artist](http://www.4pcb.com/media/basic-design-requirement-order-process.pdf)

* Component Search web
  + [America II Electronics](http://www.americaii.com) 
  + [Digikey](http://www.digikey.com/) 
  + [Amazon](http://www.amazon.com/) 
  + [Micron-distributors](http://www.micron.com/support/how-to-buy/authorized-distributors) 
  + [Everspin-distributors](http://www.everspin.com/sales#tab_dis-na)
 
* Calculators for PCB design
  + [Trace Width](http://www.4pcb.com/trace-width-calculator.html)
  + [Unit Converters](http://www.4pcb.com/metric-converter.html)
  + [Other](http://daycounter.com/Calculators/)

* Manufacture your own PCB
  + [FAB your own PCB by pcbfx ](http://www.pcbfx.com)
  + [Print Circuit by Voltera: future on desk PCB-FAB](http://www.voltera.io)
 

##PCB Drawing
  + MRAM![](https://raw.githubusercontent.com/lubmn/PCB/master/pic/pcb_mram.png)
  + TLC-Nand![](https://raw.githubusercontent.com/lubmn/PCB/master/pic/pcb_tlcNand.png)
  + PCM![]()

##My Design CONS
Though the daughter board design meet the purpose, the best design practice may not be followed, as we are far away from critical condition. Still I like to mention it for future improvement:

###Schematic Cons

###Layout Cons
 
Take a look at the TLC-Nand above try to tell how we can improve. If you guess already thats right:
  - Not have designed for minimum Area, even with 2 metal layers.
  - Traces are not for minimum possible resistance routing.
  - Right angle trace turn can be avoided more.
  - GND between SATA to NVM can easily have approximately 1/5th of route
  - Though Vcc to R-pull-up and R-pull-up to R/B# pin share the same current path, trace-widths are different
  - One life ending error which may kill the Design--> VHDCI Vcc trace-bridge via (the one near to PCB edge) was chosen all-layer, which cause direct contact with VHDCI-body frame (which is metallic for our case) may often keep grounded, that may result Vcc short circuit. We fix it by PCB-corrector patch during assembly on that particular via-contact. 

Make Comments if you observe anymore.
