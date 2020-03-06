# pi-tools

Various tools for single board computers like Raspberry Pi, useful and not so.

## Available tools

### [create-ap](create-ap)
Creates wireless Access Point (AP) on specified interface and configure local DHCP server (dnsmasq) accordingly.

Compatible only with single AP hosts, if other APs exists their setup can be overwritten!

### [pi-img](pi-img)
Helps to manage disk images for single board computers: create, flash, mount, modify.

### [pi-reset](pi-reset)
Resets host to factory state.
Effectively it self-reflash SD card of live system from compressed disk image pack downloaded from the web.

### [pi-vol](pi-vol)
Allows to change PCM volume by quick `vol` command.
This script is just a mapping for `amixer` tool.

### [raspi-id](raspi-id)
Shows Raspberry Pi unique ID's (with additional verifications):
- CPU serial
- embedded MAC addresses (Ethernet and Wireless).

### [set-wifi-creds](set-wifi-creds)
Creates wifi configuration for wpa_supplicant based on configuration file (by default `/boot/wifi`) or based on commandline arguments, then write it to wpa_supplicant configuration file and apply changes.

The script can be added to `/etc/rc.local` to check `SRC_FILE` on every boot, or you may create separate systemd service for it.
It can be useful to setup wifi creds before OS booting by creation of file in /boot partition (which is FAT32 on Raspberry Pi, so the file can be created on Windows hosts easily).

### [show-temperature](show-temperature)
Shows temperature from builtin sensors on Raspberry Pi or some other pi's.
Just a small wrapper to access temperature information from sysfs and/or vcgencmd.

### [tricolor-led](tricolor-led)
Bash script `led` which manage tricolor green/red/orange LED using sysfs.

This is deb package sources.
