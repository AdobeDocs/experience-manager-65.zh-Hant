---
title: 瞄準你的Adobe Campaign
description: 設定細分包括建立細分、品牌、活動和體驗。
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

# 瞄準你的Adobe Campaign{#targeting-your-adobe-campaign}

要針對您的Adobe Campaign通訊，您需要首先設定分段，該分段僅在經典用戶介面中提供。 之後，你就可以為Adobe Campaign創造有針對性的體驗。

## 在中設定分AEM段 {#setting-up-segmentation-in-aem}

設定細分包括建立細分、品牌、活動和體驗。 您只能在經典UI中建立段。 您可以在啟用觸摸的UI中建立品牌、市場活動和體驗。

>[!NOTE]
>
>段ID需要映射到Adobe Campaign一側的段ID。

### 建立段 {#creating-segments}

要建立段：

1. 開啟 [分段控制台](http://localhost:4502/miscadmin#/etc/segmentation) 在 **&lt;host>:&lt;port>/miscadmin#/etc/segmentation**。
1. 建立新頁面並輸入標題 — 例如， **交流段**  — 並選擇 **段(Adobe Campaign)** 的下界。
1. 在左側的樹視圖中選擇已建立的頁面。
1. 通過在您建立的段（稱為「男性」）下建立新頁面，然後選擇 **段(Adobe Campaign)** 的下界。
1. 開啟建立的段頁，拖放 **段ID** 從旁邊到頁面。
1. 按兩下該特性，輸入表示此情況的ID，即在Adobe Campaign定義的男性段 — 例如， **男性**  — 按一下 **確定**。 應出現以下消息： `targetData.segmentCode == "MALE"`
1. 對另一段重複這些步驟，例如針對女性用戶的段。

### 建立品牌 {#creating-a-brand}

要建立品牌：

1. 在 **站點**，導航至 **市場活動** 資料夾（例如，在We.Retail中）。
1. 按一下 **建立頁** 並輸入頁面標題，例如We.Retail Brand，然後選擇 **品牌** 的下界。

### 建立市場活動 {#creating-a-campaign}

要建立市場活動，請執行以下操作：

1. 開啟 **品牌** 的子菜單。
1. 按一下 **建立頁** 並為頁面輸入標題，例如We.Retail Campaint，然後選擇 **活動** 按一下 **建立**。

### 建立體驗 {#creating-experiences}

要為段建立體驗，請執行以下操作：

1. 開啟 **活動** 的子菜單。
1. 通過按一下 **建立頁** 並為頁面輸入標題，例如，在為「男性」段建立體驗時，「男性」，然後選擇 **經驗** 的下界。
1. 開啟建立的「體驗」頁。
1. 按一下 **編輯**，然後在段下按一下 **添加項**。
1. 輸入公段的路徑，例如 `/etc/segmentation/ac-segments/male` 按一下 **確定**。 應出現以下消息： *經驗的目標是：男性*
1. 重複上述步驟，為所有段建立體驗，例如女性目標。

## 建立具有目標內容的新聞稿 {#creating-a-newsletter-with-targeted-content}

在您建立了段、品牌、活動和體驗後，您可以建立具有目標內容的新聞稿。 建立體驗後，您將體驗連結到您的細分市場。

您可以在支援觸摸的用戶介面和傳統用戶介面中建立具有目標內容的新聞稿。 本文檔介紹啟用觸摸的UI的過程。

要建立具有目標內容的新聞稿，請執行以下操作：

1. 建立具有目標內容的新聞稿：在Geometrixx Outdoors中的電子郵件市場活動下，按一下或點擊 **建立** > **頁面**，然後選擇一個Adobe Campaign郵件模板。

   >[!NOTE]
   >
   >[電子郵件示例僅在Geometrixx中提供](/help/sites-developing/we-retail.md#weretail)。 請從包共用下載示例Geometrixx內容。

1. 在新聞稿中，添加文本和個性化元件。
1. 將文本添加到文本和個性化元件中，如「這是預設值」。
1. 按一下旁邊的箭頭 **編輯** 選擇 **目標**。
1. 從「品牌」下拉菜單中選擇您的品牌，然後選擇您的「市場活動」。 （這是您之前建立的品牌和市場活動）。
1. 按一下 **開始目標**。 您會看到您的段出現在「受眾」區域。 如果定義的段均不匹配，則使用預設體驗。

   >[!NOTE]
   >
   >預設情況下，包含的電子郵件示例AEM使用Adobe Campaign作為目標引擎。 對於自定義新聞稿，您可能需要選擇Adobe Campaign作為目標引擎。 當瞄準時，點擊或按一下工具欄中的+，輸入新活動的標題，然後選擇 **Adobe Campaign** 作為目標引擎。

1. 按一下 **預設** 然後是您添加的「文本和個性化」元件，您會看到帶有箭頭的「牛眼」。 按一下該表徵圖以瞄準此元件。

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. 導航到另一段（公），然後按一下 **添加優惠** 並按一下加號表徵圖+。 然後編輯優惠。
1. 導航到另一段（母），然後按一下 **添加優惠** 和加號表徵圖。 然後編輯此優惠。
1. 按一下 **下一個** 查看映射，然後按一下 **下一個** 查看不適用於Adobe Campaign的設定，然後按一下 **保存**。

   當內AEM容在Adobe Campaign內的交付中使用時，自動為Adobe Campaign生成正確的目標代碼

1. 在Adobe Campaign，建立交貨 — 選擇 **包含內容的電子郵AEM件傳遞** 並選擇本AEM地帳戶，然後確認更改。

   在HTML看來，Adobe Campaign目標代碼中載有目標元件的不同經驗。

   ![chlimage_1-166](assets/chlimage_1-166.png)

   >[!NOTE]
   >
   >如果還在Adobe Campaign設定段，請按一下 **預覽** 將向您展示每段的體驗。
