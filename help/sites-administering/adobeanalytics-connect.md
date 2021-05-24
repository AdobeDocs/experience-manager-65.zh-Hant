---
title: 連接Adobe Analytics和建立框架
seo-title: 連接Adobe Analytics和建立框架
description: 了解如何將AEM連線至SiteCatalyst及建立架構。
seo-description: 了解如何將AEM連線至SiteCatalyst及建立架構。
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
source-wordcount: '1550'
ht-degree: 8%

---

# 連接Adobe Analytics和建立框架{#connecting-to-adobe-analytics-and-creating-frameworks}

若要在Adobe Analytics中追蹤AEM頁面的網頁資料，請建立Adobe Analytics Cloud服務設定和Adobe Analytics架構：

* **Adobe Analytics設定：** 您Adobe Analytics帳戶的相關資訊。Adobe Analytics設定可讓AEM連線至Adobe Analytics。 為您使用的每個帳戶建立Adobe Analytics設定。
* **Adobe Analytics架構：** Adobe Analytics報表套裝屬性和CQ變數之間的一組對應。使用架構來設定網站資料如何填入Adobe Analytics報表。 架構與Adobe Analytics設定相關聯。 您可以為每個設定建立多個架構。

將網頁與框架關聯時，框架將執行該頁和該頁的子體的跟蹤。 然後可從Adobe Analytics擷取頁面檢視，並顯示在Sites主控台中。

## 必備條件 {#prerequisites}

### Adobe Analytics帳戶{#adobe-analytics-account}

若要在Adobe Analytics中追蹤AEM資料，您必須具備有效的Adobe Marketing Cloud Adobe Analytics帳戶。

Adobe Analytics帳戶需要：

* 具有&#x200B;**管理員**&#x200B;權限
* 分配給&#x200B;**Web服務訪問**&#x200B;用戶組。

>[!CAUTION]
>
>提供&#x200B;**管理員**&#x200B;權限(在Adobe Analytics內)不足以允許使用者從AEM連線至Adobe Analytics。 帳戶也必須具有&#x200B;**網站服務存取**&#x200B;權限。

![chlimage_1-67](assets/chlimage_1-67.png)

繼續之前，請確定您的認證可讓您登入Adobe Analytics。 透過下列其中一種方式：

