===Proposed Amstrad HAL/PAL Replacement


This is *prototype* design for a replacement for the HAL/PAL memory manager in an Amstrad CPC6128.
This project has *NOT* been tested.
The pinouts of these designs are different those of the original Amstrad HAL/PAL and some form of adapter will be required.


The design uses one of two chips from the Renesas GreenPAK range - https://www.renesas.com/eu/en/products/programmable-mixed-signal-asic-ip-products/greenpak-programmable-mixed-signal-products

The chips used are:
* SLG46826G - available in a TSSOP package
* SLG46826V - available in a QFN package
* SLG46826V-DIP - the same chip as above but in the PCB-DIP package

The design files are identical except for the package setting. Note that the pinouts are flipped between the TSSOP and QFN packages.

These chips where chosen because they can be (re)programmed via an I2C connection. This means a) they can be reprogrammed multiple times and b) they can be programmed without needing an expesive development board.

At this stage this project assumes the use of a programmer and extra software (and a microcontroller) will need to be written to enable I2C programming. However, the design files for doing so are included here.

Also included here is an adapter PCB to mount an SLG46826V-DIP IC into the original HAL socket.

Files included:
* *.gp6 - Design files for use with the Renesas Go Configure software which can be downloaded from https://www.renesas.com/eu/en/software-tool/go-configure-software-hub
* *_NVM.txt - Exports of the NVM data which will be needed to program the IC(s) via I2C. (See below)
* AmstradHALTests.txt - The results of tests run against an Amstrad HAL/PAL.
* GreenHALTests.txt - Results of the same tests run against the GreenHAL design.
* DIPDapter (folder) - The design for an adapter PCB between the -DIP variant of the chip and the Amstrad HAL socket.

==Chip Programming with a Dev Board
1) Open the appropriate .gp6 file with the Go COnfigure software
2) Insert the chip (and adapter if needed) into the Dev Board.
3) Plug the Dev Board into your computer (via USB).
4) In the Go Configure software click 'Debug' on the toolbar. The debugging Controls will appear on the right hand panel.
5) Click Change Platform and select your model of Dev Board.
6) Click the Program button/dropdown. This should now program your chip and give a confirmation message.

==Chip Programming via I2C (without a Dev Board)
As mentioned the necessary software etc for this has not been developed yet. If you want to try yourself these are the steps you'll need to go through:

For this you'll need a suitable microcontroller with I2C outputs.
You'll need to process the relevant NVM file from the repository into suitable I2C data.
For an unprogrammed chip: You'll need to encode the I2C device address on the appropriate pins (by connecting them to 5V or ground) to match the device address you're sending data to. (Consult the datasheet for the IC to ascertain which pins to use).
For an already programmed chip: the previous step is unecessary as the I2C address will now be programmed into the device. This address is set to 0001 (binary). You'll need to use this address programming software.
You'll need to connect the chips ground and power pins to power the device.
You'll need to connect the I2C pins (SDA and SCL) to the appropriate pins on your microcontroller.
You'll also need pullup resistors on these pins. 2.2k ohms *should* be suitable here.
And finally you can get the microcontroller to send the data to the IC. :phew:

The DIPDapter board included with the project includes a header for the SDA, SCL and ground pins.

==Chip Programming via I2C (with a Dev Board)
The Go Configure software can also program a chip via I2C using the Dev Board. This may be useful where a chip has been soldered in place.

To do this follow the steps under Chip Porgramming with a Dev Board except:
You will need to connect the power, ground, SDA and SCL pins of the chip to the external connector of the Dev Board. For a QFN chip the pinout here is the same as the chip. For a TSSOP chip the pin ordering is reversed!

Follow the notes under Chip Programming via I2C (without a dev board) with regards to configuring an I2C address for the chip. I.e. connect pins to 5v/ground as needed for an unprogrammed chip. For a previously programmed chip the on chip address will be used instead.

I the Debugging Controls of the Go Configure software find the Device setting and change from Onboard to the I2C device address. Either as configure on the pins (for an unprogrammed device) or '0001' for a previously programmed device.

© Mike Sutton, 2023
Licence: CERN-OHL-P-2.0