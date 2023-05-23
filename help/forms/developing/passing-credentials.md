---
title: 使用WS安全標頭傳遞憑據
description: 瞭解如何使用WS安全標頭傳遞憑據
exl-id: 519d57ad-81ab-4caf-ae25-4390ae2eee13
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# 使用WS-Security標頭傳遞憑據 {#using-execute-script-service-aem-forms-jee-workbench}

在使用Web服務調用JEE服務上的AEM Forms時，可以使用WS-Security標頭傳遞AEM Forms在JEE上要求的客戶端身份驗證資訊。 WS-Security定義SOAP擴展以實現客戶端身份驗證、消息機密性和消息完整性。 因此，當JEE上的AEM Forms部署為獨立伺服器或在群集環境中時，可以調用JEE服務上的AEM Forms。

如何將WS-Security標頭傳遞到JEE上的AEM Forms，取決於您是使用Axis生成的Java類還是使用服務的本機SOAP堆棧的.NET客戶端程式集。

>[!NOTE]
>
>作為使用WS-Security標頭調用服務的示例，本主題通過調用加密服務來使用口令加密PDF文檔。

本文檔涵蓋以下主題：

* 使用Axis生成的Java類傳遞客戶端身份驗證

* 生成調用加密服務所需的軸庫檔案

* 使用WS-Security標頭調用加密服務

* 使用.NET客戶端程式集傳遞客戶端身份驗證

* 使用WS-Security標頭調用加密服務


## 要求 {#requirements}

為了充分利用本文檔，您需要對JEE軟體上的AEM Forms有深入的瞭解。

>[!MORELIKETHIS]
>
>* [使用WS-Security標頭傳遞憑據](assets/passing-credentials-using-ws-security-headers.pdf)

