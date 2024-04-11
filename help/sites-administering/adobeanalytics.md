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
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 26%

---

# 整合 Adobe Analytics{#integrating-with-adobe-analytics}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/integrations/integrating-adobe-analytics.html) |
| AEM 6.5 | 本文章 |


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

您也可以使用 [選擇加入精靈](/help/sites-administering/opt-in.md) 以輕鬆執行整合。

>[!NOTE]
>
>另請參閱作法文章： [使用DTM整合AEM與Adobe Target和Adobe Analytics](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

## 更多資訊 {#further-information}

請參閱：

* [擴充Adobe Analytics整合](/help/sites-developing/extending-analytics.md) 有關開發會收集使用者資料的元件以及自訂Adobe Analytics架構的資訊。
* 知識庫文章， [Adobe Analytics整合 — 疑難排解問題](https://helpx.adobe.com/experience-manager/kb/sitecatalystintegrationtroubleshooting.html)，以取得疑難排解Adobe Analytics整合的相關資訊。

>[!NOTE]
>
>如果您使用Adobe Analytics搭配自訂的代理設定，則需要 [設定](/help/sites-deploying/configuring-osgi.md) Apache HTTP Client **** Proxy設定所需的兩個OSGi組合 (例如，搭配Web主控台)。由於AEM的某些功能使用3.x API，而其他功能則使用4.x API，因此這兩者皆為必要。設定：
>
>* **Day Commons HTTP使用者端3.1** 設定3.x API；
>  例如， [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>
>* **Apache HTTP元件Proxy設定** 設定4.x API；
>  例如， [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>
