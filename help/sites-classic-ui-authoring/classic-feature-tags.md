---
title: 使用標籤
description: 標籤是一種將網站內容分類的快速輕鬆方法。 標籤可視為可以附加至頁面、資產或其他內容的關鍵字或標籤，以啟用搜尋來尋找該內容和相關內容。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: 4b6c273c-560e-4330-b886-a02825d5aaa1
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 1%

---

# 使用標記{#using-tags}

標籤是一種將網站內容分類的快速輕鬆方法。 標籤可視為可以附加至頁面、資產或其他內容的關鍵字或標籤，以啟用搜尋來尋找該內容和相關內容。

* 另請參閱 [管理標籤](/help/sites-administering/tags.md) 以取得關於建立和管理標籤，以及已對哪些內容標籤套用的資訊。
* 另請參閱 [為開發人員加上標籤](/help/sites-developing/tags.md) 以取得標籤架構的相關資訊，以及在自訂應用程式中包含和擴充標籤。

## 使用標籤的十大理由 {#ten-reasons-to-use-tagging}

1. 組織內容：標籤讓作者的工作更輕鬆，因為他們可以輕鬆快速地組織內容。
1. 組織標籤：當標籤組織內容時，階層分類/名稱空間會組織標籤。
1. 深度組織標籤：有了建立標籤和子標籤的功能，就可以表示整個分類系統，涵蓋術語、子術語及其關係。 這可讓您建立與正式內容階層平行的第二個（或第三個）內容階層。
1. 控制的標籤：可以透過對標籤和/或名稱空間套用許可權來控制標籤建立和套用，從而控制標籤。
1. 彈性標籤：標籤有許多名稱和面孔：標籤、分類術語、類別、標籤等等。 它們在內容模型和使用方式上較靈活；例如，在概述目標人口統計、分類及評等內容或建立次要內容階層時。
1. 改良搜尋：AEM中的預設搜尋元件包含大量已建立的標籤和已套用的標籤，可套用篩選器以將結果縮小到相關範圍。
1. SEO啟用：套用為頁面屬性的標籤會自動顯示在頁面的中繼資料中，對搜尋引擎可見。
1. 複雜化：只要輕觸按鈕，就能使用單字建立標籤。 之後，可以新增標題、說明和無限標籤，為標籤提供更多語意。
1. 核心一致性：標籤系統是AEM的核心元件，可供所有AEM功能用來分類內容。 此外，開發人員可以使用標籤API來建立已啟用標籤的應用程式，並存取相同分類法。
1. 結合的結構與彈性：由於巢狀內嵌頁面和路徑，AEM非常適合處理結構化資訊。 由於內建的全文檢索搜尋功能，在處理非結構化資訊時，也同樣強大。 標籤結合了結構和彈性的優點。

在設計網站的內容結構和資產的中繼資料結構時，請考慮標籤提供的輕量且方便存取的方法。

## 套用標籤 {#applying-tags}

在作者環境中，作者可透過存取頁面屬性並在中輸入一或多個標籤來套用標籤 **標籤/關鍵字** 欄位。

要套用 [預先定義的標籤](/help/sites-administering/tags.md)，在 **頁面屬性** 視窗使用 `Tags/Keywords` 欄位下拉式清單，從頁面允許的標籤清單中選取。 此 **標準標籤** tab是預設的名稱空間，這表示沒有 `namespace-string:` 在分類前面加上前置詞。

![chlimage_1-2](assets/chlimage_1-2a.png)

### 發佈標記 {#publishing-tags}

和頁面一樣，您可以對標籤和名稱空間執行下列動作：

**啟動**

* 啟用個別標籤。

  就像頁面一樣，新建立的標籤必須先啟動，才能在發佈環境中使用。

>[!NOTE]
>
>當您啟動頁面時，會自動開啟對話方塊，讓您啟動屬於該頁面的未啟動標籤。

**停用**

* 停用選取的標籤。

## 標籤雲端 {#tag-clouds}

標籤雲會顯示目前頁面、整個網站或最常存取之網站的標籤雲端。 標籤雲是強調使用者感興趣之問題（一直）的方法。 用於顯示標籤的文字大小會因使用而有所不同。

此 [標籤雲](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md#tag-cloud) 元件（一般元件群組）可用來將標籤雲新增至頁面。

## 在標籤上搜尋 {#searching-on-tags}

您可以在作者和發佈環境中搜尋標籤。

### 使用搜尋元件 {#using-search-component}

新增 [搜尋元件](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md#search) 至頁面提供搜尋功能，其中包含標籤，且可用於製作和發佈環境。

![chlimage_1-3](assets/chlimage_1-3a.png)
