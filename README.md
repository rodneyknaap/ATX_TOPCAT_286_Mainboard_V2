# ATX_TOPCAT_286_Mainboard_V2  
REV2 design for the VLSI TOPCAT ATX 286 mainboard  

A rough preview of the design in progress, to be updated after various changes are added:   

![A photo of the TOPCAT REV2 design in progress](TOPCAT_286_MAINBOARD_REV2_IN_PROGRESS_03.png)  


After building the somewhat limited version of the TOPCAT "V1", we now have a proof of concept for how to create a 286 system with the VLSI TOPCAT chipset.  
sqpat sent us some VLSI chips and Intel versions of the 331 companion chip. I have tested these on a MSI TOPCAT 386SX board so they are valid equivalents for the VLSI 331.  

Now we know the concept is correct, we can elaborate the design further.  
We will add some CPLD support for additional hardware. The mainboard gerbers will be at least available in micro-ATX format since much is integrated and for those who want a micro tower build, and additionally I will probably feature a full sized gerber set as well for those who want more ISA slot connectors and a larger case.  
Check below for the further details of this design.  

## Purpose and permitted use, cautions for a potential builder of this design  

This project was created for historical purposes out of love for historical computing designs and for the purpose of enabling computing enthousiasts with a sufficient level of building and troubleshooting expertise to be able to experience the technology by building and troubleshooting the hardware described in this project. Due to the level of this project, it may be suitable as a project for students to get into. If there are any questions from teachers who like to teach about this technology I would be happy to answer them. It may be really interesting to analyse the elaborate and complex CPU timing and 8 bit to 16 bit data byte translation and DMA mechanisms in an educational setting.

Besides the GPL3 license there are a few warnings and usage restrictions applicable:
No guarantees of function or fitness for any particular or useful purpose is given, building and using this design is at the sole responsibility of the builder.

Do not attempt this project unless you have the necessary electronics assembly expertise and experience, and know how to observe all electronics safety guidelines which are applicable.

It is not permitted to use the computer built from this design without the assumption of the possibility of loss of data or malfunction of the connected device. To be used strictly for personal hobby and experimental purposes only. No applications are permitted where failure of the device could result in damage or injury of any kind.

If you plan to use this design or any part of it in new designs, the acknowledgement of the designer and the design sources and inspirations, historical and modern, of all subparts contained within this design should be included and respected in your publication, to accredit the hard work, time and effort dedicated by the people before you who contributed to make your project possible.

No guarantee for any proper operation or suitability for any possible use or purpose is given, using the resulting hardware from this design is purely educational and experimental and not intended for serious applications. Loss of data is likely and to be expected when connecting any storage device or storage media to the resulting system from this design, or when configuring or operating any storage device or media with the system of this design.

When connecting this system to a computer network which contains stored information on it, it is at the sole responsibility and risk of the person making the connection, no guarantee is given against data loss or data corruption, malfunctions or failure of the whole computer network and/or any information contained inside it on other devices and media which are connected to the same network.

When building this project, the builder assumes personal responsibility for troubleshooting it and using the necessary care and expertise to make it function properly as defined by the design. You can email me with questions, but I will reply only if I have time and if I find the question to be valid. Which will probably also lead to an update here. I want to primarily dedicate my time to new project development, I am not able to do any user support, so that's why I provide the elaborate info here which will be expanded if needed.

# Design details  
After building the first version of a TOPCAT 286 system, it's time to design a second improved version which includes a number of changes:  
- adding series termination resistor footprints for possibly improving edges of signals going to the DRAMs
- 72 pin DRAM modules instead of 30 pin ones
- using 4 megabit 4 bit wide DRAMs on SIMMs will reduce the DRAM address and control bus load
- adding series termination resistors for the fast clocks
- adding the possibility to remove the BUSCLOCK from the 320 controller to possibly force it into synchronous slot command timing mode
- moving the 286 into a PLCC socket for being able to swap the CPU  
Please take note of the fact that including series termination resistors does not mean that these must be populated.
Whether these will remain a part of the recommended build will depend on testing and measurements.
I will update depending on the findings and a definitive partslist will follow from those. Possibly certain footprints will be changed to zero ohm resistors.

# PicoGUS  
I have asked polpo and he has kindly given me permission to add the PicoGUS into the design.  
This will be experimental at first to use some PLCC logic to drive the PicoGUS control.  

The PicoGUS is created by polpo here on GitHub  
https://github.com/polpo/picogus  
Licensing conditions for PicoGUS parts apply as defined in the picogus repository.  

The license of PicoGUS applies to all parts of PicoGUS integrated into this system:  
The hardware portions of the PicoGUS repository (hw/ directory) are licensed under the CERN OHL version 2, permissive.  

The software portions of the PicoGUS repository (sw/, pgusinit/ directories) as a collection are licensed under the GNU GPL version 2. Some files are individually dual-licensed under BSD or MIT licenses – see the license in the file headers for details.  

PicoGUS is always under development by polpo so it's always in a beta status.  
When building this mainboard project, the intellectual property and conditions of the PicoGUS project must be respected and observed.  
Not to be sold for profit and design is "as-is" without any guarantees.   
Builders must take their own responsibility in debugging the PicoGUS from the provided information in the PicoGUS repo.  

Only build the PicoGUS parts of you agree with the conditions of the PicoGUS project by polpo, same as if you were building a stand alone PicoGUS.  
Many thanks go out to polpo for agreeing with PicoGUS to be included in this project!  
Be sure to check out his repo because he is always developing the PicoGUS further!  

Further features currently being added to the design:  
A larger CPLD will be used:
- primary and secondary IDE port
- POST LED display
- separating the BUS Clock of the 320 system controller to its own oscillator so we may freely swap other oscillators without affecting the rest of the system.  Speeding up the BUS Clock to the 331 will be under investigation and may improve VGA read and write cycle speeds which may increase gaming speeds.
- the system will be adaptable to feature a 286 and/or 386SX where a 386SX can be added or removed using a plug-in module
- we can test the differences between the 286 and 386SX
- more CPLD pins available to support PicoGUS control and other system functions, continuing to work on and verifying the adapted PicoGUS design areas

# Big news!  
A TOPCAT AMI BIOS has been adapted by sqpat to make use of a more advanced AMI BIOS previously developed for a TOPCAT 386SX system.  
This has led to a substantial speed up of the REV1 TOPCAT 286 system to run RealDOOM at 6.85 frames per second, 8.6 frames per second in 3D bench.  
At maximum 22.4 MHz the REV1 ATX TOPCAT system also featured in my repositories can perform 14922 writes and 11115 reads per millisecond to system DRAM.  
Many thanks go out to sqpat who has made a repo for his work on the disassembled code:  
https://github.com/sqpat/topcatbios  
If interested, do check out the code for various comments by sqpat and results of his code examination!  
So we now have a much faster and more responsive TOPCAT 286 system with the REV1 system capable of running at 22.4MHz!  
The advanced AMI BIOS allows us to fully tweak the TOPCAT chipset to maximize the performance as far is it is able to go!  

I am currently working on the schematic to add and update more circuit areas and also doing verifications and going over of the entire design.

Last update:  

18-4-2026
