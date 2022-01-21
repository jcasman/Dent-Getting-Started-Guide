# Configuration

Upon booting the system will enter the dentOS environment, after which users can start configuring the system.

We can print basic information about the operating system using the `uname` tool.
`uname -a` will give information about all options, such as kernel name and version, hardware platform, processor archivesture, information about the operating system, etc.
```
ONIE:/ # uname -a
Linux (none) 4.9.95-gf9ad16f #1 SMP PREEMPT Fri Jan 8 15:58:30 CST 2021 aarch64
```


## System information
Password for the `root` user can be set with the `passwd` command:
```
~ $ passwd
```

We can view the operating system information by printing the `/etc/os-release` file:
```
ONIE:/ # cat /etc/os-release
NAME="onie"
VERSION="2020.11-V01"
ID=linux
```

## Locale configuration
Locale is a set of environment variables that define country, language and character encoding settings for various applications and the shell session on the Linux system.
`locale` utility can be used to view information about the curretly installed locale.

## Time configuration
System time is used in all Linux systems to keep track of time. It can se set by an onboard hardware clocl or by an external time server.
s
Systemd init provides the `timedatectl` utility to manage time zones.
We can list all available timezones with:
```
~ $ timedatectl list-timezones
```
To change the time zone, e.g. for UK: 
```
~ $ timedatectl set-timezone Europe/London
```

## Setting up network connection

Upon booting the device we can set up a working network connecion. The are multiple ways of doing this, out of which the simplest one being, configuring the `management 1` port intereface using `dhclient`:
```
ONIE:/ # dhclient ma1
```
The device should now have a working network connection. We can verify this with the `ping` command:
```
ONIE:/ # ping 8.8.8.8
PING 8.8.8.8 (8.8.8.8): 56 data bytes
64 bytes from 8.8.8.8: seq=0 ttl=113 time=25.051 ms
64 bytes from 8.8.8.8: seq=1 ttl=113 time=23.805 ms
64 bytes from 8.8.8.8: seq=2 ttl=113 time=24.740 ms
```
