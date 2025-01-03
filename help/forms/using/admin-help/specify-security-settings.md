---
title: 指定安全性設定
description: 瞭解如何指定安全性設定以保護XML資料檔案。 安全性設定功能可控制XML輸入中的外部圖元。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1f544485-5a01-4a4a-ab0f-dcee67e1a38b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 1%

---

# 指定安全性設定 {#specify-security-settings}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

輸出可讓您控制是否解析XML輸入中的外部圖元。 預設會解決這些問題，但您可以變更此行為以提高AEM表單系統的安全性。

**禁止處理包含外部實體參照的XML資料檔**

1. 在Administration Console中，按一下「服務>輸出」。
1. 清除「解析外部圖元」核取方塊。
1. 按一下「儲存」。
