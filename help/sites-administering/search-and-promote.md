---
title: 與AdobeSearch&Promote整合
seo-title: 與AdobeSearch&Promote整合
description: 了解如何與AdobeSearch&Promote整合。
seo-description: 了解如何與AdobeSearch&Promote整合。
uuid: 7e9384d9-9e4f-4e00-a1c9-35547de6ceb8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: aca444f6-418a-4c01-ae19-663b4e04fab9
docset: aem65
exl-id: 15f45978-a983-49a0-91cf-c7610fc37eef
source-git-commit: 99230f2b9ce8179de4034d8bd739a5535b2cc0da
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 1%

---

# 與AdobeSearch&amp;Promote整合{#integrating-with-adobe-search-promote}

若要從您的網站呼叫AdobeSearch&amp;Promote服務，請執行下列工作：

1. 指定雲端的URL。
1. 設定與Search&amp;Promote服務的連線。
1. 將Search&amp;Promote元件新增至Sidekick。
1. 使用元件來製作內容。 (請參閱[將Search&amp;Promote功能新增至網頁](/help/sites-authoring/search-and-promote.md)。)
1. 將橫幅新增至您的頁面。 橫幅影像對Search&amp;Promote資料很敏感。
1. 產生要使用的Search&amp;Promote服務的網站地圖。

