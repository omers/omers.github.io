---
title: "OpenSSL Generate self signed certificate"
date: 2022-07-26T14:37:48+03:00
tags: ["openssl"]
author: "Omer Segev"
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: ""
disableHLJS: false
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
---
This is a one liner on how to create SSL Self signed certificate with OpenSSL

```
openssl req -new -newkey rsa:4096 -days 365 \
-nodes -x509 -keyout server.key -out server.crt
```