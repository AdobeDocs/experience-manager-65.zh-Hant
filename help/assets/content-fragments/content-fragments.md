---
title: 使用內容片段
description: 瞭解Adobe Experience Manager(AEM)中的內容片段如何允許您設計、建立、建立和使用與頁面無關的內容，這是無頭傳送的理想選擇。
feature: Content Fragments
role: User
exl-id: 0ee883c5-0cea-46b7-a759-600b8ea3bc3e
source-git-commit: ad0f0bd8b0c230e002c734adca87da22bfa3a7cd
workflow-type: tm+mt
source-wordcount: '1989'
ht-degree: 4%

---

# 使用內容片段 {#working-with-content-fragments}

使用Adobe Experience Manager(AEM)，內容片段允許您設計、建立、策劃和 [發佈頁面無關內容](/help/sites-authoring/content-fragments.md) 它們使您能夠準備內容，以便在多個位置/多個渠道中使用，非常適合無頭傳送。

內容片段包含結構化內容：

* 它們基於 [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)，它為生成的片段預定義結構。
* 該結構可以介於以下之間：
   * 基本
      * 例如，單行多行文本欄位。
      * 可用於準備直接內容以用於頁面創作。
   * 複雜
      * 多種資料類型不同的欄位的組合，包括文本、數字、布爾值、資料和時間等。
      * 可用於準備更多結構化內容以用於頁面創作或交付到應用程式。
   * 嵌套
      * 可用的引用資料類型允許您嵌套內容。
      * 通常用於交付到應用程式。

使用核心元件的Sling Model(JSON)導出功能，內容片段也可以以JSON格式AEM傳送。 此交付形式：

* 允許您使用元件來管理要傳遞的片段元素
* 允許批量交付，方法是在用於API交付的頁面上添加多個內容片段核心元件

本頁和以下頁介紹建立、配置、維護和使用內容片段的任務：

* [為實例啟用內容片段功能](/help/assets/content-fragments/content-fragments-configuration-browser.md)
* [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)  — 啟用、建立和定義模型
* [管理內容片段](/help/assets/content-fragments/content-fragments-managing.md)  — 建立內容片段；然後編輯、發佈和引用
* [變體 — 創作片段內容](/help/assets/content-fragments/content-fragments-variations.md)  — 編寫片段內容並建立主檔案的變體
* [馬爾克當](/help/assets/content-fragments/content-fragments-markdown.md)  — 使用標籤語法
* [使用關聯內容](/help/assets/content-fragments/content-fragments-assoc-content.md)  — 添加關聯內容
* [元資料 — 片段屬性](/help/assets/content-fragments/content-fragments-metadata.md)  — 查看和編輯片段屬性
* 使用 [內容片段與GraphQL一起，用於傳遞內容](/help/assets/content-fragments/content-fragments-graphql.md) 在您的應用程式中使用。 要幫助處理此問題，可以預覽 [JSON輸出](/help/assets/content-fragments/content-fragments-json-preview.md)。

>[!NOTE]
>
>這些頁面可以與以下內容一起閱讀：
>
>* [帶內容片段的頁面創作](/help/sites-authoring/content-fragments.md)。
>* [自訂和擴充內容片段](/help/sites-developing/customizing-content-fragments.md)
>* [轉譯專用內容片段設定元件](/help/sites-developing/content-fragments-config-components-rendering.md)
>* [AEM Assets HTTP API 內容片段支援](/help/assets/assets-api-content-fragments.md)
>* [與內容片段搭配使用的 AEM GraphQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md)


通信通道的數量每年都在增加。 通常，渠道是指遞送機制，或者是：

* 物理通道；例如台式機、移動式。
* 實物渠道的交付形式；例如，案頭的「產品詳細資訊頁面」、「產品類別頁面」或移動的「移動web」、「移動應用」。

但是，您（可能）不希望對所有頻道使用完全相同的內容 — 您需要根據特定頻道優化您的內容。

內容片段允許您：

* 考慮如何跨渠道高效地訪問目標受眾。
* 建立和管理渠道中性的編輯內容。
* 為一系列渠道構建內容池。
* 為特定頻道設計內容變體。
* 通過插入資產（混合媒體片段）將影像添加到文本中。
* 建立嵌套內容以反映資料的複雜性。

然後，這些內容片段可被組合以在多種頻道上提供體驗。

