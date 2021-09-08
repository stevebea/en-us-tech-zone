---
layout: doc
h3InToc: true
contributedBy: First Last, First2 Last2
specialThanksTo: First Last, First2 Last2
description: TODO insert description of article
tz_title: TODO insert title of article
tz_products: citrix-analytics;citrix-content-collaboration;citrix-endpoint-management;citrix-networking;citrix-secure-internet-access;citrix-secure-workspace-access;citrix-service-providers;citrix-virtual-apps-and-desktops-standard-for-azure;citrix-virtual-apps-and-desktops;citrix-workspace;google-cloud-platform;other;security;third-party-content
---
# PoC Guide: Citrix Endpoint Management

## Overview
Citrix Endpoint Management is an industry acknowledged Unified Endpoint Management aka UEM solution offered through the Citrix Cloud as a Service. Unified Endpoint Management solutions offer a single uniform over-the-air management interface for mobile, laptops, PCs, and other devices like wearables and IoT endpoints. Citrix Endpoint Management provides a flexible choice in platform management, ownership models (Bring Your Own Device, Choose Your Own Device, Company Owned - Personally Enabled and Company Owned – Business Only) and delivery models for securing the endpoint, applications, the connections, and data.
This Poc Guide provide you a guidance to prepare and deploy Citrix Endpoint Management solution with three uses cases (MDM,MAM, MicroVPN).
First you should prepare the backend PoC environnement for:
  1. Install two Cloud Connector
  2. Citrix Gateway if you plan to demonstrate access of internal apps with MicroVPN or access to Microsoft Exchange
  3. ....
![image](https://user-images.githubusercontent.com/89078107/132574091-f095824b-5b50-4f80-91d1-bcd088ad7aaf.png)
Cloud Connector on Citrix Endpoint Management perform connection between On-Prem identity (ActiveDirector) and Citrix Endpoint Management solution. 
Then you can consume On-Prem Active Directory on Citrix Cloud.

![image](https://user-images.githubusercontent.com/89078107/132574613-d813a8e5-20ba-48e5-a740-62db70adb959.png)
This part is the most difficult to implement in case of this deployment at custormer side you should take in mind enough time to implement, open flow, test and remediate.
Below list of port to open:
![image](https://user-images.githubusercontent.com/89078107/132575338-02fea2d5-e38b-4ac2-9a2d-e53b3f0121bb.png)

