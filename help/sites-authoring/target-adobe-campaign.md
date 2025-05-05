---
title: 鎖定Adobe Campaign
description: 設定細分後，您可以為Adobe Campaign建立鎖定目標的體驗。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
exl-id: fc6fccba-41c5-4c13-aac0-b4ef67767abe
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization,Integration
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 0%

---

# 鎖定您的Adobe Campaign{#targeting-your-adobe-campaign}

若要鎖定您的Adobe Campaign電子報，您必須先設定分段，而這僅適用於傳統UI （適用於使用者端內容）。 之後，您可以建立Adobe Campaign的鎖定目標體驗。 本節將說明這兩種方式。

## 在AEM中設定分段 {#setting-up-segmentation-in-aem}

若要設定區段，您必須使用傳統UI來設定區段。 其餘步驟可以在標準UI中執行。

設定細分包括建立區段、品牌、行銷活動和體驗。

>[!NOTE]
>
>區段ID必須對應至Adobe Campaign端的ID。

### 建立區段 {#creating-segments}

若要建立區段：

1. 在&#x200B;**&lt;host>：&lt;port>/miscadmin#/etc/segmentation**&#x200B;開啟[分段主控台](http://localhost:4502/miscadmin#/etc/segmentation)。
1. 建立頁面並輸入標題 — 例如&#x200B;**AC區段** — 並選取&#x200B;**區段(Adobe Campaign)**&#x200B;範本。
1. 在左側的樹狀檢視中選取建立的頁面。
1. 建立區段，例如，將目標定位為男性使用者，方法是在您建立的名為「男性」的區段下建立頁面，並選取&#x200B;**區段(Adobe Campaign)**&#x200B;範本。
1. 開啟已建立的區段頁面，並將&#x200B;**區段ID**&#x200B;從Sidekick拖放到頁面上。
1. 按兩下特徵，輸入代表在此案例中定義在Adobe Campaign中的男性區段（例如，**MALE**）的ID，然後按一下&#x200B;**確定**。 應該會顯示下列訊息： *`targetData.segmentCode == "MALE"`*
1. 對另一個區段重複這些步驟，例如以女性使用者為目標的區段。

### 建立品牌 {#creating-a-brand}

若要建立品牌：

1. 在&#x200B;**Sites**&#x200B;中，導覽至&#x200B;**Campaigns**&#x200B;資料夾（例如We.Retail中的）。
1. 按一下&#x200B;**建立頁面**&#x200B;並輸入頁面的標題，例如We.Retail品牌，然後選取&#x200B;**品牌**&#x200B;範本。

### 建立行銷活動 {#creating-a-campaign}

若要建立行銷活動：

1. 開啟您建立的&#x200B;**品牌**&#x200B;頁面。
1. 按一下&#x200B;**建立頁面**&#x200B;並輸入頁面的標題，例如We.Retail行銷活動，然後選取&#x200B;**行銷活動**&#x200B;範本並按一下&#x200B;**建立**。

### 建立體驗 {#creating-experiences}

若要建立區段的體驗：

1. 開啟您建立的&#x200B;**促銷活動**&#x200B;頁面。
1. 按一下「**建立頁面**」並輸入頁面的標題（例如，「男性」）來建立您區段的體驗，然後選取「**體驗**」範本。
1. 開啟已建立的體驗頁面。
1. 按一下[編輯]&#x200B;**&#x200B;**，然後在[區段]下方按一下[新增專案]&#x200B;**&#x200B;**。
1. 輸入男性區段的路徑，例如&#x200B;**/etc/segmentation/ac-segments/male**，然後按一下&#x200B;**確定**。 應該會出現下列訊息： *體驗目標為：男性*
1. 重複上述步驟以建立所有區段的體驗，例如女性目標。

## 建立具有目標內容的新聞稿 {#creating-a-newsletter-with-targeted-content}

建立區段、品牌、行銷活動和體驗後，您可以建立具有目標內容的新聞稿。 建立體驗後，您可以將體驗連結至區段。

>[!NOTE]
>
>[電子郵件範例僅適用於Geometrixx](/help/sites-developing/we-retail.md)。 從封裝共用下載範例Geometrixx內容。

若要建立具有目標內容的Newsletter：

1. 建立具有目標內容的Newsletter：在Geometrixx Outdoors的電子郵件行銷活動底下，按一下「**建立** > **頁面**」，然後選取其中一個Adobe Campaign郵件範本。

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. 在Newsletter中新增文字和Personalization元件。
1. 將文字新增至文字和Personalization元件，例如「此為預設值」。
1. 按一下&#x200B;**編輯**&#x200B;旁的箭頭，然後選取&#x200B;**鎖定目標**。
1. 從「品牌」下拉式選單中選取您的品牌，然後選取您的行銷活動。 （這是您先前建立的品牌和促銷活動）。
1. 按一下&#x200B;**開始鎖定目標**。 您會看到您的區段出現在「對象」區域中。 如果沒有相符的已定義區段，則會使用預設體驗。

   >[!NOTE]
   >
   >依預設，AEM隨附的電子郵件範例會使用Adobe Campaign作為目標定位引擎。 針對自訂電子報，您可能需要選取Adobe Campaign作為定位引擎。 鎖定目標時，請按一下工具列中的+ ，輸入新活動的標題，然後選取&#x200B;**Adobe Campaign**&#x200B;作為鎖定目標引擎。

1. 按一下「**預設**」，然後按一下您新增的Text和Personalization元件，您會看到裡面有箭頭的靶心。 按一下圖示以鎖定此元件。

   ![chlimage_1-189](assets/chlimage_1-189.png)

1. 導覽至另一個區段（男性），然後按一下&#x200B;**新增選件**，然後按一下加號圖示+。 然後編輯選件。
1. 導覽至另一個區段（女性），然後按一下「**新增選件**」和加號圖示+。 然後編輯此選件。
1. 按一下[下一步]&#x200B;**&#x200B;**&#x200B;檢視對應，然後按一下[下一步]&#x200B;**&#x200B;**&#x200B;檢視不適用於Adobe Campaign的設定，然後按一下[儲存]&#x200B;**&#x200B;**。

   當內容在Adobe Campaign內的傳遞中使用時，AEM會自動產生適用於Adobe Campaign的正確目標定位代碼

1. 在Adobe Campaign中，建立您的傳遞 — 選取包含AEM內容的&#x200B;**電子郵件傳遞**，並視需要選取本機AEM帳戶並確認您的變更。

   在HTML檢視中，目標元件的不同體驗會包含在Adobe Campaign目標定位程式碼中。

   ![chlimage_1-190](assets/chlimage_1-190.png)

   >[!NOTE]
   >
   >如果您也在Adobe Campaign中設定區段，按一下「**預覽**」會顯示每個區段的體驗。
