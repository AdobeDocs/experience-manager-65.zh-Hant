---
title: 連線至Adobe Analytics和建立架構
seo-title: 連線至Adobe Analytics和建立架構
description: 瞭解如何將AEM連接至SiteCatalyst並建立架構。
seo-description: 瞭解如何將AEM連接至SiteCatalyst並建立架構。
uuid: 3820dd24-4193-42ea-aef2-4669ebfeaa9d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6b545a51-3677-4ea1-ac7e-2d01ba19283e
docset: aem65
translation-type: tm+mt
source-git-commit: 4b965d8f7814816126601f6366c1ba313e404538

---


# 連線至Adobe Analytics和建立架構 {#connecting-to-adobe-analytics-and-creating-frameworks}

若要在Adobe Analytics中追蹤AEM頁面的網頁資料，請建立Adobe Analytics Cloud services設定和Adobe Analytics架構：

* **** Adobe Analytics設定：Adobe Analytics帳戶的相關資訊。 Adobe Analytics設定可讓AEM連線至Adobe Analytics。 為您使用的每個帳戶建立Adobe Analytics設定。
* **** Adobe Analytics Framework:Adobe Analytics報表套裝屬性與CQ變數之間的一組映射。 使用架構來設定網站資料填入Adobe Analytics報表的方式。 架構與Adobe Analytics組態相關聯。 您可以為每個配置建立多個框架。

將網頁與框架關聯時，框架將對該頁和該頁的後代執行跟蹤。 然後，可從Adobe Analytics擷取頁面檢視，並顯示在「網站」主控台中。

## 必備條件 {#prerequisites}

### Adobe Analytics帳戶 {#adobe-analytics-account}

若要在Adobe Analytics中追蹤AEM資料，您必須擁有有效的Adobe Marketing Cloud Adobe Analytics帳戶。

Adobe Analytics帳戶需要：

* 具有管 **理員** 權限
* 被指派給「 **Web服務訪問** 」用戶組。

>[!CAUTION]
>
>提供 **管理員** （在Adobe Analytics中）權限不足以讓使用者從AEM連線至Adobe Analytics。 帳戶也必須擁有 **Web服務存取權** 。

![chlimage_1-67](assets/chlimage_1-67.png)

繼續之前，請確定您的認證可讓您登入Adobe Analytics。 透過下列其中一種方式：

