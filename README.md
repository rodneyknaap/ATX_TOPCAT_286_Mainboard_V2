# ATX_TOPCAT_286_Mainboard_V2  
REV2 design for the VLSI TOPCAT ATX 286 mainboard  

A few images of the finished design:   

![TOP layer of the TOPCAT V2 mainboard](TOPCAT_286_MAINBOARD_REV2_TOP.png)  

![BOTTOM layer of the TOPCAT V2 mainboard](TOPCAT_286_MAINBOARD_REV2_BOTTOM.png)  

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

# PicoGUS  
I have asked polpo and he has kindly given me permission to add the PicoGUS into the design.  

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
My design is non standard so please don't contact polpo to get support for this deviated design, and await my testing of the first build done this way.

My integration of the PicoGUS will be experimental at first to use CPLD logic to drive the PicoGUS control.  
So before testing there is no verification of this design. The CPLD is fast and reprogrammable so possibly modifications can be done in the future by reprogramming the CPLD support logic. It is my hope that having this in place, we may succeed to get the PicoGUS to work correctly.
The bus switch logic is really fast as long as the OE function of the bus switch is not used so we don't get any on/off time involved in the timing.
Bus switches used in the PicoGUS to multiplex between address and data bus to reduce pin usage on the RP2040 side are bidirectional.
What level of IO data transfer commands are possible will depend on testing.
The IO reads and writes are both by the CPU and by the 8 bit DMAC in this implementation.
I have integrated the two RP2040 modules to the system RESET procedure so each time the system is RESET, the RP2040s also are RESET on the RUN input.  
RP2040 RESET is driven by separate output on the CPLD so we can modify or expand the RESET behavior if needed. For example using a software controlled RESET for the RP2040s.  

# Big news regarding AMI BIOS support for the 286 CPU!  
A TOPCAT AMI BIOS has been adapted by sqpat to make use of a more advanced AMI BIOS previously developed for a TOPCAT 386SX system.  
This has led to a substantial speed up of the REV1 TOPCAT 286 system to run RealDOOM at 6.85 frames per second, 8.6 frames per second in 3D bench.  
At maximum 22.4 MHz the REV1 ATX TOPCAT system also featured in my repositories can perform 14922 writes and 11115 reads per millisecond to system DRAM.  
Many thanks go out to sqpat who has made a repo for his work on the disassembled code:  
https://github.com/sqpat/topcatbios  
If interested, do check out the code for various comments by sqpat and results of his code examination!  
So we now have a much faster and more responsive TOPCAT 286 system with the REV1 system capable of running at 22.4MHz!  
The advanced AMI BIOS allows us to fully tweak the TOPCAT chipset to maximize the performance as far is it is able to go!  

# Updated feature list of this second revision  
The design work on the mainboard PCB layout is now finished.  
The gerber files will be generated and uploaded shortly, as well as several support files such as component placement diagrams.

Feature list for this design:  
- 286 featured in a PLCC socket for being able to swap the CPU  
- micro ATX board size qualifying as a normal and not large board size with JLCPCB
- two 72 pin SIMM DRAM modules
- verified IO decoder design areas inherited from REV3E
- support for removable 386SX module using pinheader connectors
- CPLD logic controls 286/386SX mode switch using single header input pin for switch or jumper
- optional dual system BIOS supported for 286/386SX using 1 megabit flash ROM
- 64KB option ROM space support on system data bus using the CPLD
- primary and secondary IDE port
- POST LED display
- LPT port (from REV3E design, not yet tested, needs connector wiring)
- USB to serial mouse using RP2040 by limeprogramming
- PicoGUS by polpo integrated (CPLD support logic and access speed not yet tested)
- BUSCLK on separate oscillator which can be swapped or possibly removed for experimental testing
- optional series termination resistors added for the fast clocks
- optional series termination resistor footprints present for possibly improving edges of fast signals such as DRAM address and controls

Using 4 megabit 4 bit wide DRAMs on 72 pin SIMMs reduces the DRAM and CPU data bus load by a substantial factor.  

Please take clear note of the fact that including series termination resistors does not mean that these must be populated.  
Whether these will remain a part of the recommended build will depend on testing and measurements.  
I will update depending on the findings and a definitive partslist regarding the recommended series termination footprints will follow from those. Possibly certain footprints will be changed to zero ohm resistors if no improvement or any negative effects are found.

