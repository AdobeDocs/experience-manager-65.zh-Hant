---
title: 如何使用WS-security標頭傳遞憑據？
description: 了解如何使用WS-security標頭傳遞憑證
exl-id: 519d57ad-81ab-4caf-ae25-4390ae2eee13
source-git-commit: de38dbb9d0ce523543c11e665c02034f4b38f1e6
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# 使用WS-Security標頭傳遞憑據 {#using-execute-script-service-aem-forms-jee-workbench}

在JEE服務上使用網站服務叫用AEM Forms時，您可以使用WS-Security標題來傳遞JEE上AEM Forms所需的用戶端驗證資訊。 WS-Security定義SOAP擴展，以實現客戶端身份驗證、消息機密性和消息完整性。 因此，當JEE上的AEM Forms部署為獨立伺服器或在叢集環境中時，您就可以在JEE服務上叫用AEM Forms。

如何在JEE上將WS-Security標題傳遞至AEM Forms，取決於您是使用Axis產生的Java類，還是使用服務的原生SOAP堆疊的.NET用戶端程式集。

>[!NOTE]
>
>作為使用WS-Security標頭調用服務的示例，本主題通過調用加密服務來使用密碼加密PDF文檔。

本檔案涵蓋下列主題：

* 使用Axis生成的Java類傳遞客戶端驗證

* 生成調用加密服務所需的軸庫檔案

* 使用WS-Security標頭調用加密服務

* 使用.NET客戶端程式集傳遞客戶端驗證

* 使用WS-Security標頭調用加密服務


## 需求 {#requirements}

若要充分運用本檔案，您必須對JEE上的AEM Forms軟體有紮實的了解。

>[!MORELIKETHIS]
>
>* [使用WS-Security標頭傳遞憑據](assets/passing-credentials-using-ws-security-headers.pdf)

