# Success! Big Sur on AMD FX-6300 (GA-990XA-UD3) everything working (but Sleep and Shutdown) including audio (VoodooHDA.kext in Library/Extensions)

**System Configuration**

- Gigabyte 990XA-UD3 motherboard

- FX-6300 CPU
 
- 8GB RAM
 
- Gigabyte (Nvidia) GT730 Silent 2GB graphics card (metal compatible)
 
- Embedded Etron EJ168 USB contollers for USB 2.0 and USB 3.0 (**not compatible** with macOS)
 
- Discrete (VIA based) USB 3.0 controller compatible with macOS
 
- Various HDDs and SSDs with Windows 10, Linux and OS X / macOS systems (Sierra, Catalina)
 
**Background**

After succesfully installing and running Catalina on the above system, it was time to try and upgrade to Big Sur.
Since it was not wise to upgrade the "production" system disk (Catalina), the decision was made to install Big Sur on a separate disk
for safety reasons.

All the attempts following install instructions for AMD FX type systems failed, either because the Opencore would not boot properly or the install process hung on kernel panic errors or some other obsure errors.

Finally the solution came from a post on https://forum.amd-osx.com site.

The **EFI** provided by the author of the post worked flawlessly with just a minor adjustment for the number of CPUs in Kernel patches as per instructions in https://github.com/AMD-OSX/AMD_Vanilla/tree/master


**Prerequisites**

- USB stick 16 or 32 GB
 
- Spare SSD (or HDD) and maybe USB-to-SATA adapter for experimentation w/o case opening
 
- Prepare the disk by opening the Disk Utility and format the disk as APFS
 
- Apropriate SSDTs, kexts and patches for AMD FX CPU (SSDT-EC.aml, SSDT-USBX.aml, SSDT-XOSI.aml, Lilu.kext, VirttuslSMC.kext, etc.). Get info and necessary files from https://dortania.github.io/OpenCore-Install-Guide/AMD/fx.html#starting-point
 
- AMD Vanilla Kernel patches from https://github.com/AMD-OSX/AMD_Vanilla/tree/master
 
- Opencore package  https://mackie100projects.altervista.org/download-opencore-configurator/
 
- All necessary files are included in the EFI folder provided in the given post: https://forum.amd-osx.com/index.php?threads/success-asus-sabertooth-990fx-r2-0-fx-8350-nvidia-gtx-690-oc-0-7-6-big-sur-11-6-2-monterey-12-1.2400/
 

**Installing Big Sur for FX-6300 (GA-990XA-UD3)**

Download **Install macOS Big Sur** app (there are various ways to do that) and place it in the Applications folder

Install Big Suro installer on the USB stick by opening a Terminal and using the command  

**sudo /Applications/Install\ macOS\ Big\ Sur.app/Contents/Resources/createinstallmedia --volume /Volumes/USB /Applications/Install\ macOS\ Big\ Sur.app --nointeraction**

Then, Open the above downloaded EFI folder and using the **ProperTree** editor make the appropriate adjustments in the **config.plist** regarding the number of cores of the CPU (06 in this case) for the three "**algrey - Force cpuid_cores_per_package**" patches and alter the **Replace** value only.

Changing B8000000 0000/BA000000 0000/BA000000 0090* to B8 **CoreCount** 0000 0000/BA **CoreCount** 0000 0000/BA **CoreCount** 0000 0090* substituting **CoreCount** with the hexadecimal value matching your physical core count.

Copy the EFI folder to the EFI partition of the USB installer stick and reboot

After the system boots into the Opencore menu of the USB installer choose the appropriate entry to start installing Big Sur onto the new disk.

**Post Install**
  
  After Big Sur is installed on the new disk, copy the USB installer's **EFI folder** onto the new disk's EFI partition.
  
  Reboot into the new system disk (Big Sur)
  
  Everything (but Sleep and proper Shutdown) should be working except Audio. For some reason Big Sur brakes VoodooHDA.kext injected through Opencore.
  
 ** Fix Audio / VoodooHDA in Big Sur**

  To fix audio in Big Sur (using VoodooHDA kext) follow the instructions from this post https://kaneis.wordpress.com/2022/06/13/how-to-fix-voodoohda-audio-for-amd-fx-cpus-ga-990xa-ud3-in-big-sur/
  
