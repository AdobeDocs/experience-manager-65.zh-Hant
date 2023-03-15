---
title: 使用標記
seo-title: Using Tags
description: 標籤是快速且簡單的網站內容分類方法。 標籤可以被視為可附加至頁面、資產或其他內容的關鍵字或標籤，以使搜索能夠找到該內容和相關內容。
seo-description: Tags are a quick and easy method of classifying content within a website. Tags may be thought of as keywords or labels that can be attached to a page, an asset, or other content to enable searches to find that content and related content.
uuid: 9799131f-4043-4022-a401-af8be93a1bf6
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: c117b9d1-e4ae-403f-8619-6e48d424a761
exl-id: 4b6c273c-560e-4330-b886-a02825d5aaa1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 1%

---

# 使用標記{#using-tags}

標籤是快速且簡單的網站內容分類方法。 標籤可以被視為可附加至頁面、資產或其他內容的關鍵字或標籤，以使搜索能夠找到該內容和相關內容。

* 請參閱 [管理標籤](/help/sites-administering/tags.md) ，以取得建立和管理標籤以及套用內容標籤的相關資訊。
* 請參閱 [為開發人員進行標籤](/help/sites-developing/tags.md) 以取得標籤架構的相關資訊，以及在自訂應用程式中包含和擴充標籤。

## 使用標籤的十個理由 {#ten-reasons-to-use-tagging}

1. 組織內容：標籤可讓作者更輕鬆，因為他們可以輕鬆快速地組織內容。
1. 組織標籤：標籤組織內容時，分層分類/命名空間組織標籤。
1. 有條理的標籤：有了建立標籤和子標籤的能力，就可以表示整個分類系統，包括術語、子術語及其關係。 這可以建立與官方層級平行的第二（或第三）個內容階層。
1. 控制標籤：可借由對標籤和/或命名空間套用權限來控制標籤，以控制標籤的建立和應用程式。
1. 彈性的標籤：標籤有許多名稱和面孔：標籤、分類術語、類別、標籤等。 在內容模型和使用方式上，這些規則是有彈性的；例如，在概述目標人口統計資料時，將內容分類和評分，或建立次要內容階層。
1. 改進搜尋：AEM中的預設搜尋元件廣泛包含已建立的標籤和已套用的標籤，可套用篩選條件，將結果縮小至相關的標籤。
1. SEO啟用：套用為頁面屬性的標籤會自動顯示在頁面的中繼標籤中，讓搜尋引擎可看見。
1. 簡單複雜：只需從字詞和按鈕的觸控來建立標籤即可。 之後，可以新增標題、說明和無限標籤，為標籤提供更多語意。
1. 核心一致性：標籤系統是AEM的核心元件，供所有AEM功能用來分類內容。 此外，開發人員可使用標籤API來建立啟用標籤的應用程式，以存取相同的分類。
1. 結合結構和彈性：AEM是處理結構化資訊的理想選擇，因為頁面和路徑有巢狀。 由於內置的全文搜索功能，它在處理非結構化資訊時同樣具有強大的功能。 標籤結合了結構和彈性的優點。

設計網站的內容結構和資產的中繼資料結構時，請考慮提供的精簡且可存取的方法標籤。

## 套用標籤 {#applying-tags}

在製作環境中，作者可透過存取頁面屬性並在 **標籤/關鍵字** 欄位。

要應用 [預先定義的標籤](/help/sites-administering/tags.md)，在 **頁面屬性** 視窗使用 `Tags/Keywords` 欄位下拉式清單，從頁面允許的標籤清單中選取。 此 **標準標籤** 標籤是預設的命名空間，這表示 `namespace-string:` 前置詞為分類法。

![chlimage_1-2](assets/chlimage_1-2a.png)

### 發佈標籤 {#publishing-tags}

和頁面一樣，您可以在標籤和命名空間上執行下列動作：

**啟動**

* 啟動個別標籤。

   就像頁面一樣，新建立的標籤必須先啟動，才能在發佈環境中使用。

>[!NOTE]
>
>當您啟動頁面時，會自動開啟對話方塊，讓您啟動屬於該頁面的未啟動標籤。

**停用**

* 停用選取的標籤。

## 標籤雲 {#tag-clouds}

標籤雲端會顯示一組標籤，可針對目前頁面、整個網站或最常存取的網站。 標籤雲是強調使用者所關心之問題的一種方式。 用來顯示標籤的文字大小，會因其使用而異。

此 [Tag Cloud](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md#tag-cloud) 元件（一般元件群組）可用來將標籤雲新增至頁面。

## 在標籤上搜尋 {#searching-on-tags}

您可以在製作和發佈環境中搜尋標籤。

### 使用搜尋元件 {#using-search-component}

新增 [搜尋元件](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md#search) 至頁面提供搜尋功能，其中包含標籤，可同時用於製作和發佈環境。

![chlimage_1-3](assets/chlimage_1-3a.png)
