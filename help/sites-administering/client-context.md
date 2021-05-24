---
title: ClientContext
seo-title: ClientContext
description: 了解如何在AEM中使用用戶端內容。
seo-description: 了解如何在AEM中使用用戶端內容。
uuid: 82b2f976-cb41-42f8-ad4b-3a5cd23cc5f5
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 7a3322fe-554e-479e-a27c-4259cdd3ba2e
docset: aem65
exl-id: 69c66c82-fbd6-406e-aefd-b85480a62109
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1889'
ht-degree: 0%

---

# ClientContext{#client-context}

>[!NOTE]
>
>客戶端上下文已被ContextHub取代。 如需詳細資訊，請參閱相關的[configuration]ch-configuring.md)和[developer](/help/sites-developing/contexthub.md)檔案。

「用戶端內容」是一種機制，可提供您目前頁面和訪客的特定資訊。 可使用&#x200B;**Ctrl-Alt-c**(windows)或&#x200B;**control-option-c**(Mac)開啟：

![](assets/clientcontext_alisonparker.png)

在[發佈與製作環境中，都會顯示以下相關資訊：](#propertiesavailableintheclientcontext)

* 訪客；根據您的執行個體，會要求或衍生特定資訊。
* 頁面標籤以及目前訪客存取這些標籤的次數（當您將滑鼠移至特定標籤上方時，就會顯示）。
* 頁面資訊。
* 技術環境資訊；例如IP位址、瀏覽器和螢幕解析度。
* 目前已解析的任何區段。

圖示（僅限製作環境中使用）可讓您設定用戶端內容的詳細資訊：

![](do-not-localize/clientcontext_icons.png)

* ****
編輯將開啟一個新頁面，允許您 [編輯、添加或刪除配置檔案屬性](#editingprofiledetails)。

* ****
載入您 [可以從設定檔清單中選取，並載](#loading-a-new-user-profile) 入您要測試的設定檔。

* ****
重設您可 [以將設](#resetting-the-profile-to-the-current-user) 定檔重設為目前使用者的設定檔。

## 可用客戶端上下文元件{#available-client-context-components}

「客戶端上下文」可以顯示以下屬性（[，具體取決於使用Edit](#adding-a-property-component)選擇的內容）:

**瀏覽** 者資訊顯示下列用戶端資訊：

* **IP地址**
* **** 用於搜尋引擎反向連結的關鍵字
* 使用的&#x200B;**browser**
* 使用的&#x200B;**OS**（作業系統）
* 螢幕&#x200B;**解析度**
* **滑鼠X**&#x200B;位置
* **滑鼠Y**&#x200B;位置

**活** 動資料流這可提供使用者在各種平台上的社交活動的相關資訊；例如，AEM論壇、部落格、評等等。

**** 促銷活動可讓作者模擬促銷活動的特定體驗。此元件會覆寫一般促銷活動解析度和體驗選取，以啟用各種排列的測試。

促銷活動解析度通常以促銷活動的優先順序屬性為基礎。 體驗通常會根據區段來選取。

**** 購物車顯示購物車資訊，包括產品項目（標題、數量、價格格式化等）、解析的促銷活動（標題、訊息等）和憑單（代碼、說明等）。

購物車工作階段存放區也會使用ClientContextCartServlet通知伺服器已解析的促銷變更（根據分段變更）。

**通** 用儲存是顯示儲存內容的通用元件。它是通用儲存屬性元件的較低級別版本。

一般存放區必須以JS轉譯器設定，且轉譯器會以自訂方式顯示資料。

**通用儲** 存屬性是顯示儲存內容的通用元件。它是通用儲存元件的更高級別版本。

「通用儲存屬性」元件包含一個預設的轉譯器，該轉譯器列出配置的屬性（連同縮圖）。

**** 地理位置顯示用戶端的經緯度。它會使用HTML5地理位置API來查詢瀏覽器的目前位置。 這會導致快顯視窗顯示給訪客，瀏覽器會在快顯視窗中詢問訪客是否同意共用其位置。

在Context Cloud中顯示時，元件會使用Google API將地圖顯示為縮圖。 元件受Google API [使用限制](https://developers.google.com/maps/documentation/staticmaps/intro#Limits)的約束。

>[!NOTE]
>
>在AEM 6.1中，地理位置存放區不再提供反向地理編碼功能。 因此，地理位置存放區不再擷取目前位置的詳細資訊，例如城市名稱或國家/地區代碼。 使用此存放區資料的區段無法正常運作。 地理位置存放區僅包含位置的經緯度。

**JSONP儲** 存顯示與安裝相關內容的元件。

JSONP標準是JSON的補充，可規避相同的來源政策（使網頁應用程式無法與位於其他網域的伺服器通訊）。 它包含將JSON物件包裝在函式呼叫中，以便能夠從其他網域（這是相同來源原則允許的例外）將其載入為`<script>`。

JSONP儲存區與任何其他儲存區一樣，但它載入來自其他網域的資訊，而不需要擁有代理來取得目前網域的資訊。 請參閱[透過JSONP](/help/sites-administering/client-context.md#storing-data-in-client-context-via-jsonp)在用戶端內容中儲存資料中的範例。

>[!NOTE]
>
>JSONP儲存區不會快取Cookie中的資訊，但會在每次頁面載入時擷取該資料。

**設定** 檔資料顯示在使用者設定檔中收集的資訊。例如性別、年齡、電子郵件地址等。

**已解** 析的區段顯示目前解析的區段（通常取決於用戶端內容中顯示的其他資訊）。這在設定促銷活動時很有意義。

例如，滑鼠當前是位於窗口的左手部分還是右手部分。 此區段主要用於測試，因為可立即看到變更。

**社** 交圖表顯示使用者朋友和追隨者的社交圖表。

>[!NOTE]
>
>目前，此示範功能需仰賴示範使用者設定檔節點上預先設定的資料集來運作。 例如，請參閱：
>
>`/home/users/geometrixx/aparker@geometrixx.info/profile` =>朋友屬性

**標** 記雲端顯示在目前頁面上設定的標籤，以及在瀏覽網站時收集的標籤。將滑鼠移至標籤上會顯示目前使用者存取包含該特定標籤之頁面的次數。

>[!NOTE]
在DAM資產上設定的標籤若顯示在已造訪的頁面上，則不會計入。

**技術圖** 形儲存此元件取決於您的安裝。

**** ViewedProducts追蹤購物者已檢視的產品。可以查詢最近查看的產品，或購物車中尚未查看的最近查看的產品。

此會話儲存沒有預設的客戶端上下文元件。

如需詳細資訊，請參閱[詳細資訊中的用戶端內容](/help/sites-developing/client-context.md)。

>[!NOTE]
頁面資料不再是在用戶端內容中作為預設元件。 如有需要，您可以編輯用戶端內容、新增&#x200B;**一般存放區屬性**&#x200B;元件，然後設定此元件，將&#x200B;**存放區**&#x200B;定義為`pagedata`。

## 更改客戶端上下文配置檔案{#changing-the-client-context-profile}

客戶端上下文允許您交互更改詳細資訊：

* 變更用戶端內容中使用的設定檔可讓您查看不同使用者在目前頁面會看到的不同體驗。
* 除了變更使用者設定檔，您還可以變更一些設定檔詳細資訊，以了解不同條件下的頁面體驗差異。

### 載入新用戶配置檔案{#loading-a-new-user-profile}

您可以透過下列任一項來變更設定檔：

* [使用載入圖示](#loading-a-new-visitor-profile-with-the-load-profile-icon)
* [使用選取滑桿](#loadinganewvisitorprofilewiththeselectionslider)

完成後，您可以[重設設定檔](#resetting-the-profile-to-the-current-user)。

#### 載入具有載入描述檔圖示{#loading-a-new-visitor-profile-with-the-load-profile-icon}的新訪客描述檔

1. 按一下「載入描述檔」圖示：

   ![](do-not-localize/clientcontext_loadprofile.png)

1. 這會開啟對話方塊，您可以在此處選取要載入的設定檔：

   ![](assets/clientcontext_profileloader.png)

1. 按一下&#x200B;**OK**&#x200B;載入。

#### 使用選擇滑塊{#loading-a-new-user-profile-with-the-selection-slider}載入新用戶配置檔案

您也可以使用選取滑桿選取描述檔：

1. 連按兩下代表目前使用者的圖示。 選取器將會開啟，使用箭頭來導覽並查看可用的設定檔：

   ![](assets/clientcontext_profileselector.png)

1. 按一下您要載入的設定檔。 載入詳細資料時，按一下選取器外部以關閉。

#### 將配置檔案重置為當前用戶{#resetting-the-profile-to-the-current-user}

1. 使用重設圖示將用戶端內容中的設定檔傳回給目前使用者的設定檔：

   ![](do-not-localize/clientcontext_resetprofile.png)

### 變更瀏覽器平台{#changing-the-browser-platform}

1. 連按兩下代表瀏覽器平台的圖示。 選取器將會開啟，使用箭頭來導覽並查看可用的平台/瀏覽器：

   ![](assets/clientcontext_browserplatform.png)

1. 按一下您要載入的平台瀏覽器。 載入詳細資料時，按一下選取器外部以關閉。

### 更改地理位置{#changing-the-geolocation}

1. 連按兩下地理位置圖示。 將會開啟展開的地圖，您可以在此處將標籤拖曳到新位置：

   ![](assets/clientcontext_geomocationrelocate.png)

1. 按一下地圖外部以關閉。

### 更改標籤選擇{#changing-the-tag-selection}

1. 連按兩下用戶端內容的「標籤雲端」區段。 對話方塊將會開啟，您可在此選取標籤：

   ![](assets/clientcontext_tagselection.png)

1. 按一下「確定」以載入到客戶端上下文。

## 編輯客戶端上下文{#editing-the-client-context}

編輯用戶端內容可用來設定（或重設）某些屬性的值、新增屬性或移除不再需要的屬性。

### 編輯屬性詳細資訊{#editing-property-details}

編輯用戶端內容可用來設定（或重設）特定屬性的值。 這可讓您測試特定藍本（對[segmentation](/help/sites-administering/campaign-segmentation.md)和[campaigns](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)特別有用）。

![](assets/clientcontext_alisonparker_edit.png)

### 添加屬性元件{#adding-a-property-component}

開啟&#x200B;**ClientContext設計頁面**&#x200B;後，您也可以使用可用元件&#x200B;**新增**&#x200B;全新屬性（元件會列在sidekick上，或在&#x200B;**拖曳元件或資產至此**&#x200B;方塊後開啟的&#x200B;**插入新元件**&#x200B;對話方塊中）:

![](assets/clientcontext_alisonparker_new.png)

### 刪除屬性元件{#removing-a-property-component}

開啟&#x200B;**ClientContext設計頁面**&#x200B;後，如果不再需要，您也可以&#x200B;**刪除**&#x200B;屬性。 這包括現成可用的屬性；**重設**&#x200B;將在移除後恢復這些值。

## 透過JSONP {#storing-data-in-client-context-via-jsonp}在用戶端內容中儲存資料

請依照此示例使用JSONP儲存上下文儲存元件將外部資料添加到客戶端上下文。 接著，根據該資料中的資訊建立區段。 此示例使用WIPmania.com提供的JSONP服務。 該服務基於Web客戶端的IP地址返回地理位置資訊。

此範例使用Geometrixx Outdoors範例網站來存取「用戶端內容」並測試建立的區段。 只要頁面已啟用「用戶端內容」，您就可以使用不同的網站。 （請參閱[將客戶端上下文添加到頁面](/help/sites-developing/client-context.md#adding-client-context-to-a-page)。）

### 添加JSONP儲存元件{#add-the-jsonp-store-component}

將JSONP儲存元件添加到客戶端上下文，並使用它檢索和儲存有關Web客戶端的地理位置資訊。

1. 開啟AEM製作例項上Geometrixx Outdoors網站的英文首頁。 ([https://localhost:4502/content/geometrixx-outdoors/en.html](https://localhost:4502/content/geometrixx-outdoors/en.html))。
1. 要開啟「客戶端上下文」，請按Ctrl-Alt-c(windows)或control-option-c(Mac)。
1. 按一下「客戶端上下文」頂部的編輯表徵圖以開啟「客戶端上下文設計器」。

   ![](do-not-localize/chlimage_1.png)

1. 將JSONP儲存元件拖曳至用戶端內容。

   ![](assets/chlimage_1-4.jpeg)

1. 按兩下元件以開啟編輯對話方塊。
1. 在「JSONP服務URL」框中，輸入以下URL，然後按一下「提取儲存」：

   `https://api.wipmania.com/jsonp?callback=${callback}`

   元件會呼叫JSONP服務，並列出傳回資料包含的所有屬性。 清單中的屬性是那些將在客戶端上下文中可用的屬性。

   ![](assets/chlimage_1-40.png)

1. 按一下「確定」。
1. 返回Geometrixx Outdoors首頁並重新整理頁面。 用戶端內容現在包含來自JSONP儲存元件的資訊。

   ![](assets/chlimage_1-41.png)

### 建立區段{#create-the-segment}

使用您使用JSONP儲存元件建立的工作階段存放區資料。 區段會使用工作階段存放區的緯度和目前日期，判斷是否為用戶端位置的冬季時間。

1. 在Web瀏覽器中開啟工具控制台(`https://localhost:4502/miscadmin#/etc`)。
1. 在資料夾樹中，按一下「工具/分段」資料夾，然後按一下「新增>新增資料夾」。 指定下列屬性值，然後按一下「建立」：

   * 名稱：mysegments
   * 標題：我的區段

1. 選取「我的區段」資料夾，然後按一下「新增>新增頁面」：

   1. 在「Title（標題）」中，鍵入Winter。
   1. 選取「區段」範本。
   1. 按一下建立。

1. 以滑鼠右鍵按一下「冬季」區段，然後按一下「開啟」。
1. 將「一般商店屬性」拖曳至預設的AND容器。

   ![](assets/chlimage_1-5.jpeg)

1. 按兩下元件以開啟編輯對話框，指定以下屬性值，然後按一下確定：

   * 商店：維馬尼亞
   * 屬性名稱：latitude
   * 運算子：大於
   * 屬性值：30

1. 將指令碼元件拖曳至相同的AND容器，並開啟其編輯對話方塊。 添加以下指令碼，然後按一下「確定」：

   `3 < new Date().getMonth() < 12`
