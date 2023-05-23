---
title: 整合 Adobe Analytics
seo-title: Integrating with Adobe Analytics
description: 學習如何與AEMAdobe Analytics融合。
seo-description: Learn how to integrate AEM with Adobe Analytics.
uuid: d8548263-6ac5-45fb-8c70-52ecd4161bbb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 444c522e-2f33-4f41-846c-8d317e799659
docset: aem65
exl-id: 0a87ece4-57ed-4022-a78a-264c1edf4b4e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 21%

---

# 整合 Adobe Analytics{#integrating-with-adobe-analytics}

整合Adobe AnalyticsAEM並允許您跟蹤網頁活動：

* Adobe Analytics配置可AEM以向Adobe Analytics驗證。
* 框架標識發送到您的Adobe Analytics報告套件的資料。

資料包括頁面和用戶資料；例如：

* 元件收AEM集的資料
* 連結按一下
* 視頻使用資訊
* Adobe Analytics的頁面訪問次數

以下頁可幫助您配置整合：

* [連接到Adobe Analytics並建立框架](/help/sites-administering/adobeanalytics-connect.md)
* [為Adobe Analytics配置鏈路跟蹤](/help/sites-administering/adobeanalytics-link.md)
* [使用Adobe Analytics屬性映射元件資料](/help/sites-administering/adobeanalytics-mapping.md)
* [為Adobe Analytics配置視頻跟蹤](/help/sites-administering/adobeanalytics-video.md)
* [Adobe分類](/help/sites-administering/adobeanalytics-classifications.md)

您還可以使用 [選擇加入嚮導](/help/sites-administering/opt-in.md) 輕鬆執行整合。

>[!NOTE]
>
>另請參見「how-to」文章： [使用AEMDTM與Adobe Target和Adobe Analytics整合](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html)。

## 更多資訊 {#further-information}

請參閱：

* [擴大Adobe Analytics一體化](/help/sites-developing/extending-analytics.md) 有關開發收集用戶資料和自定義Adobe Analytics框架的元件的資訊。
* 知識庫文章， [Adobe Analytics整合 — 故障排除](https://helpx.adobe.com/experience-manager/kb/sitecatalystintegrationtroubleshooting.html)，以獲取有關診斷您的Adobe Analytics整合的資訊。

>[!NOTE]
>
>如果您使用Adobe Analytics搭配自訂的代理設定，則需要 [設定](/help/sites-deploying/configuring-osgi.md) Apache HTTP Client **** Proxy設定所需的兩個OSGi組合 (例如，搭配Web主控台)。由於AEM的某些功能使用3.x API，而其他功能則使用4.x API，因此這兩者皆為必要。設定:
>
>* **Day Commons HTTP Client 3.1** 配置3.x API;
   >  比如說， [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>
>* **Apache HTTP元件代理配置** 配置4.x API;
   >  比如說， [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>