So we are using the dual IDE port IO decoder from REV3E which has operated flawlessly in the REV3D.
From now on we can also monitor the POST reporting on port 80 by AMI BIOS on the POST LED displays present on the board.  

We switch over the system between 286 and 386SX using CPLD logic. This allows us to seamlessly change the CPU mode and CPU RESET control of the TOPCAT and direct the appropriate CPU to the RESET. In addition we have a double capacity system ROM which provides us with two system ROM banks which can be switched over by the CPLD. The idea is to also control the ROM bank by the same mechanism which selects the CPU, so the system is fully adaptable between 286 and 386SX where we also can use separate system BIOS. In addition, the system ROM bank can be used in other ways to switch between two BIOS versions independent from CPU selection if desired.  

## Option ROM support  
The TOPCAT itself internally doesn't support option ROM BIOS chip select decoding. So the option ROM needs to be added to a TOPCAT system as if it were on a slot card. So the ROM is wired to the system data bus to be able to support this in a compatible way as the TOPCAT directs the data bus. The option ROM is enabled only sub 1MB address range as the PC/AT offers using /SMEMR and then decoded from this range in order to need less address lines on the CPLD. The option ROM offers 64KB of option ROM space which does not necessarily need to be adjacent in the memory map. Where the ROM is inserted into the memory map is freely reprogrammable within the A15 address line selection the CPU does in a certain memory area. Typical use way will be to insert half of the ROM(32KB) into the 0C8000h - 0CFFFFh area.
Theoretically a VGA BIOS can be programmed into the ROM for a custom VGA solution such as FPGA based VGA output using its own VGA BIOS, and the CPLD can be reprogrammed to enable the option ROM in this area of the memory map. In that case the VGA controller should not offer any BIOS enabling in its internal memory mapping as applied on the system bus.

The LPT1 port is inherited from the REV3D and REV3E designs however this has not been tested yet. The REV3D/E and LPT design here is partially implemented externally with two TTL ICs because of limited 6 different output enable function capability of the CPLD. The decoding and control signals of the LPT port are all handled by the CPLD internally.  

Two flatcable wires need to be soldered to connect the 25 pin female LPT D-connector to the board. In this case I have separated the LPT data port and control port into two separate headers because of the limited PCB space available in that board area where a single longer header cannot fit. In addition the two TTL chips used to complete the CPLD LPT port logic are located on top and bottom layers to make everything fit onto the board space.  

Using the two 10 pin flatcable boxheaders and cable solution is mostly straight forward however additional care must be observed to clearly label the connectors making sure that these are always inserted into the correct headers when using the printer port.  

If the LPT port is not used, the TTL chips can be left off the board, and IO pins from the CPLD present on the 10 pin LPT control header can be used for other purposes. Generally the TTL chip clocked data register could still be populated because it can also be repurposed for various other IO port operations and experiments if the user likes. So the data output is clocked and output enable controlled, the data input can be realized with the TTL transceiver and directly read by the CPU from the header data bits using the output enable driven by the CPLD.

# The USB to serial mouse adapter by Limeprogramming  
This adapter is proven to operate equally to any modern PC using a USB mouse receiver, tested with a cheap but reliable Logictech serial mouse.  
The RP2040 needs to be soldered to a single angled pin strip which can mate with a double female pinsocket connector on the board. In addition it needs a bridge to be soldered onto the mouse speed jumper GPIO pin connecting it to GND and selecting the proper mouse speed. See my example photos for what I used, and recommended for your initial tests, likely to be the version mouse speed you may continue to use. In addition the USB + and - signal pins need to be connected from the RP2040 pads to a two pin female header which you can plug into the two pin male pinheader on the board next to the RP2040 connector. Finally you need to solder the VCC pins of the RP2040 to a single wire, plugging into the two VCC holes of the PCB female pinsocket. Otherwise the photos also illustrate the process of preparing and connecting the RP2040. This needs to be programmed with the Limeprogramming project file. His GitHub for the project is here:
https://github.com/LimeProgramming/USB-serial-mouse-adapter  
The file to drop into the RP2040 is in this folder:  
https://github.com/LimeProgramming/USB-serial-mouse-adapter/tree/main/binary  

A few example photos of the module as prepared and inserted into the mainboard pinsocket:  
![RP2040_LIMEPROGRAMMING](USBMOUSE_RP_PICO_INSTALLED.jpg)   

![RP2040_LIMEPROGRAMMING_BACK](RP_PICO_MOUSE_SPEED_JUMPER.jpg)   

