---
title: 管理活動
seo-title: 管理活動
description: 「活動」主控台可讓您建立、組織和管理品牌的行銷活動
seo-description: 「活動」主控台可讓您建立、組織和管理品牌的行銷活動
uuid: 0aebf88e-f298-410a-8c82-4076b671624f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: ef2321a3-cd51-4298-8782-e1a2ca721868
docset: aem65
translation-type: tm+mt
source-git-commit: d53e72b198db91d368ddddac768d19b88ee29050

---


# 管理活動{#managing-activities}

「活動」主控台可讓您建立、組織和管理品牌的 [行銷活](/help/sites-authoring/personalization.md#activities) 動：

* 新增品牌。
* 針對每個品牌新增及設定活動。
* 管理活動。

>[!NOTE]
>
>如果您使用Adobe Target做為定位引擎，您也可以檢 [視活動的效能資料](#viewing-performance-and-converting-winning-experiences-a-b-test)。 如果您使用A/B測試，可以轉換 [贏家](#viewing-performance-and-converting-winning-experiences-a-b-test)。

在「活動」控制台上，活動按品牌組織。 您可以使用品牌和資料夾來組織您的活動。 您可以點選／按一下「個人化」並點選／按一下「活 **動** 」，以導覽至「活動 **」主控台**。

活動可在「定位」模式下，用 [於製作目標內容](/help/sites-authoring/content-targeting-touch.md)，您也可以在此建立活動。 您在「定位」模式下建立的活動會顯示在「活動」主控台中。

活動會顯示一個標籤，說明定義的活動類型：

* XT - Adobe target體驗目標
* A/B - Adobe Target A/B測試
* AEM - Adobe Experience manager目標鎖定（contexthub或clientcontext driven）

![chlimage_1-114](assets/chlimage_1-114.png)

>[!NOTE]
>
>可用的活動類型由以下各項決定：

>* 如果 **AEM端使用的Adobe Target租用戶(clientcode)上啟用** xt_only **選項以連線至Adobe Target，則您只能在AEM中建立** XT活動。
   >
* 如果 **Adobe Target租用戶(clientcode)** 未啟用xt_only **** 選項 **，則您可以在AEM中建立** XT和A/B活動。

**** 其他附註： **xt_only** options是套用在特定Target租用戶（客戶代碼）上的設定，只能在Adobe Target中直接修改。 您無法在AEM中啟用或停用此選項。

>[!CAUTION]
您必須保護發佈例項上的活動設 **定節點cq:ActivitySettings** ，如此一般使用者便無法存取它。 處理Adobe Target活動同步的服務只能訪問活動設定節點。
如需詳 [細資訊，請參閱與Adobe target整合的必要條件](/help/sites-administering/target-requirements.md#securingtheactivitysettings) 。

## 使用活動控制台建立品牌 {#creating-a-brand-using-the-activities-console}

建立您要管理行銷活動的品牌。

當您使用「活動」主控台建立品牌時，該品牌也會出現在「選件」主控台中 [](/help/sites-authoring/offerlib.md) ，您可在此處建立選件，以供您的活動體驗使用。

1. 在導覽主控台中，按一下或點選「個 **人化」**。 按一下或點選「 **活動**」。

   ![screen_shot_2018-03-21at151821](assets/screen_shot_2018-03-21at151821.png)

1. 在「活動」主控台中，按一下或點選「 **建立**」**，然後點選「建立品牌」**。
1. 選取品牌範本，然後按一下或點選「下 **一步**」。
1. 在「活動」和「選件」控制台中，輸入您想要該品牌的標題。 （可選）鍵入或選擇一個或多個標籤以與品牌關聯。
1. 按一下或點選「 **建立**」。 您的品牌會出現在「活動」主控台中。

## 使用活動控制台添加／編輯活動 {#adding-editing-an-activity-using-the-activities-console}

新增活動或編輯現有活動，將行銷工作集中在特定受眾。 當您建立／編輯活動時，請指定下列資訊：

* **** 名稱：活動的名稱。
* **** 定位引擎：AEM [](/help/sites-authoring/personalization.md#aem) 或 [Adobe Target](/help/sites-authoring/personalization.md#adobe-target) ，做為目標內容的引擎。

* **** 選擇目標配置：（僅限Adobe Target）此活動應用來連線至Adobe Target的雲端設定。 只有在為「定位引擎」選取Adobe Target時，才會顯示此選項。
* **活動類型：**活動類型- A/B測試或體驗定位
* **** 目標：（可選）活動的說明。
* **** 體驗：對象名稱與您所定位之行銷區段之間的對應。
* **** 流量百分比：如果選取A/B測試，您可以變更每個體驗的流量（百分比）。
* **** 持續時間：套用活動的時段。
* **** 優先順序：活動的相對優先順序。 當活動提供相同使用者區段的內容時，優先順序較高的活動優先。
* **** 目標量度：如果選取Adobe target作為定位引擎，您可以將成功度量新增至活動。 需要一個成功度量。

>[!NOTE]
新的Adobe target活動必須在目 ***標內容編輯器中建立*** ，而不是在 **Activity** Console中，因為與Adobe target的同步將會失敗。
不過，您可以在主控台中編輯現有的Adobe Target活動。

要添加活動，請執行以下操作：

1. 按一下或點選您要建立活動的品牌，然後按一下或點選**「建立」，然 **後** 「建立活動」。 **如果編輯，請在「主版區域」畫面中選取活動，然後按一下或點選「編輯 **活動」**。
1. 提供下列資訊，然後按一下或點選「下 **一步**」:

   * 活動的名稱。
   * 要使用的定位引擎。 預設會選取ContextHub(AEM)。 如果您需要使用Adobe Target，請在目標內容編輯器中建立活動。
   * 如果您選取Adobe target做為定位引擎，請選取／編輯雲端設定，以用來連線至Adobe Target。 （請注意，您不要選取您為雲端設定所建立的架構。）
   * （可選）活動的目標或說明。
   * 選擇活動類型。

1. 新增一或多個體驗至活動。 按一下或點選「 **新增體驗」**。
1. 如果您使用AEM定位或Adobe Target體驗定位：

   1. 按一下或點選**選取對象**，然後選取您的體驗目標群體。
   1. 按一下或點選「 **新增體驗**」，輸入名稱，然後按一下或點選「 **確定」**。

   1. 按一下或點選「 **下一步**」。
   如果您使用Adobe Target A/B測試：

   1. 按一下或點選「觀眾」方塊中的鉛筆，以選取觀眾。
   1. 按一下或點選「 **新增體驗**」，輸入名稱，然後按一下或點選「 **確定」**。

   1. 輸入顯示每個體驗的流量百分比。
   1. 按一下或點選「 **下一步**」。


1. 若要指定活動何時啟動，請使用「 **開始** 」下拉式功能表來選取下列值之一：

   * **** 啟動時：活動會在包含目標內容的頁面被啟用時開始。
   * **** 指定的日期和時間：特定時間。 選取此選項時，按一下或點選日曆圖示，選取日期，並指定啟動活動的時間。

1. 要指定活動何時結束，請使用「結束」下拉菜單選擇以下值之一：

   * **停用時**:當包含目標內容的頁面停用時，活動便會結束。
   * **指定的日期和時間**:特定時間。 選取此選項時，按一下或點選日曆圖示，選取日期，並指定結束活動的時間。

1. 要指定活動的優先順序，請使用滑塊選擇「低 **」**、「 **正常**」或「 **高」**。
1. 如果您使用Adobe target做為定位引擎，請選取您要使用此活動來測量的項目。 如需 [可用成功度量的詳細資訊](/help/sites-authoring/content-targeting-touch.md) ，請參閱設定活動和設定目標。 您必須至少選擇一個目標。
1. 按一下或點選「 **儲存**」。

   >[!NOTE]
   建立活動後，您必須發佈活動，才能使用。

## 發佈和取消發佈活動 {#publishing-and-unpublishing-activities}

您需要發佈活動才能使活動可供使用。 相反地，您可能想要取消發佈活動，讓活動無法使用。

>[!NOTE]
取消發佈活動時，

若要發佈或取消發佈活動：

1. 按一下或點選品牌，然後是包含您要發佈或取消發佈之活動的區域。
1. 點選或按一下您要發佈或取消發佈之活動旁的圖示。

   ![screen-shot_2019-03-05at123846](assets/screen-shot_2019-03-05at123846.png)

1. 若要發佈，請點選或按一下「 **發佈**」。 若要解除發佈，請點選或按一下「 **解除發佈**」。 您的活動或活動會在「活動」主控台中發佈或取消發佈，且其狀態會變更（可能需要重新整理）。

## 作者與發佈例項的活動 {#activities-on-author-and-publish-instances}

啟用使用Adobe target目標引擎的活動時，會在發佈例項上建立第二個活動：

* 作者例項上的活動會追蹤作者例項上的活動，對於模擬訪客體驗非常有用。 針對此活動記錄的分析只反映作者例項的發生。
* 發佈實例上的活動反映並響應發佈伺服器上的活動。 這是在公共網站上執行的活動。 只有發佈活動與追蹤和分析實際公開網站的使用情況相關。

## 檢視效能和轉換成功體驗（A/B測試） {#viewing-performance-and-converting-winning-experiences-a-b-test}

您可以看到任何Adobe Target活動（XT或A/B）的效能。 如果您使用A/B測試，您也可以轉換成功體驗，然後變成預設體驗。

若要檢視活動效能並轉換成功體驗：

1. 在「 **個人化**」中，按一下或點選「 **活動** 」以導覽至「活 **動** 」主控台。
1. 按一下或點選您要查看其活動的品牌。
1. 選取活動，然後按一下或點選「 **檢視屬性** 」，然後按一下「報表 **** 」標籤，然後選取您要檢視成功體驗之效能／轉換成功體驗的活動。 將顯示效能資料。

   ![chlimage_1-115](assets/chlimage_1-115.png)

1. 按一下或點選「 **推播成功者** 」連結，將該體驗推送為預設體驗。

   轉換成功者會執行下列動作：

   * 它會停用目前的活動
   * 修改所有頁面，並以成功體驗的實際內容取代目標內容。 成功體驗的內容會成為正常頁面的一部分，而無 **目標** 。
   ![chlimage_1-116](assets/chlimage_1-116.png)

   成功體驗是指根據轉換率在報表中產生更多提升度的體驗。

1. 按一下或點 **選「是** 」以確認您要轉換成功者、停用目前的體驗並以成功體驗的內容取代。

## 與Adobe Target同步化活動 {#synchronizing-activities-with-adobe-target}

使用Adobe Target定位引擎的活動會與Adobe Target促銷活動同步。 當符合下列條件時，活動會自動同步至Adobe Target:

* 活動至少包含一個體驗。
* 至少有一個體驗包含映射的區段和一個選件。
* 活動中的每個體驗都必須有相同的選件數。

這些條件適用於作者和發佈例項的活動。

同步活動時，Adobe target會建立對應的促銷活動：

* 發佈例項上的活動與對應的Adobe Target促銷活動具有相同名稱。
* 作者例項上的活動會與名稱相同且加上尾碼的Target促銷 `_author` 活動。

![chlimage_1-117](assets/chlimage_1-117.png)

修改活動時，會立即同步_author活動。 立即同步可讓您模擬使用Client Context或ContextHub的活動。

當活動發佈至AEM發佈例項時，會同步發佈活動。

## 活動同步疑難排解 {#troubleshooting-activity-synchronization}

當AEM與Adobe Target同步活動時，AEM會包含名為的活動屬性 `thirdPartyId`。 此屬性的值以AEM儲存庫中活動的路徑為基礎。 Adobe target中沒有兩個促銷活動可以具有相同的屬性 `thirdPartyId` 值。 因此，如果Adobe Target中的現有促銷活動（AB,XT類型不同）使用相同的值，則無法同步活動 `thirdPartyId`。

這種情況可能發生在以下情況下：

1. 活動會建立並與Adobe Target同步。
1. 在另一個AEM例項中，會以相同品牌建立活動，並使用相同名稱。 嘗試同步此活動時失敗。

這種情況也可能發生在以下情況下：

1. 活動會建立並與Adobe Target同步。 然後會在AEM上刪除活動。
1. 活動是在相同品牌下建立，並使用與已刪除活動相同的名稱。 嘗試同步此活動時失敗。

為避免同步化問題，請務必為活動使用唯一的名稱。 如果活動無法同步，您可以刪除Adobe Target中未使用相同名稱的促銷活動。

>[!NOTE]
當您在Adobe target中建立促銷活動時，會指派一個名為每個促銷活動 `thirdPartyId t`的屬性。 當您在Adobe target中刪除促銷活動時， `thirdPartyId` 不會刪除。 您無法針對不同類 `thirdPartyId` 型(AB、XT)的促銷活動重新使用，且無法手動移除。 為避免此問題，請為每個促銷活動命名一個唯一的名稱；因此，促銷活動名稱無法重複用於不同的促銷活動類型。
如果您在相同的促銷活動類型中使用相同的名稱，您將會覆寫現有的促銷活動。
如果在同步時，您會遇到「請求失敗」錯誤。 `thirdPartyId` 已存在」，請變更促銷活動的名稱，然後再次同步。

