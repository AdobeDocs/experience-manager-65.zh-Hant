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
source-git-commit: 8279cd590244a7f2d20cfaf1c7505a3ef57fae4a
workflow-type: tm+mt
source-wordcount: '1550'
ht-degree: 3%

---


# 連線至Adobe Analytics並建立架構{#connecting-to-adobe-analytics-and-creating-frameworks}

若要在Adobe Analytics中追蹤AEM頁面的網頁資料，請建立Adobe Analytics Cloud Services設定和Adobe Analytics架構：

* **Adobe Analytics設定：** Adobe Analytics帳戶的相關資訊。Adobe Analytics設定可讓AEM連線至Adobe Analytics。 為您使用的每個帳戶建立Adobe Analytics設定。
* **Adobe Analytics Framework:Adobe** Analytics報表套裝屬性與CQ變數之間的一組對應。使用架構來設定網站資料填入Adobe Analytics報表的方式。 架構與Adobe Analytics組態相關聯。 您可以為每個配置建立多個框架。

將網頁與框架關聯時，框架將對該頁和該頁的後代執行跟蹤。 然後，可從Adobe Analytics擷取頁面檢視，並顯示在「網站」主控台中。

## 必備條件 {#prerequisites}

### Adobe Analytics帳戶{#adobe-analytics-account}

若要在Adobe Analytics中追蹤AEM資料，您必須擁有有效的Adobe Marketing Cloud Adobe Analytics帳戶。

Adobe Analytics帳戶需要：

* 具有&#x200B;**管理員**&#x200B;權限
* 被指派給&#x200B;**Web服務訪問**&#x200B;用戶組。

>[!CAUTION]
>
>提供&#x200B;**管理員**&#x200B;權限（在Adobe Analytics中）不足以讓使用者從AEM連線至Adobe Analytics。 帳戶還必須具有&#x200B;**Web服務訪問**&#x200B;權限。

![chlimage_1-67](assets/chlimage_1-67.png)

繼續之前，請確定您的認證可讓您登入Adobe Analytics。 透過下列其中一種方式：

