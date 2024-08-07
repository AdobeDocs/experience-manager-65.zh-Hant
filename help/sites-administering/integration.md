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
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '102'
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
>如果您使用自訂Proxy設定與整合，則您必須同時設定HTTP使用者端Proxy設定，因為AEM的某些功能使用3.x API，而其他功能則使用4.x API：
>
>* 3.x已使用[http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)設定
>* 4.x已使用[http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)設定
>
