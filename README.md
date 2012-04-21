rpi-update
==========

An easier way to update the firmware of your Raspberry Pi

To install the tool, run the following command as root:

<pre>
wget http://goo.gl/1BOfJ -O /usr/bin/rpi-update --quiet && chmod +x /usr/bin/rpi-update
</pre>

To then update your firmware, simply run the following command as root:

<pre>
rpi-update
</pre>

After the firmware has been sucessfully updated, you'll need to reobot to load the new firmware.

This tool is experimental, and may screw up your install. If you have problems with it, post an issue to this GitHub repo and I'll see if I can help you.
