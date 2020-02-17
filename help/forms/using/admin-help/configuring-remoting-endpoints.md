---
title: 配置遠程端點
seo-title: 配置遠程端點
description: 瞭解如何設定遠端端點。
seo-description: 瞭解如何設定遠端端點。
uuid: 4d4f9274-dcae-4b9f-975a-575376c2f89c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: aab9d622-d76b-4100-9ca6-e5b86f543381
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 配置遠程端點 {#configuring-remoting-endpoints}

遠端端點可讓使用Flex建立的應用程式，使用（AEM表單不建議使用）AEM表單Remoting來叫用服務。 系統會為每個激活的服務自動建立遠程端點。 建立的Flex目標與端點名稱相同，而Flex用戶端可建立指向此目標的遠端物件，以叫用相關服務的作業。

## 刪除端點設定 {#remoting-endpoint-settings}

**** Flex用戶端驗證方法：確定在啟用安全性時，伺服器向客戶端發送的響應類型，調用的操作不支援匿名調用，並且客戶端傳遞無或無效的憑據。
