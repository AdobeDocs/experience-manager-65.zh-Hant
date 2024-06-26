---
title: 升級後解除安裝的過時套件組合清單
description: 詳細說明升級至AEM 6.3時自動解除安裝的套件組合清單。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
feature: Upgrading
exl-id: 0defbdc7-d414-4662-a31f-88c8d63d68eb
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---

# 升級後解除安裝的過時套件組合清單{#list-of-obsolete-bundles-uninstalled-after-the-upgrade}

>[!NOTE]
>
>如果您的程式碼仰賴這些套件，請務必聯絡Adobe支援，要求取得受影響區域的相容性套件。

升級至AEM 6.3時，系統會根據執行升級的AEM版本，自動解除安裝下列套件組合：

**AEM 6.1：**

* org.eclipse.equinox.region，1.1.0.v20120522-1841版，作用中
* org.apache.sling.installer.factory.subsystems，版本1.0.0，Active
* org.apache.aries.subsystem.core，1.2.0版，Active
* org.apache.aries.subsystem.api，1.1.0版，Active
* org.apache.felix.resolver，版本1.0.0，作用中
* org.osgi.service.subsystem.region.context.0，版本1.0.0，作用中
* com.adobe.cq.cq-creativecloud-cloudims，0.0.10版，Active
* com.adobe.cq.cq-creativecloud-commons，0.0.8版，Active
* com.adobe.cq.cq-creativecloud-filesync，0.0.12版，已安裝
* com.adobe.cq.cq-creativecloud-storage，0.0.8版，已安裝
* biz.aQute.bndlib，1.43.0版，作用中
* com.day.cq.dam.commons.nekohtml，0.9.5版，Active
* com.day.cq.mcm.cq-mcm-silverpop-integration，1.2.2版，Active

**AEM 6.0：**

* org.apache.sling.discovery.impl，版本1.1.6，活動
* com.adobe.granite.installer.patch，0.4.0版，Active
* biz.aQute.bndlib，1.43.0版，作用中
* com.day.cq.cq-jobs-core，5.4.0版，Active
* com.day.cq.cq-opensocial，5.7.2版，Active
* com.day.cq.cq-pinauthhandler，1.1.2版，Active
* com.day.cq.dam.commons.nekohtml，0.9.5版，Active
* com.day.cq.mcm.cq-mcm-silverpop-integration，1.1.6版，Active
* com.day.cq.wcm.cq-wcm-mobile-phonegap-build-integration，5.7.18版，Active

**CQ 5.6.1：**

* biz.aQute.bndlib，1.43.0版，作用中
* com.day.cq.cq-pinauthhandler，1.0.0版，Active
* com.day.cq.dam.commons.nekohtml，0.9.5版，Active
* com.day.crx.crxde支援，2.3.14版，已安裝
* com.day.cq.mcm.cq-mcm-silverpop-integration，1.0.2版，Active

**CQ 5.6.0：**

* com.day.cq.cq-pinauthhandler，1.0.0版，Active
* com.day.cq.dam.commons.nekohtml，0.9.5版，Active
* com.day.crx.crxde支援，2.3.14版，已安裝
