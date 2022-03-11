---
title: 管理活動
seo-title: Managing Activities
description: 活動控制台使您能夠建立、組織和管理品牌的營銷活動
seo-description: The Activities console enables you to create, organize, and manage the marketing activities of your brands
uuid: 0aebf88e-f298-410a-8c82-4076b671624f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: ef2321a3-cd51-4298-8782-e1a2ca721868
docset: aem65
exl-id: f510ca08-977d-45d5-86af-c4b7634b01ba
source-git-commit: 10e46fe60edcaa116978173b8c61542653f6a551
workflow-type: tm+mt
source-wordcount: '2001'
ht-degree: 13%

---

# 管理活動{#managing-activities}

活動控制台使您能夠建立、組織和管理營銷 [活動](/help/sites-authoring/personalization.md#activities) 品牌：

* 添加品牌。
* 對於每個品牌，添加和配置活動。
* 管理活動。

>[!NOTE]
>
>如果你把Adobe Target當作你的瞄準引擎，你也 [查看活動的效能資料](#viewing-performance-and-converting-winning-experiences-a-b-test)。 如果您使用A/B測試，則 [轉換贏家](#viewing-performance-and-converting-winning-experiences-a-b-test)。

在活動控制台上，活動按品牌組織。 您可以使用品牌和資料夾來構建活動的組織。 按一下/按一下可導航至「活動」控制台 **個性化** 並點擊/按一下 **活動**。

活動在「目標」模式下可用 [創作目標內容](/help/sites-authoring/content-targeting-touch.md)，也可以在其中建立活動。 在「目標」模式下建立的活動將顯示在「活動」控制台中。

活動顯示時帶有一個標籤，該標籤描述定義了哪種活動：

* XT -Adobe Target經驗瞄準
* A/B -Adobe TargetA/B測試
* AEM-Adobe Experience Manager目標（環境圖布或客戶環境驅動）

![chlimage_1-114](assets/chlimage_1-114.png)

>[!NOTE]
>
>可用的活動類型由以下各項決定：
>
>* 如果 **xt_only** 選項在Adobe Target租戶（客戶端代碼）上啟AEM用以連接到Adobe Target，然後 **僅** 中的XT活AEM動。
>
>* 如果 **xt_only** 選項 **不** 在Adobe Target租戶（客戶端代碼）上啟用，然後可以建立 **兩者** XT和A/B活AEM動
>
>**附加說明：** **xt_only** 選項是應用於特定目標租戶（客戶端代碼）的設定，只能在Adobe Target直接修改。 您無法在AEM中啟用或停用此選項。

>[!CAUTION]
>
>必須保護活動設定節點的安全 **cq：活動設定** 在發佈實例上，以便普通用戶無法訪問。 活動設定節點只能由處理與Adobe Target的活動同步的服務訪問。
>
>請參閱 [與Adobe Target整合的先決條件](/help/sites-administering/target-requirements.md#securingtheactivitysettings) 的上界。

## 使用活動控制台建立品牌 {#creating-a-brand-using-the-activities-console}

建立要管理其營銷活動的品牌。

使用「活動」控制台建立品牌時，該品牌也會出現在 [提供控制台](/help/sites-authoring/offerlib.md) 您可以建立活動體驗的優惠。

1. 在導航控制台中，按一下或點擊 **個性化**。 按一下或點擊 **活動**。

   ![screen_shot_2018-03-21at151821](assets/screen_shot_2018-03-21at151821.png)

1. 在活動控制台中，按一下或點擊 **建立**&#x200B;然後&#x200B;**建立品牌**。
1. 選擇品牌模板，然後按一下或點擊 **下一個**。
1. 在「活動」和「優惠」控制台中鍵入品牌的標題。 （可選）鍵入或選擇一個或多個要與品牌關聯的標籤。
1. 按一下或點擊 **建立**。 您的品牌將顯示在「活動」控制台中。

## 使用活動控制台添加/編輯活動 {#adding-editing-an-activity-using-the-activities-console}

添加活動或編輯現有活動，以將營銷工作重點放在特定受眾上。 建立/編輯活動時，可指定以下資訊：

* **** 名稱：活動的名稱。
* **** 定位引擎：AEM [](/help/sites-authoring/personalization.md#aem) 或 [Adobe Target](/help/sites-authoring/personalization.md#adobe-target) ，做為目標內容的引擎。

* **** 選擇目標配置： (僅限Adobe Target) 此活動應用來連線至Adobe Target的雲端設定。只有在為「定位引擎」選取Adobe Target時，才會顯示此選項。
* **活動類型：**活動類型 — A/BTest或經驗目標
* **** 目標：(可選) 活動的說明。
* **** 體驗：對象名稱與您所定位之行銷區段之間的對應。
* **** 流量百分比：如果選取A/B測試，您可以變更每個體驗的流量 (百分比)。
* **** 持續時間：套用活動的時段。
* **** 優先順序：活動的相對優先順序。當活動提供相同使用者區段的內容時，優先順序較高的活動優先。
* **** 目標量度：如果選取Adobe target作為定位引擎，您可以將成功度量新增至活動。需要一個成功度量。

>[!NOTE]
>
>新的Adobe target活動必須在目 ***標內容編輯器中建立*** ，而不是在 **Activity** Console中，因為與Adobe target的同步將會失敗。
>
>但是，您可以編輯控制台中的現有Adobe Target活動。

要添加活動，請執行以下操作：

1. 按一下或點選您要建立活動的品牌，然後按一下或點選「建立」 **** ，然 **後點選「建立活動」**。如果正在編輯，請選擇活動，然後按一下或點擊 **編輯**。
1. 提供以下資訊，然後按一下或點擊 **下一個**:

   * 活動的名稱。
   * 要使用的目標引擎。 預設AEM情況下選擇ContextHub()。 如果需要使用Adobe Target，請在目標內容編輯器中建立活動。
   * 如果選擇Adobe Target作為目標引擎，請選擇/編輯用於連接到Adobe Target的雲配置。 （請注意，不要選擇為雲配置建立的框架。）
   * （可選）活動的目標或說明。
   * 選擇活動類型。

1. 新增一或多個體驗至活動。按一下或點選「 **新增體驗」**。
1. 如果您使用目標AEM或Adobe Target經驗目標：

   1. 按一下或點擊**選擇受眾**，然後選擇您的體驗目標段。
   1. 按一下或點擊 **添加體驗**&#x200B;鍵入名稱，然後按一下或點擊 **確定**。

   1. 按一下或點擊 **下一個**。

   如果您使用Adobe TargetA/B測試：

   1. 按一下或點擊觀眾框中的鉛筆以選擇觀眾。
   1. 按一下或點擊 **添加體驗**&#x200B;鍵入名稱，然後按一下或點擊 **確定**。

   1. 輸入顯示每個體驗的通信量百分比。
   1. 按一下或點擊 **下一個**。


1. 要指定活動何時啟動，請使用 **開始** 下拉菜單，以選擇以下值之一：

   * **激活時：** 活動在包含目標內容的頁面被激活時開始。
   * **指定日期和時間：** 特定時間。 選取此選項時，按一下或點選日曆圖示，選取日期，並指定啟動活動的時間。

1. 要指定活動何時結束，請使用「結束」下拉菜單選擇以下值之一：

   * **停用時**:當包含目標內容的頁面被停用時，活動將結束。
   * **指定日期和時間**:特定時間。 選擇此選項後，按一下或點擊日曆表徵圖，選擇日期，並指定結束活動的時間。

1. 要指定活動的優先順序，請使用滑塊選擇 **低**。 **正常**&#x200B;或 **高**。
1. 如果您將Adobe Target用作目標引擎，請選擇要使用此活動測量的內容。 請參閱 [配置活動和設定目標](/help/sites-authoring/content-targeting-touch.md) 的子菜單。 必須至少選擇一個目標。
1. 按一下或點擊 **保存**。

   >[!NOTE]
   >
   >建立活動後，需要發佈該活動以使其可用。

## 發佈和取消發佈活動 {#publishing-and-unpublishing-activities}

您需要發佈活動以使其可用。 相反，您可能希望通過取消發佈活動來使活動不可用。

>[!NOTE]
>
>取消發佈活動時，除非刷新頁面，否則活動的狀態不會更改。

要發佈或取消發佈活動，請執行以下操作：

1. 按一下或點擊該品牌，然後按一下包含要發佈或取消發佈的活動的區域。
1. 按一下或按一下要發佈或取消發佈的活動或活動旁邊的表徵圖。

   ![screen-shot_2019-03-05at123846](assets/screen-shot_2019-03-05at123846.png)

1. 要發佈，請點擊或按一下 **發佈**。 要取消發佈，請點擊或按一下 **取消發佈**。 您的活動或活動在「活動」控制台中被發佈或未發佈，並且其狀態發生更改（可能需要刷新）。

## 有關作者和發佈實例的活動 {#activities-on-author-and-publish-instances}

激活使用Adobe Target目標引擎的活動時，將在發佈實例上建立第二個活動：

* 作者實例上的活動跟蹤作者實例上的活動，對於模擬訪問者體驗非常有用。 為此活動記錄的分析只反映作者實例上發生的情況。
* 發佈實例上的活動反映並響應發佈伺服器上的活動。 這是在公共網站上運行的活動。 只有發佈活動與跟蹤和分析實際公共站點的使用情況相關。

## 查看效能和轉換獲勝體驗(A/BTest) {#viewing-performance-and-converting-winning-experiences-a-b-test}

您可以看到任何Adobe Target活動（XT或A/B）的效能。 如果您使用A/B測試，您還可以轉換獲勝體驗，這將成為預設體驗。

要查看活動效能並轉換成功體驗，請執行以下操作：

1. 在 **個性化**，按一下 **活動** 導航至 **活動** 控制台。
1. 按一下或點擊要查看其活動的品牌。
1. 選取活動，然後按一下或點選「 **檢視屬性** 」，然後按一下「報表 **** 」標籤，然後選取您要檢視成功體驗之效能/轉換成功體驗的活動。將顯示效能資料。

   ![chlimage_1-115](assets/chlimage_1-115.png)

1. 按一下或點擊 **推贏者** 連結以將該體驗作為預設體驗。

   轉換獲獎者將執行以下操作：

   * 它禁用當前活動
   * 修改所有頁面，並用獲勝體驗的實際內容替換目標內容。 獲勝體驗的內容成為正常頁面的一部分 **無** 瞄準。

   ![chlimage_1-116](assets/chlimage_1-116.png)

   獲勝體驗是在報表中生成更多提升的體驗，這基於轉換率。

1. 按一下或點擊 **是** 確認要轉換獲勝者，請禁用當前體驗並用獲勝體驗的內容替換它。

## 與Adobe Target同步活動 {#synchronizing-activities-with-adobe-target}

使用Adobe Target瞄準引擎的活動與Adobe Target運動同步。 當滿足以下條件時，活動將自動同步到Adobe Target:

* 該活動至少包含一個體驗。
* 至少一個體驗包含映射段和一個優惠。
* 活動中的每種體驗都必須有相同數量的優惠。

這些條件適用於有關作者和發佈實例的活動。

同步活動時，將在Adobe Target建立相應的活動：

* 發佈實例上的活動與相應的Adobe Target市場活動同名。
* 作者實例上的活動與具有相同名稱的目標市場活動相對應 `_author` 尾碼。

![chlimage_1-117](assets/chlimage_1-117.png)

修改活動時，將立即同步作者活動(_A)。 即時同步允許使用Client Context或ContextHub模擬活動。

將活動發佈到發佈實例時，將同步發AEM布活動。

## 排除活動同步故障 {#troubleshooting-activity-synchronization}

當AEM將活動與Adobe Target同步AEM時，包括名為 `thirdPartyId`。 此屬性的值基於儲存庫中活動的路AEM徑。 在Adobe Target，沒有哪兩個運動對 `thirdPartyId` 屬性。 因此，如果Adobe Target的現有市場活動（不同類型的AB、XT）使用相同的值，則活動將無法同步 `thirdPartyId`。

這種情況可能發生在以下情況下：

1. 建立活動並與Adobe Target同步。
1. 在另AEM一個實例中，活動是在同一品牌下使用相同名稱建立的。 嘗試時，此活動的同步失敗。

這種情況也可能發生在以下情況下：

1. 建立活動並與Adobe Target同步。 然後，將刪除該活AEM動。
1. 活動在同一品牌下建立，並使用與刪除的活動相同的名稱。 嘗試時，此活動的同步失敗。

為避免同步問題，請始終為活動使用唯一名稱。 如果活動無法同步，則您可以刪除Adobe Target市的市場活動，該市場活動在未使用時使用相同名稱。

>[!NOTE]
>
>當您在Adobe Target建立市場活動時，它會指定一個名為 `thirdPartyId t`每次競選。 當你刪除Adobe Target的競選活動， `thirdPartyId` 未刪除。 您不能重新使用 `thirdPartyId` 對於不同類型的市場活動(AB、XT)，不能手動刪除它。 為避免此問題，請為每個活動指定一個唯一的名稱；因此，不能在不同的市場活動類型中重新使用市場活動名稱。
>
>如果在同一市場活動類型中使用相同的名稱，則將改寫現有市場活動。
>
>如果同步時遇到錯誤「請求失敗」。 `thirdPartyId` 已存在」，更改市場活動的名稱並再次同步。
