---
title: "Setting Up AWS ECR service"
date: 2022-12-27T16:44:45+02:00
tags: ["AWS", "Docker"]
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

# Create ECR Repository with vulnerability scanning
```bash
aws ecr create-repository --repository-name <MY_ECR_REPO_NAME> \
--image-scanning-configuration scanOnPush=true --region us-east-2
```

