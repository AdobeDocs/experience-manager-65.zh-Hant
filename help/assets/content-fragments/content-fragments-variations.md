---
title: 變化 - 編寫片段內容
description: 瞭解變體如何使無頭內容更AEM加靈活，它允許您為片段創作內容，然後根據目的建立該內容的變體。
feature: Content Fragments
role: User
exl-id: 50982ede-7ccf-45b2-b0dd-a49d23e0f971
source-git-commit: bb5d39277db10fd8d3b436c8d1f40d9d2010adee
workflow-type: tm+mt
source-wordcount: '2426'
ht-degree: 11%

---

# 變化 - 編寫片段內容{#variations-authoring-fragment-content}

[變體](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) 是內容片段的AEM重要功能，因為它們允許您建立和編輯用於特定渠道和/或場景的主內容副本，從而使無頭內容交付更加靈活。

從 **變體** 頁籤：

* [輸入內容](#authoring-your-content) 你的碎片，
* [建立和管理變體](#managing-variations) 的 **母版** 內容，

根據正在編輯的資料類型執行一系列其他操作；例如：

* [將可視資產插入片段](#inserting-assets-into-your-fragment) （影像）

* 在 [富文本](#rich-text)。 [純文字檔案](#plain-text) 和 [馬爾克當](#markdown) 編輯

* [上傳內容](#uploading-content)

* [查看關鍵統計資訊](#viewing-key-statistics) （關於多行文本）

* [摘要文字](#summarizing-text)

* [與主內容同步變體](#synchronizing-with-master)

>[!CAUTION]
>
>發佈和/或引用片段後，當作AEM者開啟片段以重新進行編輯時，將顯示警告。 這是警告對片段的更改也會影響引用的頁面。

## 創作內容 {#authoring-your-content}

開啟內容片段進行編輯時， **變體** 頁籤 在這裡，您可以為Master或您擁有的任何變體創作內容。 該結構化片段包含在內容模型中定義的各種資料類型的各種欄位。

例如：

![全屏編輯器](assets/cfm-variations-02.png)

您可以：

* 直接在 **變體** 頁籤；每種資料類型都提供不同的編輯選項，例如：

   * 為 **多行文本** 您也可以開啟的 [全屏編輯器](#full-screen-editor) 至：

      * 選擇 [格式](#formats)
      * 查看更多編輯選項( [富文本](#rich-text) 格式)
      * 訪問 [動作](#actions)
   * 對於 **片段引用** 欄位 [編輯內容片段](#fragment-references-edit-content-fragment) 選項可用，具體取決於模型定義。


* 分配 **標籤** 與當前變化的關係；可以添加、更新和刪除標籤

   * [標籤](/help/sites-authoring/tags.md) 在組織碎片時尤其強大，因為它們可用於內容分類和分類。 標籤可用於查找內容（按標籤）和應用批量操作。

      * 搜索標籤將返回帶標籤變體突出顯示的片段。
      * 變體標籤還可用於為特定內容分發網路(CDN)配置檔案（用於CDN快取）分組變體，而不是使用變體名稱。

      例如，可以將相關片段標籤為「聖誕節啟動」，以便僅允許將這些片段作為子集進行瀏覽，或將它們複製以供將來在新資料夾中的另一個啟動時使用。
   >[!NOTE]
   >
   >**標籤** 也可以添加到 **母版** 變體) [元資料](/help/assets/content-fragments/content-fragments-metadata.md)

* [建立和管理變體](#managing-variations) 的 **母版** 內容。

### 全屏編輯器 {#full-screen-editor}

編輯多行文本欄位時，可以開啟全屏編輯器；在實際文本中按一下或按一下，然後選擇以下操作表徵圖：

![全屏編輯器表徵圖](assets/cfm-variations-03.png)

這將開啟全屏文本編輯器：

![全屏編輯器](assets/cfm-variations-fullscreentexteditor.png)

全屏文本編輯器提供：

* 訪問各種 [動作](#actions)
* 取決於 [格式](#formats)，其他格式選項[富文本](#rich-text))

### 動作 {#actions}

以下操作也可用(對於 [格式](#formats))全屏編輯器（即多行文本）開啟時：

* 選擇 [格式](#formats) ([富文本](#rich-text)。 [純文字檔案，](#plain-text) [馬爾克當](#markdown))

* [上載內容](#uploading-content)

* [顯示文本統計資訊](#viewing-key-statistics)

* [與主同步](#synchronizing-with-master) （編輯變體時）

* [摘要文字](#summarizing-text)

### 格式 {#formats}

編輯多行文本的選項取決於所選格式：

* [RTF](#rich-text)
* [純文字](#plain-text)
* [Markdown](#markdown)

當全屏編輯器時，可以選擇格式。

### RTF {#rich-text}

富格文本編輯允許您設定格式：

* 粗體
* 斜體
* 底線
* 對齊：左，中，右
* 項目符號清單
* 編號清單
* 縮進：增加，減少
* 建立/斷開超連結
* 貼上文本/從Word
* 插入表
* 段落樣式：段落，標題1/2/3
* [插入資產](#inserting-assets-into-your-fragment)
* 開啟全屏編輯器，其中提供以下格式設定選項：
   * 搜尋
   * 尋找/取代
   * 拼寫檢查器
   * [註解](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [插入內容片段](#inserting-content-fragment-into-your-fragment);在 **多行文本** 欄位 **允許片段引用**。

的 [動作](#actions) 也可從全屏編輯器訪問。

### 純文字 {#plain-text}

純文字檔案允許快速輸入內容，而無需格式化或標籤資訊。 您還可以開啟全屏編輯器，以便進一步 [動作](#actions)。

>[!CAUTION]
>
>如果您選取「純 **文字** 」 **，可能會遺失您已插入「豐富文字」或「標籤文字」的任何格式、標籤和/或資產******。

### Markdown {#markdown}

>[!NOTE]
>
>有關完整資訊，請參閱 [馬爾克當](/help/assets/content-fragments/content-fragments-markdown.md) 文檔。

這允許您使用標籤來格式化文本。 您可以定義：

* 標題
* 段落和換行符
* 連結
* 影像
* 阻止引號
* 清單
* 強調
* 代碼塊
* 反斜線轉義

您還可以開啟全屏編輯器，以便進一步 [動作](#actions)。

>[!CAUTION]
>
>如果您在 **Rich Text** 和 **** Markdown之間切換，可能會在區塊引號和程式碼區塊中遇到意外的效果，因為這兩種格式在處理方式上可能會有差異。

### 片段參考 {#fragment-references}

如果內容片段模型包含片段引用，則片段作者可能具有其他選項：

* [編輯內容片段](#fragment-references-edit-content-fragment)
* [新內容片段](#fragment-references-new-content-fragment)

![片段參考](assets/cfm-variations-12.png)

#### 編輯內容片段 {#fragment-references-edit-content-fragment}

選項 **編輯內容片段** 將在新窗口頁籤中開啟該片段。

<!--
The option **Edit Content Fragment** will open that fragment in a new editor tab (within the same browser tab).

Selecting the original tab again (for example, **Little Pony Inc.**), will close this secondary tab (in this case, **Adam Smith**).

![Fragment References](assets/cfm-variations-editreference.png)
-->

#### 新內容片段 {#fragment-references-new-content-fragment}

選項 **新內容片段** 就可以建立一個全新的片段。 要實現此目標，將在編輯器中開啟建立內容片段嚮導的變體。

然後，您將能夠通過以下方式建立新片段：

1. 導航到，然後選擇所需的資料夾。
1. 選擇 **下一個**。
1. 指定屬性；例如 **標題**。
1. 選擇 **建立**。
1. 最後：
   1. **完成** 將返回（到原始片段）並引用新片段。
   1. **開啟** 將引用新片段，並在新瀏覽器頁籤中開啟新片段進行編輯。

### 查看關鍵統計資訊 {#viewing-key-statistics}

當全螢幕編輯器開啟時，「文字統計 **資料** 」動作會顯示一系列有關文字的資訊。

例如：

![statistics](assets/cfm-variations-04.png)

### 正在上載內容 {#uploading-content}

要簡化創作內容片段的過程，您可以上載在外部編輯器中準備的文本，並直接將其添加到片段中。

### 摘要文本 {#summarizing-text}

摘要文本旨在幫助用戶將其文本的長度縮短到預定義的單詞數，同時保留關鍵點和總體意義。

>[!NOTE]
>
>在更技術性的層面上，系統保留它所評價的句子 *資訊密度和唯一性的最佳比* 根據具體算法。

>[!CAUTION]
>
>內容片段必須具有有效的語言資料夾（ISO代碼）作為祖先；這用於確定要使用的語言模型。
>
>比如說， `en/` 如下所示：
>
>  `/content/dam/my-brand/en/path-down/my-content-fragment`

>[!CAUTION]
英語是開箱即用的。
其他語言可作為包共用中的語言模型包：
* [French(fr)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)
* [German(de)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
* [Italian(it)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
* [Spanish(es)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
>


1. 選擇 **母版** 或所需的變體。
1. 開啟全屏編輯器。

1. 選擇 **摘要文本** 的子菜單。

   ![總結](assets/cfm-variations-05.png)

1. 指定目標字數並選擇 **開始**:
1. 原始文本與建議的摘要並排顯示：

   * 任何要刪除的句子都以紅色突出顯示，並帶有刪除。
   * 按一下任何突出顯示的句子，將其保留在摘要內容中。
   * 按一下任何未加亮的句子以將其清除。

1. 選擇 **摘要** 確認更改。

1. 原始文本與建議的摘要並排顯示：

   * 任何要刪除的句子都以紅色突出顯示，並帶有刪除。
   * 按一下任何突出顯示的句子，將其保留在摘要內容中。
   * 按一下任何未加亮的句子以將其清除。
   * 摘要統計資訊如下所示： **實際** 和 **目標**-
   * 你可以 **預覽** 更改。

   ![摘要比較](assets/cfm-variations-06.png)

### 注釋內容片段 {#annotating-a-content-fragment}

要注釋片段：

1. 選擇 **母版** 或所需的變體。

1. 開啟全屏編輯器。

1. 的 **注釋** 表徵圖。 如果需要，可以選擇一些文本。

   ![注釋](assets/cfm-variations-07.png)

1. 將會開啟對話框。 在此可以輸入注釋。

   ![注釋](assets/cfm-variations-07a.png)

1. 選擇 **應用** 對話框。

   ![注釋](assets/cfm-variations-annotations-apply-icon.png)

   如果注釋已應用於選定文本，則該文本將保持高亮顯示。

   ![注釋](assets/cfm-variations-07b.png)

1. 關閉全屏編輯器，注釋仍會突出顯示。 如果選中，將開啟一個對話框，以便您可以進一步編輯注釋。

1. 選取&#x200B;**儲存**。

1. 關閉全屏編輯器，注釋仍會突出顯示。 如果選中，將開啟一個對話框，以便您可以進一步編輯注釋。

   ![注釋](assets/cfm-variations-07c.png)

### 查看、編輯和刪除注釋 {#viewing-editing-deleting-annotations}

註解:

* 在編輯器的全屏和正常模式下，由文本上的突出顯示指示。 然後，可以通過按一下將重新開啟對話框的突出顯示文本來查看、編輯和/或刪除注釋的全部詳細資訊。

   >[!NOTE]
   如果已將多個注釋應用於一個文本，則提供下拉選擇器。

* 刪除應用注釋的整個文本時，注釋也會被刪除。

* 通過選擇 **注釋** 頁籤。

   ![附註](assets/cfm-variations-08.png)

* 可以在中查看和刪除 [時間軸](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments) 的子菜單。

### 將資產插入片段 {#inserting-assets-into-your-fragment}

要簡化創作內容片段的過程，可以添加 [資產](/help/assets/manage-assets.md) （影像）直接到片段。

將不加任何格式，將其添加到片段的段落序列中；在 [頁面上使用/引用片段](/help/sites-authoring/content-fragments.md)。

>[!CAUTION]
不能在引用頁面上移動或刪除這些資產，必須在片段編輯器中完成此操作。
但是，必須在 [頁面編輯器](/help/sites-authoring/content-fragments.md)。 片段編輯器中資產的表示純粹是為了創作內容流。

>[!NOTE]
有多種方法可添加 [影像](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) 到片段和/或頁面。

1. 將游標置於要添加影像的位置。
1. 使用「插 **入資產** 」圖示開啟搜尋對話方塊。

   ![插入資產表徵圖](assets/cfm-variations-09.png)

1. 在對話框中，您可以：

   * 導航到DAM中的所需資產
   * 在DAM中搜索資產

   找到後，通過按一下縮略圖來選擇所需資產。

1. 使用 **「選取** 」將資產新增至目前位置之內容片段的段落系統。

   >[!CAUTION]
   如果新增資產後，您將格式變更為：
   * **純文字檔案**:資產將完全從碎片中丟失。
   * **Markdown**:資產將不可見，但當您返回 **Rich Text時，資產仍會存在**。


### 將內容片段插入片段 {#inserting-content-fragment-into-your-fragment}

要簡化創作內容片段的過程，您還可以將另一個內容片段添加到您的片段中。

它們將被添加為引用，位於片段的當前位置。

>[!NOTE]
當 **多行文本** 已配置 **允許片段引用**。

>[!CAUTION]
不能在引用頁面上移動或刪除這些資產，必須在片段編輯器中完成此操作。
但是，必須在 [頁面編輯器](/help/sites-authoring/content-fragments.md)。 片段編輯器中資產的表示純粹是為了創作內容流。

>[!NOTE]
有多種方法可添加 [影像](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) 到片段和/或頁面。

1. 將游標置於要添加片段的位置。
1. 使用 **插入內容片段** 表徵圖開啟搜索對話框。

   ![插入內容片段表徵圖](assets/cfm-variations-13.png)

1. 在對話框中，您可以：

   * 導航到「資產」資料夾中所需的片段
   * 搜索片段

   找到後，通過按一下縮略圖來選擇所需的片段。

1. 使用 **選擇** 將對所選內容片段的引用添加到當前內容片段（位於當前位置）。

   >[!CAUTION]
   如果在添加對另一個片段的引用後，將格式更改為：
   * **純文字檔案**:從碎片中將完全丟失引用。
   * **馬爾克當**:引用將保留。


## 管理變體 {#managing-variations}

### 建立變體 {#creating-a-variation}

變體允許您 **母版** 內容，並根據目的（如果需要）對其進行更改。

要建立新變體，請執行以下操作：

1. 開啟片段並確保側面板可見。
1. 選擇 **變體** 的上界。
1. 選擇 **建立變體**。
1. 將會開啟對話方塊，指定新變 **數的****「標題」(Title)和「說明」(Description** )。
1. 選擇 **添加**;片段 **Master** 將會複製到新的變數，現在會開啟供編 [輯](#editing-a-variation)。

   >[!NOTE]
   建立新變體時，始終 **母版** 而不是當前開啟的變體。

   >[!NOTE]
   建立新變體時， **標籤** 當前分配給 **母版** 變體會複製到新變體中。

### 編輯變體 {#editing-a-variation}

可以在以下任一操作之後更改變體內容：

* [建立變體](#creating-a-variation)。
* 開啟現有片段，然後從側面板中選擇所需的變數。

![編輯變體](assets/cfm-variations-10.png)

### 更名變體 {#renaming-a-variation}

要更名現有變體，請執行以下操作：

1. 開啟片段並選擇 **變體** 從側面板上。
1. 選擇所需的變體。
1. 選擇 **更名** 從 **操作** 下拉。

1. 在產生的對 **話方塊中** ，輸入新的「 **** 標題」和/或「說明」。

1. 確認 **更名** 操作。

>[!NOTE]
這隻影響變體 **標題**。

### 刪除變體 {#deleting-a-variation}

要刪除現有變體，請執行以下操作：

1. 開啟片段並選擇 **變體** 從側面板上。
1. 選擇所需的變體。
1. 選擇 **刪除** 從 **操作** 下拉。

1. 確認 **刪除** 對話框。

>[!NOTE]
無法刪除 **母版**。

### 與主節點同步 {#synchronizing-with-master}

**母版** 是內容片段的一個組成部分，根據定義，它保留內容的主副本，而變體保留該內容的個別更新和定製版本。 更新「主資料」時，這些更改可能也與變體相關，因此需要傳播到它們。

編輯變體時，您有權訪問用於將變體的當前元素與主元素同步的操作。 這允許您自動將對「母版」所做的更改複製到所需的變體。

>[!CAUTION]
同步僅可用於將更改從 *主&#x200B;**版複製**到變化*。
將只同步變體的當前元素。
同步僅在 **多行文本** 資料類型。
將變 *更從變更傳輸&#x200B;**至Master*** ，不提供選項。

<!-- needs new screenshot for synchronize effect -->

1. 在片段編輯器中開啟內容片段。 確保 **母版** 已編輯。

1. 選擇特定的變體，然後從以下任一位置選擇適當的同步操作：

   * 這樣 **操作** 下拉選擇器 —  **將當前元素與主元素同步**

      ![與主同步](assets/cfm-variations-11a.png)

   * 全屏編輯器的工具欄 —  **與主同步**

      ![與主同步](assets/cfm-variations-11b.png)

1. 母版和變體將並排顯示：

   * 綠色表示添加的內容（到變體）
   * 紅色表示已刪除（來自變體）的內容
   * 藍色表示替換的文本

   ![與主同步](assets/cfm-variations-11c.png)

1. 選擇 **同步**，將更新並顯示變體。
