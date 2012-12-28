rpi-update
==========

An easier way to update the firmware of your Raspberry Pi

Instructions
------------

To install the tool, run the following command:

<pre>
sudo wget http://goo.gl/1BOfJ -O /usr/bin/rpi-update && sudo chmod +x /usr/bin/rpi-update
</pre>

If you get errors relating to certificates, then the problem is likely due to one of two things. Either the time is set incorrectly on your Raspberry Pi, which you can fix by simply setting the time using NTP. The other possible issue is that you might not have the ca-certificates package installed, and so GitHub's SSL certificate isn't trusted. If you're on Debian, you can resolve this by typing:

<pre>
sudo apt-get install ca-certificates
</pre>

To then update your firmware, simply run the following command:

<pre>
sudo rpi-update
</pre>

To upgrade/downgrade to a specific firmware revision, specify it's Git hash as follows:

    rpi-update <git hash>

If you'd like to set a different GPU/ARM memory split, then define gpu_mem in /boot/config.txt.

Expert options
--------------

There are a number of options for experts you might like to use, these are all environment variables you must set if you wish to use them.

### SKIP_KERNEL

#### Usage

SKIP_KERNEL=1 rpi-update

#### Effect

Will update everything EXCEPT the kernel.img files and the kernel modules. Use with caution, some firmware updates might depend a kernel update.

### ROOT_PATH/BOOT_PATH

#### Usage

ROOT_PATH=/media/root BOOT_PATH=/media/boot rpi-update

#### Effect

Allows you to perform an "offline" update, ie update firmware on an SD card you're not currently booted from. Useful for installing firmware/kernel to a non-RPI customised image. Be careful, you must specify both options or neither. Specifying only one will not work.
