---
title: 使用內容片段
description: 了解Adobe Experience Manager(AEM)中的內容片段如何讓您設計、建立、組織及使用不受頁面影響的內容，最適合無頭式傳送。
feature: Content Fragments
role: User
source-git-commit: 819df6d6123575b378676dda200064725de47b84
workflow-type: tm+mt
source-wordcount: '1991'
ht-degree: 3%

---

# 使用內容片段 {#working-with-content-fragments}

透過Adobe Experience Manager(AEM)，內容片段可讓您設計、建立、組織及[發佈頁面無關內容](/help/sites-authoring/content-fragments.md)，讓您準備可在多個位置/透過多個頻道使用的內容，非常適合無頭傳送。

內容片段包含結構化內容：

* 它們以[內容片段模型](/help/assets/content-fragments/content-fragments-models.md)為基礎，該模型預先定義所產生片段的結構。
* 結構可介於：
   * 基本
      * 例如，單行多行文本欄位。
      * 可用來準備簡單明瞭的內容以用於頁面編寫。
   * 複雜
      * 多種資料類型欄位的組合，包括文字、數字、布林值、資料和時間等。
      * 可用於準備更多結構化內容以供頁面編寫，或用於傳遞至您的應用程式。
   * 巢狀
      * 可用的參考資料類型可讓您巢狀內嵌內容。
      * 通常用於傳遞至您的應用程式。

使用AEM核心元件的Sling模型(JSON)匯出功能，也能以JSON格式傳送內容片段。 此傳遞形式：

* 可讓您使用元件來管理要傳送的片段元素
* 在用於API傳送的頁面上新增多個內容片段核心元件，以允許大量傳送

本頁及以下頁面涵蓋建立、設定、維護和使用內容片段的工作：

* [為您的執行個體啟用內容片段功能](/help/assets/content-fragments/content-fragments-configuration-browser.md)
* [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)  — 啟用、建立和定義您的模型
* [管理內容片段](/help/assets/content-fragments/content-fragments-managing.md)  — 建立您的內容片段；然後編輯、發佈和參考
* [變異 — 編寫片段內容](/help/assets/content-fragments/content-fragments-variations.md)  — 編寫片段內容並建立主版的變異
* [Markdown](/help/assets/content-fragments/content-fragments-markdown.md)  — 對片段使用Markdown語法
* [使用關聯內容](/help/assets/content-fragments/content-fragments-assoc-content.md)  — 新增關聯內容
* [中繼資料](/help/assets/content-fragments/content-fragments-metadata.md)  — 片段屬性 — 檢視和編輯片段屬性
* 使用[內容片段和GraphQL來提供內容](/help/assets/content-fragments/content-fragments-graphql.md)，以便在您的應用程式中使用。 若要提供相關協助，您可以預覽[JSON輸出](/help/assets/content-fragments/content-fragments-json-preview.md)。

>[!NOTE]
>
>這些頁面可與下列內容一併閱讀：
>
>* [使用內容片段進行頁面編寫](/help/sites-authoring/content-fragments.md)。
>* [自訂和擴充內容片段](/help/sites-developing/customizing-content-fragments.md)
>* [轉譯專用內容片段設定元件](/help/sites-developing/content-fragments-config-components-rendering.md)
>* [AEM Assets HTTP API 內容片段支援](/help/assets/assets-api-content-fragments.md)
>* [AEM GraphQL API以搭配內容片段使用](/help/assets/content-fragments/graphql-api-content-fragments.md)


通信渠道的數量每年都在增加。 通常管道是指傳送機制，如下所示：

* 物理通道；例如案頭、行動。
* 物理通道中的傳遞形式；例如案頭版的「產品詳細資料頁面」、「產品類別頁面」或行動版的「行動網頁」、「行動應用程式」。

不過，您（可能）不想對所有頻道使用完全相同的內容，您需要根據特定頻道最佳化內容。

內容片段可讓您：

* 考慮如何跨管道有效觸及目標對象。
* 建立和管理不受管道影響的編輯內容。
* 為一系列頻道建立內容池。
* 設計特定頻道的內容變數。
* 透過插入資產（混合媒體片段），將影像新增至文字。
* 建立巢狀內容以反映資料的複雜性。

然後，可組合這些內容片段，以透過各種管道提供體驗。

>[!NOTE]
>
>**內容** 片段和 **[體驗](/help/sites-authoring/experience-fragments.md)** 片段是AEM內的不同功能：
>* **內容** 片段是編輯內容，可用來存取結構化資料，包括文字、數字和日期等。它們是純內容，具有定義和結構，但沒有額外的視覺設計和/或版面。
>* **體驗** 片段內容已完整規劃；網頁的片段。

