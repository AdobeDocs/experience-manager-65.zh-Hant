---
title: 互動式影片
description: 瞭解如何在動態媒體中處理互動式視訊和可購買視訊
uuid: c3ff6839-fff5-4709-8163-5c4245b80e6d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 04be55f2-c7d8-45ef-89e5-58856b971de5
docset: aem65
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# 互動式影片{#interactive-videos}

您可以輕鬆製作互動式視訊（也稱為可購買的視訊），直接從視訊推動轉換。 客戶與視訊的互動會與視訊播放器一起在面板中進行，視訊播放器會根據視訊中的功能捲動相關服務、資訊或產品縮圖。 客戶可以點選縮圖並直接連結至服務，或將項目新增至購物車以立即購買，或連結至網頁以取得詳細資訊。

當視訊結束時，會顯示所有方案的視覺化摘要，以推動行動要求。 客戶有另一個機會來點選他們想要的項目。 可操作且具體的體驗，例如這些可提升客戶參與度和轉化率。

另請參閱 [互動式影像](/help/assets/interactive-images.md)。

## 互動式視訊的實際運作 {#interactive-video-in-action}

若要檢視互動式可購物視訊的實際運作，請按一下「 [Live Demos](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html)」（即時展示），捲動至頁面上的 **[!UICONTROL Shopbable Media]** 標題，然後按一下可購物視訊。

* 在播放期間，當視訊中使用產品時，相同的產品會以縮圖影像的形式出現在右側。

* 按一下縮圖以暫停影片並開啟產品的快速檢視。 例如，按一下影片中的KitchenAid縮圖影像，即可體驗混音器的360度旋轉檢視，或放大以檢視混音器詳細資訊。

<!-- There was a link here that showed the video frame of an interactive video and when the reader clicked the frame the video would play https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/AXIS/index.html. This now needs to call a new interactive video-->

![互動式可購物視訊的影格](assets/chlimage_1-126.png)*從互動式可購物視訊擷取視訊影格。*

