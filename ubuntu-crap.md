# Shit I have to deal with running Ubuntu 18.04 on X1 Yoga G3 and some solutions

## Mic auto adjusting volume in hangouts calls
https://askubuntu.com/questions/689209/how-to-disable-microphone-volume-auto-adjustment-in-cisco-webex/761103#761103

## Getting External GPU dock to work

Preface: https://www.youtube.com/watch?v=iYWzMvlj2RQ

* Make sure nomodeset flag is set off to in the grub config
* ~~Nvidia 436 works for me~~ Everything broke on 07/25/2020. Had to install Nvidia 440.100. Which caused x11 to seg fault. Run nvidia-xconfig to generate /etc/X11/xorg.conf, but usually that's not necessary. All the following steps work on 440.100
* If shit just blows up and you cant get xserver to start, just get rid of every fucking thing
```
sudo apt-get purge xorg "xserver-*"
sudo apt-get purge lightdm plymouth
sudo rm -rf /etc/X11/xorg
sudo apt-get autoremove

```
* YOU MAY HAVE TO REINSTALL [HWE](https://wiki.ubuntu.com/Kernel/LTSEnablementStack) IF YOU'RE ON 18.04.4
* lightdm broke with Linux 5.4.0.42, use gdm3. using gdm3 would require setting UseWayland=False in /etc/gdm3/custom.conf.
* [MUST DO] If you get black screen on your external display and dmesg output on your internal display, create `/etc/X11/xorg.conf.d/20-nvidia.conf` to add `Option "AllowExternalGpus" "True"`. It should look like:
```
Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    BoardName      "GeForce GTX 1050"
    Option         "AllowExternalGpus" "True"
EndSection
```
* Reboot and your external display should work, but internal display would still be black. To fix that, create `/etc/X11/xorg.conf.d/21-intel.conf` and add:
```
Section "Device"
    Identifier "Intel Graphics"
    Driver "intel"
EndSection
```
* THERE IS NO HOTPLUG SUPPORT SO DONT BOTHER
* Good luck getting CUDA installed

If someone from Nvidia is reading this: WHY THE FUCK DOES SETTING UP A NVIDIA GPU ON A LINUX MACHINE RUNNING XORG HAVE TO BE SO FUCKING COMPLICATED? WHY CANT YOU FUCKING DELIVER ON YOUR PROMISE TO SUPPORT WAYLAND? WHY THE FUCK DID YOU SHIP A BRAND NEW CLUSTERFUCK THAT IS EGLSTREAMS INSTEAD OF JUST SUPPORTING GBM LIKE LITERALLY EVERY OTHER COMPANY? EVERYTIME THERE IS A NVIDIA DRIVER UPDATE I START SHAKING BECAUSE I KNOW I AM GOING TO BE SPENDING THE NEXT TWO DAYS FIXING XORG/GDM3/LIGHTDM BECAUSE YOU WANT TO STRONG ARM EVERYONE INTO USING YOUR PROPRIETARY EGLSTREAMS. I AM FORCED TO USE YOUR CRAP BECAUSE EVERYTHING IS BUILT ON CUDA. I REALLY WISH I DID A PHD IN PHYSICS SO I COULD INVENT A TIME MACHINE, GO BACK IN TIME AND DO SOMETHING TO MAKE OPENCL TAKE OFF INSTEAD OF CUDA JUST SO THAT I DONT HAVE TO DEAL WITH YOUR BULLY TACTICS.

## Install tpfan control or the fans wont work

## s3 suspend is broken in BIOS, update to 1.35+ from lenovo

## Touchscreen stops working when resuming from suspend - to fix suspend using the power button and resume.

## Install this settings powertoy to adjust font scaling for 4k monitors and your inbuilt display

## Getting MX Master 2s to work
Use logiops
https://wiki.archlinux.org/index.php/Logitech_MX_Master
