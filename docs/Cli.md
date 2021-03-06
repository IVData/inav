# Command Line Interface (CLI)

INAV has a command line interface (CLI) that can be used to change settings and configure the FC.

## Accessing the CLI.

The CLI can be accessed via the GUI tool or via a terminal emulator connected to the CLI serial port.

1. Connect your terminal emulator to the CLI serial port (which, by default, is the same as the MSP serial port)
2. Use the baudrate specified by msp_baudrate (115200 by default).
3. Send a `#` character.

To save your settings type in 'save', saving will reboot the flight controller.

To exit the CLI without saving power off the flight controller or type in 'exit'.

To see a list of other commands type in 'help' and press return.

To dump your configuration (including the current profile), use the 'dump' or 'diff' command.

See the other documentation sections for details of the cli commands and settings that are available.

## Backup via CLI

Disconnect main power, connect to cli via USB/FTDI.

dump using cli

```
profile 0
dump
```

dump profiles using cli if you use them

```
profile 1
dump profile
profile 2
dump profile
```

copy screen output to a file and save it.

Alternatively, use the `diff` command to dump only those settings that differ from their default values (those that have been changed).


## Restore via CLI.

Use the cli `defaults` command first.

When restoring from backup it's a good idea to do a dump of the latest defaults so you know what has changed - if you do this each time a firmware release is created you will be able to see the cli changes between firmware versions. If you blindly restore your backup you would not benefit from these new defaults or may even end up with completely wrong settings in case some parameters changed semantics and/or value ranges.

It may be good idea to restore settings using the `diff` output rather than complete `dump`. This way you can have more control on what is restored and the risk of mistakenly restoring bad values if the semantics changes is minimised.

To perform the restore simply paste the saved commands in the Configurator CLI tab and then type `save`.

After restoring it's always a good idea to `dump` or `diff` the settings once again and compare the output with previous one to verify if everything is set as it should be.


## CLI Command Reference

| `Command`        | Description                                    |
|------------------|------------------------------------------------|
| `1wire <esc>`    | passthrough 1wire to the specified esc         |
| `adjrange`       | show/set adjustment ranges settings            |
| `aux`            | show/set aux settings                          |
| `beeper`         | show/set beeper (buzzer) usage (see docs/Buzzer.md) |
| `mmix`           | design custom motor mixer                      |
| `smix`           | design custom servo mixer                      |
| `color`          | configure colors                               |
| `defaults`       | reset to defaults and reboot                   |
| `dump`           | print configurable settings in a pastable form |
| `diff`           | print only settings that have been modified    |
| `exit`           |                                                |
| `feature`        | list or -val or val                            |
| `get`            | get variable value                             |
| `gpspassthrough` | passthrough gps to serial                      |
| `help`           |                                                |
| `led`            | configure leds                                 |
| `map`            | mapping of rc channel order                    |
| `motor`          | get/set motor output value                     |
| `msc`            | Enter USB Mass storage mode. See docs/USB_Mass_Storage_(MSC)_mode.md for usage information.|
| `play_sound`     | index, or none for next                        |
| `profile`        | index (0 to 2)                                 |
| `rxrange`        | configure rx channel ranges (end-points) |
| `save`           | save and reboot                                |
| `serial`         | Configure serial ports                         |
| `serialpassthrough <id> <baud> <mode>`| where `id` is the zero based port index, `baud` is a standard baud rate, and mode is `rx`, `tx`, or both (`rxtx`) |
| `set`            | name=value or blank or * for list              |
| `status`         | show system status                             |
| `temp_sensor`    | list or configure temperature sensor(s). See docs/Temperature sensors.md |
| `wp`             | list or configure waypoints. See more in docs/Navigation.md section NAV WP |
| `version`        |                                                |

### serial

The syntax of the `serial` command is `serial <id>  <functions> <msp-baudrate> <gps-baudrate> <telemetry-baudate> <peripheral-baudrate>`.

A shorter form is also supported to enable and disable functions using `serial <id> +n` and
`serial <id> -n`, where n is the a serial function identifier. The following values are available:

| Function              | Identifier    |
|-----------------------|---------------|
| MSP                   | 0             |
| GPS                   | 1             |
| TELEMETRY_FRSKY       | 2             |
| TELEMETRY_HOTT        | 3             |
| TELEMETRY_LTM         | 4             |
| TELEMETRY_SMARTPORT   | 5             |
| RX_SERIAL             | 6             |
| BLACKBOX              | 7             |
| TELEMETRY_MAVLINK     | 8             |
| TELEMETRY_IBUS        | 9             |
| RCDEVICE              | 10            |
| VTX_SMARTAUDIO        | 11            |
| VTX_TRAMP             | 12            |
| UAV_INTERCONNECT      | 13            |
| OPTICAL_FLOW          | 14            |
| LOG                   | 15            |
| RANGEFINDER           | 16            |
| VTX_FFPV              | 17            |

`serial` can also be used without any argument to print the current configuration of all the serial ports.

## Flash chip management

For targets that have a flash data chip, typically used for blackbox logs, the following additional comamnds are provided.

| Command | Effect |
| ------- | ------ |
| `flash_erase` | Erases the  flash chip |
| `flash_info` | Displays flash chip information (used, free etc.) |
| `flash_read <length> <address>` | Reads `length` bytes from `address` |
| `flash_write <address> <data>` | Writes `data` to `address` |

## CLI Variable Reference

See [Settings.md](Settings.md).