* [Adobe Experience Cloud登入](https://login.experiencecloud.adobe.com/exc-content/login.html)

* [Adobe Analytics登入](https://sc.omniture.com/login/)

### 設定AEM以使用您的Adobe Analytics資料中心{#configuring-aem-to-use-your-adobe-analytics-data-centers}

Adobe Analytics [資料中心](https://developer.omniture.com/en_US/content_page/concepts-terminology/c-how-is-data-stored)會收集、處理及儲存與您的Adobe Analytics報表套裝相關的資料。 您必須設定AEM，以使用裝載Adobe Analytics報表套裝的資料中心。 下表列出可用的資料中心及其URL。

| 資料中心 | URL |
|---|---|
| 聖荷西 | https://api.omniture.com/admin/1.4/rest/ |
| 達拉斯 | https://api2.omniture.com/admin/1.4/rest/ |
| 倫敦 | https://api3.omniture.com/admin/1.4/rest/ |
| 新加坡 | https://api4.omniture.com/admin/1.4/rest/ |
| 俄勒岡 | https://api5.omniture.com/admin/1.4/rest/ |

AEM依預設會使用聖荷西(https://api.omniture.com/admin/1.4/rest/)資料中心。

使用[Web Console來設定OSGi bundle](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) **Adobe AEM Analytics HTTP Client**。 為資料中心新增&#x200B;**資料中心URL**，該資料中心托管您的AEM頁面收集資料的報表套裝。

![aa-07](assets/aa-07.png)

1. 在您的網頁瀏覽器中開啟網頁主控台。 ([https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. 輸入您的認證以存取主控台。

   >[!NOTE]
   >
   >請連絡您的網站管理員，以瞭解您是否可存取此主控台。

1. 選取名為&#x200B;**Adobe AEM Analytics HTTP Client**&#x200B;的設定項目。
1. 要添加資料中心的URL，請按&#x200B;**資料中心URL**&#x200B;清單旁的+按鈕，然後在框中鍵入URL。

1. 若要從清單中移除URL，請按一下URL旁的——按鈕。
1. 按一下「儲存」。

## 設定Adobe Analytics {#configuring-the-connection-to-adobe-analytics}的連線

>[!CAUTION]
>
>由於Adobe Analytics API中的安全性變更，無法再使用AEM中包含的Activity Map版本。
>
>Adobe Analytics](https://docs.adobe.com/content/help/en/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html)提供的[ActivityMap外掛程式現在應該使用。

## 為Activity Map {#configuring-for-the-activity-map}進行配置

>[!CAUTION]
>
>由於Adobe Analytics API中的安全性變更，無法再使用AEM中包含的Activity Map版本。
>
>Adobe Analytics](https://docs.adobe.com/content/help/en/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html)提供的[ActivityMap外掛程式現在應該使用。

## 建立Adobe Analytics Framework {#creating-a-adobe-analytics-framework}

對於您使用的報表套裝ID(RSID)，您可以控制哪些伺服器例項（作者、發佈或兩者）將資料貢獻至報表套裝：

* **全部**:來自作者和發佈例項的資訊都會填入報表套裝。
* **作者**:只有作者例項的資訊會填入報表套裝。
* **發佈**:只有來自發佈例項的資訊會填入報表套裝。

>[!NOTE]
>
>選取伺服器例項類型並不會限制對Adobe Analytics的呼叫，只會控制哪些呼叫包含RSID。
>
>例如，架構已設定為使用&#x200B;*diweretail*&#x200B;報表套裝，而作者是選取的伺服器例項。 當頁面與架構一起發佈時，仍會對Adobe Analytics進行呼叫，但這些呼叫不包含RSID。 只有來自作者例項的呼叫會包含RSID。

1. 使用&#x200B;**Navigation**，選擇&#x200B;**Tools**、**Cloud Services**，然後選擇&#x200B;**Legacy Cloud Services**。
1. 捲動至&#x200B;**Adobe Analytics**，然後選取&#x200B;**顯示設定**。
1. 按一下Adobe Analytics設定旁的&#x200B;**[+]**&#x200B;連結。

1. 在&#x200B;**建立框架**&#x200B;對話框中：

   * 指定&#x200B;**Title**。
   * 或者，您可以為儲存庫中儲存框架詳細資訊的節點指定&#x200B;**名稱**。
   * 選擇&#x200B;**Adobe Analytics Framework**

   然後按一下&#x200B;**建立**。

   此框架將開啟以供編輯。

1. 在側面pod的&#x200B;**報表套裝**&#x200B;區段（主面板右側）中，按一下「新增項目」。 ****&#x200B;然後使用下拉式清單來選取框架將與之互動的報表套裝ID（例如`geometrixxauth`）。

   >[!NOTE]
   >
   >當您選取報表套裝ID時，左側的內容搜尋器會填入Adobe Analytics變數（SiteCatalyst變數）。

1. 然後使用&#x200B;**執行模式**&#x200B;下拉式清單（位於報表套裝ID旁）來選取您要傳送資訊至報表套裝的伺服器例項。

   ![aa-framework-01](assets/aa-framework-01.png)

1. 若要讓架構在您網站的發佈例項上可用，請在sidekick的&#x200B;**Page**&#x200B;標籤上，按一下「啟動架構」。****

### 設定Adobe Analytics的伺服器設定{#configuring-server-settings-for-adobe-analytics}

架構系統可讓您變更每個Adobe Analytics架構內的伺服器設定。

>[!CAUTION]
>
>這些設定會決定您的資料的傳送位置及傳送方式，因此您必須&#x200B;*不要竄改這些設定*，並讓您的Adobe Analytics代表自行設定。

從開啟面板開始。 按&#x200B;**Servers**&#x200B;旁邊的向下箭頭：

![server_001](assets/server_001.png)

* **追蹤伺服器**

   * 包含用來傳送Adobe Analytics呼叫的URL

      * cname —— 預設為Adobe Analytics帳戶的&#x200B;*公司名稱*
      * d1 —— 對應於要發送資訊的資料中心（可以是d1、d2或d3）
      * sc.omtrdc.net —— 域名

* **安全追蹤伺服器**

   * 具有與追蹤伺服器相同的區段
   * 這用於從安全頁面(https://)傳送資料

* **訪客命名空間**

   * 命名空間會決定追蹤URL的第一部分。
   * 例如，將namespace變更為&#x200B;**CNAME**&#x200B;會導致對Adobe Analytics的呼叫看起來像&#x200B;**CNAME.d1.omtrdc.net**，而非預設值。

## 將頁面與Adobe Analytics Framework {#associating-a-page-with-a-adobe-analytics-framework}關聯

當頁面與Adobe Analytics架構相關聯時，頁面會在頁面載入時傳送資料至Adobe Analytics。 頁面填入的變數會從架構中的Adobe Analytics變數進行映射和擷取。 例如，頁面檢視是從Adobe Analytics擷取的。

頁面的後代繼承與框架的關聯。 例如，當您將網站的根頁面與架構建立關聯時，網站的所有頁面都會與架構建立關聯。

1. 從&#x200B;**Sites**&#x200B;主控台中，選擇您要設定追蹤的頁面。
1. 直接從控制台或頁面編輯器開啟&#x200B;**[頁面屬性](/help/sites-authoring/editing-page-properties.md)**。
1. 開啟**雲端服務**標籤。

1. 使用&#x200B;**新增設定**&#x200B;下拉式清單，從可用選項中選取&#x200B;**Adobe Analytics**。 如果放置了繼承，則需要在選擇器可用之前禁用該繼承。

1. **Adobe Analytics**&#x200B;的下拉式選取器將附加至可用的選項。 使用此選項可選擇所需的框架配置。

1. 選擇&#x200B;**保存並關閉**。
1. **[發](/help/sites-authoring/publishing-pages.md)** 布頁面以啟動頁面和任何連接的設定／檔案。
1. 最後一個步驟是造訪發佈例項上的頁面，並使用&#x200B;**Search**&#x200B;元件搜尋關鍵字（例如茄子）。
1. 然後，您可以使用適當的工具檢查對Adobe Analytics的呼叫；例如，[Adobe Experience Cloud除錯程式](https://docs.adobe.com/content/help/en/debugger/using/experience-cloud-debugger.html)。
1. 在提供的範例中，呼叫應包含eVar7中輸入的值（即茄子），而事件清單應包含event3。

### 頁面檢視 {#page-views}

當頁面與Adobe Analytics架構關聯時，頁面檢視次數可顯示在網站主控台的「清單」檢視中。

如需詳細資訊，請參閱[查看頁面分析資料](/help/sites-authoring/page-analytics-using.md)。

### 配置導入間隔{#configuring-the-import-interval}

設定&#x200B;**Adobe AEM Managed Polling Configuration**&#x200B;服務的適當例項：

* **輪詢間隔**:服務從Adobe Analytics擷取頁面檢視資料的間隔（以秒為單位）。預設間隔為43200000毫秒（12小時）。

* **啟用**:啟用或禁用服務。預設情況下，服務處於啟用狀態。

要配置此OSGi服務，可以使用儲存庫](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)中的[Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)或[osgiConfig節點（服務PID為`com.day.cq.polling.importer.impl.ManagedPollConfigImpl`）。

## 編輯Adobe Analytics設定和／或架構{#editing-adobe-analytics-configurations-and-or-frameworks}

如同建立Adobe Analytics設定或架構時，導覽至（舊版）**雲端服務**&#x200B;畫面。 選擇&#x200B;**顯示配置** ，然後按一下指向要更新的特定配置的連結。

編輯Adobe Analytics配置時，您也需要在配置頁面本身按&#x200B;**編輯**&#x200B;按鈕，以開啟&#x200B;**編輯元件**&#x200B;對話方塊。

## 刪除Adobe Analytics Frameworks {#deleting-adobe-analytics-frameworks}

若要刪除Adobe Analytics架構，請先開啟[以進行編輯。](#editing-adobe-analytics-configurations-and-or-frameworks)

然後，從側腳的&#x200B;**Page**&#x200B;標籤中選擇&#x200B;**刪除框架**。

