# MiniDuino
A minimalist arduino module featuring a ATmega328p, external clock, and 5v regulator with reverse polarity protection. 
Note unite does not have USART <-> USB capability.

# Programming
Connect Bus Pirate (red board) to MiniDuino.
	MISO -> PB4
	MOSI -> PB3
	CLK -> PB5
	CS -> RESET
	GND -> GND

Apply power to the MiniDuino. 
	9 volts -> Vin

Write Program in Arduino (or atmel studio). For pin numbering reference see Arduino_Uno_Rev3-schematic.pdf.
Export compiled hex file from Arduino IDE
	Sketch > Export Compiled Binary

Upload the hex file to MiniDuino using AVRDude
	$ sudo avrdude -c buspirate -P /dev/ttyUSB0 -p atmega328p -F -v -U flash:w:[name of file].hex

# Technical Details
![schematic](schematic.png)
![GERBER](gerber.png)

The board was partially constructed to test the input polarity protection (up to 20v), voltage regulator (drop off 5.12v), and reset pin circuit (default pulled to 5v, button press pulls to GND).
![partially constructed](sans-MCU.jpg)
MCU was drag soldered and the first blinky program is flashed. The factory default is for the MCU to use the internal RC oscillator, resulting in a very slow blinky.
![fully constructed](full.jpg)
Using AVRDude, fuse bits CKSEL[0..3] was changed from the default 0010 to 1111 for the external low power crystal oscilator.
avrdude -c usbtiny -p atmega328p -F -v -U lfuse:w:0xFF:m
![fuse bits](fuse.jpg)
![clock setting](clock.jpg)

Channel 1(yellow) is XTAL1, channel 2 (blue is XTAL2). Both waveforms are within spec. Just look at their stability...
![clock waveform](clock_wave.jpg.bmp)

There does however seem to be some stray inductance; mostlikely due to my bad soldering.

Done!
![done](complete.jpg)
