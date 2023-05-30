---
title: How to burn ISO image to USB stick drive on Ubuntu
date: 2019-04-26
redirect_from: /how-to-burn-iso-image-to-usb-stick-drive-on-ubuntu/
---
Burning ISO to a usb stick drive is very easy in Ubuntu and all the necessary applications are already installed for you. Bear in mind that you should be able to use command line (terminal).

First plug in the usb stick drive.

Find out where it’s mounted with `sudo fdisk -l`.

Then unmount the drive with `sudo umount /dev/sdX`. Make sure to change the sdX to your specific case.

Now you are ready to burn the image into the drive. Use the following command of dd:`sudo dd bs=4M if=/PATH/TO/THE/ISO/FILE of=/dev/sdX`

You can monitor the process of dd by running the following command:`sudo kill -USR1 $(pgrep ^dd)`

The kill command doesn’t actually kill the command but instead dd will output information about the process.