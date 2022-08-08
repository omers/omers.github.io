---
title: "Teleport Access and Authorization"
date: 2022-08-08T14:48:17+03:00
draft: true
tags: ["teleport"]
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

Teleport has a strong RBAC system that allows to grant access to specific resources.  
In order to setup your environment, You need to do some preperations:  

1. Define what are the Groups in your organization
2. Define which access each group needs, For example:  
```Developers group needs access to Grafana and server Superset```
3. Decide how to label each server / resource, and assign the labels to each resource
4. Deinfe the policy that grants the access to the resources

```yaml
kind: role
version: v5
metadata:
  name: Developers
  description: Developers Team Role
spec:
  allow:
    logins: ['admin']
    node_labels:
      'type': 'Grafana'
      'type': 'Superset'
```