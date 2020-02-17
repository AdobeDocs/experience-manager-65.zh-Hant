---
title: 使用內容片段製作頁面
seo-title: 使用內容片段製作頁面
description: AEM內容片段可讓您設計、建立、組織和使用不受頁面影響的內容
seo-description: AEM內容片段可讓您設計、建立、組織和使用不受頁面影響的內容
uuid: 987de428-8354-4b23-a552-3ea415122184
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 4049a7a5-4b33-4462-a25f-3c0daeb6a8a9
docset: aem65
translation-type: tm+mt
source-git-commit: 4d47310ebf9d450de52c925642978ba92ef9c1d4

---


# 使用內容片段製作頁面{#page-authoring-with-content-fragments}

Adobe Experience Manager(AEM)內容片段會建 [立並管理為不受頁面影響的資產](/help/assets/content-fragments.md)。

它們可讓您建立不受頻道影響的內容，以及（可能是特定頻道的）變化。 然後，您可以在製作內容頁面時使用這些片段及其變化。

結合更新的JSON匯出器，結構化內容片段也可用來透過Content services將AEM內容傳送至AEM頁面以外的通道。

>[!NOTE]
>
>**「內容片段** 」和「 **[體驗片段](/help/sites-authoring/experience-fragments.md)**」是AEM中的不同功能：
>
>* **內容片段** 是編輯內容，主要是文字和相關影像。 它們是純粹的內容，不需要設計和版面配置。
>* **體驗片段** ，內容已完整排版；網頁的片段。
>
>
「體驗片段」可以包含內容片段的形式，但不能以相反的方式包含。

>[!CAUTION]
>
>此頁面必須與「使用內容片段 [](/help/assets/content-fragments.md) （及相關頁面）」一起閱讀，因為它提供基本術語和概念，以及建立和管理片段。

內容片段可啟用：

* **行銷和宣傳策略**

   * 透過集中管理的內容片段來審核內容。

* **Creative Pro**

   * 透過與內容片段關聯的系列追蹤創意資產。

* **複製撰寫人員**

   * 在AEM內容片段編輯器中寫入。
   * 可以建立內容變化。
   * 可將相關內容與內容片段建立關聯。
   * 可以使用版本修訂／工作流。
   * 可以共用內容片段。
   * 可集中管理翻譯。

* **製作人與歷程經理**

   * 在AEM中使用編寫功能，從預先定義的片段和變數中選取。
   * 當複製撰寫人員和創意人員在集中管理的片段和資產中進行更新時，可依賴片段和相關內容隨時保持最新狀態。
   * 可依賴已策劃的相關媒體內容來產生關聯性。
   * 可即時建立臨機內容變化，同時仍可確保這些變化在片段中仍能集中管理。

## 新增內容片段至您的頁面 {#adding-a-content-fragment-to-your-page}

1. 開啟您的頁面進行編輯。

1. 新增內 **容片段** ;從「元件」瀏 **覽器** ，或「插入 **新元件」**。

1. 您可以:

   * 開啟「 **Assets** 」瀏覽器並篩選 **「內容片段** 」（預設為「影像」）。 然後將所需片段拖曳至元件例項。

   * 選擇內容片段元件，然後從工 **具欄中** 「配置」。 在對話方塊中，您可以開啟選取對話方塊，以瀏覽並選取所需的 **內容片段**。
   >[!NOTE]
   >
   >另一種方法是將特定內容片段直接拖曳至頁面上。 這會自動建立關聯的元件（內容片段）。

