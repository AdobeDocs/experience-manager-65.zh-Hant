---
title: 設定遠端端點
description: 瞭解如何設定遠端端點。 本檔案說明如何啟用以Flex建立的應用程式，以使用AEM表單遠端功能來叫用服務。
uuid: 4d4f9274-dcae-4b9f-975a-575376c2f89c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: aab9d622-d76b-4100-9ca6-e5b86f543381
exl-id: 891d7d75-555a-46c6-a8a0-d5238b48bc79
source-git-commit: 6caf3ef4a00275f0f73be52b6a9ccba77d277f1a
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---

# 設定遠端端點 {#configuring-remoting-endpoints}

遠端端點可讓以Flex建立的應用程式使用(AEM表單已棄用) AEM表單遠端來叫用服務。 系統會自動為每個啟用的服務建立遠端端點。 會建立與端點同名的Flex目的地，而Flex使用者端可建立指向此目的地的遠端物件，以叫用相關服務的作業。

## 遠端端點設定 {#remoting-endpoint-settings}

**Flex使用者端驗證方法：** 決定當所叫用的服務已啟用安全性、叫用的作業不支援匿名叫用，且使用者端傳入的認證無效或無效認證時，伺服器傳回給使用者端的回應型別。
