---
layout: default
parent: Nix
grand_parent: Pentest Cheatsheets
title: Nix Shells
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

**Shell upgrade to interactive**
===========

**Reverse via http**
---------------------

<details>
<summary><u>Locally</u></summary>
<p>
REVERSE_IP - IP target will be connecting to send reverse shell
<br>
REVERSE_PORT - Port host will open to recieve reverse shell
<br>
EVILEXE - name of EXE
</p>
</details>

```
/bin/sh -i
python3 -c 'import pty; pty.spawn("/bin/sh")'
perl -e 'exec "/bin/sh";'
```
