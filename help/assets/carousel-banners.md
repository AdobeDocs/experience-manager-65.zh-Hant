---
title: 輪播橫幅
description: 了解如何在Dynamic Media中使用輪播橫幅
uuid: 73684a08-d84d-4665-ab89-3a1bf88ac5dd
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e26c7f7f-bdd7-421a-8614-ba48abf381d2
docset: aem65
feature: Carousel Banners
role: User, Admin
exl-id: 53d34d3a-ecb6-4fa0-9665-60d21f48021e
source-git-commit: 5192a284c38eb10c214c67a8727de0f7dd4d1ee2
workflow-type: tm+mt
source-wordcount: '4730'
ht-degree: 2%

---

# 輪播橫幅{#carousel-banners}

轉盤橫幅可讓行銷人員輕鬆建立互動式旋轉促銷內容，並將其傳遞至任何畫面，借此促進轉換。

建立和修改促銷橫幅中特有的內容可能非常耗時，限制您快速發佈新內容或使其更具針對性的能力。 輪播橫幅可讓您快速建立或修改旋轉橫幅。 您可以添加交互功能（如連結到產品詳細資訊或相關資源的熱點），並將它們提供到任何螢幕，從而讓您更快地將新促銷內容推向市場。

輪播橫幅是由具有單字的橫幅指定 **[!UICONTROL 卡魯塞]**

![chlimage_1-438](assets/chlimage_1-438.png)

在您的網站上，輪播橫幅可以如下所示：

![chlimage_1-439](assets/chlimage_1-439.png)

您可以在此導覽影像（按一下數字）。 此外，幻燈片會根據您可以自定義的時間間隔自動旋轉。 您在轉盤橫幅中新增的影像支援熱點和影像地圖，使用者可在其中選取或前往超連結或存取快速檢視視窗。

在此示例中，用戶已點選或按一下影像映射，並訪問手套的「快速視圖」窗口：

![chlimage_1-440](assets/chlimage_1-440.png)

## 觀看輪播橫幅的建立方式 {#watch-how-carousel-banners-are-created}

在上播放逐步說明 [輪播橫幅的建立方式](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner)（10分33秒）。 您也可以了解如何預覽、編輯和傳送輪播橫幅。

>[!NOTE]
>
>必須將非管理使用者新增至 **[!UICONTROL dam-users]** 群組，以便能夠建立或編輯輪播橫幅。 如果您在建立或編輯時遇到問題，請咨詢系統管理員，該管理員可將您添加到 **[!UICONTROL dam-users]** 群組。

## 快速入門：輪播橫幅 {#quick-start-carousel-banners}

若要使用輪播橫幅快速上手並執行：