>[!NOTE]
>
>如果您建立互動式視訊，以在使用者按一下縮圖影像時啟動網頁，有些裝置會封鎖快顯網頁。 在這種情況下，您必須變更裝置上的快顯封鎖程式設定。 例如，在Apple iPhone 6上，點選 **[!UICONTROL設定** > **Safari** > **Block快顯視窗**，然後將控制項滑入 ****[!UICONTROL Off. 現在，當您播放互動式視訊並按一下縮圖時，如果您要開啟快顯視窗，就會出現提示。 如果您接受，則會開啟網頁。

### 觀看互動式影片的製作方式 {#watch-how-interactive-videos-are-created}

觀看如何建立互動式視訊的7分 [鐘30秒逐步解說](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&emailurl=https://s7d5.scene7.com/s7/emailFriend&serverUrl=https://s7d5.scene7.com/is/image/&config=Scene7SharedAssets/Universal_HTML5_Video_social&contenturl=https://s7d5.scene7.com/skins/&asset=S7tutorials/InteractiveVideo)[](https://outv.omniture.com?v=s4NHQ2dzqd7hIqWjeG2sIdyNWsTWyupA)。
（雖然視訊逐步說明已加上「隨選資產」品牌，但AEM Assets中的「互動式視訊」仍適用原則和步驟。）

### Adobe客戶成功網路研討會 {#adobe-customer-success-webinar}

「在AEM Assets中使用互動式視訊、連結分享和YouTube分享」網路研討會教您如何使用互動式視訊和其他功能，將轉換導向的活動連結至您的視訊行銷內容。

>[!NOTE]
[在AEM Assets中使用互動式視訊、連結分享和YouTube分享](https://adobecustomersuccess.adobeconnect.com/p1yxzdo4aec/)。

## 快速入門：互動式影片 {#quick-start-interactive-videos}

下列逐步工作流程說明旨在協助您在動態媒體中快速上手使用互動式視訊。

在某些「快 **速啟動** 」任務中查找「示例」標題。 它包含一個簡短的教學課程，以此開始的示範網頁為基礎， *尚未加* 入互動功能：

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html)

範例 **可協助您說明** ，如何將互動式視訊整合在您自己的網站上。

當您在最後一個範例區段中完成教學課程時，完整整合互動式影片的最終示範網頁如下所示：

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-3.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-3.html)

互動式視訊步驟：

1. **（可選）識別Quickview變數** -首先，確定現有Quickview實施所使用的動態變數。 當您建立互動式視訊時，可使用變數將產品縮圖對應至其對應的產品Quickview。 請參 [閱（可選）識別Quickview變數](#optional-identifying-quickview-variables)。
   *請注意，只有在以下所有步驟都正確時，才需要此步驟*:·您想要透過觸發快速檢視，為視訊新增互動功能。
·您的AEM實作不會使 *用* eCommerce整合架構，將產品資料從任何電子商務解決方案（例如IBM Websphere Commerce、Elastic Path、hybris或Intershop）拉入AEM。 請參 [閱AEM Assets中的電子商務概念](/help/sites-administering/concepts.md)。

1. **（可選）建立互動式視訊檢視器預設集** -自訂各種元件的外觀和行為，這些元件是播放器的組成元件，例如視訊筆畫和互動式縮圖。
如果您想要使用現成可用的互動式視訊檢視器預設集，或改用現成可用的互動式視訊檢視器預設集，則不需要建立您自己的互動式視 `Shoppable_Video_Light` 訊檢視 `Shoppable_Video_Dark` 器預設集。
請參 [閱建立新檢視器預設集](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset) （此為選用）和建 [立互動檢視器預設集的特殊考量事項](/help/assets/managing-viewer-presets.md#special-considerations-for-creating-an-interactive-viewer-preset)。

1. **上傳視訊及其相關影像資產** -上傳您要製作互動內容的視訊和相關影像。
請參 [閱上傳視訊及其相關的縮圖資產](#uploading-a-video-and-its-associated-thumbnail-assets)。

1. **在視訊中新增互動功能** -在視訊中新增一或多個時間區段。 然後，在這些時間區段內建立影像縮圖的關聯。 將每個影像縮圖指派給動作，例如超連結、Quickview或體驗片段。
（請注意，如果您的互動式內容具有相對URL的連結，尤其是AEM Sites頁面的連結，則無法使用以URL為基礎的連結方法。）發佈互動式視訊資產以完成。 發佈會建立內嵌程式碼或URL，您最終會將其複製並套用至網站登陸頁面。請參閱 [新增視訊互動功能](#adding-interactivity-to-your-video)。
請參閱 [發佈資產](/help/assets/publishing-dynamicmedia-assets.md)。

1. **在AEM中將互動式視訊新增至您的網站或網站**：如果您使用AEM Sites、AEM eCommerce或兩者，您可將互動式視訊直接拖曳至AEM的網頁，即可將互動式視訊新增至AEM中的網頁。 請參閱 [新增動態媒體資產至頁面。](/help/assets/adding-dynamic-media-assets-to-pages.md)
使用內嵌程式碼或URL，將您的互動式視訊與網站體驗整合。 請參 [閱整合互動式視訊與您的網站](#integrating-an-interactive-video-with-your-website)。
如果您使用協力廠商WCM(Web Content Manager)，您必須將新的互動式視訊與網站上使用的現有Quickview實作整合。 請參 [閱整合互動式視訊與現有的Quickview](#integrating-an-interactive-video-with-an-existing-quickview)。
   [](/help/assets/adding-dynamic-media-assets-to-pages.md)

## （可選）識別Quickview變數 {#optional-identifying-quickview-variables}

>[!NOTE]
只有在以下情況下，才需要此任務：
* 您想要透過觸發至Quickviews，將互動功能加入視訊中。
* 您的AEM實作不會使 *用* eCommerce整合架構，將產品資料從任何電子商務解決方案（例如IBM Websphere Commerce、Elastic Path、hybris或Intershop）拉入AEM。 請參 [閱AEM Assets中的電子商務概念](/help/sites-administering/concepts.md)。

如果您的AEM實作使用電子商務，您可以略過此工作並繼續下一個工作。

首先，您可以識別現有Quickview實作所使用的動態變數，以便在互動式視訊建立程式中，將產品縮圖對應至其對應的產品Quickview。

在視訊中新增時間區段時，您會指派SKU和任何其他變數至您新增至區段的每個縮圖。 這些變數稍後會用來顯示正確的Quickview產品。

請務必正確識別唯一觸發產品Quickview所需的變數。

有時，與負責您現有Quickview實施的IT專家協商可能已足夠。 他們可能知道在系統中標識Quickview所需的最小資料集。 不過，在大多數情況下，您也可以只分析前端程式碼的現有行為。

Quickview的大多數實施都採用以下模式：

* 使用者在網站上啟動使用者介面元素。 例如，按一下「快速視圖」按鈕。
* 如有需要，網站會傳送Ajax要求至後端以載入Quickview資料或內容。
* Quickview資料會轉譯為內容，以準備在網頁上轉譯。
* 最後，前端程式碼會以視覺化方式在螢幕上呈現此類內容。

因此，方法是瀏覽您現有網站上實作Quickview的不同區域、觸發Quickview並擷取網頁所傳送的Ajax URL，以載入Quickview資料或內容。

通常您不需使用任何專用的除錯工具。 現代網頁瀏覽器採用Web檢視器，可讓您完成適當的工作。 以下是包含Web檢視程式的Web瀏覽器範例：

* 若要在Google Chrome中查看所有傳出的HTTP要求，請按 **F12** (Windows)或 **Command+Options+I** (Mac)以開啟「開發人員工具」面板，然後按一下「網 **路** 」標籤。

* 在Firefox中，您可以按 **F12** (Windows)或 **Command+Option+I** (Mac)並使用其 **Net** )標籤來啟動Firebug外掛程式，或使用內建的偵測器工具及其網路標籤。

* 在Internet explorer中，按 **F12啟動除錯工具**。

在瀏覽器中開啟網路監視時，觸發頁面上的Quickview。

現在，在網路記錄檔中尋找Quickview Ajax URL，並複製已記錄的URL以供日後分析。 在大多數情況下，當您觸發Quickview時，會有許多請求被發送到伺服器。 通常，Quickview Ajax URL是清單中第一個URL。 它有複雜的查詢字串部分或路徑，其回應MIME類型為 `text/html`、 `text/xml`或 `text/javascript`。

在此程式中，請務必造訪您網站的不同區域，以及不同的產品類別和類型。 原因是Quickview URL可能有特定網站類別的常用部分，但只有在您造訪網站的不同區域時才會變更。

在最簡單的情況下，Quickview URL中唯一的變數部分是產品SKU。 在這種情況下，產品SKU值是在AEM中將縮圖新增至互動式視訊中的時間區段時，唯一需要的資料片段。

但是，在複雜情況下，Quickview URL除了產品SKU以外，還有不同的元素，例如類別ID、顏色代碼等。 在這種情況下，每個此類元素都會變成AEM中縮圖資料定義中的個別變數。

請考慮下列Quickview URL及其產生的縮圖變數範例：

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
    </ul> <p>URL中唯一的變數部分是查詢字串參 <code>productId=</code> 數的值，而它顯然是SKU值。 因此，我們的縮圖只需要填入值如、、 <strong><code>866558</code></strong>、 <strong><code>1196184</code></strong>、 <strong><code>1081492</code></strong>等的SKU欄位 <strong><code>1898294</code></strong>。</p> </td>
  </tr>
  <tr>
    <td><p>單一SKU，位於URL路徑中。</p> </td>
    <td><p>記錄的Quickview URL包括：</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>變數部分位於路徑的最後一部分，它會變成AEM縮圖的SKU值： <strong><code>6422350843</code></strong>, <strong><code>1607745002</code></strong>, <strong><code>0086724882</code></strong>。</p> </td>
  </tr>
  <tr>
    <td><p>查詢字串中的SKU和類別ID。</p> </td>
    <td><p>記錄的Quickview URL包括：</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>在此例中，URL中有兩個不同的部分。 SKU會儲存在參數 <code>prodId</code> 中，類別ID會儲存在參 <code>category=</code> 數中。</p> <p>因此，縮圖定義是成對的。 亦即SKU值和稱為的其他變數 <code>categoryId</code>。 產生的對如下：</p>
    <ul>
      <li>SKU是 <code>305466</code> 且 <code>categoryId</code> 是 <code>1100004</code></li>
      <li>SKU是 <code>310181</code> 且 <code>categoryId</code> 是 <code>1100004</code></li>
      <li>SKU是 <code>308706</code> 且 <code>categoryId</code> 是 <code>1740148</code></li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**範例**

將上述方法套用至我們的範例網站時，我們有一個含有許多產品縮圖的網頁，每個網頁都有「SEE MORE」（查看更多）按鈕：

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html)

在啟動頁面上所有可用的產品Quickview後，您將獲得向後端發出的Quickview請求的以下清單：

* datafeed/candles-233396346.json
* datafeed/candles-233978050.json
* datafeed/candles-234024346.json
* datafeed/candles-234024356.json
* datafeed/candles-234024359.json
* datafeed/cushions-233939848.json
* datafeed/cushions-234019477.json
* datafeed/cushions-234019483.json
* datafeed/furniture-231747479.json
* datafeed/furniture-232625621.json
* datafeed/furniture-232625626.json
* datafeed/furniture-233939810.json
* datafeed/furniture-233939825.json
* datafeed/furniture-233939828.json
* datafeed/furniture-233939853.json
* datafeed/furniture-233940334.json
* datafeed/glassware-000064007.json
* datafeed/glassware-230722193.json
* datafeed/glassware-233916550.json
* datafeed/glassware-233916597.json

檢視這些伺服器呼叫，您會發現產品特定資訊只存在於請求路徑中。 您也會注意到查詢字串完全未使用，並且涉及兩種不同的資料片段類型：

* 第一種是蠟燭，墊子，家具，玻璃器皿。 您可以將此稱為「產品類別」。
* 第二種類型是產品代碼，例如233916597。 您可以假設它是「產品SKU」。

根據此資訊，整個Quickview URL具有以下模式：

`/datafeed/$categoryId$-$SKU$.json`

根據此類分析，您可得出以下兩個變數用於縮圖： `categoryId` 和 `SKU`。

您現在可以上傳視訊及其相關的縮圖資產。

## （可選）建立互動式視訊檢視器預設集 {#optional-creating-an-interactive-video-viewer-preset}

如果您要使用預設、現成可用的互動式視訊檢視器預設集類型或，可以略過此工作並繼續下 `Shoppable_Video_dark` 一步 `Shoppable_Video_light`。

在製作環境中按一下縮圖時，會出現「快速檢視」對話方塊的預覽。

![chlimage_1-21](assets/chlimage_1-127.png)

您可以選擇建立自訂的互動式視訊檢視器預設集。 您可決定視訊播放器的樣式、互動式縮圖和視訊結尾的縮圖格線檢視。

互動式視訊檢視器預設集會正確呈現您新增的視訊和所有時間軸區段。 當您在「預覽」模式中按一下產品縮圖時，也會使用預設的Quickview範例，讓您在發佈前先測試其互動性。

儲存檢視器預設集後，其狀態會在「檢視器預設集」頁面中自動設為**On **。 此狀態表示在動態媒體元件中及您使用它預覽視訊時，都可看到它。 請確定您也手動發佈新的檢視器預設集。

請參 [閱建立新檢視器預設集](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset) ，以建立您自己的互動式視訊檢視器預設集。

## 上傳視訊及其相關縮圖資產 {#uploading-a-video-and-its-associated-thumbnail-assets}

如果您已上傳視訊和縮圖資產，請繼續「新增 [視訊的互動功能」](#adding-interactivity-to-your-video)。

如果您上傳的視訊或影像不正確，或您想要刪除已上傳的視訊或影像，而您不再需要，請參閱刪 [除資產](/help/assets/managing-assets-touch-ui.md#deleting-assets)。

若要上傳視訊及其相關縮圖資產：

1. 將視訊和相關的縮圖資產上傳至您想要的檔案夾或檔案夾。

   請參閱 [上傳資產](/help/assets/managing-assets-touch-ui.md)。
請參 [閱使用FTP工作排程上傳資產](/help/assets/managing-assets-touch-ui.md)。

   現在，為您的視訊加入互動功能。

## 為視訊新增互動功能 {#adding-interactivity-to-your-video}

您可使用「建立互動式視訊」頁面上的就地視覺編輯器，將時間軸區段新增至視訊。

新增時間軸區段後，您會在每個區段中新增縮圖影像。 針對您新增的每個縮圖，您都會套用動作。 例如，您可以將Quickview套用至縮圖，或指派超連結給縮圖，或是體驗片段。

請參閱 [體驗片段](/help/sites-authoring/experience-fragments.md)。

>[!NOTE]
請注意，當您將檢視器內嵌在「體驗片段」時，不支援「互動式視訊」中的社交媒體分享工具。若要解決這個問題，您可以使用或建立沒有社交媒體分享工具的檢視器預設集。 這些檢視器預設集可讓您成功將它內嵌在「體驗片段」中。

>[!NOTE]
如果您的互動式內容具有相對URL的連結，尤其是AEM Sites頁面的連結，則無法使用以URL為基礎的連結方法。

在目前的建立／編輯作業階段中，支援在頁面右上角的「復原」和「重做」選項。

儲存互動式視訊後，視訊會立即開啟至「預覽」。 您可以從中選取互動式視訊檢視器預設集，並播放視訊，以大致呈現客戶的呈現方式。

若要將互動功能新增至影片：

1. 在「資產」檢視中，導覽至您上傳並想要製作互動式影片。
1. 執行下列任一項作業：

   * 將滑鼠暫留在影像上，然後點選「 **[!UICONTROL 選取]** （勾選圖示）」。 在工具列上，點選「 **[!UICONTROL 編輯」]**。

   * 將滑鼠指標暫留在影像上，然 **[!UICONTROL 後點選「更多動作]** 」（三個點圖示） **[!UICONTROL >「編輯」]**。

   * 點選影像以在「詳細資料檢視」頁面中開啟影像。 在工具列上，點選「 **[!UICONTROL 編輯」]**。

1. 在「建立互動式視訊」頁面上，執行下列任一項作業：

   * 點選「 **[!UICONTROL 播放]** 」按鈕開始播放影片。 當您要反白顯示的特定產品、服務或詳細資訊出現在檢視中時，點選工具列 **[!UICONTROL 上的「新增區段]** 」。 重複，直到您到達視訊結束為止。

      您可以針對您新增的每個時段，指派一或多張縮圖影像給它，然後將這些縮圖連結至Quickview產品頁面供客戶購買，或連結至網頁以取得詳細資訊。

   * 點選「 **[!UICONTROL 播放]** 」按鈕開始播放影片。 當您要反白顯示的特定產品、服務或詳細資訊進入檢視時，點選「暫 **[!UICONTROL 停」]**。 點選「 **[!UICONTROL 新增區段」]**。

      在您要新增區段的時間軸上，繼續播放和暫停視訊，直到視訊結束為止。

1. （可選）向左拖曳時間軸縮放滑桿上的橫條，以放大或向右縮小，借此控制您所新增區段的詳細程度。 ****

   ![chlimage_1-22](assets/chlimage_1-128.png)

   視視訊的長度而定，「區段持續時間」預設值如下：

   <table>
      <tbody>
        <tr>
        <td><strong>如果視訊長度是……</strong></td>
        <td><strong>「區段持續時間」設定預設為……</strong></td>
        </tr>
        <tr>
        <td>3分鐘以上</td>
        <td>60秒</td>
        </tr>
        <tr>
        <td>2-3分鐘</td>
        <td>30秒</td>
        </tr>
        <tr>
        <td>1-2 分鐘</td>
        <td>20 seconds<br /> </td>
        </tr>
        <tr>
        <td>30-60秒</td>
        <td>10秒</td>
        </tr>
        <tr>
        <td>30秒或更短</td>
        <td>5秒</td>
        </tr>
      </tbody>
    </table>

   視訊時間軸使用的螢幕空間和可用的空間一樣多。 因此，當您調整瀏覽器大小時，您新增的區段會維持其正確寬度。

   為了說明，以下三個螢幕擷取畫面使用相同的影片。 請注意，每個區段的寬度會依時間軸縮放設定而改變。

   ![chlimage_1-23](assets/chlimage_1-129.png)

   螢幕擷取A

   以上螢幕擷取A顯示29秒產品視訊的預設檢視。 時間軸比例預設為5秒。

   ![chlimage_1-130](assets/chlimage_1-130.png)

   螢幕擷取B

   在上述的螢幕擷取B中，「時間軸縮放」滑桿從預設的5秒拖曳至3秒。 請注意，個別時間軸縮放時間戳記現在都是以3秒間隔設定。

   ![chlimage_1-25](assets/chlimage_1-131.png)

   螢幕擷取C

   在上述的螢幕擷取C中，「時間軸縮放」設定已移至8秒。 請注意，包含產品縮圖的區段已縮小。 如果您有長視訊，而且想要看到通常符合頁面寬度的更多區段的概述，以這種方式縮小影片很有用。

1. （可選）執行下列任一項作業：

   * 調整區段的開始時間和結束時間。

      選取區段，然後分別拖曳前導或尾隨藍色橢圓以調整開始或結束時間。 顯示的視訊影格會根據您的調整，移至視訊中的適當時間。 時間軸段的移動基於時間軸中的任何相鄰段進行限制。 允許的最小區段時間為1秒。

      使用下列導覽捷徑，快速檢查並微調您的視訊區段：

      * 點選前導藍色橢圓，即可直接在該區段的開頭尋找視訊。
      * 點選結尾的藍色橢圓，即可直接在該區段的結尾處尋找視訊。
      * 點選整個區段，將視訊播放傳回至該區段的開頭
   ![chlimage_1-26](assets/chlimage_1-132.png)

   重新定位時間軸段的結尾

   * 若要刪除區段

      選取時間軸上的最後一個區段，然後在工具列上點選「刪 **[!UICONTROL 除區段」]**。 如果選取了兩或多個區段，「刪除區段」功能會停用。

      您只能刪除最後一個區段。 例如，如果您想要刪除時間軸上的所有區段，您必須一律選取最後一個區段，然後點選「刪 **[!UICONTROL 除區段」]**。


1. 選取您要關聯一或多個縮圖影像的時段。
1. 在視訊右側，點選「內容 **[!UICONTROL 」標籤]** 。
1. 在「內容」索引標籤下，點選「 **[!UICONTROL 選取資產]**」，然後瀏覽並選取您要用於影片的所有影像資產。 選取的資產會新增至「內容」索引標籤中的「資產選擇器」面板。

1. 在「內容」標籤下方的資產選擇器中，執行下列任一項作業：

   <table>
      <tbody>
        <tr>
        <td>將縮圖與所選時間軸段關聯</td>
        <td><p>在右側的資產選擇器面板中點選影像。</p> <p>您可以新增任意數量的縮圖至時間軸區段。 對於您選取的每個影像，資產選取器中的影像上會出現核取標籤。</p> </td>
        </tr>
        <tr>
        <td>要從所選時間軸段中刪除縮略圖，請執行以下操作：</td>
        <td><p>執行下列任一操作：</p>
          <ul>
          <li>在資產選擇器面板中，點選含有核取標籤的影像以取消選取它。 影像資產會從時間軸區段中移除。<br /> </li>
          <li>在選取的時間軸區段中，點選影像，然後在工具列上點選「刪 <strong>除產品」</strong>。</li>
          </ul> </td>
        </tr>
      </tbody>
    </table>

   ![資產選擇器](assets/chlimage_1-133.png)

   點選資產選取器面板中的影像會將其新增至選取的時間軸區段。

1. 在其中一個時間軸區段中選取單一縮圖影像，然後點選「動 **[!UICONTROL 作]** 」標籤。
1. 執行下列任一操作：
   <table> 
    <tbody> 
      <tr> 
      <td>將選定的縮圖影像與Quickview關聯</td> 
      <td><p>在「動作類型」下，點選「 <strong>Quickview」</strong>。</p> <p>如果您是AEM Sites和Ecommerce客戶：</p> 
       <ul> 
       <li>請注意，「SKU值」文字欄位已預先填入所選產品的SKU（庫存保留單位），此為您提供之每個不同產品或服務的唯一識別碼。 當影像與AEM Commerce中的產品相關聯時，會自動填入此項目。</li> 
       <li>如果預先填入的SKU不正確，請點選或按一下「產品選擇器」圖示（放大鏡）以開啟「選擇產品」頁面。 點選或按一下您要使用的產品，然後點選頁面右上角的核取標籤，以返回互動式視訊編輯器。</li> 
       </ul> <p> 如果您不 <em>是</em> AEM Sites或Ecommerce客戶</p> 
       <ul> 
       <li>請參 <a href="/help/assets/carousel-banners.md#identifying-hotspot-and-image-map-variables">閱識別熱點變數</a>。 您需要定義這些變數。 </li> 
       <li>依預設，此SKU欄位會使用影像資產的檔案名稱，但不含副檔名。 如果您根據SKU遵循檔案的標準命名慣例，則通常不需要進行任何其他編輯。 </li> 
       <li>否則，請編輯預設值並輸入正確的SKU值。 在「SKU值」文字欄位中，輸入產品的SKU（庫存保留單位），此為您提供之每個不同產品或服務的唯一識別碼。 輸入的SKU值會自動填入Quickview範本的變數部分，讓系統知道將點選的影像與特定SKU的Quickview建立關聯。</li> 
       </ul> <p>（可選）如果Quickview中有其他變數需要用來進一步識別產品，請點選「新增一般變 <strong>數」</strong>。 在文字欄位中，指定其他變數。 例如， <code>category=Womens</code> 是新增的變數。</p> <p> </p> </td> 
      </tr> 
      <tr> 
      <td>將選定的縮圖影像與超連結關聯</td> 
      <td><p>在「動作類型」下方，點選「 <strong>超連結</strong>」，然後執行下列其中一項作業：</p> 
       <ul> 
       <li>如果您是AEM Sites客戶，請點選「網站選擇器」圖示（資料夾）以導覽至網頁。 請注意，如果您的互動式內容具有相對URL的連結，尤其是AEM Sites頁面的連結，就無法使用以URL為基礎的連結方法。</li> 
       <li>如果您是獨立的Dynamic media客戶，請在HREF文字欄位中，指定連結網頁的完整URL路徑。</li> 
       </ul> <p>請確定您要指定是在新瀏覽器標籤中或在目前標籤中開啟連結。</p> </td> 
      </tr> 
      <tr> 
      <td>將選取的縮圖影像與體驗片段建立關聯</td> 
      <td><p>在「動作類型」下方，點選「 <strong>體驗片段</strong>」，然後執行下列動作：<p> 
       <ul> 
       <li>如果您是AEM Sites客戶，請點選或按一下「搜尋」圖示（放大鏡）以開啟「體驗片段」頁面。 點選或按一下您要使用的體驗片段，然後點 <strong></strong>選頁面右上角的「選取」，返回上一頁的「動作」面板。<br /> 請參閱 <a href="/help/sites-authoring/experience-fragments.md">體驗片段</a>。</li> 
      </ul> 
       <ul> 
       <li>指定「體驗片段」的寬度和高度，如影片所示。</li>
       </ul><strong>注意</strong>:請注意，當您將檢視器內嵌在「體驗片段」時，不支援「互動式視訊」中的社交媒體分享工具。 若要解決這個問題，您可以使用或建立沒有社交媒體分享工具的檢視器預設集。 這些檢視器預設集可讓您成功將它內嵌在「體驗片段」中。</p></tr>&lt; 
      <tr> 
      <td>若要編輯已指派給縮圖影像的動作</td> 
      <td>在時間軸區段中，點選文字標籤右側有連結的縮圖影像。 連結指示已為其指派操作。 點選「 <strong>動作</strong> 」標籤以進行變更。</td> 
      </tr> 
      <tr> 
      <td>若要變更縮圖影像的文字標籤</td> 
      <td><p>依預設，文字標籤會使用縮圖影像的中繼資料 <code>Title</code> 欄位。 如果 <code>Title</code> 未顯示，則會改用縮圖影像的檔案名稱，但不使用副檔名。</p> <p>若要變更縮圖影像的文字標籤，請在「動作」標 <strong>簽 </strong>的正下方，輸入所要的文字。 請參閱下圖。</p> <p>請注意，新文字標籤僅供視訊播放器本身及顯示在時間軸區段中的縮圖文字使用。 標籤變更不會影響縮圖影像的「標題」中繼資料欄位，也不會影響其檔案名稱。</p> </td> 
      </tr> 
      <tr> 
      <td>要恢復您所做的更改</td> 
      <td>在頁面的右上角附近，點選「復原 <strong>」</strong> 或「 <strong>重做」</strong>。</td> 
      </tr> 
    </tbody> 
   </table>

   ![experiencefragment_interactivevideos](assets/experiencefragment_interactivevideos.png)

   縮圖影像會新增一個文字標籤。

1. 執行下列任一項作業：

   * 重複步驟6-11，將更多縮圖影像新增至影片中的時間軸區段。
   * 繼續選擇步驟13。

1. （可選）執行下列任一項作業：

   * **[!UICONTROL 合併區段]** -您可以將兩個相鄰的區段（無論是否已指派產品縮圖）合併為一個區段。

      在時間軸上，點選兩或多個要合併為一個的連續區段。 請注意，下圖中的兩個選定段上沒有藍色橢圓拖動控制滑塊。

      點選 **[!UICONTROL 工具列上的]** 「合併區段」。
   ![chlimage_1-134](assets/chlimage_1-134.png)

   將兩個選定的五個第二段合併為一個十個第二段。

   * **[!UICONTROL 分割區段]** -您可以將單一區段分割為兩個計時相同的區段。 如果已將產品縮圖指派給區段，則縮圖會合併到左側區段。

      在時間軸上，點選您要分成一半的區段，然後點選工具列上的 **[!UICONTROL 分割區段]** 。

      選取兩或多個區段會停用「分割 **[!UICONTROL 區段]** 」功能。
   ![chlimage_1-135](assets/chlimage_1-135.png)

   將選取的10秒區段分割為兩個區段，每個區段5秒。

1. 在「建立互動式視訊」頁 **[!UICONTROL 面的右上角附近]** ，會顯示目前選取與視訊一起使用的檢視器預設集名稱。 點選名稱以選取不同的檢視器預設集。

   例如，檢視器預 `Shoppable_Video_light` 設集可讓您播放視訊，其中顯示區域是與視訊相鄰的白色。 顯示區域是播放期間可點選縮圖影像的顯示區域。 檢視 `Shoppable_Video_dark` 器預設集可讓您播放視訊，其中視訊旁有黑色顯示區域。

   如果您建立了自己的互動式視訊檢視器預設集，您也會在您可選擇的預設集清單中看到它。

   完成後，點選「儲 **[!UICONTROL 存」]**。

   >[!NOTE]
   當您儲存互動式視訊時，會自動 `.vtt` 儲存相關的檔案。 檔 `.vtt` 案會儲存至位 `_VTT` 於資產根目錄的資 **[!UICONTROL 料夾]**。 您的互動式視訊必須有檔案和資料夾才能在網站上正確播放。 因此，請勿移動、編輯或刪除資料夾 `_VTT` 或其內容。

1. 發佈互動式視訊。 發佈會建立內嵌代碼或URL，您最終會將其複製並貼至您的網站體驗。

   如果您使用Quickviews新增互動功能，則只使用內嵌程式碼；如果您使用超連結網頁新增互動功能，也可以使用發佈的URL。 不過請注意，如果您的互動式內容具有相對URL的連結，尤其是AEM Sites頁面的連結，就無法使用以URL為基礎的連結方法。

   請參閱 [發佈資產](publishing-dynamicmedia-assets.md)。

   >[!NOTE]
   若要使用Quickviews發佈可購買的視訊，請確定您也會從您的商務區個別發佈視訊的每個相關影像資產。

   新增時間軸區段並發佈互動式視訊後，您就可將它新增至現有的網站登陸頁面。 請參 [閱整合互動式視訊與您的網站。](#integrating-an-interactive-video-with-your-website)

## 發佈互動式視訊資產 {#publishing-interactive-video-assets}

如需如 [何發佈互動式視訊資產](/help/assets/publishing-dynamicmedia-assets.md) ，請參閱發佈資產。

## 將互動式視訊與您的網站整合 {#integrating-an-interactive-video-with-your-website}

在您上傳影片、新增時間軸區段至影片，以及發佈互動式影片後，您現在可以將它新增至現有網站。

如果您是AEM Sites客戶，可將Interactive media元件拖曳至您的頁面，以新增互動式視訊。 請參閱 [新增動態媒體資產至頁面。](/help/assets/adding-dynamic-media-assets-to-pages.md)

如果您是獨立的AEM Assets客戶，您可以依本節所述，手動將互動式視訊新增至您的網站。

1. 複製已發佈的互動式視訊的內嵌程式碼或URL。
請參 [閱將視訊或影像檢視器內嵌在網頁上](/help/assets/embed-code.md)。
如果您使用Quickviews新增互動功能，則只使用內嵌程式碼；如果您使用超連結網頁新增互動功能，也可以使用發佈的URL。 不過請注意，如果您的互動式內容具有相對URL的連結，尤其是AEM Sites頁面的連結，就無法使用以URL為基礎的連結方法。

1. 在目標的網頁程式碼中，識別靜態視訊的位置。
1. 移除靜態視訊，並以您從AEM Assets複製的內嵌代碼或URL取代代碼，如同。
複製的內嵌程式碼是為回應式環境而設定，因此應自動符合靜態視訊先前所佔用的區域。

>[!NOTE]
此時，如果您只新增超連結網頁的互動功能，就完成了。
不過，如果您新增任何互動功能來觸發Quickview，則互動視訊旁的縮圖僅供顯示之用；它們尚未與您現有的Quickviews整合。 在這種情況下，您現在需要將互動式視訊與網站上現有的Quickviews整合。

**範例**

以示範網站為例：

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html)

請注意，它是標準的視訊內嵌代碼：

```xml
<style type="text/css">
 #s7video_div.s7videoviewer{
   width:100%;
   height:auto;
 }
</style>

<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/VideoViewer.js"></script>
<div id="s7video_div"></div>
<script type="text/javascript">
 var s7videoviewer = new s7viewers.VideoViewer({
  "containerId" : "s7video_div",
  "params" : {
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Video",
   "config2": "/etc/dam/presets/analytics",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "posterimage": "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 }).init();
</script>
```

整合就像從AEM移除視訊內嵌程式碼，並以互動式視訊內嵌程式碼取代一樣簡單。 您可在下列URL中看到結果。 雖然它會在頁面上顯示互動式視訊，但尚未與現有的Quickview整合：

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-1.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-1.html)

## 將互動式視訊與現有的Quickview整合 {#integrating-an-interactive-video-with-an-existing-quickview}

>[!NOTE]
此工作僅在您是獨立AEM Assets客戶時適用。

此程式的最後一個步驟是將互動式視訊與網站上使用的現有Quickview實作整合。 沒有適合所有情況的整合解決方案。 每個Quickview實施都是獨一無二的。 因此，需要一種最可能需要前端IT人員協助的具體方法。

現有的Quickview實施通常表示網頁上發生的一系列相互關聯的操作，其順序如下：

1. 使用者會在您網站的使用者介面中觸發元素。
1. 前端代碼根據在步驟1中觸發的用戶介面元素獲取Quickview URL。
1. 前端程式碼會使用步驟2中取得的URL來傳送AJAX要求。
1. 後端邏輯會將對應的Quickview資料或內容傳回前端程式碼。
1. 前端代碼載入Quickview資料或內容。
1. 或者，前端代碼將載入的Quickview資料轉換為HTML表示法。
1. 前端程式碼會顯示模式對話方塊或面板，並轉譯HTML內容給使用者。

這些呼叫可能不代表獨立的公用API呼叫，而網頁邏輯可透過任意步驟呼叫這些呼叫。 相反地，它是連結呼叫，在此連結呼叫中，前一個步驟的最後一個階段（回呼）中將隱藏下一個步驟。

在互動式視訊取代步驟1和部分步驟2的同時，當使用者按一下互動式視訊中的縮圖時，檢視器會處理這類使用者互動。 檢視器會將事件傳回網頁，其中包含先前新增至AEM的所有縮圖資料。

在這種事件處理常式中，前端程式碼會執行下列動作：

* 監聽互動式視訊所發出的事件。
* 根據縮圖資料建構Quickview URL。
* 觸發從後端載入Quickview並在螢幕上顯示的程式。

此外，互動式視訊檢視器支援全螢幕作業模式。 一般使用者只要按一下縮圖，就會觸發Quickviews，而不需離開全螢幕。 若要實現此功能，請變更前端程式碼，讓Quickview強制回應對話方塊附加至檢視器的容器。 請勿新增檢視器處於全螢幕模式時無法使用的檔案BODY或其他網頁元素。 執行此工作的程式碼需要聽取檢視器載入頁面後所傳送的另一個檢視器回呼。

AEM傳回的內嵌代碼已經有現成的事件處理常式。 如下列反白顯示的程式碼片段所示，會加上註解：

```xml
<style type="text/css">
 #s7interactivevideo_div.s7interactivevideoviewer{
   width:100%;
   height:auto;
 }
</style>
<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/InteractiveVideoViewer.js"></script>

<div id="s7interactivevideo_div"></div>
<script type="text/javascript">
 var s7interactivevideoviewer = new s7viewers.InteractiveVideoViewer({
  "containerId" : "s7interactivevideo_div",
  "params" : {
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Video_light",
   "config2": "/etc/dam/presets/analytics",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "interactivedata": "content/dam/_VTT/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4.svideo.vtt",
   "VideoPlayer.contenturl": "https://adobedemo62-h.assetsadobe.com/is/content",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 })
 /* // Example of interactive video event for quickview.
   s7interactivevideoviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku; //SKU for product ID
    //To pass other parameter from the hotspot, you need to add custom parameter during the hotspot setup as parameterName=value
    loadQuickView(sku); //Replace this call with your quickview plugin
    //Please refer to your quickviewer plugin for the quickview call
    },
"initComplete":function() {
    //--- Attach quickview popup to viewer container so popup will work in fullscreen mode ---
    var popup = document.getElementById('quickview_div'); // get custom quickview container
    popup.parentNode.removeChild(popup); // remove it from current DOM
    var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
    var inner_container = document.getElementById(sdkContainerId);
    inner_container.appendChild(popup); //Attach custom quickview container to viewer
    }
   });
 */
 s7interactivevideoviewer.init();
</script>
```

因此，只需取消上述反白顯示的程式碼片段的註解，並以特定網頁專用的程式碼取代虛擬處理常式主體即可。

標準內嵌程式碼中有兩個預設回呼處理常式： `quickViewActivate` 和 `initComplete`。 在檢 `quickViewActivate` 視器中按一下縮圖時，處理常式就會觸發。 使用它將檢視器與Quickview啟動邏輯整合。 當檢 `initComplete` 視器載入頁面時，處理常式只會觸發一次。 此處理常式用於調整網頁DOM中的Quickview對話方塊位置。

建構Quickview URL的程式與識別本主題前面所涵蓋的縮圖變數的程式相反。 使用我們先前確定的Quickview URL示例，您可以瞭解每種情況下如何構建Quickview URL:

<table>
  <tbody>
  <tr>
    <td><p>單一SKU，可在查詢字串中找到</p> </td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;source=100";
      },
      });</code></td>
  </tr>
  <tr>
    <td>單一SKU，位於URL路徑中</td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/product/" + inData.sku;
      },
      });</code></td>
  </tr>
  <tr>
    <td><p>查詢字串中的SKU和類別ID</p> </td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;prodId=" + inData.sku;
      },
      });</code></td>
  </tr>
  </tbody>
