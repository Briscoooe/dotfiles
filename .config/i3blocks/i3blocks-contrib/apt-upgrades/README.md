# i3blocks-apt-upgrades

i3blocks-apt-upgrades is an i3blocks blocklet script to show the number of pending system upgrades.

![](apt-upgrades.png)

# Requirements

Dependencies: aptitude, bash

Suggested: fonts-font-awesome

# Suggested usage

Copy the `i3blocks.conf` section into your i3blocks configuration.
We assume you use `signal=1` but you can choose another signal number if you prefer.
Create apt/dpkg hooks to signal the script.
For example, create `/etc/apt/apt.conf.d/80i3blocks` with contents

```
APT::Update::Post-Invoke { "pkill -RTMIN+1 i3blocks"; };
DPkg::Post-Invoke { "pkill -RTMIN+1 i3blocks"; };
```
**Warning**: make sure to 
```ShellSession
sudo chown root:root /etc/apt/apt.conf.d/80i3blocks
sudo chmod 644 /etc/apt/apt.conf.d/80i3blocks
```
so that only the root user may modify
`80i3blocks`. This is necessary because apt has root privileges when upgrading the system,
and therefore commands in `80i3blocks` will be executed with root privileges.

You may also combine this script with a cron job that calls `apt-get update` periodically for
a more "popup upgrade reminder" feeling.

# Simple usage

Instead of using `signal=1` in the configuration, you can use `interval=3600` 
to have the script execute every hour.
This method avoids the usage of apt/dpkg hooks.

# Options

```
Usage: apt-upgrades [-s pending_symbol] [-o] [-c pending_color] [-N|-n nonpending_color] [-h]
Options:
-s  Specify a refresh symbol. Default: "\uf021 "
-o  Show refresh symbol only, but no numbers.
-c  Color when upgrade is pending. Default:  #00FF00
-n  Color when no upgrade is pending. Default: #FFFFFF
-N  Only display text if upgrade is pending (supercedes -n)
-h  Show this help text
```
