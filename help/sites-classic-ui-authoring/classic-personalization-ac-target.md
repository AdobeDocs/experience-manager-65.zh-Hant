---
title: 鎖定您的Adobe Campaign
seo-title: 鎖定您的Adobe Campaign
description: 設定區段包括建立區段、品牌、促銷活動和體驗。
seo-description: 設定區段包括建立區段、品牌、促銷活動和體驗。
uuid: 520cd006-0aa8-43f3-b754-efb7397bb92f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: bbc2aac9-ccf1-40c3-be4f-d59c2d0d8a6c
translation-type: tm+mt
source-git-commit: 016c705230dffec052c200b058a36cdbe0520fc4

---


# 鎖定您的Adobe Campaign{#targeting-your-adobe-campaign}

若要鎖定您的Adobe Campaign電子報，您必須先設定區段，這只能在Classic UI中使用。 之後，您就可以建立Adobe Campaign的目標體驗。

## 在AEM中設定區段 {#setting-up-segmentation-in-aem}

設定區段包括建立區段、品牌、促銷活動和體驗。 您只能在傳統UI中建立區段。 您可以在觸控式UI中建立品牌、促銷活動和體驗。

>[!NOTE]
>
>區段ID必須對應至Adobe Campaign方面的區段ID。

### 建立區段 {#creating-segments}

若要建立區段：

1. 在 [&lt;host>](http://localhost:4502/miscadmin#/etc/segmentation) :&lt;port>/miscadmin#/etc/segmentation中開啟分段控制台 ****。
1. 建立新頁面並輸入標題——例如 **AC區段** -並選取 **區段(Adobe Campaign)範本** 。
1. 在樹視圖的左側選擇建立的頁面。
1. 建立區段（例如定位男性使用者），方法是在您所建立的區段下建立新頁面，稱為「男性」，然後選取 **區段(Adobe Campaign)範本** 。
1. 開啟已建立的區段頁面，並從側 **腳拖放區段ID** 至頁面。
1. 連按兩下特徵，輸入此情況下代表的ID，即Adobe Campaign中定義的男性區段——例如 **MALE** —— 然後按一下 **確定**。 應出現以下消息： `targetData.segmentCode == "MALE"`
1. 重複其他區段的步驟，例如針對女性使用者的區段。

### 建立品牌 {#creating-a-brand}

若要建立品牌：

1. 在 **Sites**&#x200B;中，導覽至 **Campaigns** 資料夾（例如在We.Retail中）。
1. 按一 **下「建立頁面** 」，然後輸入頁面的標題，例如We.Retail品牌，然後選取「品 **牌** 」範本。

### 建立促銷活動 {#creating-a-campaign}

若要建立促銷活動：

1. 開啟您 **剛建立** 的品牌頁面。
1. 按一 **下「建立頁面** 」，然後輸入頁面的標題，例如We.Retail促銷活動，然後選取「促銷活動」範本，然後按一下「建立」 ********。

### 建立體驗 {#creating-experiences}

若要建立區段的體驗：

1. 開啟您 **剛建立** 的「促銷活動」頁面。
1. 按一下「建立頁面 **」並輸入頁面標題，以建立區段的體驗，例如，當您為「男性」區段建立體驗時，「男性」，然後選取「** Experience **** 」範本。
1. 開啟建立的「體驗」頁面。
1. 按一 **下編輯**，然後在區段下方按一 **下新增項目**。
1. 例如，輸入公線段的路徑，然後 `/etc/segmentation/ac-segments/male` 按一下 **確定**。 應出現以下消息：體 *驗的目標：男*
1. 重複上述步驟，為所有區段（例如女性目標）建立體驗。

## 建立具有目標內容的電子報 {#creating-a-newsletter-with-targeted-content}

在您建立區段、品牌、促銷活動和體驗後，就可以建立具有目標內容的電子報。 建立體驗後，您會將體驗連結至您的區段。

您可以在觸控式和傳統使用者介面中，建立包含目標內容的電子報。 本檔案說明啟用觸控的UI的程式。

若要建立包含目標內容的電子報：

1. 建立包含目標內容的電子報：在Geometrixx Outdoors的「電子郵件促銷活動」下方，按一下或點選「 **建立** > **頁面**」，然後選取其中一個Adobe Campaign mail範本。

   >[!NOTE]
   >
   >[電子郵件範例僅在Geometrixx中提供](/help/sites-developing/we-retail.md#weretail)。 請從Package Share下載範例Geometrixx內容。

1. 在電子報中，新增文字和個人化元件。
1. 將文字新增至「文字與個人化」元件，例如「這是預設值」。
1. 按一下「編輯」旁的箭 **頭** ，然後選 **取「定位」**。
1. 從「品牌」下拉式選單中選取您的品牌，然後選取您的促銷活動。 （這是您先前建立的品牌和促銷活動）。
1. 按一下 **開始定位**。 您會看到您的區段出現在「對象」區域。 如果定義的區段不符合，則會使用預設體驗。

   >[!NOTE]
   >
   >依預設，AEM隨附的電子郵件範例會使用Adobe Campaign做為定位引擎。 若是自訂電子報，您可能需要選擇Adobe Campaign作為定位引擎。 定位時，點選或按一下工具列中的+，輸入新活動的標題，並選取 **Adobe Campaign** 作為定位引擎。

1. 按一 **下「預設** 」，然後按一下您新增的「文字與個人化」元件，您就會看到Bullseye中有一個箭頭。 按一下圖示以定位此元件。

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. 導覽至另一個區段（男性），然後按一下「 **新增選件** 」，然後按一下加號圖示+。 然後編輯選件。
1. 導覽至另一個區段（女性），然後按一 **下「新增選件** 」和加號圖示+。 然後編輯此選件。
1. 按一 **下** 「下一步」以查看「對應」，然後按一下「下一步 **」以查看「設定」，此設定不適用於Adobe Campaign，然後按一下「** 儲存」 ****。

   當內容用於Adobe Campaign內的傳送時，AEM會自動產生Adobe Campaign的正確定位代碼

1. 在Adobe Campaign中，建立您的傳送——選取「 **Email delivery with AEM content** 」（含AEM內容的電子郵件傳送），並視需要選取本機AEM帳戶，然後確認您所做的變更。

   在HTML檢視中，Adobe Campaign定位程式碼會包含目標元件的不同體驗。

   ![chlimage_1-166](assets/chlimage_1-166.png)

   >[!NOTE]
   >
   >如果您也在Adobe Campaign中設定群體，按一下「預 **覽** 」將顯示每個群體的體驗。

