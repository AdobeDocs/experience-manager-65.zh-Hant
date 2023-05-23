---
title: 使用API執行服務操作
seo-title: Performing Service Operations Using APIs
description: 使用AEM FormsAPI開發客戶端應用程式。
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

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

在開始使用AEM FormsAPI開發客戶端應用程式之前，建議您首先閱讀調用AEM Forms，它描述了調用服務的不同方式。 (請參閱 [服務容器](/help/forms/developing/service-container.md#service-container)。)

熟悉不同的調用方法後，可以學習如何以寫程式方式與每個服務交互。 您可以在AdobeFlex®構建器™、Java開發環境或MicrosoftVisual Studio .NET等環境中開發客戶端應用程式，這些環境允許您使用暴露的WSDL在本機SOAP堆棧上進行消耗。

每個主題都包括介紹性資訊（包括步驟摘要部分）、代碼檢查和代碼示例。 步驟摘要說明了所需的子任務和每個子任務連結到代碼檢查中的某個部分。 所有主題都具有指向「快速啟動」的連結，這些是完整的代碼示例，旨在通過將代碼複製並貼上到項目中來幫助您快速啟動。
