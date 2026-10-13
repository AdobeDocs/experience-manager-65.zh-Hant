---
title: 解決方案整合
description: 深入瞭解如何整合Adobe Experience Manager (AEM)與其他Adobe或協力廠商服務。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: ee5e8ebb-773f-4aa6-9c3e-2cc3bf4a3bbd
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 243139ec-8e41-5296-a287-31343ab1bc0f
    internal-label: Integration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%
---
# 解決方案整合{#solutions-integration}

* [與Adobe Experience Cloud整合](/help/sites-administering/marketing-cloud.md)
* [與協力廠商服務整合](/help/sites-administering/third-party-services.md)
* [Analytics與外部提供者](/help/sites-administering/external-providers.md)
* [目錄製作者](/help/sites-administering/catalog-producer.md)
* [瞭解、套用及組織智慧標籤](/help/assets/enhanced-smart-tags.md)

下列為整合AEM與其他Adobe或協力廠商服務的相關資訊：

>[!NOTE]
>
>如果您使用自訂Proxy設定搭配整合，則您必須同時設定HTTP使用者端Proxy設定，因為AEM的某些功能使用3.x API，而其他部分則使用4.x API：
>
>* 3.x已使用[http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)設定
>* 4.x已使用[http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)設定
>
