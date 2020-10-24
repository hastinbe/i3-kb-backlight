# i3-kb-backlight

Keyboard backlight control and notifications. Written for use with [i3wm], but works with any window manager or as a standalone script.

[![License: GPL v2][license-badge]][license]

#### On-Screen Notifications

| [notify-osd] | [dunst] |
| ------------ | ------- |
| ![notify-osd](https://user-images.githubusercontent.com/195790/97069983-d8eda580-1606-11eb-9a20-ba2433043c44.png) | ![dunst](https://user-images.githubusercontent.com/195790/97069981-d723e200-1606-11eb-94d8-6bc8340f7584.png) |

| [xosd] | [herbe] |
| ------ | ------- |
| ![xosd](https://user-images.githubusercontent.com/195790/97069984-d8eda580-1606-11eb-9c5f-31a0cbee4587.png) | ![herbe](https://user-images.githubusercontent.com/195790/97069982-d8550f00-1606-11eb-98a8-42bd2b16d67f.png) |

## Installation

### Dependencies

* awk (POSIX compatible)
* bc
* [upower]

### Manual setup for [i3wm]

Clone this repository:
```bash
git clone https://github.com/hastinbe/i3-kb-backlight.git ~/i3-kb-backlight
```

#### i3wm

Edit the following example and append it to your ~/.config/i3/config:

```sh
## Keyboard backlight control

# Path to backlight script
set $backlight_path ~/i3-kb-backlight

# Amount to increase/decrease brightness
set $brightness_step 1

bindsym XF86KbdBrightnessUp   exec $backlight_path/brightness -n increase $brightness_step
bindsym XF86KbdBrightnessDown exec $backlight_path/brightness -n decrease $brightness_step
```

Reload i3 configuration by pressing `mod+Shift+r`

### Usage

Use your keyboard backlight brightness keys to increase or decrease your brightness.When notifications are enabled a popup will display the brightness level.

#### Notifications

Several different programs are supported for on-screen notifications. Including but not limited to [dunst] and [notify-osd]. See the `notifications` command for a list of supported notification methods.

### Standalone

This script does not require any particular desktop environment and can be used as a standalone script.

#### Command-line options
```bash
Usage: ./brightness [<options>] <command> [<args>]
Control keyboard backlight brightness.

Commands:
  increase <value>      increase brightness
  decrease <value>      decrease brightness
  notifications         show available notification methods
  help                  display help

Options:
  -e <expires>          expiration time of notifications in ms
  -i <icon>             name of keyboard brightness icon
  -n                    enable notifications
  -N <method>           notification method (default: libnotify)
  -p                    enable progress bar
  -h                    display help

### Examples

# Increase brightness only
./brightness increase

# Decrease brightness by 3
./brightness decrease 3

# Notifications using herbe, progress bar
./brightness -np -N herbe increase

# Notifications using libnotify with notify-send, custom icon name, expiration time of 2.5 seconds
./brightness -n -i keyboard-brightness -e 2500 increase

# Notifications using libnotify with dunstify, custom symbolic icon, custom dunstify path
env DUNSTIFY_PATH=/path/to/dunst/ ./brightness -npy -i keyboard-brightness-symbolic increase

# Notifications using XOSD
./brightness -n -N xosd increase
```

## Migrating

### Version 1.x to 2.x

Version 2 introduces commands which makes it incompatible with previous versions. Your command-line usage and/or configured hotkeys need to be updated to reflect this.

| Change | v1 | v2 |
| ------ | -- | -- |
| `-d` is now the `decrease` command | `brightness -d 1` | `brightness decrease` |
| `-i` is now the `increase` command | `brightness -i 1` | `brightness increase` |

## License

`i3-kb-backlight` is released under [GNU General Public License v2][license]

Copyright (C) 1989, 1991 Free Software Foundation, Inc.

[dunst]: https://dunst-project.org
[herbe]: https://github.com/dudik/herbe
[i3wm]: https://i3wm.org
[libnotify]: https://developer.gnome.org/libnotify
[license]: https://www.gnu.org/licenses/gpl-2.0.en.html
[license-badge]: https://img.shields.io/badge/License-GPL%20v2-blue.svg
[notify-osd]: https://launchpad.net/notify-osd
[upower]: https://upower.freedesktop.org
[xosd]: https://sourceforge.net/projects/libxosd/
