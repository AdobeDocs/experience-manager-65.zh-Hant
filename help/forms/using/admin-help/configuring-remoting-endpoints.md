---
title: 設定遠端端點
description: 瞭解如何設定遠端端點。 本檔案說明如何啟用以Flex建立的應用程式，以使用AEM表單遠端功能來叫用服務。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 891d7d75-555a-46c6-a8a0-d5238b48bc79
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%
---
# 設定遠端端點 {#configuring-remoting-endpoints}

遠端端點可讓以Flex建立的應用程式使用（AEM表單已棄用） AEM表單遠端來叫用服務。 系統會自動為每個啟用的服務建立遠端端點。 會建立與端點同名的Flex目的地，而Flex使用者端可建立指向此目的地的遠端物件，以叫用相關服務的作業。

## 遠端端點設定 {#remoting-endpoint-settings}

**Flex使用者端驗證方法：**&#x200B;決定當所叫用的服務已啟用安全性、叫用的作業不支援匿名叫用，且使用者端傳入的認證無效或無效時，伺服器傳回給使用者端的回應型別。
