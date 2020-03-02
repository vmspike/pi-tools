# raspi-id

This script shows Raspberry Pi unique ID's (with additional verifications):
- CPU serial
- embedded MAC addresses (Ethernet and Wireless).

If `-r` or `--raw` option specified output will be without name prefixes.

By default Ethernet MAC calculated from Raspberry Pi Foundation registered
MAC prefix (b8:27:eb:) and CPU serial number, but you can force Ethernet MAC
check by `-f` or `--force-ethernet-check` option, in this case "ethtool"
required to get real Ethernet MAC.

It's generally recommended to have "ethtool" because sometimes real wireless
MAC address cannot be identified via sysfs.

Exit codes:
- 0: success (all values correct for sure)
- 2: error (some values are incorrect for sure)
- 127: invalid options
- 128: warning (some values are not trusted, can be valid but can be invalid as well)
- *: unknown - script failure (should never occur)

Single line alternatives without additional checks assuming that embedded interfaces are eth0 and wlan0 and MAC addresses was not changed:
```
echo -n 'CPU serial:   '; cat /proc/device-tree/serial-number; echo -n $'\n''Ethernet MAC: '; cat /sys/class/net/eth0/address; echo -n 'Wireless MAC: '; cat /sys/class/net/wlan0/address
echo "CPU serial:   $(read c </proc/device-tree/serial-number; echo $c)"$'\n'"Ethernet MAC: $(</sys/class/net/eth0/address)"$'\n'"Wireless MAC: $(</sys/class/net/wlan0/address)"
```
