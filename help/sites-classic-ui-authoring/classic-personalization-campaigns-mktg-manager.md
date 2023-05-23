---
title: 使用市場營銷活動經理
seo-title: Working with the Marketing Campaign Manager
description: 市場營銷活動經理(MCM)是一個控制台，可幫助您管理多渠道市場活動。 使用此營銷自動化軟體，您可以管理所有品牌、市場活動和體驗，以及相關的細分、清單、銷售線索和報告。
seo-description: The Marketing Campaign Manager (MCM) is a console that helps you manage multi-channel campaigns. With this marketing automation software you can manage all your brands, campaigns and experiences together with the related segments, lists, leads, and reports.
uuid: 63b817e4-34b9-42b8-845b-e0b7d9af3a96
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 11ff8bb3-39eb-4f77-b3dc-720262fa7f3f
docset: aem65
exl-id: 0e13112b-d9df-4ba6-bd73-431c87890b79
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 0%

---

# 使用市場營銷活動經理{#working-with-the-marketing-campaign-manager}

在中AEM,Marketing Campaign Manager(MCM)是一個控制台，可幫助您管理多渠道市場活動。 使用此營銷自動化軟體，您可以管理所有品牌、市場活動和體驗，以及相關的細分、清單、銷售線索和報告。

MCM可從中國各地訪問AEM;例如，「歡迎」螢幕，使用「市場活動」表徵圖或URL:

`https://<hostname>:<port>/libs/mcm/content/admin.html`

例如：

`https://localhost:4502/libs/mcm/content/admin.html`

![screen_shot_2012-02-21at114636am](assets/screen_shot_2012-02-21at114636am.png)

從MCM可以訪問：

