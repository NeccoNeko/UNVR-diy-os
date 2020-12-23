# Overview

The Ubiquiti UniFi NVR (SKU: UNVR) is a $300, 1U, 4-bay, short depth, low power, silent server that runs Ubiquiti's proprietary UbiOS and applications.

This repo contains files used for exploration of the UNVR and hopefully will have instructions for installing your own OS on it.

# Project files

* [images/](images/): Pictures and other images related to the discovery done on this hardware and replacing the OS
* [logs/](logs/): Text files from the boot process and output of commands ran at the bootloader.
* [ubios-info/](ubios-info/): The output of various commands ran on the default OS installation

# Background

In November, 2020, I learned about the UNVR and saw potential for it to be used as a NAS.  Unfortunately it comes shipped with Ubiquiti's UbiOS.  It's based on Debian, but has very little documentation and runs a myriad of their proprietary applications that I don't need.

On Black Friday, 2020, the UNVR went on sale for $50 off the usual price and I couldn't resist picking it up to play with it.

This project will cover my attempts to modify the UNVR to run a standard Linux installation (starting with Debian), and if that doesn't work, starting from the ground up using LFS (Linux From Scratch).

# Word of caution

If you make changes to your NVR you will very likely invalidate the warranty on it.  Ubuiti made several efforts to prevent modifications from being performed to the device:

* Warranty sticker over a chassis screw
* Glued down USB boot stick
* Upublished modified GPL source code

Proceed with caution.

# Hardware specs

* 1U (442.4 x 325 x 43.7 mm / 17.4 x 12.8 x 1.7")
* 4 hot swap bays (3.5" and 2.5" supported)
* Quad-Core ARM Cortex-A57 at 1.7 GHz (Annapurnalabs / Amazon SoC)
* 4 GB RAM
* 8 GB USB boot stick (for the OS)
* Max 100W power consumption (75W for drives)
* 10GbE SFP+ port (no optics included)
* 1GbE RJ45 port
* 3 cooling fans

# Console access

There are serial port pins on the mainboard almost directly behild the SFP+ port.  Only the first three pins are required (GND, TXD, RXD). Using a TTL serial adapter of some sort (e.g. FTDI based USB card, the Adafruit TTL serial cable, or an Arduino or one of its clones) you can access the console.  

There is no need to use the 4th pin (3v3 pin).  

See the [images for this project](/IMAGES.md) for an example of connecting a basic Moyina FTDI TTL USB adapter.

The UNVR uses the following serial console settings:

* 115200 (baud rate)
* 8N1

I used the following gnu screen command to connect to the console:

    screen /dev/tty.usbserial-AG0KB280 115200 8N1

Replace `/dev/tty.usbserial-AG0KB280` with the appropriate device name for your system

# Removing the USB boot stick from the UNVR

Between the PSU and the CPU is a USB connected flash drive.  This contains the OS that is used to boot the UNVR.  It is glued down.

I used a hair dryer to warm up the glue and dental floss to cut through the softened glue. Unfortunately I did not get pictures of this process, only the end result.

See the [images for this project](/IMAGES.md) for pictures of the flash drive.