* [Adobe Experience Cloud登入](https://login.experiencecloud.adobe.com/exc-content/login.html)

* [Adobe Analytics登入](https://sc.omniture.com/login/)

### 設定AEM以使用您的Adobe Analytics資料中心{#configuring-aem-to-use-your-adobe-analytics-data-centers}

Adobe Analytics [資料中心](https://developer.omniture.com/en_US/content_page/concepts-terminology/c-how-is-data-stored)收集、處理和儲存與您的Adobe Analytics報表套裝相關聯的資料。 您必須將AEM設定為使用托管Adobe Analytics報表套裝的資料中心。 下表列出可用的資料中心及其URL。

| 資料中心 | URL |
|---|---|
| 聖荷西 | https://api.omniture.com/admin/1.4/rest/ |
| 達拉斯 | https://api2.omniture.com/admin/1.4/rest/ |
| 倫敦 | https://api3.omniture.com/admin/1.4/rest/ |
| 新加坡 | https://api4.omniture.com/admin/1.4/rest/ |
| 俄勒岡 | https://api5.omniture.com/admin/1.4/rest/ |

AEM預設會使用聖荷西(https://api.omniture.com/admin/1.4/rest/)資料中心。

使用[Web主控台來設定OSGi套件組合](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) **AdobeAEM Analytics HTTP用戶端**。 為資料中心新增&#x200B;**資料中心URL**，該資料中心托管您的AEM頁面要為其收集資料的報表套裝。

![aa-07](assets/aa-07.png)

1. 在網頁瀏覽器中開啟Web主控台。 ([https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. 輸入您的憑證以存取主控台。

   >[!NOTE]
   >
   >請連絡您的網站管理員，了解您是否擁有此主控台的存取權。

1. 選取名為&#x200B;**AdobeAEM Analytics HTTP Client**&#x200B;的設定項目。
1. 若要新增資料中心的URL，請按&#x200B;**資料中心URL**&#x200B;清單旁的+按鈕，然後在方塊中輸入URL。

1. 若要從清單中移除URL，請按一下URL旁的 — 按鈕。
1. 按一下「儲存」。

## 設定與Adobe Analytics的連線{#configuring-the-connection-to-adobe-analytics}

>[!CAUTION]
>
>由於 Adobe Analytics API 中的安全性變更，AEM 中包含的 Activity Map 版本已無法再使用。
>
>現在應該使用Adobe Analytics](https://docs.adobe.com/content/help/zh-Hant/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html)提供的[ActivityMap外掛程式。

## 配置Activity Map{#configuring-for-the-activity-map}

>[!CAUTION]
>
>由於 Adobe Analytics API 中的安全性變更，AEM 中包含的 Activity Map 版本已無法再使用。
>
>現在應該使用Adobe Analytics](https://docs.adobe.com/content/help/en/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html)提供的[ActivityMap外掛程式。

## 建立Adobe Analytics框架{#creating-a-adobe-analytics-framework}

對於您使用的報表套裝ID(RSID)，您可以控制哪些伺服器例項（製作、發佈或兩者）會對報表套裝貢獻資料：

* **全部**:製作和發佈例項的資訊會填入報表套裝。
* **作者**:只有來自製作例項的資訊會填入報表套裝。
* **發佈**:只有來自發佈例項的資訊會填入報表套裝。

>[!NOTE]
>
>選取伺服器例項類型並不會限制對Adobe Analytics的呼叫，而只會控制哪些呼叫包含RSID。
>
>例如，框架已設定為使用&#x200B;*diweretail*&#x200B;報表套裝，而作者是選取的伺服器例項。 當頁面連同架構一起發佈時，仍會呼叫Adobe Analytics，但這些呼叫不包含RSID。 來自製作例項的呼叫僅包含RSID。

1. 使用&#x200B;**導航**，選擇&#x200B;**工具**、**Cloud Services**，然後選擇&#x200B;**舊式Cloud Services**。
1. 捲動至&#x200B;**Adobe Analytics**&#x200B;並選取&#x200B;**顯示設定**。
1. 按一下Adobe Analytics設定旁的&#x200B;**[+]**&#x200B;連結。

1. 在&#x200B;**建立框架**&#x200B;對話框中：

   * 指定&#x200B;**Title**。
   * 您可以選擇為儲存庫中框架詳細資訊的節點指定&#x200B;**名稱**。
   * 選擇&#x200B;**Adobe Analytics Framework**

   然後按一下&#x200B;**Create**。

   架構隨即開啟供編輯。

1. 在側面窗格的&#x200B;**報表套裝**&#x200B;區段中（主面板右側），按一下「新增項目&#x200B;**」。**&#x200B;然後使用下拉式清單來選取框架將與其互動的報表套裝ID（例如`geometrixxauth`）。

   >[!NOTE]
   >
   >選取報表套裝ID時，左側的內容尋找器會填入Adobe Analytics變數(SiteCatalyst變數)。

1. 然後，使用&#x200B;**執行模式**&#x200B;下拉式清單（位於報表套裝ID旁），選取您要傳送資訊至報表套裝的伺服器例項。

   ![aa-framework-01](assets/aa-framework-01.png)

1. 若要讓架構可在網站的發佈執行個體上使用，請在sidekick的&#x200B;**Page**&#x200B;標籤上，按一下&#x200B;**啟動架構。**

### 配置Adobe Analytics的伺服器設定{#configuring-server-settings-for-adobe-analytics}

架構系統可讓您變更每個Adobe Analytics架構內的伺服器設定。

>[!CAUTION]
>
>這些設定會決定您資料的傳送位置及傳送方式，因此您必須&#x200B;*不要篡改這些設定*，並讓您的Adobe Analytics代表改為設定。

首先，開啟面板。 按&#x200B;**Servers**&#x200B;旁邊的向下箭頭：

![server_001](assets/server_001.png)

* **追蹤伺服器**

   * 包含用於傳送Adobe Analytics呼叫的URL

      * cname — 預設為Adobe Analytics帳戶的&#x200B;*公司名稱*
      * d1 — 與資料中心相對應，資訊將傳送至（可為d1、d2或d3）
      * sc.omtrdc.net — 網域名稱

* **安全追蹤伺服器**

   * 與追蹤伺服器有相同的區段
   * 這可用來從安全頁面傳送資料(https://)

* **訪客命名空間**

   * 命名空間會決定追蹤URL的第一部分。
   * 例如，將命名空間變更為&#x200B;**CNAME**&#x200B;會導致對Adobe Analytics發出的呼叫看起來像&#x200B;**CNAME.d1.omtrdc.net**，而非預設值。

## 將頁面與Adobe Analytics架構{#associating-a-page-with-a-adobe-analytics-framework}關聯

將頁面與Adobe Analytics架構建立關聯時，頁面會在頁面載入時傳送資料至Adobe Analytics。 頁面填入的變數會在架構中對應，並從Adobe Analytics變數中擷取。 例如，頁面檢視是從Adobe Analytics擷取。

頁面的後代繼承與框架的關聯。 例如，當您將網站的根頁面與架構建立關聯時，網站的所有頁面都會與架構建立關聯。

1. 從&#x200B;**Sites**&#x200B;控制台中，選取您要設定追蹤的頁面。
1. 直接從主控台或頁面編輯器開啟&#x200B;**[頁面屬性](/help/sites-authoring/editing-page-properties.md)**。
1. 開啟**Cloud Services**標籤。

1. 使用&#x200B;**新增設定**&#x200B;下拉式清單，從可用選項中選取&#x200B;**Adobe Analytics**。 如果已放置繼承，則需要在選取器可用前停用該功能。

1. **Adobe Analytics**&#x200B;的下拉式選取器將附加至可用選項。 使用此選項可選擇所需的框架配置。

1. 選擇&#x200B;**保存並關閉**。
1. **[](/help/sites-authoring/publishing-pages.md)** 發佈頁面以啟動頁面及任何已連線的設定/檔案。
1. 最後一步是造訪發佈例項上的頁面，並使用&#x200B;**Search**&#x200B;元件搜尋關鍵字（例如茄子）。
1. 之後，您就可以使用適當的工具來檢查對Adobe Analytics進行的呼叫；例如， [Adobe Experience Cloud Debugger](https://docs.adobe.com/content/help/en/debugger/using/experience-cloud-debugger.html)。
1. 在提供的範例中，呼叫應包含eVar7中輸入的值（即茄子），而事件清單應包含event3。

### 頁面檢視 {#page-views}

將頁面與Adobe Analytics架構關聯時，頁面檢視的數量會顯示在Sites主控台的「清單」檢視中。

如需詳細資訊，請參閱[查看頁面分析資料](/help/sites-authoring/page-analytics-using.md) 。

### 配置導入間隔{#configuring-the-import-interval}

配置&#x200B;**AdobeAEM Managed Polling Configuration**&#x200B;服務的適當實例：

* **輪詢間隔**:服務從Adobe Analytics擷取頁面檢視資料的間隔（以秒為單位）。預設間隔為43200000毫秒（12小時）。

* **啟用**:啟用或停用服務。預設會啟用服務。

要配置此OSGi服務，可以使用儲存庫](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)中的[Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)或[osgiConfig節點（服務PID為`com.day.cq.polling.importer.impl.ManagedPollConfigImpl`）。

## 編輯Adobe Analytics設定和/或架構{#editing-adobe-analytics-configurations-and-or-frameworks}

如同建立Adobe Analytics設定或架構時，請導覽至（舊版）**Cloud Services**&#x200B;畫面。 選擇&#x200B;**顯示配置**，然後按一下指向要更新的特定配置的連結。

編輯Adobe Analytics設定時，您也需要在設定頁面本身上按&#x200B;**Edit**&#x200B;按鈕，才能開啟&#x200B;**Edit Component**&#x200B;對話方塊。

## 刪除Adobe Analytics架構{#deleting-adobe-analytics-frameworks}

若要刪除Adobe Analytics架構，請先開啟[以進行編輯](#editing-adobe-analytics-configurations-and-or-frameworks)。

然後，從sidekick的&#x200B;**Page**&#x200B;標籤中選擇&#x200B;**Delete Framework**。
