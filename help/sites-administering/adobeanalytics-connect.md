---
title: 連接到Adobe Analytics並建立框架
seo-title: Connecting to Adobe Analytics and Creating Frameworks
description: 瞭解如何連AEM接到SiteCatalyst和建立框架。
seo-description: Learn about connecting AEM to SiteCatalyst and creating frameworks.
uuid: 3820dd24-4193-42ea-aef2-4669ebfeaa9d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6b545a51-3677-4ea1-ac7e-2d01ba19283e
docset: aem65
exl-id: 8262bbf9-a982-479b-a2b5-f8782dd4182d
source-git-commit: 71842228dd3cb1ce3b79728912e8333d25fccefc
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 6%

---

# 連接到Adobe Analytics並建立框架 {#connecting-to-adobe-analytics-and-creating-frameworks}

要跟蹤您在Adobe Analytics的頁AEM面中的Web資料，請建立Adobe Analytics Cloud服務配置和Adobe Analytics框架：

* **Adobe Analytics配置：** 關於你的Adobe Analytics帳戶的資訊。 Adobe Analytics配置AEM可連接到Adobe Analytics。 為您使用的每個帳戶建立Adobe Analytics配置。
* **Adobe Analytics框架：** Adobe Analytics報告套件屬性和CQ變數之間的一組映射。 使用框架配置網站資料如何填充Adobe Analytics報告。 框架與Adobe Analytics配置相關。 可為每個配置建立多個框架。

將網頁與框架關聯時，框架將對該頁和該頁的子體執行跟蹤。 然後，可以從Adobe Analytics檢索頁面視圖並在站點控制台中顯示。

## 必備條件 {#prerequisites}

### Adobe Analytics帳戶 {#adobe-analytics-account}

要跟蹤AEMAdobe Analytics的資料，您必須擁有有效的Adobe Experience CloudAdobe Analytics帳戶。

Adobe Analytics帳戶必須：

* 有 **管理員** 權限
* 已分配給 **Web服務訪問** 用戶組。

>[!CAUTION]
>
>提供 **管理員** 權限(在Adobe Analytics內)不足以允許用戶從Adobe AnalyticsAEM連接。 帳戶還必須 **Web服務訪問** 權限。

![chlimage_1-67](assets/chlimage_1-67.png)

在繼續之前，請確保您的憑據允許您登錄Adobe Analytics。 通過以下任一方式：

