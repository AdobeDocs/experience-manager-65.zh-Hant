---
title: 使用行銷活動管理員
seo-title: 使用行銷活動管理員
description: 行銷促銷活動管理員(MCM)是可協助您管理多管道促銷活動的主控台。 使用此行銷自動化軟體，您可以管理所有品牌、宣傳和體驗，以及相關的細分、清單、潛在客戶和報表。
seo-description: 行銷促銷活動管理員(MCM)是可協助您管理多管道促銷活動的主控台。 使用此行銷自動化軟體，您可以管理所有品牌、宣傳和體驗，以及相關的細分、清單、潛在客戶和報表。
uuid: 63b817e4-34b9-42b8-845b-e0b7d9af3a96
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 11ff8bb3-39eb-4f77-b3dc-720262fa7f3f
docset: aem65
translation-type: tm+mt
source-git-commit: dc1985c25c797f7b994f30195d0586f867f9b3ee
workflow-type: tm+mt
source-wordcount: '1218'
ht-degree: 0%

---


# 使用行銷促銷活動管理員{#working-with-the-marketing-campaign-manager}

在AEM中，Marketing Campaign Manager(MCM)是可協助您管理多管道促銷活動的主控台。 使用此行銷自動化軟體，您可以管理所有品牌、宣傳和體驗，以及相關的細分、清單、潛在客戶和報表。

MCM可從AEM的不同位置存取；例如，「歡迎」畫面，使用「促銷活動」圖示或搭配URL:

`https://<hostname>:<port>/libs/mcm/content/admin.html`

例如：

`https://localhost:4502/libs/mcm/content/admin.html`

![screen_shot_2012-02-21at114636am](assets/screen_shot_2012-02-21at114636am.png)

從MCM中，您可以訪問：

