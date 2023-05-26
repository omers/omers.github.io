---
title: "Prometheus Common Queries"
date: 2022-07-23T09:15:49+03:00
draft: false
tags: ["prometheus", "monitoring"]
author: "Omer Segev"
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: ""
canonicalURL: "https://canonical.url/to/page"
disableHLJS: false # to disable highlightjs
disableShare: false
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

## Rates of increase for counters
### Per-second rate of increase, averaged over last 5 minutes:
```
rate(demo_api_request_duration_seconds_count[5m])
```
### Per-second rate of increase, calculated over last two samples in a 1-minute time window
```
irate(demo_api_request_duration_seconds_count[1m])
```

### Absolute increase over last hour:
```
increase(demo_api_request_duration_seconds_count[1h])
```

## Aggregating over time
### Average within each series over a 5-minute period
```
avg_over_time(go_goroutines[5m])
```
### Get the maximum for each series over a one-day period
```
max_over_time(process_resident_memory_bytes[1d])
```
### Count the number of samples for each series over a 5-minute period
```
count_over_time(process_resident_memory_bytes[5m])
```


