---
title: 配置遠程處理端點
seo-title: 配置遠程處理端點
description: 了解如何配置遠程端點。
seo-description: 了解如何配置遠程端點。
uuid: 4d4f9274-dcae-4b9f-975a-575376c2f89c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: aab9d622-d76b-4100-9ca6-e5b86f543381
exl-id: 891d7d75-555a-46c6-a8a0-d5238b48bc79
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# 配置遠程處理端點{#configuring-remoting-endpoints}

遠端端點可讓使用Flex建置的應用程式，使用(AEM forms遭取代)AEM forms Remoting叫用服務。 系統會自動為每個已激活的服務建立遠程端點。 建立與端點同名的Flex目的地，Flex用戶端可建立指向此目的地的遠端物件，以叫用相關服務上的作業。

## 刪除終結點設定{#remoting-endpoint-settings}

**Flex用戶端驗證方法：** 判斷啟用安全性時，伺服器傳回給用戶端的回應類型，叫用的操作不支援匿名叫用，且用戶端傳入的憑證無或無效。
