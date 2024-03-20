---
title: 使用內容片段編寫內容頁面
description: AEM內容片段可讓您設計、建立、組織和使用獨立於頁面的內容。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
exl-id: d5dad844-80ca-4ace-a082-38d892d9ffe2
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1138'
ht-degree: 3%

---

# 使用內容片段編寫頁面{#page-authoring-with-content-fragments}

Adobe Experience Manager(AEM)內容片段會建 [立並管理為不受頁面影響的資產](/help/assets/content-fragments/content-fragments.md)。

它們可讓您建立管道中性內容，連同（可能特定於管道）變數。 接著，您就可以在編寫內容頁面時，使用這些片段及其變數。

結構化內容片段與更新的JSON匯出工具搭配使用，也可用來透過Content Services將AEM內容傳送至AEM頁面以外的管道。

>[!NOTE]
>
>**內容片段** 和 **[體驗片段](/help/sites-authoring/experience-fragments.md)** 是AEM中的不同功能：
>
>* **內容片段** 是可編輯內容，主要為文字和相關影像。 它們是純內容，沒有設計和配置。
>* **體驗片段** 是完全佈局的內容；網頁的片段。
>
>體驗片段可以包含內容片段形式的內容，反之則不行。

>[!CAUTION]
>
>此頁面必須透過以下方式讀取： [使用內容片段](/help/assets/content-fragments/content-fragments.md) （和相關頁面），因為它會介紹基本術語和概念，以及建立和管理片段。

內容片段會啟用：

* **行銷和行銷活動策略**

   * 透過集中管理的內容片段稽核內容。

* **Creative Pro**

   * 透過與內容片段相關聯的集合追蹤創意資產。

* **複製寫入者**

   * 在AEM內容片段編輯器中寫入。
   * 可以建立內容變數。
   * 可以關聯相關內容與內容片段。
   * 可以使用版本設定/工作流程。
   * 可共用內容片段。
   * 可集中管理翻譯。

* **製作者和歷程管理員**

   * 從預先定義的片段和AEM中編寫的變數中選取。
   * 當復本作者和創意人員以集中管理的片段和資產進行更新時，可依賴片段和相關內容始終保持最新。
   * 可以依賴因關聯性而管理的相關媒體內容。
   * 可以立即建立隨選內容變數，同時仍然確保這些變數在片段中受到集中管理。

## 新增內容片段至您的頁面 {#adding-a-content-fragment-to-your-page}

1. 開啟您的頁面以進行編輯。

1. 新增 **內容片段** 元件；從 **元件** 瀏覽器或 **插入新元件**.

1. 您可以執行下列兩個動作中的一個:

   * 開啟 **資產** 瀏覽器和篩選器 **內容片段** （預設值為「影像」）。 然後將所需的片段拖曳到元件例項上。

   * 選取內容片段元件，然後 **設定** 工具列中的。 在對話方塊中，您可以開啟選取對話方塊以瀏覽並選取所需的專案 **內容片段**.

   >[!NOTE]
   >
   >另一種方法是將特定的內容片段直接拖曳到頁面上。 這會自動建立關聯的元件（內容片段）。