* **[儀表板](#dashboard)**
這分為四個窗格：

   * [清單](#lists)
此窗格顯示您已建立的清單以及該清單中的銷售線索數。 在此窗格中，您可以直接建立新清單或導入銷售線索以建立新清單。
選擇特定清單將帶您 [清單](#lists) 清單的詳細資訊。

   * [段](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#anoverviewofsegmentation)
此窗格顯示已定義的段。 通過網段，可以描述一組具有某些特性的訪問者。
選擇特定段將開啟段定義頁。

   * [報告](/help/sites-administering/reporting.md)
提AEM供不同的報告，以幫助您分析和監視實例的狀態。 此MCM窗格列出報告。
選擇報告將開啟報告頁。

   * [市場活動](#campaigns)
此窗格列出您的市場活動體驗，如 [通訊](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#newsletters) 和 [沖茶器](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#teasers)。

* **[銷售線索](#leads)**
在這裡，你可以管理你的線索。 您可以建立或導入銷售線索、編輯單個銷售線索的特定詳細資訊或在不再需要時刪除。 您還可以將銷售線索放入不同的組，稱為清單。 **注：** Adobe並沒有計畫進一步增強這一能力。
建議是 [利用Adobe Campaign和AEM](/help/sites-administering/campaign.md)。

* **[清單](#lists)**
在這裡，您可以管理您的銷售線索清單。**注：** Adobe並沒有計畫進一步增強這一能力。
建議是 [利用Adobe Campaign和AEM](/help/sites-administering/campaign.md)。

* **[市場活動](#campaigns)**
在這裡，您可以管理您的品牌、活動和體驗。

## 控制面板 {#dashboard}

控制面板顯示四個窗格，這些窗格提供了清單（銷售線索）、段、報表和市場活動的概覽。 此處還提供對這些基本功能的訪問。

![mcm_dashboard](assets/mcm_dashboard.png)

### 銷售機會 {#leads}

>[!NOTE]
>
>Adobe不打算進一步增強此功能（管理銷售線索）。
>建議是利用 [Adobe Campaign和AEM](/help/sites-administering/campaign.md)。

在AEMMCM中，您可以通過手動輸入線索或導入逗號分隔的清單來組織和添加線索；例如，郵件清單。 生成潛在顧客的其他方法包括通過新聞簡報註冊或社區註冊（如果配置，這些方法可觸發填充潛在顧客的工作流）。 銷售線索通常被分類並放入一個清單中，以便以後您可以對整個清單執行操作；例如，向特定清單發送自定義電子郵件。

下 **銷售線索** 在左窗格中，您可以建立、導入、編輯和刪除銷售線索，然後根據需要激活或停用。 您可以向清單添加潛在顧客，或查看其已屬於哪些清單。

>[!NOTE]
>
>請參閱 [使用Lead](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#workingwithleads) 的子菜單。

![screen_shot_2012-02-21at114748am-1](assets/screen_shot_2012-02-21at114748am-1.png)

### 清單 {#lists}

>[!NOTE]
>
>Adobe不打算進一步增強此功能（管理清單）。
>建議是利用 [Adobe Campaign和AEM](/help/sites-administering/campaign.md)。

清單允許您將銷售線索組織成組。 使用清單，您可以將市場營銷活動目標定為一組選定的人員；例如，您可以將目標新聞簡報發送到清單。

下 **清單**，您可以通過建立、導入、編輯、合併和刪除清單來管理清單，然後可以根據需要激活或停用這些清單。 您還可以查看該清單中的銷售線索，查看清單是否是其他清單的成員，或查看說明。

>[!NOTE]
>
>請參閱 [使用清單](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#workingwithlists) 的子菜單。

![screen_shot_2012-02-21at124828pm-1](assets/screen_shot_2012-02-21at124828pm-1.png)

### 行銷活動 {#campaigns}

>[!NOTE]
>
>請參閱 [預告和策略](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#workingwithlists)。 [設定市場活動](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#settingupyourcampaign) 和 [通訊](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#newsletters) 的子菜單。

要訪問現有市場活動，請在MCM中按一下 **市場活動**。

![screen_shot_2012-02-21at1106pm](assets/screen_shot_2012-02-21at11106pm.png)

* **在左窗格中**:這裡有一張所有品牌和活動的清單。
按一下一個品牌將同時實現：

   * 展開清單，在左窗格中顯示所有相關市場活動；此清單還顯示每個市場活動存在的體驗數。
   * 在右窗格中開啟品牌概述。

* **在右窗格中**:每個品牌都顯示表徵圖（不顯示歷史市場活動）。
您可以按兩下這些選項以開啟品牌概述。

#### 品牌概述 {#brand-overview}

![mcm_brandoverview](assets/mcm_brandoverview.png)

在此，您可以：

* 請參閱此品牌存在的市場活動和體驗數（左窗格中顯示的數字）。
* 建立 **新建……** 為這個品牌進行宣傳。

* 更改正在查看的時間範圍；選擇 **周**。 **月** 或 **季度**，使用箭頭選擇特定期間或返回 **今天**。

* 選擇市場活動（在右窗格中）:

   * 編輯 **屬性……**
   * **刪除** 競選。

* 開啟市場活動概覽（在右窗格中按兩下市場活動，或在左窗格中按一下）。

#### 市場活動概覽 {#campaign-overview}

對於單個市場活動，有兩種視圖：

1. **日曆檢視**

   使用表徵圖：

   ![](do-not-localize/mcm_iconcalendarview.png)

   此列出所有觸點（灰色）的清單，其中包含與該觸點連接的體驗（綠色）的水準時間範圍：

   ![mcm_banner_calendarview](assets/mcm_banner_calendarview.png)

   在此，您可以：

   * 使用箭頭更改您正在查看的時間範圍，或返回到 **今天**。

   * 使用 **添加觸點……** 為現有體驗添加新的觸點。

   * 按一下預告（在右窗格中）以設定 **準時** 和 **關機時間**。

1. **清單檢視**

   使用表徵圖：

   ![](do-not-localize/mcm_icon_listview.png)

   這列出了所選市場活動的所有體驗（如茶具和新聞稿）:

   ![mcm_banner_listview](assets/mcm_banner_listview.png)

   在此，您可以：

   * 建立 **新建……** 經驗；例如，Adobe Target提供、茶具和通訊。
   * **編輯** 特定預告頁面或新聞稿的詳細資訊（還可使用按兩下）。
   * 定義 **屬性……** 特定預告頁或新聞簡報。
   * **模擬** 體驗的外觀和感覺（預告頁或新聞稿）。
開啟模擬頁面後，可以開啟邊框以切換到該頁面的編輯模式。

   * **分析……** 為頁面生成的印象。

   * **刪除** 不再需要的項目。
   * **搜索** （將搜索體驗的標題欄位）。
   * 使用 **高級** 搜索以將篩選器應用於搜索。

### 模擬您的活動體驗 {#simulating-your-campaign-experiences}

在MCM中，按一下 **市場活動**。 確保清單視圖處於活動狀態，然後選擇所需的市場活動體驗，然後按一下 **模擬**。 觸點（預告或新聞簡報頁面）將開啟，以顯示您選擇的體驗 — 訪問者將看到它。

![mcm_simulater經驗](assets/mcm_simulateexperience.png)

在此處，您還可以開啟旁鍵（按一下小向下箭頭）以更改為編輯模式以更新頁面。

### 分析您的活動體驗 {#analyzing-your-campaign-experiences}

在MCM中，按一下 **市場活動**。 確保清單視圖處於活動狀態，然後選擇所需的市場活動體驗並選擇 **分析……**。 將顯示一段時間的頁面印象圖。

![mcm_campaignany分析](assets/mcm_campaignanalyze.png)
