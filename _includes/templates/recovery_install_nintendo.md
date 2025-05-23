## Pre-Install Information

LineageOS builds for this device support the following device configurations:

Configuration 1:
* An original, exploitable "v1" Nintendo Switch with your preferred JoyCons attached during installation
    {% include alerts/note.html content="This can usually be identified by the model number 'MOD.' on the rear of the device. *Most* `HAC-001` models are exploitable (you can check if your particular device is compatible [here](https://suchmememanyskill.github.io/guides/switchserials/)), while `HAC-001(-01)`, or any other model number is not, and therefore you must use Configuration 2." %}
* An RCM Jig such as [this one](https://www.amazon.com/Nintendo-Switch-Short-Connector-Recovery/dp/B07J9JJRRG))
* Hekate `v6.1.0` or newer loaded via a Fusee launcher such as [this one](https://webrcm.github.io)
    {% include alerts/warning.html content="This configuration requires that the Fusee launcher be ran every time you wish to boot Android! With this in mind, Configuration 2 is heavily preferred." %}

Configuration 2:
* A hard-modded (often called "ModChipped") Switch v1 / v2 / Lite / OLED with your preferred JoyCons attached during installation
* The latest Hekate on your SD Card, and loaded by your ModChip

Additionally, we support two installation locations:
* SD Card
    {% include alerts/warning.html content="This installation location requires a high quality, high speed SD Card to function." %}
* eMMC
    {% include alerts/warning.html content="This installation location requires space be taken from HOS (the stock Switch OS), so please tread carefully." %}

This guide will detail SD Card installation, if you wish to install Android to the eMMC, you will need to consult external resources.

Additionally, this guide will not detail exploiting or ModChipping your Switch, or the installation of Hekate, so please go select the applicable/preferred installation configuration to your device, and come back when Hekate `v6.1.0` or newer is booted on the device.

## Partitioning the System
1. Please back up ALL data on the SD Card before proceeding with installation, as all data/games/save data stored on the SD Card will be erased in the process of installation.
    {% include alerts/warning.html content="Upgrades, or dirty-installs from any unofficial build will NOT function, please start with a freshly partitioned system." %}
    {% include alerts/warning.html content="Please note that the files you have just copied in prior steps will be backed up and restored onto the SD Card by Hekate." %}
3. In Hekate, select "Tools" in the top-center of the screen, then "Partition SD Card", then click "OK" when prompted.
4. Now, make your partition scheme selections based on your needs, as well as any other operating systems you may plan to install alongside Android.
    {% include alerts/note.html content="Please give Android no less than roughly 10 GB to ensure that enough space is present." %}
5. When content with your selections, click "Next Step" in the bottom-right of the screen, then when ready click "Start", and the safety pause period is complete, press the Power Button to proceed.
    {% include alerts/warning.html content="Please ensure that you select 'Dynamic: Android 13+' when prompted." %}
    {% include alerts/warning.html content="If you were on ANY prior Switchroot/Unofficial release of ANY version, you MUST repartition your SD Card, there is no upgrade path." %}
6. When this process completes, you will be presented with several options, select "SD UMS" when prompted.

## Preparing the SD Card
1. Connect your device to your PC, and navigate to your SD Card once it is mounted.
2. Please download the following files from [here](https://lineage-downloads.mainlining.org/devices/{{ device.codename }}/builds) and place them in the noted folders (which you will potentially have to create) on your device's SD Card:
   * `boot.img` -> `switchroot/install/boot.img`
   * `recovery.img` -> `switchroot/install/recovery.img`
   * `nx-plat.dtimg` -> `switchroot/install/nx-plat.dtimg`
   * `bl31.bin` -> `switchroot/android/bl31.bin`
   * `bl33.bin` -> `switchroot/android/bl33.bin`
   * `boot.scr` -> `switchroot/android/boot.scr`
    {% include alerts/warning.html content="Please ensure that the name, path, and case of these files all match the above list identically." %}
3. Please download the following files and place them in the noted folders (which you will potentially have to create) on your device's SD Card:
   * [`bootlogo_android.bmp`]({{ "images/device_specific/nx/bootlogo_android.bmp" | relative_url }}) -> `switchroot/android/bootlogo_android.bmp`
   * [`icon_android_hue.bmp`]({{ "images/device_specific/nx/icon_android_hue.bmp" | relative_url }}) -> `switchroot/android/icon_android_hue.bmp`
4. Create a new text file called `android.ini` at `bootloader/ini/android.ini` and populate it with the following:
```
[LineageOS]
l4t=1
boot_prefixes=switchroot/android/
id=SWANDR
icon=switchroot/android/icon_android_hue.bmp
logopath=switchroot/android/bootlogo_android.bmp
r2p_action=self
; alarms_disable=1 uncomment to disable notifications for better battery life
; touch_skip_tuning=1 uncomment if your touchscreen is broken
; usb3_enable=1 uncomment for faster USB at expense of WiFi/BT quality
; ddr200_enable=1 uncomment for faster SD speed on models that support it (Samsung enabled by default)
; emmc=1 uncomment to boot from the internal eMMC (not reccomended, and requires a signifigantly different set of installation instructions/partitioning process)
```
5. Safely eject the SD Card from your PC's file browser, then click "Close" on the device, then the "X" icon in the top right of the screen, and finally the "Home" button in the top-left of the screen.
6. Now select "Flash Android", go through the process, then when asked if you'd like to reboot into recovery, click "No".
7. When the process is complete, navigate to the Hekate's main menu by clicking "X Close" in the top right of the screen.
8. In Hekate, select "Nyx Settings" in the bottom-left of the screen, then "Dump Joy-Con BT" from the top-right.
9. Click "OK" once a message indicates success, the message will look like this:
```
Success!
Found 2 out of 2 Joy-Con Pairing data!
Both pairing data are HOS based!
```
    {% include alerts/note.html content="You must have booted HOS (the stock Nintendo Switch OS) with your preferred JoyCons attached prior to doing this, or it will likely not succeed. You may boot to HOS at this point if necessary, and re-run this specific step after reboot." %}
10. When the process is complete, navigate to the Hekate's main menu by clicking "X Close" in the top right of the screen. Then select "More Configs", hold the Volume Up button, and select the "LineageOS" option to boot into recovery. Do not release the Volume Up button until you see the LineageOS splash screen.
    {% include alerts/note.html content="If any messages display in the top left of the LineageOS splash screen, please start again and follow the guide more carefully." %}
    {% include alerts/warning.html content="Please note that all references to wiping/formatting  `Internal Storage` in LineageOS Recovery refers **only** to the `/data` and `/cache` partitions of your Android installation. None of these actions are capable of wiping/formatting your HOS (the stock Nintendo Switch OS), or HOS Data SD Card partition." %}