# CPLD programming details  
This requires Quartus II version 13.0 SP1.
You will need a ALTERA USB blaster programmer for the 208 pin CPLD directly from quartus by loading the .QPF project file, double click in the folder on the project QPF file which should load quartus when correctly installed. First compile the project by pressing the triangle "play" button. After full compilation is completed, you can then press the programmer icon. There you can define the programming hardware using the "hardware setup" button. Next highlight the file line in the file area, and on the left click on "change file", this dialog may take a while to produce the next window, there go to the "output files" directory inside your current quartus project, and choose the .POF file. Make sure to check that date and time match your time of just compiling the project a moment ago before confirming the file. Next to the file, check the boxes for "program/configure" and "verify". Next power up the system and click on "start" button. The dialog should show green in the "progress" section, running up until 100%. Sometimes the programmer communication from quartus may have some issue, which usually can be fixed by trying the "start" button again. Sometimes it's necessary to replug the USB connector into the USB blaster, and do the "hardware setup" again using the button. Finally the USB blaster will do the programming possibly after a little fiddling and retry.  

# CPLD JTAG cable  
A custom JTAG cable can be used. On the programmer side, you can use a 10 pin flatcable connector and solder the flatcable to a 6 pin pinheader using some more solid flexible wires which you can solder and use some heat shrink tubing to solidify the attachment to the flatcable ends. Next the more solid flexible wires can be soldered to the female single row pinheader that goes on the JTAG pins on the board, again using heat shrink tubing to ensure the wires won't bend and snap off easily from the connector.  
Pinouts of the cable are as follows:  

![JTAG_PROGRAMMING_CABLE](JTAG_CABLE.png)  

Here is the cable inserted into the tiny "USB Blaster REV C" for programming the larger 208 pin ALTERA CPLDS:  
![JTAG_PROGRAMMING_CABLE](JTAG_CABLE_2.jpg)  

![JTAG_PROGRAMMING_CABLE](JTAG_CABLE_3.jpg)  

As seen here in the photo, I indicated pin 1 by using a longer connector strip where the unused section with pins removed protrudes at the opposite side of pin 1, so the "edge" wire is always pin 1, as seen here in the photo above.  

# A special caution when you suspect your CPLD to be recycled  
If you got your CPLD from a recycler, this can be evident from the chip looking like it has been soldered before, that may mean that programming is present in the chip, which can then conflict with the other chips on the board, so a special procedure is advised for such chips suspected to contain programming:  
- first solder the ATX PSU connector and all components of the ATX circuit on the bottom right of the board (top ICs, capacitor and bottom resistors, capacitors and diode), as well as the VCC fuse and for example one ELCO next to the ATX connector on VCC.  
- solder the POWER and RESET two pin headers into the board, and add a jumper to short the RESET header until all further assembly and programming is done.  
- then solder the CPLD to the board, including the JTAG header pinstrip  
- power on the board (VCC needs to power the CPLD in order to program it, or the software will fail the programming sequence)
- immediately program the specific quartus project POF(208 pin) file into the CPLD  
- power off the board after the programming sequence is completed  
- continue normally with assembly and testing of your board
If previous unknown programming is suspected to be present in the CPLD, assemble it first without other ICs like the TOPCAT chips and CPU etc., if possible.
When pressing the "start" button in the quartus programmer window, the CPLD should tri-state all its pins except the JTAG I/O pins, which will immediately disable the previous programming.
If JTAG is not responding, this may indicate that the JTAG IO pins are programmed as normal IO pins, disabling the JTAG function of the CPLD. In that case I suggest posting in the VCF thread where we can attempt to find a solution to externally override the IO pin function of the JTAG pins and switching back into JTAG support mode of the CPLD.

# Current status of the project  
The PCB layout has been updated (update U1) to add a few missing address lines to the CPLD. If you manufactured a board already from the first release, check my VCF thread for details how to wire the address lines from the slot to the IO decoder CPLD on a few free pin vias using a small piece of flatcable.  
The project is being built by sqpat, check his updates in the VCF thread for his assembly and testing work.  
I will also order the TOPCAT REV2 PCB made and I will transfer my REV1 components to the new board so I can fully test it myself as well.  
Regardless, I will be testing with the Intel 331 chip and VLSI 320A TOPCAT chip revision, which has shown indications to be able to operate faster than the normal 320 version.  

More details from assembly, debugging and testing the project will follow here as soon as I have a board available to assemble.  

Further updates will follow.  

Last update:  

25-5-2026
