+++
title = "OpenWrt vs. pfSense vs. OPNSense"
date = 2023-10-27
weight = 20

[extra]
show_toc = true
show_sidebar = true
group_id = 2
+++

This doc is intended to provide a detailed comparison of those router OSes. For a brief one, see [Which router OS to chose](@/docs/which-router-os-to-chose.md).

# Installation

## OpenWrt

Install by write the disk image on to the disk of the router.

## pfSense & OPNSense

Install by write the installation image on to USB drive first, then use it to boot up the router, and run the installer to install to the disk of the router. In fact their install process is the customized FreeBSD install process.

# Upgrade

## OpenWrt

On x86 soft routers, it can’t be easily upgraded “in place”. The upgrade process is very much like a new install: backup the configuration, install the new version, restore the backup.

This usually involves certain technical skill such as writing disk image to a drive, and debug problems in case they occur. This some times creates problems for not-so-experienced users as it is more time consuming and error prone.

However, it is possible to setup the router to have multiple OpenWrt root partitions if there is enough disk space. And then the new version could be installed into one of the spare partitions without wiping the old version. This allows you to switch back to the old version if there's something wrong with the new version.

## pfSense & OPNSense

They can be upgraded in the web UI easily. By clicking few buttons, the web UI will check for updates and show them if available. Then updates can be installed by another few clicks.

This easy-to-upgrade feature actually makes pfSense & OPNSense a bit more “secure” in some environment, as the user could upgrade their router more frequently and with less issues they could stick with the latest version easily.

## Usability

# OpenWrt

It has more packages than the other two. For example, Transmission and Samba are available on OpenWrt and can be installed easily via the opkg command or the web UI. However pfSense & OPNSense does not provide such packages. In fact, they are somewhat against of running such applications on a router or firewall.

## pfSense & OPNSense

They have less packages then OpenWrt

# Web UI

The UI styles are all different. It is hard to tell which one is better as they all can get your job done.

IMHO the pfSense web UI is less intuitive than the other two, as some of the navigation wording may not be what a regular user expects.

# Performance

# Security

OpenWrt is based on Linux, pfSense and OPNSense are based on FreeBSD. Both operating systems are widely used and very secure. The communities of the three router OSes are all working hard to keep them secure, by releasing upgrades to fix known security issues.

However, I believe OpenWrt is a little bit less secure than the other two unless the user works very hard to make them up to date. This is because, as mentioned, upgrading OpenWrt is not as convenient as the other two so it is more possible that a OpenWrt installation is left outdated. This could be mitigated if the user upgrade their router in time, for example, follow the instruction mentioned above.

Furthermore, OpenWrt provides more functionalities than the other two, means it could potentially introduce more security risks. This, however, could be mitigated too if the user chose to run a basic installation with only firewall and routing functionality.