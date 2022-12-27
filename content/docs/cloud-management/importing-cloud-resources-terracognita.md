---
title: "Importing Cloud Resources Terracognita"
date: 2022-12-26T11:59:57+02:00
tags: [""]
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

## About Terracognita

TerraCognita allows you to migrate your current cloud infrastructure to infrastructure-as-code. It quickly and automatically creates Terraform from all of your manually-provisioned resources, allowing them to be easily replicated by you and your cloud provider.

## The Challange

For example, There is a security group that was created manually long time ago.  
Now, You need to start amanaging and audit any events and changes related to this Security gtoup.

## The code

```bash
terracognita aws -i aws_security_group \
--aws-access-key <YOUR_ACCESS_KEY> \
--aws-secret-access-key <YOUR_SECRET_ACCESS_KEY> \
--tfstate terraform.tfstate --hcl sg.tf  \
--aws-default-region us-east-2 --target <RESOURCE_ID>
```

terracognita aws --target aws_security_group.sg-0cf9d7d81a21c43c3 -i aws_security_group --tfstate terraform.tfstate --hcl sg.tf  --aws-default-region us-east-2