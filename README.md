# Arch Overlay-ed Root

This overlay is really fairly simple with the option of disabling it through kernel parameters.

The `/var` directory is mounted `rw` from the lower filesystem because I'm mainly too lazy to separate the proper directories to make sure that Docker works properly.

## Installation

1. Create hook and install scripts according to this repository's directory structure
2. Update `MODULES` and HOOKS with `MODULES=(overlay ...)` and `HOOKS=(... overlayroot)`
3. Run `mkinitcpio -P`
4. Update kernel boot parameters to include `overlayroot=enable`
5. Add a new boot entry that contains `overlayroot=disable` as a maintenance option to update the system and fix potential issues with the overlay.

## Example Systemd Boot entry

```conf
title   Arch Linux (Crypt / LVM / Overlayed)
linux   /vmlinuz-linux
initrd  /initramfs-linux.img
options cryptdevice=PARTUUID=2d781b26-0285-421a-b9d0-d4a0d3b55680:cryptlvm root=/dev/lvm/root overlayroot=enable nvidia-drm.modeset=1 nvidia-drm.fbdev=1
```

## My system setup

- Luks encrypted volume
- LVM with separated `/` and `/home` partitions
