---
title: 使用API執行服務操作
seo-title: Performing Service Operations Using APIs
description: 使用AEM Forms API開發用戶端應用程式。
seo-description: Develop client applications using the AEM Forms APIs.
uuid: a5697c91-d643-4265-973c-18467ca0437a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8fa1426f-f453-45c5-89b9-67038f56c70e
role: Developer
exl-id: 62489194-82ca-44f6-b5be-4411c95f6f80
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---

# 使用API執行服務操作 {#performing-service-operations-using-apis}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

開始使用AEM Forms API開發用戶端應用程式之前，建議您先閱讀叫用AEM Forms ，其中說明叫用服務的不同方式。 (請參閱 [服務容器](/help/forms/developing/service-container.md#service-container).)

熟悉不同的叫用方法後，您就可以了解如何以程式設計方式與每個服務互動。 您可以在Flex® Builder™Adobe、Java開發環境或Microsoft Visual Studio .NET等環境中開發客戶端應用程式，這些環境允許您將公開的WSDL用於本機SOAP堆棧上的消耗。

每個主題都包含簡介資訊（包括步驟摘要區段）、程式碼逐步說明和程式碼範例。 步驟摘要說明所需的子任務以及每個子任務連結至程式碼逐步中的區段。 所有主題都有「快速入門」的連結，這些是完整的程式碼範例，旨在協助您復製程式碼並貼到專案中，以快速上手。
