rpi-update
==========

An easier way to update the firmware of your Raspberry Pi

To install the tool, run the following command as root:

<pre>
wget http://goo.gl/1BOfJ -O /usr/bin/rpi-update && chmod +x /usr/bin/rpi-update
</pre>

If you get errors relating to certificates, then the problem is likely due to one of two things. Either the time is set incorrectly on your Raspberry Pi, which you can fix by simply setting the time using NTP. The other possible issue is that you might not have the ca-certificates package installed, and so GitHub's SSL certificate isn't trusted. If you're on Debian, you can resolve this by typing:

<pre>
sudo apt-get install ca-certificates
</pre>

To then update your firmware, simply run the following command as root:

<pre>
rpi-update
</pre>


By default, rpi-update will attempt to determine the split you're currently using, and then use that split. If it cannot determine what split you are using, it will default to 224MB.

If you'd like to explicitly select a split, simply provide the RAM split value after the command as follows:

<pre>
rpi-update 192
</pre>

If you'd like to use the 128MB memory split, then the command is the same as the above, except with 128 instead of 192.

After the firmware has been sucessfully updated, you'll need to reboot to load the new firmware.

This tool is experimental, and may screw up your install. If you have problems with it, post an issue to this GitHub repo and I'll see if I can help you.

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
