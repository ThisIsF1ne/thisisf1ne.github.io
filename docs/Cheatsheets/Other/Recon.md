---
layout: default
parent: Other
grand_parent: Pentest Cheatsheets
title: General Recon
nav-order: 1
---

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>


nmap
====

Multi-purpose scanner that checks ports, has signatures for different operating systems, can run scripts

**Common Uses**
---------------
_Base Format - defaults to SYN scan of top 1k ports at a random pattern_
```
nmap <TARGET_IP>
```

_Tries to get service version, runs scripts, checks OS version, and only scans top 100 ports_
```
nmap -sC -sV -O -F <TARGET_IP>
```
_Run all available nmap scripts against mysql_

```
nmap -sV --script=mysql* <TARGET_IP>
```

**Useful Directories**
--------------------------------------------------------------
_All available scripts for nmap locally_
```
/usr/share/nmap/scripts/
```

**Lessons Learned**
-------------------
1. _Error - Scan Type requires root privileges_

    * This is because only privileged users can use raw sockets on unix type systems, so rerun the command with sudo and go on your merry way.

2. _Port no longer up after running scripts against it_

    * Nmap scripts have multiple categories and you have to make sure what you are running is safe unless you know what you are doing. There are many scripts that will crash the service they are ran against which may deny you future access.

masscan
=======

[masscan - github](https://github.com/robertdavidgraham/masscan)

Robust mass port scanner that is designed to work on entire internet. Uses own TCP/IP stack separate from the main OS.

**Common Uses**
---------------
_Base Format - Prints results to stdout_

```
masscan -p<PORT>,<PORT>-<PORT> <TARGET_NETWORK>
```

_Banner Grab, set unused local IP for source-ip_

```
masscan <TARGET_NETWORK> -p<PORT> --banners --source-ip <UNUSED_LOCAL>
```
_Increased rate to 1000 (can max out at 10M packets with proper equipment and drivers) packets per second and output to an easily greppable file_

```
masscan -p<PORT>,<PORT>-<PORT> <TARGET_NETWORK> --max-rate 1000 -oG <FILE>
```

**Lessons Learned**
-------------------

1. _Not getting banners properly_

    * This happens because masscan uses its own TCP/IP stack so when the host OS gets a SYN,ACK with no idea what it is from it will send a reset and close the connection before masscan can pull a banner. Solution is to use an unused IP on your current subnet as the source IP or using iptables which will stop OS from closing connection and give masscan to see it since it doesn't use the OS stack
