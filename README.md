# AVRDUDE 6.3 with x0xb0x bootloader support

This small avrdude-6.3 patch allows you to upload firmware to the x0xb0x
synthesizer without using obsolete software. x0xb0x bootloader uses
simplified AVR910 protocol.

**This is NOT an official avrdude repo!**
For official avrdude site please visit:
https://savannah.nongnu.org/projects/avrdude

## Supported features:

* flash memory: read/erase/write/verify
* lfuse and hfuse: read

## Unsupported features (due to x0xb0x bootloader limitations):

* efuse read (0xFF factory default is returned)
* fuse write
* custom serial programming commands (since it isn't a real AVR910 device attached to MCU's SPI bus)

## Usage:

```
avrdude -c avr910 -x x0xb0x -p m162 -P <serial port> <avrdude options>
```

## Example:

```
[djsf@raspi2:~/dvp/avrdude]$ ./avrdude -c avr910 -x x0xb0x -p m162 -P /dev/ttyUSB0 -U flash:w:/home/djsf/x0xb0x/firmware/x0xb0x.hex:i

Found programmer: Id = "x0xb0x1"; type = S
    Software Version = 1.2; Programmer supports auto addr increment.

Programmer supports the following devices:
    Device code: 0x63 = ATmega162

avrdude: AVR device initialized and ready to accept instructions

Reading | ################################################## | 100% 0.01s

avrdude: Device signature = 0x1e9404 (probably m162)
avrdude: NOTE: "flash" memory has been specified, an erase cycle will be performed
         To disable this feature, specify the -D option.
avrdude: erasing chip
avrdude: reading input file "/home/djsf/x0xb0x/firmware/x0xb0x.hex"
avrdude: writing flash (15214 bytes):

Writing | ################################################## | 100% 251.24s

avrdude: 15214 bytes of flash written
avrdude: verifying flash memory against /home/djsf/x0xb0x/firmware/x0xb0x.hex:
avrdude: load data flash data from input file /home/djsf/x0xb0x/firmware/x0xb0x.hex:
avrdude: input file /home/djsf/x0xb0x/firmware/x0xb0x.hex contains 15214 bytes
avrdude: reading on-chip flash data:

Reading | ################################################## | 100% 123.70s

avrdude: verifying ...
avrdude: 15214 bytes of flash verified

avrdude: safemode: Fuses OK (E:FF, H:94, L:EE)

avrdude done.  Thank you.
```
