---
title: Adobe Experience Manager觸控式UI的結構
description: 在Adobe Experience Manager中實作的觸控最佳化UI有幾項基礎原則，而且由數個關鍵元素組成
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: e562b289-5d8b-4fa8-ad1c-fff5f807a45e
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 3%

---

# Adobe Experience Manager觸控式UI的結構{#structure-of-the-aem-touch-enabled-ui}

Adobe Experience Manager (AEM)觸控式UI具備數項基礎原則，而且由數個關鍵元素組成：

## 主控台 {#consoles}

### 基本版面與調整大小 {#basic-layout-and-resizing}

UI同時適用於行動裝置和桌上型裝置，不過Adobe已決定使用適用於所有熒幕和裝置的一種樣式，而不是建立兩種樣式。

所有模組都使用相同的基本版面，在AEM中這可以視為：

![chlimage_1-142](assets/chlimage_1-142.png)

此版面會遵循回應式設計樣式，並根據您所使用的裝置/視窗大小進行調整。

例如，當解析度低於1024 px （如同在行動裝置上）時，顯示器將會據此調整：

![chlimage_1-143](assets/chlimage_1-143.png)

### 標題列 {#header-bar}

![chlimage_1-144](assets/chlimage_1-144.png)

標題列會顯示全域元素，包括：

* 標誌以及您目前使用的特定產品/解決方案；若為AEM，也會形成全域導覽的連結
* 搜尋
* 用於存取說明資源的圖示
* 圖示以存取其他解決方案
* 正在等候您的任何警報或收件匣專案的指標（以及存取權）
* 使用者圖示，以及設定檔管理的連結

### 工具列 {#toolbar}

這與您的位置及表面工具相關，與控制以下頁面中的檢視或資產相關。 工具列是產品專屬的，但這些元素有一些共同之處。

工具列會在任何位置顯示目前可用的動作：

![chlimage_1-145](assets/chlimage_1-145.png)

也取決於是否選取資源：

![chlimage_1-146](assets/chlimage_1-146.png)

### 左側邊欄 {#left-rail}

您可以視需要開啟/隱藏左側邊欄，以顯示：

* **時間軸**
* **參考**
* **篩選**

預設值為 **僅限內容** （邊欄已隱藏）。

![chlimage_1-147](assets/chlimage_1-147.png)

## 頁面製作 {#page-authoring}

編寫頁面時，結構區域如下。

### 內容框架 {#content-frame}

頁面內容會在內容框架中呈現。 內容框架獨立於編輯器 — 以確保不會因CSS或JavaScript而發生衝突。

內容框架位於視窗的右側區段（在工具列下）。

![chlimage_1-148](assets/chlimage_1-148.png)

### 編輯器框架 {#editor-frame}

編輯器框架會實現編輯功能。

編輯器框架是所有 *頁面製作元素*. 它位在內容框架頂端，包括：

* 頂端工具列
* 側面板
* 所有覆蓋
* 任何其他頁面製作元素；例如，元件工具列

![chlimage_1-149](assets/chlimage_1-149.png)

### 側面板 {#side-panel}

此檔案包含兩個預設標籤，可讓您選取資產和元件。 您可從此處拖曳這些量度並放置在頁面上。

側面板預設為隱藏。 選取時，它將顯示在左側，或滑過以涵蓋整個視窗（當視窗大小低於1024畫素；例如在行動裝置上）。

![chlimage_1-150](assets/chlimage_1-150.png)

### 側面板 — 資產 {#side-panel-assets}

在「資產」標籤中，您可以從資產範圍中選取。 您也可以篩選特定辭彙，或選取群組。

![chlimage_1-151](assets/chlimage_1-151.png)

### 側面板 — 資產群組 {#side-panel-asset-groups}

在「資產」標籤中，有一個下拉式清單可用來選取特定資產群組。

![chlimage_1-152](assets/chlimage_1-152.png)

### 側面板 — 元件 {#side-panel-components}

在「元件」標籤中，您可以從元件範圍中選取。 您也可以篩選特定辭彙，或選取群組。

![chlimage_1-153](assets/chlimage_1-153.png)

### 覆蓋 {#overlays}

這些會覆蓋內容框架，並由 [圖層](#layer) 以瞭解（透明）與元件及其內容互動的機制。

這些覆蓋圖會在編輯器框架中呈現（包含所有其他頁面製作元素），不過實際上會在內容框架中覆蓋適當的元件。

![chlimage_1-154](assets/chlimage_1-154.png)

### 圖層 {#layer}

圖層是獨立的功能組合，可以啟動為：

* 提供頁面的不同檢視
* 可讓您操控及/或與頁面互動

這些圖層提供整個頁面的複雜功能，而非個別元件上的特定動作。

AEM隨附數個已針對頁面製作實作的圖層；包括例如，編輯、預覽、註釋。

>[!NOTE]
>
>圖層是一個強大的概念，可影響使用者對頁面內容的檢視以及與頁面內容的互動。 開發您自己的圖層時，您必須確保圖層在退出時進行清除。

### 圖層切換器 {#layer-switcher}

圖層切換器可讓您選擇要使用的圖層。 關閉時，它會指出目前使用的圖層。

圖層切換器可從工具列（在視窗頂端、編輯器框架中）以下拉式清單形式提供。

![chlimage_1-155](assets/chlimage_1-155.png)

### 元件工具列 {#component-toolbar}

元件的每個例項在按一下（一次或緩慢按兩下）時都會顯示其工具列。 工具列包含頁面上元件例項（可編輯）可用的特定動作（例如，複製、貼上、開啟編輯器）。

根據可用的空間，元件工具列會放置在適當元件的右上角或右下角。

![chlimage_1-156](assets/chlimage_1-156.png)

## 更多資訊 {#further-information}

如需有關觸控式UI概念的詳細資訊，請閱讀 [AEM觸控式UI的概念](/help/sites-developing/touch-ui-concepts.md).

如需詳細技術資訊，請參閱 [JS檔案集](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html) 用於觸控式頁面編輯器。
