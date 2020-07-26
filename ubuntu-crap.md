# Shit I have to deal with running Ubuntu 18.04 on X1 Yoga G3 and some solutions

## Mic auto adjusting volume in hangouts calls
https://askubuntu.com/questions/689209/how-to-disable-microphone-volume-auto-adjustment-in-cisco-webex/761103#761103

## Getting External GPU dock to work
* Make sure nomodeset flag is set off to in the grub config
* Nvidia 436 works for me (Everything broke on 07/25/2020. Had to install Nvidia 440. Which caused x11 to seg fault. Run nvidia-xconfig to generate /etc/X11/xorg.conf)
* edit the nvidia device in /etc/X11/xorg.conf to add `Option "AllowExternalGpus" "True"`. It should look like:
```
Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    BoardName      "GeForce GTX 1050"
    BusID          "PCI:4:0:0"
    Option         "AllowExternalGpus" "True"
EndSection
```
* Reboot and your external display should work, but internal display would still be black. Need to fix that.
* There was some crap I had to do to get the internal monitor to work I don't remember ARGH
* THERE IS NO HOTPLUG SUPPORT SO DONT BOTHER

## Install tpfan control or the fans wont work

## s3 suspend is broken in BIOS, update to 1.35+ from lenovo

## Touchscreen stops working when resuming from suspend - to fix suspend using the power button and resume.

## Install this settings powertoy to adjust font scaling for 4k monitors and your inbuilt display

## Getting MX Master 2s to work
Use logiops
https://wiki.archlinux.org/index.php/Logitech_MX_Master
