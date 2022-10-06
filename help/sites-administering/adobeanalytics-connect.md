---
title: 連接Adobe Analytics和建立框架
seo-title: Connecting to Adobe Analytics and Creating Frameworks
description: 了解如何將AEM連線至SiteCatalyst及建立架構。
seo-description: Learn about connecting AEM to SiteCatalyst and creating frameworks.
uuid: 3820dd24-4193-42ea-aef2-4669ebfeaa9d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6b545a51-3677-4ea1-ac7e-2d01ba19283e
docset: aem65
exl-id: 8262bbf9-a982-479b-a2b5-f8782dd4182d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 8%

---

# 連接Adobe Analytics和建立框架 {#connecting-to-adobe-analytics-and-creating-frameworks}

若要在Adobe Analytics中追蹤AEM頁面的網頁資料，請建立Adobe Analytics Cloud服務設定和Adobe Analytics架構：

* **Adobe Analytics設定：** Adobe Analytics帳戶的相關資訊。 Adobe Analytics設定可讓AEM連線至Adobe Analytics。 為您使用的每個帳戶建立Adobe Analytics設定。
* **Adobe Analytics架構：** Adobe Analytics報表套裝屬性與CQ變數之間的對應集。 使用架構來設定網站資料如何填入Adobe Analytics報表。 架構與Adobe Analytics設定相關聯。 您可以為每個設定建立多個架構。

將網頁與框架關聯時，框架將執行該頁和該頁的子體的跟蹤。 然後可從Adobe Analytics擷取頁面檢視，並顯示在Sites主控台中。

## 必備條件 {#prerequisites}

### Adobe Analytics帳戶 {#adobe-analytics-account}

若要在Adobe Analytics中追蹤AEM資料，您必須具備有效的Adobe Marketing Cloud Adobe Analytics帳戶。

Adobe Analytics帳戶需要：

* 有 **管理員** 權限
* 指派給 **網站服務存取** 使用者群組。

>[!CAUTION]
>
>提供 **管理員** 權限(在Adobe Analytics內)不足以讓使用者從AEM連線至Adobe Analytics。 帳戶也必須 **網站服務存取** 權限。

![chlimage_1-67](assets/chlimage_1-67.png)

繼續之前，請確定您的認證可讓您登入Adobe Analytics。 透過下列其中一種方式：

