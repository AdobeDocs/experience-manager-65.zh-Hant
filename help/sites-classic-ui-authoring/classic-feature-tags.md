---
title: 使用標籤
seo-title: 使用標籤
description: 標籤是快速且簡單的網站內容分類方法。 標籤可視為可附加至頁面、資產或其他內容的關鍵字或標籤，以便搜尋以尋找該內容及相關內容。
seo-description: 標籤是快速且簡單的網站內容分類方法。 標籤可視為可附加至頁面、資產或其他內容的關鍵字或標籤，以便搜尋以尋找該內容及相關內容。
uuid: 9799131f-4043-4022-a401-af8be93a1bf6
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: c117b9d1-e4ae-403f-8619-6e48d424a761
translation-type: tm+mt
source-git-commit: 016c705230dffec052c200b058a36cdbe0520fc4

---


# 使用標籤{#using-tags}

標籤是快速且簡單的網站內容分類方法。 標籤可視為可附加至頁面、資產或其他內容的關鍵字或標籤，以便搜尋以尋找該內容及相關內容。

* 如需 [有關建立和管理標籤](/help/sites-administering/tags.md) ，以及已套用內容標籤的資訊，請參閱管理標籤。
* 如需 [標籤架構的相關資訊](/help/sites-developing/tags.md) ，請參閱為開發人員標籤，以及在自訂應用程式中包含和擴充標籤。

## 使用標籤的十個理由 {#ten-reasons-to-use-tagging}

1. 組織內容：標籤可讓作者更輕鬆地組織內容，因為他們可以事半功倍地快速組織內容。
1. 組織標籤：當標籤組織內容時，階層式分類／命名空間會組織標籤。
1. 有條理的標籤：由於能夠建立標籤和子標籤，因此可以表達整個分類系統，涵蓋術語、子術語及其關係。 這允許建立與正式內容階層平行的第二（或第三）內容階層。
1. 控制標籤：標籤可借由套用權限至標籤和／或名稱空間來控制標籤建立和應用程式。
1. 彈性標籤：標籤有許多名稱和面孔：標籤、分類術語、類別、標籤等。 它們的內容模型及使用方式有彈性；例如，在概述目標人口統計資料時，將內容分類和評分，或建立次要內容階層。
1. 改進搜尋：aem中的預設搜尋元件大致包含已建立的標籤和套用的標籤，篩選器可套用至這些標籤，將結果縮小為相關的標籤。
1. 啟用SEO:套用為頁面屬性的標籤會自動顯示在頁面的中繼標籤中，讓搜尋引擎可以看到。
1. 簡單易用：只需從單字和按鈕的觸控，即可建立標籤。 之後，可新增標題、說明和無限制的標籤，為標籤提供更多語義。
1. 核心一致性：標籤系統是AEM的核心元件，所有AEM功能都會使用它來分類內容。 此外，標籤API可供開發人員用來建立具有相同分類存取權的標籤啟用應用程式。
1. 結合結構與彈性：AEM最適合處理結構化資訊，因為頁面和路徑已巢狀化。 由於內置全文搜索功能，它在處理非結構化資訊時同樣具有強大的功能。 標籤結合了結構和靈活性的優點。

當設計網站的內容結構和資產的中繼資料架構時，請考慮提供的輕量型和可存取的方法標籤。

## 套用標籤 {#applying-tags}

在作者環境中，作者可以存取頁面屬性並在「標籤／關鍵字」欄位中輸入一或多個標籤，以套 **用標籤** 。

若要套 [用預先定義的標籤](/help/sites-administering/tags.md)，請在「頁面屬性 **」視窗中，使用欄**`Tags/Keywords` 位下拉式清單，從頁面允許的標籤清單中選取。 「標 **準標籤** 」標籤是預設的命名空間，這表示分類 `namespace-string:` 沒有前置詞。

![chlimage_1-2](assets/chlimage_1-2a.png)

### 發佈標籤 {#publishing-tags}

與頁面一樣，您可以對標籤和名稱空間執行下列動作：

**啟動**

* 啟動個別標籤。

   如同頁面一樣，新建立的標籤必須先啟動，才能在發佈環境中使用。

>[!NOTE]
>
>當您啟動頁面時，會自動開啟對話方塊，讓您啟動屬於頁面的未啟動標籤。

**停用**

* 停用選取的標籤。

## 標籤雲端 {#tag-clouds}

標籤雲端會顯示一組標籤，可用於目前頁面、整個網站或最常存取的標籤。 標籤雲端是反白顯示使用者感興趣（已經）的問題的方式。 用來顯示標籤的文字大小視其使用而定。

Tag Cloud [](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md#tag-cloud) component(General component group)是用來將Tag cloud新增至頁面的。

## 在標籤上搜尋 {#searching-on-tags}

您可以在作者和發佈環境中搜尋標籤。

### 使用搜尋元件 {#using-search-component}

將 [Search元件新增至頁面](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md#search) ，可提供包含標籤的搜尋功能，並可用於作者和發佈環境。

![chlimage_1-3](assets/chlimage_1-3a.png)

