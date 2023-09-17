Proposed Amstrad HAL/PAL Replacement


This is *prototype* design for a replacement for the HAL/PAL memory manager in an Amstrad CPC6128.
This project has *NOT* been tested.
The pinouts of these designs are different those of the original Amstrad HAL/PAL and some form of adapter will be required.


The design uses one of two chips from the Renesas GreenPAK range - https://www.renesas.com/eu/en/products/programmable-mixed-signal-asic-ip-products/greenpak-programmable-mixed-signal-products

The chips used are:
SLG46826G - available in a TSSOP package
SLG46826V - available in a QFN package
SLG46826V-DIP - the same chip as above but in the PCB-DIP package

The design files are identical except for the package setting. Note that the pinouts are flipped between the TSSOP and QFN packages.

These chips where chosen because they can be (re)programmed via an I2C connection. This means a) they can be reprogrammed multiple times and b) they can be programmed without needing an expesive development board.

At this stage this project assumes the use of a programmer and extra software (and a microcontroller) will need to be written to enable I2C programming. However, the design files for doing so are included here.

Also included here is an adapter PCB to mount an SLG46826V-DIP IC into the original HAL socket.

Files included:
*.gp6 - Design files for use with the Renesas Go Configure software which can be downloaded from https://www.renesas.com/eu/en/software-tool/go-configure-software-hub
*_NVM.txt - Exports of the NVM data which will be needed to program the IC(s) via I2C. (See below)
AmstradHALTests.txt - The results of tests run against an Amstrad HAL/PAL.
GreenHALTests.txt - Results of the same tests run against the GreenHAL design.
DIPDapter (folder) - The design for an adapter PCB between the -DIP variant of the chip and the Amstrad HAL socket.


© Mike Sutton, 2023
Licence: CERN-OHL-P-2.0