+++
title = "Should I chose ext4 or squashfs image for OpenWrt?"
date = 2023-11-20
weight = 30

[extra]
show_toc = true
show_sidebar = true
group_id = 3
+++

Now, you decide to install OpenWrt on a x86 router. And you go to the [OpenWrt download site](https://downloads.openwrt.org/releases/) for the [latest version (as of writing, it's 25.0.2)](https://downloads.openwrt.org/releases/23.05.2/targets/x86/64/). Then you noticed that there are quite a few files listed.

You may ask, what the heck are are those files and which one should I download? Let me explain it for you.

# What are those files?

- generic-**ext4**-combined-**efi**.img.gz

  This is the disk image for system that supports UEFI boot. The rootfs is formatted as ext4.

- generic-**ext4**-combined.img.gz

  This is the disk image for system that *DOESN'T* supports UEFI boot. The rootfs is formatted as ext4.

- generic-**ext4**-**rootfs**.img.gz

  This is the **partition** image for the ext4 rootfs only.

- generic-**kernel**.bin

  This is the kernel image, i.e. the `vmlinuz` file you may see on a regular Linux system.

- generic-**squashfs**-combined-**efi**.img.gz

  This is the disk image for system that supports UEFI boot. The rootfs is formatted as squashfs(on this later).

- generic-**squashfs**-combined.img.gz

  This is the disk image for system that *DOESN'T* supports UEFI boot. The rootfs is formatted as squashfs.

- generic-**squashfs**-**rootfs**.img.gz

  This is the **partition** image for the squashfs rootfs only.

- rootfs.tar.gz

  This is the tarball that packs all the files on the rootfs.

Basically there are two decisions to make:

- Should I chose UEFI disk image or not? This depends on the hardware you own. As a rule of thumb, if your box is manufactured in the last few years, it should support UEFI and you can try the image with `efi` in their name. If it doesn't boot, you will need the image without `efi` in their name. Don't worry, they don't actually have any differences regarding functionalities.

- Ext4 or squashfs? These two are tricky. You'll have to read one to understand their differences and see which one you prefer. If you don't really care, go with ext4.

# Ext4 vs. SquashFS

Both of them are popular filesystems on Linux system. They have a fundamental difference: ext4 is read AND writable, while squashfs is read-only.

The ext4 filesystem is writable thus changes could be made in-place. For example, editing config files, install or upgrade packages, these operations will just modify existing files or add new files to the ext4 filesystem. This is just like a regular Linux system.

On the other hand, squashfs is read-only. That means you can't change files on it. Usually, it is used with another writable filesystem together to provide the write capability. In such way, you will have a unchangeable rootfs that allows you to revert the system to the factory state, just by wiping the writable filesystem, thus lose all the changes made. The ext4 filesystem couldn't provide such convenience.

# Pros and Cons

Here are the pros and cons of the OpenWrt system that use these two filesystems.

## Ext4
### Pros
- Easy to manage like a regular Linux system.
- The partition setup is very straightforward. It's easy to enlarge root partition without losing data.

### Cons
- No way to do a factory reset.
- No easy way to do a system backup, as it's hard to tell what files have changed since the first boot.

## SquashFS
### Pros
- It's easy to do a full system backup. The builtin `sysupgrade` tool handles it very well.
- It allows factory reset to revert the system to a clean state. It is useful in case you messed up your router. It even doesn't matter if you deleted system files, as they are read-only and can't be really deleted, they are just "masked" and can be taken back.

### Cons
- The partition setup is a little bit tricky, makes enlarging root partition harder.

# How to chose?

If you just want a router up and running and manageable like a regular Linux system, go with ext4.

If you are going to play with the router a lot, such as install and uninstall packages, try different configurations, go with squashfs. This is also my personal preference.