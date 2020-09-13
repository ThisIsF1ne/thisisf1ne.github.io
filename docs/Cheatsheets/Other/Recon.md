---
layout: default
parent: Other
grand_parent: Pentest Cheatsheets
title: Recon
nav-order: 1
---

Port Scanning
=============

NMAP
----

Multi-purpose scanner that checks ports, has signatures for different operating systems, can run scripts

**Common Uses**

_Base Format - defaults to SYN scan of top 1k ports at a random pattern_
```
nmap <TARGET_IP>
```

_Tries to get service version, runs scripts, checks OS version, and only scans top 100 ports_
```
nmap -sC -sV -O -F <TARGET_IP>
```

**Lessons Learned**

1. Scan Type requires root privileges

> _This is because only privileged users can use raw sockets on unix type systems, so rerun the command with sudo and go on your merry way._

2. Port no longer up after running scripts against it

> Nmap scripts have multiple categories and you have to make sure what you are running is safe unless you know what you are doing. There are many scripts that will crash the service they are ran against which may deny you future access.

masscan
-------
https://github.com/robertdavidgraham/masscan
Robust mass port scanner that is designed to work on entire internet. Uses own TCP/IP stack separate from the main OS.

**Common Uses**

_Base Format - Prints results to stdout_

```
masscan -p<PORT>,<PORT>-<PORT> <TARGET_NETWORK>
```

_Banner Grab, set unused local IP for source-ip_

```
masscan <TARGET_NETWORK> -p<PORT> --banners --source-ip <UNUSED_LOCAL>
```
_Increased rate to 1000 packets per second and output to an xml file_

```
masscan -p<PORT>,<PORT>-<PORT> <TARGET_NETWORK> --max-rate 1000 -oX <FILE>.xml
```
**Lessons Learned**

1. Not getting banners properly

> _This happens because masscan uses own TCP/IP stack so when the host OS gets a _

2. Port no longer up after running scripts against it

> Nmap scripts have multiple categories and you have to make sure what you are running is safe unless you know what you are doing. There are many scripts that will crash the service they are ran against which may deny you future access.
