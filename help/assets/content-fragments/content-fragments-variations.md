---
title: 變化 - 編寫片段內容
description: 了解變異如何讓您在AEM中的無頭式內容更有彈性，方法是允許您為片段製作內容，然後根據目的建立該內容的變異。
feature: Content Fragments
role: User
exl-id: 50982ede-7ccf-45b2-b0dd-a49d23e0f971
source-git-commit: bb5d39277db10fd8d3b436c8d1f40d9d2010adee
workflow-type: tm+mt
source-wordcount: '2426'
ht-degree: 11%

---

# 變化 - 編寫片段內容{#variations-authoring-fragment-content}

[變異](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) 是AEM內容片段的重要功能，因為它們可讓您建立和編輯主要內容的復本，以用於特定頻道和/或情境，讓無頭式內容傳送更具彈性。

從 **變異** 標籤：

* [輸入內容](#authoring-your-content) 對於你的片段，
* [建立和管理變數](#managing-variations) 的 **主版** 內容，

根據要編輯的資料類型執行一系列其他動作；例如：

* [將視覺化資產插入片段](#inserting-assets-into-your-fragment) （影像）

* 在之間選擇 [RTF](#rich-text), [純文字](#plain-text) 和 [Markdown](#markdown) 編輯

* [上傳內容](#uploading-content)

* [查看關鍵統計資訊](#viewing-key-statistics) （關於多行文本）

* [摘要文字](#summarizing-text)

* [將變數與主內容同步](#synchronizing-with-master)

>[!CAUTION]
>
>發佈和/或參考片段後，製作者開啟片段並再次編輯時AEM會顯示警告。 這將警告對片段的變更也會影響參考的頁面。

## 編寫內容 {#authoring-your-content}

當您開啟內容片段進行編輯時， **變異** 標籤預設為開啟。 您可以在此為「主版」或您擁有的任何變體製作內容。 結構化片段包含內容模型中定義之各種資料類型的各種欄位。

例如：

![全螢幕編輯器](assets/cfm-variations-02.png)

您可以：

* 直接在 **變異** 標籤；每種資料類型提供不同的編輯選項，例如：

   * for **多行文本** 您也可以開啟的欄位 [全螢幕編輯器](#full-screen-editor) 至：

      * 選取 [格式](#formats)
      * 查看更多編輯選項( [RTF](#rich-text) 格式)
      * 存取範圍 [動作](#actions)
   * 針對 **片段參考** 欄位 [編輯內容片段](#fragment-references-edit-content-fragment) 選項可供使用，具體取決於模型定義。


* 指派 **標籤** 對當前變化的影響；可新增、更新及移除標籤

   * [標籤](/help/sites-authoring/tags.md) 在組織片段時，效能尤其強大，因為片段可用於內容分類和分類。 標籤可用來尋找內容（依標籤）並套用大量作業。

      * 搜尋標籤時，會傳回片段，並反白顯示標籤的變數。
      * 變異標籤也可用來將特定內容傳遞網路(CDN)設定檔的變異分組（用於CDN快取），而非使用變異名稱。

      例如，您可以將相關片段標籤為「聖誕節啟動」，以允許僅以子集形式瀏覽這些片段，或複製這些片段，以便與新資料夾中其他未來啟動搭配使用。
   >[!NOTE]
   >
   >**標籤** 也可以新增(至 **主版** 變異) [中繼資料](/help/assets/content-fragments/content-fragments-metadata.md)

* [建立和管理變數](#managing-variations) 的 **主版** 內容。

### 全螢幕編輯器 {#full-screen-editor}

編輯多行文本欄位時，可以開啟全螢幕編輯器；點選或按一下實際文字，然後選取下列動作圖示：

![全螢幕編輯器圖示](assets/cfm-variations-03.png)

這會開啟全螢幕文字編輯器：

![全螢幕編輯器](assets/cfm-variations-fullscreentexteditor.png)

全螢幕文字編輯器提供：

* 存取各種 [動作](#actions)
* 視 [格式](#formats)，其他格式選項([RTF](#rich-text))

### 動作 {#actions}

下列動作也可供使用(適用於 [格式](#formats))，當全螢幕編輯器（即多行文字）開啟時：

* 選取 [格式](#formats) ([RTF](#rich-text), [純文字，](#plain-text) [Markdown](#markdown))

* [上傳內容](#uploading-content)

* [顯示文本統計資訊](#viewing-key-statistics)

* [與主版同步](#synchronizing-with-master) （編輯變數時）

* [摘要文字](#summarizing-text)

### 格式 {#formats}

用於編輯多行文本的選項取決於所選的格式：

* [RTF](#rich-text)
* [純文字](#plain-text)
* [Markdown](#markdown)

全螢幕編輯器時可選取格式。

### RTF {#rich-text}

RTF編輯可讓您設定格式：

* 粗體
* 斜體
* 底線
* 對齊方式：左，中，右
* 項目符號清單
* 編號清單
* 縮排：增加，減少
* 建立/中斷超連結
* 貼上文字/來自字詞
* 插入表格
* 段落樣式：第1/2/3段
* [插入資產](#inserting-assets-into-your-fragment)
* 開啟全螢幕編輯器，其中提供下列格式選項：
   * 搜尋
   * 尋找/取代
   * 拼字檢查程式
   * [註解](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [插入內容片段](#inserting-content-fragment-into-your-fragment);在 **多行文本** 欄位已設定 **允許片段參考**.

此 [動作](#actions) 也可從全螢幕編輯器存取。

### 純文字 {#plain-text}

純文字檔案允許快速輸入內容，而不需格式設定或標籤資訊。 您也可以開啟全螢幕編輯器以進一步 [動作](#actions).

>[!CAUTION]
>
>如果您選取「純 **文字** 」 **，可能會遺失您已插入「豐富文字」或「標籤文字」的任何格式、標籤和/或資產******。

### Markdown {#markdown}

>[!NOTE]
>
>如需完整資訊，請參閱 [Markdown](/help/assets/content-fragments/content-fragments-markdown.md) 檔案。

這可讓您使用Markdown來設定文字格式。 您可以定義：

* 標題
* 段落和分行
* 連結
* 影像
* 塊引號
* 清單
* 強調
* 程式碼區塊
* 反斜線逸出

您也可以開啟全螢幕編輯器以進一步 [動作](#actions).

>[!CAUTION]
>
>如果您在 **Rich Text** 和 **** Markdown之間切換，可能會在區塊引號和程式碼區塊中遇到意外的效果，因為這兩種格式在處理方式上可能會有差異。

### 片段參考 {#fragment-references}

如果內容片段模型包含片段參考，您的片段作者可能有其他選項：

* [編輯內容片段](#fragment-references-edit-content-fragment)
* [新內容片段](#fragment-references-new-content-fragment)

![片段參考](assets/cfm-variations-12.png)

#### 編輯內容片段 {#fragment-references-edit-content-fragment}

選項 **編輯內容片段** 會在新視窗索引標籤中開啟該片段。

<!--
The option **Edit Content Fragment** will open that fragment in a new editor tab (within the same browser tab).

Selecting the original tab again (for example, **Little Pony Inc.**), will close this secondary tab (in this case, **Adam Smith**).

![Fragment References](assets/cfm-variations-editreference.png)
-->

#### 新內容片段 {#fragment-references-new-content-fragment}

選項 **新內容片段** 將允許您建立全新片段。 為此，將在編輯器中開啟建立內容片段精靈的變數。

然後，您將能夠通過以下方式建立新片段：

1. 導覽至，然後選取所需的資料夾。
1. 選取 **下一個**.
1. 指定屬性；例如 **標題**.
1. 選取 **建立**.
1. 最後：
   1. **完成** 將返回（到原始片段）並參考新片段。
   1. **開啟** 將參考新片段，以及在新瀏覽器索引標籤中開啟新片段以供編輯。

### 查看關鍵統計資訊 {#viewing-key-statistics}

當全螢幕編輯器開啟時，「文字統計 **資料** 」動作會顯示一系列有關文字的資訊。

例如：

![statistics](assets/cfm-variations-04.png)

### 上傳內容 {#uploading-content}

若要簡化製作內容片段的程式，您可以上傳在外部編輯器中準備的文字，並直接將其新增至片段。

### 摘要文字 {#summarizing-text}

摘要文字旨在協助使用者將文字長度縮短為預先定義的字數，同時保留關鍵點和整體意義。

>[!NOTE]
>
>在更技術性的層面上，系統會保留其評分為提供的句子 *資訊密度和唯一性的最佳比* 根據具體算法。

>[!CAUTION]
>
>內容片段必須具備有效的語言資料夾（ISO代碼）作為上階；這可用來決定要使用的語言模型。
>
>例如， `en/` 如下列路徑所示：
>
>  `/content/dam/my-brand/en/path-down/my-content-fragment`

>[!CAUTION]
英文是現成可用的。
其他語言則可從Package Share中作為語言模型包：
* [French(fr)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)
* [German(de)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
* [Italian(it)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
* [Spanish(es)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
>


1. 選擇 **主版** 或所需的變數。
1. 開啟全螢幕編輯器。

1. 選擇 **摘要文字** 的上界。

   ![摘要](assets/cfm-variations-05.png)

1. 指定目標字數並選取 **開始**:
1. 原始文本與建議的總結並排顯示：

   * 任何要刪除的句子都以紅色突出顯示，並帶有字串。
   * 按一下任何醒目提示的句子，將其保留在摘要內容中。
   * 按一下任何未加亮的句子以將其刪除。

1. 選擇 **摘要** 以確認變更。

1. 原始文本與建議的總結並排顯示：

   * 任何要刪除的句子都以紅色突出顯示，並帶有字串。
   * 按一下任何醒目提示的句子，將其保留在摘要內容中。
   * 按一下任何未加亮的句子以將其刪除。
   * 顯示總結統計資訊： **實際** 和 **目標**-
   * 您可以 **預覽** 變更。

   ![摘要比較](assets/cfm-variations-06.png)

### 為內容片段加上註解 {#annotating-a-content-fragment}

若要注釋片段：

1. 選擇 **主版** 或所需的變數。

1. 開啟全螢幕編輯器。

1. 此 **注釋** 圖示。 您可以視需要選取一些文字。

   ![注釋](assets/cfm-variations-07.png)

1. 對話方塊將會開啟。 您可以在此輸入注釋。

   ![注釋](assets/cfm-variations-07a.png)

1. 選擇 **套用** 對話框。

   ![注釋](assets/cfm-variations-annotations-apply-icon.png)

   如果將注釋應用於選定文本，則該文本將保持突出顯示。

   ![注釋](assets/cfm-variations-07b.png)

1. 關閉全螢幕編輯器時，仍會強調顯示註解。 如果選中，將開啟一個對話框，以便您可以進一步編輯注釋。

1. 選取&#x200B;**儲存**。

1. 關閉全螢幕編輯器時，仍會強調顯示註解。 如果選中，將開啟一個對話框，以便您可以進一步編輯注釋。

   ![注釋](assets/cfm-variations-07c.png)

### 查看、編輯、刪除注釋 {#viewing-editing-deleting-annotations}

註解:

* 在編輯器的全螢幕和一般模式中，以文字上的醒目提示指示。 然後，可通過按一下突出顯示的文本來查看、編輯和/或刪除注釋的完整詳細資訊，這將重新開啟對話框。

   >[!NOTE]
   如果已將多個註解套用至一個文字，則提供下拉式選取器。

* 刪除應用了注釋的整個文本時，注釋也會被刪除。

* 您可以選取 **註解** 頁簽。

   ![附註](assets/cfm-variations-08.png)

* 可在 [時間表](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments) ，針對所選片段。

### 在片段中插入資產 {#inserting-assets-into-your-fragment}

若要簡化編寫內容片段的程式，您可以新增 [資產](/help/assets/manage-assets.md) （影像）直接傳至片段。

這些檔案將添加到片段的段落序列中，而無需任何格式；若 [頁面上使用/參考片段](/help/sites-authoring/content-fragments.md).

>[!CAUTION]
無法在參考頁面上移動或刪除這些資產，必須在片段編輯器中完成此操作。
不過，必須在 [頁面編輯器](/help/sites-authoring/content-fragments.md). 片段編輯器中資產的表示純粹是為了編寫內容流程。

>[!NOTE]
有多種方法可新增 [影像](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) 至片段和/或頁面。

1. 將游標置於要添加影像的位置。
1. 使用「插 **入資產** 」圖示開啟搜尋對話方塊。

   ![插入資產圖示](assets/cfm-variations-09.png)

1. 在對話方塊中，您可以：

   * 導覽至DAM中的必要資產
   * 在DAM中搜尋資產

   找到後，按一下縮圖以選取所需的資產。

1. 使用 **「選取** 」將資產新增至目前位置之內容片段的段落系統。

   >[!CAUTION]
   如果新增資產後，您將格式變更為：
   * **純文字檔案**:資產將完全從碎片中丟失。
   * **Markdown**:資產將不可見，但當您返回 **Rich Text時，資產仍會存在**。


### 在片段中插入內容片段 {#inserting-content-fragment-into-your-fragment}

若要簡化編寫內容片段的程式，您也可以新增其他內容片段至您的片段。

它們會新增為參考，位於您片段的目前位置。

>[!NOTE]
此選項可在 **多行文本** 已設定為 **允許片段參考**.

>[!CAUTION]
無法在參考頁面上移動或刪除這些資產，必須在片段編輯器中完成此操作。
不過，必須在 [頁面編輯器](/help/sites-authoring/content-fragments.md). 片段編輯器中資產的表示純粹是為了編寫內容流程。

>[!NOTE]
有多種方法可新增 [影像](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) 至片段和/或頁面。

1. 將游標置於要添加片段的位置。
1. 使用 **插入內容片段** 表徵圖以開啟搜索對話框。

   ![插入內容片段圖示](assets/cfm-variations-13.png)

1. 在對話方塊中，您可以：

   * 導覽至「資產」資料夾中的必要片段
   * 搜尋片段

   找到後，按一下縮圖以選取所需的片段。

1. 使用 **選擇** 將參考新增至您目前的內容片段（在目前位置）。

   >[!CAUTION]
   如果在將參考新增至另一個片段後，您將格式變更為：
   * **純文字**:引用將完全從片段中丟失。
   * **Markdown**:參考將保留。


## 管理變數 {#managing-variations}

### 建立變異 {#creating-a-variation}

變數可讓您 **主版** 內容，並視需要加以變更。

要建立新變數：

1. 開啟您的片段，並確認側面板可見。
1. 選擇 **變異** 從側面板的表徵圖欄中。
1. 選擇 **建立變異**.
1. 將會開啟對話方塊，指定新變 **數的****「標題」(Title)和「說明」(Description** )。
1. 選擇 **添加**;片段 **Master** 將會複製到新的變數，現在會開啟供編 [輯](#editing-a-variation)。

   >[!NOTE]
   建立新變異時，一律 **主版** 會複製，而非目前開啟的變數。

   >[!NOTE]
   建立新變數時，所有 **標籤** 目前已指派給 **主版** 變異會複製到您的新變異。

### 編輯變異 {#editing-a-variation}

您可以在下列任一項之後，變更變異內容：

* [建立變異](#creating-a-variation).
* 開啟現有片段，然後從側面板選取所需的變數。

![編輯變異](assets/cfm-variations-10.png)

### 更名變數 {#renaming-a-variation}

要更名現有變數：

1. 開啟您的片段並選取 **變異** 從側面板。
1. 選取所需的變數。
1. 選擇 **重新命名** 從 **動作** 下拉。

1. 在產生的對 **話方塊中** ，輸入新的「 **** 標題」和/或「說明」。

1. 確認 **重新命名** 動作。

>[!NOTE]
這只會影響變數 **標題**.

### 刪除變數 {#deleting-a-variation}

要刪除現有變數：

1. 開啟您的片段並選取 **變異** 從側面板。
1. 選取所需的變數。
1. 選擇 **刪除** 從 **動作** 下拉。

1. 確認 **刪除** 動作。

>[!NOTE]
無法刪除 **主版**.

### 與主伺服器同步 {#synchronizing-with-master}

**主版** 是內容片段的必要部分，並且根據定義，它保留內容的主副本，而變化保留該內容的個別更新和定製版本。 更新主版時，這些變更也可能與變更相關，因此需要傳播至變更。

編輯變體時，您可以存取動作，將變體的目前元素與主版同步。 這可讓您自動將對Master所做的變更複製到所需的變數。

>[!CAUTION]
同步僅可用於將更改從 *主&#x200B;**版複製**到變化*。
只會同步變數的目前元素。
同步只適用於 **多行文本** 資料類型。
將變 *更從變更傳輸&#x200B;**至Master*** ，不提供選項。

<!-- needs new screenshot for synchronize effect -->

1. 在片段編輯器中開啟內容片段。 確保 **主版** 已編輯。

1. 選擇特定變數，然後從以下任一項選擇適當的同步操作：

   * the **動作** 下拉式選取器 —  **與主版同步目前元素**

      ![與主同步](assets/cfm-variations-11a.png)

   * 全螢幕編輯器的工具列 —  **與主版同步**

      ![與主同步](assets/cfm-variations-11b.png)

1. 主版和變異會並排顯示：

   * 綠色表示已新增的內容（至變數）
   * 紅色表示內容已移除（從變數中）
   * 藍色表示已替換的文字

   ![與主同步](assets/cfm-variations-11c.png)

1. 選擇 **同步**，則會更新並顯示變數。
