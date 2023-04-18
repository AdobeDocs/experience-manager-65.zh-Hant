---
title: 定位您的Adobe Campaign
description: 設定細分包括建立區段、品牌、行銷活動和體驗。
uuid: 520cd006-0aa8-43f3-b754-efb7397bb92f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: bbc2aac9-ccf1-40c3-be4f-d59c2d0d8a6c
exl-id: e56986b2-397e-4802-992b-05a9ea7b2e36
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 0%

---

# 定位您的Adobe Campaign{#targeting-your-adobe-campaign}

若要定位Adobe Campaign電子報，您必須先設定區段，這只能在傳統UI中使用。 之後，您就可以為Adobe Campaign建立目標體驗。

## 在AEM中設定區段 {#setting-up-segmentation-in-aem}

設定細分包括建立區段、品牌、行銷活動和體驗。 您只能在傳統UI中建立區段。 您可以在觸控式UI中建立品牌、促銷活動和體驗。

>[!NOTE]
>
>區段ID必須對應至Adobe Campaign端的區段ID。

### 建立區段 {#creating-segments}

若要建立區段：

1. 開啟 [細分控制台](http://localhost:4502/miscadmin#/etc/segmentation) at **&lt;host>:&lt;port>/miscadmin#/etc/segmentation**.
1. 建立新頁面並輸入標題，例如 **AC段**  — 並選取 **區段(Adobe Campaign)** 範本。
1. 在左側的樹視圖中選擇已建立的頁。
1. 在您建立的區段（稱為「男性」）下建立新頁面，並選取「 **區段(Adobe Campaign)** 範本。
1. 開啟已建立的區段頁面，並拖放 **區段ID** 從sidekick上傳到頁面。
1. 連按兩下特徵，輸入代表此例中的ID，即Adobe Campaign中定義的男性區段，例如 **男性**  — 按一下 **確定**. 應會顯示下列訊息： `targetData.segmentCode == "MALE"`
1. 對其他區段重複這些步驟，例如以女性使用者為目標的區段。

### 建立品牌 {#creating-a-brand}

建立品牌：

1. 在 **網站**，導覽至 **行銷活動** 資料夾（例如在We.Retail中）。
1. 按一下 **建立頁面** 並輸入頁面標題，例如We.Retail Brand ，然後選取 **品牌** 範本。

### 建立行銷活動 {#creating-a-campaign}

若要建立促銷活動：

1. 開啟 **品牌** 頁面。
1. 按一下 **建立頁面** 並輸入頁面標題，例如We.Retail促銷活動，然後選取 **行銷活動** 範本，按一下 **建立**.

### 建立體驗 {#creating-experiences}

若要建立區段的體驗：

1. 開啟 **行銷活動** 頁面。
1. 按一下 **建立頁面** 並輸入頁面標題，例如，當您為「男性」區段建立體驗時，「男性」，然後選取 **體驗** 範本。
1. 開啟已建立的體驗頁面。
1. 按一下 **編輯**，然後在區段下方按一下 **新增項目**.
1. 輸入男性區段的路徑，例如 `/etc/segmentation/ac-segments/male` 按一下 **確定**. 應會顯示下列訊息： *體驗鎖定在：男性*
1. 重複上述步驟，為所有區段（例如女性目標）建立體驗。

## 使用目標內容建立電子報 {#creating-a-newsletter-with-targeted-content}

建立區段、品牌、行銷活動和體驗後，您就可以建立具有目標內容的電子報。 建立體驗後，您會將體驗連結至您的區段。

您可以在觸控式和傳統使用者介面中，使用目標式內容建立電子報。 本檔案說明觸控式UI的程式。

若要建立具有目標內容的電子報：

1. 建立具有目標內容的電子報：在「電子郵件促銷活動」下方的「Geometrixx Outdoors」中，按一下或點選 **建立** > **頁面**，然後選取其中一個Adobe Campaign Mail範本。

   >[!NOTE]
   >
   >[電子郵件範例僅適用於Geometrixx](/help/sites-developing/we-retail.md#weretail). 請從「封裝共用」下載Geometrixx內容範例。

1. 在電子報中，新增文字和個人化元件。
1. 將文字新增至文字和個人化元件，例如「這是預設值」。
1. 按一下旁邊的箭頭 **編輯** 選取 **定位**.
1. 從「品牌」下拉式選單中選取您的品牌，然後選取您的促銷活動。 （這是您先前建立的品牌和行銷活動）。
1. 按一下 **開始鎖定目標**. 您會看到您的區段出現在「對象」區域中。 如果所定義的區段皆不相符，則會使用預設體驗。

   >[!NOTE]
   >
   >依預設，AEM隨附的電子郵件範例會使用Adobe Campaign作為定位引擎。 若為自訂電子報，您可能需要選取Adobe Campaign作為定位引擎。 定位時，點選或按一下工具列中的+，輸入新活動的標題，然後選取 **Adobe Campaign** 作為定位引擎。

1. 按一下 **預設** 然後是您新增的「文字與個人化」元件，您會看到內含箭頭的「牛頭」。 按一下圖示以定位此元件。

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. 導覽至其他區段（男性），然後按一下 **新增選件** 並按一下加號表徵圖+。 然後編輯選件。
1. 導覽至其他區段（女性），然後按一下 **新增選件** 和加號表徵圖+。 然後編輯此選件。
1. 按一下 **下一個** 若要查看對應，請按一下 **下一個** 若要查看不適用於Adobe Campaign的設定，請按一下 **儲存**.

   當內容用於Adobe Campaign內的傳送時，AEM會自動為Adobe Campaign產生正確的定位代碼

1. 在Adobe Campaign中建立您的傳送 — 選取 **包含AEM內容的電子郵件傳送** 並視情況選取本機AEM帳戶，並確認您的變更。

   在HTML檢視中，目標元件的不同體驗會括在Adobe Campaign目標程式碼中。

   ![chlimage_1-166](assets/chlimage_1-166.png)

   >[!NOTE]
   >
   >如果您也在Adobe Campaign中設定區段，請按一下 **預覽** 會顯示每個區段的體驗。
