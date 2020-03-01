# create-ap

This script creates wireless Access Point on specified interface and configure local DHCP server accordingly.
Compatible only with single AP hosts, if other AP exists its setup can be overwritten.

Usage:
    `create-ap IFACE SSID PASSWORD [SUBNET] [COUNTRY] [FORWARDING] [HOSTAPD_CONF] [HOSTAPD_DRIVER]`

Defaults:
- SUBNET: `192.168.43.0/24`
- COUNTRY: `00` (World)
- FORWARDING: `0` (True values: 1|true|yes|y|on|ok)
- HOSTAPD_CONF: `/etc/hostapd/hostapd.conf`
- HOSTAPD_DRIVER: `nl80211`

`hostapd` and `dnsmasq` packages required for this script.