1. 一開始會顯示 **Main** Element和 **Master** (variation)的內容。 您可以 [視需要選取其他元素和／或變](#selecting-the-element-or-variation) 化。

   ![cfm-6420-01](assets/cfm-6420-01.png)

   >[!NOTE]
   >
   >如需進一步編輯功能的詳細資訊，請參閱：
   >
   >
   >
   >    * [互動式版面](/help/sites-authoring/responsive-layout.md)
   >    * [編輯頁面內容](/help/sites-authoring/editing-content.md)


### 選取元素或變數 {#selecting-the-element-or-variation}

開啟片段的「設 **定** 」對話方塊，以設定要在目前頁面上使用的片段。 對話方塊可視使用的元件而定。

在適當的設定對話方塊中，您可以選取可用的參數，包括：

* **內容片段**

   指定要使用的片段。

* **顯示模式**:

   * **單文字元素**

   * **多重元素**

* **元素**

   * 預設 **主** (Main)將始終可用。
   * 如果片段是使用適當的範本建立，則可使用選取範圍。
   >[!NOTE]
   >
   >可用的元素取決於使用的模板。

* **變數**

   * 預設主 **版** (Master)將始終可用。
   * 如果已為片段建立變數，則可使用選取範圍。

* **段落**:指定要包含的段落範圍：

   * **全部**
   * **範圍**:例如 `1`, `3-5`, `9-*`

      * **將標題當作其段落的一部分來處理**

* **將標題當作其段落的一部分來處理**

### 快速連線至片段編輯器 {#quick-connection-to-fragment-editor}

您可以使用元件工具列上的「編輯」圖示，開啟片段來源以 **進行編輯** （資產）。 這可讓您編輯 [和管理內容片段](/help/assets/content-fragments.md)。

>[!CAUTION]
>
>和以往一樣，編輯片段來源會影響參照該內容片段的所有頁面。

### 新增內容 {#adding-in-between-content}

將特定內容片段新增至頁面時，片段的每個HTML段落（以及片段的上／下）之間都會有 **Drag components** here預留位置。

這可讓您在中間( [亦即中間內容)](/help/assets/content-fragments.md#inbetweencontent) （在任何可用點）新增額外內容，而不需變更根片段。

對於中介內容，您可以：

* 從「元件」瀏覽器 [新增元件](/help/sites-authoring/author-environment-tools.md#components-browser)。
* 從「資產」瀏覽器 [新增資產](/help/sites-authoring/author-environment-tools.md#assets-browser)。
* 使 [用關聯內容](#using-associated-content) ，作為中間內容的來源。

>[!CAUTION]
>
>中間內容是頁面內容。 它不會儲存在內容片段中。

![cfm-6420-02](assets/cfm-6420-02.png)

>[!NOTE]
>
>您也可以 [將視覺資產（影像）插入片段本身](/help/assets/content-fragments-variations.md#inserting-assets-into-your-fragment)。
>
>插入到片段本身的視覺資產附加到片段的前一段。 這表示您無法在視覺資產和前段之間放置內容。

>[!CAUTION]
>
>在頁面上將內容加入內容片段後，變更基礎內容片段的結構（例如在內容片段編輯器中）可能會導致錯誤／非預期結果。
>
>發生此情況時，中間內容會依原樣保留：
>
>* 在片段流中的片段序列內的片段之間具有絕對位置。 即使片段中段落的內容變更，此位置也不會變更。
   >  這可讓相對位置看起來好像已變更，因為中間段落與位於旁邊的（片段）段落沒有關聯關係。
>* 除非兩款結構有衝突；在這種情況下，不顯示中間內容（儘管它仍在內部存在）。
>



### 使用關聯的內容 {#using-associated-content}

如果您有 [與內容片段](/help/assets/content-fragments-assoc-content.md)[相關的內容](/help/assets/content-fragments.md) ，這些資產將可從側面板使用（在您將片段放在內容頁面後）。 關聯內容實際上是中間內容的特 [殊內容來源](#adding-in-between-content)。

>[!NOTE]
>
>有各種方法可將視 [覺資產（例如影像）新增至片段和](/help/assets/content-fragments.md#fragments-with-visual-assets) /或頁面。

>[!NOTE]
>
>如果您在單一頁面上有多個內容片段，「關聯的 **內容** 」索引標籤會顯示適合所有片段的資產。

在將含有關聯內容的片段新增至頁面後，會在側面板中開啟新的標&#x200B;**簽(關聯內容**)。

您可以從這裡將資產拖曳至所需位置（拖曳至現有元件，或拖曳至建立適當元件的必要位置）:

![cfm-6420-03](assets/cfm-6420-03.png)

### 插入片段的資產 {#assets-inserted-into-the-fragment}

如果資產（例如影像）已插入片段本身，則頁面編輯器中編輯這些資產的選項會受到限制。 <!-- Removed link as it was a 404 on helpx -->

例如，若是影像，您可以

* 裁切、旋轉或翻轉影像。
* 新增標題或替代文字。
* 指定大小。
* 您也可以設定版面。

其他變更（例如移動、複製、刪除）必須在片段編輯器中進行。

### 發佈 {#publishing}

片段必須發佈，才能用於您發佈的網頁：

* 在「資產」主控台中建 [立片段後，可發佈片段](/help/assets/content-fragments.md#publishingandreferencingafragment)。
* 如果在 *發佈的頁面上使用未發佈的片段* ，則此時也可以發佈該片段。