>
>體驗片段可以包含內容片段形式的內容，但不能以相反的方式。
>
>如需詳細資訊，請參閱[了解AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html?lang=en#content-fragments)中的內容片段和體驗片段。

>[!NOTE]
>
>在AEM 6.3之前，是使用範本（而非模型）建立內容片段。 不再提供範本以建立新片段，但使用此範本建立的任何片段仍受支援。

## 內容片段與內容服務 {#content-fragments-and-content-services}

AEM Content Services的設計目的，是為了將AEM中/來自的內容的說明和傳送，歸納為網頁上的重點以外。

它們使用可供任何用戶端使用的標準化方法，將內容傳遞至非傳統AEM網頁的頻道。 這些管道可包括：

* 單頁應用程式
* 原生行動應用程式
* AEM外部的其他通道和接觸點

使用JSON匯出工具，以JSON格式傳送。

AEM內容片段可用來說明及管理結構化內容。 結構化內容定義於可包含多種內容類型的模型中；包括文字、數值資料、布林值、日期和時間等。

此結構化內容再加上AEM核心元件的JSON匯出功能，便可用來將AEM內容傳送至AEM頁面以外的管道。

<!--
>[!NOTE]
>
>See [Headless and AEM](/help/implementing/developing/headless/introduction.md) for an introduction to Headless Development for AEM Sites.
-->

>[!NOTE]
>
>AEM也支援片段內容的翻譯。

<!--
>[!NOTE]
>
>AEM also supports the translation of fragment content. See [Translating Assets](/help/assets/translate-assets.md) for further information.
-->

## 內容類型 {#content-type}

內容片段包括：

* 儲存為&#x200B;**Assets**:

   * 您可以從&#x200B;**Assets**&#x200B;主控台建立和維護內容片段（及其變體）。
   * 在內容片段編輯器中撰寫和編輯。

* 透過內容片段元件](/help/sites-authoring/content-fragments.md)（參考元件）用於[頁面編輯器：

   * 頁面作者可使用&#x200B;**內容片段**&#x200B;元件。 它可讓使用者以HTML或JSON格式參照和傳送所需的內容片段。

* 使用[AEM GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)存取。

內容片段是內容結構，可：

* 沒有版面或設計（在RTF模式中可能有一些文字格式）。
* 包含一個或多個[組成部分](#constituent-parts-of-a-content-fragment)。
* 可以[包含或連接到影像](#fragments-with-visual-assets)。
* 在頁面上參考時，可以在內容](#in-between-content-when-page-authoring-with-content-fragments)之間使用[。

* 與傳送機制（即頁面、通道）無關。

### 具有視覺資產的片段 {#fragments-with-visual-assets}

為了讓作者更能控制其內容，可將影像新增至內容片段及/或與其整合。

資產可透過數種方式搭配內容片段使用；各有其優點：

* **插入** 資產片段（混合媒體片段）

   * 是片段的完整部分（請參閱[內容片段的組成部分](#constituent-parts-of-a-content-fragment)）。
   * 定義資產的位置。
   * 如需詳細資訊，請參閱片段編輯器中的[將資產插入您的片段](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment) 。

   >[!NOTE]
   >
   >插入內容片段本身的視覺資產會附加至前一段。 將片段新增至頁面時，當內容介於之間時，這些資產會相對於該段落移動。

* **相關聯的內容**

   * 連接到片段；但不是片段的固定部分（請參閱[內容片段的組成部分](#constituent-parts-of-a-content-fragment)）。
   * 允許一些定位靈活性。
   * 在頁面上使用片段時，可輕鬆供使用（作為中間內容）。
   * 如需詳細資訊，請參閱[關聯內容](/help/assets/content-fragments/content-fragments-assoc-content.md) 。

* 頁面編輯器的「 **資產** 」瀏覽器可用的資產

   * 允許完全彈性地選取資產。
   * 允許一些定位靈活性。
   * 不提供針對特定片段核准的概念。

<!--
  * See [Assets Browser](/help/sites-authoring/environment-tools.md#assets-browser) for more information.
-->

### 內容片段的組成部分 {#constituent-parts-of-a-content-fragment}

內容片段資產由下列部分組成（直接或間接）:

* **片段元素**

   * 元素與包含內容的資料欄位相關聯。
   * 您可以使用內容模型來建立內容片段。 模型中指定的元素（欄位）定義片段的結構。 這些元素（欄位）可以是多種資料類型。

* **片段段落**

   * 以個別實體分隔的文字區塊，通常為多行。

   * 在富 [文本](/help/assets/content-fragments/content-fragments-variations.md#rich-text)[](/help/assets/content-fragments/content-fragments-variations.md#markdown) 和標籤下拉模式中，段落可以格式化為標題，在這種情況下，它和以下段落作為一個單位一起組成。

   * 在頁面製作期間啟用內容控制。

* **插入片段中的資產（混合媒體片段）**

   * 插入實際片段中並用作片段內部內容的資產（影像）。
   * 內嵌於片段的段落系統中。
   * 在頁面](/help/sites-authoring/content-fragments.md)上使用/參考[片段時，可設定格式。
   * 只能使用片段編輯器，在片段中新增、刪除或移動。 無法在頁面編輯器中執行這些動作。
   * 您只能在片段編輯器](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment)中使用[RTF格式，將片段新增至、從中刪除或移動。
   * 只能新增至多行文字元素（任何片段類型）。
   * 附於前文（段）。

      >[!CAUTION]
      >
      >切換為純文字格式後，可能會（無意中）從片段中移除資產。

      >[!NOTE]
      >
      >在頁面上使用片段時，也可以將資產新增為[其他（介於）內容](/help/sites-authoring/content-fragments.md#using-associated-content);使用「資產」瀏覽器中的「關聯內容」或「資產」。

* **相關聯的內容**

   * 這是片段外部的內容，但與編輯相關。 通常是影像、視訊或其他片段。
   * 將集合內的個別資產新增至頁面時，可與頁面編輯器中的片段搭配使用。 這表示這些量度為選用，視特定管道的需求而定。
   * 資產是透過集合](/help/assets/content-fragments/content-fragments-assoc-content.md)與片段關聯的[;相關聯的集合可讓作者在編寫頁面時決定要使用的資產。

      * 集合可以以預設內容的形式與片段相關聯，或由作者在片段製作期間建立關聯。
      * [資產(DAM)](/help/assets/manage-collections.md) 集合是片段相關聯內容的基礎。
   * （可選）您也可以將片段本身新增至集合以輔助追蹤。

* **片段中繼資料**

   * 使用[Assets中繼資料結構](/help/assets/metadata-schemas.md)。
   * 標籤可在下列情況下建立：

      * 建立及製作片段
      * 或更新版本：

         * 通過從控制台檢視/編輯片段&#x200B;**屬性**
         * 在片段編輯器中編輯&#x200B;**中繼資料**&#x200B;時

   >[!CAUTION]
   >
   >中繼資料處理設定檔不適用於內容片段。

* **主版**

   * 片段的一個完整部分

      * 每個內容片段都有一個主版例項。
      * 無法刪除主版。
   * 可在&#x200B;**[Valiations](/help/assets/content-fragments/content-fragments-variations.md)**&#x200B;下的片段編輯器中存取主版。
   * 主版並非如此，而是所有變異的基礎。


* **變數**

   * 轉譯專用於編輯目的的片段文字；可與管道相關，但非強制性，也可用於臨機本機修改。
   * 建立為&#x200B;**Master**&#x200B;的副本，但之後可視需要編輯；變異本身之間通常會有內容重疊。
   * 可在片段製作期間定義。
   * 儲存在片段中，以協助避免內容復本的分散。
   * 如果更新了主內容，則變數可以是與主內容同步的[](/help/assets/content-fragments/content-fragments-variations.md#synchronizing-with-master)。
   * 可以是[摘要](/help/assets/content-fragments/content-fragments-variations.md#summarizing-text)，以快速截斷文字至預先定義的長度。
   * 在片段編輯器的[Valuations](/help/assets/content-fragments/content-fragments-variations.md)標籤下可用。

### 使用內容片段製作頁面時的內容之間 {#in-between-content-when-page-authoring-with-content-fragments}

中間內容：

* 使用內容片段時，可在頁面編輯器中使用。
* 是在頁面上使用/參考片段](/help/sites-authoring/content-fragments.md#adding-in-between-content)後，在片段的流程中新增的其他內容。[
* 使用內容片段](/help/sites-authoring/content-fragments.md)時，可在[頁面編輯器中使用。
* 中間內容可新增至任何片段，其中只會顯示一個元素。
* 您也可以使用相關內容，使用適當瀏覽器的資產和/或元件。

>[!CAUTION]
>
>中間內容是頁面內容。 它不會儲存在內容片段中。

### 片段所需 {#required-by-fragments}

若要建立所需的內容片段：

* **內容模型**

   * 使用配置瀏覽器](/help/assets/content-fragments/content-fragments-configuration-browser.md)啟用[。
   * 是使用工具](/help/assets/content-fragments/content-fragments-models.md)建立的[。
   * [建立片段](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments)所需。
   * 定義片段的結構（標題、內容元素、標籤定義）。
   * 內容模型定義需要標題和一個資料元素；其他所有項目均為選用。
   * 模型可定義預設內容（如果適用）。
   * 製作片段內容時，作者無法變更已定義的結構。
   * 建立相依內容片段後對模型所做的變更可能會影響這些內容片段。

若要將內容片段用於頁面編寫，您也需要：

* **內容片段元件**

   * 協助以HTML和/或JSON格式傳送片段。
   * [參考頁面](/help/sites-authoring/content-fragments.md)上的片段所需。
   * 負責片段的版面配置和傳送；即頻道。
   * 片段需要一或多個專用元件來定義版面，並傳送部分或所有元素/變異和相關內容。
   * 在製作時將片段拖曳至頁面會自動建立所需元件的關聯。

## 使用範例 {#example-usage}

片段及其元素和變數可用來建立多個頻道的一致內容。 設計片段時，您需要考慮要在哪個位置使用。
