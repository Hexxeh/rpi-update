# rpi-update

An easier way to update the firmware of your Raspberry Pi

## Status

This tool is experimental, and may screw up your install. If you have problems
with it, post an issue to this GitHub repo and I'll see if I can help you.

## Preparations

To prevent errors relating certificates, one can fix two possible problems.

-   Either the time is set incorrectly on your Raspberry Pi, which you can fix
    by simply setting the time using NTP.

        sudo ntpdate -u ntp.ubuntu.com

-   The other possible issue is that you might not have the ca-certificates
    package installed, and so GitHub's SSL certificate isn't trusted. If you are
    on Debian, you can resolve this by typing:

        sudo apt-get install ca-certificates

## Installing

To install the tool, run the following command:

    sudo wget http://goo.gl/1BOfJ -O /usr/bin/rpi-update && chmod +x /usr/bin/rpi-update

## Updating

To then update your firmware, simply run the following command:

    sudo rpi-update
    
### Options

By default, rpi-update will attempt to determine the split you're currently
using, and then use that split. If it cannot determine what split you are using,
it will default to 224MB. If you'd like to explicitly select a split, simply
provide the RAM split value after the command as follows:

    sudo rpi-update 192

If you'd like to use the 128MB memory split, then the command is the same as the
above, except with 128 instead of 192:

    sudo rpi-update 128

### Environment Variables

There are a number of options for experts you might like to use, these are all
environment variables you must set if you wish to use them.

#### SKIP_KERNEL

    sudo SKIP_KERNEL=1 rpi-update

Will update everything **except** the kernel.img files and the kernel modules.
Use with caution, some firmware updates might depend a kernel update.

#### ROOT_PATH/BOOT_PATH

    sudo ROOT_PATH=/media/root BOOT_PATH=/media/boot rpi-update

Allows you to perform an "offline" update, ie update firmware on an SD card you
are not currently booted from. Useful for installing firmware/kernel to a
non-RPI customised image. Be careful, you must specify both options or neither.
Specifying only one will not work.

## Activating

After the firmware has been sucessfully updated, you'll need to reboot to load
the new firmware.
