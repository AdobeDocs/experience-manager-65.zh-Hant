---
title: 使用內容片段
seo-title: 使用內容片段
description: 瞭解內容片段如何讓您設計、建立、組織和使用不受頁面限制的內容。
seo-description: 瞭解內容片段如何讓您設計、建立、組織和使用不受頁面限制的內容。
uuid: d35d5638-43a9-424d-9806-6e8d459980d7
contentOwner: Alison Heimoz
topic-tags: content-fragments
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 7ecc1bcf-38a9-4a59-8dd3-79cb90dec33d
docset: aem65
translation-type: tm+mt
source-git-commit: 72d225b5afd1872fb5c4ac89a9b8fb3db25a92a9

---


# 使用內容片段{#working-with-content-fragments}

Adobe Experience Manager(AEM)內容片段可讓您設計、建立、組織和發 [布不受頁面影響的內容](/help/sites-authoring/content-fragments.md)。 它們可讓您準備內容，以便在多個位置／多個通道中使用。

內容片段也可以使用AEM核心元件的Sling Model(JSON)匯出功能，以JSON格式傳送。 這種交付形式：

* 可讓您使用元件來管理要傳送的片段元素
* 允許大量傳送，方法是在用於API傳送的頁面上新增多個內容片段核心元件

本頁及下列各頁涵蓋建立、設定和維護內容片段的工作：

* [管理內容片段](/help/assets/content-fragments-managing.md) -建立您的內容片段；然後編輯、發佈和參考
* [內容片段模型](/help/assets/content-fragments-models.md) -啟用、建立和定義模型
* [變數——製作片段內容](/help/assets/content-fragments-variations.md) -製作片段內容並建立主版的變數
* [Markdown](/help/assets/content-fragments-markdown.md) —— 使用Markdown語法建立片段
* [使用關聯內容](/help/assets/content-fragments-assoc-content.md) -新增關聯內容
* [中繼資料——片段屬性](/help/assets/content-fragments-metadata.md) -檢視和編輯片段屬性

>[!NOTE]
>
>這些頁面應與「使用內容片段 [編寫頁面」一起閱讀](/help/sites-authoring/content-fragments.md)。

通訊頻道的數量逐年增加。 通常渠道是指傳送機制，例如：

* 物理通道；例如桌上型電腦、行動裝置。
* 實體渠道的交付形式；例如，「產品詳細資訊頁面」、「產品類別頁面」（適用於桌上型電腦）或「行動網頁」（適用於行動裝置）、「行動應用程式」（適用於行動裝置）。

不過，您（可能）不想針對所有通道使用完全相同的內容——您需要根據特定通道最佳化您的內容。

內容片段可讓您：

* 考慮如何跨通道有效觸及目標受眾。
* 建立並管理不受頻道影響的編輯內容。
* 建立適用於各種通道的內容池。
* 針對特定通道設計內容變化。
* 插入資產（混合媒體片段），將影像新增至文字。

然後，這些內容片段可以組合起來，以透過多種通道提供體驗。

## 內容片段與內容服務 {#content-fragments-and-content-services}

AEM Content services的設計目的，是將AEM中／來自AEM的內容描述和傳送，從而延伸到網頁。

它們使用可供任何用戶端使用的標準化方法，將內容傳送至非傳統AEM網頁的頻道。 這些渠道可以包括：

* 單頁應用程式
* 原生行動應用程式
* AEM外部的其他通道和觸點

傳送是以JSON格式進行。

AEM內容片段可用來描述和管理結構化內容。 結構化內容定義在可包含多種內容類型的模型中；包括文字、數值資料、布林值、日期和時間等。

此結構化內容可搭配AEM核心元件的JSON匯出功能，用來將AEM內容傳送至AEM頁面以外的通道。

>[!NOTE]
>
>**「內容片段** 」和「 **[體驗片段](/help/sites-authoring/experience-fragments.md)**」是AEM中的不同功能：
>* **內容片段** 是編輯內容，主要是文字和相關影像。 它們是純粹的內容，不需要設計和版面配置。
>* **體驗片段** ，內容已完整排版；網頁的片段。
>
>
「體驗片段」可以包含內容片段的形式，但不能以相反的方式包含。
>
>如需詳細資訊，請參閱「了 [解AEM中的內容片段和體驗片段」](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/content-fragments-experience-fragments-article-understand.html)。

>[!CAUTION]
>
>傳統UI中不提供內容片段。
>
>「內容片段」元件可在傳統UI側鍵中看到，但無法使用其他功能。

>[!NOTE]
>
>AEM也支援片段內容的轉譯。 如需詳 [細資訊，請參閱建立內容片段的轉譯專案](/help/assets/creating-translation-projects-for-content-fragments.md) 。

## 內容片段類型 {#types-of-content-fragment}

內容片段可以是：

