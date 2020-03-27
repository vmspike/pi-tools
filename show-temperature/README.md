# show-temperature

This script shows temperature from builtin sensors on Raspberry Pi or some other pi's.
Without arguments show CPU and GPU values in human readable format.
If `-r` specified, show raw CPU temperature in 0.001 °C units (e.g. 42123).
If `-rh` specified, show CPU temperature in °C units (e.g. 42.123).

To be able to run it by single letter command `t` you may put it to `/usr/local/bin/t` (or create a symlink) and make it executable by `chmod +x /usr/local/bin/t`.
