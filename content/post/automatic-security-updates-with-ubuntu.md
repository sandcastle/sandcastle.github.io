---
date: 2015-04-06
title: "Automatic security updates with Ubuntu"
slug: "automatic-security-updates-with-ubuntu"
tags: [ "ubuntu", "linux", "security" ]
categories: [ "ops" ]
---

To configure automatic updates on Ubuntu you will first need ensure that the `unattended-upgrades` package is installed.

```bash
sudo apt-get install unattended-upgrades
```

We then need to enable the package by running the following command (you will be prompted with a confirmation screen - select `yes`):

```bash
sudo dpkg-reconfigure -plow unattended-upgrades
```

Once enabled, edit the auto upgrades settings file (`/etc/apt/apt.conf.d/20auto-upgrades`) so it contains the following 4 lines (some may already exist):

```bash
APT::Periodic::Update-Package-Lists "1";
APT::Periodic::Download-Upgradeable-Packages "1";
APT::Periodic::AutocleanInterval "7";
APT::Periodic::Unattended-Upgrade "1";
```

These settings will ensure that it checks for updates daily and runs a weekly cleanup.

Finally, you may want to tweak the unattended upgrades settings file (`/etc/apt/apt.conf.d/50unattended-upgrades`). This file allows you to chose what updates are run and where apt can search for new updates.

```bash
Unattended-Upgrade::Allowed-Origins {
  "${distro_id}:${distro_codename}-security";
//  "${distro_id}:${distro_codename}-updates";
//  "${distro_id}:${distro_codename}-proposed";
//  "${distro_id}:${distro_codename}-backports";
};
```
It is recommended you stick with just security updates initially, unless you know what you are doing.

_Note: The variables ${distro_id} and ${distro_codename} are expanded automatically. I would comment out the updates entry and just leave security._