>[!NOTE]
>
>如果您使用Search&amp;Promote搭配自訂的代理設定，您需要設定兩個HTTP用戶端代理設定，因為AEM的某些功能使用3.x API，而其他一些功能則使用4.x API:
>
>* 3.x的設定為[https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x的設定為[https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>



## 變更Search&amp;Promote服務URL {#changing-the-search-promote-service-url}

為Search&amp;Promote服務配置的預設URL為`https://searchandpromote.omniture.com/px/`。 若要使用不同的服務，請使用OSGi主控台來指定不同的URL。

1. 開啟OSGi主控台，然後按一下「設定」標籤。 ([https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. 按一下Day CQSearch&amp;Promote設定項目。
1. 在「遠程伺服器URI」框中輸入URL，然後按一下「保存」。

## 配置與Search&amp;Promote{#configuring-the-connection-to-search-promote}的連接

設定一或多個與Search&amp;Promote的連線，讓您的網頁可與服務互動。 要連接，您需要Search&amp;Promote帳戶的成員標識和帳號。

1. 從&#x200B;**工具**&#x200B;表徵圖> **部署**&#x200B;中，選擇&#x200B;**Cloud Services**。

   這會帶您前往「Cloud Services控制面板」。 如果在本機電腦上，控制面板的url將如下所示：

   [https://localhost:4502/libs/cq/core/content/tools/cloudservices.html](https://localhost:4502/libs/cq/core/content/tools/cloudservices.html)

1. 在「Cloud Services」頁面中，按一下「AdobeSearch&amp;Promote」連結或「Search&amp;Promote」圖示。

1. 如果這是您第一次配置AdobeSearch&amp;Promote，請按一下&#x200B;**立即配置**&#x200B;以開啟「建立配置」面板。

   如果您想要進一步了解Search&amp;Promote，請按一下「**了解更多**」。

   ![](assets/chlimage_1-59.png)

1. 輸入頁面作者可識別的&#x200B;**標題**，然後輸入唯一的&#x200B;**名稱**，然後按一下&#x200B;**建立**。

   將開啟「**編輯元件**」窗口。

   此外，新建立的「配置」將顯示在&#x200B;**Cloud Services儀表板** AdobeSearch&amp;Promote清單項的&#x200B;**可用配置**&#x200B;下。

   ![](assets/chlimage_1-60.png)

1. 將以下內容添加到&#x200B;**編輯元件**&#x200B;對話框中的欄位。

   * **成員 ID**
   * **帳號**

   >[!NOTE]
   >
   >若要自行取得此資訊&#x200B;**，請先登入**
   >
   >[https://searchandpromote.omniture.com/center/](https://searchandpromote.omniture.com/center/)
   >
   >
   >使用有效的Seach&amp;Promote憑證（電子郵件/密碼）。
   >接著，您需要在瀏覽器的位址列中查看您的url，其看起來會像這樣：
   >[](https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY)
   >
   >[https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY](https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY)
   >
   >**其中：**
   >
   >    * **** XXXXXXXX與您的**成員id**
   >    * **** spYYYYYYYY與您的帳 **號對應**


1. 按一下&#x200B;**連接到Search&amp;Promote**。

   出現連接成功消息時，按一下「**確定**」。

   (連接後，按鈕文本將更改為** Re-Connect To Analytics**。)

1. 按一下&#x200B;**「確定」**。此時會針對您剛建立的組態顯示「Search&amp;Promote設定」頁面。

## 配置資料中心{#configuring-the-data-center}

如果您的Search&amp;Promote帳戶位於亞洲或歐洲，則需要更改預設資料中心，使其指向正確的資料中心（預設資料中心用於北美帳戶）。

配置資料中心：

1. 導覽至`https://localhost:4502/system/console/configMgr/com.day.cq.searchpromote.impl.SearchPromoteServiceImpl`的Web主控台

   ![](assets/chlimage_1-61.png)

1. 根據伺服器的位置，將URI更改為以下任一項：

   * 北美：[https://center.atomz.com/px/](https://center.atomz.com/px/)
   * 歐洲、中東和非洲：[https://center.lon5.atomz.com/px/](https://center.lon5.atomz.com/px/)
   * APAC:[https://center.sin2.atomz.com/px/](https://center.sin2.atomz.com/px/)

1. 按一下「**儲存**」。

## 將Search&amp;Promote元件新增至Sidekick {#adding-search-promote-components-to-sidekick}

在「設計」模式中，編輯&#x200B;**par**&#x200B;元件以允許Sidekick中的Search&amp;Promote元件。 （如需詳細資訊，請參閱[元件](/help/sites-developing/components.md#addinganewcomponenttotheparagraphsystemdesignmode)檔案）。

有關使用元件的資訊，請參閱[向網頁添加Search&amp;Promote功能](/help/sites-authoring/search-and-promote.md)。)

## 指定您的頁面使用{#specifying-the-search-promote-service-that-your-pages-use}的Search&amp;Promote服務

設定網頁，使其使用特定Search&amp;Promote服務。 Search&amp;Promote元件會自動使用其主機頁面的服務。

配置Search&amp;Promote的屬性時，所有子頁都會繼承設定。 如果需要，您可以配置子頁以覆蓋繼承的設定。

>[!NOTE]
>
>必須已配置服務連接。 (請參閱[設定與Search&amp;Promote](#connection)的連線。)

1. 開啟&#x200B;**頁面屬性**&#x200B;對話方塊。 例如，在** Websites**頁面上，以滑鼠右鍵按一下該頁面，然後按一下&#x200B;**Properties**。
1. 按一下&#x200B;**Cloud Services**&#x200B;標籤。
1. 若要停用上層頁面中雲端服務設定的繼承，請按一下繼承路徑旁的掛鎖圖示。

   ![](assets/sandpinheritpadlock.png)

1. 按一下「**添加服務**」，選擇「**AdobeSearch&amp;Promote**」，然後按一下「**確定**」。
1. 選擇Search&amp;Promote帳戶的連接配置，然後按一下&#x200B;**確定**。

## 產品摘要{#product-feed}

Search&amp;Promote整合可讓您：

* 使用eCommerce API，不受基礎存放庫結構和商務平台影響。
* 運用Search&amp;Promote的「索引連接器」功能，以XML格式提供產品摘要。
* 運用Search&amp;Promote的「遠端控制」功能，執行產品摘要的隨選或排程請求
* 不同Search&amp;Promote帳戶的摘要產生（設定為雲端服務設定）。

如需詳細資訊，請參閱[產品摘要](/help/sites-administering/product-feed.md)。
