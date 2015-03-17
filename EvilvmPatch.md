If VM is supposed to provide window manager for X11 applications, it is anyway more convenient to have some minimal window management on the host as well. When starting a VM, host's window manager should release screen to the VM's window manager.

The `patches` subdirectory of `kvmadm` contains a file named `evilwm-1.0.0-USR1USR2.diff`. It is to be applied to the source code of the [`evilwm` 1.0.0 release](http://www.6809.org.uk/evilwm/evilwm-1.0.0.tar.gz).

This patch makes evilwm to release the screen upon the `SIGUSR1` signal, and restart itself upon the `SIGUSR2` signal.

So, it is recommended to have `evilwm` running on the host, and start the VM with these commands:

```
kill -USR1 `pidof evilwm`
/usr/sbin/kvmrun NewVM
kill -USR2 `pidof evilwm`
```

If for some reason VM crashes without proper release of the screen, `evilwm` will restart itself right after the VM terminates.

