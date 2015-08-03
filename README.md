# usb_modeswitch for FreeBSD

## Why?

Simply because I, initial porter wanted to make a Huawei 3G E3531-s2 
stick run on FreeBSD since it "just worked"(tm) on my Linux laptop
but not my FreeBSD hackery router.

## Goals

On Linux udev/systemd-udev, in conjunction with usb-modeswitch
can look up in its udev rules for whether special action is needed
upon certain acivity such as insertion of a device.

usb_modeswitch_dispatcher (usb_modeswitch.tcl) is a wrapper script
that figures out the right data needed for usb_modeswitch and looks
up the right options needed to switch the device if known from the
usb-modeswitch-data package.

This Linux-specific part is missing for FreeBSD: We have devd(8) 
and usb_modeswich but no usb_modeswitch_dispatch, so that's what 
this is about.

Another issue to tackle later on is an equivalent to the script in the
usb-modeswitch-data package that generates udev rules, but we'd need
rules to be format in the format devd(8) likes.

### Upstream work

I do hope that upstream is willing to include patches, so yes, that's
a main cause usb_modeswitch_bsd.tcl sticks with Tcl.

## Why this should not be needed - possibly

FreeBSD has, at least for u3g(4) the ability to add usb_quirks(4)
but your modem or $device (and there often many variations) may not
be covered by FreeBSD yet.

However usb_modeswitch runs on FreeBSD, and the usb-modeswitch-data
package contains a rather large collection of switching instructions
people have found to work on Linux. - So why not make use of it?

## Portability

The first focus is FreeBSD, however since DragonFly BSD also has
devd(8) it might be possible to extend to this.

Apparently NetBSD has devpubd(8) which is quite different and its
main job is to create device nodes. OpenBSD and bitrig are unknown.

## License

Sticks with the upstream usb-modeswitch project, that means since code
is derived, its GPLv2+.