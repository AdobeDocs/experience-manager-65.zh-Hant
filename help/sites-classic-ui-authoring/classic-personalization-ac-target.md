---
title: 鎖定您的Adobe Campaign
description: 設定細分包括建立區段、品牌、行銷活動和體驗。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: e56986b2-397e-4802-992b-05a9ea7b2e36
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 0%

---

# 鎖定您的Adobe Campaign{#targeting-your-adobe-campaign}

若要鎖定您的Adobe Campaign電子報，您必須先設定分段，而這僅適用於傳統UI。 之後，您可以為Adobe Campaign建立鎖定目標的體驗。

## 在AEM中設定分段 {#setting-up-segmentation-in-aem}

設定細分包括建立區段、品牌、行銷活動和體驗。 您只能在傳統UI中建立區段。 您可以在觸控式UI中建立品牌、行銷活動和體驗。

>[!NOTE]
>
>區段ID必須對應至Adobe Campaign端的ID。

### 建立區段 {#creating-segments}

若要建立區段：

1. 開啟 [分段主控台](http://localhost:4502/miscadmin#/etc/segmentation) 在 **&lt;host>：&lt;port>/miscadmin#/etc/segment**.
1. 建立頁面並輸入標題 — 例如 **AC區段**  — 並選取 **區段(Adobe Campaign)** 範本。
1. 在左側的樹狀檢視中選取建立的頁面。
1. 建立區段，例如，將目標定位為男性使用者，方法是在您建立的區段下建立一個名為「男性」的頁面，然後選取 **區段(Adobe Campaign)** 範本。
1. 開啟已建立的區段頁面，並拖放 **區段ID** 從sidekick到頁面。
1. 連按兩下特徵，輸入ID，在此案例中代表Adobe Campaign中定義的男性區段 — 例如， **男性**  — 並按一下 **確定**. 下列訊息應會顯示出來： `targetData.segmentCode == "MALE"`
1. 對另一個區段重複這些步驟，例如以女性使用者為目標的區段。

### 建立品牌 {#creating-a-brand}

若要建立品牌：

1. 在 **網站**，導覽至 **行銷活動** 資料夾（例如We.Retail中的）。
1. 按一下 **建立頁面** 並輸入頁面標題，例如We.Retail Brand ，然後選取 **品牌** 範本。

### 建立行銷活動 {#creating-a-campaign}

若要建立行銷活動：

1. 開啟 **品牌** 您已建立的頁面。
1. 按一下 **建立頁面** 並輸入頁面的標題，例如We.Retail Campaign，然後選取 **Campaign** 範本並按一下 **建立**.

### 建立體驗 {#creating-experiences}

若要建立區段的體驗：

1. 開啟 **Campaign** 您已建立的頁面。
1. 按一下「 」，為您的區段建立體驗 **建立頁面** 並輸入頁面的標題，例如，當您為男性區段建立體驗時，請選取 **體驗** 範本。
1. 開啟已建立的體驗頁面。
1. 按一下 **編輯**，然後按一下「區段」下方的 **新增專案**.
1. 輸入男性區段的路徑，例如， `/etc/segmentation/ac-segments/male` 並按一下 **確定**. 下列訊息應會顯示出來： *體驗鎖定目標：男性*
1. 重複上述步驟以建立所有區段的體驗，例如女性目標。

## 建立具有目標內容的新聞稿 {#creating-a-newsletter-with-targeted-content}

建立區段、品牌、行銷活動和體驗後，您可以建立具有目標內容的新聞稿。 建立體驗後，您可以將體驗連結至區段。

您可以在已啟用觸控功能的使用者介面和傳統使用者介面中，建立具有目標內容的Newsletter。 本檔案說明觸控式UI的程式。

若要建立具有目標內容的Newsletter：

1. 建立具有目標內容的新聞稿：在Geometrixx Outdoors中的電子郵件行銷活動下方，按一下或點選 **建立** > **頁面**，並選取其中一個Adobe Campaign郵件範本。

   >[!NOTE]
   >
   >[電子郵件範例僅適用於Geometrixx](/help/sites-developing/we-retail.md#weretail). 從封裝共用下載範例Geometrixx內容。

1. 在Newsletter中，新增文字和個人化元件。
1. 將文字新增至「文字與個人化」元件，例如「此為預設值」。
1. 按一下旁邊的箭頭 **編輯** 並選取 **目標定位**.
1. 從「品牌」下拉式選單中選取您的品牌，然後選取您的行銷活動。 （這是您先前建立的品牌和促銷活動）。
1. 按一下 **開始定位**. 您會看到您的區段出現在「對象」區域中。 如果沒有相符的已定義區段，則會使用預設體驗。

   >[!NOTE]
   >
   >依預設，AEM隨附的電子郵件範例會使用Adobe Campaign作為目標定位引擎。 針對自訂電子報，您可能需要選取Adobe Campaign作為定位引擎。 鎖定目標時，點選或按一下工具列中的「+」，輸入新活動的標題，然後選取 **Adobe Campaign** 作為目標定位引擎。

1. 按一下 **預設** 然後是您新增的文字與個人化元件，您會看到裡面有箭頭的靶心。 按一下圖示以鎖定此元件。

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. 導覽至另一個區段（男性），然後按一下 **新增選件** 並按一下加號圖示+。 然後編輯選件。
1. 導覽至另一個區段（女性）並按一下 **新增選件** 和加號圖示+。 然後編輯此選件。
1. 按一下 **下一個** 若要檢視對應，請按一下 **下一個** 若要檢視不適用於Adobe Campaign的設定，請按一下 **儲存**.

   當內容在Adobe Campaign內的傳遞中使用時，AEM會自動產生適用於Adobe Campaign的正確目標定位代碼

1. 在Adobe Campaign中建立您的傳遞 — 選取 **包含AEM內容的電子郵件傳遞** 並視情況選取本機AEM帳戶，確認變更。

   在HTML檢視中，目標元件的不同體驗會包含在Adobe Campaign目標定位程式碼中。

   ![chlimage_1-166](assets/chlimage_1-166.png)

   >[!NOTE]
   >
   >如果您也在Adobe Campaign中設定區段，請按一下 **預覽** 將顯示每個區段的體驗。
