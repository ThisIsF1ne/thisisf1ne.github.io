---
layout: default
parent: Windows
grand_parent: Pentest Cheatsheets
title: Web Enumeration
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

**gobuster**
==========

https://github.com/OJ/gobuster

Quick tool built with go to enumerate URIs, DNS, and vhosts in

**Checking directories on web server**

```
gobuster dir -w /usr/share/wordlists/dirb/big.txt -u http://10.10.10.10:8000
```

**Checking directories on web server and also files with extensions**

```
gobuster dir -w /usr/share/wordlists/dirb/big.txt -u http://10.10.10.56/ -x .php,.sh
```

**dirbuster**
==========

**dirb**
==========

**dirb**
==========