1. 最初，內容來自 **主要** 元素和 **主版** （變數）會顯示。 您可以 [選取其他元素和/或變數](#selecting-the-element-or-variation) 視需要。

   ![cfm-6420-01](assets/cfm-6420-01.png)

   >[!NOTE]
   >
   >如需進一步編輯功能的詳細資訊，請參閱下列內容：
   >
   >
   >
   >    * [回應式版面](/help/sites-authoring/responsive-layout.md)
   >    * [編輯頁面內容](/help/sites-authoring/editing-content.md)
   >
   >

### 選取元素或變數 {#selecting-the-element-or-variation}

開啟片段的 **設定** 對話方塊，讓您可以設定片段以在目前頁面上使用。 此對話方塊取決於所使用的元件。

在適當的組態對話方塊中，您可以選取可用的引數，包括：

* **內容片段**

  指定要使用的片段。

* **顯示模式**：

   * **單一文字元素**

   * **多個元素**

* **元素**

   * 預設 **主要** 一律可用。
   * 如果片段是以適當的範本建立的，則此選項可供選擇。

  >[!NOTE]
  >
  >可用的元素視使用的範本而定。

* **變異**

   * 預設 **主版** 一律可用。
   * 如果變數是為片段而建立，則可供選取。

* **段落**：指定要包含的段落範圍：

   * **全部**
   * **Range**：例如， `1`， `3-5`， `9-*`

      * **將標題處理為它們自己的段落**

* **將標題處理為它們自己的段落**

### 快速連線到片段編輯器 {#quick-connection-to-fragment-editor}

您可以使用開啟片段來源以進行編輯（資產） **編輯** 圖示來切換元件。 這可讓您 [編輯和管理內容片段](/help/assets/content-fragments/content-fragments.md).

>[!CAUTION]
>
>一如既往，編輯片段來源可能會影響參照該內容片段的所有頁面。

### 新增中間內容 {#adding-in-between-content}

將特定內容片段新增到頁面時， **將元件拖曳到這裡** 片段中每個HTML段落（和上/下）之間的預留位置。

這可讓您新增額外內容 [中間（即中間內容）](/help/assets/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments) 片段內容（在任何可用點），不必變更根片段。

針對中間內容，您可以：

* 從新增元件 [元件瀏覽器](/help/sites-authoring/author-environment-tools.md#components-browser).
* 從新增資產 [資產瀏覽器](/help/sites-authoring/author-environment-tools.md#assets-browser).
* 使用 [關聯內容](#using-associated-content) 作為中間內容的來源。

>[!CAUTION]
>
>中間內容是頁面內容。 它不會儲存在內容片段中。

![cfm-6420-02](assets/cfm-6420-02.png)

>[!NOTE]
>
>您也可以 [將視覺資產（影像）插入片段本身](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
>
>插入片段本身的視覺資產會附加至片段中前面的段落。 這表示您無法在視覺資產與前一段落之間放置中間內容。

>[!CAUTION]
>
>將中間內容新增至頁面上的內容片段後，變更基礎內容片段的結構（即在內容片段編輯器中）可能會導致錯誤/未預期的結果。
>
>發生此情況時，中間內容會維持不變：
>
>* 中間元件在片段流程中的元件順序內有絕對位置。 此位置不會變更，即使片段中段落的內容變更亦然。
>
>  這可能使其看起來像是相對位置已變更，因為中間段落與它們旁邊的（片段）段落沒有上下文關係。
>* 除非兩個段落結構衝突；在這種情況下，不會顯示中間內容（儘管它仍然存在於內部）。
>

### 使用關聯內容 {#using-associated-content}

如果您有 [關聯內容](/help/assets/content-fragments/content-fragments-assoc-content.md) 使用 [內容片段](/help/assets/content-fragments/content-fragments.md)，這些資產可從側面板使用（在您將片段放在內容頁面後）。 關聯內容實際上是中間內容的特 [殊內容來源](#adding-in-between-content)。

>[!NOTE]
>
>有多種方法可新增 [視覺資產（例如影像）](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) 至片段和/或頁面。

>[!NOTE]
>
>如果您在一個頁面上有多個內容片段，請 **關聯內容** 索引標籤會顯示適用於所有片段的資產。

將具有關聯內容的片段新增到頁面後，會新增索引標籤(**關聯內容**)即會在側面板中開啟。

從這裡，您可以將資產拖曳至所需位置（可拖曳至現有元件，或拖曳至建立適當元件的所需位置）：

![cfm-6420-03](assets/cfm-6420-03.png)

### 插入到片段中的資產 {#assets-inserted-into-the-fragment}

如果資產（例如影像）已插入片段本身，則頁面編輯器中用於編輯這些資產的選項會受到限制。 <!-- Removed link as it was a 404 on helpx -->

例如，您可以對影像執行

* 裁切、旋轉或翻轉影像。
* 新增標題或替代文字。
* 指定大小。
* 您也可以配置配置。

您必須在片段編輯器中執行其他變更，例如移動、複製、刪除。

### 發佈 {#publishing}

片段必須發佈，才能用於您已發佈的網頁：

* 片段可以在以下時間後發佈： [在資產控制檯中建立片段](/help/assets/content-fragments/content-fragments.md#publishingandreferencingafragment).
* 如果 *未發佈的片段* 用於正在發佈的頁面，片段現在也可以發佈。