* **[儀](#dashboard)**
表板這分為四個窗格：

   * [列](#lists)
表此窗格顯示您已建立的清單，以及該清單中的銷售線索數。在此窗格中，您可以直接建立新清單，或匯入銷售機會以建立新清單。
選擇特定清單後，您將進入[Lists](#lists)區段，其中顯示清單的詳細資訊。

   * [區](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#anoverviewofsegmentation)
段此窗格顯示您已定義的區段。區段可讓您描述共用特定特徵的訪客集合。
選取特定區段會開啟區段定義頁面。

   * [ReportsAEM提](/help/sites-administering/reporting.md)
供不同的報表，可協助您分析和監控執行個體的狀態。此MCM窗格列出報告。
選取報表會開啟報表頁面。

   * [促銷](#campaigns)
活動此窗格會列出您的促銷活動體驗， [](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#newsletters) 例如電 [子報和茶報](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#teasers)。

* **[銷](#leads)**
售機會您可以在這裡管理銷售機會。您可以建立或匯入銷售線索、編輯個別銷售線索的特定詳細資料，或在不再需要時刪除。 您也可以將銷售機會放入不同的群組，稱為清單。 **注意：** Adobe不打算進一步增強這項功能。建議使用[運用Adobe Campaign和AEM](/help/sites-administering/campaign.md)的整合。

* **[清](#lists)**
單您可以在這裡管理您的銷售機會清單。**注意：** Adobe不打算進一步增強這項功能。建議使用[運用Adobe Campaign和AEM](/help/sites-administering/campaign.md)的整合。

* **[促銷](#campaigns)**
活動您可以在這裡管理品牌、促銷活動和體驗。

## 控制面板 {#dashboard}

控制面板顯示四個窗格，提供您清單（銷售機會）、區段、報表和促銷活動的概觀。 您也可從這裡存取這些功能的基本功能。

![mcm_dashboard](assets/mcm_dashboard.png)

### 銷售機會 {#leads}

>[!NOTE]
>
>Adobe不打算進一步增強這項功能（管理銷售機會）。
>建議您使用[Adobe Campaign和AEM](/help/sites-administering/campaign.md)的整合。

在AEM MCM中，您可以手動輸入銷售線索或匯入逗號分隔清單，以組織和新增銷售線索；例如，郵件清單。 產生銷售機會的其他方式包括電子報註冊或社群註冊（如果設定，這些方式可觸發填入銷售機會的工作流程）。 銷售線索通常被分類並放入一個清單中，以便您以後能夠對整個清單執行操作；例如，將自訂電子郵件傳出至特定清單。

在左窗格的&#x200B;**Leads**&#x200B;下，您可以建立、匯入、編輯和刪除您的銷售機會，然後視需要啟用或停用。 您可以新增銷售線索至清單，或查看其已屬於哪些清單。

>[!NOTE]
>
>有關特定任務的詳細資訊，請參閱[使用Lead](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#workingwithleads)。

![screen_shot_2012-02-21at114748am-1](assets/screen_shot_2012-02-21at114748am-1.png)

### 清單 {#lists}

>[!NOTE]
>
>Adobe不打算進一步增強這項功能（管理清單）。
>建議您使用[Adobe Campaign和AEM](/help/sites-administering/campaign.md)的整合。

清單可讓您將潛在客戶組織成群組。 有了清單，您可以將行銷活動鎖定在特定人群；例如，您可以將定位的電子報傳送至清單。

在&#x200B;**Lists**&#x200B;下，您可以建立、匯入、編輯、合併和刪除清單，然後視需要啟用或停用清單，以管理清單。 您也可以查看該清單中的銷售線索、查看該清單是否是其他清單的成員或查看說明。

>[!NOTE]
>
>有關特定任務的詳細資訊，請參閱[使用清單](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#workingwithlists)。

![screen_shot_2012-02-21at124828pm-1](assets/screen_shot_2012-02-21at124828pm-1.png)

### 促銷活動 {#campaigns}

>[!NOTE]
>
>如需特定工作的詳細資訊，請參閱[預告與策略](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#workingwithlists)、[設定促銷活動](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#settingupyourcampaign)和[電子報](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#newsletters)。

若要存取現有的促銷活動，請在MCM中按一下&#x200B;**Campaigns**。

![screen_shot_2012-02-21at1106pm](assets/screen_shot_2012-02-21at11106pm.png)

* **在左窗格中**:有所有品牌和宣傳的清單。只要按一下品牌，兩者皆可：

   * 展開清單，在左窗格中顯示所有相關的促銷活動；此清單也顯示每個促銷活動的體驗數。
   * 在右窗格中開啟品牌概觀。

* **在右窗格中**:會針對每個品牌顯示圖示（不會顯示歷史促銷活動）。您可以按兩下這些項目，以開啟品牌概觀。

#### 品牌概觀{#brand-overview}

![mcm_brandoverview](assets/mcm_brandoverview.png)

從這裡，您可以：

* 查看此品牌存在的促銷活動和體驗數量（顯示在左窗格中的數量）。
* 建立&#x200B;**新……**&#x200B;促銷活動。

* 變更檢視的時間範圍；選擇&#x200B;**Week**、**Month**&#x200B;或&#x200B;**Quarter**，使用箭頭選擇特定期間或返回&#x200B;**Today**。

* 選擇促銷活動（在右窗格中）以：

   * 編輯&#x200B;**屬性……**
   * **刪** 除促銷活動。

* 開啟促銷活動概述（按兩下右窗格中的促銷活動，或在左窗格中按一下）。

#### 促銷活動概述{#campaign-overview}

對於個別促銷活動，有兩種檢視可供使用：

1. **日曆檢視**

   使用圖示：

   ![](do-not-localize/mcm_iconcalendarview.png)

   這會顯示所有觸點（灰色）的清單，以及與該觸點連接的體驗（綠色）的水準時間範圍：

   ![mcm_banner_calendarview](assets/mcm_banner_calendarview.png)

   從這裡，您可以：

   * 使用箭頭更改您正在查看的時間範圍，或返回&#x200B;**Today**。

   * 使用&#x200B;**新增接觸點……**&#x200B;以新增現有體驗的觸點。

   * 按一下摘要（在右窗格中）以設定&#x200B;**開機**&#x200B;和&#x200B;**關機**。

1. **清單檢視**

   使用圖示：

   ![](do-not-localize/mcm_icon_listview.png)

   這會列出所選促銷活動的所有體驗（例如茶具和電子報）:

   ![mcm_banner_listview](assets/mcm_banner_listview.png)

   從這裡，您可以：

   * 建立&#x200B;**新……**&#x200B;體驗；例如，Adobe Target優惠、廣告和電子報。
   * **編** 輯特定摘要頁面或電子報的詳細資訊（也可使用按兩下功能）。
   * 定義&#x200B;**屬性……**，以取得特定摘要頁面或電子報。
   * **模** 擬體驗的外觀和感覺（摘要頁面或電子報）。當模擬頁面開啟時，您可以開啟sidekick，以切換至該頁面的編輯模式。

   * **分析……** 為頁面產生的印象。

   * **刪除** 不再需要的項目。
   * **搜** 尋您的文字（將搜尋體驗的「標題」欄位）。
   * 使用&#x200B;**Advanced**&#x200B;搜尋，將篩選套用至搜尋。

### 模擬促銷活動體驗{#simulating-your-campaign-experiences}

在MCM中，按一下&#x200B;**Campaigns**。 確定清單檢視處於作用中，然後選取所需的促銷活動體驗，然後按一下「模擬」。 ****&#x200B;觸點（摘要或電子報頁面）將會開啟，以顯示您所選取的體驗——如訪客所見。

![mcm_simulateexperience](assets/mcm_simulateexperience.png)

您也可以從這裡開啟側鍵（按一下小向下箭頭），以變更為編輯模式以更新頁面。

### 分析促銷活動體驗{#analyzing-your-campaign-experiences}

在MCM中，按一下&#x200B;**Campaigns**。 確定清單檢視處於作用中，然後選取所需的促銷活動體驗，並選取「分析……」**。**&#x200B;將會顯示隨時間變化的頁面印象圖表。

![mcm_campaignanyle](assets/mcm_campaignanalyze.png)
