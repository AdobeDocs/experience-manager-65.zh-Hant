---
title: 與Adobe Campaign Classic和Adobe Campaign Standard合作
seo-title: Working with Adobe Campaign 6.1 and Adobe Campaign Standard
description: 您可以在中建立電子郵件內容AEM，並在Adobe Campaign電子郵件中處理
seo-description: You can create email content in AEM and process it in Adobe Campaign emails
uuid: 23195f0b-71c0-4554-8c8b-b0e7704d71d7
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 2fd0047d-d0f6-4289-98cf-454486f9cd61
exl-id: d7e4d424-0ca7-449f-95fb-c4fe19dd195d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2758'
ht-degree: 1%

---

# 與Adobe Campaign Classic和Adobe Campaign Standard合作{#working-with-adobe-campaign-classic-and-adobe-campaign-standard}

您可以在中建立電子郵件內AEM容並在Adobe Campaign電子郵件中處理。 要做到這一點，您必須：

1. 從特定於Adobe Campaign的AEM模板中建立新新聞簡報。
1. 選擇 [Adobe Campaign](#selecting-the-adobe-campaign-cloud-service-and-template) 編輯內容以訪問所有功能之前。
1. 編輯內容。
1. 驗證內容。

然後，內容可以與在Adobe Campaign的遞送同步。 本文檔中介紹了詳細說明。

另請參閱 [建立Adobe CampaignForms AEM](/help/sites-authoring/adobe-campaign-forms.md)。

>[!NOTE]
>
>在使用此功能之前，必須配置AEM以與 [Adobe Campaign](/help/sites-administering/campaignonpremise.md) 或 [Adobe Campaign Standard](/help/sites-administering/campaignstandard.md)。

## 通過Adobe Campaign發送電子郵件內容 {#sending-email-content-via-adobe-campaign}

配置和AEMAdobe Campaign後，您可以直接在中建立電子郵件傳遞內AEM容，然後在Adobe Campaign處理。

在中建立Adobe Campaign內AEM容時，必須先連結到Adobe Campaign服務，然後才能編輯內容以訪問所有功能。

可能有兩種情況：

* 內容可以與來自Adobe Campaign的傳送同步。 這允許您在交AEM付中使用內容。
* (僅限Adobe Campaign Classic)內容可以直接發送到Adobe Campaign，而後自動生成新的電子郵件傳送。 此模式具有限制。

本文檔中介紹了詳細說明。

### 建立新電子郵件內容 {#creating-new-email-content}

>[!NOTE]
>
>添加電子郵件模板時，請確保在 **/內容/活動** 讓它們可用。

#### 建立新電子郵件內容 {#creating-new-email-content-1}

1. 在選AEM擇 **站點** 然後 **市場活動**，然後瀏覽到管理電子郵件活動的位置。 在以下示例中，路徑為 **站點** > **市場活動** > **Geometrixx Outdoors** > **電子郵件活動**。

   >[!NOTE]
   >
   >[電子郵件示例僅在Geometrixx中提供](/help/sites-developing/we-retail.md)。 請從包共用下載示例Geometrixx內容。

   ![chlimage_1-15](assets/chlimage_1-15a.png)

1. 選擇 **建立** 然後 **建立頁**。
1. 選擇您要連接到的Adobe Campaign的可用模板之一，然後按一下 **下一個**。 預設情況下有三個模板：

   * **Adobe Campaign Classic電子郵件**:允許您在將內容發送到Adobe Campaign Classic以交付之前，將內容添加到預定義模板（兩列）。
   * **Adobe Campaign Standard電子郵件**:允許您在將內容發送到Adobe Campaign Standard以交付之前，將內容添加到預定義模板（兩列）。

1. 填寫 **標題** （可選） **說明** 按一下 **建立**。 標題用作新聞簡報/電子郵件的主題，除非您在編輯電子郵件時覆蓋它。

### 選擇Adobe Campaign雲服務和模板 {#selecting-the-adobe-campaign-cloud-service-and-template}

要與Adobe Campaign整合，您需要在頁面中添加Adobe Campaign雲服務。 這樣，您就可以訪問個性化和其他Adobe Campaign資訊。

此外，您還可能需要選擇Adobe Campaign模板並更改主題，並為那些不在HTML中查看電子郵件的用戶添加純文字檔案內容。

您可以從 **站點** 或在您建立電子郵件/新聞稿後從其中發送。

從 **站點** 頁籤是推薦的方法。 從電子郵件/新聞稿中選擇雲服務需要一種解決方法。

從 **站點** 頁：

1. 在AEM選擇電子郵件頁面並按一下 **查看屬性**。

   ![chlimage_1-16](assets/chlimage_1-16a.png)

1. 選擇 **編輯** 然後 **雲服務** 頁籤，向下滾動到底部，然後按一下+號添加配置，然後選擇 **Adobe Campaign**。

   ![chlimage_1-17](assets/chlimage_1-17a.png)

1. 從下拉清單中選擇與Adobe Campaign實例匹配的配置，然後按一下確認 **保存**。
1. 通過按一下&#x200B;**Adobe Campaign** 頁籤。 如果要選擇其他模板，可以在編輯時從電子郵件中訪問該模板。

   如果要應用特定的電子郵件傳遞模板(來自Adobe Campaign)，而不是預設郵件模板，請在 **屬性**，選擇 **Adobe Campaign** 頁籤。 在相關的Adobe Campaign實例中輸入電子郵件傳遞模板的內部名稱。

   您選擇的模板決定了哪些個性化欄位可從Adobe Campaign獲得。

   ![chlimage_1-18](assets/chlimage_1-18a.png)

在創作時的新聞稿/電子郵件中，您可能無法在 **頁面屬性** 因為佈局問題。 您可以使用下面介紹的解決方法：

1. 在AEM選擇電子郵件頁面並按一下 **編輯**。 按一下 **開啟屬性**。

   ![chlimage_1-19](assets/chlimage_1-19a.png)

1. 選擇 **雲服務** 按一下 **+** 的子菜單。 選擇任何可見配置（與哪個配置無關）。 按一下或點擊 **+** 登錄以添加其他配置，然後選擇 **Adobe Campaign**。

   >[!NOTE]
   >
   >或者，您可以通過選擇 **查看屬性** 的 **站點** 頁籤。

1. 從下拉清單中選擇與Adobe Campaign實例匹配的配置，刪除您建立的第一個不用於Adobe Campaign的配置，然後按一下複選標籤進行確認。
1. 繼續上一步驟中的步驟4以選擇模板並添加純文字檔案。

### 編輯電子郵件內容 {#editing-email-content}

要編輯電子郵件內容：

1. 開啟電子郵件，預設情況下，您進入編輯模式。

   ![chlimage_1-20](assets/chlimage_1-20a.png)

1. 如果要更改電子郵件的主題或為那些不以HTML方式查看電子郵件的用戶添加純文字檔案，請選擇 **電子郵件** 並添加主題和文本。 選擇頁面表徵圖以從HTML自動生成純文字檔案版本。 完成後按一下複選標籤。

   您可以使用Adobe Campaign個性化欄位個性化新聞稿。 要添加個性化欄位，請按一下顯示Adobe Campaign徽標的按鈕，開啟個性化欄位選取器。 然後，您可以從此新聞稿可用的所有欄位中進行選擇。

   >[!NOTE]
   >
   >如果編輯器中屬性中的個性化欄位呈灰色顯示，請重新檢查您的配置。

   ![chlimage_1-21](assets/chlimage_1-21a.png)

1. 開啟螢幕左側的元件面板並選擇 **Adobe Campaign通訊** 的下界。

   ![chlimage_1-22](assets/chlimage_1-22a.png)

1. 將元件直接拖到繪圖頁上，並相應地編輯它們。 例如，可以 **文本和個性化（市場活動）** 元件和添加個性化文本。

   ![chlimage_1-23](assets/chlimage_1-23a.png)

   請參閱 [Adobe Campaign元件](/help/sites-authoring/adobe-campaign-components.md) 的子菜單。

   ![chlimage_1-24](assets/chlimage_1-24a.png)

### 插入個性化 {#inserting-personalization}

編輯內容時，可以插入：

* Adobe Campaign上下文欄位。 這些欄位可以插入文本中，並根據收件人的資料（例如，名字、姓氏或目標維的任何資料）進行調整。
* Adobe Campaign個性化區。 這些是與收件人資料無關的預定義內容塊，如品牌徽標或指向鏡像頁面的連結。

請參閱 [Adobe Campaign元件](/help/sites-authoring/adobe-campaign-components.md) 的子菜單。

>[!NOTE]
>
>* 只有Adobe Campaign的田地 **配置檔案** 目標維度被考慮在內。
>* 查看屬性時 **站點**，您無權訪問Adobe Campaign上下文欄位。 您可以在編輯時直接從電子郵件訪問這些內容。


插入個性化：

1. 插入新 **新聞稿** > **文本和個性化（市場活動）** 將元件拖到頁面上。

   ![chlimage_1-25](assets/chlimage_1-25a.png)

1. 按一下「鉛筆」(Pencil)表徵圖開啟元件。 就地編輯器開啟。

   ![chlimage_1-26](assets/chlimage_1-26a.png)

   >[!NOTE]
   >
   >**Adobe Campaign Standard:**
   >
   >* 可用上下文欄位與 **配置檔案** 瞄準Adobe Campaign。
   >* 請參閱 [將頁面AEM連結到Adobe Campaign電子郵件](#linking-an-aem-page-to-an-adobe-campaign-email-adobe-campaign-standard)。

   >
   >**Adobe Campaign Classic:**
   >
   >* 可用的上下文欄位從Adobe Campaign動態恢復 **nms:seedMember** 架構。 從包含與內容同步的傳遞的工作流動態恢復目標擴展資料。 (請參閱 [將建立的內容與AEM來自Adobe Campaign的傳送同步](#synchronizing-content-created-in-aem-with-a-delivery-from-adobe-campaign-classic) )的正平方根。
   >
   >* 要添加或隱藏個性化元素，請參閱 [管理個性化欄位和塊](/help/sites-administering/campaignonpremise.md#managing-personalization-fields-and-blocks)。
   >* **重要**:所有種子表欄位也必須位於收件人表（或相應的聯繫表）中。


1. 通過鍵入插入文本。 通過按一下Adobe Campaign元件並選擇它們，插入上下文欄位或個性化塊。 完成後，選擇複選標籤。

   ![chlimage_1-27](assets/chlimage_1-27a.png)

   插入上下文欄位或個性化塊後，您可以預覽新聞稿並test欄位。 請參閱 [預覽新聞稿](#previewing-a-newsletter)。

### 預覽新聞稿 {#previewing-a-newsletter}

您可以預覽新聞稿的外觀以及預覽個性化。

1. 開啟新聞稿後，按一下 **預覽** 右上角AEM。 顯AEM示新聞稿在用戶收到時的外觀。

   ![chlimage_1-28](assets/chlimage_1-28a.png)

   >[!NOTE]
   >
   >如果您使用Adobe Campaign Standard並使用示例模板，則兩個顯示初始內容的個性化塊 —  **&quot;&lt;%@ include view=&quot;MirrorPage&quot; %>&quot;** 和 **&quot;&lt;%@ include view=&quot;UnsubscriptionLink&quot; %>&quot;**  — 在交付期間導入內容時將引發錯誤。 您可以通過使用個性化塊選取器選擇相應的塊來調整這些塊。

1. 要預覽個性化設定，請通過按一下/點擊工具欄中的相應表徵圖來開啟ContextHub。 個性化欄位標籤現在被所選個人的種子資料替換。 查看在ContextHub中切換角色時變數如何調整。

   ![chlimage_1-29](assets/chlimage_1-29a.png)

1. 您可以查看來自Adobe Campaign的與當前選定的角色關聯的種子資料。 要執行此操作，請按一下/點擊ContextHub欄中的Adobe Campaign模組。 此時將開啟一個對話框，顯示當前配置檔案的所有種子資料。 同樣，當切換到其他角色時，資料會適應。

   ![chlimage_1-30](assets/chlimage_1-30a.png)

### 在中批准內AEM容 {#approving-content-in-aem}

內容完成後，您可以啟動審批流程。 轉到 **工作流** 的子菜單。 **批准Adobe Campaign** 工作流。

此現成工作流分為兩個步驟：修訂，然後審批，或修訂，然後拒絕。 然而，該工作流可以擴展並適應更複雜的過程。

![chlimage_1-31](assets/chlimage_1-31a.png)

要批准Adobe Campaign的內容，請通過選擇 **工作流** 選擇 **批准Adobe Campaign** 按一下 **啟動工作流**。 執行步驟並批准內容。 也可以通過選擇 **拒絕** 而不是 **批准** 的上界。

![chlimage_1-32](assets/chlimage_1-32a.png)

內容獲得批准後，它似乎在Adobe Campaign獲得批准。 然後可以發送電子郵件。

在Adobe Campaign Standard:

![chlimage_1-33](assets/chlimage_1-33a.png)

在Adobe Campaign Classic:

![chlimage_1-34](assets/chlimage_1-34a.png)

>[!NOTE]
未批准的內容可以與Adobe Campaign的傳遞同步，但無法執行該傳遞。 只能通過市場活動交付發送已批准的內容。

## 連接AEMAdobe Campaign Standard和Adobe Campaign Classic {#linking-aem-with-adobe-campaign-standard-and-adobe-campaign-classic}

您與Adobe Campaign的鏈AEM接或同步方式取決於您是使用基於訂閱的Adobe Campaign Standard，還是使用基於內部部署的Adobe Campaign Classic。

有關基於您的Adobe Campaign解決方案的說明，請參閱以下各節：

* [將頁AEM面連結到Adobe Campaign電子郵件(Adobe Campaign Standard)](#linking-an-aem-page-to-an-adobe-campaign-email-adobe-campaign-standard)
* [將建立的內容與AEM來自Adobe Campaign Classic的傳遞同步](#synchronizing-content-created-in-aem-with-a-delivery-from-adobe-campaign-classic)

### 將頁AEM面連結到Adobe Campaign電子郵件(Adobe Campaign Standard) {#linking-an-aem-page-to-an-adobe-campaign-email-adobe-campaign-standard}

Adobe Campaign Standard允許您恢復和連結在中建立的AEM內容：

* 一封電子郵件。
* 電子郵件模板。

這樣，您就可以提供內容。 您可以通過頁面上顯示的代碼查看新聞稿是否連結到單個交貨。

![chlimage_1-35](assets/chlimage_1-35a.png)

>[!NOTE]
如果新聞稿連結到多個交貨，則連結的交貨數（但不顯示每個ID）。

要將在中建立的頁面與來自AEMAdobe Campaign的電子郵件連結：

1. 基於特定電子郵件模AEM板建立新電子郵件。 請參閱 [在Adobe Campaign Standard建立電子郵件](https://helpx.adobe.com/campaign/standard/channels/using/creating-an-email.html) 的子菜單。

   ![chlimage_1-36](assets/chlimage_1-36a.png)

1. 開啟 **內容** 從交貨儀表板中鎖定。

   ![chlimage_1-37](assets/chlimage_1-37a.png)

1. 選擇 **連結Adobe Experience Manager內容** 的子菜單AEM。

   >[!NOTE]
   如果 **連結Adobe Experience Manager** 選項，檢查 **內容編輯模式** 已正確配置為 **Adobe Experience Manager** 的子菜單。

   ![chlimage_1-38](assets/chlimage_1-38a.png)

1. 選擇要在電子郵件中使用的內容。

   此清單指定：

   * 中內容的標籤AEM。
   * 中內容的批准狀AEM態。 如果內容未獲批准，則可以同步內容，但必須在發送前批准內容。 但是，您可以執行某些操作，如發送證明或預覽test。
   * 內容上次修改的日期。
   * 任何已連結到傳遞的內容。

   >[!NOTE]
   預設情況下，已與傳遞同步的內容將隱藏。 但是，您可以顯示並使用它。 例如，如果要將內容用作多個交貨的模板。

   當電子郵件連結到某個內AEM容時，該內容在Adobe Campaign無法編輯。

1. 從其儀表板指定電子郵件的其他參數（訪問群體、執行計畫）。
1. 執行電子郵件傳遞。 在傳遞分析期間，檢索內容的最新AEM版本。

   >[!NOTE]
   如果內容在鏈AEM接到電子郵件時在中更新，則分析期間將在Adobe Campaign自動更新。 也可以使用 **刷新Adobe Experience Manager內容** 的子菜單。
   您可以使用 **刪除與Adobe Experience Manager內容的連結** 的子菜單。 僅當內容已與傳遞連結時，此按鈕才可用。 要將其他內容與傳遞連結起來，必須先刪除當前內容連結，然後才能建立新連結。
   刪除連結後，本地內容將保留並在Adobe Campaign可編輯。 如果在修改內容後再次連結內容，則所有更改都將丟失。

### 將建立的內容與AEM來自Adobe Campaign Classic的傳送同步 {#synchronizing-content-created-in-aem-with-a-delivery-from-adobe-campaign-classic}

Adobe Campaign允許您恢復和同步在中建立的AEM內容：

* 市場活動交付
* 市場活動工作流中的交貨活動
* 循環交貨
* 連續交付
* 消息中心傳遞
* 交貨模板

在AEM中，如果新聞稿連結到單個交貨，則交貨代碼將顯示在頁面上。

![chlimage_1-39](assets/chlimage_1-39a.png)

>[!NOTE]
如果新聞稿連結到多個交貨，則連結的交貨數（但不顯示每個ID）。
[!NOTE]
工作流步驟 **發佈到Adobe Campaign** 在6.AEM1中不建議使用。這一步是與Adobe CampaignAEM6.0一體化的一部分，不再必要。

要將在中建立的內容與來自AEMAdobe Campaign的傳送同步，請執行以下操作：

1. 通過選擇 **帶內容的電AEM子郵件發送(mailAEMContent)** 交貨模板。

   ![chlimage_1-40](assets/chlimage_1-40a.png)

1. 選擇 **同步** 的子菜單AEM。

   >[!NOTE]
   如果 **同步** 的子菜單，檢查 **內容編輯模式** 欄位在中正確配置 **AEM** 通過 **屬性** > **高級**。

   ![chlimage_1-41](assets/chlimage_1-41a.png)

1. 選擇要與交貨同步的內容。

   此清單指定：

   * 中內容的標籤AEM。
   * 中內容的批准狀AEM態。 如果內容未獲批准，則可以同步內容，但必須在發送前批准內容。 但是，您可以執行某些操作，如發送BAT或預覽test。
   * 上次修改內容的日期。
   * 任何已連結到傳遞的內容。

   >[!NOTE]
   預設情況下，已與傳遞同步的內容將隱藏。 但是，您可以顯示並使用它。 例如，如果要將內容用作多個交貨的模板。

   ![chlimage_1-42](assets/chlimage_1-42a.png)

1. 指定交貨的其他參數（目標等）
1. 如有必要，請在Adobe Campaign啟動交付審批流程。 除了在Adobe CampaignAEM（預算、目標等）中配置的批准外，還需要在中進行內容批准。 只有在中已批准內容時，才可能在Adobe Campaign中批准內AEM容。
1. 執行交貨。 在交付分析期間，恢復內容的最新AEM版本。

   >[!NOTE]
   * 在傳送和內容同步後，Adobe Campaign的傳送內容變為只讀。 無法再修改電子郵件主題及其內容。
   * 如果內容在鏈AEM接到Adobe Campaign的交付時在中更新，則在交付分析期間在交付中自動更新。 還可以使用 **立即刷新內容** 按鈕
   * 可以使用 **取消同步** 按鈕 僅當內容已與傳遞同步時，才可使用此選項。 要將其他內容與傳遞同步，必須取消當前內容同步，然後才能建立新連結。
   * 如果本地內容已失同步，則會保留該內容並在Adobe Campaign中變為可編輯。 如果在修改內容後重新同步內容，則將丟失所有更改。
   * 對於定期和連續的遞送，每次AEM執行遞送時都停止與內容的同步。

