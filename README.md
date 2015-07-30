# RPi-WD-Packet-Interface - A digital mode soundcard interface for the Raspberry Pi!

I set up an APRS igate using a Raspberry Pi device and a TNC-Pi 'hat'. While troubleshooting some other issues, I inadvertantly damaged the TNC-Pi, so I decided to go with a software TNC application. In this case, I chose [Dire Wolf](https://home.comcast.net/~wb2osz/site/) by WB2OSZ. In his documentation, he specified a simple radio PTT interface that included a 'watchdog timer' to prevent a software issue from locking the radio into transmit. Working with WB2OSZ, I expanded the circuit and created a board with the following features:

### Selectable transmit and receive channels
* I noticed between sound card dongles, the mic input could be on the left or the right channel, depending on how much care the manufacturer put into it. A jumper lets you pick the channel that works with your card. I added a transmit channel selector for the same reason, but also so you can use a 'Y' cable with your stereo sound card and use two interfaces to work with two radios without any cable hacking.

### Transmit audio level pot
* The radio is expecting millivolts of input into its MIC input. Modern sound cards can put out more than 2V peak to peak. This is really bad for distortion and over-deviation. Right now, I use about 40% volume on the sound card, and 20% volume on the pot. The audio is DC isolated with a capacitor to prevent phantom voltage (for electret microphones) from either the sound card or the radio from damaging anything.

### Adjustable watchdog delay
* Most people will use this for packet, but some others may use it for things like RTTY, JT-65, QRSS or any other digital mode that has a long duty cycle. I added a big cap and 25-turn trimmer for a delay adjustable between 0 and 110 seconds with the parts specified. One can solder in a fixed resistor or change values for something that doesn't need to be adjusted. [Calculators](http://www.ohmslawcalculator.com/555-monostable-calculator) are out there.

### DCD (received packet) LED
* The newest version of Dire Wolf can trigger a GPIO pin to signal a successfully decoded packet. Just bring this pin 'high' and the yellow DCD LED will light up. Yay. Good for watching activity at-a-glance from across the shack.

### Selectable single-wire handheld PTT or 'Kenwood' dedicated PTT wire method
* Most HTs use a resistor to ground on the microphone input to trigger PTT. Kenwood/Baofeng and some others have to be different and ground the mic shield to trigger. You can set a jumper to select whatever method you need.
	
### Standard Kantronics DB-9 radio interface
* I already had some cables I made and bought for radios when using my KPC3. The TNC-Pi and (I believe) the TinyTrak and OpenTracker devices use the same standard. This makes it easy to buy cables if you don't want to make them, or re-use ones you already have kicking around. FWIW, I hate DB9 connectors and prefer RJ-45 for these purposes, but I wanted to make it 'standard'. Signalink and RigBlaster use a similar (although RB is reversed) RJ-45 standard, but it's not as prolific. In case someone hates DB-9 as much as I do, I called out the signals on the pads to which they can be directly soldered for a cable, header pins, etc.

### Native 3.3v Rpi logic levels
* Using this board as configured works with the 3.3v logic the RPi uses. If you use another controller (like an Arduino) you *can* use 5V logic as the LMC555 CMOS can handle it without a sweat, but you will need to change the resistor values for the LEDs and transistor bias. You can also skip 3.3v altogether if you want to use it with a 5V microcontroller and use a cheap and widely-available LM555N (and the appropriate resistor changes).

### Uses standard 60mm x 60mm 'Sick of Beige' PCB size
* Just like the [xkcd](https://xkcd.com/927/) comic about standards, there is a new PCB size standard for the Maker crowd called [Sick of Beige](http://dangerousprototypes.com/docs/Sick_of_Beige). They have some cool acrylic cases at [Seeed Studios](http://www.seeedstudio.com/depot/Sick-Of-Beige-Basic-Case-v1-60mm-Square-DP6060-p-1329.html), but you can probably find others or fab up your own. The original board was smaller, but in order to fit into the SoB standard size, the minimum size that would fit the DB-9 connector is 60mm. Please note this is *not* a 'hat' for the RPi. It's a separate board. 

### Open Hardware
* I put the time into it, but like most of my projects, once it's done, it's done. I figure others can benefit from my work, so I may as well pass it on. This project is licensed under [Creative Commons Attribution-ShareAlike](https://creativecommons.org/licenses/by-sa/3.0/), so you can edit it, improve it, remix it into another project, make and sell PCBs or kits, etc. You just need to specify a link back to the original source (here) to comply. It's no big deal.
		
### Readily-available parts
* You probably have most of these parts in your bin, but things like the 3.5mm and DB-9 connectors are available at [SparkFun](https://www.sparkfun.com/). I specified genuine Borne trimpots in the PCB footprints but they are commonly used by others. You can find them at [Mouser](http://www.mouser.com/) or many other places.

You can order a [pre-made PCB from OSH Park](https://oshpark.com/shared_projects/rPyD67jj) (with the beautiful purple solder mask as shown). They come in multiples of three, so order some for your friends or make a couple for a multi-rig interface. You can also take the Eagle files and have them made elsewhere, or make your own using a toner transfer or photo etch PCB process. Go nuts.

# Known issues
None at this time. 

## Enjoy the interface, and see you on the air. 
