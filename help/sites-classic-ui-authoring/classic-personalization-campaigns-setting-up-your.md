---
title: 設定您的行銷活動
description: 設定新的行銷活動需要建立品牌以舉辦您的行銷活動、建立行銷活動以舉辦體驗，以及最後定義新行銷活動的屬性。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: 1b607a52-f065-4e35-8215-d54df7c8403d
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '2194'
ht-degree: 0%

---

# 設定您的行銷活動{#setting-up-your-campaign}

設定新的行銷活動包括下列（一般）步驟：

1. [建立品牌](#creating-a-new-brand)以舉辦您的行銷活動。
1. 如有必要，您可以[定義新品牌的內容](#defining-the-properties-for-your-new-brand)。
1. [建立行銷活動](#creating-a-new-campaign)以保留體驗；例如Teaser頁面或電子報。
1. 如有必要，您可以[為新的行銷活動](#defining-the-properties-for-your-new-campaign)定義屬性。

然後，根據您建立的體驗型別，您必須[建立體驗](#creating-a-new-experience)。 體驗的詳細資訊及其建立後的動作取決於您要建立的體驗型別：

* 如果建立Teaser：

   1. [建立Teaser體驗](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingateaserexperience)。
   1. [新增內容至您的Teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#addingcontenttoyourteaser)。
   1. [為您的Teaser建立接觸點](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingatouchpointforyourteaser) （將您的Teaser新增至內容頁面）。

* 如果建立Newsletter：

   1. [建立電子報體驗](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatinganewsletterexperience)。
   1. [將內容新增至Newsletter。](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#addingcontenttonewsletters)
   1. [個人化電子報。](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#personalizingnewsletters)
   1. [建立極具吸引力的Newsletter登陸頁面](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#settingupanewsletterlandingpage)。
   1. [傳送Newsletter](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#sendingnewsletters)給訂閱者或潛在客戶。

* 如果建立Adobe Target （先前稱為Test&amp;Target）選件：

   1. [建立Adobe Target選件體驗](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingatesttargetofferexperience)。
   1. [整合Adobe Target](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#integratewithadobetesttarget)

>[!NOTE]
>
>如需定義區段的詳細指示，請參閱[區段](/help/sites-administering/campaign-segmentation.md)。

## 建立新品牌 {#creating-a-new-brand}

1. 開啟&#x200B;**MCM**&#x200B;並在左窗格中選取&#x200B;**促銷活動**。

1. 選取「**新增……**」以輸入&#x200B;**Title**&#x200B;和&#x200B;**Name**&#x200B;以及要用於新品牌的範本：

   ![chlimage_1-17](assets/chlimage_1-17.png)

1. 按一下「**建立**」。您的新品牌會顯示在MCM中（具有預設圖示）。

### 定義新品牌的屬性 {#defining-the-properties-for-your-new-brand}

1. 從左窗格中的&#x200B;**行銷活動**，在右窗格中選取您的新品牌圖示，然後按一下&#x200B;**內容……**

   您可以輸入&#x200B;**Title**、**Description**&#x200B;以及要做為圖示的影像。

   ![chlimage_1-18](assets/chlimage_1-18.png)

1. 按一下&#x200B;**確定**&#x200B;以儲存。

### 建立新行銷活動 {#creating-a-new-campaign}

1. 從&#x200B;**行銷活動**，在左窗格中選取您的新品牌，或按兩下右窗格中的圖示。

   概覽隨即顯示（如果品牌是新的，則為空白）。

1. 按一下&#x200B;**新增……**，並指定要用於新行銷活動的&#x200B;**標題**、**名稱**&#x200B;和範本。

   ![chlimage_1-19](assets/chlimage_1-19.png)

1. 按一下「**建立**」。您的新行銷活動會顯示在MCM中。

### 定義新行銷活動的屬性 {#defining-the-properties-for-your-new-campaign}

設定控制行為的行銷活動屬性：

* **優先順序：**&#x200B;此行銷活動相對於其他行銷活動的優先順序。 同時開啟多個行銷活動時，具有最高優先順序的行銷活動會控制訪客體驗。
* **開啟與關閉時間：**&#x200B;這些屬性會控制行銷活動控制訪客體驗的時間期間。 開啟時間屬性會控制行銷活動開始控制體驗的時間。 關閉時間屬性可控制行銷活動何時停止控制體驗。
* **影像：**&#x200B;代表AEM中行銷活動的影像。
* **Cloud Services：**&#x200B;與行銷活動整合的Cloud Service設定。 (請參閱[與Adobe Marketing Cloud整合](/help/sites-administering/marketing-cloud.md)。)

* **Adobe Target：**&#x200B;設定與Adobe Target整合之行銷活動的屬性。 (請參閱[與Adobe Target整合](/help/sites-administering/target.md)。)

1. 從&#x200B;**行銷活動**，選取您的品牌。 在右窗格中，選取您的行銷活動，然後按一下&#x200B;**屬性**。

   您可以輸入各種屬性，包括&#x200B;**Title**、**Description**&#x200B;以及您想要的任何&#x200B;**Cloud Service**。

   ![chlimage_1-20](assets/chlimage_1-20.png)

1. 按一下&#x200B;**確定**&#x200B;以儲存。

### 建立新體驗 {#creating-a-new-experience}

建立體驗的程式取決於體驗型別：

* [建立Teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingateaser)
* [建立Newsletter](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatinganewsletter)
* [建立Adobe Target選件](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingatesttargetoffer)

>[!NOTE]
>
>和舊版一樣，仍可在&#x200B;**網站**&#x200B;主控台中將體驗建立為頁面（且舊版中建立的任何這類頁面仍完全受支援）。
>
>建議的作法是現在使用MCM來建立體驗。

### 設定您的新體驗 {#configuring-your-new-experience}

現在您已為體驗建立基本骨架，您必須根據體驗型別繼續下列動作：

* [預告](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#teasers)：

   * [將Teaser頁面連結至訪客區段。](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#applyingasegmenttoyourteaser)
   * [為您的Teaser建立接觸點](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingatouchpointforyourteaser) （將您的Teaser新增至內容頁面）。

* [電子報](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#newsletters)：

   * [將內容新增至Newsletter。](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#addingcontenttonewsletters)
   * [個人化電子報。](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#personalizingnewsletters)
   * [傳送Newsletter](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#sendingnewsletters)給訂閱者或潛在客戶。
   * [建立極具吸引力的Newsletter登陸頁面](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#settingupanewsletterlandingpage)。

* [Adobe Target選件](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#testtargetoffers)：

   * [整合Adobe Target](/help/sites-administering/target.md)

### 新增接觸點 {#adding-a-new-touchpoint}

如果您有現有的體驗，您可以直接從MCM的「行事曆」檢視新增接觸點：

1. 選取行銷活動的行事曆檢視。

1. 按一下&#x200B;**新增接觸點……**&#x200B;以開啟對話方塊。 指定要新增的體驗：

   ![chlimage_1-21](assets/chlimage_1-21.png)

1. 按一下&#x200B;**確定**&#x200B;以儲存。

## 使用銷售機會 {#working-with-leads}

>[!NOTE]
>
>Adobe不打算進一步增強此功能（管理銷售機會）。
>建議使用[Adobe Campaign以及與AEM](/help/sites-administering/campaign.md)的整合。

在AEM MCM中，您可以手動輸入潛在客戶或匯入逗號分隔的清單（例如郵寄清單）來整理和新增潛在客戶。 產生銷售機會的其他方法來自電子報註冊或社群註冊（如果設定，這些方法可以觸發工作流程填入銷售機會）。

潛在客戶通常會分類並放入清單中，以便您稍後可以對整個清單執行動作，例如，傳送自訂電子郵件給特定清單。

在[儀表板]中，按一下左窗格中的&#x200B;**銷售機會**，即可存取所有銷售機會。 您也可以從&#x200B;**清單**&#x200B;窗格存取銷售機會。

![screen_shot_2012-02-21at114748am](assets/screen_shot_2012-02-21at114748am.png)

>[!NOTE]
>
>若要新增或修改使用者的頭像，請開啟點按資料流雲端(Ctrl+Alt+c)、載入設定檔，然後按一下&#x200B;**編輯**。

### 建立新的銷售機會 {#creating-new-leads}

建立新的銷售機會後，請務必[啟用銷售機會](#activating-or-deactivating-leads)，以便您可以追蹤他們在發佈執行個體上的活動，並個人化他們的體驗。

若要手動建立銷售機會，請執行下列步驟：

1. 在AEM中，導覽至MCM。 在儀表板中，按一下&#x200B;**銷售機會**。
1. 按一下&#x200B;**新增**。 **建立新**&#x200B;視窗隨即開啟。

   ![screen_shot_2012-02-21at115008am](assets/screen_shot_2012-02-21at115008am.png)

1. 視情況在欄位中輸入資訊。 按一下「**位址**」標籤。

   ![screen_shot_2012-02-21at115045am](assets/screen_shot_2012-02-21at115045am.png)

1. 視需要輸入地址資訊。 按一下[儲存]儲存潛在客戶。 ****&#x200B;如果您需要新增其他銷售機會，請按一下[儲存並新增]。****

   新潛在客戶會出現在「潛在客戶」窗格中。 當您按一下專案時，所有輸入的資訊都會顯示在右窗格中。 建立銷售機會後，您可以將其新增至清單。

   ![screen_shot_2012-02-21at120307pm](assets/screen_shot_2012-02-21at120307pm.png)

### 啟用或停用銷售機會 {#activating-or-deactivating-leads}

啟用銷售機會有助於您追蹤其在發佈例項上的活動，並讓您個人化其體驗。 當您不再想要追蹤其活動時，可以將其停用。

若要使用中或停用潛在客戶：

1. 在AEM中，導覽至MCM並按一下&#x200B;**銷售機會**。

1. 選取您要啟動或停用的潛在客戶，然後按一下[啟動] ****&#x200B;或[停用] ****。

   ![screen_shot_2012-02-21at120620pm](assets/screen_shot_2012-02-21at120620pm.png)

   與AEM頁面一樣，發佈狀態會顯示在&#x200B;**已發佈**&#x200B;欄。

   ![screen_shot_2012-02-21at122901pm](assets/screen_shot_2012-02-21at122901pm.png)

### 匯入新的銷售機會 {#importing-new-leads}

當您匯入新的銷售機會時，您可以自動將其新增到現有清單或建立清單以包含這些銷售機會。

若要從逗號分隔的清單匯入銷售機會：

1. 在AEM中，導覽至MCM並按一下&#x200B;**銷售機會**。

   >[!NOTE]
   >
   >或者，您可以執行下列其中一項作業來匯入銷售機會：
   >
   >* 在儀表板中，按一下&#x200B;**清單**&#x200B;窗格中的&#x200B;**匯入銷售機會**
   >* 按一下「**清單**」，然後在「**工具**」功能表中選取「**匯入銷售機會**」。

1. 在&#x200B;**工具**&#x200B;功能表中，選取&#x200B;**匯入** **銷售機會**。

1. 依照範例資料中的說明輸入資訊。 可以匯入下列欄位：email，familyName，givenName，gender，aboutMe，city，country，phoneNumber，postalCode，region，streetAddress

   >[!NOTE]
   >
   >CSV清單中的第一列是預先定義的標籤，必須完全依照範例來撰寫：
   >
   >
   >`email,givenName,familyName` — 例如，如果寫成`givenname`，系統將無法識別它。
   >
   >

   ![screen_shot_2012-02-21at123055pm](assets/screen_shot_2012-02-21at123055pm.png)

1. 按一下「**下一步**」。您可在此預覽銷售機會，以確保其正確性。

   ![screen_shot_2012-02-21at123104pm](assets/screen_shot_2012-02-21at123104pm.png)

1. 按一下「**下一步**」。選取您要銷售機會所屬的清單。 如果您不希望它們屬於清單，請刪除欄位中的資訊。 依預設，AEM會建立包含日期和時間的清單名稱。 按一下&#x200B;**匯入**。

   ![screen_shot_2012-02-21at123123pm](assets/screen_shot_2012-02-21at123123pm.png)

   新潛在客戶會出現在「潛在客戶」窗格中。 如果按一下專案，所有輸入的資訊都會顯示在右窗格中。 建立銷售機會後，您可以將其新增至清單。

### 將銷售機會新增至清單 {#adding-leads-to-lists}

若要將潛在客戶新增至預先存在的清單：

1. 在MCM中，按一下&#x200B;**銷售機會**&#x200B;以檢視所有可用的銷售機會。

1. 選取要新增至清單的銷售機會，方法是選取該銷售機會旁邊的核取方塊。 您可以新增任意數量的銷售機會。

   ![screen_shot_2012-02-21at123835pm](assets/screen_shot_2012-02-21at123835pm.png)

1. 在&#x200B;**工具**&#x200B;功能表中，選取&#x200B;**新增至清單....** **新增至清單**&#x200B;視窗開啟。

   ![screen_shot_2012-02-21at124019pm](assets/screen_shot_2012-02-21at124019pm.png)

1. 選取您要新增銷售機會的清單，然後按一下[確定]。**** 潛在客戶會新增至適當的清單中。

### 檢視潛在客戶資訊 {#viewing-lead-information}

若要檢視銷售機會資訊，請在MCM中按一下銷售機會旁邊的核取方塊，然後開啟一個右窗格，其中會顯示所有銷售機會資訊，包括清單關聯。

![screen_shot_2012-02-21at124228pm](assets/screen_shot_2012-02-21at124228pm.png)

### 修改現有的銷售機會 {#modifying-existing-leads}

若要修改現有潛在客戶資訊，請執行下列步驟：

1. 在MCM中，按一下&#x200B;**銷售機會**。 從銷售機會清單中，選取您要編輯的銷售機會旁邊的核取方塊。 所有潛在客戶資訊都會顯示在右窗格中。

   ![screen_shot_2012-02-21at124514pm](assets/screen_shot_2012-02-21at124514pm.png)

   >[!NOTE]
   >
   >您一次只能編輯一個銷售機會。 如果您需要修改屬於相同清單的銷售機會，您可以改為修改清單。

1. 按一下&#x200B;**編輯**。 **編輯銷售機會**&#x200B;視窗隨即開啟。

   ![screen_shot_2012-02-21at124609pm](assets/screen_shot_2012-02-21at124609pm.png)

1. 視需要進行編輯，然後按一下[儲存] ****&#x200B;儲存變更。

   >[!NOTE]
   >
   >若要變更銷售機會頭像，請前往使用者設定檔。 您可以按CTRL+ALT+c，按一下&#x200B;**載入**，然後選取設定檔，以載入點按資料流雲端中的設定檔。

### 刪除現有銷售機會 {#deleting-existing-leads}

若要刪除MCM中現有的銷售機會，請選取銷售機會旁邊的核取方塊，然後按一下&#x200B;**刪除**。 潛在客戶會從潛在客戶清單及所有相關清單中移除。

>[!NOTE]
>
>刪除前，AEM會確認您要刪除現有的銷售機會。 刪除後即無法擷取。

## 使用清單 {#working-with-lists}

>[!NOTE]
>
>Adobe不打算進一步增強此功能（管理清單）。
>建議使用[Adobe Campaign以及與AEM](/help/sites-administering/campaign.md)的整合。

清單可讓您將銷售機會整理到群組中。 透過清單，您可以將行銷活動目標定位為特定一群人員，例如，您可以傳送目標定位電子報至清單。 清單可在MCM中顯示，可在控制面板中或按一下&#x200B;**清單**。 兩者都會提供清單的名稱和成員數目。

![screen_shot_2012-02-21at125021pm](assets/screen_shot_2012-02-21at125021pm.png)

如果按一下&#x200B;**清單**，您也可以檢視清單是否為其他清單的成員並檢視說明。

![screen_shot_2012-02-21at124828pm](assets/screen_shot_2012-02-21at124828pm.png)

### 建立新清單 {#creating-new-lists}

1. 在MCM儀表板中，按一下&#x200B;**新增清單……**，或在&#x200B;**清單**&#x200B;中，按一下&#x200B;**新增** ...「建立清單」視窗隨即開啟。

   ![screen_shot_2012-02-21at125147pm](assets/screen_shot_2012-02-21at125147pm.png)

1. 輸入名稱（必要），如有需要，按一下[儲存]。**** 清單會顯示在&#x200B;**清單**&#x200B;窗格中。

   ![screen_shot_2012-02-21at125320pm](assets/screen_shot_2012-02-21at125320pm.png)

### 修改現有清單 {#modifying-existing-lists}

1. 在MCM中，按一下&#x200B;**清單**。

1. 從清單中，選取您要編輯的清單旁邊的核取方塊，然後按一下&#x200B;**編輯**。 **編輯清單**&#x200B;視窗隨即開啟。

   ![screen_shot_2012-02-21at125452pm](assets/screen_shot_2012-02-21at125452pm.png)

   >[!NOTE]
   >
   >您一次只能編輯一個清單。

1. 視需要進行編輯，然後按一下[儲存] **以儲存變更。**

### 刪除現有清單 {#deleting-existing-lists}

若要刪除現有清單，請在MCM中選取清單旁的核取方塊，然後按一下&#x200B;**刪除**。 清單即會移除。 不會移除與清單關聯的潛在客戶 — 只會刪除與清單關聯的潛在客戶。

>[!NOTE]
>
>刪除前，AEM會確認您要刪除現有清單。 刪除後即無法擷取。

### 合併清單 {#merging-lists}

您可以將現有清單與其他清單合併。 執行此操作時，要合併的清單會成為另一個清單的成員。 它仍以獨立實體存在，不應刪除。

如果您在兩個不同位置有相同的會議，並且想要將它們合併到所有會議的出席者清單中，則可以合併清單。

若要合併現有清單，請執行下列動作：

1. 在MCM中，按一下&#x200B;**清單**。

1. 選取清單旁邊的核取方塊，以選取要合併其他清單的清單。

1. 在&#x200B;**工具**&#x200B;功能表中，選取&#x200B;**合併清單**。

   >[!NOTE]
   >
   >您一次只能合併一個清單。

1. 在&#x200B;**合併清單**&#x200B;視窗中，選取您要合併的清單，然後按一下&#x200B;**確定**。

   ![screen_shot_2012-02-21at10259pm](assets/screen_shot_2012-02-21at10259pm.png)

   您合併的清單應該會增加一個成員。 若要檢視您的清單是否已合併，請選取您合併的清單，並在&#x200B;**工具**&#x200B;功能表中選取&#x200B;**顯示銷售機會**。

1. 重複此步驟，直到合併所有想要的清單為止。

   ![screen_shot_2012-02-21at10538pm](assets/screen_shot_2012-02-21at10538pm.png)

>[!NOTE]
>
>從合併清單的成員資格中移除與從清單中移除潛在客戶相同。 開啟&#x200B;**清單**&#x200B;標籤，選取包含合併清單的清單，然後按一下清單旁的紅色圓圈來移除成員資格。

### 檢視清單中的銷售機會 {#viewing-leads-in-lists}

您可以隨時透過瀏覽或搜尋成員來檢視哪些潛在客戶屬於特定清單。

若要檢視清單中的銷售機會，請執行下列步驟：

1. 在MCM中，按一下&#x200B;**清單**。

1. 選取您要檢視其成員的清單旁的核取方塊。

1. 在&#x200B;**工具**&#x200B;功能表中，選取&#x200B;**顯示銷售機會**。 AEM會顯示屬於該清單成員的潛在客戶。 您可以瀏覽清單或搜尋成員。

   >[!NOTE]
   >
   >此外，您可以從清單中刪除銷售機會，方法是選取銷售機會，然後按一下&#x200B;**移除成員資格**。

   ![screen_shot_2012-02-21at10828pm](assets/screen_shot_2012-02-21at10828pm.png)

1. 按一下&#x200B;**關閉**&#x200B;以返回MCM。
