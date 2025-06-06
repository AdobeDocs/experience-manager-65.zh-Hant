---
title: ClientContext
description: 瞭解如何使用Client Context來檢視有關Adobe Experience Manager中目前頁面和訪客的資訊。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: 69c66c82-fbd6-406e-aefd-b85480a62109
solution: Experience Manager, Experience Manager Sites
feature: Administering,Personalization
role: Admin
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '1961'
ht-degree: 0%

---


# ClientContext{#client-context}

>[!NOTE]
>
>ContextHub已取代使用者端內容。 如需詳細資訊，請參閱相關的[組態](/help/sites-developing/ch-configuring.md)和[開發人員](/help/sites-developing/contexthub.md)檔案。

Client Context是一種機制，可提供有關目前頁面和訪客的特定資訊。 可以使用&#x200B;**Ctrl-Alt-c** (windows)或&#x200B;**control-option-c** (Mac)開啟：

![使用者端內容視窗的範例](assets/clientcontext_alisonparker.png)

在發佈和作者環境中，它會顯示以下相關資訊：

* 訪客；根據您的執行個體，系統會要求或衍生某些資訊。
* 頁面標籤以及目前訪客存取這些標籤的次數（這會在您將滑鼠移到特定標籤上時顯示） 。
* 頁面資訊。
* 技術環境的相關資訊；例如IP位址、瀏覽器和熒幕解析度。
* 目前解析的任何區段。

圖示（僅適用於作者環境）可讓您設定使用者端內容的詳細資訊：

![使用者端內容視窗的編輯、載入及重設圖示](do-not-localize/clientcontext_icons.png)

