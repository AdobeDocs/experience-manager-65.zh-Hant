---
title: 互動式影像
description: 瞭解如何在動態媒體中處理互動式影像
uuid: 0bdb73f7-6ce9-4cdf-b6b5-a4d3d4e19a23
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: a6f58f6a-015a-4ced-941c-ef1b6d3e1d6f
docset: aem65
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# 互動式影像{#interactive-images}

將「可購買」的熱點拖放至影像上，即可輕鬆為客戶製作豐富、吸引人的靜態影像。 可購物熱點結合了有關產品或服務的其他資訊以及直接、銷售點「新增至購物車」或「購買」功能。 客戶可以點選或按一下這些熱點，並直接連結至產品或服務、將其新增至購物車，或連結至網頁。 此類直接體驗可提升客戶在您網站上的參與度和轉化率。

以下是具有快速檢視快顯視窗的可購物橫幅。 用戶通過在模型上點選圓或「熱點」來激活Quickview。

![chlimage_1-152](assets/chlimage_1-368.png)

前往下列網頁，檢視互動式影像在上述網頁上的實際運作：

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html)

## 觀看互動式影像橫幅的建立方式 {#watch-how-interactive-image-banners-are-created}

觀看如何建立互動式影像橫幅的10分 [鐘和33秒的逐步說明](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&emailurl=https://s7d5.scene7.com/s7/emailFriend&serverUrl=https://s7d5.scene7.com/is/image/&config=Scene7SharedAssets/Universal_HTML5_Video_social&contenturl=https://s7d5.scene7.com/skins/&asset=S7tutorials/InteractiveCarouselBanner)。 您也將學習如何預覽、編輯和傳遞互動式影像橫幅。

## 快速入門：互動式影像 {#quick-start-interactive-images}

下列逐步工作流程說明旨在協助您在AEM Assets中快速啟動並執行互動式影像。

在某些「快 **速啟動** 」任務中查找「示例」標題。 本教學課程包含以下網頁範例為基礎的簡短教學課程，目前尚未新增互動式影像：

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html)

本教學課程可協助您說明將互動式影像整合在您自己的網站上的步驟。

互動式影像步驟：