* 簡單片段這些片段沒有預先定義的結構。 它們只包含文字和影像。
這些是以「簡單片段」範本為基礎。

* 包含結構化內容的片段這些片段是以內容 [片段模型為基礎](/help/assets/content-fragments-models.md)，此模型會預先定義產生的片段結構。
這些功能也可用於使用JSON匯出器來實現內容服務。

## 內容類型 {#content-type}

內容片段包括：

* 儲存為 **資產**:

   * 內容片段（及其變數）可從「資產」主控台建 **立和維** 護。
   * 在「內容片段編輯器」中撰寫和編輯。

* 在頁面編 [輯器中，透過內容片段元件](/help/sites-authoring/content-fragments.md) （參考元件）使用：

   * 頁 **面作者可使用** 「內容片段」元件。 它可讓使用者參考並傳送HTML或JSON格式的必要內容片段。

內容片段是一種內容結構，可：

* 沒有版面或設計（在Rich Text模式中可能有某些文字格式）。
* 包含一或多個組 [成部分](#constituent-parts-of-a-content-fragment)。
* 可以 [包含或連接到映像](#fragments-with-visual-assets)。
* 可在頁 [面上參考時](#in-between-content-when-page-authoring-with-content-fragments) ，使用中間內容。

* 獨立於傳送機制（即頁面、頻道）。

### 包含視覺資產的片段 {#fragments-with-visual-assets}

為了讓作者更能控制其內容，可將影像新增至內容片段及／或與內容片段整合。

資產可以幾種方式與內容片段搭配使用；各自各有優勢：

* **將資產插入** （混合媒體片段）

   * 是片段的一個完整部分(請參 [閱內容片段的組成部分](#constituent-parts-of-a-content-fragment))。
   * 定義資產的位置。
   * 如需詳 [細資訊，請參閱片段編輯器中](/help/assets/content-fragments-variations.md#inserting-assets-into-your-fragment) 「將資產插入片段」。
   >[!NOTE]
   >
   >插入到內容片段本身的視覺資產附加在前段。 將片段新增至頁面時，這些資產會在新增中間內容時相對於該段落移動。

* **相關聯的內容**

   * 連接到碎片；但不是片段的固定部分(請參閱 [內容片段的組成部分](#constituent-parts-of-a-content-fragment))。
   * 提供一定的定位彈性。
   * 在頁面上使用片段時，可輕鬆使用（當成中間內容）。
   * 如需詳 [細資訊](/help/assets/content-fragments-assoc-content.md) ，請參閱關聯內容。

* 頁面編輯器的「 **資產** 」瀏覽器可用的資產

   * 允許完全彈性地選擇資產。
   * 提供一定的定位彈性。
   * 不提供特定片段的核准概念。
   * 如需詳 [細資訊](/help/sites-authoring/author-environment-tools.md#assets-browser) ，請參閱資產瀏覽器。

### 內容片段的組成部分 {#constituent-parts-of-a-content-fragment}

內容片段資產由下列部分（直接或間接）組成：

* **片段元素**

   * 元素會關聯至包含內容的資料欄位。
   * 對於具有結構化內容的片段，您可使用內容模型來建立內容片段。 在模型中指定的元素（欄位）定義片段的結構。 這些元素（欄位）可以是多種資料類型。
   * 對於簡單片段：

      * 內容保存在一（或多個）多行文字欄位或元素中。
      * 元素是在片段範本中定義(在編寫片段時無法定義，請參 [閱內容片段範本](/help/sites-developing/content-fragment-templates.md))。

* **片段段落**

   * 文字區塊，即：

      * 由垂直空格分隔（歸位）
      * 在多行文字元素中；簡單或結構化片段
   * 在富 [文本](/help/assets/content-fragments-variations.md#rich-text)[](/help/assets/content-fragments-variations.md#markdown) 和標籤下拉模式中，段落可以格式化為標題，在這種情況下，它和以下段落作為一個單位一起組成。

   * 在製作頁面時啟用內容控制。


* **插入片段的資產（混合媒體片段）**

   * 插入實際片段並用作片段內部內容的資產（影像）。
   * 嵌入片段的段落系統中。
   * 可在頁面上使 [用／參考片段時格式化](/help/sites-authoring/content-fragments.md)。
   * 只能使用片段編輯器將片段添加到片段、從中刪除或在其中移動。 這些動作無法在頁面編輯器中執行。
   * 只能在片段編輯器中使用 [Rich Text格式將片段添加到片段、從中刪除或移動](/help/assets/content-fragments-variations.md#inserting-assets-into-your-fragment)。
   * 只能新增至多行文字元素（任何片段類型）。
   * 附於前文（段）。
   >[!CAUTION]
   >
   >可以（不慎）切換為純文字格式，從片段中移除。

   >[!NOTE]
   >
   >在頁面上使用 [片段時](/help/sites-authoring/content-fragments.md#using-associated-content) ，也可將資產新增為額外（中間）內容；使用「資產」瀏覽器中的「關聯內容」或「資產」。

* **相關聯的內容**

   * 這是片段外部的內容，但與編輯相關。 通常是影像、視訊或其他片段。
   * 當系列中的個別資產新增至頁面時，可與頁面編輯器中的片段搭配使用。 這表示它們是可選的，具體取決於特定渠道的要求。
   * 這些資產會 [透過系列關聯至片段](/help/assets/content-fragments-assoc-content.md);關聯的系列可讓作者決定在編寫頁面時要使用哪些資產。

      * 系列可以透過範本、預設內容或作者在片段製作期間，與片段建立關聯。
      * [資產(DAM)集合](/help/assets/managing-collections-touch-ui.md) ，是片段相關內容的基礎。
   * （可選）您也可以將片段本身新增至系列，以協助追蹤。


* **片段中繼資料**

   * 使用「資 [產」中繼資料結構](/help/assets/metadata.md)。
   * 標籤可在下列情況下建立：

      * 建立並編寫片段
      * 或更新版本：

         * 通過從控制台查看／編 **輯片段** 「屬性」
         * 在片段編輯 **器中** ，編輯中繼資料
   >[!CAUTION]
   >
   >中繼資料處理設定檔不適用於內容片段。

* **主版**

   * 碎片的一個整體

      * 每個內容片段都有一個主體實例。
      * 無法刪除主版。
   * 主版可在片段編輯器的「變數」下 **[存取](/help/assets/content-fragments-variations.md)**。
   * 主變數不是變數，而是所有變數的基礎。


* **變數**

   * 轉譯特定於編輯目的的片段文字；可以與頻道相關，但非強制性，也可以是臨機本機修改。
   * 建立為主版的副 **本**，但可根據需要進行編輯；這些變化本身之間通常有內容重疊。
   * 可在片段製作期間定義，或在片段範本中預先定義。
   * 儲存在片段中，以協助避免內容復本散布。
   * 如果主版內 [容已更新](/help/assets/content-fragments-variations.md#synchronizing-with-master) ，則可與主版同步變數。
   * 可以摘 [要](/help/assets/content-fragments-variations.md#summarizing-text) ，快速將文字截斷為預先定義的長度。
   * 可在片段編輯 [器的](/help/assets/content-fragments-variations.md) 「變化」標籤下使用。

### 使用內容片段製作頁面時的內容夾 {#in-between-content-when-page-authoring-with-content-fragments}

中間內容：

* 在使用內容片段時， [可在頁面編輯器中使用](/help/sites-authoring/content-fragments.md)。
* 在 [頁面上使用／參考片段後](/help/sites-authoring/content-fragments.md#adding-in-between-content) ，會在片段流程中新增其他內容嗎？
* 您可以將中間內容新增至任何片段，其中只有一個元素可見。
* 可使用相關的內容，也可使用適當瀏覽器的資產和／或元件。

>[!CAUTION]
>
>中間內容是頁面內容。 它不會儲存在內容片段中。

### 片段所需 {#required-by-fragments}

若要建立、編輯和使用您也需要的內容片段：

* **內容模型**

   * 啟 [用，然後使用工具建立](/help/assets/content-fragments-models.md)。
   * 建立結 [構化片段所需](/help/assets/content-fragments-managing.md#creating-content-fragments)。
   * 定義片段的結構（標題、內容元素、標籤定義）。
   * 內容模型定義需要一個標題和一個資料元素；其他一切都是可選的。 模型會定義片段的最小範圍，並定義預設內容（如果適用）。 製作片段內容時，作者無法變更已定義的結構。

* **片段範本**

   * 建立簡 [單片段所需](/help/assets/content-fragments-managing.md#creating-content-fragments)。
   * 通常 [在項目實施期間開發](/help/sites-developing/content-fragment-templates.md);無法在編寫時建立。
   * 定義簡單片段的基本屬性（標題、文字元素數目、標籤定義）。
   * 範本定義需要一個標題和一個文字元素；其他一切都是可選的。 範本會定義片段的最小範圍和預設內容（如果適用）。 作者稍後可將片段延伸至範本中定義的範圍以外。

* **內容片段元件**

   * 有助於以HTML和／或JSON格式傳送片段。
   * 在頁面 [上參考片段時需要](/help/sites-authoring/content-fragments.md)。
   * 負責片段的排版和傳送；即頻道。
   * 片段需要一個或多個專用元件來定義版面，並傳送部分或所有元素／變化和相關內容。
   * 將片段拖曳至編寫時的頁面，將會自動關聯所需的元件。

## 範例使用 {#example-usage}

片段及其元素和變化可用於為多個通道建立相干內容。 在設計片段時，您需要考慮將使用哪些內容。

### We.Retail範例 {#we-retail-sample}

範例片段可在以下網址查看：

`https://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten`
