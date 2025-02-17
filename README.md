# Steam-Deck.Mount-External-Drive 3.5
Script to Auto-Mount NTFS, BTRFS & exFat SDCards, External USB Drives (or SSD Docks) & Internal Partitions (If you Dual-Boot) on the Steam Deck

NTFS & BTRFS Partitions containing a SteamLibrary at root level or in a folder named `SteamLibrary` will automatically be added to Steam, exFAT isn't supported as a SteamLibrary but will be Mounted for use with other Launchers or for Media/ROMs etc.

# "This is cool! How can I thank you?"
### Why not drop me a sub over on my youtube channel ;) [Chinballs Gaming](https://www.youtube.com/chinballsTV?sub_confirmation=1)

### Also [Check out all these other things I'm making](https://github.com/scawp/Steam-Deck.Tools-List)


# Steam OS 3.5 Now supports Ext4 external Drives out the box so see **Uninstall** if thats all you need!

Not only that but Valve have also improved their SD card mounting script (No More SD Card Bricking!!!* *maybe...) 

So now my script (the one you are looking at now) is basically a mirror of that but replacing `ext4` with `ntfs`, `btrfs` & `exFAT` and adding rules for Internal Partitions.

Looking for the old code? see https://github.com/scawp/Steam-Deck.Mount-External-Drive/tree/pre-3.5

# How does this work?

a `udev` rule is added to `/etc/udev/rules.d/98-external-drive-mount.rules`
which calls systemd `/etc/systemd/system/external-drive-mount@[sda1|sda2|sdd1|etc].service`
that then runs `automount.sh` to Auto Mount any NTFS SD/External USB/Internal Partitions.

`/etc/fstab` is not required for mounting in this way, (however if a Device has an `fstab` entry these scripts will still work)

# Video Guide

https://www.youtube.com/watch?v=Yglf1EKBv2A

# Operation

The Drive(s) will be Auto-Mounted to `/run/media/deck/[LABEL]` eg `/run/media/deck/External-ssd/` if the Device has no `label` then the Devices `UUID` will be used eg `/run/media/deck/a12332-12bf-a33ab-eef/`

~The install will also offer an optional install of `zMount.sh` which will be added to your Steam Library as a non-steam game which can be ran from `GameMode`, this will allow manual (un)mounting of USB Devices and the SD-Card. (NOTE: This is probably more useful for unmounting as the auto mount script should mount anything anyway).~ No longer required, can unmount from `settings>storage`

# Installation

## Via Curl (One Line Install)

In Konsole type `curl -sSL https://raw.githubusercontent.com/scawp/Steam-Deck.Mount-External-Drive/main/curl_install.sh | bash`

a `sudo` password is required (run `passwd` if required first)

# Uninstall

`sudo rm /etc/udev/rules.d/99-external-drive-mount.rules`

`sudo rm /etc/udev/rules.d/98-external-drive-mount.rules`

#Note: ones of these may not exist depending on the version of my script you originally installed.

`sudo rm /etc/systemd/system/external-drive-mount@.service`

`sudo rm -r /home/deck/.local/share/scawp/SDMED`

`sudo udevadm control --reload`

`sudo systemctl daemon-reload`

# WORK IN PROGRESS!

This will probably have bugs, so beware! log bugs under [issues](https://github.com/scawp/Steam-Deck.Mount-External-Drive/issues)!