1. **（可選）識別熱點變數** -如果您使用AEM Assets和Dynamic Media獨立作業，請先識別現有Quickview實作中使用的動態變數，以便在建立互動式影像時輸入熱點資料。 請參 [閱（可選）識別熱點變數](#optional-identifying-hotspot-variables)。
不過，如果您使用AEM Sites或AEM eCommerce，或兩者皆使用，則不需要此步驟。
請參 [閱AEM Assets中的電子商務概念](/help/sites-administering/concepts.md)。

1. **（可選）建立互動式影像檢視器預設集** -自訂用於表示熱點的圖形影像。 如果您想要使用現成可用的互動式影像檢視器預設集，則不需要建立您自己的互動式影像檢視器預設集，而且此預設集的名稱是 `Shoppable_Banner` 現成的。
請參 [閱（選用）建立互動式影像檢視器預設集](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset)。

1. **上傳影像橫幅** -上傳您想要製作互動式的影像橫幅。
請參 [閱上傳影像橫幅](#uploading-an-image-banner)。

1. **將熱點添加到影像橫幅** -將一個或多個熱點添加到影像橫幅中，並將每個熱點與超連結、快速視圖或體驗片段等操作關聯。 添加熱點後，將通過發佈互動式影像完成此任務。
請參 [閱向影像橫幅添加熱點](#adding-hotspots-to-an-image-banner)。
請參 [閱預覽互動式影像](#optional-previewing-interactive-images) -選用。 視需要，您可以檢視可購買橫幅的呈現方式，並測試其互動性。
如需如 [何發佈互動式影像資產](/help/assets/publishing-dynamicmedia-assets.md) ，請參閱發佈資產。

1. **在AEM中將互動式影像新增至網站或網站**&#x200B;如果您使用AEM Sites、AEM eCommerce或兩者，您可以將互動式影像拖曳至頁面上，直接新增至AEM的網頁。 請參閱 [新增動態媒體資產至頁面。](/help/assets/adding-dynamic-media-assets-to-pages.md)
如果您單獨使用AEM Assets和Dynamic Media，則必須複製網站上的內嵌代碼，然後將它與您現有的Quickview整合。 請參 [閱整合互動式影像與您的網站](#integrating-an-interactive-image-with-your-website)。
如果您使用協力廠商WCM(Web Content Manager)，您必須將新的互動式視訊與網站上使用的現有Quickview實作整合。 請參 [閱將互動式影像與現有的Quickview整合](#integrating-an-interactive-image-with-an-existing-quickview)。

## （可選）識別熱點變數 {#optional-identifying-hotspot-variables}

>[!NOTE]
>
>只有在以下情況下，才需要此任務：
>
>* 您想要透過觸發至Quickviews，將互動功能加入影像。
>* 您的AEM實作不會使 *用* eCommerce整合架構，將產品資料從任何電子商務解決方案（例如IBM Websphere Commerce、Elastic Path、hybris或Intershop）拉入AEM。 請參 [閱AEM Assets中的電子商務概念](/help/sites-administering/concepts.md)。
>
>
如果您的AEM實作使用電子商務，您可以略過此工作並繼續下一個工作。

首先，您可以識別現有Quickview實作所使用的動態變數，以便輸入熱點資料以建立互動式影像。

當您在AEM Assets中將熱點新增至橫幅影像時，您必須指派SKU(庫存保留單位；您提供的每個不同產品或服務的唯一識別碼)，以及每個熱點的可選附加變數。 這些熱點變數稍後用於匹配熱點與Quickview內容。

請務必正確識別要與熱點資料關聯的變數數目和類型。 每個新增至橫幅影像的熱點都必須包含足夠的資訊，以明確識別現有後端系統中的產品。

有不同的方法可識別一組要用於熱點資料的變數。

有時，與負責現有Quickview實施的IT專家協商可能已足夠，因為他們可能知道在系統中標識Quickview所需的最低資料集。 不過，在大多數情況下，您也可以只分析前端程式碼的現有行為。

Quickview的大多數實施都採用以下模式：

* 使用者在網站上啟動使用者介面元素。 例如，按一下「快速視圖」按鈕。
* 如有需要，網站會傳送Ajax要求至後端以載入Quickview資料或內容。
* Quickview資料會轉譯為內容，以準備在網頁上轉譯。
* 最後，前端程式碼會以視覺化方式在螢幕上呈現此類內容。

接著，方法是造訪實施Quickview功能的現有網站的不同區域，觸發Quickview並擷取網頁所傳送的Ajax URL，以載入Quickview資料或內容。

通常您不需使用任何專用的除錯工具。 現代網頁瀏覽器採用Web檢視器，可讓您完成適當的工作。 以下是包含Web檢視程式的Web瀏覽器範例：

* 若要在Google Chrome中查看所有傳出的HTTP要求，請按F12以開啟「開發人員工具」面板，然後按一下「網路」標籤。
在Mac上，按Command+Option+I以開啟「開發人員工具」面板，然後按一下「網路」標籤。

* 在Firefox中，您可以按F12啟動Firebug外掛程式並使用其網頁標籤，或使用內建的檢查工具及其網路標籤。
在Mac上，按Command+Option+I以開啟「開發人員工具」面板，然後按一下「偵測器」標籤。

在瀏覽器中開啟網路監視時，觸發頁面上的Quickview。

現在，在網路記錄檔中尋找Quickview Ajax URL，並複製已記錄的URL以供日後分析。 在大多數情況下，當您觸發Quickview時，會有許多請求被發送到伺服器。 通常，Quickview Ajax URL是清單中第一個URL。 它有複雜的查詢字串部分或路徑，其回應MIME類型為 `text/html`、 `text/xml`或 `text/javascript`。

在此程式中，請務必造訪您網站的不同區域，以及不同的產品類別和類型。 原因是Quickview URL可能有特定網站類別的常用部分，但只有在您造訪網站的不同區域時才會變更。

在最簡單的情況下，Quickview URL中唯一的變數部分是產品SKU。 在這種情況下，SKU值是您在橫幅影像中新增熱點所需的唯一資料片段。

但是，在複雜情況下，Quickview URL除了SKU以外，還有不同的元素，例如類別ID、顏色代碼、大小代碼等。 在這種情況下，AEM Assets中可購買的互動式影像功能中，每個元素都是熱點資料定義中的個別變數。

請考慮以下Quickview URL及其產生的熱點變數範例：

<table>
  <tbody>
  <tr>
    <td><p>單一SKU，可在查詢字串中找到。</p> </td>
    <td><p>記錄的Quickview URL包括：</p>
    <ul>
      <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>URL中唯一的變數部分是productId=查詢字串參數的值，而它顯然是SKU值。 因此，我們的熱點只需要填入值如、、、 <strong><code>866558</code></strong>、 <strong><code>1196184</code></strong>等 <strong><code>1081492</code></strong>的SKU欄位 <strong><code>1898294</code></strong>。</p> </td>
  </tr>
  <tr>
    <td><p>單一SKU，位於URL路徑中。</p> </td>
    <td><p>記錄的Quickview URL包括：</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>變數部分位於路徑的最後一部分，並成為熱點的SKU值： <strong><code>6422350843</code></strong>, <strong><code>1607745002</code></strong>, <strong><code>0086724882</code></strong>。</p> </td>
  </tr>
  <tr>
    <td><p>查詢字串中的SKU和類別ID。</p> </td>
    <td><p>記錄的Quickview URL包括：</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>在此例中，URL中有兩個不同的部分。 SKU會儲存在參數 <code>prodId</code> 中，類別ID會儲存在<code></code> 參數 <code>category=</code> 中。</p> <p>因此，熱點定義是對。 亦即SKU值和稱為的其他變數 <code>categoryId</code>。 產生的對如下：</p>
    <ul>
      <li><p>SKU是 <strong><code>305466</code></strong> 且 <code>categoryId</code> 是 <code>1100004</code>。</p> </li>
      <li><p>SKU是 <strong><code>310181</code></strong> 且 <code>categoryId</code> 是 <strong><code>1100004</code></strong>。</p> </li>
      <li><p>SKU是 <strong><code>308706</code></strong> 且 <code>categoryId</code> 是 <strong><code>1740148</code></strong>。</p> </li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**範例**

您可以將上述三個範例中使用的相同方法套用至示範網頁：

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html)

示範網頁包含數個產品縮圖，每個產品縮圖都有標有「檢視更多」的Quickview按鈕。 在您的網頁瀏覽器除錯工具仍處於啟用狀態時，按一下每個按鈕並記下錄制的Quickview URL。 在您啟動頁面上所有4種可用的Quickview產品後，您會有下列Quickview要求清單給後端：

* `/datafeed/Men-Windbreaker.json`
* `/datafeed/Men-SimpleHenley.json`
* `/datafeed/Men-CamoPullover.json`
* `/datafeed/Women-QuiltedDownJacket.json`

檢視這些伺服器呼叫，您會發現產品特定資訊只存在於請求路徑中。 您也注意到查詢字串完全未使用，並且涉及兩種不同的資料片段類型：

* 第一種是「男」或「女」。 您可以將此稱為「產品類別」。
* 第二種類型是產品名稱，例如CamoPullover。 您可以假設這是產品SKU。

根據此資訊，整個Quickview URL具有以下模式：

`/datafeed/$categoryId$-$SKU$.json`

基於此類分析，您將使用和 `categoryId` 用於 `SKU` 熱點。

您現在可以使用AEM Assets中可購買的互動式影像功能，上傳影像橫幅並新增熱點。

## （可選）建立互動式影像檢視器預設集 {#optional-creating-an-interactive-image-viewer-preset}

您可以選擇使用AEM Assets隨附的預設、立即可用的互動式影像檢視器 `Shoppable_Banner` 預設集。 或者，您也可以建立您自己的自訂檢視器預設集，以便用於互動式影像。

當您建立自訂的互動式影像檢視器預設集時，可以決定影像橫幅上熱點的外觀。 在建立檢視器預設集時，您可以選擇使用預先定義影像收藏館中的熱點圖形。

儲存檢視器預設集後，就會在AEM Assets的「檢視器預設集」清單頁面上自動啟動（開啟）它。 此功能表示它可在互動式媒體元件中顯示，且在您檢視資產時也可顯示。 不過，若要*傳送*具有此檢視器預設集的互動式橫幅，您也必須*發佈*您的檢視器預設集（自訂或現成可用的檢視器預設集）。

**若要建立互動式影像檢視器預設集**

1. 在左側導軌中，點選「工 **[!UICONTROL 具>資產>檢視器預設集」]**。
1. 在頁面的右上角附近，點選「建 **[!UICONTROL 立」]**。
1. 在「新建檢視器預設集」對話方塊中，輸入名稱以說明互動式橫幅檢視器預設集。

   這是在您儲存後，將會出現在「檢視器預設集」清單頁面中的標題。

1. 在「豐富型媒體類型」下拉式功能表中，選取「互動 **[!UICONTROL 式影像」]**。
1. 點選「 **[!UICONTROL 建立]**」。
1. 在「編輯檢視器預設集」頁面上，點選「外 **[!UICONTROL 觀]** 」標籤。
1. 執行下列任一項作業：

   * 若要上傳您要用於影像的自己熱點影像，請點選「資產選擇器」圖示。 在「選擇內容」頁面中，導覽至您要使用的熱點影像，選取它，然後點選右上角的「勾選標籤」圖示。
   * 若要選取預先定義的熱點影像，請點選「熱點圖庫」圖示。 在熱點圖庫調色板上，點選要使用的熱點影像。

1. 在頁面的右上角附近，點選「儲存 **[!UICONTROL 」]**。

   請確定您已發佈新的檢視器預設集。

   請參 [閱已新增的Publishing Viewer預設集](/help/assets/managing-viewer-presets.md#publishing-viewer-presets)。

   您現在已準備好上傳影像橫幅。

## 上傳影像橫幅 {#uploading-an-image-banner}

如果您已上傳您要使用的影像，請進入下一個步驟「新增熱點至影 [像橫幅」](#adding-hotspots-to-an-image-banner)。

**若要上傳影像橫幅**

1. 上傳您要製作互動式影像橫幅。

   請參閱 [上傳資產](/help/assets/managing-assets-touch-ui.md#uploading-assets)。

   您現在可以在影像橫幅中加入熱點；請參閱下面的下一項工作。

## 向影像橫幅添加熱點 {#adding-hotspots-to-an-image-banner}

您可以使用「熱點管理」頁上的編輯器將熱點添加到影像橫幅。

添加熱點時，可以將其定義為Quickview彈出式顯示、超連結或體驗片段。

請參閱 [體驗片段](/help/sites-authoring/experience-fragments.md)。

>[!NOTE]
>
>請注意，當您將檢視器內嵌在「體驗片段」時，不支援「互動式影像」中的社交媒體分享工具。若要解決這個問題，您可以使用或建立沒有社交媒體分享工具的檢視器預設集。 這些檢視器預設集可讓您成功將它內嵌在「體驗片段」中。

在目前的建立／編輯作業階段中，支援在頁面右上角的「復原」和「重做」選項。

當您完成互動影像的建立後，您可以使用「預覽」來呈現您的互動影像對客戶的呈現方式。

請參 [閱（選用）預覽互動影像](#optional-previewing-interactive-images)。

>[!NOTE]
>
>在「互動式影像」或「轉盤橫幅」中新增熱點至影像時，熱點資訊會儲存在相對於影像位置的相同中繼資料位置，不論是「互動式影像」或「轉盤橫幅」。 這項功能表示，您可以在任一檢視器中，輕鬆地重複使用相同的影像及其定義的熱點資料。

>但是，請注意，轉盤橫幅支援影像上的影像地圖，這些影像也可能包含熱點；互動式影像則否。 如果您想要建立使用相同影像的互動式影像或轉盤橫幅，請記住這一點。 您可能想要使用相同影像的個別副本來建立互動式影像和轉盤橫幅。
>
>另請參閱 [轉盤橫幅](/help/assets/carousel-banners.md)。

>[!NOTE]
>
>如果您正在編輯具有熱點的互動式影像並裁剪影像，則會刪除熱點。

**向影像橫幅添加熱點**

1. 在「資產」檢視中，導覽至您要建立互動功能的影像橫幅。
1. 執行下列任一項作業：

   * 將滑鼠暫留在影像上，然後點選「 **[!UICONTROL 選取]** （勾選圖示）」。 在工具列上，點選「 **[!UICONTROL 編輯」]**。

   * 將滑鼠指標暫留在影像上，然 **[!UICONTROL 後點選「更多動作]** 」（三個點圖示） **[!UICONTROL >「編輯」]**。

   * 點選影像以在「詳細資料檢視」頁面中開啟影像。 在工具列上，點選「 **[!UICONTROL 編輯」]**。

1. 在頁面的左上角附近，點選「新增熱點」( **[!UICONTROL 手指點選圖示]** )以開啟「熱點」管理頁面。
1. 在頁面的左上角附近，點選「熱 **[!UICONTROL 點」]**。

1. 在「熱點管理」頁面的左上角附近，點選「熱 **[!UICONTROL 點」]**。
1. 在影像上，點選您要熱點出現的位置。 如有必要，請拖動熱點以調整其位置。
1. 通過重複步驟a和b，根據需要添加其他熱點。
1. （可選）若要刪除熱點，請在影像上選取它，然後點選「熱點」標題下 **[!UICONTROL 的]** 「刪除」(廢棄項目可 **[!UICONTROL 以圖示)]** 。

1. 在「名稱」文本欄位中，鍵入熱點的名稱。 此名稱也會出現在「選定熱點」下拉清單中。
1. 執行下列任一項作業：

   * 點選 **[!UICONTROL Quickview]**。

      * 如果您是AEM Sites或電子商務客戶，請點選或按一下「產品選擇器」圖示（放大鏡）以開啟「選擇產品」頁面。 點選或按一下您要使用的產品，然後點選頁面右上角的**選擇**以返回熱點管理頁面。
      * 如果您不 *是* AEM Sites或電子商務客戶

         * 請參閱 [識別熱點變數](#optional-identifying-hotspot-variables);您需要定義這些變數。
         * 然後，手動輸入SKU值。 在「SKU值」文字欄位中，輸入產品的SKU（庫存保留單位），此為您提供之每個不同產品或服務的唯一識別碼。 輸入的SKU值會自動填入Quickview範本的變數部分，讓系統知道將點選的熱點與特定SKU的Quickview關聯。
         * （可選）如果Quickview中有其他變數需要用來進一步識別產品，請點選「新增一般變 **[!UICONTROL 數」]**。 在文字欄位中，指定其他變數。 例如， `category=Mens` 是新增的變數。
   * 點選「 **[!UICONTROL 超連結]**」。

      * 如果您是AEM Sites客戶，請點選或按一下「網站選擇器」圖示（資料夾）以導覽至URL。 請注意，如果您的互動式內容具有相對URL的連結，尤其是AEM Sites頁面的連結，就無法使用以URL為基礎的連結方法。
      * 如果您是獨立客戶，請在HREF文字欄位中，指定連結網頁的完整URL路徑。
   請確定您要指定是在新的瀏覽器標籤（建議預設值）或相同的標籤中開啟連結。

   如需詳 [細資訊，請參閱使用選](/help/assets/working-with-selectors.md) 擇器。

   * 點選 **[!UICONTROL 體驗片段]**。

      * 如果您是AEM Sites客戶，請點選或按一下「搜尋」圖示（放大鏡）以開啟「體驗片段」頁面。 點選或按一下您要使用的體驗片段，然後點選頁面右上角的「選取」以返回熱點管理頁面。
請參閱 [體驗片段](/help/sites-authoring/experience-fragments.md)。

      * 指定「體驗片段」在橫幅上顯示的寬度和高度。

         >[!NOTE]
         >
         >請注意，當您將檢視器內嵌在「體驗片段」時，不支援「互動式影像」中的社交媒體分享工具。若要解決這個問題，您可以使用或建立沒有社交媒體分享工具的檢視器預設集。 這些檢視器預設集可讓您成功將它內嵌在「體驗片段」中。



1. 點選 **[!UICONTROL 「儲存]** 」以儲存您的工作並返回「瀏覽頁」。
1. 發佈互動式影像。 發佈可讓橫幅透過雲端傳送，而且如果您需要與協力廠商網站整合，也可產生內嵌代碼。

   請參閱 [發佈資產](/help/assets/managing-assets-touch-ui.md#publishing-assets)。

   新增熱點並發佈互動式影像後，您現在可以將它新增至現有的網站。

   請參 [閱整合互動式影像與您的網站](#integrating-an-interactive-image-with-your-website)。

   >[!NOTE]
   >
   >如果您正在編輯具有熱點的互動式影像並裁切影像，則會刪除熱點。

### （選擇性）預覽互動式影像 {#optional-previewing-interactive-images}

您可以使用「預覽」來查看您的互動式影像對客戶的呈現效果，並測試影像的熱點，以確保它們如預期般運作。

當您對互動式影像感到滿意時，就可以發佈它。
請參 [閱將視訊或影像檢視器內嵌在網頁上](/help/assets/embed-code.md)。
請參 [閱連結URL至您的Web應用程式](/help/assets/linking-urls-to-yourwebapplication.md)。 請注意，如果您的互動式內容具有相對URL的連結，尤其是AEM Sites頁面的連結，就無法使用以URL為基礎的連結方法。
請參閱 [新增動態媒體資產至頁面。](/help/assets/adding-dynamic-media-assets-to-pages.md)

**若要預覽互動式影像**

1. 在「資產」檢視中，導覽至您已建立的現有互動影像，然後點選以在「預覽」中開啟它。
1. 在「預覽」頁面的左上角附近，在「內容」下拉式清單中，點選「檢視 **[!UICONTROL 器」]**。
1. 在「檢視器」清單中，點選 **[!UICONTROL Shopbable_Banner]** ，或您所建立的互動式影像檢視器預設集的名稱。
1. 點選影像上的熱點，以測試其相關動作。

## 發佈互動式影像資產 {#publishing-interactive-image-assets}

如需如 [何發佈互動式影像資產](/help/assets/publishing-dynamicmedia-assets.md) ，請參閱發佈資產。

## 將互動式影像與您的網站整合 {#integrating-an-interactive-image-with-your-website}

在您上傳橫幅影像、新增影像熱點並發佈互動式影像後，您現在可以將它新增至網站頁面。

如果您是AEM Sites客戶，可將互動式媒體元件拖曳至您的頁面，以新增互動式影像。 請參閱 [新增動態媒體資產至頁面。](/help/assets/adding-dynamic-media-assets-to-pages.md)

如果您是獨立的AEM Assets客戶，您可以依本節所述手動將互動式影像新增至您的網站。

1. 複製已發佈的互動式影像的內嵌程式碼。
請參 [閱將視訊或影像檢視器內嵌在網頁上](/help/assets/embed-code.md)。

1. 將複製的內嵌程式碼新增至網頁中所需的位置。
複製的內嵌程式碼會設定為回應式環境，因此應自動符合指定的區域。

**範例**

以示範網站為例：

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html)

請注意，這三個人的照片是一個靜態標 `IMG` 簽：

```xml
<img class="img-responsive" width="100%" title="Hero Image 2" alt="Hero Image 2" src="images/shoppable-banner.jpg">
```

整合就像從AEM Assets移除標 `IMG` 簽並以複製的內嵌代碼取代標籤一樣簡單。 您可在下列URL中看到結果，其中顯示具有三個社交熱點的頁面上的可購物互動影像：

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-1.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-1.html)

>[!NOTE]
>
>因此，演示網站上可購物交互影像上的熱點僅用於顯示；它們尚未與現有的Quickviews整合。

若要針對回應式環境將「裁切」套用至可購買的互動式影像，您可將「互動式影像」組態屬性加入路徑——其中是要呼叫的元件， `ZoomView.iscommand``ZoomView``iscommand` 是您套用的「裁切」影像伺服命令。

請參 [閱ZoomView.iscommand配置](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/r_html5_aem_interactive_image_config_attrib_zoomview_iscommand.html) 屬性。

請參 [閱裁切](https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/http_ref/r_crop.html) 影像伺服命令。

您現在已準備好將互動式影像與網站上現有的Quickview整合。

## 將互動式影像與現有的Quickview整合 {#integrating-an-interactive-image-with-an-existing-quickview}

>[!NOTE]
>
>此工作僅在您是獨立AEM Assets客戶時適用。

此程式的最後一個步驟是將互動式影像與網站上現有的Quickview實作整合。 沒有適合所有情況的整合解決方案。 每個Quickview實施都是獨一無二的，需要一種最可能需要前端IT人員幫助的具體方法。

現有的Quickview實施通常表示網頁上發生的一系列相互關聯的操作，其順序如下：

1. 使用者會在您網站的使用者介面中觸發元素。
1. 前端代碼根據在步驟1中觸發的用戶介面元素獲取Quickview URL。
1. 前端程式碼會使用步驟2中取得的URL來傳送Ajax要求。
1. 後端邏輯會將對應的Quickview資料或內容傳回前端程式碼。
1. 前端代碼載入Quickview資料或內容。
1. 或者，前端代碼將載入的Quickview資料轉換為HTML表示法。
1. 前端程式碼會顯示模式對話方塊或面板，並轉譯HTML內容給使用者。

這些呼叫可能不代表獨立的公用API呼叫，而網頁邏輯可透過任意步驟呼叫這些呼叫。 相反地，它是連結呼叫，在此連結呼叫中，前一個步驟的最後一個階段（回呼）中將隱藏下一個步驟。

在可購買互動影像取代步驟1和部分步驟2的同時，當使用者按一下可購買影像中的熱點時，檢視者會處理此類使用者互動。 檢視器會將事件傳回至網頁，其中包含先前新增至AEM Assets的所有熱點資料。

在此類事件處理常式中，前端程式碼會執行下列動作：

* 監聽由可購買互動影像發出的事件。
* 根據熱點資料構建Quickview URL。
* 觸發從後端載入Quickview並在螢幕上顯示的程式。

AEM Assets傳回的內嵌代碼已經有可供使用的事件處理常式，已加上註解，如下列反白顯示的程式碼片段所示：

```xml
        var s7interactiveimageviewer = new s7viewers.InteractiveImage({
            "containerId" : "s7interactiveimage_div",
            "params" : {
                "serverurl" : "https://aodmarketingna.assetsadobe.com/is/image",
                "contenturl" : "https://aodmarketingna.assetsadobe.com/",
                "config" : "/etc/dam/presets/viewer/Shoppable_Media",
                "asset" : "/content/dam/mac/aodmarketingna/shoppable-banner/shoppable-banner.jpg" }
        })
        /* // Example of interactive image event for Quickview.
             s7interactiveimageviewer.setHandlers({
                "quickViewActivate": function(inData) {
                    var sku=inData.sku; //SKU for product ID
                    //To pass other parameter from the hotspot, you will need to add custom parameter during the hotspot setup as parameterName=value
                    loadQuickView(sku); //Replace this call with your Quickview plugin
                    //Please refer to your Quickviewer plugin for the Quickview call
                 },
             });
        */
        s7interactiveimageviewer.init();
```

因此，只需取消程式碼的註解，並以特定網頁專用的程式碼取代虛擬處理常式主體即可。

建立Quickview URL的程式與用來識別先前涵蓋的熱點變數的程式基本相反。

請參 [閱識別熱點變數](#optional-identifying-hotspot-variables)。

使用我們先前的Quickview URL示例，您可以在以下示例中查看每種情況下如何構建Quickview URL:

<table>
 <tbody>
  <tr>
   <td><p>單一SKU，可在查詢字串中找到</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;amp;source=100";
      },
      });</code></td>
  </tr>
  <tr>
   <td><p>單一SKU，位於URL路徑中</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/product/" + inData.sku;
      },
      });</code></td>
  </tr>
  <tr>
   <td><p>查詢字串中的SKU和類別ID</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;amp;prodId=" + inData.sku;
      },
      });</code></td>
  </tr>
 </tbody>
</table>

觸發Quickview URL並啟動Quickview面板的最後一個步驟很可能需要您IT部門的前端IT人員協助。 他們具備最佳的知識，可瞭解如何從正確的步驟準確觸發Quickview實施，並擁有現成可用的Quickview URL。

您可以瞭解這些步驟如何套用至示範網站，以便將可購買的互動式影像與Quickview程式碼完全整合。 之前，Quickview URL的結構已識別為：

```xml
/datafeed/$categoryId$-$SKU$.json
```

若要在處理常式中重 `quickViewActivate` 新建構此URL，您可以使用 `categoryId``SKU` 物件中可用的和欄位，該物件會由檢視器的程式碼傳遞 `inData` 至處理常式：

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

示範網站會使用簡單函式呼叫來觸發「快速檢視」 `loadQuickView()` 對話方塊。 此函式只使用一個引數，即Quickview資料URL。 因此，整合可購買互動影像的最後一個步驟，就是將下列程式碼行新增至處理 `quickViewActivate` 常式：

```xml
loadQuickView(quickViewUrl);
```

以下是完整的原始碼：

```xml
 var s7interactiveimageviewer = new s7viewers.InteractiveImage({
  "containerId" : "s7interactiveimage_div",
  "params" : {
   "serverurl" : "https://aodmarketingna.assetsadobe.com/is/image",
   "contenturl" : "https://aodmarketingna.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Media",
   "asset" : "/content/dam/mac/aodmarketingna/shoppable-banner/shoppable-banner.jpg" }
 })
   s7interactiveimageviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku;
     var categoryId=inData.categoryId;
    var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
    loadQuickView(quickViewUrl);
    },
   });
 s7interactiveimageviewer.init();
```

完整整合互動影像的最終示範網站如下所示：

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-3.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-3.html)

## 使用Quickviews建立自訂快顯視窗 {#using-quickviews-to-create-custom-pop-ups}

請參 [閱使用快速檢視建立自訂快顯視窗](/help/assets/custom-pop-ups.md)。
