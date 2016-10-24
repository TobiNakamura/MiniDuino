# MiniDuino
A minimalist arduino module featuring a ATmega328p, external clock, and 5v regulator with reverse polarity protection. 
Note unite does not have USART <-> USB capability.
![schematic](schematic.png)
![GERBER](gerber.png)

The board was partially constructed to test the input polarity protection (up to 20v), voltage regulator (drop off 5.12v), and reset pin circuit (default pulled to 5v, button press pulls to GND).
![partially constructed](sans-MCU.jpg)
MCU was drag soldered and the first blinky program is flashed. The factory default is for the MCU to use the internal RC oscillator, resulting in a very slow blinky.
![fully constructed](full.jpg)
Using AVRDude, fuse bits CKSEL[0..3] was changed from the default 0010 to 1111 for the external low power crystal oscilator.
![fuse bits](fuse.jpg)
![clock setting](clock.jpg)
Channel 1(yellow) is XTAL1, channel 2 (blue is XTAL2). Both waveforms are within spec. Just look at their stability...
![clock waveform](clock_wave.png)
