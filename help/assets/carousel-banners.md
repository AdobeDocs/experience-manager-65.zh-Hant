---
title: 輪播橫幅
description: 瞭解如何在Dynamic Media使用轉盤橫幅
uuid: 73684a08-d84d-4665-ab89-3a1bf88ac5dd
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e26c7f7f-bdd7-421a-8614-ba48abf381d2
docset: aem65
feature: 輪播橫幅
role: 業務從業人員、管理員
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '4807'
ht-degree: 3%

---


# 輪播橫幅{#carousel-banners}

轉盤橫幅可讓行銷人員輕鬆建立互動式旋轉促銷內容，並將它發佈至任何螢幕，以推動轉化。

建立和修改促銷橫幅中的內容可能相當耗時，限制了您快速發佈新內容或使其更具針對性的能力。 轉盤橫幅可讓您快速建立或修改旋轉橫幅、新增連結至產品細節或相關資源的熱點等互動功能，並將它們傳送至任何螢幕，讓您更快速地將新的促銷內容推向市場。

轉盤橫幅由單字&#x200B;**[!UICONTROL CAROUSELSET]**&#x200B;的橫幅指定：

![chlimage_1-438](assets/chlimage_1-438.png)

在您的網站上，轉盤橫幅的外觀如下：

![chlimage_1-439](assets/chlimage_1-439.png)

您可以在這裡導覽影像（按一下數字）。 此外，投影片會根據您可自訂的時間間隔自動旋轉。 您在轉盤橫幅中新增的影像同時支援熱點和影像地圖，使用者可以點選或前往超連結或存取快速檢視視窗。

在此範例中，使用者點選或點選影像地圖，並存取手套的快速檢視視窗：

![chlimage_1-440](assets/chlimage_1-440.png)

## 觀看轉盤橫幅的建立方式{#watch-how-carousel-banners-are-created}

觀看[如何建立轉盤橫幅的10分鐘33秒逐步解說。 ](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner)您也將學習如何預覽、編輯和傳遞轉盤橫幅。

>[!NOTE]
>
>必須將非管理使用者新增至&#x200B;**[!UICONTROL dam-users]**&#x200B;群組，才能建立或編輯轉盤橫幅。 如果您在建立或編輯時遇到問題，請洽詢系統管理員，可將您新增至&#x200B;**[!UICONTROL dam-users]**&#x200B;群組。

## 快速入門：轉盤橫幅{#quick-start-carousel-banners}

要快速啟動並運行，請執行以下操作：

