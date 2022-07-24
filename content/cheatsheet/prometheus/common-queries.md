---
title: "Prometheus Common Queries"
date: 2022-07-23T09:15:49+03:00
draft: true
tags: ["prometheus", "monitoring"]
author: "Omer Segev"
# author: ["Me", "You"] # multiple authors
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

## Quantiles from histograms
90th percentile request latency over last 5 minutes, for every label dimension:
```
histogram_quantile(0.9, rate(api_duration_seconds_bucket[5m]))
```
