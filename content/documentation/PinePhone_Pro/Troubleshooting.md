---
title: "Troubleshooting"
draft: false
menu:
  docs:
    title:
    parent: "PinePhone_Pro"
    identifier: "PinePhone_Pro/Troubleshooting"
    weight: 5
---

If the PinePhone Pro is not booting (either booting incompletely into a boot splash or tty or if the PinePhone Pro is showing no signs of life) this will typically have the following two reasons:

## The battery is fully drained

If the battery is drained then the board can reset during boot causing a boot loop because of undervoltage condition. It can happen on all stages of the boot including _U-Boot_ bootloader, display initialization and USB (re-)configuration. In that case it is not possible to charge the phone. The battery can be charged by interrupting the boot loop by booting the PinePhone Pro into _Maskrom mode_ or by charging the battery externally. It is possible to follow these instructions without a computer by using a wall charger, however it would not be possible to determine if Maskrom mode was started successfully. To boot the PinePhone Pro into _Maskrom mode_:

* Remove any microSD card from the phone and keep it removed for the below procedure
* Remove the battery, any USB cable and any serial cable
* Reinsert the battery
* Hold the _RE_ button underneath the back cover of your _Explorer Edition_ (or short the bypass contact points on the _Developer Edition_)

{{< admonition type="note" >}}
 Confirm that the label of the button says _RE_ and not _RESET_! If the button label says _RESET_ instead you probably have a regular PinePhone and you’re reading the wrong page.
{{< /admonition >}}

* Connect the phone to an USB port of a computer, while still holding the button for some time
* Confirm if the phone was booted in Maskrom mode:
  * On _Linux_ check if the Maskrom mode appears as device in the output of the terminal command `lsusb` on the computer, the expected _VID:PID_ of the device is _2207:330c_.
  * On _Windows_ this can be checked using the _Device Manager_ and checking the VID "2207" and PID "330c" of an _Unknown device_ appears.
  * On _macOS_ this can be checked in _/Applications/Utilities/System Information.app_ under _USB_ and by checking if the VID "2207" and PID "330c" is appearing for a _Composite Device_.
* Let the phone charge for multiple hours

{{< admonition type="note" >}}
 If the device doesn’t appear under _lsusb_ please try again with a different known good USB-C cable and make sure that there is no microSD card in the phone inserted.
{{< /admonition >}}

The device should now be able to boot from the boot medium again. If that is not the case the installation got corrupted, as explained below.

## The installation is corrupted

The PinePhone Pro won’t be able to boot if the installation on the SPI flash, the eMMC or the microSD card got corrupted. To boot a working operating system:

* Prepare a microSD card as explained in the section [Flashing to microSD card](/documentation/PinePhone_Pro/Installing_a_different_operating_system)
* Remove any USB-C cable or device or add-on case from the PinePhone Pro
* Make sure the device is powered off by shortly removing the battery for a second
* Insert the microSD card into the top slot of the PinePhone Pro. Make sure the microSD card is inserted all the way and that the notch of the right side of the microSD card is not visible anymore.
* Power on the device (bypassing the SPI and eMMC might be required, see [Boot order](/documentation/PinePhone_Pro/Software/Boot_order))

The device should now boot from the microSD card. If the phone does not boot from the microSD card the microSD card was flashed with an incompatible image or the battery got drained as explained above.
