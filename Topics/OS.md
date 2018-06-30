# ARM

## Bootrom

Bootrom (or Boot ROM) is a small piece of mask ROM or write-protected flash embedded inside the processor chip. It contains the very first code which is executed by the processor on power-on or reset. Depending on the configuration of some strap pins or internal fuses it may decide from where to load the next part of the code to be executed and how or whether to verify it for correctness or validity. Sometimes it may contain additional functionality, possibly usable by user code during or after booting. Some examples:

- iPhone boot ROM. Embedded in the mask ROM and can't be modified. Loads the next stage boot loader from flash or USB (in DFU mode) and verifies its signature using built-in RSA implementation. Also provides accelerated decryption functions for the next stage bootloader.
- TI's OMAP4 boot ROM. Can load user code from flash (NOR, NAND, OneNAND), external memory, SD/MMC, USB or UART. Boot order and options are set by strap (SYSBOOT) pins. Provides some functionality for later stages (cache/TLB management etc.)
- NXP's LPCxxxx series Boot ROM. Placed in a hidden portion of the internal flash which is mapped at 0 on power-on. Implements CRP (code read protection), ISP (In-System Programming) which allows to upload and flash new code over UART. If a valid user code is in flash (needs to have proper checksum), maps it to 0 and jumps to it. A part of bootrom remains mapped to provide IAP (In-Application Programming) and some other services.

## Bootloader

Bootloader is responsible for finding and loading the final OS or firmware which is supposed to run on the chip. One main difference from bootrom is that it's usually in writable flash and can be replaced or upgraded.

Sometimes bootrom can perform the job of the bootloader. For example, OMAP's bootrom is complex enough (it can parse FAT32!) that you can probably have it load and start a Linux kernel directly.

However, in many cases a separate bootloader is used, either because the bootrom is not capable enough (or absent), or because extra flexibility is needed. It can be very simple (load kernel from a fixed flash location in RAM and jump to it), or can be much more complicated. For example, [U-Boot](http://www.denx.de/wiki/U-Boot) is a like a mini-OS by itself - it has a console, some commands, allows you break the boot process and e.g. modify the kernel command line arguments or even load the kernel from a different location (SD/MMC or USB), run some tests and so on.

Bootloaders are usually used when you have a more or less complex OS which may need some set up before it can be started. Smaller microcontrollers like NXP's LPC series usually use a monolithic firmware so they can get by without it (however, there may be [custom bootloaders](http://www.lpcware.com/content/nxpfile/an10866-lpc1700-secondary-usb-bootloader) for them too).

On the very simplest chips there may be no boot ROM or boot loader at all - they just try to fetch and execute instructions from a fixed startup address. In fact, most x86 chips to this day work like this - they just start executing code at FFFFFFF0 with the expectation that the chipset has mapped the BIOS flash chip there. Here, you can say that BIOS is the bootloader (though it also provides services to the OS, similar to bootrom).