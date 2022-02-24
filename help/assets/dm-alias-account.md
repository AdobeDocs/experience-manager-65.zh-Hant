---
title: Configure a Dynamic Media company alias account
description: Learn how to configure a company alias account in Dynamic Media.
contentOwner: Rick Brough
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User,Admin
mini-toc-levels: 4
exl-id: 2ca7b8b2-573c-40e9-b8c3-f38736e819ef
source-git-commit: 787c0c25da2258f234d3c821038d62bf8ef68932
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

<!-- hide: yes
hidefromtoc: yes -->

# About configuring a Dynamic Media company alias account {#about-dm-alias-acct}

Dynamic Media URLs and viewer embed code contain your company account name. This account name was created at the time of provisioning Dynamic Media. There may be scenarios where your business has undergone an acquisition, or a rebranding, or you simply want to use a more memorable name. In such scenarios, it is not easy to manually update your company account name in all URLs and viewer embed code that comes out of the box. Furthermore, there is the possibility that you may impact your existing Dynamic Media repository or impact live content. To resolve this issue, you can configure a Dynamic Media company alias account.

A Dynamic Media company alias account ensures that all out-of-the-box Dynamic Media URLs and viewer embed code in the user interface reflect any updates made to your business context, such as rebranding. An alias account also has a positive impact on your SEO (Search Engine Optimization) because the Dynamic Media URLs and viewer embed code reflect the new company account name.

When you configure a Dynamic Media company alias account, be aware of the following:

* ** However, any URLs or viewers embed code with your original Dynamic Media company name continue to work for existing or new assets.
* The Dynamic Media company alias account capability is limited to Experience Manager Assets Authoring mode and delivery. The company alias name does not work with Experience Manager Sites. WCM (Web Content Management) components are not updated for this change. Those components continue to work with the original Dynamic Media company name for fetching Dynamic Media assets.
* **** However, you can create as many company alias accounts by way of a support case, and manually reflect the necessary alias name in the Dynamic Media URLs or viewer embed code.
* [](/help/assets/invalidate-cdn-cache-dynamic-media.md)
* **************

[](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)

## Configure a Dynamic Media company alias Account {#configure-dm-alias-account}

You begin configuring a Dynamic Media company alias account by first submitting a Support case. This step is required.

1. [](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html)
1. Provide the following information in your support case:

   * The Dynamic Media company alias name you want to use. **
   * Your region.
   * [](/help/assets/using-rulesets-to-transform-urls.md)

1. After the Dynamic Media alias account is created by Support, in Experience Manager as a Cloud Service Author instance, select the Experience Manager as a Cloud Service logo to access the global navigation console.
1. ****
1. ************

   ![](/help/assets/assets-dm/dm-company-alias.png)

1. ********
1. **** The Dynamic Media company alias account is now saved and enabled; all URLs and viewer embed code for existing and new assets now reflect the new company alias name.