</table>

觸發Quickview URL並啟動Quickview面板的最後一個步驟很可能需要您IT部門的前端IT人員協助。 他們具備最佳的知識，可瞭解如何從正確的步驟準確觸發Quickview實施，並擁有現成可用的Quickview URL。

您可以瞭解這些步驟如何套用至示範網站，以將互動式視訊與Quickview程式碼完全整合。 在本主題的前面，Quickview URL的結構已標識為：

```xml
/datafeed/$CategoryId$-$SKU$.json
```

使用物件中可用的欄位(透過檢 `quickViewActivate` 視器的程式碼傳遞 `categoryId``sku``inData` 至處理常式)，輕鬆在處理常式中重建此URL，如下所示：

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

示範網站會使用簡單函式呼叫來觸發「快速檢視」 `loadQuickView()` 對話方塊。 此函式只使用一個引數，即Quickview資料URL。 因此，整合互動式視訊的最後一個步驟是將下列程式碼行新增至處理 `quickViewActivate` 常式：

```xml
loadQuickView(quickViewUrl);
```

最後，請確定您的Quickview對話方塊已附加至檢視器的容器元素。 預設內嵌程式碼提供實現此功能的範例步驟。 若要取得檢視器容器元素的參考，您可以使用下列程式碼行：

```xml
var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
var inner_container = document.getElementById(sdkContainerId);
```

