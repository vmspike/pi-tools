# vol

Allows to change PCM volume by quick "vol" command.
This script is just a mapping for "amixer" tool.

You can choose audio device by `VOL_DEVICE` environmental variable (default is "PCM").

`alsa-utils` package required for this script usage.

Run without arguments to see inline help:
```
Usage:
    vol [unmute|on|u]
        Unmute volume.

    vol [mute|off|m]
        Mute volume.

    vol [toggle|t]
        Toggle volume (mute/unmute).

    vol [status|s]
        Show amixer's status. Use the mapped volume for evaluating the
        percentage representation like alsamixer, to be more natural for human
        ear.

    vol [+-]VALUE[%]
        Set volume level to VALUE and unmute.
        "%" sign is optional, VALUE is always percentage.
        If leading "+" or "-" specified volume will be incremented or
        decremented correspondingly and resulting value will be printed to
        stdout.

    vol [+|up|-|down]
        Just an alias for previous command with VALUE=5.
```
