---
title: 使用WS-security標頭傳遞認證
description: 瞭解如何使用WS-security標頭傳遞認證
exl-id: 519d57ad-81ab-4caf-ae25-4390ae2eee13
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---

# 使用WS-Security標頭傳遞認證 {#using-execute-script-service-aem-forms-jee-workbench}

使用網路服務在JEE服務上叫用AEM Forms時，您可以使用WS-Security標頭來傳遞JEE上AEM Forms所需的使用者端驗證資訊。 WS-Security定義SOAP擴充功能，以實作使用者端驗證、訊息機密性及訊息完整性。 因此，當JEE上的AEM Forms部署為獨立伺服器或叢集環境時，您可以叫用JEE上的AEM Forms 。

如何在JEE上將WS-Security標頭傳遞至AEM Forms取決於您是使用軸產生的Java類別，還是使用服務的原生SOAP棧疊的.NET使用者端元件。

>[!NOTE]
>
>作為使用WS-Security標頭叫用服務的範例，本主題會叫用Encryption服務，以密碼加密PDF檔案。

本檔案涵蓋下列主題：

* 使用Axis產生的Java類別傳遞使用者端驗證

* 產生呼叫加密服務所需的Axis程式庫檔案

* 使用WS-Security標頭叫用加密服務

* 使用.NET使用者端元件傳遞使用者端驗證

* 使用WS-Security標頭叫用加密服務


## 要求 {#requirements}

若要充分運用本檔案，您必須對JEE軟體上的AEM Forms有深入的瞭解。

>[!MORELIKETHIS]
>
>* [使用WS-Security標頭傳遞認證](assets/passing-credentials-using-ws-security-headers.pdf)
