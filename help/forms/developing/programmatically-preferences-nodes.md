---
title: 以寫程式方式管理PreferencesNodes
seo-title: Programmatically managing the PreferencesNodes
description: 使用「首選項管理器」服務API(Java)以寫程式方式管理「首選項節點」。
seo-description: Use the Preferences Manager Service API (Java) to programmatically manage the Preferences Nodes.
uuid: f0cb117a-a6cc-4ca5-8511-b3bc9f6738e9
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9d4dba7f-49d8-4112-bc8a-04dafc99a936
role: Developer
exl-id: 108eb249-879b-4e4f-b431-8118b8656e62
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# 以寫程式方式管理首選項節點 {#programmatically-managing-the-preferencesnodes}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

本主題介紹如何使用首選項管理器服務API(Java)以寫程式方式管理首選項節點。

可以從管理員UI手動更改配置設定。 要更改選項，請導航至 `Home>Settings>User Management> Configuration>Manual Configuration`。 導入 `config.xml` 進行更改後，您會注意到除在節點上所做的更改外的所有更改 `/Adobe/Adobe Experience Manager Forms/Config/UM persist` 就丟了。 用戶管理導入和導出的預覽不支援更改其他元件的配置設定。 現在，可以使用 `PreferencesManagerServiceClient` API。

**步驟摘要**&#x200B;要以寫程式方式管理「首選項節點」，請執行以下步驟：

1. 包括項目檔案。
1. 建立PreferencesManagerService客戶端
1. 調用適當的角色或權限操作

**包括項目檔案**

在開發項目中包括必要的檔案。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立PreferencesManagerService客戶端**

在以寫程式方式執行用戶管理首選項ManagerService操作之前，必須建立PreferencesManagerService客戶端。 使用Java API，可通過建立PreferencesManagerServiceClient對象來完成此操作。

**調用適當的角色或權限操作**

建立服務客戶端後，可以調用「首選項管理器」(Preferences Manager)操作。 服務客戶端允許您讀取和設定權限。
