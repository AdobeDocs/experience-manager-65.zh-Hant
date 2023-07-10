---
title: 大量處理作業
seo-title: Bulk Processing Operations
description: null
seo-description: null
page-status-flag: never-activated
uuid: 62a6c379-a460-4f8f-a909-03d04fa8944b
contentOwner: sarchiz
discoiquuid: 47c2a80f-78ac-4372-86b4-06351a1dd58f
docset: aem65
source-git-commit: d045fc1ac408f992d594a4cb68d1c4eeae2b0de1
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 2%

---


# 大量處理作業 {#bulk-processing-operations}

## 簡介 {#introduction}

使用最新版AEM時，「全選」按鈕已擴充至所有檢視：「清單」、「欄」和「卡片」檢視。 全選按鈕現在會選取指定資料夾或集合中的所有內容，而不僅僅是使用者端瀏覽器中載入和顯示的資產和頁面。

已為大量作業啟用主要動作： **移動**， **刪除** 和 **複製**. 新的對話方塊可讓客戶知道哪些動作無法使用大量處理。

## 使用方式 {#how-to-use}

名為的新按鈕 **全選** 已新增至「卡片」、「清單」或「欄」檢視。 此按鈕可用於任何檢視，以選取資料集中的所有元素。

在舊版AEM中，選取範圍受到使用者端瀏覽器中載入內容的限制。 引入此新變更是為了避免與正在執行大量操作的元素數量混淆。

目前，已將三個作業新增至大量處理：

* 移動
* 複製
* 刪除

未來將新增對更多操作的支援。
若要使用此功能，您必須導覽至您要對「頁面」或「資產」執行大量作業的資料夾或集合。

然後，選擇其中一個檢視，如下所示：

### 卡片檢視 {#card-view}

![顯示各種影像資產縮圖影像的卡片檢視。](assets/unu.png)

### 卡片檢視中的大量選取 {#bulk-selection-in-card-view}

資產或頁面可透過以下方式大量選取： **全選** 右上角的按鈕：

![選取「卡片檢視」右上角顯示的「全部」按鈕。](assets/doi.png) ![「卡片檢視」中影像資產的所有縮圖影像都會顯示為已選取且帶有核取標籤。](assets/trei.png)

### 清單檢視 {#list-view}

清單檢視也是一樣：

![「清單檢視」右上角的「全選」選項會反白顯示。](assets/patru_modified.png)

### 清單檢視中的大量選取 {#bulk-selection-in-list-view}

在清單檢視中，使用 **全選** 按鈕，或使用左側的核取方塊進行大量選取。

![顯示影像資產縮圖影像的即時檢視會以水準列顯示。](assets/cinci.png) ![顯示影像資產縮圖影像的清單方塊，以及「名稱」左側的核取方塊。](assets/sase.png)

### 欄檢視 {#column-view}

![欄檢視，顯示垂直欄中顯示之影像資產的縮圖影像。](assets/sapte.png)

### 欄檢視中的大量選取 {#bulk-selection-in-column-view}

![「欄檢視」中影像資產的所有縮圖影像都會顯示為已選取且帶有核取標籤。](assets/opt.png)

## 大量啟用的作業 {#bulk-enabled-operations}

選取後，可以執行三個大量啟用的動作之一： **移動**， **複製** 或 **刪除**.

此處， **移動** 會針對上述選取的資產執行作業。 在任何檢視中，這會導致所有資產被移動到所選位置，而不只是載入到畫面上的資產。

![在「欄檢視」中移動顯示所選資料夾的資產。](assets/noua.png)

對於未大量啟用的其他作業，例如 **下載，** 系統會顯示警告，指出只有瀏覽器中載入的元素才會包含在作業中。

![資產檢視顯示選取的影像資產，以及快顯對話方塊「不支援大量動作」。](assets/zece.png)
