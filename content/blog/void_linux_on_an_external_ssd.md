---
title: "Installing Void Linux on an External SSD"
author: "Jaedeok Kim"
date: "2025-09-28"
tags: ["linux", "rootfs", "void-linux"]
---

Welcome to Jae's Tech Tips.

As my first blog post, I decided to write a tutorial about installing [Void Linux](https://voidlinux.org/) on an external SSD **from another Linux distribution**. This might be helpful for those like me who is forced to use Windows at work, but prefer using Linux at home. 

Let's get started by connecting your external SSD to your computer:

<!-- `keyboard.vusb.enable = "TRUE"` -->

```console
# fdisk -l

(...)

Disk /dev/sdb: 29 GB, 30765219840 bytes, 60088320 sectors
29340 cylinders, 64 heads, 32 sectors/track
Units: sectors of 1 * 512 = 512 bytes

Disk /dev/sdb doesn't contain a valid partition table
```

<br />

### Partitioning the device

Now that we know `/dev/sdb` refers to the external device, we can start partitioning it.

```console
# wipefs -a /dev/sdb
# cfdisk /dev/sdb
```

- Label Type: `gpt`
    - `/dev/sdb1` (128M): "EFI System"
    - `/dev/sdb2` (2G): "Linux Swap"
    - `/dev/sdb3` (26.5G): "Linux Filesystem"

**Don't forget to write the partition table before quitting `cfdisk`!**

```
Syncing disks.
```

<br />

### Making file systems

Next, we need to make a file system on each partition:

```console
# mkfs.vfat /dev/sdb1
# mkswap /dev/sdb2
# mkfs.ext4 /dev/sdb3
```

Let's mount each partition as follows:

```
# mount /dev/sdb3 /mnt/
# mkdir -p /mnt/boot/efi/
# mount -t vfat /dev/sdb1 /mnt/boot/efi/
```

Optionally, if you're working in a virtual machine:

```
# mount -o rbind /dev /mnt/dev
# mount -o rbind /proc /mnt/proc
# mount -o rbind /sys /mnt/sys
```

<br />

### Bootstrapping via `chroot`

We're going to install Void Linux by unpacking the ['rootfs'](https://docs.voidlinux.org/installation/guides/chroot.html) tarball first, and then entering the `chroot` environment to configure the base system:

```console
# wget https://repo-default.voidlinux.org/live/current/void-x86_64-ROOTFS-20250202.tar.xz 
# tar xvf void*.xz -C /mnt && cp /etc/resolv.conf /mnt/etc/resolv.conf
# chroot /mnt/ /bin/bash

bash-5.2# 
```

It's time to install mandatory packages such as `base-system` and `xtools`:

```console
bash-5.2# xbps-install -Su xbps && xbps-install -u
bash-5.2# xbps-install base-system xmirror xtools
bash-5.2# xbps-remove base-container-full
```

<br />

### Installing additional packages

Here's the list of packages that I find necessary or very useful:

```console
bash-5.2# xbps-install acpi alsa-pipewire base-devel blueman bluez \
    btop chezmoi chrony cmatrix curl dbus elogind eudev eudev-libudev \
    fastfetch git grub-x86_64-efi libspa-bluetooth lynx NetworkManager \
    pavucontrol pipewire ripgrep terminus-font tmux vim wget xorg
```

<br />

### Setting up a bootloader, locale, timezone, etc.

Since we are [installing Void Linux on a removable disk](https://docs.voidlinux.org/installation/guides/chroot.html#installing-on-removable-media-or-non-compliant-uefi-systems), we will have to install [GRUB](https://www.gnu.org/software/grub/) with the `--removable` option:

```console
bash-5.2# grub-install --target=x86_64-efi --efi-directory=/boot/efi/ \
    --bootloader-id="Void" --removable

Installing for x86_64-efi platform.
Installation finished. No error reported.
```

Then, we're going to configure a console font, hostname, locale, timezone:

```
bash-5.2# ls /usr/share/kbd/consolefonts
bash-5.2# vim /etc/rc.conf && cat /etc/rc.conf

(...)

# Set RTC to UTC or localtime.
HARDWARECLOCK="localtime"

(...)

# Console font to load, see setfont(8).
FONT="ter-v16n"

(...)
```

```
bash-5.2# vim /etc/hostname && cat /etc/hostname
void

bash-5.2# vim /etc/locale.conf && cat /etc/locale.conf
LANG=en_US.UTF-8
LC_COLLATE=C

bash-5.2# vim /etc/default/libc-locales
bash-5.2# xbps-reconfigure -f glibc-locales
```

```
bash-5.2# ln -sf /usr/share/zoneinfo/Asia/Seoul /etc/localtime
```

```
bash-5.2# passwd
New password:
Retype new password:
passwd: password updated successfully

bash-5.2# useradd -m -G bluetooth,wheel -s /bin/bash jdeokkim
bash-5.2# passwd jdeokkim
New password:
Retype new password:
passwd: password updated successfully
```

```
bash-5.2# EDITOR=vim visudo && cat /etc/sudoers

(...)

## Uncomment to allow members of group wheel to execute any command
%wheel ALL=(ALL:ALL) ALL

(...)
```

Finally, run `xbps-reconfigure` to complete the installation process:

```
bash-5.2# xbps-reconfigure -fa && exit
exit
```

```
# umount -l /mnt/dev && umount -l /mnt/proc && umount -l /mnt/sys
# umount /mnt/boot/efi && umount /mnt

# poweroff
```

<br />

### Booting into Void Linux

The first thing we need to do after booting into our Void installation is enabling the `NetworkManager` service:

```
[jdeokkim@void ~]$ sudo ln -s /etc/sv/chronyd /var/service/
[jdeokkim@void ~]$ sudo ln -s /etc/sv/dbus /var/service/
[jdeokkim@void ~]$ sudo ln -s /etc/sv/NetworkManager /var/service/
[jdeokkim@void ~]$ sudo sv start NetworkManager
```

TODO: ...