* [Adobe Experience Cloud登錄](https://experience.adobe.com/#/@login/home)

* [Adobe Analytics登錄](https://sc.omniture.com/login/)

### 配置AEM以使用Adobe Analytics資料中心 {#configuring-aem-to-use-your-adobe-analytics-data-centers}

Adobe Analytics [資料中心](https://experienceleague.adobe.com/docs/analytics/analyze/reports-analytics/reporting-interface/overview-data-collection.html?lang=en) 收集、處理和儲存與您的Adobe Analytics報告套件關聯的資料。 配置AEM為使用承載Adobe Analytics報告套件的資料中心。 您的合同中提到了資料中心。 請與組織中的管理員聯繫以獲取此資訊。

如有必要，請使用以下內容路由到正確的資料中心： `https://api.omniture.com/`。

如果您的組織需要從特定資料中心收集或檢索資料，請使用以下方法：

| 資料中心 | URL |
|---|---|
| 倫敦 | `https://api3.omniture.com/` |
| 新加坡 | `https://api4.omniture.com/` |
| 俄勒岡 | `https://api5.omniture.com/` |

使用 [配置OSGi捆綁包的Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) **AdobeAEM分析HTTP客戶端**。 添加 **資料中心URL** 用於承載報表套件的資料中心，您的頁面AEM為其收集資料。

![aa-07](assets/aa-07.png)

1. 在Web瀏覽器中開啟Web控制台。 ([https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. 要訪問控制台，請輸入您的憑據。

   >[!NOTE]
   >
   >要瞭解您是否有權訪問此控制台，請與站點管理員聯繫。

1. 選擇名為的配置項 **AdobeAEM分析HTTP客戶端**。
1. 要添加資料中心的URL，請按 **資料中心URL** ，然後在框中鍵入URL。

1. 要從清單中刪除URL，請按一下URL旁邊的 — 按鈕。
1. 按一下「儲存」。

## 配置到Adobe Analytics的連接 {#configuring-the-connection-to-adobe-analytics}

>[!CAUTION]
>
>由於 Adobe Analytics API 中的安全性變更，AEM 中包含的 Activity Map 版本已無法再使用。
>
>的 [由Adobe Analytics提供的ActivityMap插件](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html) 應該被使用。

## 為Activity Map配置 {#configuring-for-the-activity-map}

>[!CAUTION]
>
>由於 Adobe Analytics API 中的安全性變更，AEM 中包含的 Activity Map 版本已無法再使用。
>
>的 [由Adobe Analytics提供的ActivityMap插件](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html) 應該被使用。

## 建立Adobe Analytics框架 {#creating-a-adobe-analytics-framework}

對於您正在使用的報表套件ID(RSID)，您可以控制哪些伺服器實例（作者、發佈或兩者）將資料提供給報表套件：

* **全部**:來自作者和發佈實例的資訊將填充報表套件。
* **作者**:僅作者實例中的資訊將填充報告套件。
* **發佈**:僅發佈實例中的資訊將填充報表套件。

>[!NOTE]
>
>選擇伺服器實例的類型不會限制對Adobe Analytics的調用，它只會控制包括RSID的調用。
>
>例如，框架配置為使用 *零售* report suite和author是選定的伺服器實例。 當頁面與框架一起發佈時，仍會向Adobe Analytics發出調用，但這些調用不包含RSID。 僅來自作者實例的調用包括RSID。

1. 使用 **導航**&#x200B;選中 **工具**。 **Cloud Services**，則 **舊Cloud Services**。
1. 滾動到 **Adobe Analytics** 選擇 **顯示配置**。
1. 按一下 **[+]** 連結到您的Adobe Analytics配置。

1. 在 **建立框架** 對話框：

   * 指定 **標題**。
   * （可選）您可以指定 **名稱**，用於將框架詳細資訊儲存在儲存庫中的節點。
   * 選擇 **Adobe Analytics框架**

   然後按一下 **建立**。

   該框架將開啟以進行編輯。

1. 在 **報表套件** 按一下 **添加項**。 然後使用下拉框選擇「報表套件ID」(例如， `geometrixxauth`)。

   >[!NOTE]
   >
   >選擇報告套件ID時，左側的內容查找器將填充Adobe Analytics變數(SiteCatalyst變數)。

1. 要選擇要向報告套件發送資訊的伺服器實例，請使用 **運行模式** 下拉清單（在「報告套件ID」旁邊）。

   ![aa框架–01](assets/aa-framework-01.png)

1. 要使框架在網站的發佈實例上可用，請在 **頁面** 按一下 **激活框架。**

### 為Adobe Analytics配置伺服器設定 {#configuring-server-settings-for-adobe-analytics}

框架系統允許您更改每個Adobe Analytics框架中的伺服器設定。

>[!CAUTION]
>
>這些設定決定了資料的發送位置和發送方式，因此您必須 *不篡改這些設定* 讓你的Adobe Analytics代表來。

首先開啟面板。 按旁邊的向下箭頭 **伺服器**:

![server_001](assets/server_001.png)

* **追蹤伺服器**

   * 包含用於發送Adobe Analytics呼叫的URL

      * `cname`  — 預設至Adobe Analytics帳戶 *公司名稱*
      * `d1`  — 對應於資訊發送到的資料中心( `d1`。 `d2`或 `d3`)
      * `sc.omtrdc.net`  — 域名

* **安全追蹤伺服器**

   * 與跟蹤伺服器具有相同的段
   * 用於從安全頁發送資料(`https://`)

* **訪客命名空間**

   * 命名空間確定跟蹤URL的第一部分。
   * 例如，將命名空間更改為 **名稱** 使給Adobe Analytics的電話看起來 **CNAME.d1.omtrdc.net** 而不是預設值。

## 將頁面與Adobe Analytics框架關聯 {#associating-a-page-with-a-adobe-analytics-framework}

當頁面與Adobe Analytics框架關聯時，頁面載入時會將資料發送到Adobe Analytics。 該頁填充的變數將從框架中的Adobe Analytics變數映射和檢索。 例如，從Adobe Analytics檢索頁面視圖。

頁面的後代繼承與框架的關聯。 例如，將站點的根頁與框架關聯時，站點的所有頁都與框架關聯。

1. 從 **站點** 控制台，選擇要設定的跟蹤頁面。
1. 開啟 **[頁面屬性](/help/sites-authoring/editing-page-properties.md)**，可直接從控制台或頁面編輯器進行。
1. 開啟**Cloud Services**頁籤。

1. 使用 **添加配置** 下拉選擇 **Adobe Analytics** 的子菜單。 如果置於繼承位置，請在選擇器可用之前禁用該繼承。

1. 的下拉選擇器 **Adobe Analytics** 的子菜單。 選擇所需的框架配置。

1. 選擇 **保存並關閉**。
1. 要激活頁面和所有連接的配置/檔案， **[發佈](/help/sites-authoring/publishing-pages.md)** 頁。
1. 最後一步是訪問發佈實例上的頁面，並使用 **搜索** 元件。
1. 然後，你可以使用適當的工具檢查對Adobe Analytics的呼叫；比如說， [Adobe Experience Cloud調試器](https://experienceleague.adobe.com/docs/experience-platform/debugger/home.html)。
1. 使用提供的示例，調用應包含在eVar7中輸入的值（即，茄子），事件清單應包含event3。

### 頁面檢視 {#page-views}

當頁面與Adobe Analytics框架關聯時，頁面視圖的數量可以顯示在站點控制台的「清單」視圖中。

請參閱 [查看頁面分析資料](/help/sites-authoring/page-analytics-using.md) 的上界。

### 配置導入間隔 {#configuring-the-import-interval}

配置相應的實例 **AdobeAEM托管輪詢配置** 服務：

* **輪詢間隔**:服務從Adobe Analytics檢索頁面視圖資料的間隔（秒）。
預設間隔為43200000毫秒（12小時）。

* **啟用**:啟用或禁用服務。 預設情況下，服務處於啟用狀態。

要配置此OSGi服務，您可以使用 [Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 或 [儲存庫中的osgiConfig節點](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) (服務PID為 `com.day.cq.polling.importer.impl.ManagedPollConfigImpl`)。

## 編輯Adobe Analytics配置和/或框架 {#editing-adobe-analytics-configurations-and-or-frameworks}

與建立Adobe Analytics配置或框架時一樣，導航到（舊） **Cloud Services** 的上界。 選擇 **顯示配置**，然後按一下指向要更新的特定配置的連結。

編輯Adobe Analytics配置時，按 **編輯** 當在配置頁面上開啟 **編輯元件** 對話框。

## 刪除Adobe Analytics框架 {#deleting-adobe-analytics-frameworks}

要刪除Adobe Analytics框架，請首先 [開啟它進行編輯](#editing-adobe-analytics-configurations-and-or-frameworks)。

然後選擇 **刪除框架** 從 **頁面** 擊中了。
