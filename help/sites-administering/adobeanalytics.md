---
title: 整合 Adobe Analytics
description: 瞭解如何將Adobe Experience Manager (AEM)與Adobe Analytics整合。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 0a87ece4-57ed-4022-a78a-264c1edf4b4e
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 243139ec-8e41-5296-a287-31343ab1bc0f
    internal-label: Integration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 22%
---
# 整合 Adobe Analytics{#integrating-with-adobe-analytics}

整合Adobe Analytics和AEM可讓您追蹤您的網頁活動：

* Adobe Analytics設定可讓AEM使用Adobe Analytics進行驗證。
* 框架可識別傳送至Adobe Analytics報表套裝的資料。

資料包括頁面和使用者資料；例如：

* AEM元件收集的資料
* 連結點按次數
* 視訊使用資訊
* 來自Adobe Analytics的頁面瀏覽數

下列頁面可協助您設定整合：

* [連線到Adobe Analytics並建立框架](/help/sites-administering/adobeanalytics-connect.md)
* [設定Adobe Analytics的連結追蹤](/help/sites-administering/adobeanalytics-link.md)
* [使用Adobe Analytics屬性對應元件資料](/help/sites-administering/adobeanalytics-mapping.md)
* [設定Adobe Analytics的視訊追蹤](/help/sites-administering/adobeanalytics-video.md)
* [Adobe分類](/help/sites-administering/adobeanalytics-classifications.md)

您也可以使用[選擇加入精靈](/help/sites-administering/opt-in.md)輕鬆執行整合。

>[!NOTE]
>
>另請參閱作法文章： [使用DTM整合AEM與Adobe Target和Adobe Analytics](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html)。

## 更多資訊 {#further-information}

請參閱：

* [延伸Adobe Analytics整合](/help/sites-developing/extending-analytics.md)，以取得有關開發收集使用者資料的元件以及自訂Adobe Analytics架構的資訊。

>[!NOTE]
>
>如果您使用Adobe Analytics搭配自訂的代理設定，則需要 [設定](/help/sites-deploying/configuring-osgi.md) Apache HTTP Client **** Proxy設定所需的兩個OSGi組合 (例如，搭配Web主控台)。 由於AEM的某些功能使用3.x API，而其他功能則使用4.x API，因此這兩者皆為必要。 設定：
>
>* **Day Commons HTTP Client 3.1**以設定3.x API；
>  例如，[https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>
>* **Apache HTTP元件Proxy設定**以設定4.x API；
>  例如，[https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>
