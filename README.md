# T68KRC, Tiny68K for RC2014
## Introduction

T68KRC derived from version 1 of Tiny68K. The major differences are Instead of 16 meg of memory, T68KRC has 2 meg of memory, and an expansion bus that's compatible with RC2014's I/O module is added. Like Tiny68K, T68KRC has no parallel ROM. The boot ROM is a 32Kbyte serial flash that's copied into the lowest 32Kbyte of the memory when powered up or with a reset. The RAM-resident boot software can be modified just like any data in RAM but is overwritten on the next power cycle or with a reset.

Figure below shows an assembled T68KRC.

www.retrobrewcomputers.org_lib_plugins_ckgedit_fckeditor_userfiles_image_builderpages_plasmo_t68krc_dsc_37130712.jpg
## Features

- Motorola 68000 CPU
- MC68681 DUART, port A is the console operating at 38400 baud, 8N1, with CTS/RTS hardware handshake.
- Altera EPM7128 CPLD contains the glue logic:
  - State machine to load 32K serial flash when powered up or with a reset,
  - DRAM controller for the 2-megabyte DRAM,
  - Hidden CAS-before-RAS refresh in hardware, no software overhead required,
  - memory decoder,
  - Interrupt controller,
  - Bus Error watchdog timer,
- 8-16 MHz oscillator (only 8 MHz operation is tested)
- 32Kbyte serial flash, 24C256 as the boot device.
- Second 32K serial flash that can be programmed in-situ and serves as the alternate boot device with just one jumper change.
- 44-pin edge connector interfaces to a low-cost IDE-CF module
- HY5118164 1Mx16 DRAM
- I/O expansion port compatible with RC2014 I/O bus interface.
- 7-segment LED display as visual indicator of board operations.
- Target for CP/M-68K ver 1.3
- 100mm x 76mm 2-layer pc board

## Descriptions

Low cost without sacrificing performance is the design goal of T68KRC. Cost control is achieved by:

    Two-layer PC board in 100mm x 76mm format. Many board manufacturers only charge 50 cents per board in quantity of 10 in this format,
    Memory in the form of single-chip 1Mx16 DRAM,
    Low cost 5-Volt CPLD, Altera EPM7128, that is about $3-4 each from China,
    Use low-cost serial flash memory as the boot memory,
    Interface via pc board edge connector to a low-cost 44-pin IDE-CF module,
    No on-board RS232 transceiver because most USB-based serial port modules operate at the TTL level,
    Low cost RC2014 expansion bus connector.

Good performance is maintained by:

    16-bit wide data bus,
    2-megabyte 60ns DRAM operating at zero wait state (at 8MHz system clock),
    Fast serial flash loads monitor in 0.6 second after a reset or power on,
    16-bit wide bus-connected IDE interface operating with two wait state at 8MHz, ←verify this
    Hidden CAS-before-RAS refresh cycle with no software overhead.

### Memory map

    RAM is from 0x0 to 0x1FFFFF,
    Serial Flash is from 0xFFD000-0xFFDFFF
    IDE-CF is from 0xFFE000-0xFFEFFF
    68681 DUART is from 0xFFF000-0xFFFFFF
    RC2014 expansion bus is from 0xFF8000-0xFF8FFF. 2 wait states access ← verify this

## Design Files <- Need extensive updates

* Rev 1 schematic
* Rev 1 Gerber files
* Part list
* Tiny68K Monitor debugger. The software is developed in the EASy68K tool chain. Programming binary for serial EEPROM programmer (CH341).
* Altera EPM7128 design files Designs are created in Quartus 8.1, should be compatible with later version of Quartus. Designs are entirely in schematics. Schematic in PDF format. Programming binary in .pof format.
    11/23/17 update: The original design files posted were incorrect. This is the correct version of the design files. Altera EPM7128 design files Designs are created in Quartus 8.1, should be compatible with later version of Quartus. Designs are entirely in schematics. Schematic in PDF format. Programming binary in .pof format. ← need revision
* CP/M-68K BIOS for T68KRC *
* CP/M-68K CPM v1.3
* CP/M-68K v1.3 distribution disk image for T68KRC RAMdrive
* RS232 adapter board to interface to the DB9 serial connector of a PC. The RS232 adapter is not needed for most USB-to-serial adapters which have TTL level I/O.
* Utility

    Memory diagnostics
    Clear CP/M memory area

### Connect to a PC

A PC with terminal program such as Hyperterminal is needed to interface with Tiny68K. An USB-to-serial adapter with TTL level input/output can connect directly to T68KRC's console connector. For USB-to-serial adapter with RS232 I/O, an adapter board is needed.
### Powering up T68KRC

Apply 5V to the board via the 2.5mm power jack, the center is 5V, barrel is ground. The nominal power consumption at 8MHz system clock is 500mA. When powered is applied, the 7-segment LED will display '8' for a second and then '6'. While waiting for console command, the outer segments of the 7-segment display will flash for 1/2 second, one segment at a time, in a circular sequence. If the display indicate a static '4', it is waiting for hardware handshake signal to assert. Be sure the terminal program has RTS/CTS hardware handshake enabled.
### Creating a new CF disk

Procedure for creating a new CF disk
