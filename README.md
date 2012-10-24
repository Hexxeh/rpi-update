# rpi-update

An easier way to update the firmware of your Raspberry Pi.

## Preparations

There are two possible problems related to SSL certificates that may prevent
this tool from working.

-   The time may be set incorrectly on your Raspberry Pi, which you can fix
    by setting the time using NTP.

        sudo ntpdate -u ntp.ubuntu.com

-   The other possible issue is that you might not have the `ca-certificates`
    package installed, and so GitHub's SSL certificate isn't trusted. If you are
    on Debian, you can resolve this by typing:

        sudo apt-get install ca-certificates

## Installing

To install the tool, run the following command:

    sudo wget http://goo.gl/1BOfJ -O /usr/bin/rpi-update && chmod +x /usr/bin/rpi-update

## Updating

Then, to update your firmware, just run the following command:

    sudo rpi-update

## Activating

After the firmware has been sucessfully updated, you'll need to reboot to load
the new firmware.

## Options

If you'd like to set a different GPU/ARM memory split, then define `gpu_mem` in
`/boot/config.txt`.

To upgrade/downgrade to a specific firmware revision, specify its Git hash
(from the https://github.com/Hexxeh/rpi-firmware repository) as follows:

    sudo rpi-update fab7796df0cf29f9563b507a59ce5b17d93e0390

### Expert options

There are a number of options for experts you might like to use.  These are all
environment variables you must set if you wish to use them.

#### `UPDATE_SELF`

By default, `rpi-update` will attempt to update itself each time it is run.
You can disable this behavior by:

    UPDATE_SELF=0 sudo rpi-update

#### `SKIP_KERNEL`

    SKIP_KERNEL=1 sudo rpi-update

Will update everything **except** the `kernel.img` files and the kernel modules.
Use with caution, some firmware updates might depend on a kernel update.

#### `ROOT_PATH` and `BOOT_PATH`

    ROOT_PATH=/media/root BOOT_PATH=/media/boot sudo rpi-update

Allows you to perform an "offline" update, ie update firmware on an SD card you
are not currently booted from. Useful for installing firmware/kernel to a
non-RPI customised image. Be careful, you must specify both options or neither.
Specifying only one will not work.
