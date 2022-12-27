---
title: "DORA Metrics"
date: 2022-12-27T10:58:04+02:00
tags: ["DevOps", "Continiues improvement"]
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

## What is DORA?
DORA is the acronym for the DevOps Research and Assessment group: they’ve surveyed more than 50,000 technical professionals worldwide to better understand how the technical practices, cultural norms, and management approach affect organizational performance.

![Dora addoption flow](/software-delivery-performance-relationships.png)


## The four key metrics we measure

* Deployment Frequency — How often an organization successfully releases to production
* Lead Time for Changes — The amount of time it takes a commit to get into production
* Change Failure Rate — The percentage of deployments causing a failure in production
* Time to Restore Service — How long it takes an organization to recover from a failure in production

## How do we understand the metrics?
* Deployment Frequency - limiting amount of code going to * production at once (limited batch size)
* Lead Time for Changes - reducing amount of blockers for developers
* Time to Restore Service - improving speed of incident recovery
* Change Failure Rate - improving quality focus


## Following the rules of lean:
* Value is only released to production, once it leaves the factory floor (production deploy frequency)
* Optimize Work In Progress (lead time)
* Invest in SRE/automation (mean time to recover)
* Practice kaizen (change fail rate)
* Have efficient knowledge sharing and work allocation processes (time to onboard)

## Get into business
