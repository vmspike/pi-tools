# set-wifi-creds

This script creates wifi configuration for wpa_supplicant based on file `SRC_FILE` (by default `/boot/wifi`) or based on commandline arguments, then write it to `WPA_SUPPLICANT_FILE` (by default `/etc/wpa_supplicant/wpa_supplicant.IFACE.conf`) and apply changes.

`SRC_FILE` (if any) have to contain 1-3 lines:
```
SSID
password
country
```
If password is empty network considered unsecure.

Country can contain two symbols of country abbreviation, see
https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2

Country length truncated to two chars, so next chars if any are ignored.
If country empty or invalid drop to 00 (World).

`SRC_FILE` if any will be removed after successful configuration.

The script can be added to `/etc/rc.local` to check `SRC_FILE` on every boot, or you may create separate systemd service for it.
It can be useful to setup wifi creds before OS booting by creation of file in /boot partition (which is FAT32 on Raspberry Pi, so the file can be created on Windows hosts easily).

From command line `SRC_FILE` can be set by:
```
set-wifi-creds -f SRC_FILE
```
Alternatively the script can be called this way (optional args are in `[]`):
```
set-wifi-creds IFACE SSID [PW] [COUNTRY] [WPA_SUPPLICANT_FILE]
```

You may use empty strings `''` if you don't want to set `PW` or `COUNTRY` but want to set `WPA_SUPPLICANT_FILE`.

Also `IFACE`, `SRC_FILE`, `WPA_SUPPLICANT_FILE` can be set as an environmental variables.
