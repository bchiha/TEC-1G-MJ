## File Links
| File | Description | Version |
|---|---|---|
| [Errata](./Errata.md) | <b>*CRITICAL:*</b> The latest Errata announcements. **Read BEFORE assembly!** | 2/jun/2024 |
| [Assembly Instructions](./Documentation/Assembly/Readme.md) | Instructions on putting the TEC-1G together | 0.2 |
| [Component Overlay](./TEC-1G_Component_Overlay_v1-13.pdf) | (Out of date. Needs updating. Use with caution. Always follow silkscreen.) | 1.1 |
| [Parts List](./TEC-1G_PartsList_v1-5.pdf) | (Out of date. Needs updating. Use with caution. Always follow schematic.) | 1.5 |
| [BOM Sourcing](./files/TEC-1G_BOM_v1.5.xlsx) | (Out of date. Needs updating. Use with caution. Always follow schematic.) | 1.5 |
| [Schematic](./TEC-1G_Schematic_v1-22.pdf) | See what makes the TEC-1G tick. | 1.22 |
| [PCB Gerbers](./TEC-1G_Gerbers_v1-22_SigEd.zip) | Gerbers of the PCB so you can print your own! | 1.22 |
| [Monitors / ROMs](./ROMs/) | Download and burn the ROMs for your TEC-1G from this link! | 1.5 |
| [MON3 User Guide](./MON3_User_Guide_v1.5.pdf) | The comprehensive User Guide to MON3 | 1.5 |
| [TEC Deck](./TEC-Deck/) | The TEC Deck has multiple Cards that add major functionalityto the TEC-1G! | 1.2 |
| [GPIO Modules](./GPIO/) | See what modules can be attached to the GPIO connector on the LHS of the TEC-1G | 1.0 |
| [TEC Expander](./Expander/) | The Expander finally has the 8x8 LED Array... And it's in RGB! | 1.0 |


## News & Developments

We have added a new section to the GitHub that agregates all the news and new items for the TEC-1G. [Follow this link](https://github.com/MarkJelic/TEC-1G/tree/main/News) for all the latest info.

# TEC-1G Introduction

TEC-1G - A Z80 based single board computer.

The TEC-1G is a direct descendant of the Talking Electronics Computer, known as the TEC-1, which was first published by the Australian electronics hobbyist magazine ["Talking Electronics"](https://www.talkingelectronics.com/te_interactive_index.html) (or simply TE), between 1981 and 1991.

The TEC-1 was developed as a learning computer, designed to teach the basics of how a microprocessor works at the fundamental hardware and software level, and offered the ability to create and run simple programs in Z80 machine code. TE magazine covered the TEC-1 in six installments, known as "Issue 10" to "Issue 15". These magazines can be downloaded freely from the TEC-1 GitHub, located at [tec1group/TE-Magazines](https://github.com/tec1group/TE-Magazines)

Interest in the TEC-1 declined following the winding down of TE through the 1990's, which reflected a general decline in electronics as a hobby in Australia. This, coupled with interest in more advanced 'single chip' microcontrollers saw TEC-1's put aside and the world moved on.

The TEC-1 was revived around 2018 with a release of a reproduction PCB and related peripherals on the Internet. Retro computing has become quite popular of late, and so a an active TEC community has (re)formed through [Facebook](https://www.facebook.com/groups/tec1z80) with new hardware designs, enhanced versions and various expansion options being offered by various contributors within the community.

The 1G builds on both the TEC-1's base and recent history to modernize the overall design, address various design limitations and integrate many of the excellent add-ons into to a single PCB for the first time.

The TEC-1G remains true to the original TE design goals: it is is built using only simple through-hole TTL logic chips so it is easily built and understood by the hobbyist. For the first time, the TEC-1G will also be fully free and open source, in both its hardware and software. The TEC-1G is the ultimate TEC-1!

The 1G has been developed by Mark Jelic with the input of the original designers, John Hardy and Ken Stone, ex-TE staff member Craig Hart, along with contributions from community members Brian Chiha and Ian McLean. Finally, the 1G has also been produced with the blessing of Colin Mitchell, Talking Electronics owner.

## Major Features

- Full TEC-1 hardware and software compatability; runs all previous MONitors without modification
- Flexible memory options; 32K RAM, 16k ROM in default configuration. Up to 64k RAM + 16k ROM supported.
- Support for multiple configuration options and memory types from 2k to 32k memory devices
- RAM write protection for improved software development
- Shadow Memory and bank switching capabilities
- 20x4 LCD screen as primary display device
- Diagnostic & LED bar indicator for system state
- Z80A CPU running at 4.0MHz; 'slow' clock support for older monitors retained
- Full QWERTY MATRIX keyboard & joystick options
- Upgraded key options for onboard hex keypad; supports Gateron Low Profile switches with optional backlighting, as well as standard 12mm tactile buttons
- Improved RESET circuit for reliable start up and system stability
- USB B or 9-12v AC/DC power sources
- Serial interface using an optional FTDI/FT232 adaptor for USB communication with a PC or terminal
- Future support for SD card mass storage interface
- Native Z-80 expansion bus connectors supporting a full range of peripherals
- 'TEC-Deck' expansion connectors for future daughterboards
- 'TEC Expander' port for compatability with existing TEC peripherals
- HALT status LED


## More Documentation [Coming Soon™](/Documentation/readme.md)

![TEC-1G Render - Gateron Keys](/pictures/TEC-1G_Render-Green+Components.jpg)

I'd like to thank PCBWay for sponsoring the ongoing development of modules that are being added to the TEC-1G ecosystem. I'm impressed how proactive they are in finding projects like this one and encourage and foster such development. Thank you, PCBWay!

![PCBWay Logo](/pictures/PCBWay_Logo_S.png)