* [Adobe Experience Cloud登入](https://login.experiencecloud.adobe.com/exc-content/login.html)

* [Adobe Analytics登入](https://sc.omniture.com/login/)

### 設定AEM以使用您的Adobe Analytics資料中心 {#configuring-aem-to-use-your-adobe-analytics-data-centers}

Adobe Analytics [資料中心](https://developer.omniture.com/en_US/content_page/concepts-terminology/c-how-is-data-stored) 收集、處理和儲存與您的Adobe Analytics報表套裝相關聯的資料。 您必須將AEM設定為使用托管Adobe Analytics報表套裝的資料中心。 下表列出可用的資料中心及其URL。

| 資料中心 | URL |
|---|---|
| 聖荷西 | https://api.omniture.com/admin/1.4/rest/ |
| 達拉斯 | https://api2.omniture.com/admin/1.4/rest/ |
| 倫敦 | https://api3.omniture.com/admin/1.4/rest/ |
| 新加坡 | https://api4.omniture.com/admin/1.4/rest/ |
| 俄勒岡 | https://api5.omniture.com/admin/1.4/rest/ |

AEM預設會使用聖荷西(https://api.omniture.com/admin/1.4/rest/)資料中心。

使用 [配置OSGi捆綁包的Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) **AdobeAEM Analytics HTTP用戶端**. 新增 **資料中心URL** 用於資料中心，其中包含您的AEM頁面收集資料的報表套裝。

![aa-07](assets/aa-07.png)

1. 在網頁瀏覽器中開啟Web主控台。 ([https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. 輸入您的憑證以存取主控台。

   >[!NOTE]
   >
   >請連絡您的網站管理員，了解您是否擁有此主控台的存取權。

1. 選擇名為的配置項 **AdobeAEM Analytics HTTP用戶端**.
1. 若要新增資料中心的URL，請按 **資料中心URL** 清單，然後在方塊中輸入URL。

1. 若要從清單中移除URL，請按一下URL旁的 — 按鈕。
1. 按一下「儲存」。

## 設定與Adobe Analytics的連線 {#configuring-the-connection-to-adobe-analytics}

>[!CAUTION]
>
>由於 Adobe Analytics API 中的安全性變更，AEM 中包含的 Activity Map 版本已無法再使用。
>
>此 [ActivityMap外掛程式由Adobe Analytics提供](https://docs.adobe.com/content/help/zh-Hant/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html) 現在應該使用。

## 為Activity Map配置 {#configuring-for-the-activity-map}

>[!CAUTION]
>
>由於 Adobe Analytics API 中的安全性變更，AEM 中包含的 Activity Map 版本已無法再使用。
>
>此 [ActivityMap外掛程式由Adobe Analytics提供](https://docs.adobe.com/content/help/en/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html) 現在應該使用。

## 建立Adobe Analytics架構 {#creating-a-adobe-analytics-framework}

對於您使用的報表套裝ID(RSID)，您可以控制哪些伺服器例項（製作、發佈或兩者）會對報表套裝貢獻資料：

* **全部**:製作和發佈例項的資訊會填入報表套裝。
* **作者**:只有來自製作例項的資訊會填入報表套裝。
* **發佈**:只有來自發佈例項的資訊會填入報表套裝。

>[!NOTE]
>
>選取伺服器例項類型並不會限制對Adobe Analytics的呼叫，而只會控制哪些呼叫包含RSID。
>
>例如，框架已設定為使用 *diweretail* 報表套裝和作者是選取的伺服器例項。 當頁面連同架構一起發佈時，仍會呼叫Adobe Analytics，但這些呼叫不包含RSID。 來自製作例項的呼叫僅包含RSID。

1. 使用 **導覽**，選取 **工具**, **Cloud Services**，然後 **舊版Cloud Services**.
1. 捲動至 **Adobe Analytics** 選取 **顯示配置**.
1. 按一下 **[+]** 連結至您的Adobe Analytics設定。

1. 在 **建立框架** 對話框：

   * 指定 **標題**.
   * （可選）您可以指定 **名稱**，用於儲儲存存庫中框架詳細資訊的節點。
   * 選擇 **Adobe Analytics架構**

   然後按一下 **建立**.

   架構隨即開啟供編輯。

1. 在 **報表套裝** 按一下側面盒（主面板右側）的「 」部分 **新增項目**. 然後使用下拉式清單來選取報表套裝ID(例如 `geometrixxauth`)，架構將與此互動。

   >[!NOTE]
   >
   >選取報表套裝ID時，左側的內容尋找器會填入Adobe Analytics變數(SiteCatalyst變數)。

1. 然後使用 **運行模式** 下拉式清單（位於報表套裝ID旁），以選取您要傳送資訊至報表套裝的伺服器例項。

   ![aa-framework-01](assets/aa-framework-01.png)

1. 若要讓架構可在網站的發佈例項上使用，請前往 **頁面** sidekick標籤，按一下 **啟動框架。**

### 配置Adobe Analytics的伺服器設定 {#configuring-server-settings-for-adobe-analytics}

架構系統可讓您變更每個Adobe Analytics架構內的伺服器設定。

>[!CAUTION]
>
>這些設定會決定資料的傳送位置及傳送方式，因此您必須 *不篡改這些設定* 讓您的Adobe Analytics代表改為設定。

首先，開啟面板。 按旁邊的向下箭頭 **伺服器**:

![server_001](assets/server_001.png)

* **追蹤伺服器**

   * 包含用於傳送Adobe Analytics呼叫的URL

      * cname — 預設為Adobe Analytics帳戶的 *公司名稱*
      * d1 — 與資料中心相對應，資訊將傳送至（可為d1、d2或d3）
      * sc.omtrdc.net — 網域名稱

* **安全追蹤伺服器**

   * 與追蹤伺服器有相同的區段
   * 這可用來從安全頁面傳送資料(https://)

* **訪客命名空間**

   * 命名空間會決定追蹤URL的第一部分。
   * 例如，將命名空間變更為 **CNAME** 會讓對Adobe Analytics的呼叫看起來像 **CNAME.d1.omtrdc.net** 而非預設值。

## 將頁面與Adobe Analytics架構關聯 {#associating-a-page-with-a-adobe-analytics-framework}

將頁面與Adobe Analytics架構建立關聯時，頁面會在頁面載入時傳送資料至Adobe Analytics。 頁面填入的變數會在架構中對應，並從Adobe Analytics變數中擷取。 例如，頁面檢視是從Adobe Analytics擷取。

頁面的後代繼承與框架的關聯。 例如，將網站的根頁面與框架相關聯時，網站的所有頁面都與框架相關聯。

1. 從 **網站** 控制台，選取您要設定追蹤的頁面。
1. 開啟 **[頁面屬性](/help/sites-authoring/editing-page-properties.md)**，可直接從主控台或頁面編輯器。
1. 開啟**Cloud Services**標籤。

1. 使用 **新增設定** 下拉式清單選取 **Adobe Analytics** 中。 如果已放置繼承，則需要在選取器可用前停用該功能。

1. 的下拉式選取器 **Adobe Analytics** 會附加至可用選項。 使用此選項可選擇所需的框架配置。

1. 選擇 **儲存並關閉**.
1. **[發佈](/help/sites-authoring/publishing-pages.md)** 用於激活該頁和所有連接的配置/檔案的頁。
1. 最後一步是瀏覽發佈例項上的頁面，並使用 **搜尋** 元件。
1. 之後，您就可以使用適當的工具來檢查對Adobe Analytics進行的呼叫；例如， [Adobe Experience Cloud Debugger](https://docs.adobe.com/content/help/en/debugger/using/experience-cloud-debugger.html).
1. 在提供的範例中，呼叫應包含eVar7中輸入的值（即茄子），而事件清單應包含event3。

### 頁面檢視 {#page-views}

將頁面與Adobe Analytics架構關聯時，頁面檢視的數量會顯示在Sites主控台的「清單」檢視中。

請參閱 [查看頁面分析資料](/help/sites-authoring/page-analytics-using.md) 以取得詳細資訊。

### 配置導入間隔 {#configuring-the-import-interval}

設定的適當例項 **AdobeAEM管理輪詢配置** 服務：

* **輪詢間隔**:服務從Adobe Analytics擷取頁面檢視資料的間隔（以秒為單位）。
預設間隔為43200000毫秒（12小時）。

* **啟用**:啟用或停用服務。 預設會啟用服務。

若要設定此OSGi服務，您可以使用 [Web主控台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 或 [存放庫中的osgiConfig節點](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) (服務PID為 `com.day.cq.polling.importer.impl.ManagedPollConfigImpl`)。

## 編輯Adobe Analytics設定和/或架構 {#editing-adobe-analytics-configurations-and-or-frameworks}

如同建立Adobe Analytics設定或架構時，請導覽至（舊版） **Cloud Services** 螢幕。 選擇 **顯示配置**，然後按一下連結至您要更新的特定設定。

編輯Adobe Analytics設定時，您也需要按下 **編輯** 按鈕 **編輯元件** 對話框。

## 刪除Adobe Analytics架構 {#deleting-adobe-analytics-frameworks}

若要刪除Adobe Analytics架構，請先 [開啟供編輯](#editing-adobe-analytics-configurations-and-or-frameworks).

然後選取 **刪除框架** 從 **頁面** sidekick的標籤。
