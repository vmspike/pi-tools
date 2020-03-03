# tricolor-led

Bash `led` script which manage tricolor green/red/orange LED using sysfs.

This is deb package sources.
For prebuilt package see https://vmspike.com/repo/pi-tools/tricolor-led/

It's recommended to install it as a package because of additional configuration done on installation:
- create required filesystem structure in tmpfs `/run/tricolor-led` on each boot (configured by tmpfiles.d of systemd)
- configure systemd "led-on-boot.service" to run on early boot to set initial led state
- set proper permissions and create gpio group if does not exists

To build deb package:
- be sure you have tools to build deb packages: `sudo apt install dh-make devscripts`
- clone this repo and go to the dir with sources, e.g. `cd ./pi-tools/tricolor-led/tricolor-led-1.0.0/`
- run `dch -i` to set proper changelog entry
- run `cd ./` to apply changed PWD (if dch have renamed current dir)
- build the package: `debuild -uc -us -b`, if all is fine you'll find it in parent dir `../`

Output of `led man`:
```
DESCRIPTION
    Help to manage tricolor green/red/orange LED using sysfs.
    Allow to set solid colors, blinking sequences, and check LED state.

    LED_GPIO1 and LED_GPIO2 environmental variables can be set to replace
    default GPIO pins: 16 26.

    Only "gpio" group members and root can use this tool.

USAGE
    led [ACTION] [OPTIONS]

ACTION
    help, --help, usage, man
        Print this help.
        The text outputs to stderr and exit code is 255.

        Action "man" behave a bit differently: try to print using pager
        ("less" or "more" in most cases) or stdout if no pager. Exit code in
        this case is equal to pager exit code.

    export, e
        Export GPIO in sysfs for the LED. In most cases do not need to call it
        explicitly.

    unexport, u
        Unexport GPIO for the LED from sysfs. The LED will be switched off in
        this case.

    [solid] green, g
    [solid] red, r
    [solid] orange, o
    [solid] off, 0
        Set corresponding solid color. If any blinking process exists it will
        be preliminary killed. 'solid' argument is optional, will be removed if exists.

    blink [INTERVAL] [COLOR]...
    b     [INTERVAL] [COLOR]...
        Run/replace background process with blinking sequence.

        INTERVAL between blink can be set as a float or integer number of
        seconds or via text alias:
            snail,  xs: 2
            slow,    s: 1
            medium,  m: 0.5
            fast,    f: 0.25
            falcon, xf: 0.125

        COLOR is a sequence of colors. See EXAMPLES section for more info.

        If only one color specified 'off' color will be added automatically for blinking.
        If no colors specified default color sequence will be used: red orange green off
        If no INTERVAL specified default value will be used: 0.5

    [ALIAS]
        Example: disaster, ok, netfail, boot, upgrade, vague...
        LED state aliases for various use cases. Set predefined LED state.

        For other available aliases and specified sequences for them see the
        dictionary ALIASES in source code. You can customize that dictionary
        if you wish.

    state, s
        Check existing LED state. For solid colors it shows full color name,
        for blinking state show space separated line:
            blink INTERVAL [COLOR]...
        where INTERVAL is a float or int number, each of COLOR is a full color
        name: green, red, orange, off.

        If GPIO sysfs is unexported or LED color check failed it shows
        nothing and exit with the code 1.

    alias, a
        Similar to state action but show the state alias (if defined) or
        nothing if no aliases defined for it.

        Example:
            Current state is
                blink 1 red off
            and ALIASES dictionary has item specified as
                [disaster]='blink slow red off'
            and BLINK_INTERVAL_ALIASES has item specified as
                [slow]=1
            output will be:
                disaster

    save [FILE]
        Save current state to the file.
        If FILE specified save to that file instead of the default.

        Saved state will be printed to stdout (with prefix line "Saved:" on
        stderr).

    restore [FILE]
        Restore LED state from the file. Inverse of "save" action.
        If FILE specified restore from that file instead of the default LED_SAVEFILE.
        Default LED_SAVEFILE value is /run/tricolor-led/led.state

        Restored state will be printed to stdout (with prefix line "Restored:"
        on stderr).

    version, --version
        Show script version and exit.

EXAMPLES
    - Set solid green (alias: ok)
        led green
        led g
        led ok

    - Check current LED state
        led state
        led s

        Output:
            green

    - Unexport LED on GPIO sysfs
        led unexport
        led u

    - Blink fast with red color
        led blink fast red
        led b f r
        led b f r 0
        led blink 0.25 red off

    - Blink with long sequence with double intervals for some colors
        led blink medium green red orange orange red green off off
        led b m g r o o r g 0 0

    - Check state again
        led s

        Output:
            blink 0.5 green red orange orange red green off off

        As you can see status output can be reused as arguments for led
        command.

    - Check existing state and its alias
        led s && led a

        Output example:
            blink 0.25 red orange
            boot

    - Save existing state
        led save  # To default file
        led save /path/to/my/fancy/led.state  # To custom file

    - Restore previous LED state
        led restore  # From default file
        led restore /path/to/my/fancy/led.state  # From custom file

        Using "restore" action you can implement custom state aliases without
        code changes:
            echo 'blink fast g r o 0 o r g 0' >./joy
            echo 'blink snail o 0' >./slowpoke
            echo 'orange' >./boring
            led restore ./slowpoke

        Feel free to add state aliases to ALIASES dictionary if you're able to change the code.
```
