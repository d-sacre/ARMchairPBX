# ARMchairPBX
A script to facilitate the installation of asterisk/FreePBX on an ARM-based SBC (focus: Raspberry Pi 3B+) running Manjaro ARM.

## Requirements
1. Computer running Linux where you have root permissions.
2. SBC which can run Manjaro ARM <br> (list of supported devices: <https://gitlab.manjaro.org/manjaro-arm/documentation/manjaro-arm-wiki/-/wikis/Device-Support>)
3. Display, Ethernet cable/adapter (Wifi currently not supported), keyboard and mouse which can be connected to your SBC. 
4. Downloaded Manjaro ARM Image suitable for your SBC (Minimal recommended, but others should also work).
5. SD card (should be fast; recommendation: class 10) of at least 8 GB, better 16 GB.
6. SD card reader which can be used with the Linux computer.
7. Software to write Image files to SD card (recommended tool: Balena Etcher, although command line tools like `dd` can be used by experts).

## How to use this utility
1. Burn the Manjaro ARM Image on a SD card.
2. Open the ext4 ROOT-Partition on the SD card with root permissions in a file browser (command line should also work, but is trickier).
3. Locate the `manjaro-arm-oem-install` script (for a Raspberry Pi, it should be located at `/usr/share/manjaro-arm-oem-install/`).
4. Download/clone this git repository. 
5. Open the file `TOBEADDED` provided in this repository in a text editor/development enviroment and adjust the `SCRIPTPATH` variable with the information obtained in Step 3 as needed <br> (for a Raspberry Pi, the default `SCRIPTPATH="/usr/share/manjaro-arm-oem-install/manjaro-arm-oem-install"` should be correct).
6. Delete the original `manjaro-arm-oem-install` file on the SD card  and add the modified `TOBEADDED`. Rename the replacement file `TOBEADDED` to `manjaro-arm-oem-install`.
7. Copy the folder `TOBEADDED` from the downloaded git repository to the `manjaro-arm-oem-install` parent folder on the ROOT partition of the SD card (for a Raspberry Pi, the parent folder is `/usr/share/`).
8. Close all the file browsers, unmount the SD card.
9. Insert the SD card into your SBC. Connect a display, Ethernet, keyboard and mouse.
10. Power-on the SBC. After the Manjaro logo splash screen, the script will be executed. During the first boot cycle, you will need to set passwords, time zone, locales etc. 
11. After applying these inital settings, the system will automatically reboot. During the second boot cycle, all the relevant packages will be installed. Due to the fact that many have to be custom compiled from source, this can take some considerable amount of time (depending on the speed of your internet and SBC processor this could take hours).
12. After a final reboot, the automated ARMchairPBX configuration is finished. Now you can manually set the ssh behaviour/security and configure your PBX via the FreePBX web GUI (where you have to add trunk(s), extensions, inbound/outbound routes, etc.). 

## Important remarks
1. You have to manually tweak the security settings (ssh, firewall, etc.) to your requirements. The needs and technical prerequisites differ largely and therefor could not be taken into account during the automatic setup procedure.
2. Most SBCs do not react well to sudden power outages. One always has to power them off properly, otherwise data corruption will occur. It is highly recommended to install a UPS and a shutdown script, especially if one is planning to use the ARMchairPBX as ones main connection to the outside world (imagine needing to place an emergency call and the PBX does not work properly due to data corruption...).
