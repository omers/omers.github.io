---
title: "Building Loki Cluster With Terraform"
date: 2023-05-03T19:42:18+03:00
tags: ["monitoring", "grafana", "loki"]
author: "Omer Segev"
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: ""
disableHLJS: false
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

## The Idea
Elasticsearch and Grafana Loki are both log management systems, but they have different strengths and weaknesses. Here are some reasons why you might want to consider migrating from Elasticsearch to Grafana Loki:

* Cost: Elasticsearch can be expensive, especially for larger deployments. Grafana Loki, on the other hand, is open source and free to use.

* Simplicity: Grafana Loki is designed to be simple and easy to use, with a focus on searching and visualizing logs. Elasticsearch, while powerful, can be more complex to set up and configure.

* Scalability: Grafana Loki is designed to be highly scalable and performant, with a focus on horizontal scalability. Elasticsearch can also be scaled horizontally, but it requires more effort to set up and configure.

* Kubernetes integration: Grafana Loki was designed with Kubernetes in mind, and integrates seamlessly with Kubernetes clusters. Elasticsearch can be integrated with Kubernetes, but it requires more effort and configuration.

* Query language: Grafana Loki uses a query language that is similar to PromQL, which makes it easy to learn and use for users who are familiar with Prometheus. Elasticsearch uses its own query language, which can be more complex and difficult to learn.

Ultimately, the decision to migrate from Elasticsearch to Grafana Loki will depend on your specific needs and use case. However, if you are looking for a more cost-effective, simple, scalable, and Kubernetes-friendly log management system, Grafana Loki might be a good choice for you.

Stream 600Gb logs per day

### Why Grafana Loki?
Loki is a horizontally scalable, highly available, multi-tenant log aggregation system inspired by Prometheus. It is designed to be very cost effective and easy to operate. It does not index the contents of the logs, but rather a set of labels for each log stream.

Loki takes a unique approach by only indexing the metadata rather than the full text of the log lines.
## Business Value
 * Better alerting mechanism
 * Cost saving - Store on S3
 * Longer retention period
 * Better integration with Grafana 
### Cost
Compute:
3 x c6i.4xlarge	= 0.68 x 3 x 24 x 30 = $1468  

Storage:
STANDARD TIER save for 90 days
STANDARD_IA TIER - after 90 days move to STANDARD_IA -> After 180 days delete

Network:


## Solution

### Architecture
* Ingesters: Ingesters are responsible for ingesting log data from producers.
* Queriers: Queriers are responsible for querying log data.
* Compactors: Compactors are responsible for compacting log data to reduce storage space.
* Rulers: Rulers are responsible for enforcing policies on log data.
* Index gateways: Index gateways are responsible for serving log data to clients.
#### Read Nodes
#### Write Nodes
#### Backend Storage
#### Data Retention
The retention_deletes_enabled flag specifies whether or not Grafana Loki should delete old log data. The retention_period specifies the number of days that log data will be retained.

Once you have configured the Loki object store and table manager configurations, you can start collecting and storing log data in Grafana Loki.
```yaml
compactor:
  working_directory: /data/retention
  shared_store: s3
  compaction_interval: 10m
  retention_enabled: true
  retention_delete_delay: 2h
  retention_delete_worker_count: 150

chunk_store_config:
  max_look_back_period: 672h

table_manager:
  retention_deletes_enabled: true
  retention_period: 7d
```

#### Visualization
#### Load balancer
Write rules  
Read rules

### Components
#### Infrastrucutre as code