---
title: 使用WS-security標頭傳遞認證
description: 瞭解如何使用WS-security標頭傳遞認證
exl-id: 519d57ad-81ab-4caf-ae25-4390ae2eee13
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 50158d81-1c06-57f7-8bd7-e8ff76a93f85
    internal-label: Document Security
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%
---
# 使用WS-Security標頭傳遞認證 {#using-execute-script-service-aem-forms-jee-workbench}

使用網路服務在JEE服務上叫用AEM Forms時，您可以使用WS-Security標頭來傳遞JEE上AEM Forms所需的使用者端驗證資訊。 WS-Security定義SOAP擴充功能，以實作使用者端驗證、訊息機密性及訊息完整性。 因此，當JEE上的AEM Forms部署為獨立伺服器或叢集環境時，您可以叫用JEE上的AEM Forms 。

如何在JEE上將WS-Security標頭傳遞至AEM Forms，取決於您是使用軸產生的Java類別，還是使用服務的原生SOAP棧疊的.NET使用者端元件。

>[!NOTE]
>
>作為使用WS-Security標頭叫用服務的範例，本主題會叫用加密服務以密碼加密PDF檔案。

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
