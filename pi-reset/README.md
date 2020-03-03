# pi-reset

This script resets host to factory state.
Effectively it self-reflash SD card of live system from compressed disk image pack downloaded from the web.

All log messages (except arguments parsing) broadcasted to all live terminals on the system as well as LOG if possible.
On failure result information written to STATUS_LOG.

The whole process may take 20 minutes approximately, on slow connections can take much more.

If you have tricolor LED attached to the host (or two single color LEDs) and tricolor-led package installed you can monitor the script stages.

There are three of them:
- Preparatory: red<->orange ~2 times per second (interruption is relatively safe,
  like usual power loss)
- Intermediate: solid orange (should take not more than a few seconds)
- Flashing: red<->green ~4 times per second (interruption will cause SD card corruption,
  you'll need to reflash SD manually!)

Custom options will be loaded from config file if present. See script defaults for the syntax

Options priority: commandline options > config options > script defaults

```
Commandline options:
    --config str
        Must be the first argument if specified!
        Options from config file overrides script defaults.
        Default is /etc/pi-config.conf

    --dry-run 0|1
        If 1 do all the same except real flashing, instead unpack and flash to /dev/null
        Can be useful for testing purposes.

    --tricolor-led 0|1
        Report device state by changing tricolor LED state if tricolor LED attached to the host
        and "led" utility exists.

    --keep-ssh 0|1
        If enabled SSH connection will be preserved as long as possible and
        additional binaries will be available on ramdisk (coreutils, libs and others)
        so final rootfs will consume more RAM.
        Some low RAM hosts or big images may be unable to reset with this option.
        Approximately the image pack compressed by xz should be less than RAM size minus ~100MB.

    --allow-unverified-https 0|1
        If 1 ignore TLS cert for image downloading. It forces to use --no-check-certificate wget option.

    --img-url str
        Now it must be tar.xz (or txz) archive. Others are unsupported.

    --ram-disk-size int
        The size of RAM disk to create in bytes. Suffixes allowed: K M %
        Default is 90% of total RAM.

    --sdcard-device str
        The device to be flashed.
        Default is /dev/mmcblk0

Depends: bash (>= 4.3), coreutils (>= 8.26), grep (>= 2.27), util-linux (>= 2.29.2), mount (>= 2.29.2), psmisc (>= 22.21), iproute2 (>= 4.9.0), wget (>= 1.18), tar (>= 1.29b), xz-utils (>= 5.2.2), procps (>= 2:3.3), bsdutils (>= 1:2.29.2), openssl (>= 1.1.0f)
Recommends: tricolor-led (>= 1.0.0)
```
TODO:
- Current script state is unstable, thorough testing required.
- Use busybox for ramdisk filesystem, because the way using existing system binaries is unstable.