* **編輯**
新頁面隨即開啟，讓您[編輯、新增或移除設定檔屬性](#editingprofiledetails)。

* **載入**
您可以[從設定檔清單中選取，並載入您要測試的設定檔](#loading-a-new-user-profile)。

* **重設**
您可以[將設定檔](#resetting-the-profile-to-the-current-user)重設為目前使用者的設定檔。

## 可用的使用者端內容元件 {#available-client-context-components}

Client Context可以顯示下列屬性（[視使用[編輯]](#adding-a-property-component)選取的內容而定）：

**瀏覽者資訊**&#x200B;顯示下列使用者端資訊：

* **IP位址**
* **關鍵字**&#x200B;用於搜尋引擎轉介
* 正在使用的&#x200B;**瀏覽器**
* 正在使用的&#x200B;**OS** （作業系統）
* 熒幕&#x200B;**解析度**
* **滑鼠X**&#x200B;位置
* **滑鼠Y**&#x200B;位置

**活動資料流**&#x200B;這可提供使用者在各種平台(例如AEM論壇、部落格、評分等)上的社交活動相關資訊。

**促銷活動**&#x200B;可讓作者模擬促銷活動的特定體驗。 此元件會覆寫一般的促銷活動解析度和體驗選取範圍，以啟用各種置換測試。

行銷活動的解析通常以行銷活動的優先順序屬性為基礎。 通常會根據細分來選取體驗。

**購物車**&#x200B;顯示購物車資訊，包括產品專案（標題、數量、價格格式等）、已解決的促銷活動（標題、訊息等）和憑單（代碼、說明等）。

購物車工作階段存放區也會使用ClientContextCartServlet將已解決的促銷活動變更（根據分段變更）通知伺服器。

**一般存放區**&#x200B;是顯示存放區內容的一般元件。 這是一般存放區屬性元件的較低層級版本。

Generic Store必須設定有JS轉譯器，以便以自訂方式顯示資料。

**一般存放區屬性**&#x200B;是顯示存放區內容的一般元件。 這是一般存放區元件的較高層級版本。

「一般存放區屬性」元件包括預設轉譯器，其會列出已設定的屬性（連同縮圖）。

**地理位置**&#x200B;顯示使用者端的經緯度。 它會使用HTML5地理位置API來查詢瀏覽器中的目前位置。 這會向訪客顯示快顯視窗，瀏覽器會詢問訪客是否同意共用其位置。

在Context Cloud中顯示時，元件會使用Google API將地圖顯示為縮圖。 元件受Google API [使用量限制](https://developers.google.com/maps/documentation/staticmaps/intro#Limits)的約束。

>[!NOTE]
>
>在AEM 6.1中，地理位置存放區不再提供反向地理編碼功能。 因此，地理位置存放區不會再擷取有關目前位置的詳細資料，例如城市名稱或國家/地區代碼。 使用此存放區資料的區段將無法正常運作。 地理位置存放區僅包含位置的經緯度。

**JSONP存放區**&#x200B;顯示與安裝相依之內容的元件。

JSONP標準是JSON的補充功能，可讓您規避相同原始原則（使網頁應用程式無法與另一個網域上的伺服器通訊）。 其包含於包裝JSON物件在函式呼叫中，以便能夠將其從其他網域載入為`<script>` （這是相同來源原則的允許例外狀況）。

JSONP存放區就像任何其他存放區一樣，但是它會載入來自其他網域的資訊，而不需要在目前網域上為該資訊擁有Proxy。 請參閱[透過JSONP將資料儲存在使用者端內容](/help/sites-administering/client-context.md#storing-data-in-client-context-via-jsonp)中的範例。

>[!NOTE]
>
>JSONP存放區不會快取Cookie中的資訊，但會在每次頁面載入時擷取該資料。

**設定檔資料**&#x200B;顯示在使用者設定檔中收集的資訊。 例如，性別、年齡、電子郵件地址等。

**已解析的區段**&#x200B;顯示目前解析的區段（通常取決於使用者端內容中顯示的其他資訊）。 這在設定行銷活動時是有意義的。

例如，滑鼠目前是在視窗的左手或右手部分。 此區段主要用於測試，因為可以立即看到變更。

**社交圖**&#x200B;顯示使用者朋友和關注者的社交圖。

>[!NOTE]
>
>目前這是示範功能，依賴示範使用者設定檔節點上預先設定的資料集。 例如，請參閱：
>
>`/home/users/geometrixx/aparker@geometrixx.info/profile` =>朋友屬性

**標籤雲**&#x200B;顯示目前頁面上設定的標籤以及瀏覽網站時收集的標籤。 將滑鼠移到標籤上會顯示目前使用者存取包含該特定標籤的頁面的次數。

>[!NOTE]
>
>在造訪的頁面上顯示的DAM資產上設定的標籤則不會計算在內。

**Technographics存放區**&#x200B;此元件依存於您的安裝。

**ViewedProducts**&#x200B;追蹤購物者已檢視的產品。 可查詢最近檢視的產品或未在購物車中的最近檢視的產品。

此工作階段存放區沒有預設的使用者端內容元件。

如需詳細資訊，請參閱[使用者端內容](/help/sites-developing/client-context.md)。

>[!NOTE]
>
>頁面資料不再於使用者端內容中作為預設元件。 如有需要，您可以編輯使用者端內容、新增&#x200B;**一般存放區屬性**&#x200B;元件，然後將其設定為將&#x200B;**存放區**&#x200B;定義為`pagedata`，以新增此專案。

## 變更使用者端內容設定檔 {#changing-the-client-context-profile}

「使用者端內容」可讓您以互動方式變更詳細資訊：

* 變更「使用者端內容」中使用的設定檔，可讓您檢視不同使用者在目前頁面上會看到的不同體驗。
* 除了變更使用者設定檔之外，您還可以變更一些設定檔詳細資料，以檢視頁面體驗在各種條件下的差異。

### 載入新的使用者設定檔 {#loading-a-new-user-profile}

您可以透過以下其中一種方式來變更設定檔：

* [使用載入圖示](#loading-a-new-visitor-profile-with-the-load-profile-icon)
* [使用選取範圍滑桿](#loadinganewvisitorprofilewiththeselectionslider)

完成後，您可以[重設設定檔](#resetting-the-profile-to-the-current-user)。

#### 使用載入設定檔圖示載入新訪客設定檔 {#loading-a-new-visitor-profile-with-the-load-profile-icon}

1. 按一下「載入設定檔」圖示：

   ![使用者端內容的載入設定檔圖示](do-not-localize/clientcontext_loadprofile.png)

1. 這將開啟對話方塊，您可以在此處選取要載入的設定檔：

   ![設定檔載入器對話方塊顯示選取設定檔的下拉式清單](assets/clientcontext_profileloader.png)

1. 按一下&#x200B;**確定**&#x200B;以載入。

#### 使用選取範圍滑桿載入新的使用者設定檔 {#loading-a-new-user-profile-with-the-selection-slider}

您也可以使用選取項滑桿來選取設定檔：

1. 連按兩下代表目前使用者的圖示。 選取器隨即開啟，使用箭頭導覽並檢視可用的設定檔：

   ![使用者選擇器](assets/clientcontext_profileselector.png)

1. 按一下要載入的設定檔。 載入詳細資料後，按一下選取器外部以關閉。

#### 將設定檔重設為目前使用者 {#resetting-the-profile-to-the-current-user}

1. 使用重設圖示將「使用者端內容」中的設定檔傳回至目前使用者的設定檔：

   ![重設圖示](do-not-localize/clientcontext_resetprofile.png)

### 變更瀏覽器平台 {#changing-the-browser-platform}

1. 連按兩下代表瀏覽器平台的圖示。 選取器隨即開啟，使用箭頭導覽並檢視可用的平台/瀏覽器：

   ![瀏覽器平台選擇器](assets/clientcontext_browserplatform.png)

1. 按一下您要載入的平台瀏覽器。 載入詳細資料後，按一下選取器外部以關閉。

### 變更地理位置 {#changing-the-geolocation}

1. 按兩下地理位置圖示。 展開的地圖隨即開啟，您可以在此處將標籤拖曳至新位置：

   ![地理位置詳細資料](assets/clientcontext_geomocationrelocate.png)

1. 按一下地圖外部以關閉。

### 變更標籤選取範圍 {#changing-the-tag-selection}

1. 連按兩下Client Context的「標籤雲」區段。 對話方塊隨即開啟，您可以在此處選取標籤：

   ![標籤雲端對話方塊](assets/clientcontext_tagselection.png)

1. 按一下「確定」以載入「使用者端內容」。

## 編輯Client Context {#editing-the-client-context}

編輯使用者端內容可用於設定（或重設）特定屬性的值、新增屬性或移除不再需要的屬性。

### 編輯屬性詳細資料 {#editing-property-details}

編輯使用者端內容可用來設定（或重設）某些屬性的值。 這可讓您測試特定案例（對[細分](/help/sites-administering/campaign-segmentation.md)和[行銷活動](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)特別有用）。

![編輯使用者端內容](assets/clientcontext_alisonparker_edit.png)

### 新增屬性元件 {#adding-a-property-component}

開啟&#x200B;**ClientContext設計頁面**&#x200B;之後，您也可以&#x200B;**使用可用的元件，新增**&#x200B;全新的屬性（元件會列在sidekick上，或是在按兩下&#x200B;**將元件或資產拖曳到這裡**&#x200B;方塊後開啟的&#x200B;**插入新元件**&#x200B;對話方塊中）：

![正在新增屬性至使用者端內容視窗](assets/clientcontext_alisonparker_new.png)

### 移除屬性元件 {#removing-a-property-component}

開啟&#x200B;**ClientContext設計頁面**&#x200B;之後，您也可以&#x200B;**移除**&#x200B;屬性（若不再需要）。 這包括提供的現成屬性；如果屬性已移除，**Reset**&#x200B;將會恢復這些屬性。

## 透過JSONP在Client Context中儲存資料 {#storing-data-in-client-context-via-jsonp}

請依照此範例使用JSONP存放區內容存放區元件，將外部資料新增至使用者端內容。 然後，根據該資料的資訊建立區段。 此範例使用WIPmania.com提供的JSONP服務。 此服務會根據Web使用者端的IP位址傳回地理位置資訊。

此範例使用Geometrixx Outdoors範例網站來存取Client Context並測試建立的區段。 只要網頁已啟用使用者端內容，您就可以使用不同的網站。 （請參閱[新增使用者端內容至頁面](/help/sites-developing/client-context.md#adding-client-context-to-a-page)。）

### 新增JSONP存放區元件 {#add-the-jsonp-store-component}

將JSONP Store元件新增至Client Context，並使用它來擷取和儲存Web使用者端的地理位置資訊。

1. 在AEM編寫執行個體上，開啟Geometrixx Outdoors網站的英文首頁。 ([https://localhost:4502/content/geometrixx-outdoors/en.html](https://localhost:4502/content/geometrixx-outdoors/en.html))。
1. 若要開啟「使用者端內容」，請按Ctrl-Alt-c (windows)或control-option-c (Mac)。
1. 按一下「Client Context」頂端的編輯圖示，開啟「Client Context Designer」。

   ![連結圖示](do-not-localize/chlimage_1.png)

1. 將JSONP存放區元件拖曳至Client Context。

   ![將JSONP存放區元件拖放至使用者端內容](assets/chlimage_1-4.jpeg)

1. 連按兩下元件，開啟編輯對話方塊。
1. 在「JSONP服務URL」方塊中，輸入以下URL，然後按一下「擷取存放區」：

   `https://api.wipmania.com/jsonp?callback=${callback}`

   元件會呼叫JSONP服務並列出傳回資料包含的所有屬性。 清單中的屬性是可在Client Context中使用的屬性。

   ![ JSONP服務的屬性](assets/chlimage_1-40.png)

1. 按一下「確定」。
1. 返回Geometrixx Outdoors首頁並重新整理頁面。 Client Context現在包含來自JSONP存放區元件的資訊。

   ![填入資料的JSONP元件範例](assets/chlimage_1-41.png)

### 建立區段 {#create-the-segment}

使用您透過JSONP存放區元件建立的工作階段存放區中的資料。 區段會使用工作階段存放區的緯度和目前日期，判斷這是否為使用者端位置的冬季時間。

1. 在網頁瀏覽器(`https://localhost:4502/miscadmin#/etc`)中開啟[工具]主控台。
1. 在資料夾樹狀結構中，按一下Tools/Segmentation資料夾，然後按一下「新增>新增資料夾」。 指定下列屬性值，然後按一下「建立」：

   * 名稱： mysegments
   * 標題：我的區段

1. 選取「我的區段」資料夾，然後按一下「新增>新增頁面」：

   1. 在「標題」中輸入Winter。
   1. 選取區段範本。
   1. 按一下「建立」。

1. 以滑鼠右鍵按一下Winter區段，然後按一下「開啟」。
1. 將一般存放區屬性拖曳至預設的AND容器。

   ![正在將元件加入區段編輯器](assets/chlimage_1-5.jpeg)

1. 連按兩下元件以開啟編輯對話方塊，指定下列屬性值，然後按一下確定：

   * 商店： wipmania
   * 屬性名稱： latitude
   * 運運算元：大於
   * 屬性值： 30

1. 將指令碼元件拖曳至相同的AND容器，並開啟其編輯對話方塊。 新增下列指令碼，然後按一下確定：

   `3 < new Date().getMonth() < 12`
