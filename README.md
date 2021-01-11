# TriMod Adapter (SMD Version)

![](https://github.com/DL2DW/TriMod_Adapter_SMD_Version/blob/main/Images/TriMod_CBM_Adapter.jpg)



## IEEE-488 for the Commodore 1541 Disk Drive

Before I developed the [version with normal THT components](https://github.com/DL2DW/TriMod_Adapter), I built a version with SMD components. 

Only the integrated Kernal adapter is missing. This must be plugged in externally additionally.



# Technical

Commodore had derived the 2031LP from the 1541 at that time. If you look at both schematics, they only differ in one detail.

And this is the connection to the outside world. 

On the 1541, the VIA 6522 is only partially used, because port A is not connected. Port B provides the lines for the CBM bus, which communicate with the computer via a 74LS14 and 74LS06 driver.

In contrast, port A is also required for the 2031LP. This provides the 8 parallel data lines, while port B is responsible for the control lines of the GPIB bus. Here the two drivers SN75160 and SN75161 are used.

And these are basically the actual differences, to put it simply.

So the 1541 can be easily converted to a 2031 with an adapter board. Of course, the Kernal has to be exchanged accordingly.

So that the adapter does not have to be removed every time you want to use the CBM bus, I have made the whole switchable.

With the help of CD4066 4-fold switches, the lines can be easily switched. A connector for switching a Kernal adapter is also available.



![](https://github.com/DL2DW/TriMod_Adapter_SMD_Version/blob/main/Images/TriMod_CBM_Adapter_TOP.jpg)



The IEEE-488 connector is clearly visible on the left side. This can either be led out with a ribbon cable or connected to a corresponding socket in the case. 

The two pin headers at the bottom are for the connection to the kernel adapter and the switch itself. 

- Contact 1 = GND
- Contact 2 = RESET
- Contact 3 = Kernel switch
- Contact 4 & 5 = Switching between IEC and IEEE-488

A standard switch is connected to contact 4 & 5. Connecting the two contacts switches to IEEE-488 mode. Contact 3 is used to switch the kernel then as well. This contact is connected to the above mentioned kernel adapter board.

A 27128 EPROM is required for the Kernal. First (address 0x0000) the binary for the 1541 mode is written and afterwards (address 0x2000) the binary for the IEEE-488 mode.

With setting the jumper the mode can be switched. Of course this should be done only in the switched off state.



# BOM

Here is the list of components. 

|      | Description                                                  | Part                  | References           | Value                       | Quantity Per PCB |
| ---- | ------------------------------------------------------------ | --------------------- | -------------------- | --------------------------- | ---------------- |
| 1    | Unpolarized capacitor                                        | C                     | C1 C2 C3 C4 C5 C6 C7 | 100nF                       | 7                |
| 2    | Generic connector, single row, 01x03, script generated (kicad-library-utils/schlib/autogen/connector/) | Conn_01x03            | CN1                  | Kernal                      | 1                |
| 3    | Diode                                                        | D                     | D1 D2                | 1N4148                      | 2                |
| 4    | Generic connector, double row, 02x12, top/bottom pin numbering scheme (row 1: 1...pins_per_row, row2: pins_per_row+1 ... num_pins), script generated (kicad-library-utils/schlib/autogen/connector/) | Conn_02x12_Top_Bottom | J3                   | IEEE-488 Connector          | 1                |
| 5    | Generic connector, single row, 01x20, script generated (kicad-library-utils/schlib/autogen/connector/) | Conn_01x20            | J1 J2                | PIN Header to PCB 6522 1-20 | 2                |
| 6    | Jumper, 2-pole, open                                         | Jumper_2_Open         | JP1                  | Jumper                      | 1                |
| 7    | Resistor                                                     | R                     | R3                   | 10k                         | 1                |
| 8    | Resistor                                                     | R                     | R4                   | 1k                          | 1                |
| 9    | Resistor                                                     | R                     | R1 R2 R5             | 3k3                         | 3                |
| 10   | 2x DIP Switch, Single Pole Single Throw (SPST) switch, small symbol | SW_DIP_x02            | SW1                  | IEEE-488 Device ID          | 1                |
| 11   | Quad Analog Switches                                         | 4066                  | U1 U2                | 4066                        | 2                |
| 12   |                                                              | 7406N                 | U7                   | 7406N                       | 1                |
| 13   | Quad 2-input XOR                                             | 74LS86                | U3                   | 74LS86                      | 1                |
| 14   |                                                              | MOS6522               | U4                   | MOS6522                     | 1                |
| 15   |                                                              | SN75160               | U5                   | SN75160                     | 1                |
| 16   |                                                              | SN75161               | U6                   | SN75161                     | 1                |





If you liked my project, I would be very happy about a small coffee donation.

[![ko-fi](https://www.ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/R6R62T6RN)



# License

The contents of this repository, with the exception of the Docs and Software directories, are released under the following license:

- the "Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License" (CC BY-NC-SA 4.0) full text of this license is included in the [LICENSE.CC-NC-BY-SA-4.0](https://github.com/DL2DW/TriMod_Adapter_SMD_Version/blob/main/LICENSE.CC-NC-BY-SA) file and a copy can also be found at https://creativecommons.org/licenses/by-nc-sa/4.0/