其中 `inner_container` 是檢視器管理之 `DIV` 元素的參考。 您希望該對話框是該對話框的子項 `DIV`。

實際定位模態對話框元素並將其附加到上述容器的步驟是特定大小寫的。 同樣地，您也可以向熟悉您所需Quickview實作的前端開發人員尋求協助。

在範例網站中，「快速檢視」模式對話方塊會實作為直接附 `DIV` 加至檔案的快速檢視模式ID `BODY`。 因此，將該對話方塊移至檢視器容器的程式碼與下列程式碼一樣簡單：

```xml
var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
var inner_container = document.getElementById(sdkContainerId);
inner_container.appendChild(document.getElementById("quickview-modal"));
```

完整的原始碼如下：

```xml
<style type="text/css">
 #s7interactivevideo_div.s7interactivevideoviewer{
   width:100%;
   height:auto;
 }
</style>
<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/InteractiveVideoViewer.js"></script>

<div id="s7interactivevideo_div"></div>
<script type="text/javascript">
 var s7interactivevideoviewer = new s7viewers.InteractiveVideoViewer({
  "containerId" : "s7interactivevideo_div",
  "params" : {
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Video_light",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "interactivedata": "content/dam/_VTT/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4.svideo.vtt",
   "VideoPlayer.contenturl": "https://adobedemo62-h.assetsadobe.com/is/content",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 })
 // Example of interactive video event for quickview.
   s7interactivevideoviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku; //SKU for product ID
     var categoryId=inData.categoryId; //categoryId
    var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
    loadQuickView(quickViewUrl);
    },
   "initComplete":function() {
    //--- Attach quickview popup to viewer container so popup will work in fullscreen mode ---
    var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
    var inner_container = document.getElementById(sdkContainerId);
    inner_container.appendChild(document.getElementById("quickview-modal"));
    }
   });
 s7interactivevideoviewer.init();
</script>
```

完整整合互動式影片的最終示範網站如下所示：

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-3.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-3.html)

## 使用Quickviews建立自訂快顯視窗 {#using-quickviews-to-create-custom-pop-ups}

請參 [閱使用快速檢視建立自訂快顯視窗](/help/assets/custom-pop-ups.md)。
