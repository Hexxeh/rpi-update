# rpi-update

An easier way to get the latest firmware for your Raspberry Pi.

# Notes

This is only intended for use with Raspbian. If you are using a different
distribution then check with the maintainers if using rpi-update is safe.

If the distribution ships a custom kernel, then it almost certainly is not
safe. Also differences in the usage of /boot and /opt/vc directories will
likely make it unsafe.

Even on Raspbian you should only use this with a good reason.

This gets you the latest bleeding edge kernel/firmware.
There is always the possibility of regressions.

Bug fixes and improvements will eventually make their way into new Raspbian
releases and apt-get when they are considered sufficiently well tested.

A good reason for using this would be if you like to help with the testing effort,
and are happy to risk breakages and submit bug reports. These testers are welcome.

Also if you are suffering from a bug in current firmware (perhaps as one of
the reporters of the bug on github or forum) and a fix has been pushed out for
testing, then using rpi-update is the right way to get the fix until it makes
its way into new Raspbian images and apt-get.

Backing up before updating is always advisable.

## Installing

### Installing under Raspbian
 
To install the tool, run the following command:

    sudo apt-get install rpi-update

### Installing under other OSes

To install the tool, run the following command:

    sudo curl -L --output /usr/bin/rpi-update https://raw.githubusercontent.com/Hexxeh/rpi-update/master/rpi-update && sudo chmod +x /usr/bin/rpi-update

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

    sudo UPDATE_SELF=0 rpi-update

#### `SKIP_KERNEL`

    sudo SKIP_KERNEL=1 rpi-update

Will update everything **except** the `kernel.img` files and the kernel modules.
Use with caution, some firmware updates might depend on a kernel update.

#### `SKIP_BACKUP`

    sudo SKIP_BACKUP=1 rpi-update

Avoids making backup of /boot and /lib/modules on first run.

#### `SKIP_REPODELETE`

    sudo SKIP_REPODELETE=1 rpi-update

By default the downloaded files (/root/.rpi-firmware) are deleted at end of update.
Use this option to keep the files.

#### `ROOT_PATH` and `BOOT_PATH`

    sudo ROOT_PATH=/media/root BOOT_PATH=/media/boot rpi-update

Allows you to perform an "offline" update, ie update firmware on an SD card you
are not currently booted from. Useful for installing firmware/kernel to a
non-RPI customised image. Be careful, you must specify both options or neither.
Specifying only one will not work.

#### `BRANCH`

By default, clones the firmware files from the master branch, else uses the files
from the specified branch, eg:

    sudo BRANCH=next rpi-update

will use the 'next' branch.

#### `PRUNE_MODULES`

Allows you to delete unused module directories when doing an update. Set it equal to a non-zero value and it will remove all modules except the latest installed:

    sudo PRUNE_MODULES=1 rpi-update

will remove previously installed module files. Use this option to free disk space used by older module updates.

#### `JUST_CHECK`

To just get a list of commits contained in rpi-update since you last updated, run:

    sudo JUST_CHECK=1 rpi-update

This won't update your firmware

#### `GITHUB_API_TOKEN`

By default, `rpi-update` will not use a custom GitHub API token. If you run into rate limiting issues, you can supply an API token on the command line:

	sudo GITHUB_API_TOKEN=<your API token> rpi-update

## Troubleshooting

There are two possible problems related to SSL certificates that may prevent
this tool from working.

-   The time may be set incorrectly on your Raspberry Pi, which you can fix
    by setting the time using NTP.

        sudo apt-get install ntpdate
        sudo ntpdate -u ntp.ubuntu.com

-   The other possible issue is that you might not have the `ca-certificates`
    package installed, and so GitHub's SSL certificate isn't trusted. If you are
    on Debian, you can resolve this by typing:

        sudo apt-get install ca-certificates
