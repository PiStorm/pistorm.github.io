---
title: Setting up Picasso96 with Emu68
classes: single
permalink: "/tutorials/p96setup/"
---

In this short tutorial I will try to guide you over the installation of the Picasso96 (P96) subsystem on Emu68 with PiStorm to allow for use of RTG. The guide works both for systems with some software installed already as well as freshly installed environments.

### Important!

The emu68-vc4.card driver does not reconfigure the HDMI port. The port configuration is only done only once during startup of the VPU processor. Therefore, if you want to use the Emu68 RTG feature, please make sure that you have some sort of device (monitor, framegrabber, active splitter etc...) already attached to the HDMI port when powering on your Amiga.

First of all, you need to get a copy of P96. You can find an older version on Aminet, but if you prefer the most recent version with several bug fixes and improvements, go to the iComp website and obtain it there. Subsequently, prepare an ADF image (for example on WinUAE) where you will put

1. P96 archive: [AmiNet version](https://aminet.net/package/driver/video/Picasso96)
2. emu68-vc4.card or VideoCore.card file: [You can find it in Emu68-tools package](https://github.com/michalsc/Emu68-tools/releases)
3. Lha if you don't have it yet: [Get from Aminet](https://aminet.net/package/util/arc/lha)

![step_01](/assets/images/p96/step_01.png)

Boot Emu68 and copy the contents of your floppy image to RAM. Once you did it, you can safely remove the floppy from the drive as it will not be necessary anymore. Now, start a new CLI window. If you don't have LhA installed on your system yet, execute the ``lha.run`` file. If will unpack few versions of the LhA executable. Copy the one you prefer to C: and name it ``LhA``. Now you can unpack ``Picasso96.lha`` archive by typing

```shell
lha x Picasso96.lha
```

![step_02](/assets/images/p96/step_02.png)

Once the installer is decompressed, you may start the installation process now. It is important to select **at least one** graphics card to install. If you don't, the P96 installer will not create the necessary file in DEVS:Monitors. In my case I have selected PicassoIV, but any card should be fine.

![step_03](/assets/images/p96/step_03.png)

Complete the installation of P96 now, but **do not restart** your machine yet. Instead, copy the emu68-vc4.card to the picasso96 sub-folder in libs

```shell
copy RAM:emu68-vc4.card LIBS:Picasso96/
```

Go to ``Devs/Monitors`` on your Workbench partition. You will find the PicassoIV icon there. If you don't care about the name, leave it with the existing name or you can rename it to something like ``Emu68-VC4``. It is just a cosmetic change so it is not really important. Now, open the ``Information`` about that icon and go to the tool types. Locate the entry ``BOARDTYPE``  and change it to ``Emu68-VC4``. Save the changes.

### Important!

As of version 1.2.1 of Videocore, an additional step is required if you are using the Aminet version of P96. You also need to add the ``VC4_LEGACY_ID`` tooltype. Go to the Tooltypes section and add this as a separate line. While the order the line appears in in the list of Tooltypes is  important, it must be on a separate line.

Save the changes.

![step_04](/assets/images/p96/step_04.png)

Now it is the time to reboot your machine. At this point you will still be using your existing screenmode so Workbench will be showing on a regular PAL (or NTSC) screen. Go to your Prefs folder on Workbench partition and open Picasso96Mode. It is rather empty so it has to be populated now. First, create new setting by dragging "New Item" icon to Settings area of the window. Drop it there

![step_05](/assets/images/p96/step_05.png)

Give this setting a name, keep it short. Something like ``VC4`` should be just fine. Now, attach the setting to the Emu68 VC4 board (via the pull down menu)

![step_06](/assets/images/p96/step_06.png)

Use the same technique to populate resolutions. Create at least one, something like 640x480 should be fine as a first try. Subsequently, for every resolution you have created, attach the color modes, e.g. 256colors, HiColor, TrueAlpha. You can of course add more color modes to a single resolution if you wish.

Now, this is the moment where you can press the ``Test`` button and actually see the created video mode on HDMI output from your RaspberryPi! Save the changes, Picasso96Mode will inform you that a reboot is necessary now. Just follow the instruction in the dialog box and the machine will be rebooted.

Once you are back in Workbench, open the ScreenMode preferences. You will see the newly created video mode(s) now. Select the one you like, test it, and either use it or save the settings. You should now be using a RTG screenmode!

![step_07](/assets/images/p96/step_07.png)

Well, that's all. Thank you for reading and I wish you a lot of joy with Emu68 and RTG :)

![step_08](/assets/images/p96/step_08.png)
