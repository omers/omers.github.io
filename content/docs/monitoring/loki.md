---
title: "Loki Log based metrics a.k.a logs2metrics"
date: 2022-07-23T19:09:12+03:00
draft: true
tags: ["monitoring", "loki", "grafana"]
author: "Omer Segev"
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: ""
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
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

Loki is a datastore optimized for efficiently holding log data.  
The efficient indexing of log data distinguishes Loki from other logging systems. Unlike other logging systems, a Loki index is built from labels, leaving the original log message unindexed.  
  
The Basic native tool to send data to Loki, is [Promtail](https://grafana.com/docs/loki/latest/clients/promtail/#:~:text=Promtail%20is%20an%20agent%20which,applications%20needed%20to%20be%20monitored.)

A sample config file for Loki might seen like the follows:
```yaml
server:
  http_listen_port: 0
  grpc_listen_port: 0

positions:
  filename: /tmp/positions.yaml

clients:
   -  url: https://your.loki.cluster

scrape_configs:
- job_name: system
  static_configs:
  - targets:
      - localhost
    labels:
      job: varlogs
      __path__: /var/log/*.log
  - targets:
      - localhost
    labels:
      job: syslog
      __path__: /var/log/syslog
```