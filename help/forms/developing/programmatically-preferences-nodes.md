---
title: 以程式設計方式管理PreferencesNodes
seo-title: 以程式設計方式管理PreferencesNodes
description: 使用Preferences Manager Service API(Java)以程式設計方式管理Preferences節點。
seo-description: 使用Preferences Manager Service API(Java)以程式設計方式管理Preferences節點。
uuid: f0cb117a-a6cc-4ca5-8511-b3bc9f6738e9
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9d4dba7f-49d8-4112-bc8a-04dafc99a936
role: 開發人員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---


# 以程式設計方式管理偏好設定節點{#programmatically-managing-the-preferencesnodes}

**本文中的範例和範例僅適用於AEM Forms的JEE環境。**

本主題說明如何使用Preferences Manager Service API(Java)以程式設計方式管理Preferences Nodes。

您可以從管理員UI手動變更組態設定。 若要變更選項，請導覽至`Home>Settings>User Management> Configuration>Manual Configuration`。 在進行更改後導入`config.xml`，您會發現除在節點`/Adobe/Adobe Experience Manager Forms/Config/UM persist`上所做的更改外的所有更改都將丟失。 「使用者管理匯入與匯出」的預覽不支援變更其他元件的組態設定。 現在，您可使用`PreferencesManagerServiceClient` API進行這些變更。

**步驟摘**&#x200B;要要要以寫程式方式管理首選項節點，請執行以下步驟：

1. 包含專案檔案。
1. 建立PreferencesManagerService客戶端
1. 調用適當的角色或權限操作

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立PreferencesManagerService客戶端**

您必須先建立PreferencesManagerService客戶端，才能以寫程式方式執行User Management PreferencesManagerService操作。 使用Java API，您可建立PreferencesManagerServiceClient物件來完成此作業。

**調用適當的角色或權限操作**

建立服務客戶端後，可以調用「首選項管理器」操作。 服務客戶端允許您讀取和設定權限。
