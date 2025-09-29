---
title: "Installing Void Linux on an External SSD"
author: "Jaedeok Kim"
date: "2025-09-28"
tags: ["linux", "rootfs", "void-linux"]
---

Welcome to Jae's Tech Tips.

As my first blog post, I decided to write a tutorial about installing [Void Linux](https://voidlinux.org/) on an external SSD **from another Linux distribution**. This might be helpful for those like me who is forced to use Windows at work, but prefer using Linux at home. 

Let's get started by connecting your external SSD to your computer:

```console
# fdisk -l

(...)

Disk /dev/sdb: 29 GB, 30765219840 bytes, 60088320 sectors
29340 cylinders, 64 heads, 32 sectors/track
Units: sectors of 1 * 512 = 512 bytes

Disk /dev/sdb doesn't contain a valid partition table
```

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

### Making file systems

Next, we need to make a file system on each partition:

```console
# mkfs.vfat /dev/sdb1
# mkswap -c /dev/sdb2
# mkfs.ext4 /dev/sdb3
```

Let's mount each partition as follows:

```
# mount /dev/sdb3 /mnt/
# mkdir -p /mnt/boot/efi/
# mount /dev/sdb1 /mnt/boot/efi/
```

### Bootstrapping via `chroot`

We're going to install Void Linux by unpacking the ['rootfs'](https://docs.voidlinux.org/installation/guides/chroot.html) tarball first, and then entering the `chroot` environment to configure the base system:

```console
# wget https://repo-default.voidlinux.org/live/current/void-x86_64-ROOTFS-20250202.tar.xz && tar xvf void*.xz -C /mnt
# cp /etc/resolv.conf /mnt/etc/resolv.conf
# chroot /mnt/ /bin/bash

bash-5.2# 
```

It's time to install mandatory packages such as `base-system` and `xtools`:

```
bash-5.2# xbps-install -Su xbps && xbps-install -u
bash-5.2# xbps-install base-system xtools
bash-5.2# xbps-remove base-container-full
```

### Installing additional packages

Here's the list of packages that I find necessary or very useful:

```
bash-5.2# xbps-install acpi alsa-pipewire base-devel bluez btop  \
    chezmoi chrony cmatrix curl dbus elogind eudev eudev-libudev \
    fastfetch git grub-x86_64-efi libspa-bluetooth lynx          \
    NetworkManager pavucontrol pipewire ripgrep                  \
    terminus-font tmux vim wget xorg
```

TODO: ...
