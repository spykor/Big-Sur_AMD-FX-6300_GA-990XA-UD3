# Success! Big Sur on AMD FX-6300 (GA-990XA-UD3) everything working (but Sleep and Shutdown) including audio (VoodooHDA.kext in Library/Extensions)

**System Configuration**

Gigabyte 990XA-UD3 motherboard

FX-6300 CPU

8GB RAM

Gigabyte (Nvidia) GT730 Silent 2GB graphics card (metal compatible)

Embedded Etron EJ168 USB contollers for USB 2.0 and USB 3.0 (**not compatible** with macOS)

Discrete (VIA based) USB 3.0 controller compatible with macOS

Various HDDs and SSDs with Windows 10, Linux and OS X / macOS systems (Sierra, Catalina)

**Background**

After succesfully installing and running Catalina on the above system, it was time to try the upgrade of Big Sur.
Since it was not wise to upgrade the "production" system disk (Catalina), the decision was made to install Big Sur on a separate disk
for safety reasons.

All the attempts following install instructions for AMD FX type systems failed, either because the Opencore would not boot properly or the install process hung on kernel panic errors or some other obsure errors.

Finally the solution came from a post on https://forum.amd-osx.com site.

The **EFI** provided by the author of the post worked flawlessly with just a m inor adjustment for the number of CPUs in 3 Kernel patches as per instructions in https://github.com/AMD-OSX/AMD_Vanilla/tree/master


**Prerequisites**

USB stick 16 or 32 GB

Spare SSD (or HDD) and maybe USB-to-SATA adapter for experimentation w/o case opening

Apropriate SSDTs, kexts and patches (SSDT-EC.aml, SSDT-USBX.aml, SSDT-XOSI.aml, Lilu.kext, VirttuslSMC.kext, etc.)

AMD Vanilla Kernel patches from https://github.com/AMD-OSX/AMD_Vanilla/tree/master

Opencore package



