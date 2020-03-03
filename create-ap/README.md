# create-ap

This script creates wireless Access Point (AP) on specified interface and configure local DHCP server (dnsmasq) accordingly.

Compatible only with single AP hosts, if other APs exists their setup can be overwritten!

```
Usage:
    create-ap IFACE SSID PASSWORD [SUBNET] [COUNTRY] [FORWARDING] [HOSTAPD_CONF] [HOSTAPD_DRIVER]

Defaults:
  SUBNET=192.168.43.0/24
  COUNTRY=00  # 00 means World
  FORWARDING=0  # Enable/disable forwarding between interfaces
  HOSTAPD_CONF=/etc/hostapd/hostapd.conf
  HOSTAPD_DRIVER=nl80211

Depends: bash (>= 4.3), coreutils (>= 8.0), grep (>= 2.0), wpasupplicant (>= 2.0), hostapd (>= 2.4), dnsmasq (>= 2.76), iproute2 (>= 4.9), ifupdown (>= 0.8), sed (>= 4.4), systemd (>= 232), hostname (>= 3.18), iptables (>= 1.6)
```

