---
title: 變數——製作片段內容
seo-title: 變數——製作片段內容
description: 變數可讓您為片段製作內容，然後根據用途建立該內容的變數（如有需要）。
seo-description: 變數可讓您為片段製作內容，然後根據用途建立該內容的變數（如有需要）。
uuid: 0844f271-79bc-4f76-8031-d388b81d6feb
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: content-fragments
content-type: reference
discoiquuid: 324df1da-78fa-460f-a744-3504259f1d4a
docset: aem65
translation-type: tm+mt
source-git-commit: 9d5fa8b85f6724097e34edd66745e0daf95d66cc

---


# 變數——製作片段內容{#variations-authoring-fragment-content}

[變數](/help/assets/content-fragments.md#constituent-parts-of-a-content-fragment) 是內容片段的重要功能，因為它們可讓您建立和編輯主要內容的副本，以用於特定頻道和／或藍本。

從「變 **數** 」標籤，您可以：

* [輸入片段的內容](#authoring-your-content) ,
* [建立並管理主版](#managing-variations) ( **Master** )內容的變化

根據正在編輯的資料類型執行一系列其他操作；例如：

* [將視覺資產插入您的片段](#inserting-assets-into-your-fragment) （影像）
* 在富格 [文字](#rich-text)、純 [文字和標籤](#plain-text) 之間選 [](#markdown) 擇

* [上傳內容](#uploading-content)

* [檢視關鍵統計](#viewing-key-statistics) （關於多行文字）
* [摘要文字](#summarizing-text)

* [使變化與主版內容同步](#synchronizing-with-master)

>[!CAUTION]
>
>發佈和／或參考片段後，當作者開啟片段以進行重新編輯時，AEM會顯示警告。 這會警告對片段所做的變更也會影響參照的頁面。

## 製作內容 {#authoring-your-content}

當您開啟內容片段進行編輯時，預 **設會開啟** 「變數」標籤。 您可以在這裡為「主版」或您擁有的任何變體製作內容。 您可以：

* 直接在「變化」索引標籤 **中編輯**
* 開啟全 [螢幕編輯器](#full-screen-editor) :

   * 選擇格 [式](#formats)
   * 檢視更多編輯選項(適用於 [Rich Text格式](#rich-text) )

   * 存取一系列動 [作](#actions)

例如：

* 編輯簡單片段

   簡單片段包含一個多行文字欄位（可從全螢幕編輯器新增視覺資產）。

   ![cfm-6420-21](assets/cfm-6420-21.png)

* 使用結構化內容編輯片段

   結構化片段包含在內容模型中定義的各種不同資料類型的欄位。 對於任何多行欄位，全熒 [幕編輯器都可使用](#full-screen-editor) 。

   ![cfm-6420-16](assets/cfm-6420-16.png)

### 全螢幕編輯器 {#full-screen-editor}

編輯多行文字欄位時，您可以開啟全螢幕編輯器：

![cf-fullscreeneditor-icon](assets/cf-fullscreeneditor-icon.png)

全螢幕編輯器提供：

* 存取各種動 [作](#actions)
* 視格式 [而定](#formats)，其他格式選[項(Rich Text](#rich-text))

### 動作 {#actions}

當全螢幕編輯器( [即多行文字](#formats))開啟時，也可使用下列動作（適用於所有格式）:

* 選擇格 [式](#formats) ([Rich Text](#rich-text)、 [Plain Text](#plain-text) 、 [Markdown](#markdown)Markdown)

* [顯示文本統計資訊](#viewing-key-statistics)

* [上傳內容](#uploading-content)
* [與主版同步](#synchronizing-with-master) （編輯變數時）
* [摘要文字](#summarizing-text)
* [註解](/help/assets/content-fragments-variations.md#annotating-a-content-fragment) ，您的文字

* [將視覺資產插入您的片段](#inserting-assets-into-your-fragment) （影像）

### 格式 {#formats}

編輯多行文本的選項取決於所選格式：

* [RTF](#rich-text)
* [純文字](#plain-text)
* [Markdown](#markdown)

當全螢幕編輯器時，可選取格式。

### RTF {#rich-text}

豐富式文字編輯可讓您設定格式：

* 粗體
* 斜體
* 底線
* 對齊：左，中，右
* 項目符號清單
* 編號清單
* 縮排：增加，減少
* 建立／中斷超連結
* 開啟全螢幕編輯器，其中提供下列格式選項：

   * 貼上文字／從Word
   * 插入表格
   * 段落樣式：第1/2/3段
   * [插入視覺資產](#inserting-assets-into-your-fragment)
   * 搜尋
   * 尋找/取代
   * 拼字檢查器
   * [註解](/help/assets/content-fragments-variations.md#annotating-a-content-fragment)

您也可以 [](#actions) 從全螢幕編輯器存取這些動作。

### 純文字 {#plain-text}

純文字可讓您快速輸入內容，毋需格式化或標注資訊。 您也可以開啟全螢幕編輯器，以執行進一 [步動作](#actions)。

>[!CAUTION]
>
>如果您選取「純 **文字** 」 **，可能會遺失您已插入「豐富文字」或「標籤文字」的任何格式、標籤和／或資產******。

### Markdown {#markdown}

>[!NOTE]
>
>如需完整資訊，請參閱 [Markdown檔案](/help/assets/content-fragments-markdown.md) 。

這可讓您使用標籤下載來格式化文字。 您可以定義：

* 標題
* 段落和分行
* 連結
* 影像
* 塊引號
* 清單
* 強調
* 程式碼區塊
* 反斜線轉義

您也可以開啟全螢幕編輯器，以執行進一 [步動作](#actions)。

>[!CAUTION]
>
>如果您在 **Rich Text** 和 **** Markdown之間切換，可能會在區塊引號和程式碼區塊中遇到意外的效果，因為這兩種格式在處理方式上可能會有差異。

### 查看關鍵統計資訊 {#viewing-key-statistics}

當全螢幕編輯器開啟時，「文字統計 **資料** 」動作會顯示一系列有關文字的資訊。 例如：

![cfx-6420-22](assets/cfx-6420-22.png)

### 上傳內容 {#uploading-content}

若要簡化內容片段的製作程式，您可以上傳在外部編輯器中準備的文字，並直接將它加入片段。

### 摘要文字 {#summarizing-text}

摘要文字旨在協助使用者將文字長度縮短為預先定義的字數，同時保留關鍵點和整體意義。

>[!NOTE]
>
>在更技術性的層次上，系統根據具體算法保留其評 *價的句子，以提供資訊密度和唯一性的最佳比* 。

>[!CAUTION]
>
>內容片段必須有有效的語言（ISO代碼）資料夾做為祖先；這可用來決定要使用的語言模型。
>
>例如， `en/` 如下列路徑：
>
>`/content/dam/my-brand/en/path-down/my-content-fragment`

>[!CAUTION]
>
>英文是現成可用的。
>
>其他語言則可從Package Share中取得：
>
>* [French(fr)](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/smartcontent-model-fr)
>* [German(de)](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/smartcontent-model-de)
>* [Italian(it)](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/smartcontent-model-it)
>* [Spanish(es)](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/smartcontent-model-es)
>



1. 選擇 **主版** ，或所需的變化。
1. 開啟全螢幕編輯器。

1. 從工 **具列選擇** 「摘要文字」。

   ![cf-17](assets/cf-17.png)

1. 指定目標字數，然後選取「開 **始**:
1. 原始文本與建議的總結並排顯示：

   * 任何要刪除的句子都會以紅色強調顯示，並加上刪除。
   * 按一下任何反白顯示的句子，將它保留在摘要內容中。
   * 按一下任何未反白顯示的句子，即可將其刪除。
   ![cfm-6420-23](assets/cfm-6420-23.png)

1. 選擇 **摘要** ，確認更改。

### 為內容片段加上註解 {#annotating-a-content-fragment}

要注釋片段：

1. 選擇 **主版** ，或所需的變化。
1. 開啟全螢幕編輯器。
1. 選取一些文字。 「注 **釋** 」表徵圖變為可用。

   ![cfm-6420-24](assets/cfm-6420-24.png)

1. 對話方塊將會開啟。 您可以在這裡輸入注釋。

1. 關閉全螢幕編輯器並 **儲存片段** 。

### 查看、編輯、刪除注釋 {#viewing-editing-deleting-annotations}

註解:

* 在編輯器的全螢幕和一般模式下，都會以文字上的反白顯示來指示。 然後，只要按一下反白顯示的文字，即可檢視、編輯和／或刪除註解的完整詳細資訊，如此就會重新開啟對話方塊。

   >[!NOTE]
   >
   >如果已將多個註解套用至一個文字，則提供下拉式選取器。

* 刪除應用注釋的整個文本時，注釋也會被刪除。

* 在片段編輯器中選擇「註解」( **Annotations** )頁籤，即可列出和刪除。

   ![cfm-6420-25](assets/cfm-6420-25.png)

* 可在時間軸中檢視和刪 [除所選片段](/help/assets/content-fragments-managing.md#timeline-for-content-fragments) 。

### 將資產插入片段 {#inserting-assets-into-your-fragment}

若要簡化製作內容片段的程式，您可以直接將 [Assets](/help/assets/managing-assets-touch-ui.md) （影像）新增至片段。

這些文字將加到片段的段落序列中，不需任何格式；當頁面上使用／參 [考片段時，可執行格式設定](/help/sites-authoring/content-fragments.md)。

>[!CAUTION]
>
>這些資產無法在參考頁面上移動或刪除，這必須在片段編輯器中完成。
>
>但是，必須在頁面編輯器中完成資產的格式 [化（如大小）](/help/sites-authoring/content-fragments.md)。 片段編輯器中資產的表示純粹是為了製作內容流程。

>[!NOTE]
>
>有各種方法可將影 [像新增](/help/assets/content-fragments.md#fragments-with-visual-assets) 至片段和／或頁面。

1. 將游標置於要添加影像的位置。
1. 使用「插 **入資產** 」圖示開啟搜尋對話方塊。

   ![cf-insertasset-icon](assets/cf-insertasset-icon.png)

1. 在對話方塊中，您可以：

   * 導覽至DAM中的必要資產
   * 在DAM中搜尋資產
   找到後，按一下縮圖以選取所需的資產。

1. 使用 **「選取** 」將資產新增至目前位置之內容片段的段落系統。

   >[!CAUTION]
   >
   >如果新增資產後，您將格式變更為：
   >
   >* **純文字檔案**:資產將完全從碎片中丟失。
   >* **Markdown**:資產將不可見，但當您返回 **Rich Text時，資產仍會存在**。


## 管理變數 {#managing-variations}

### 建立變數 {#creating-a-variation}

變數可讓您取用 **Master** （主版）內容，並視需要加以變更。

要建立新變化，請執行以下操作：

1. 開啟您的片段，並確保側面板可見。
1. 從側 **面板的圖示列選取** 「變數」。
1. 選擇 **建立變數**。
1. 將會開啟對話方塊，指定新變 **數的****「標題」(Title)和「說明」(Description** )。
1. 選擇 **添加**;片段 **Master** 將會複製到新的變數，現在會開啟供編 [輯](#editing-a-variation)。

   >[!NOTE]
   >
   >建立新變數時，一律是複製的 **Master** ，而非目前開啟的變數。

### 編輯變數 {#editing-a-variation}

您可以在下列任一項後，變更變更內容：

* [建立變數](#creating-a-variation)。
* 開啟現有片段，然後從側面板選取所需的變數。

![cfm-6420-26](assets/cfm-6420-26.png)

### 更名變數 {#renaming-a-variation}

要更名現有變數：

1. 開啟您的片段，然後從 **側面板** 選取「變化」。
1. 選擇所需的變化。
1. 從「 **動作** 」下拉式清 **單中選** 取「重新命名」。

1. 在產生的對 **話方塊中** ，輸入新的「 **** 標題」和／或「說明」。

1. 確認「重 **命名** 」動作。

>[!NOTE]
>
>這只會影響變 **化Title**。

### 刪除變數 {#deleting-a-variation}

要刪除現有變數，請執行以下操作：

1. 開啟您的片段，然後從 **側面板** 選取「變化」。
1. 選擇所需的變化。
1. 從「 **動作** 」下拉式清 **單中選** 取「刪除」。

1. 確認對 **話方塊中** 的「刪除」動作。

>[!NOTE]
>
>您無法刪除 **主版**。

### 與主版同步 {#synchronizing-with-master}

**主版** (Master)是內容片段的一個完整部分，依定義，它包含內容的主版復本，而變數則包含該內容的個別更新及自訂版本。 更新主版時，這些更改可能也與變化有關，因此需要傳播到它們。

在編輯變數時，您可以存取動作，以便將變數的目前元素與「主版」同步。 這可讓您自動將對「主版」所做的變更複製到所需的變更。

>[!CAUTION]
>
>同步僅可用於將更改從 *主&#x200B;**版複製**到變化*。
>
>只有變更的當前元素將同步。
>
>同步只適用於多 **行文本** -資料類型。
>
>將變 *更從變更傳輸&#x200B;**至Master ***，不提供選項。

1. 在片段編輯器中開啟您的內容片段。 請確定已 **編輯主** 版。
1. 選擇特定的變化，然後從以下任一項中選擇適當的同步操作：

   * 「動 **作」下拉式選擇器** -將目前的元 **素與主版同步**

   * 全螢幕編輯器的工具列——與 **主版同步**

1. 主版和變數會並排顯示：

   * 綠色表示已新增（至變數）的內容
   * 紅色表示內容已移除（從變數中）
   ![cfm-6420-27](assets/cfm-6420-27.png)

1. 選擇「 **同步**」(Synchronize)，將更新並顯示變化。

