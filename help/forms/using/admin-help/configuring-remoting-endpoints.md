---
title: 配置遠程處理終結點
seo-title: Configuring Remoting endpoints
description: 瞭解如何配置遠程處理終結點。
seo-description: Learn how to configure remoting endpoints.
uuid: 4d4f9274-dcae-4b9f-975a-575376c2f89c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: aab9d622-d76b-4100-9ca6-e5b86f543381
exl-id: 891d7d75-555a-46c6-a8a0-d5238b48bc79
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# 配置遠程處理終結點 {#configuring-remoting-endpoints}

遠程處理終結點使用Flex構建的應用程式能夠使用（表單棄用）AEM表單遠AEM程處理調用服務。 為每個激活的服務自動建立遠程處理終結點。 建立與終結點同名的Flex目標，Flex客戶端可以建立指向此目標以調用相關服務上的操作的遠程對象。

## 遠程處理終結點設定 {#remoting-endpoint-settings}

**Flex客戶端認證方法：** 確定在啟用調用的服務安全性、調用的操作不支援匿名調用以及客戶端以無憑據或無效憑據傳遞時，伺服器發回給客戶端的響應類型。