1. [識別熱點和影像映射變數](#identifying-hotspot-and-image-map-variables) (僅限使用Experience Manager Assets + Dynamic Media的客戶)

   首先，找出現有Quickview實作所使用的動態變數，以便在Adobe Experience Manager Assets中轉盤橫幅建立程式期間正確輸入熱點和影像地圖資料。

   >[!NOTE]
   >
   >如果您是Experience Manager Sites或電子商務客戶，可以使用內建功能來導覽至產品頁面，並查閱產品目錄中的現有SKU（存貨單位）。 您不需要手動輸入熱點或影像地圖變數。 請參閱 [設定電子商務](/help/commerce/cif-classic/administering/generic.md).
   >
   >
   >如果您是Experience Manager Assets和Dynamic Media客戶，請手動輸入熱點和影像地圖的資料，然後將發佈的URL或內嵌程式碼與您的協力廠商內容管理系統整合。

1. 可選：視需 [要建立轉盤集檢視器預設](/help/assets/managing-viewer-presets.md)。

   如果您是管理員，則可建立自己的轉盤檢視器預設集，以自訂轉盤的行為和外觀。 主要優點是，您可以對多個輪播重複使用此自訂檢視器預設集。 不過，使用者可選擇在編寫轉盤時直接自訂轉盤的行為和外觀。 當您想要指定輪播的特定設計時，此方法是慣用的方法。

1. [上傳影像橫幅](#uploading-image-banners).

   上傳您要製作互動式的影像橫幅。

1. [建立轉盤集](#creating-carousel-sets).

   在輪播集中，用戶瀏覽橫幅影像，並選擇熱點或影像映射以訪問相關內容。

   若要在資產中建立轉盤集，請選取 **[!UICONTROL 建立]**，然後選取 **[!UICONTROL 轉盤集]**. 新增資產至投影片並選取 **[!UICONTROL 儲存]**. 您也可以直接在編輯器中編輯轉盤的外觀和行為。

1. [將熱點或影像映射添加到影像橫幅](#adding-hotspots-or-image-maps-to-an-image-banner).

   新增一或多個熱點或影像地圖至影像橫幅，並將每個熱點或影像地圖與連結、快速檢視或體驗片段等動作建立關聯。 添加熱點或影像映射後，通過發佈輪播集來完成此任務。 發佈會建立內嵌程式碼，供您複製並套用至網站登陸頁面。

   請參閱 [（選用）預覽輪播橫幅](#optional-previewing-carousel-banners)  — 選用。 如有需要，您可以檢視輪播集的呈現，並測試其互動性。

1. [發佈輪播橫幅](#publishing-carousel-banners).

   您發佈轉盤集的方式與發佈任何資產的方式相同。 在「資產」中，導覽至轉盤集，然後選取它並選取 **[!UICONTROL 發佈]**. 「發佈轉盤集」會啟用URL和內嵌字串。

1. 執行下列任一項作業：

   * [將輪播橫幅新增至您的網站頁面](#adding-a-carousel-banner-to-your-website-page) 您可以新增已複製到網站頁面的轉盤橫幅URL或內嵌程式碼。

      * [將轉盤橫幅與現有的Quickview整合](#integrating-the-carousel-banner-with-an-existing-quickview). 如果您使用協力廠商網頁內容管理系統，您必須將新的轉盤橫幅與網站上現有的Quickview實作整合。
   * [以Experience Manager將轉盤橫幅新增至您的網站](/help/assets/adding-dynamic-media-assets-to-pages.md) 如果您是Experience Manager Sites客戶，可使用互動式媒體元件，將轉盤集直接新增至Experience Manager中的頁面。


若要編輯轉盤集，請參閱 [編輯轉盤集](#editing-carousel-sets). 此外，您也可以檢視及編輯 [轉盤集屬性](manage-assets.md#editing-properties).

## 識別熱點和影像地圖變數 {#identifying-hotspot-and-image-map-variables}

首先，找出現有Quickview實作所使用的動態變數，以便在Experience Manager Assets中轉盤集建立程式期間，正確輸入熱點或影像地圖資料。

在Experience Manager Assets中將熱點或影像地圖新增至橫幅影像時，請指派SKU和選用的其他變數至每個熱點或影像地圖。 這些變數稍後用於匹配熱點或影像映射與Quickview內容。

>[!NOTE]
>
>如果您是Experience Manager Sites和/或Experience Manager電子商務客戶，請略過此步驟。 您不需要手動識別熱點或影像地圖變數；您可以將與Ecommerce的整合用於產品整合。 請參閱 [設定電子商務](/help/commerce/cif-classic/administering/generic.md). 此外，您也可以使用互動式元件，並將其新增至您的網頁。
>
>如果您是Experience Manager Assets或Media客戶，請發佈URL或內嵌程式碼，然後與您的協力廠商內容管理系統整合，並手動識別熱點和影像地圖。

請務必正確識別要與熱點或影像地圖資料建立關聯的變數數目和類型。 新增至橫幅影像的每個熱點或影像地圖都必須包含足夠的資訊，以明確識別現有後端系統中的產品。 同時，每個熱點或影像地圖不得包含超過必要的資料。 原因在於，這會使資料輸入程式過於複雜，且持續的熱點或影像地圖管理更容易出錯。

有不同的方式可識別要用於熱點或影像地圖資料的一組變數。

有時，與負責現有Quickview實施的IT專家協商就足夠了。 他們可能知道在系統中標識Quickview所需的最少資料集。 不過，通常也可以簡單分析前端程式碼的現有行為。

大多數Quickview實施都使用下列範例：

* 使用者在網站上啟動使用者介面元素。例如，點選 **[!UICONTROL 快速檢視]** 按鈕。
* 網站會視需要傳送Ajax要求至後端，以載入Quickview資料或內容。
* 快速檢視資料會轉譯為內容，以準備在網頁上轉譯。
* 最後，前端代碼在螢幕上直觀地呈現這樣的內容。

接著，方法是造訪實作「快速檢視」功能之現有網站的不同區域。 觸發Quickview，並擷取網頁所傳送的Ajax URL，以載入Quickview資料或內容。

通常您不需要使用任何專用的除錯工具。 現代網頁瀏覽器的功能是能夠勝任工作的網頁檢查員。 以下是一些Web瀏覽器的示例，其中包括Web檢查員：

* 若要在Google Chrome中查看所有傳出的HTTP要求，請按F12(Windows)或Command-Option-I(Mac)以開啟「開發人員工具」面板，然後選取「網路」標籤。
* 在Firefox中，您可以按F12(Windows)或Command-Option-I(Mac)並使用其Net標籤來啟動Firebug外掛程式，或使用內建的偵測器工具及其網路標籤。

在瀏覽器中開啟網路監視時，觸發頁面上的快速檢視。

現在，在網路記錄中找到Quickview Ajax URL，並複製記錄的URL以供日後分析之用。 通常，當您觸發Quickview時，會有許多請求會傳送至伺服器。 Quickview Ajax URL通常是清單中第一個的URL。 它有複雜的查詢字串部分或路徑，其響應MIME類型為 `text/html`, `text/xml`，或 `text/javascript`.

在此程式中，請務必瀏覽網站的不同區域，包含不同的產品類別和類型。 原因是Quickview URL的部分是指定網站類別的共同部分，但只有當您造訪網站的其他區域時才會變更。

在最簡單的情況下，Quickview URL中唯一的變數部分是產品SKU。 在此情況下，SKU值是您唯一需要將熱點或影像映射添加到橫幅影像的資料段。

但是，在複雜的情況下，Quickview URL除了SKU以外，還有不同的元素，例如類別ID、顏色代碼和大小代碼。 在這種情況下，每個元素都是熱點中的個別變數，或輪播橫幅功能中的影像地圖資料定義。

請考量下列Quickview URL範例及其產生的熱點或影像地圖變數：

<table>
 <tbody>
  <tr>
   <td>在查詢字串中找到的單一SKU。</td>
   <td><p>錄制的Quickview URL包括：</p>
    <ul>
     <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>URL中唯一的變數部分是 <code>productId=</code> 查詢字串參數，且顯然是SKU值。 因此，熱點或影像映射只需要填入值(如 <code>866558,</code> <code>1196184,</code> <code>1081492,</code> <code>1898294.</code></p> </td>
  </tr>
  <tr>
   <td>單一SKU，可在URL路徑中找到。</td>
   <td><p>錄制的Quickview URL包括：</p>
    <ul>
     <li><p><code>https://server/product/6422350843</code></p> </li>
     <li><p><code>https://server/product/1607745002</code></p> </li>
     <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>變數部分位於路徑的最後一部分，它將成為熱點/影像映射的SKU值：<strong><code>6422350843</code>, <code>1607745002,</code> </strong><code>0086724882.</code></p> </td>
  </tr>
  <tr>
   <td>查詢字串中的SKU和類別ID。</td>
   <td><p>錄制的Quickview URL包括：</p>
    <ul>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>在此情況下，URL中會有兩個不同的部分。 SKU儲存在 <code>prodId</code> 參數和類別ID儲存在 <code>category=</code>參數。</p> <p>因此，熱點/影像地圖定義是配對。 也就是說，SKU值和稱為的額外變數 <code>categoryId</code>. 產生的配對如下：</p>
    <ul>
     <li><p>SKU是 <strong><code>305466</code></strong> 和 <code>categoryId</code> is <code>1100004</code>.</p> </li>
     <li><p>SKU是 <strong><code>310181</code></strong> 和 <code>categoryId</code> is <strong><code>1100004</code></strong>.</p> </li>
     <li><p>SKU是 <strong><code>308706</code></strong> 和 <code>categoryId</code> is <strong><code>1740148</code></strong>.</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 上傳影像橫幅 {#uploading-image-banners}

如果您已上傳要使用的影像，請前往下一個步驟， [建立轉盤集](#creating-carousel-sets). 請注意，在啟用Dynamic Media後，必須上傳輪播中使用的影像。

若要上傳影像橫幅，請參閱 [上傳資產](/help/assets/manage-assets.md).

## 建立轉盤集 {#creating-carousel-sets}

>[!NOTE]
>
>必須將非管理使用者新增至 **[!UICONTROL dam-users]** 群組，以建立或編輯輪播橫幅。 如果您在建立或編輯時遇到問題，請咨詢系統管理員，該管理員可將您添加到 **[!UICONTROL dam-users]** 群組。

**若要建立轉盤集：**

1. 在「資產」中，導覽至您要建立轉盤集的資料夾，然後前往 **[!UICONTROL 建立]** > **[!UICONTROL 轉盤集]**.
1. 在轉盤橫幅編輯器頁面上，選取 **[!UICONTROL 點選以開啟資產選擇器]** 來選擇第一張幻燈片的影像。

   在轉盤橫幅編輯器頁面上，執行下列其中一項操作：

   * 在頁面左上角附近，選取 **[!UICONTROL 添加幻燈片]** 表徵圖。

   * 在頁面中間附近，選取 **[!UICONTROL 點選以開啟資產選擇器]**.
   選取以選取您要納入轉盤集的資產。 選取的資產上面有核取標籤圖示。完成後，在頁面右上角附近選取 **[!UICONTROL 選擇]**.

   使用「資產選擇器」，您可以輸入關鍵字並點選或按一下「退貨」來搜尋 **[!UICONTROL 資產]**。您也可以套用篩選條件來調整搜尋結果。您可以依路徑、系列、檔案類型和標籤來篩選。選取篩選，然後選取 **[!UICONTROL 篩選]** 表徵圖。 點選「檢視」圖示並選取「欄檢視」、「卡片檢視」或「清 **[!UICONTROL 單檢視」]**, **[!UICONTROL 以變更]**&#x200B;檢視 ****。

   請參閱 [使用選取器](/help/assets/working-with-selectors.md) 以取得更多資訊。

1. 繼續新增投影片，直到新增您要在轉盤集中旋轉的所有影像為止。
1. （選用）執行下列任一操作：

   * 如有必要，請拖曳幻燈片以重新排序清單中的影像。
   * 若要刪除影像，請選取影像，然後選取 **[!UICONTROL 刪除幻燈片]** 的上界。

   * 若要套用預設集，在頁面右上角附近，選取預設集下拉式清單，然後選取要一次套用至該集的預設集。
   要刪除幻燈片，請選擇該幻燈片，然後在工具欄上，選擇 **[!UICONTROL 刪除幻燈片]**. 要移動幻燈片，請選擇重新排序表徵圖，並按住並移動到所需位置。

1. 在幻燈片中添加影像後，可以將熱點、影像映射或兩者添加到影像中。 請參閱 [將熱點或影像映射添加到影像橫幅](#adding-hotspots-or-image-maps-to-an-image-banner).
1. 您可以變更轉盤集的視覺設計和行為。 選取 **[!UICONTROL 行為]** 和 **[!UICONTROL 外觀]** 標籤，並調整輪播橫幅的顯示方式或特定元件的行為。 請參閱 [管理檢視器預設集](/help/assets/viewer-presets.md) 以取得如何使用檢視器編輯器的詳細資訊。

   >[!NOTE]
   >
   >對於輪播橫幅，您可以調整下列項目：
   >
   >    * 影像顯示的持續時間。 依預設，每個影像會顯示9秒。
   >    * 動畫. 依預設，每個投影片轉變都會淡出。 您可以將其變更為滑動轉變。
   >    * 按鈕的樣式。 使用者可以點選每個點或數字來旋轉橫幅。 您可以更改設定指示符按鈕的顯示位置（以及它們是數字或點狀樣式）及其大小。
   >    * 更改影像映射的突出顯示樣式或用於熱點的表徵圖。
   >    * 編輯檢視器預設集之前，請選取您要根據預設集的樣式。 如果您沒有選擇樣式，當您開始編輯檢視器預設集時，如果您決定變更不同的預設集，則會失去所有變更。

   >
   >請參閱 [輪播橫幅的特殊考量](/help/assets/managing-viewer-presets.md#special-considerations-for-creating-a-carousel-banner-viewer-preset) 以取得檢視器編輯器的詳細指示和詳細資訊。

   您也可以預覽輪播橫幅的顯示方式。 請參閱 [（選用）預覽輪播橫幅](#optional-previewing-carousel-banners).

1. 選擇 **[!UICONTROL 儲存]** 完成時。

## 向影像橫幅添加熱點或影像映射 {#adding-hotspots-or-image-maps-to-an-image-banner}

您可以使用轉盤集編輯器將熱點或影像地圖新增至橫幅。

添加熱點或影像映射時，可以將其定義為快速視圖彈出式顯示、超連結或體驗片段。

請參閱 [體驗片段](/help/sites-authoring/experience-fragments.md).

>[!NOTE]
>
>將檢視器內嵌在體驗片段時，不支援輪播橫幅中的社交媒體共用工具。
>
>若要解決此問題，您可以使用或建立沒有社交媒體共用工具的檢視器預設集。 這類檢視器預設集可讓您成功將其內嵌在體驗片段中。

將熱點或影像映射添加到影像時，請記住保存您的工作。 目前建立/編輯工作階段期間，支援在頁面右上角附近還原和重做選項。

當您完成轉盤橫幅的建立時，您可以選擇使用「預覽」來查看向客戶呈現的轉盤橫幅。

請參閱 [（選用）預覽輪播橫幅](#optional-previewing-carousel-banners).

>[!NOTE]
>
>將熱點添加到 [互動式影像](/help/assets/interactive-images.md) 或者輪播橫幅，熱點資訊儲存在相同的中繼資料位置。 該位置是相對於影像的位置，無論是互動式影像還是輪播橫幅。 此功能表示您可以在任一檢視器中輕鬆重複使用相同的影像（及其定義的熱點資料）。
不過，請注意，轉盤橫幅支援影像上的影像地圖，這些影像也可能包含熱點；互動式影像則否。 如果您要建立使用相同影像的互動式影像或輪播橫幅，請記住此規則。 請考慮使用相同影像的個別副本建立互動式影像和輪播橫幅。

>[!NOTE]
如果您正在使用熱點編輯互動式影像並裁切影像，則會刪除熱點。

另請參閱 [新增影像地圖](/help/assets/image-maps.md).

**要將熱點或影像映射添加到影像橫幅：**

1. 從「資產」，導覽至您要進行互動式的轉盤集。
1. 選取轉盤集並選取 **[!UICONTROL 編輯]**. 轉盤檢視器編輯器隨即開啟。
1. 選取您要進行互動式的投影片。
1. 在頁面左上角附近，選取 **[!UICONTROL 熱點]** 或 **[!UICONTROL 影像圖]**.
1. 執行下列任一操作：

   * 對於熱點：在影像上，選取要熱點出現的位置。
   * 對於影像映射：在影像上，選取，然後從左上角拖曳至右下方，以建立影像地圖區域。 通過拖動角，可以調整影像映射的大小。

   如有必要，請將熱點或影像映射拖動到新位置。 根據需要添加其他熱點或影像映射。

   若要刪除熱點或影像地圖，請選取 **[!UICONTROL 動作]** 標籤。 在「地 **[!UICONTROL 圖與熱點]** 」標題下，從「選定類型 **** 」下拉菜單中，選擇要刪除的熱點或影像映射的名稱。選取 **[!UICONTROL 垃圾]** 圖示，然後選取 **[!UICONTROL 刪除]**.

1. 在「名稱」文本欄位中，鍵入熱點或影像映射的名稱。 此名稱也會顯示在 **[!UICONTROL 地圖與熱點]** 下拉式清單。 如果您決定在未來變更熱點或影像地圖，提供名稱可讓您輕鬆識別熱點或影像地圖。
1. 在 **[!UICONTROL 動作]** 標籤：

   * 選擇 **[!UICONTROL 快速檢視]**.

      * 如果您是Experience Manager Sites和Ecommerce客戶，請選取「產品選擇器」圖示（放大鏡）以開啟「選取產品」頁面。 選取您要使用的產品，然後選取頁面右上角的核取記號，以便您返回轉盤橫幅編輯器。
      * 如果您不是Experience Manager Sites或電子商務客戶

         * 請參閱 [識別熱點變數](#identifying-hotspot-and-image-map-variables) 。
         * 然後，手動輸入SKU值。 在「SKU值」文字欄位中，輸入產品的SKU（庫存保存單位），這是您提供之每個不同產品或服務的唯一識別碼。 輸入的SKU值會自動填入Quickview模板的變數部分，以便系統知道將點選熱點與特定SKU的Quickview關聯。
         * （可選）如果「快速檢視」中有您必須用來進一步識別產品的其他變數，請選取 **[!UICONTROL 新增一般變數]**. 在文字欄位中，指定額外的變數。 例如， category=Mens是新增的變數。

         * 請參閱 [使用選取器](/help/assets/working-with-selectors.md) 以取得更多資訊。
   * 選擇 **[!UICONTROL 超連結]**.

      * 如果您是Experience Manager Sites客戶，請選取網站選取器圖示（資料夾）以導覽至URL。
         >[!NOTE]
         如果您的互動式內容有連結與相對URL(尤其是連結至Experience Manager Sites頁面)，則無法使用以URL為基礎的連結方法。

      * 如果您是獨立客戶，請在HREF文字欄位中，指定連結網頁的完整URL路徑。

   請務必指定要在新的瀏覽器標籤（建議的預設值）或相同的標籤中開啟連結。

   請參閱 [使用選取器](/help/assets/working-with-selectors.md) 以取得更多資訊。

   * 選擇 **[!UICONTROL 體驗片段]**.

      * 如果您是Experience Manager Sites客戶，請選取「搜尋」圖示（放大鏡）以開啟「體驗片段」頁面。 選取您要使用的體驗片段，然後選取 **[!UICONTROL 選擇]** 位於頁面的右上角，以便返回熱點管理頁面。
請參閱 [體驗片段](/help/sites-authoring/experience-fragments.md).

      * 指定在橫幅上顯示的體驗片段寬度和高度。

         >[!NOTE]
         將檢視器內嵌在體驗片段時，不支援輪播橫幅中的社交媒體共用工具。
         若要解決此問題，請建立沒有社交媒體共用工具的檢視器預設集。 這類檢視器預設集可讓您成功將其內嵌在體驗片段中。
   ![experience_fragment-carouselbanner](assets/experience_fragment-carouselbanner.png)

   您也可以預覽輪播橫幅的顯示方式。 請參閱 [（選用）預覽輪播橫幅](#optional-previewing-carousel-banners).

1. 選取&#x200B;**[!UICONTROL 儲存]**。
1. 發佈轉盤集。 發佈會建立您可在網站頁面上使用的內嵌程式碼或URL。 如果您是Experience Manager Sites客戶，可以直接將轉盤集新增至網頁。

   請參閱 [發佈資產](/help/assets/publishing-dynamicmedia-assets.md).

   請參閱 [新增轉盤集至您的網站登陸頁面](#adding-a-carousel-banner-to-your-website-page)

## 編輯轉盤集 {#editing-carousel-sets}

>[!NOTE]
必須將非管理使用者新增至 **[!UICONTROL dam-users]** 群組，以便能夠建立或編輯輪播橫幅。 如果您在建立或編輯時遇到問題，請咨詢系統管理員，該管理員可將您添加到 **[!UICONTROL dam-users]** 群組。

您可以對轉盤集執行各種編輯工作，例如：

* 將投影片新增至轉盤集。 另請參閱 [使用選取器](/help/assets/working-with-selectors.md).
* 在輪播集中重新排序幻燈片。
* 刪除轉盤集中的資產。
* 套用檢視器預設集。
* 刪除轉盤集。
* 添加或編輯熱點和影像映射。 另請參閱 [使用選取器](/help/assets/working-with-selectors.md).

**若要編輯轉盤集：**

1. 執行下列任一操作：

   * 暫留在轉盤集資產上，然後選取 **[!UICONTROL 編輯]** （鉛筆圖示）。
   * 將滑鼠指標暫留在轉盤集資產上，選取 **[!UICONTROL 選擇]** （勾選圖示），然後選取 **[!UICONTROL 編輯]** 的上界。

   * 選取「轉盤集」資產，然後在頁面的左上角選取 **[!UICONTROL 編輯]** （鉛筆圖示）。

1. 若要編輯轉盤集，請執行下列任一操作：

   * 要添加幻燈片，請選擇 **[!UICONTROL 添加幻燈片]** 圖示，然後導覽至您要新增至該投影片的資產，並選取核取記號。
   * 要重新排序幻燈片，請將幻燈片拖到新位置（選擇重新排序表徵圖以移動項目）。
   * 若要新增熱點或影像地圖，請選取熱點或影像地圖圖示並參閱 [添加熱點和影像映射](#adding-hotspots-or-image-maps-to-an-image-banner).
   * 若要編輯轉盤集的外觀或行為，請選取 **[!UICONTROL 外觀]** 標籤或 **[!UICONTROL 行為]** ，然後設定所需的選項。
   * 要編輯熱點或影像映射，請在相應的幻燈片上選擇熱點或影像映射，並根據需要在 **[!UICONTROL 動作]** 標籤。
   * 要刪除幻燈片，請選擇它，然後選擇 **[!UICONTROL 刪除幻燈片]** 的上界。
   * 若要套用預設集，請在頁面右上角附近選取 **[!UICONTROL 預設集]** 下拉式清單，然後選取檢視器預設集。
   * 若要刪除整個轉盤集，請導覽至轉盤集，選取它，然後選取 **[!UICONTROL 刪除]**.

   >[!NOTE]
   如果您正在使用熱點編輯互動式影像並裁切影像，則會刪除熱點。

## （選用）預覽輪播橫幅 {#optional-previewing-carousel-banners}

您可以使用「預覽」來查看客戶對轉盤橫幅的顯示方式，以及測試轉盤橫幅熱點和影像地圖，以確保它們的行為如預期般。

當您對輪播橫幅感到滿意時，即可發佈它。
請參閱 [將視訊或影像檢視器內嵌在網頁上](/help/assets/embed-code.md).
請參閱 [將URL連結至您的Web應用程式](/help/assets/linking-urls-to-yourwebapplication.md). 如果您的互動式內容有連結與相對URL(尤其是連結至Experience Manager Sites頁面)，則無法使用以URL為基礎的連結方法。
請參閱 [將Dynamic Media Assets新增至頁面](/help/assets/adding-dynamic-media-assets-to-pages.md).

您可以從轉盤編輯器（偏好的方法）或 **[!UICONTROL 檢視器]** 清單。

**若要預覽輪播橫幅：**

1. 在 **[!UICONTROL 資產]**，導覽至您建立的現有輪播橫幅，並選取以開啟它。
1. 選擇 **[!UICONTROL 編輯]**.
1. 在工具列右角的檢視器預設集清單中，選取檢視器以預覽轉盤橫幅。

   ![experience_fragment-carouselbanner-viewerdown](assets/experience_fragment-carouselbanner-viewerdropdown.png)

1. 選擇 **[!UICONTROL 預覽]**.
1. 選取影像上的熱點或影像映射，以便測試其關聯的操作。

**若要從「檢視器」清單預覽輪播橫幅：**

1. 在 **[!UICONTROL 資產]**，導覽至您建立的現有輪播橫幅，並選取以開啟它。
1. 在「預覽」頁面的左上角附近，選取「內容」圖示。
1. 在 **[!UICONTROL 檢視器]** 清單（在頁面左側的面板中），選取您要使用的轉盤橫幅檢視器預設集的名稱。
1. 選取影像上的熱點或影像映射，以便測試其關聯的操作。

## 發佈輪播橫幅 {#publishing-carousel-banners}

發佈輪播，方便您使用。 發佈轉盤集會啟用URL和內嵌程式碼。 它也會將轉盤發佈至Dynamic Media雲端，與CDN整合以提供可擴充且效能優異的傳送。

>[!NOTE]
如果您使用浮動切換橫幅的現有互動式影像與熱點，在您發佈浮動切換橫幅後，必須個別發佈互動式影像。
此外，如果您修改轉盤橫幅中使用的已發佈互動式影像，則必須先發佈互動式影像，這些變更才會反映在轉盤橫幅中。

請參閱 [發佈Dynamic Media Assets](/help/assets/publishing-dynamicmedia-assets.md) 以取得如何發佈輪播橫幅的資訊。

## 將輪播橫幅新增至您的網站頁面 {#adding-a-carousel-banner-to-your-website-page}

上傳橫幅影像以建立輪播、新增熱點和/或影像對應至橫幅並發佈輪播集後，您現在可以將其新增至現有的網站頁面。

>[!NOTE]
如果您是Experience Manager Sites客戶，您可以將互動式媒體元件拖曳至頁面，直接將輪播橫幅新增至頁面。 請參閱 [新增Dynamic Media資產至頁面](/help/assets/adding-dynamic-media-assets-to-pages.md).

不過，如果您是獨立的Experience Manager資產客戶，您可以依照本區段的說明，手動將輪播橫幅新增至您的網站登陸頁面。

1. 複製已發佈的轉盤集的內嵌程式碼。
請參閱 [將視訊或影像檢視器內嵌在網頁上](/help/assets/embed-code.md).

1. 將您從Experience Manager Assets複製的內嵌程式碼新增至網頁。
複製的內嵌程式碼會回應，因此必須自動符合頁面的內嵌區域。

## 將轉盤橫幅與現有的Quickview整合 {#integrating-the-carousel-banner-with-an-existing-quickview}

>[!NOTE]
只有當您是獨立Experience Manager Assets客戶時，才適用此步驟。

此程式的最後一個步驟是將轉盤橫幅與網站上現有的Quickview實作整合。 每個Quickview實施都是獨一無二的，而且需要一種特定的方法，需要前端IT人員的協助。

現有的Quickview實施通常會依下列順序呈現網頁上發生的一系列相關動作：

1. 使用者會在您網站的使用者介面中觸發元素。
1. 前端程式碼會根據步驟1中觸發的使用者介面元素來取得快速檢視URL。
1. 前端程式碼會使用步驟2取得的URL來傳送Ajax要求。
1. 後端邏輯會將對應的Quickview資料或內容傳回前端程式碼。
1. 前端程式碼會載入Quickview資料或內容。
1. （可選）前端代碼將載入的Quickview資料轉換為HTML表示。
1. 前端程式碼會顯示強制回應對話方塊或面板，並在畫面上為一般使用者轉譯HTML內容。

這些呼叫不代表獨立的公用API呼叫，而網頁邏輯可從任意步驟呼叫。 相反地，它是連結呼叫，其中每個後續步驟都會隱藏在前一個步驟的最後一個階段（回撥）中。

當使用者點選轉盤橫幅內的熱點或影像地圖時，輪播橫幅正在取代步驟1和部分步驟2，此類互動會由檢視器處理。 檢視器會將事件傳回至網頁，其中包含先前新增的所有熱點或影像地圖資料。

在這種事件處理常式中，前端程式碼會執行下列動作：

* 監聽轉盤橫幅發出的事件。
* 根據熱點或影像地圖資料建構Quickview URL。
* 觸發從後端載入Quickview並在畫面上呈現以供顯示的程式。

Experience Manager Assets傳回的內嵌程式碼已有可供使用的事件處理常式，且已註解。

因此，只需取消對代碼的註解，並將虛擬處理程式主體替換為特定網頁特有的代碼。

構建Quickview URL的過程與用於識別先前覆蓋的熱點和影像映射變數的過程相反。

請參閱 [識別熱點和影像地圖變數](#identifying-hotspot-and-image-map-variables).

觸發Quickview URL並啟動Quickview面板的最後一個步驟很可能需要IT部門的前端IT人員協助。 他們具備最佳知識，了解如何從正確的步驟準確觸發Quickview實施，並擁有可供使用的Quickview URL。

## 使用Quickview建立自訂快顯視窗 {#using-quickviews-to-create-custom-pop-ups}

請參閱 [使用Quickview建立自訂快顯視窗](/help/assets/custom-pop-ups.md).
