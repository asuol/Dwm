# Dwm
Dwm window manager patches

This repository contains patches to dwm and scripts that I use with DWM 6.1

Safe Shutdown:

Being minimalistic, Dwm lacks a shutdown function. Although the shutdown command can be used, it does not gracefully close the open applications.

The "dwm.c.diff" patch allows dwm to forward the NetCloseWindow signal (the signal issued to a program when the close window is invoked) to the xorg server.

This allows the usage of the wmctrl program to send a close window command (same as the default MODKEY + SHIFT + c) to any open window on dwm.

The "safe-shutdown" script retrieves the list of open windows, and sends a close window signal to each. After a 1 second delay to allow the programs to gracefully close the script lists all the open windows again.
If no window is left open, invokes the shutdown command to shutdown the machine. If any window is still open, switch to the first open window and end the script. 

It is up to the user to check why the program is still running (maybe it needs more than 1 second to wrap up, or maybe you had unsaved data). After everything is sorted you can call the safe-shutdown script again to shutdown the machine.

Instructions:

1. Install "wmctrl" (Gentoo: emerge -av wmctrl | Debian: apt-get install wmctrl)
2. Apply the "dwm.c.diff" patch to the dwm.c file
3. Re-compile dwm
4. Copy the "safe-shutdown" script to /usr/local/bin, make it executable and enjoy! Just call "safe-shutdown" from dmenu when the day is over!
5. A safe-reboot script can be created as well, just switch the /sbin/shutdown line to /sbin/reboot if that is an use case for you
