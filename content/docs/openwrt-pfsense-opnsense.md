+++
title = "OpenWrt vs. pfSense vs. OPNSense"
date = 2023-10-27
weight = 20

[extra]
group_id = 2
+++

This doc is intended to provide a detailed comparison of those router OSes. For a brief one, see [Which router OS to chose](@/docs/which-router-os-to-chose.md).

# Installation

## OpenWrt

Install by write the disk image on to the disk of the router.

## pfSense & OPNSense

Install by write the installation image on to USB drive first, then use it to boot up the router, and run the installer to install to the disk of the router.

# Upgrade

## OpenWrt

On x86 soft routers, it can’t be easily upgraded “in place”. The upgrade process is very much like a new install: backup the configuration, install the new version, restore the backup.

This usually involves certain technical skill such as writing disk image to a drive, and debug problems in case they occur. This some times creates problems for not-so-experienced users as it is more time consuming and error prone.

## pfSense & OPNSense

They can be upgraded in the web UI easily. By clicking few buttons, the web UI will check for updates and show them if available. Then updates can be installed by another few clicks.

This easy-to-upgrade feature actually makes pfSense & OPNSense a bit more “secure” in some environment, as the user could upgrade their router more frequently and with less issues they could stick with the latest version easily.

## Usability

# OpenWrt

It has more packages than the other two. For example, Transmission and Samba are available on OpenWrt and can be installed easily via the opkg command or the web UI. However pfSense & OPNSense does not provide such packages. In fact, they are somewhat against of running such applications on a router or firewall.

## pfSense & OPNSense

They have less packages then OpenWrt

# Web UI

# Performance

# Secure