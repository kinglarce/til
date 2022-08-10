---
description: Wednesday, August 10, 2022
---

# AWS

Jeff Bar always writing the blog post about AWS

What is Cloud Service Provider?

* can be chained together, accessible via single unified API, metered billing, rich monitoring, offers IaaS, and IaC.
* cloud platform - twilio, hashicorp



Magic Quadrant(MQ)

Common Cloud Services

* Compute
* Networking - VPC
* Storage
* Database\


Hypervisor is the software layer that let you run VM's

Container - Normally runs in Docker

Function - VM's running managed containers known as Serverless Computer. Cold Start is a side-effect of this setup.&#x20;



Burning Platform - when company abandons old tech and move to new one



AWS Bracket - Creating quanting computing



Benefits of Cloud

* Agility
* Pay as you go pricing
* Economy of scale
* Global reach
* Security
* Reliabilty
* High Availability
* Scalability
* Elasticity



6 Advantages of Cloud

* Trade capital expense - pay on demand
* Benefit from massive economies scale - sharing cost with other customers
* Stop guessing capacity - scale up or down
* Increase speed and agility - launch resources within a few clicks
* Stop spending money on running and maintaining data centers - focus on your own customers
* Go global in minutes - deploy app in multiple regions around the world with few clicks



Availability Zones\
Normally 2-3 which is isolated from each other but close enough to provide low latency(<10ms)



Common practice to run workloads in at least 3 AZs to ensure services remain available in case one or two data centers fail.

AZs are within 100km of each other



Fault domain - section of network that vulnerable to damage. Purpose is that if failure occurs it will not cascade outside that domain, limiting the damage possibility.



Edge location - can act as on and off ramps to AWS global network

CloudFront - use edge location to provide edge storage and computer near the user

AWS Global accelerator & S3 transfer acceleration - to quickly reach aws resources in other regions traversing AWS  global network.

VPC endpoint - ensuring your resources stay within the aws network and do not traverse over the public internet.
