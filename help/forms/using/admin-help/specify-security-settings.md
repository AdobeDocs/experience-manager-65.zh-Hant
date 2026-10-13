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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 50158d81-1c06-57f7-8bd7-e8ff76a93f85
    internal-label: Document Security
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
source-wordcount: '101'
ht-degree: 1%
---
# 指定安全性設定 {#specify-security-settings}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

輸出可讓您控制是否解析XML輸入中的外部圖元。 預設會解決問題，但您可以變更此行為以提高AEM表單系統的安全性。

**禁止處理包含外部實體參照的XML資料檔**

1. 在Administration Console中，按一下「服務>輸出」。
1. 清除「解析外部圖元」核取方塊。
1. 按一下「儲存」。
