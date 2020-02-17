---
title: 與Adobe Analytics整合
seo-title: 與Adobe Analytics整合
description: 瞭解如何將AEM與Adobe Analytics整合。
seo-description: 瞭解如何將AEM與Adobe Analytics整合。
uuid: d8548263-6ac5-45fb-8c70-52ecd4161bbb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 444c522e-2f33-4f41-846c-8d317e799659
docset: aem65
translation-type: tm+mt
source-git-commit: ca25e66b280db479f69c487753a557b0240233da

---


# 與Adobe Analytics整合{#integrating-with-adobe-analytics}

整合Adobe Analytics和AEM可讓您追蹤網頁活動：

* Adobe Analytics設定可讓AEM向Adobe Analytics驗證。
* 架構可識別傳送至Adobe Analytics報表套裝的資料。

資料包括頁面資料和用戶資料；例如：

* AEM元件收集的資料
* 連結點按
* 視訊使用資訊
* 來自Adobe Analytics的頁面瀏覽次數

下列頁面可協助您設定整合：

* [連線至Adobe Analytics和建立架構](/help/sites-administering/adobeanalytics-connect.md)
* [設定Adobe Analytics的連結追蹤](/help/sites-administering/adobeanalytics-link.md)
* [使用Adobe Analytics屬性對應元件資料](/help/sites-administering/adobeanalytics-mapping.md)
* [設定Adobe Analytics的視訊追蹤](/help/sites-administering/adobeanalytics-video.md)
* [Adobe分類](/help/sites-administering/adobeanalytics-classifications.md)

您也可以使用 [選擇加入精靈](/help/sites-administering/opt-in.md) ，輕鬆執行整合。

>[!NOTE]
>
>另請參閱操作說明文章：使 [用DTM將AEM與Adobe target和Adobe Analytics整合](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html)。

## 更多資訊 {#further-information}

請參閱：

* [擴充Adobe Analytics整合](/help/sites-developing/extending-analytics.md) ，以取得開發收集使用者資料的元件和自訂Adobe Analytics架構的相關資訊。
* 知識庫文章「 [Adobe Analytics整合——疑難排解問題](https://helpx.adobe.com/experience-manager/kb/sitecatalystintegrationtroubleshooting.html)」，以取得有關疑難排解Adobe Analytics整合的資訊。

>[!NOTE]
>
>如果您使用Adobe Analytics搭配自訂的代理設定，則需要 [設定](/help/sites-deploying/configuring-osgi.md) Apache HTTP Client **** Proxy設定所需的兩個OSGi組合（例如，搭配Web主控台）。 由於AEM的某些功能使用3.x API，而其他功能則使用4.x API，因此這兩者皆為必要。 設定:
>
>* **Day Commons HTTP Client 3.1** ，用以設定3.x API;
   >  例如， [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
   >
   >
* **Apache HTTP Components Proxy Configuration** to configure the 4.x API;
   >  例如， [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>



