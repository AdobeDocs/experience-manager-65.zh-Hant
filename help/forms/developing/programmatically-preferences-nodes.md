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
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '244'
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
