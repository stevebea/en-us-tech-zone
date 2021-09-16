---
layout: doc
h3InToc: true
contributedBy: Jorge LUIS
specialThanksTo: First Last, First2 Last2
description: PoC Guide for Citrix Endpoint Management
tz_title: PoC Guide for Citrix Endpoint Management
tz_products: citrix-analytics;citrix-content-collaboration;citrix-endpoint-management;citrix-networking;citrix-secure-internet-access;citrix-secure-workspace-access;citrix-service-providers;citrix-virtual-apps-and-desktops-standard-for-azure;citrix-virtual-apps-and-desktops;citrix-workspace;google-cloud-platform;other;security;third-party-content
---
# PoC Guide: Citrix Endpoint Management

## Overview
Citrix Endpoint Management is an industry acknowledged Unified Endpoint Management aka UEM solution offered through the Citrix Cloud as a Service. Unified Endpoint Management solutions offer a single uniform over-the-air management interface for mobile, laptops, PCs, and other devices like wearables and IoT endpoints. Citrix Endpoint Management provides a flexible choice in platform management, ownership models (Bring Your Own Device, Choose Your Own Device, Company Owned - Personally Enabled and Company Owned – Business Only) and delivery models for securing the endpoint, applications, the connections, and data.

# This Poc Guide provide you a guidance to prepare and deploy Citrix Endpoint Management solution with three uses cases (MDM,MDM&MAM, MDM&MAM&MicroVPN).

![image](https://user-images.githubusercontent.com/89078107/133591319-8cf3c703-36db-4d11-9a73-f4365d3262cc.png)

Prerequisites:
 - One device (Android +10 / iPhone)
 - Entillment on Citrix EndPoint Management
 - Google Account (Gmail)

To perform evaluation of MDM feature you can use local user to perform enrollment of your devices

From Citrix Cloud portal launch Citrix Endpoint Management console:

![133486451-e8246444-04f7-4b1e-90c6-eb1b4fae6b1b](https://user-images.githubusercontent.com/89078107/133596126-ebc68adf-c06f-4c5a-bd0c-6edde34d49c6.png)

Then click on Manage -> Users -> Add Local User (With this local user you can enroll any device with secure hub

![133488092-4ffd4297-e61b-44d6-8e64-01d8cdb37c03](https://user-images.githubusercontent.com/89078107/133596168-ff256d8d-6cef-45d0-8d27-03749eb7f0f8.png)

Next you can provide username and password information and save:

![image](https://user-images.githubusercontent.com/89078107/133488092-4ffd4297-e61b-44d6-8e64-01d8cdb37c03.png)

Now we should bind Google Play Store & Apple Store to you CEM Tenant:
 
 - Follow this operation for Android Enterprise Device
 
 
 - This points for iPhone devices 

To perform this configuration create a gmail account dedicated for this PoC









Use case n°2) MDM & MAM



Use case n°3) MDM & MAM & MicroVPN
First you should prepare your backend PoC environnement and install
  1. On-Prem Active Directory
  2. Install two Cloud Connector
  3. Citrix Gateway if you plan to demonstrate access of internal apps with MicroVPN or access to Microsoft Exchange
  4. Exchange servers
![image](https://user-images.githubusercontent.com/89078107/132574091-f095824b-5b50-4f80-91d1-bcd088ad7aaf.png)
Cloud Connector on Citrix Endpoint Management perform connection between On-Prem identity (ActiveDirector) and Citrix Endpoint Management solution. 
Then you can consume On-Prem Active Directory on Citrix Cloud.

![image](https://user-images.githubusercontent.com/89078107/132574613-d813a8e5-20ba-48e5-a740-62db70adb959.png)
This part is the most difficult to implement in case of this deployment at custormer side you should take in mind enough time to implement, open flow, test and remediate.
Below list of port to open:
![image](https://user-images.githubusercontent.com/89078107/132575338-02fea2d5-e38b-4ac2-9a2d-e53b3f0121bb.png)

