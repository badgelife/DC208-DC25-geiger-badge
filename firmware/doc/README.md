TODO
====
- Determine how to get CMake to be friendly with this process.

Install toolchain
=================
```apt install gcc-avr avr-libc avrdude```

Compile the code
================
```avr-g++ -std=c++11 -mmcu=attiny1634 -Os -Wall main.cpp charlieplex.cpp led.cpp switch.cpp TWI_master.cpp ir_sensor.cpp delay.cpp clicker.cpp -I ../include/```

Create the hex output for loading
=================================
```objcopy -S -O ihex a.out hw.hex```

Flash the chip
==============
stk500v2
---
```avrdude -p attiny1634 -P /dev/ttyUSB0 -c stk500v2 -U flash:w:hw.hex:i```

avrispmkii
---
```avrdude -p attiny1634 -c avrispmkii -U flash:w:hw.hex:i```

usbtiny
---
On Ubuntu 16.04, avrdude appears to ship with faulty config settings for the attiny1634.  You may need to apply the avrdude.conf.patch before flashing.
```sudo cp /etc/avrdude.conf /etc/avrdude.conf.bak && sudo patch /etc/avrdude.conf -i avrdude.conf.patch```
Source: http://www.avrfreaks.net/comment/943976#comment-943976

```avrdude -p t1634 -c usbtiny -U flash:w:hw.hex:i```

Analyzing Size
==============
758 bytes is max
```avr-size -C --mcu=attiny1634 a.out```
