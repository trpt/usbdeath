# usbdeath
anti-forensic tool that writes udev rules for known usb devices and do some things at unknown usb device insertion or specific usb device removal

# Description
usbdeath is a small script inspired by [usbkill](https://github.com/hephaest0s/usbkill), "an anti-forensic kill-switch that waits for a change on your USB ports and then immediately shuts down your computer". The main differences are:
* it is written in `bash`, so literally anyone with basic programming skills could read through the code and audit it
* it is not a daemon, just a rule file manipulation script, all monitoring stuff are done by existing `udev` daemon
* it uses more identification values for usb devices (if usb device has these values) such as name and serial number

# Config
You should change some options inside the script. Specifically, turn off safe (demo) mode and edit trigger commands (default are `sync` and `poweroff`).

# Usage
`usbdeath action`

where `action` is:
`o`, `on` - activate usbdeath
`x`, `off` - temporarily deactivate usbdeath
`j`, `eject` - add entry on eject event
`g`, `gen` - generate or refresh whitelist udev rules file
`d`, `del` - delete udev rules file
`t`, `trigger` - trigger event on insertion or removal
`e`, `edit` - edit udev rules file manually
`s`, `show` - show currently connected usb devices

You should probably put this script in PATH and do not move it after activation, as rules file relies on absolute path to script. You can change this behavior in advanced config section of script though.

# Examples
*Check out connected usb devices*
`usbdeath show`
*First run, generate whitelist of connected usb devices*
`usbdeath on`
*Also add event on ejection of specific usb device, just choose one from the list*
`usbdeath eject`
*So usbdeath rules are active. You need to insert new trusted usb device, temporarily turn off usbdeath*
`usbdeath off`
*You decide to permanently add newly inserted device(s) to whitelist*
`usbdeath gen`
*And activate `usbdeath` rules again*
`usbdeath on`
*You are so badass that you can edit udev rules file manually*
`usbdeath edit`
*You messed up with editing or something went wrong, you decide to delete rules file and start over*
`usbdeath del`

# Dependencies
`bash`
modern linux os with `udev` and probably `systemd`

Tested in Arch Linux
