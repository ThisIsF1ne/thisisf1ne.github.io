---
layout: default
parent: Other
grand_parent: Pentest Cheatsheets
title: DNS Recon
nav-order: 2
---

**dnsrecon**
========

[dnsrecon - github](https://github.com/darkoperator/dnsrecon)

**Common Uses**
---------------

_Base command, performs general enum of target domain using system DNS settings_

```
dnsrecon -d TARGET_DOMAIN
```

_Perform zone transfer against target domain using the name server given_

```
dnsrecon -a -d TARGET_DOMAIN -n NAMESERVER
```

**dnsenum**
========

[dnsenum - github](https://github.com/fwaeytens/dnsenum)
