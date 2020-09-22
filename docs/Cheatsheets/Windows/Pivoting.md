---
layout: default
parent: Windows
grand_parent: Pentest Cheatsheets
title: Windows Pivoting
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

**Port Proxy**
==========

**Forward Connection**
--------------

<details>
<summary><u>On Redirection Host</u></summary>
<p>
LISTEN_PORT - Port listening on host to accept connections
<br>
CONNECT_PORT - Port you will connect to on the target if you send connection to LISTEN_PORT
<br>
TARGET_IP - Where you will connect to once you hit the LISTEN_PORT on the redirection host
</p>
</details>


```
v4tov4 listenport=LISTEN_PORT connectport=CONNECT_PORT connectaddress=TARGET_IP
```
