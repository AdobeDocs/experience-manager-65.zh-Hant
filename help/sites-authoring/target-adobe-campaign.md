---
title: 定位您的Adobe Campaign
seo-title: 定位您的Adobe Campaign
description: 您可以在設定細分後，為Adobe Campaign建立目標體驗
seo-description: 您可以在設定細分後，為Adobe Campaign建立目標體驗
uuid: 8fcc9210-d8c5-44e3-8aa8-6c6db810c98e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: f1cb5e98-ccd1-4b2c-acca-2b3cc1b7ac5f
exl-id: fc6fccba-41c5-4c13-aac0-b4ef67767abe
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 0%

---

# 定位您的Adobe Campaign{#targeting-your-adobe-campaign}

若要鎖定Adobe Campaign電子報，您必須先設定區段，此區段僅適用於傳統UI（適用於用戶端內容）。 之後，您就可以為Adobe Campaign建立目標體驗。 本節將對兩者進行說明。

## 在AEM {#setting-up-segmentation-in-aem}中設定分段

若要設定區段，您必須使用傳統UI來設定區段。 其餘步驟可在標準UI中執行。

設定細分包括建立區段、品牌、行銷活動和體驗。

>[!NOTE]
>
>區段ID必須對應至Adobe Campaign端的區段ID。

### 建立區段{#creating-segments}

若要建立區段：

1. 在&#x200B;**&lt;host>開啟[分段控制台](http://localhost:4502/miscadmin#/etc/segmentation):&lt;port>/miscadmin#/etc/segmentation**。
1. 建立新頁面並輸入標題 — 例如&#x200B;**AC區段** — 並選取&#x200B;**區段(Adobe Campaign)**&#x200B;範本。
1. 在左側的樹視圖中選擇已建立的頁。
1. 建立區段，例如鎖定男性使用者，方法是在您建立的區段下建立新頁面，稱為「男性」，然後選取&#x200B;**區段(Adobe Campaign)**&#x200B;範本。
1. 開啟已建立的區段頁面，並將&#x200B;**區段ID**&#x200B;從sidekick拖放至頁面。
1. 連按兩下特徵，輸入代表此例中的男性區段（例如&#x200B;**MALE**）的ID，然後按一下&#x200B;**OK**。 應會顯示下列訊息：*`targetData.segmentCode == "MALE"`*
1. 對其他區段重複這些步驟，例如以女性使用者為目標的區段。

### 建立品牌{#creating-a-brand}

建立品牌：

1. 在&#x200B;**Sites**&#x200B;中，導覽至&#x200B;**Campaigns**&#x200B;資料夾（例如在We.Retail中）。
1. 按一下「**建立頁面**」並輸入頁面標題，例如We.Retail Brand，然後選取&#x200B;**Brand**&#x200B;範本。

### 建立促銷活動{#creating-a-campaign}

若要建立促銷活動：

1. 開啟您剛建立的&#x200B;**Brand**&#x200B;頁面。
1. 按一下「**建立頁面**」並輸入頁面標題，例如We.Retail促銷活動，然後選取&#x200B;**促銷活動**&#x200B;範本，然後按一下「**建立**」。

### 建立體驗{#creating-experiences}

若要建立區段的體驗：

1. 開啟您剛建立的&#x200B;**Campaign**&#x200B;頁面。
1. 按一下&#x200B;**建立頁面**&#x200B;並輸入頁面標題，例如當您為男性區段建立體驗時為男性，並選取&#x200B;**體驗**&#x200B;範本，以建立區段的體驗。
1. 開啟已建立的體驗頁面。
1. 按一下「**編輯**」，然後在「區段」下方按一下「**新增項目**」。
1. 輸入公線段的路徑，例如&#x200B;**/etc/segmentation/ac-segments/male**，然後按一下&#x200B;**OK**。 應會顯示下列訊息：*體驗鎖定在：男性*
1. 重複上述步驟，為所有區段（例如女性目標）建立體驗。

## 使用目標內容{#creating-a-newsletter-with-targeted-content}建立電子報

建立區段、品牌、行銷活動和體驗後，您就可以建立具有目標內容的電子報。 建立體驗後，您會將體驗連結至您的區段。

>[!NOTE]
>
>[電子郵件範例僅適用於Geometrixx](/help/sites-developing/we-retail.md)。請從「封裝共用」下載Geometrixx內容範例。

若要建立具有目標內容的電子報：

1. 建立具有目標內容的電子報：在「電子郵件促銷Geometrixx Outdoors」下方，按一下或點選「**建立** > **頁面**」，然後選取其中一個「Adobe Campaign郵件」範本。

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. 在電子報中，新增文字和個人化元件。
1. 將文字新增至文字和個人化元件，例如「這是預設值」。
1. 按一下&#x200B;**Edit**&#x200B;旁的箭頭，然後選擇&#x200B;**Targeting**。
1. 從「品牌」下拉式選單中選取您的品牌，然後選取您的促銷活動。 （這是您先前建立的品牌和行銷活動）。
1. 按一下&#x200B;**開始鎖定目標**。 您會看到您的區段出現在「對象」區域中。 如果所定義的區段皆不相符，則會使用預設體驗。

   >[!NOTE]
   >
   >依預設，AEM隨附的電子郵件範例會使用Adobe Campaign作為定位引擎。 若為自訂電子報，您可能需要選取Adobe Campaign作為定位引擎。 定位時，點選或按一下工具列中的+，輸入新活動的標題，然後選取&#x200B;**Adobe Campaign**&#x200B;作為定位引擎。

1. 按一下「**預設**」，然後按一下您新增的「文字」和「個人化」元件，您會看到內含箭頭的「牛頭」。 按一下圖示以定位此元件。

   ![chlimage_1-109](assets/chlimage_1-189.png)

1. 導覽至其他區段（男性），然後按一下&#x200B;**新增選件**，然後按一下加號圖示+。 然後編輯選件。
1. 導覽至其他區段（女性），然後按一下&#x200B;**新增選件**&#x200B;和加號圖示+。 然後編輯此選件。
1. 按一下「**Next**」查看「映射」，然後按一下「**Next**」查看不適用於Adobe Campaign的「設定」，然後按一下「**Save**」。

   當內容用於Adobe Campaign內的傳送時，AEM會自動為Adobe Campaign產生正確的定位代碼

1. 在Adobe Campaign中，建立您的傳送 — 選取&#x200B;**包含AEM內容的電子郵件傳送**，並視情況選取本機AEM帳戶並確認您的變更。

   在HTML檢視中，目標元件的不同體驗會括在Adobe Campaign鎖定目標程式碼中。

   ![chlimage_1-190](assets/chlimage_1-190.png)

   >[!NOTE]
   >
   >如果您也在Adobe Campaign中設定區段，按一下&#x200B;**預覽**&#x200B;將顯示每個區段的體驗。