* [https://marketing.adobe.com](https://marketing.adobe.com)

* [https://sc.omniture.com/login/](https://sc.omniture.com/login/)

### 設定AEM以使用您的Adobe Analytics資料中心 {#configuring-aem-to-use-your-adobe-analytics-data-centers}

Adobe Analytics資 [料中心收集](https://developer.omniture.com/en_US/content_page/concepts-terminology/c-how-is-data-stored) 、處理及儲存與您的Adobe Analytics報表套裝相關的資料。 您必須設定AEM，以使用裝載Adobe Analytics報表套裝的資料中心。 下表列出可用的資料中心及其URL。

| 資料中心 | URL |
|---|---|
| 聖荷西 | https://api.omniture.com/admin/1.4/rest/ |
| 達拉斯 | https://api2.omniture.com/admin/1.4/rest/ |
| 倫敦 | https://api3.omniture.com/admin/1.4/rest/ |
| 新加坡 | https://api4.omniture.com/admin/1.4/rest/ |
| 俄勒岡 | https://api5.omniture.com/admin/1.4/rest/ |

AEM依預設會使用聖荷西(https://api.omniture.com/admin/1.4/rest/)資料中心。

使用 [Web Console來設定OSGi搭售](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)**Adobe AEM Analytics HTTP用戶端**。 新增 **資料中心URL** ，以代管您的AEM頁面收集資料的報表套裝的資料中心。

![aa-07](assets/aa-07.png)

1. 在您的網頁瀏覽器中開啟網頁主控台。 ([https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. 輸入您的認證以存取主控台。

   >[!NOTE]
   >
   >請連絡您的網站管理員，以瞭解您是否可存取此主控台。

1. 選取名為 **Adobe AEM Analytics HTTP Client的設定項目**。
1. 若要新增資料中心的URL，請按「資料中心URL」清單旁的+按鈕 **** ，然後在方塊中輸入URL。

1. 若要從清單中移除URL，請按一下URL旁的——按鈕。
1. 按一下「儲存」。

## 設定與Adobe Analytics的連線 {#configuring-the-connection-to-adobe-analytics}

>[!CAUTION]
>
>由於Adobe Analytics API中的安全性變更，無法再使用AEM中包含的Activity Map版本。
>
>現在 [應使用Adobe Analytics提供的](https://docs.adobe.com/content/help/en/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html) ActivityMap外掛程式。

## 為Activity map設定 {#configuring-for-the-activity-map}

>[!CAUTION]
>
>由於Adobe Analytics API中的安全性變更，無法再使用AEM中包含的Activity Map版本。
>
>現在 [應使用Adobe Analytics提供的](https://docs.adobe.com/content/help/en/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html) ActivityMap外掛程式。

## 建立Adobe Analytics Framework {#creating-a-adobe-analytics-framework}

對於您使用的報表套裝ID(RSID)，您可以控制哪些伺服器例項（作者、發佈或兩者）將資料貢獻至報表套裝：

* **全部**:來自作者和發佈例項的資訊都會填入報表套裝。
* **作者**:只有作者例項的資訊會填入報表套裝。
* **發佈**:只有來自發佈例項的資訊會填入報表套裝。

>[!NOTE]
>
>選取伺服器例項類型並不會限制對Adobe Analytics的呼叫，只會控制哪些呼叫包含RSID。
>
>例如，架構已設定為使用 *diweretail* 報表套裝，而author是選取的伺服器例項。 當頁面與架構一起發佈時，仍會對Adobe Analytics進行呼叫，但這些呼叫不包含RSID。 只有來自作者例項的呼叫會包含RSID。

1. 使用 **「Using** Invagation **」(工具**) **、「Cloud Services」（雲端服務），然後選擇「Legacy Cloud Services**」（舊式雲端服務）導 ****&#x200B;航。
1. 捲動至 **Adobe Analytics** ，然後按一 **下「可用** 組態」旁邊的[+] ****。
1. 按一 **下Adobe Analytics設定旁的** [+]連結。

1. 在「建立 **框架** 」對話框中：

   * 指定 **標題**。
   * 或者，您可以為儲存 **在儲存庫中的框架詳細資訊的節點指定名稱**。
   * 選取 **Adobe Analytics Framework**
   然後按一下 **建立**。

   此框架將開啟以供編輯。

1. 在側 **面pod（主面板右側）的** 「報表套裝」區段中，按一下「新 **增項目」**。 然後使用下拉式清單來選取框架將與之互動的報表套 `geometrixxauth`裝ID（例如）。

   >[!NOTE]
   >
   >當您選取報表套裝ID時，左側的內容搜尋器會填入Adobe Analytics變數（SiteCatalyst變數）。

1. 然後使用 **「執行模式** 」下拉式清單（在「報表套裝ID」旁），選取您要傳送資訊至報表套裝的伺服器例項。

   ![aa-framework-01](assets/aa-framework-01.png)

1. 若要讓架構在您網站的發佈例項上可用，請在sidekick的「頁面」標 **簽上** ，按一下「啟 **動架構」。**

### 設定Adobe Analytics的伺服器設定 {#configuring-server-settings-for-adobe-analytics}

架構系統可讓您變更每個Adobe Analytics架構內的伺服器設定。

>[!CAUTION]
>
>這些設定會決定您的資料的傳送位置及方式，因此您必須 *不要竄改這些設定* ，並讓Adobe Analytics代表自行設定。

從開啟面板開始。 按「 **Servers（伺服器）」旁邊的向下箭**&#x200B;頭：

![server_001](assets/server_001.png)

* **追蹤伺服器**

   * 包含用來傳送Adobe Analytics呼叫的URL

      * cname —— 預設為Adobe Analytics帳戶的公司 *名稱*
      * d1 —— 對應於要發送資訊的資料中心（可以是d1、d2或d3）
      * sc.omtrdc.net —— 域名

* **安全追蹤伺服器**

   * 具有與追蹤伺服器相同的區段
   * 這用於從安全頁面(https://)傳送資料

* **訪客命名空間**

   * 命名空間會決定追蹤URL的第一部分。
   * 例如，將命名空間變更為 **CNAME** ，將會導致對Adobe Analytics所進行的呼叫看起來像 **CNAME.d1.omtrdc.net** ，而非預設值。

## 將頁面與Adobe Analytics Framework關聯 {#associating-a-page-with-a-adobe-analytics-framework}

當頁面與Adobe Analytics架構相關聯時，頁面會在頁面載入時傳送資料至Adobe Analytics。 頁面填入的變數會從架構中的Adobe Analytics變數進行映射和擷取。 例如，頁面檢視是從Adobe Analytics擷取的。

頁面的後代繼承與框架的關聯。 例如，當您將網站的根頁面與架構建立關聯時，網站的所有頁面都會與架構建立關聯。

1. 從 **Sites** Console中，選取您要設定追蹤的頁面。
1. 直接從控 **[制台或頁面編輯器開啟「頁面屬性](/help/sites-authoring/editing-page-properties.md)**」。
1. 開啟**雲端服務**標籤。

1. 使用「 **新增設定** 」下拉式清單，從可 **用選項中選取Adobe Analytics** 。 如果放置了繼承，則需要在選擇器可用之前禁用該繼承。

1. Adobe Analytics的下拉式選 **取器** ，將附加至可用的選項。 使用此選項可選擇所需的框架配置。

1. 選擇「 **儲存並關閉**」。
1. **[發佈頁](/help/sites-authoring/publishing-pages.md)**，以啟動頁面和任何連接的組態／檔案。
1. 最後一個步驟是造訪發佈例項上的頁面，並使用 **** Search元件搜尋關鍵字（例如茄子）。
1. 然後，您可以使用適當的工具檢查對Adobe Analytics的呼叫；例如 [Adobe Marketing cloud除錯程式](https://marketing.adobe.com/resources/help/en_US/sc/implement/debugger_install.html)。
1. 在提供的範例中，呼叫應包含eVar7中輸入的值（即茄子），而事件清單應包含event3。

### 頁面檢視 {#page-views}

當頁面與Adobe Analytics架構關聯時，頁面檢視次數可顯示在網站主控台的「清單」檢視中。

如需詳 [細資訊，請參閱查看頁面分析](/help/sites-authoring/page-analytics-using.md) 資料。

### 配置導入間隔 {#configuring-the-import-interval}

設定 **Adobe AEM Managed Polling Configuration服務的適當例項** :

* **輪詢間隔**:服務從Adobe Analytics擷取頁面檢視資料的間隔（以秒為單位）。
預設間隔為43200000毫秒（12小時）。

* **啟用**:啟用或禁用服務。 預設情況下，服務處於啟用狀態。

要配置此OSGi服務，可以使用 [Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) ，或儲存庫中 [的osgiConfig節點](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) (服務PID是 `com.day.cq.polling.importer.impl.ManagedPollConfigImpl`)。

## 編輯Adobe Analytics設定和／或架構 {#editing-adobe-analytics-configurations-and-or-frameworks}

如同建立Adobe Analytics設定或架構時，導覽至（舊版） **Cloud Services畫面** 。 選擇 **顯示配置**，然後按一下指向要更新的特定配置的連結。

編輯Adobe Analytics設定時，您也需要在設定頁面本身按「編 **輯** 」按鈕，才能開啟「編輯元 **件」對話方塊** 。

## 刪除Adobe Analytics Frameworks {#deleting-adobe-analytics-frameworks}

若要刪除Adobe Analytics架構，請先開 [啟它以進行編輯](#editing-adobe-analytics-configurations-and-or-frameworks)。

然後，從 **sidekick的「頁** 面 **** 」索引標籤中選取「刪除架構」。

