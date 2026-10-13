---
title: 以程式設計方式管理偏好設定節點
description: 使用Preferences Manager Service API (Java)以程式設計方式管理偏好設定節點。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 108eb249-879b-4e4f-b431-8118b8656e62
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 516393bc-fa69-5e74-a04e-f7ec9ffe2c5e
    internal-label: APIs & Integrations
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%
---
# 以程式設計方式管理偏好設定節點 {#programmatically-managing-the-preferencesnodes}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

本主題說明如何使用偏好設定管理員服務API (Java)以程式設計方式管理偏好設定節點。

您可以從管理員UI手動變更組態設定。 若要變更選項，請導覽至`Home>Settings>User Management> Configuration>Manual Configuration`。 進行變更後匯入`config.xml`，您會注意到除了在節點`/Adobe/Adobe Experience Manager Forms/Config/UM persist`所做的變更以外的所有變更都已遺失。 使用者管理匯入和匯出的預覽不支援變更其他元件的組態設定。 現在，可以使用`PreferencesManagerServiceClient` API進行這些變更。

**步驟摘要**&#x200B;若要以程式設計方式管理偏好設定節點，請執行下列步驟：

1. 包含專案檔案。
1. 建立PreferencesManagerService客戶端
1. 叫用適當的角色或許可權作業

**包含專案檔**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，則請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立PreferencesManagerService使用者端**

您必須先建立PreferencesManagerService使用者端，才能以程式設計方式執行User Management PreferencesManagerService作業。 使用Java API時，可藉由建立PreferencesManagerServiceClient物件來完成。

**叫用適當的角色或許可權作業**

建立服務使用者端後，您就可以叫用「偏好設定管理員」作業。 服務使用者端可讓您讀取及設定許可權。