1. [識別熱點和影像地圖變數](#identifying-hotspot-and-image-map-variables) (僅適用於使用AEM Assets+Dynamic Media的客戶)

   首先，識別現有快速檢視實作所使用的動態變數，以便在AEM Assets的轉盤橫幅廣告建立程式中，正確輸入熱點和影像地圖資料。

   >[!NOTE]
   >
   >如果您是AEM Sites或電子商務客戶，您可以使用內建功能導覽至產品頁面，並查閱產品目錄中的現有sku。 您不需要手動輸入熱點或影像地圖變數。 請參閱[設定電子商務的相關資訊。](/help/sites-administering/generic.md)
   >
   >
   >如果您是AEM Assets和Dynamic Media的客戶，您將手動輸入熱點和影像地圖的資料，然後將發佈的URL或內嵌程式碼整合到您的協力廠商內容管理系統。

1. 可選：視需 [要建立轉盤集檢視器預設](/help/assets/managing-viewer-presets.md)。

   如果您是管理員，則可以建立自己的轉盤檢視器預設集，自訂轉盤的行為和外觀。 主要優點是，您可以針對多個轉盤重複使用此自訂檢視器預設集。 不過，使用者也可以選擇在製作轉盤時直接自訂轉盤的行為和外觀。 當您想要特定轉盤的設計時，這是您偏好的方法。

1. [上傳影像橫幅](#uploading-image-banners)。

   上傳您要製作互動式影像橫幅。

1. [建立轉盤集](#creating-carousel-sets)。

   在「轉盤集」中，使用者瀏覽橫幅影像，並點選熱點或影像地圖以存取相關內容。

   若要在資產中建立轉盤集，請點選「 **[!UICONTROL 建立]**」，然後選 **[!UICONTROL 取轉盤集。]**&#x200B;將資產新增至投影片並點選「 **[!UICONTROL 儲存」。]**&#x200B;您也可以直接在編輯器中編輯轉盤的外觀和行為。

1. [將熱點或影像映射添加到影像橫幅。](#adding-hotspots-or-image-maps-to-an-image-banner)

   將一個或多個熱點或影像映射添加到影像橫幅，並將每個熱點或影像映射與諸如連結、Quickview或體驗片段之類的操作關聯。 添加熱點或影像映射後，通過發佈轉盤集完成此任務。 發佈會建立可用來複製並套用至網站登陸頁面的內嵌代碼。

   請參閱[（選用）預覽轉盤橫幅](#optional-previewing-carousel-banners) —— 選用。 視需要，您可以檢視轉盤集的呈現方式並測試其互動性。

1. [發佈轉盤橫幅。](#publishing-carousel-banners)

   您會像發佈任何資產一樣發佈轉盤集。 在「資產」中，導覽至「轉盤集」並選取它，然後點選「**[!UICONTROL 發佈」。]** 發佈轉盤集會啟動URL和內嵌字串。

1. 執行下列任一項作業：

   * [將轉盤橫幅新增至您的網](#adding-a-carousel-banner-to-your-website-page) 站頁面您可以新增已複製至網站頁面的轉盤橫幅URL或內嵌代碼。

      * [將轉盤橫幅與現有的Quickview整合](#integrating-the-carousel-banner-with-an-existing-quickview)。如果您使用協力廠商的Web內容管理系統，您將需要將新的轉盤橫幅與網站上現有的Quickview實作整合。
   * [在](/help/assets/adding-dynamic-media-assets-to-pages.md) AEMI中將轉盤橫幅加入您的網站如果您是AEM Sites的客戶，您可以使用互動式媒體元件將轉盤集直接加入AEM的頁面。


如果需要編輯轉盤集，請參閱[編輯轉盤集。](#editing-carousel-sets) 此外，您還可以檢視和編輯「轉盤 [集」屬性](manage-assets.md#editing-properties)。

## 識別熱點和影像映射變數{#identifying-hotspot-and-image-map-variables}

首先，識別現有快速檢視實作所使用的動態變數，以便在AEM Assets的轉盤集建立程式中，正確輸入熱點或影像地圖資料。

將熱點或影像地圖新增至AEM Assets的橫幅影像時，您需要為每個熱點或影像地圖指派SKU和選用的其他變數。 這些變數稍後會用來比對熱點或影像地圖與快速檢視內容。

>[!NOTE]
>
>如果您是AEM Sites和／或電AEM子商務客戶，請略過此步驟。 您不需要手動識別熱點或影像地圖變數；您可以使用與Ecommerce的整合進行產品整合。 請參閱[設定電子商務的相關資訊。 ](/help/sites-administering/generic.md)此外，您也可以使用互動式元件並將它新增至網頁。
>
>如果您是AEM Assets或媒體客戶，請發佈URL或內嵌代碼，然後與您的協力廠商內容管理系統整合，並手動識別熱點和影像地圖。

請務必正確識別要與熱點或影像地圖資料關聯的變數數目和類型。 每個新增至橫幅影像的熱點或影像地圖都必須包含足夠的資訊，以明確識別現有後端系統中的產品。 同時，每個熱點或影像映射不應包含比需要的更多資料。 這是因為這會使資料輸入程式過於複雜，而且持續的熱點或影像地圖管理更容易出錯。

有不同的方法可識別一組要用於熱點或影像地圖資料的變數。

有時，與負責實施現有快速視圖的IT專家協商可能足夠，因為他們可能知道在系統中識別快速視圖所需的最低資料集。 不過，在大多數情況下，您也可以只分析前端程式碼的現有行為。

大部份的快速檢視實作都採用下列範例：

* 使用者在網站上啟動使用者介面元素。例如，點選「快速檢 **[!UICONTROL 視」按鈕]** 。
* 如有需要，網站會傳送Ajax要求至後端以載入快速檢視資料或內容。
* 快速檢視資料會轉譯為內容，以準備在網頁上轉譯。
* 最後，前端程式碼會以視覺化方式在螢幕上呈現此類內容。

然後，方法是瀏覽現有網站中實施快速檢視功能的不同區域，觸發快速檢視並擷取網頁所傳送的Ajax URL，以載入快速檢視資料或內容。

通常您不需使用任何專用的除錯工具。 現代網頁瀏覽器採用Web檢視器，可讓您完成適當的工作。 以下是包含Web檢視程式的Web瀏覽器範例：

* 若要在Google Chrome中查看所有傳出的HTTP要求，請按F12(Windows)或Command-Option-I(Mac)以開啟「開發人員工具」面板，然後點選「網路」標籤。
* 在Firefox中，您可以按F12(Windows)或Command-Option-I(Mac)並使用其「網路」標籤來啟動Firebug外掛程式，或使用內建的「偵測器」工具及其「網路」標籤。

在瀏覽器中開啟網路監視時，觸發頁面上的快速檢視。

現在，在網路記錄檔中尋找快速檢視的Ajax URL，並複製已記錄的URL以供日後分析。 在大多數情況下，當您觸發快速檢視時，會有許多請求傳送至伺服器。 通常，快速檢視Ajax URL是清單中第一個檢視的URL。 它有複雜的查詢字串部分或路徑，其回應MIME類型為`text/html`、`text/xml`或`text/javascript`。

在此程式中，請務必造訪您網站的不同區域，以及不同的產品類別和類型。 原因是快速檢視URL可能有特定網站類別的常見部分，但只有在您造訪網站的不同區域時才會變更。

在最簡單的情況下，快速檢視URL中唯一的變數部分是產品SKU。 在此例中，SKU值是您在橫幅影像中新增熱點或影像地圖所需的唯一資料片段。

但是，在複雜情況下，快速檢視URL除了SKU以外，還有不同的元素，例如類別ID、顏色代碼、大小代碼等。 在這種情況下，每個元素都是熱點中的個別變數，或轉盤橫幅功能中的影像地圖資料定義。

請考慮下列快速檢視URL的範例，以及產生的熱點或影像地圖變數：

<table>
 <tbody>
  <tr>
   <td>單一SKU，可在查詢字串中找到。</td>
   <td><p>錄制的快速檢視URL包括：</p>
    <ul>
     <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>URL中唯一的變數部分是<code>productId=</code>查詢字串參數的值，而它顯然是SKU值。 因此，我們的熱點或影像地圖只需要填入值(例如 <code>866558,</code> <code>1196184,</code> <code>1081492,</code> <code>1898294.</code></p> </td>
  </tr>
  <tr>
   <td>單一SKU，位於URL路徑中。</td>
   <td><p>錄制的快速檢視URL包括：</p>
    <ul>
     <li><p><code>https://server/product/6422350843</code></p> </li>
     <li><p><code>https://server/product/1607745002</code></p> </li>
     <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>變數部分位於路徑的最後一部分，並成為熱點／影像映射的SKU值：<strong><code>6422350843</code>、<code>1607745002,</code> </strong><code>0086724882.</code></p> </td>
  </tr>
  <tr>
   <td>查詢字串中的SKU和類別ID。</td>
   <td><p>錄制的快速檢視URL包括：</p>
    <ul>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>在此例中，URL中有兩個不同的部分。 SKU會儲存在<code>prodId</code>參數中，而類別ID會儲存在<code>category=</code>參數中。</p> <p>因此，熱點／影像映射定義是對。 亦即SKU值和名為<code>categoryId</code>的其他變數。 產生的對如下：</p>
    <ul>
     <li><p>SKU為<strong><code>305466</code></strong>,<code>categoryId</code>為<code>1100004</code>。</p> </li>
     <li><p>SKU為<strong><code>310181</code></strong>,<code>categoryId</code>為<strong><code>1100004</code></strong>。</p> </li>
     <li><p>SKU為<strong><code>308706</code></strong>,<code>categoryId</code>為<strong><code>1740148</code></strong>。</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 上傳影像橫幅{#uploading-image-banners}

如果您已上傳您要使用的影像，請進入下一個步驟[建立轉盤集](#creating-carousel-sets)。 請注意，轉盤中使用的影像必須在啟用Dynamic Media後上傳。

若要上傳影像橫幅，請參閱[上傳資產](/help/assets/manage-assets.md)。

## 建立轉盤集{#creating-carousel-sets}

>[!NOTE]
>
>必須將非管理使用者新增至&#x200B;**[!UICONTROL dam-users]**&#x200B;群組，才能建立或編輯轉盤橫幅。 如果您在建立或編輯時遇到問題，請洽詢系統管理員，可將您新增至&#x200B;**[!UICONTROL dam-users]**&#x200B;群組。

**要建立轉盤集**

1. 在「資產」中，導覽至您要建立轉盤集的資料夾，然後點選「建立>轉盤集」。]****[!UICONTROL 
1. 在「轉盤橫幅編輯器」頁面上，點選&#x200B;**[!UICONTROL 以開啟「資產選擇器」]**&#x200B;以選取您第一張投影片的影像。

   在「轉盤橫幅編輯器」頁面上，執行下列其中一項作業：

   * 在頁面左上角附近，點選&#x200B;**[!UICONTROL 新增投影片]**&#x200B;圖示。

   * 在頁面中間點選&#x200B;**[!UICONTROL 點選以開啟資產選擇器。]**
   點選以選取您要納入轉盤集的資產。選取的資產上面有核取標籤圖示。完成後，在頁面右上角附近點選&#x200B;**[!UICONTROL 選擇]**。

   使用「資產選擇器」，您可以輸入關鍵字並點選或按一下「退貨」來搜尋 **[!UICONTROL 資產。]**&#x200B;您也可以套用篩選條件來調整搜尋結果。您可以依路徑、系列、檔案類型和標籤來篩選。選取篩選，然後點選工具 **[!UICONTROL 列上的]** 「篩選」圖示。點選「檢視」圖示並選取「欄檢視」**[!UICONTROL 「欄檢視」]**、「卡片檢視」]**或「清單檢視」，以變更檢視。]****[!UICONTROL **[!UICONTROL 

   如需詳細資訊，請參閱[使用選擇器](/help/assets/working-with-selectors.md)。

1. 繼續新增投影片，直到您在轉盤集中新增要旋轉的所有影像。
1. （可選）執行下列任一項作業：

   * 如有必要，請拖曳投影片，以重新排序影像。
   * 若要刪除影像，請選取影像，然後點選工具列上的「刪除投影片」。****

   * 若要套用預設集，請在頁面右上角附近點選預設下拉式清單，然後選取一個預設集以一次套用至該預設集。
   若要刪除投影片，請點選或按一下投影片，然後點選或按一下工具列中的「刪除投影片」。 ****&#x200B;若要移動投影片，請點選訂單圖示並按住並移至所要的位置。

1. 在投影片中新增影像後，您可以將熱點、影像地圖或兩者新增至影像。 請參閱[添加熱點或影像映射](#adding-hotspots-or-image-maps-to-an-image-banner)。
1. 您可以點選或按一下「行為」和「外觀」標籤，並調整轉盤橫幅的外觀或特定元件的行為，以變更轉盤集的視覺設計和行為。 如需如何使用檢視器編輯器的詳細資訊，請參閱[管理檢視器預設集](/help/assets/viewer-presets.md)。

   >[!NOTE]
   >
   >對於轉盤橫幅，您可能需要調整下列項目：
   >    * 影像顯示的持續時間。 依預設，每張影像會顯示9秒。
   >    * 動畫. 依預設，每張投影片轉場都是淡入。 您可以將它變更為投影片轉場。
   >    * 按鈕的樣式。 使用者可以點選每個點或數字，在橫幅中旋轉。 您可以變更設定指標按鈕的顯示位置（如果是數值或虛線樣式），以及其大小。
   >    * 更改影像映射或用於熱點的表徵圖的加亮樣式。
   >    * 在編輯檢視器預設集之前，請選擇您要以預設集為基礎的樣式。 如果您不這麼做，當您開始編輯檢視器預設集時，如果您決定變更為其他預設集，將會遺失您的所有變更。

   >
   >請參閱[轉盤橫幅的特殊考量，以取得檢視器編輯器的詳細指示和詳細資訊。](/help/assets/managing-viewer-presets.md#special-considerations-for-creating-a-carousel-banner-viewer-preset)

   您也可以預覽轉盤橫幅的外觀。 請參閱[（可選）預覽轉盤橫幅](#optional-previewing-carousel-banners)。

1. 完成後，點選「**[!UICONTROL 儲存]**」。

## 將熱點或影像映射添加到影像橫幅{#adding-hotspots-or-image-maps-to-an-image-banner}

您可以使用轉盤集編輯器將熱點或影像地圖新增至橫幅。

添加熱點或影像映射時，可以將其定義為「快速視圖」彈出式顯示、超連結或體驗片段。

請參閱[體驗片段](/help/sites-authoring/experience-fragments.md)。

>[!NOTE]
>
>請注意，當您將檢視器內嵌在體驗片段時，不支援轉盤橫幅中的社交媒體分享工具。
>
>若要解決這個問題，您可以使用或建立沒有社交媒體分享工具的檢視器預設集。 這些檢視器預設集可讓您成功將它內嵌在「體驗片段」中。

在將熱點或影像映射添加到影像時，請記住保存您所做的工作。 在目前的建立／編輯作業階段中，支援在頁面右上角的「復原」和「重做」選項。

完成轉盤橫幅的建立後，您可選擇使用「預覽」來檢視轉盤橫幅對客戶的呈現方式。

請參閱[（可選）預覽轉盤橫幅。](#optional-previewing-carousel-banners)

>[!NOTE]
>
>當您在[互動式影像](/help/assets/interactive-images.md)或轉盤橫幅中新增熱點至影像時，熱點資訊會儲存在相同的中繼資料位置——相對於影像的位置&amp;控制面板，不論它是互動式影像或轉盤橫幅。 這項功能表示，您可以在任一檢視器中，輕鬆地重複使用相同的影像及其定義的熱點資料。
但是，請注意，轉盤橫幅支援影像上的影像地圖，這些影像也可能包含熱點；互動式影像則否。 如果您想要建立使用相同影像的互動式影像或轉盤橫幅，請記住這一點。 您可能想要使用相同影像的個別副本來建立互動式影像和轉盤橫幅。

>[!NOTE]
如果您正在編輯具有熱點的互動式影像並裁剪影像，則會刪除熱點。

另請參閱[添加映像映射](/help/assets/image-maps.md)。

**要將熱點或影像映射添加到影像橫幅**

1. 從「資產」導覽至您要建立互動功能的轉盤集。
1. 選擇轉盤集，然後點選「**[!UICONTROL 編輯」。]** 「轉盤檢視器編輯器」隨即開啟。
1. 選取您要製作互動式的投影片。
1. 在頁面的左上角附近，點選&#x200B;**[!UICONTROL 熱點]**&#x200B;或&#x200B;**[!UICONTROL 影像地圖。]**
1. 執行下列任一項作業：

   * 對於熱點：在影像上，點選您要熱點出現的位置。
   * 對於影像地圖：在影像上按一下，然後從左上角拖曳至右下方，以建立影像對應區域。 您可以拖曳轉角來調整影像地圖的大小。

   如有必要，請將熱點或影像映射拖動到新位置。 視需要新增其他熱點或影像地圖。

   若要刪除熱點或影像地圖，請點選「動 **[!UICONTROL 作]** 」標籤。在「地 **[!UICONTROL 圖與熱點]** 」標題下，從「選定類型 **** 」下拉菜單中，選擇要刪除的熱點或影像映射的名稱。點選功能表旁的&#x200B;**[!UICONTROL 垃圾筒]**&#x200B;圖示，然後點選&#x200B;**[!UICONTROL 刪除。]**

1. 在「名稱」文本欄位中，鍵入熱點或影像映射的名稱。 此名稱也會出現在&#x200B;**[!UICONTROL 地圖與熱點]**&#x200B;下拉式清單中。 如果您決定在未來對熱點或影像映射進行更改，提供名稱可以很容易地識別熱點或影像映射。
1. 在&#x200B;**[!UICONTROL Actions]**&#x200B;標籤中執行下列操作之一：

   * 點選&#x200B;**[!UICONTROL Quickview。]**

      * 如果您是AEM Sites和電子商務客戶，請點選「產品選擇器」圖示（放大鏡）以開啟「選擇產品」頁面。 點選您要使用的產品，然後點選頁面右上角的核取標籤，以返回轉盤橫幅編輯器。
      * 如果您不是AEM Sites或電子商務客戶

         * 請參閱[識別熱點變數](#identifying-hotspot-and-image-map-variables)，如同您想要定義這些變數。
         * 然後，手動輸入SKU值。 在「SKU值」文字欄位中，輸入產品的SKU（庫存保留單位），此為您提供之每個不同產品或服務的唯一識別碼。 輸入的SKU值會自動填入快速檢視範本的變數部分，讓系統知道將點選的熱點與特定SKU的快速檢視產生關聯。
         * （可選）如果快速檢視中有其他變數需要用來進一步識別產品，請點選「新增一般變數」。**** 在文字欄位中，指定其他變數。例如，category=Mens是新增的變數。

         * 如需詳細資訊，請參閱[使用選擇器](/help/assets/working-with-selectors.md)。
   * 點選「**[!UICONTROL 超連結」。]**

      * 如果您是AEM Sites客戶，請點選網站選擇器圖示（資料夾）以導覽至URL。
         >[!NOTE]
         如果您的互動式內容具有相對URL的連結，尤其是連結至AEM Sites頁面，則無法使用以URL為基礎的連結方法。

      * 如果您是獨立客戶，請在HREF文字欄位中，指定連結網頁的完整URL路徑。

   請確定您要指定是在新的瀏覽器標籤（建議預設值）或相同的標籤中開啟連結。

   如需詳細資訊，請參閱[使用選擇器](/help/assets/working-with-selectors.md)。

   * 點選「體驗片段」。]****[!UICONTROL 

      * 如果您是AEM Sites客戶，請點選「搜尋」圖示（放大鏡）以開啟「體驗片段」頁面。 點選或按一下您要使用的體驗片段，然後點選頁面右上角的「選取」以返回熱點管理頁面。
請參閱[體驗片段](/help/sites-authoring/experience-fragments.md)。

      * 指定「體驗片段」在橫幅上顯示的寬度和高度。

         >[!NOTE]
         請注意，當您將檢視器內嵌在體驗片段時，不支援轉盤橫幅中的社交媒體分享工具。
         若要解決這個問題，您可以使用或建立沒有社交媒體分享工具的檢視器預設集。 這些檢視器預設集可讓您成功將它內嵌在「體驗片段」中。
   ![experience_fragment-carouselbanner](assets/experience_fragment-carouselbanner.png)

   您也可以預覽轉盤橫幅的外觀。 請參閱[（可選）預覽轉盤橫幅](#optional-previewing-carousel-banners)。

1. 點選&#x200B;**[!UICONTROL 儲存。]**
1. 發佈轉盤集。 發佈會建立您可在網站頁面上使用的內嵌代碼或URL。 如果您是AEM Sites客戶，可將轉盤集直接加入網頁。

   請參閱[發佈資產](/help/assets/publishing-dynamicmedia-assets.md)。

   請參閱[將浮動切換集新增至您的網站登陸頁面](#adding-a-carousel-banner-to-your-website-page)

## 編輯轉盤集{#editing-carousel-sets}

>[!NOTE]
必須將非管理使用者新增至&#x200B;**[!UICONTROL dam-users]**&#x200B;群組，才能建立或編輯轉盤橫幅。 如果您在建立或編輯時遇到問題，請洽詢系統管理員，可將您新增至&#x200B;**[!UICONTROL dam-users]**&#x200B;群組。

您可以對轉盤集執行多種編輯工作，例如：

* 將投影片加入轉盤集。 另請參閱[使用選擇器](/help/assets/working-with-selectors.md)。
* 在轉盤集中重新排序投影片。
* 刪除浮動切換集中的資產。
* 套用檢視器預設集。
* 刪除轉盤集。
* 添加或編輯熱點和影像映射。 另請參閱[使用選擇器](/help/assets/working-with-selectors.md)。

**要編輯轉盤集**

1. 執行下列任一項作業：

   * 將滑鼠指標暫留在轉盤集資產上，然後點選&#x200B;**[!UICONTROL 編輯]**（鉛筆圖示）。
   * 將滑鼠指標暫留在轉盤集資產上，點選&#x200B;**[!UICONTROL 選擇]**（勾選圖示），然後點選工具列上的&#x200B;**[!UICONTROL 編輯]**。

   * 點選「轉盤集」資產，然後在頁面的左上角點選「**[!UICONTROL 編輯]**」（鉛筆圖示）。

1. 要編輯轉盤集，請執行下列任一操作：

   * 若要新增投影片，請點選「新增投影片」圖示，然後導覽至您要新增至該投影片的資產，然後點選或按一下核取標籤。****
   * 若要重新排序投影片，請將投影片拖曳至新位置（選取重新排序圖示以移動項目）。
   * 要添加熱點或影像映射，請按一下熱點或影像映射表徵圖，並查看[添加熱點和影像映射](#adding-hotspots-or-image-maps-to-an-image-banner)。
   * 若要編輯轉盤集的外觀或行為，請點選&#x200B;**[!UICONTROL 外觀]**&#x200B;標籤或&#x200B;**[!UICONTROL 行為]**&#x200B;標籤，然後設定您想要的選項。
   * 要編輯熱點或影像映射，請在相應的幻燈片上選擇熱點或影像映射，並根據需要在&#x200B;**[!UICONTROL Actions]**&#x200B;頁籤下進行更改。
   * 若要刪除投影片，請選取它，然後點選工具列上的「刪除投影片」。****
   * 若要套用預設集，請在頁面右上角附近點選&#x200B;**[!UICONTROL Preset]**&#x200B;下拉式清單，然後選取檢視器預設集。
   * 若要刪除整個轉盤集，請導覽至轉盤集，選取它，然後點選&#x200B;**[!UICONTROL 刪除。]**

   >[!NOTE]
   如果您正在編輯具有熱點的互動式影像並裁剪影像，則會刪除熱點。

## （可選）預覽轉盤橫幅{#optional-previewing-carousel-banners}

您可以使用「預覽」來查看轉盤橫幅對客戶的外觀，並測試轉盤橫幅熱點和影像地圖，以確保它們如預期般運作。

當您對轉盤橫幅感到滿意時，可以發佈它。
請參閱[將視訊或影像檢視器內嵌至網頁](/help/assets/embed-code.md)。
請參閱[將URL連結至您的Web應用程式](/help/assets/linking-urls-to-yourwebapplication.md)。 請注意，如果您的互動式內容具有相對URL的連結，尤其是連結至AEM Sites頁面，則無法使用以URL為基礎的連結方法。
請參閱[將Dynamic Media資產新增至頁面。](/help/assets/adding-dynamic-media-assets-to-pages.md)

您可以從轉盤編輯器（首選方法）或&#x200B;**[!UICONTROL 檢視器]**&#x200B;清單中預覽轉盤橫幅。

**若要預覽轉盤橫幅**

1. 在&#x200B;**[!UICONTROL Assets]**&#x200B;中，導覽至您所建立的現有轉盤橫幅，並點選以開啟它。
1. 點選&#x200B;**[!UICONTROL 編輯。]**
1. 在工具列右角的檢視器預設集清單中，選取檢視器以預覽轉盤橫幅。

   ![experience_fragment-carouselbanner-viewerdropfon](assets/experience_fragment-carouselbanner-viewerdropdown.png)

1. 點選&#x200B;**[預覽。]**
1. 點選影像上的熱點或影像地圖，以測試其相關動作。

**若要從檢視器清單預覽轉盤橫幅**

1. 在&#x200B;**[!UICONTROL Assets]**&#x200B;中，導覽至您所建立的現有轉盤橫幅，並點選以開啟它。
1. 在「預覽」頁面的左上角附近，按一下「內容」圖示。
1. 在頁面左側面板的&#x200B;**[!UICONTROL 檢視器]**&#x200B;清單中，點選您要使用的轉盤橫幅檢視器預設集的名稱。
1. 點選影像上的熱點或影像地圖，以測試其相關動作。

## 發佈轉盤橫幅{#publishing-carousel-banners}

您必須發佈轉盤才能使用。 發佈轉盤集會啟動URL和內嵌代碼。 它還將轉盤發佈至與CDN整合的Dynamic Media雲端，以進行可擴充和效能傳送。

>[!NOTE]
如果您使用具有浮動切換橫幅熱點的現有互動影像，則必須在發佈浮動切換橫幅後個別發佈互動影像。
此外，如果您修改了在轉盤橫幅中使用的預先存在的已發佈互動影像，則必須先發佈互動影像，這些變更才會反映在轉盤橫幅中。

如需如何發佈轉盤橫幅的資訊，請參閱[發佈Dynamic Media資產](/help/assets/publishing-dynamicmedia-assets.md)。

## 新增轉盤橫幅至您的網站頁面{#adding-a-carousel-banner-to-your-website-page}

上傳橫幅影像以建立轉盤、新增熱點和／或影像對應至橫幅，並發佈轉盤集後，您現在可以將它新增至現有的網站頁面。

>[!NOTE]
如果您是AEM Sites的客戶，可將互動式媒體元件拖曳至頁面，直接將轉盤橫幅加入您的頁面。 請參閱[將Dynamic Media資產新增至頁面。](/help/assets/adding-dynamic-media-assets-to-pages.md)

不過，如果您是單機版資產客AEM戶，您可以依本節所述，手動將轉盤橫幅新增至網站登陸頁面。

1. 複製已發佈的轉盤集的內嵌代碼。
請參閱[將視訊或影像檢視器內嵌至網頁](/help/assets/embed-code.md)。

1. 將您從AEM Assets複製的內嵌代碼新增至您的網頁。
複製的內嵌程式碼會回應，因此應會自動符合頁面的內嵌區域。

## 將轉盤橫幅與現有快速檢視整合{#integrating-the-carousel-banner-with-an-existing-quickview}

注意：此步驟僅適用於您是獨立的AEM Assets客戶。

此程式的最後一個步驟是將轉盤橫幅與網站上現有的快速檢視實施整合。 每個快速檢視實作都是獨一無二的，而且需要一種最可能需要前端IT人員協助的特定方法。

現有的快速檢視實作通常代表一系列互動式動作，這些動作會依下列順序在網頁上發生：

1. 使用者會在您網站的使用者介面中觸發元素。
1. 前端程式碼會根據步驟1中觸發的使用者介面元素，取得快速檢視URL。
1. 前端程式碼會使用步驟2中取得的URL來傳送Ajax要求。
1. 後端邏輯會將對應的快速檢視資料或內容傳回前端程式碼。
1. 前端程式碼會載入快速檢視資料或內容。
1. 或者，前端代碼將載入的快速檢視資料轉換為HTML表示法。
1. 前端程式碼會顯示模式對話方塊或面板，並轉譯HTML內容給使用者。

這些呼叫可能不代表獨立的公用API呼叫，而網頁邏輯可透過任意步驟呼叫這些呼叫。 相反地，它是連結呼叫，在此連結呼叫中，前一個步驟的最後一個階段（回呼）中將隱藏下一個步驟。

在轉盤橫幅正在取代步驟1和部分步驟2的同時，當使用者按一下轉盤橫幅內的熱點或影像地圖時，檢視器會處理這類使用者互動。 檢視器會將事件傳回至網頁，其中包含先前新增的所有熱點或影像地圖資料。

在此類事件處理常式中，前端程式碼會執行下列動作：

* 監聽轉盤橫幅所發出的事件。
* 根據熱點或影像地圖資料建構快速檢視URL。
* 觸發從後端載入快速檢視並在螢幕上顯示的程式。

AEM Assets傳回的內嵌程式碼已有可供使用的事件處理常式，已加以註解。

因此，只需取消程式碼的註解，並以特定網頁專用的程式碼取代虛擬處理常式主體即可。

快速檢視URL的建立程式與先前所涵蓋的識別熱點和影像地圖變數的程式基本相反。

請參閱[識別熱點和影像映射變數](#identifying-hotspot-and-image-map-variables)。

觸發快速檢視URL並啟動快速檢視面板的最後一個步驟，很可能需要IT部門的前端IT人員協助。 他們具備最佳的知識，瞭解如何從正確的步驟精確觸發快速檢視實作，並擁有現成可用的快速檢視URL。

## 使用「快速檢視」建立自訂快顯視窗 {#using-quickviews-to-create-custom-pop-ups}

請參閱[使用快速檢視建立自訂快顯視窗](/help/assets/custom-pop-ups.md)。
