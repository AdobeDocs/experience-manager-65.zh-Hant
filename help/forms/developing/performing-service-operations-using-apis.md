---
title: 使用API執行服務作業
description: 使用AEM Forms API開發使用者端應用程式。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 62489194-82ca-44f6-b5be-4411c95f6f80
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
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
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%
---
# 使用API執行服務作業 {#performing-service-operations-using-apis}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

開始使用AEM Forms API開發使用者端應用程式之前，Adobe建議您先閱讀叫用AEM Forms ，其中會說明叫用服務的不同方式。 （請參閱[服務容器](/help/forms/developing/service-container.md#service-container)。）

熟悉不同的叫用方法後，您就可以瞭解如何以程式設計方式與每個服務互動。 您可以在Adobe Flex® Builder™、Java™開發環境或Microsoft® Visual Studio .NET等環境中開發使用者端應用程式，讓您使用公開的WSDL在原生SOAP棧疊上消耗。

每個主題都包含簡介資訊（包括步驟摘要區段）、程式碼逐步解說和程式碼範例。 步驟摘要會說明必要的子任務，以及程式碼逐步說明中指向區段的每個子任務連結。 所有主題都有快速入門連結，這些是完整的程式碼範例，設計旨在透過復製程式碼並將其貼到專案中，協助您快速入門。