>[!NOTE]
>
>**內容片段** 和 **[體驗片段](/help/sites-authoring/experience-fragments.md)** 是內部的不同功AEM能：
>* **內容片段** 是編輯內容，可用於訪問結構化資料，包括文本、數字和日期等。 它們是純內容，具有定義和結構，但沒有附加的視覺設計和/或佈局。
>* **體驗片段** 內容全面，網頁的片段。
>
>體驗片段可以包含內容片段的形式，但不能以相反的方式。
>
>有關詳細資訊，另請參見 [理解中的內容片段和體驗片段AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html#content-fragments)。

>[!NOTE]
>
>6.AEM3之前使用模板而不是模型建立內容片段。 模板不再可用於建立新片段，但仍支援使用此模板建立的任何片段。

## 內容片段和內容服務 {#content-fragments-and-content-services}

Content Services旨在AEM將內容的描述和交付範圍從關注網AEM頁的範圍延伸出來。

它們使用可供任何客戶使用的標準化方法，將內AEM容交付到非傳統網頁的渠道。 這些渠道可以包括：

* 單頁應用程式
* 本機移動應用程式
* 外部的其它通道和觸AEM點

使用JSON導出器以JSON格式進行傳遞。

內AEM容片段可用於描述和管理結構化內容。 結構化內容在可包含多種內容類型的模型中定義；包括文本、數值資料、布爾值、日期和時間等。

再加上核心元件的JSON導AEM出功能，此結構化內容可用於將內AEM容傳送到頁面以外AEM的渠道。

<!--
>[!NOTE]
>
>See [Headless and AEM](/help/implementing/developing/headless/introduction.md) for an introduction to Headless Development for AEM Sites.
-->

>[!NOTE]
>
>還AEM支援片段內容的翻譯。

<!--
>[!NOTE]
>
>AEM also supports the translation of fragment content. See [Translating Assets](/help/assets/translate-assets.md) for further information.
-->

## 內容類型 {#content-type}

內容片段包括：

* 儲存為 **資產**:

   * 內容片段（及其變體）可從 **資產** 控制台。
   * 在內容片段編輯器中創作和編輯。

* 在 [通過「內容片段」元件進行頁面編輯](/help/sites-authoring/content-fragments.md) （引用元件）:

   * 的 **內容片段** 元件可供頁面作者使用。 它允許他們以HTML或JSON格式引用和傳遞所需的內容片段。

* 使用 [AEMGraphQL](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md)。

內容片段是一種內容結構，它：

* 沒有佈局或設計（在RTF模式下可能有一些文本格式）。
* 包含一個或多個， [組成部分](#constituent-parts-of-a-content-fragment)。
* 可 [包含或連接到映像](#fragments-with-visual-assets)。
* 可以使用 [內容](#in-between-content-when-page-authoring-with-content-fragments) 在頁面上引用時。

* 獨立於傳遞機制（即頁面、渠道）。

### 具有可視資產的片段 {#fragments-with-visual-assets}

為了給作者更多地控制其內容，可以將影像添加到內容片段和/或與內容片段整合。

資產可以通過多種方式與內容片段一起使用；各有其優勢：

* **插入資產** 片段（混合媒體片段）

   * 是片段的一部分(請參見 [內容片段的組成部分](#constituent-parts-of-a-content-fragment))。
   * 定義資產的位置。
   * 請參閱 [將資產插入片段](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment) 的子菜單。

   >[!NOTE]
   >
   >插入內容片段本身的視覺資產附在前款。 將片段添加到頁面時，在添加內容之間時，這些資產將相對於該段移動。

* **相關聯的內容**

   * 連接到片段；但不是碎片的固定部分(請參見 [內容片段的組成部分](#constituent-parts-of-a-content-fragment))。
   * 允許一定的定位靈活性。
   * 在頁面上使用片段時，可以輕鬆使用（如內容）。
   * 請參閱 [關聯內容](/help/assets/content-fragments/content-fragments-assoc-content.md) 的子菜單。

* 頁面編輯器的「 **資產** 」瀏覽器可用的資產

   * 允許完全靈活地選擇資產。
   * 允許一定的定位靈活性。
   * 不提供針對特定片段獲得批准的概念。

<!--
  * See [Assets Browser](/help/sites-authoring/environment-tools.md#assets-browser) for more information.
-->

### 內容片段的組成部分 {#constituent-parts-of-a-content-fragment}

內容片段資產由以下部分（直接或間接）組成：

* **片段元素**

   * 元素與保存內容的資料欄位相關。
   * 使用內容模型建立內容片段。 模型中指定的元素（欄位）定義片段的結構。 這些元素（欄位）可以是多種資料類型。

* **片段段落**

   * 文本塊（通常為多行），它們被分隔為單個實體。

   * 在富 [文本](/help/assets/content-fragments/content-fragments-variations.md#rich-text)[](/help/assets/content-fragments/content-fragments-variations.md#markdown) 和標籤下拉模式中，段落可以格式化為標題，在這種情況下，它和以下段落作為一個單位一起組成。

   * 在頁面創作期間啟用內容控制。

* **插入片段中的資產（混合媒體片段）**

   * 插入到實際片段中並用作片段的內部內容的資產（影像）。
   * 嵌入片段的段落系統中。
   * 可在 [頁面上使用/引用片段](/help/sites-authoring/content-fragments.md)。
   * 只能使用片段編輯器將片段添加到、從中刪除或移動到其中。 無法在頁面編輯器中執行這些操作。
   * 只能使用 [片段編輯器中的RTF格式](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment)。
   * 只能添加到多行文本元素（任何片段類型）。
   * 附於前文（第1款）。

      >[!CAUTION]
      >
      >通過切換到純文字檔案格式，可以（無意間）從片段中刪除資產。

      >[!NOTE]
      >
      >資產也可以添加為 [附加（中間）內容](/help/sites-authoring/content-fragments.md#using-associated-content) 在頁面上使用片段時；使用「資產」瀏覽器中的「關聯內容」或「資產」。

* **相關聯的內容**

   * 這是片段之外的內容，但與編輯相關。 通常是影像、視頻或其他片段。
   * 將集合中的單個資產添加到頁面編輯器中時，可將其與片段一起使用。 這意味著它們是可選的，具體取決於特定渠道的要求。
   * 資產 [通過集合關聯片段](/help/assets/content-fragments/content-fragments-assoc-content.md);關聯的集合允許作者在創作頁面時決定要使用哪些資產。

      * 集合可以作為預設內容與片段相關聯，或者由作者在片段創作期間關聯。
      * [資產(DAM)收集](/help/assets/manage-collections.md) 是片段關聯內容的基礎。
   * （可選）您還可以將片段本身添加到集合中，以幫助跟蹤。

* **片段元資料**

   * 使用 [資產元資料架構](/help/assets/metadata-schemas.md)。
   * 在以下情況下可建立標籤：

      * 建立和創作片段
      * 或更高版本：

         * 通過檢視/編輯片段 **屬性** 從控制台
         * 通過編輯 **元資料** 在片段編輯器中

   >[!CAUTION]
   >
   >元資料處理配置檔案不適用於內容片段。

* **主版**

   * 碎片的一個完整部分

      * 每個內容片段都有一個主實例。
      * 無法刪除主節點。
   * 在片段編輯器中，可訪問首頁 **[變體](/help/assets/content-fragments/content-fragments-variations.md)**。
   * Master不是這樣的變體，而是所有變體的基礎。


* **變數**

   * 特定於編輯目的的片段文本的格式副本；可以與通道相關，但不是強制性的，也可以是臨時的本地修改。
   * 建立為 **母版**，但可根據需要編輯；變異本身之間通常存在內容重疊。
   * 可在片段創作期間定義。
   * 儲存在片段中，以幫助避免內容副本的分散。
   * 變體可以是 [同步](/help/assets/content-fragments/content-fragments-variations.md#synchronizing-with-master) 的子目錄。
   * 可以 [摘要](/help/assets/content-fragments/content-fragments-variations.md#summarizing-text) 快速將文本截斷為預定義長度。
   * 在 [變體](/help/assets/content-fragments/content-fragments-variations.md) 頁籤。

### 使用內容片段創作頁面時的內容 {#in-between-content-when-page-authoring-with-content-fragments}

內容：

* 在使用內容片段時，可在頁面編輯器中使用。
* 是 [在片段流中添加的附加內容](/help/sites-authoring/content-fragments.md#adding-in-between-content) 在頁面上使用/引用它之後。
* 可用於 [使用內容片段時的頁面編輯器](/help/sites-authoring/content-fragments.md)。
* 可以將中間內容添加到任何片段，其中只有一個元素可見。
* 可以使用關聯的內容，也可以使用相應瀏覽器中的資產和/或元件。

>[!CAUTION]
>
>中間內容是頁面內容。 它未儲存在內容片段中。

### 片段要求 {#required-by-fragments}

要建立內容片段，您需要：

* **內容模型**

   * 是 [已使用配置瀏覽器啟用](/help/assets/content-fragments/content-fragments-configuration-browser.md)。
   * 是 [使用工具建立](/help/assets/content-fragments/content-fragments-models.md)。
   * 要求 [建立片段](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments)。
   * 定義片段的結構（標題、內容元素、標籤定義）。
   * 內容模型定義需要一個標題和一個資料元素；其他一切都是可選的。
   * 模型可定義預設內容（如果適用）。
   * 創作片段內容時，作者無法更改定義的結構。
   * 在建立從屬內容片段後對模型所做的更改可能會影響這些內容片段。

要使用內容片段進行頁面創作，您還需要：

* **內容片段元件**

   * 有助於以HTML和/或JSON格式傳遞片段。
   * 要求 [引用頁面上的片段](/help/sites-authoring/content-fragments.md)。
   * 負責碎片的佈局和交付；即頻道。
   * 片段需要一個或多個專用元件來定義佈局並傳遞部分或全部元素/變體和關聯內容。
   * 將片段拖到創作中的頁面上將自動關聯所需的元件。

## 示例用法 {#example-usage}

一個片段及其元素和變體可用於為多個通道建立相干內容。 在設計片段時，您需要考慮在何處使用什麼。
