---
title: 互動式影片
description: 瞭解如何在Dynamic Media中使用互動式視訊和可訂購視訊
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
feature: Interactive Videos
role: User, Admin
exl-id: d118879d-c17b-43f3-9cc8-0405531b4d9f
solution: Experience Manager, Experience Manager Assets
source-git-commit: f8588ef353bd08b41202350072728d80ee51f565
workflow-type: tm+mt
source-wordcount: '5914'
ht-degree: 2%

---

# 互動式影片{#interactive-videos}

您可以輕鬆建立互動式視訊（也稱為可購物視訊），以直接從視訊推動轉換。 客戶與影片互動於影片播放器旁的面板中進行，相關服務、資訊或產品縮圖會根據影片中的功能捲動至檢視畫面中。 客戶可以選取縮圖並直接連結至服務，或將專案新增至購物車以立即購買，或連結至網頁以取得詳細資訊。

影片結束時，會顯示所有方案的視覺化摘要，以推動call to action。 客戶有另一個機會可選取他們想要的專案。 這類可操作且特定的體驗，可增加客戶參與度和轉換率。

另請參閱[互動式影像](/help/assets/interactive-images.md)。

## 互動視訊的實際運作情況 {#interactive-video-in-action}

若要檢視互動式、可購物視訊的實際運作情況，請選取「[即時示範](https://landing.adobe.com/tw/na/dynamic-media/ctir-2755/live-demos.html)」，捲動至頁面上的「**[!UICONTROL 可購物媒體]**」標題，然後選取可購物視訊。

* 在播放期間，當視訊中使用產品時，相同的產品會在右側顯示為縮圖影像。

* 如果要暫停視訊並開啟產品的快速檢視，請選取縮圖。 例如，在視訊中選取KitchenAid縮圖影像以體驗混合器的360度旋轉檢視，或放大以檢視混合器詳細資訊。

<!-- There was a link here that showed the video frame of an interactive video and when the reader selected the frame the video would play https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/AXIS/index.html?lang=zh-Hant. This now needs to call a new interactive video-->

![互動式可購物視訊的影格](assets/chlimage_1-126.png) *互動式可購物視訊的視訊影格擷取。*

>[!NOTE]
>
>如果您在使用者選取縮圖影像時，建立互動視訊以啟動網頁，則某些裝置會封鎖快顯網頁的開啟。 在這種情況下，您必須變更裝置上的快顯封鎖程式設定。 例如，在Apple iPhone 6上，導覽至&#x200B;**[!UICONTROL 設定]** > **Safari** > **封鎖快顯視窗**，然後將控制項滑動至&#x200B;**[!UICONTROL 關閉]**。 現在，在播放互動式視訊並選取縮圖時，如果您想要開啟快顯視窗，系統會提示您輸入。 如果您接受，網頁會開啟。

### 觀看互動式視訊的建立方式 {#watch-how-interactive-videos-are-created}

播放[如何建立互動式視訊的逐步解說](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&emailurl=https://s7d5.scene7.com/s7/emailFriend&serverUrl=https://s7d5.scene7.com/is/image/&config=Scene7SharedAssets/Universal_HTML5_Video_social&contenturl=https://s7d5.scene7.com/skins/&asset=S7tutorials/InteractiveVideo) （7分30秒）。
雖然視訊逐步說明已加上Assets on Demand品牌，但Adobe Experience Manager Assets中的互動式視訊仍適用原則和步驟。

### Adobe客戶解決方案網路研討會 {#adobe-customer-success-webinar}

「在Experience Manager Assets中使用互動式視訊、連結共用和YouTube共用」網路研討會會教導您如何使用互動式視訊和其他功能，將轉換驅動的事件連結至視訊行銷內容。

<!-- NOT FOUND; FIND REPLACEMENT
>[!NOTE]
>
>[Using Interactive Video, Link Sharing, and YouTube sharing in Experience Manager Assets](https://adobecustomersuccess.adobeconnect.com/p1yxzdo4aec/). 
-->

## 快速入門：互動式影片 {#quick-start-interactive-videos}

下列逐步工作流程說明可協助您在Dynamic Media中快速啟動並執行互動式影片。

在部分快速入門工作中尋找&#x200B;**範例**&#x200B;標題。 它包含以這個開始示範網頁為基礎的簡短教學課程，*尚未*&#x200B;新增互動功能：

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html?lang=zh-Hant](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html?lang=zh-Hant)

範例 **可協助您說明** ，如何將互動式視訊整合在您自己的網站上。

當您完成最後一個範例區段中的教學課程時，最後示範網頁與完全整合的互動式影片看起來會像這樣：

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-3.html?lang=zh-Hant](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-3.html?lang=zh-Hant)

互動視訊步驟：

1. **（選擇性）識別Quickview變數** — 從識別現有Quickview實作所使用的動態變數開始。 當您建立互動式視訊時，可使用變數將產品縮圖對應至其對應的產品快速檢視。 請參閱[（選擇性）識別快速檢視變數](#optional-identifying-quickview-variables)。
   *只有在下列全部為true時才需要此步驟*：
   * 您想要透過觸發至快速檢視來將互動性新增至視訊。
   * 您實作Experience Manager時，*不會*&#x200B;使用電子商務整合架構，將產品資料從任何電子商務解決方案(例如IBM®WebSphere®Commerce、Elastic Path、Hybris或Intershop)提取至Experience Manager。 檢視Experience Manager Assets[中的](/help/commerce/cif-classic/administering/concepts.md)電子商務概念。

1. **（選擇性）建立互動式視訊檢視器預設集** — 自訂組成播放器的各種元件的外觀和行為，例如視訊筆畫壓感和互動式縮圖。
如果您打算使用現成的互動視訊檢視器預設集`Shoppable_Video_Light`或`Shoppable_Video_Dark`，則不需要建立自己的互動視訊檢視器預設集。
請參閱[建立檢視器預設集](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset) （選擇性）和[建立互動式檢視器預設集的特殊考量](/help/assets/managing-viewer-presets.md#special-considerations-for-creating-an-interactive-viewer-preset)。

1. **上傳視訊及其相關影像資產** — 上傳您要互動的視訊和相關影像。
請參閱[上傳視訊及其相關縮圖資產](#uploading-a-video-and-its-associated-thumbnail-assets)。

   >[!NOTE]
   >
   >Dynamic Media尚不支援MXF視訊格式用於互動式視訊。

1. **將互動性新增至您的視訊** — 新增一或多個時間區段至視訊。 然後，在這些時間區段中建立影像縮圖的關聯。 將每個影像縮圖指派給動作，例如超連結、快速檢視或體驗片段。
(如果您的互動式內容有具有相對URL的連結，尤其是指向Experience Manager Sites頁面的連結，則無法採用URL型連結方法。)
完成發佈互動式視訊資產。 發佈作業會建立內嵌程式碼或URL，您最終會複製並套用至您的網站登陸頁面。 請參閱[將互動性新增至視訊](#adding-interactivity-to-your-video)。
請參閱[發佈Assets](/help/assets/publishing-dynamicmedia-assets.md)。

1. **在Experience Manager中，將互動式視訊新增至您的網站或網站** — 如果您使用Experience Manager Sites或eCommerce或兩者，則可以將互動式視訊新增至網頁。 將互動媒體元件拖曳至Experience Manager中的頁面。 請參閱[將Dynamic Media Assets新增至頁面](/help/assets/adding-dynamic-media-assets-to-pages.md)。
使用內嵌程式碼或URL，將您的互動式視訊與網站體驗整合。 請參閱[將互動式視訊與您的網站整合](#integrating-an-interactive-video-with-your-website)。
如果您使用協力廠商WCM （Web內容管理員），您必須將新的互動式視訊與網站上使用的現有Quickview實作整合。 請參閱[將互動式視訊與現有的快速檢視](#integrating-an-interactive-video-with-an-existing-quickview)整合。
   [將Dynamic Media Assets新增至頁面](/help/assets/adding-dynamic-media-assets-to-pages.md)

## （選用）識別快速檢視變數 {#optional-identifying-quickview-variables}

>[!NOTE]
>
>只有在下列情況為真時才需要此工作：
>
>* 您想要透過觸發至快速檢視來將互動性新增至視訊。
>* 您實作Experience Manager時，*不會*&#x200B;使用電子商務整合架構，將產品資料從任何電子商務解決方案(例如IBM®WebSphere®Commerce、Elastic Path、Hybris或Intershop)提取至Experience Manager。 檢視Experience Manager Assets[中的](/help/commerce/cif-classic/administering/concepts.md)電子商務概念。
>
>如果您的Experience Manager實作使用電子商務，您可以略過此任務並繼續下一個任務。

首先，識別您現有Quickview實作所使用的動態變數，以便您可以在互動式視訊建立程式中將產品縮圖對應至其對應的產品Quickview。

當您新增時間區段至視訊時，會指派SKU （庫存單位）和任何其他變數至您新增至區段的每個縮圖。 這類變數稍後會用於顯示正確的Quickview產品。

請務必正確識別哪些變數需要以唯一方式觸發產品Quickview。

有時候，諮詢負責現有Quickview實作的IT專家就足夠了。 他們可能會知道系統中用於識別快速檢視的最低資料集。 但是，也可以只分析前端計畫碼的現有行為。

大部分的「快速檢視」實作都使用下列範例：

* 使用者在網站上啟動使用者介面元素。例如，選取「快速檢視」按鈕。
* 如有需要，網站會傳送Ajax請求至後端以載入快速檢視資料或內容。
* 快速檢視資料會轉譯成內容，以備在網頁上轉譯。
* 最後，前端程式碼會在畫面上以視覺化方式呈現此類內容。

因此，方法就是瀏覽現有網站中實作Quickview的不同區域、觸發Quickview，並擷取網頁傳送的Ajax URL以載入Quickview資料或內容。

通常您不需要使用任何專門的偵錯工具。 現代的網頁瀏覽器配備能夠執行適當工作的網頁檢查器。 以下是一些包含網頁檢查器的網頁瀏覽器範例：

* 若要檢視Google Chrome中的所有傳出HTTP要求，請按&#x200B;**F12** (Windows)或&#x200B;**Command+Options+I** (Mac)開啟[開發人員工具]面板，然後選取&#x200B;**網路**&#x200B;索引標籤。

* 在Firefox中，您可以按&#x200B;**F12** (Windows)或&#x200B;**Command+Option+I** (Mac)並使用其&#x200B;**`[Net]`**&#x200B;標籤來啟動Firebug外掛程式，或使用內建的偵測器工具及其「網路」標籤。

* 在Internet Explorer中，按&#x200B;**F12**&#x200B;啟動偵錯工具。

在瀏覽器中開啟網路監視時，會觸發頁面上的快速檢視。

現在，請在網路記錄檔中找到Quickview Ajax URL，並複製紀錄的URL以供日後分析。 通常，當您觸發「快速檢視」時，會有許多要求傳送至伺服器。 通常，快速檢視Ajax URL是清單中的第一個專案。 它具有複雜的查詢字串部分或路徑，而且其回應MIME型別是`text/html`、`text/xml`或`text/javascript`。

在此過程中，請務必使用不同的產品類別和型別，造訪您網站的不同區域。 原因是快速檢視URL可以擁有指定網站類別的共同部分，但只有在您造訪網站的其他區域時才會變更。

最簡單的情況是，快速檢視URL中的唯一變數部分是產品SKU。 在此情況下，在Experience Manager的互動式視訊中，將縮圖新增至時間區段所需的唯一資料片段就是產品SKU值。

不過，在複雜的情況下，快速檢視URL會有不同元素，以及產品SKU不同，例如類別ID、顏色代碼和大小代碼。 在這種情況下，在Experience Manager的縮圖資料定義中，每個這類元素都會變成個別變數。

請考量下列快速檢視URL範例及其產生的縮圖變數：

<table>
  <tbody>
  <tr>
    <td><p>在查詢字串中找到單一SKU。</p> </td>
    <td><p>錄製的快速檢視URL包含以下專案：</p>
    <ul>
      <li><p><code>https://server/json?productId=866558&source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1196184&source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1081492&source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1898294&source=100</code></p> </li>
    </ul> <p>URL中唯一的變數部分是<code>productId=</code>查詢字串引數的值，而且它顯然是SKU值。 因此，您的縮圖只需要填入<strong><code>866558</code></strong>、<strong><code>1196184</code></strong>、<strong><code>1081492</code></strong>、<strong><code>1898294</code></strong>等值的SKU欄位。</p> </td>
  </tr>
  <tr>
    <td><p>在URL路徑中找到單一SKU。</p> </td>
    <td><p>錄製的快速檢視URL包含以下專案：</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>變數部分位於路徑的最後一部分，且會變成Experience Manager縮圖的SKU值： <strong><code>6422350843</code></strong>、<strong><code>1607745002</code></strong>、<strong><code>0086724882</code></strong>。</p> </td>
  </tr>
  <tr>
    <td><p>查詢字串中的SKU和類別ID。</p> </td>
    <td><p>錄製的快速檢視URL包含以下專案：</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&prodId=308706</code></p> </li>
    </ul> <p>在這種情況下，URL中有兩個不同的部分。 SKU儲存在<code>prodId</code>引數中，而類別識別碼儲存在<code>category=</code>引數中。</p> <p>因此，縮圖定義成對。 即SKU值和稱為<code>categoryId</code>的額外變數。 產生的配對如下：</p>
    <ul>
      <li>SKU是<code>305466</code>，<code>categoryId</code>是 <code>1100004</code></li>
      <li>SKU是<code>310181</code>，<code>categoryId</code>是 <code>1100004</code></li>
      <li>SKU是<code>308706</code>，<code>categoryId</code>是 <code>1740148</code></li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**範例**

將上述方法套用至範例網站時，您的網頁會有數個產品縮圖，每個縮圖都有「檢視更多」按鈕：

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html?lang=zh-Hant](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html?lang=zh-Hant)

啟用頁面上可用的所有產品快速檢視後，您會取得向後端提出之快速檢視要求的清單如下：

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

檢視伺服器呼叫，就會發現要求路徑中只會出現產品專屬資訊。 您也會發現根本不會使用查詢字串，而且其中涉及兩種不同型別的資料片段：

* 第一種是蠟燭、墊子、傢俱和玻璃器具。 您可以將此區段稱為「產品類別」。
* 第二種是產品代碼，例如233916597。 您可以假設這是「產品SKU」。

根據此資訊，整個快速檢視URL的模式如下：

`/datafeed/$categoryId$-$SKU$.json`

根據此類分析，您得出結論：您可以針對縮圖使用下列兩個變數： `categoryId`和`SKU`。

您現在已準備好上傳視訊及其相關縮圖資產。

## （可選）建立互動式視訊檢視器預設集 {#optional-creating-an-interactive-video-viewer-preset}

如果您打算使用預設的、現成可用的互動式視訊檢視器預設集型別`Shoppable_Video_dark`或`Shoppable_Video_light`，可以略過此工作並繼續下一個。

在製作環境中選取縮圖時，會出現「快速檢視」對話方塊的預覽。

![chlimage_1-21](assets/chlimage_1-127.png)

您可以選擇建立自己的自訂互動式視訊檢視器預設集。 您可以決定視訊播放器的樣式、互動式縮圖，以及在視訊結尾顯示的縮圖格線檢視等。

互動式視訊檢視器預設集可正確轉譯您新增的視訊和所有時間軸區段。 當您在預覽模式中選取產品縮圖時，它也會使用預設快速檢視的範例，讓您在發佈之前測試其互動性。

儲存檢視器預設集後，「檢視器預設集」頁面中的檢視器預設集狀態會自動設為&#x200B;**On**。 此狀態表示在動態媒體元件中及您使用它預覽視訊時，都可看到它。請確定您也手動發佈新的檢視器預設集。

請參閱[建立新的檢視器預設集](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset)，以建立您自己的互動式視訊檢視器預設集。

## 上傳視訊及其相關縮圖資產 {#uploading-a-video-and-its-associated-thumbnail-assets}

如果您已上傳視訊和縮圖資產，請繼續進行[新增互動功能至視訊](#adding-interactivity-to-your-video)。

>[!NOTE]
>
>Dynamic Media尚不支援MXF視訊格式用於互動式視訊。

若您上傳了錯誤的視訊或影像，或要刪除您不再需要的已上傳視訊或影像，請參閱[刪除資產](/help/assets/manage-assets.md#deleting-assets)。

若要上傳視訊及其相關縮圖資產：

1. 將視訊和相關聯的縮圖資產上傳到您想要的資料夾。

   請參閱[上傳資產](/help/assets/manage-assets.md)。
請參閱[使用FTP工作排程](/help/assets/manage-assets.md)上傳資產。

   現在將互動性新增至您的視訊。

## 將互動性新增至視訊 {#adding-interactivity-to-your-video}

您可以使用「建立互動式視訊」頁面上的就地視覺編輯器，將時間軸區段新增至視訊。

新增時間軸區段後，您即可在每個區段內新增縮圖影像。 對於您新增的每個縮圖，您都會對其套用動作。 例如，您可以將快速檢視套用至縮圖、指派超連結至縮圖或體驗片段。

請參閱[體驗片段](/help/sites-authoring/experience-fragments.md)。

>[!NOTE]
>
>將檢視器內嵌在體驗片段中時，不支援互動視訊中的社群媒體分享工具。 若要解決此問題，您可以使用或建立沒有社群媒體分享工具的檢視器預設集。 這類檢視器預設集可讓您成功將其嵌入體驗片段中。

>[!NOTE]
>
>如果您的互動式內容有具有相對URL的連結，尤其是指向Experience Manager Sites頁面的連結，則無法採用URL型連結方法。

在您目前的建立/編輯作業階段期間，支援頁面右上角附近的「復原」和「重做」選項。

儲存互動式視訊後，視訊會立即開啟預覽。 從那裡，您可以選取互動式視訊檢視器預設集並播放視訊，以檢視向客戶呈現的大致呈現方式。

**若要在視訊中新增互動功能：**

1. 在Assets檢視中，導覽至您上傳且想要互動的影片。
1. 執行下列任一項作業：

   * 將滑鼠指標暫留在影像上，然後選取&#x200B;**[!UICONTROL 選取]** （核取記號圖示）。 在工具列上，選取&#x200B;**[!UICONTROL 編輯]**。

   * 將滑鼠停留在影像上，然後選取&#x200B;**[!UICONTROL 更多動作]** （三點圖示） **[!UICONTROL >編輯]**。

   * 選取影像，以便在「詳細資料檢視」頁面中開啟影像。 在工具列上，選取&#x200B;**[!UICONTROL 編輯]**。

1. 在「建立互動式視訊」頁面上，執行下列任一項作業：

   * 若要開始播放視訊，請選取&#x200B;**[!UICONTROL 播放]**&#x200B;按鈕。 當您要反白顯示的特定產品、服務或詳細資訊進入檢視畫面時，請選取工具列上的&#x200B;**[!UICONTROL 新增區段]**。 重複此步驟，直到您到達視訊結尾為止。

     針對您新增的每個時間區段，指派一或多個縮圖影像至該區段，然後將這些縮圖連結至Quickview產品頁面以供客戶購買或連結至網頁，以取得詳細資訊。

   * 若要開始播放視訊，請選取&#x200B;**[!UICONTROL 播放]**&#x200B;按鈕。 檢視您要反白顯示的特定產品、服務或詳細資料時，請選取&#x200B;**[!UICONTROL 暫停]**。 選取&#x200B;**[!UICONTROL 新增區段]**。

     在您要新增區段的時間軸上的各個點繼續播放和暫停視訊，直到視訊結束。

1. （可選）向左拖曳&#x200B;**[!UICONTROL 時間軸縮放滑桿]**&#x200B;上的橫條，以放大或向右縮小，讓您能夠控制您所新增區段的詳細程度。

   ![chlimage_1-22](assets/chlimage_1-128.png)

   視視訊長度而定，「區段持續時間」會預設為下列值：

   <table>
      <tbody>
        <tr>
        <td><strong>如果影片長度為……</strong></td>
        <td><strong>「區段持續時間」設定預設為……</strong></td>
        </tr>
        <tr>
        <td>3分鐘以上</td>
        <td>60秒</td>
        </tr>
        <tr>
        <td>2-3 分鐘</td>
        <td>30秒</td>
        </tr>
        <tr>
        <td>1-2 分鐘</td>
        <td>20秒<br /> </td>
        </tr>
        <tr>
        <td>30-60秒</td>
        <td>10秒</td>
        </tr>
        <tr>
        <td>30秒以內</td>
        <td>5秒</td>
        </tr>
      </tbody>
    </table>

   視訊時間軸使用的熒幕空間量，不限其可用空間。 因此，調整瀏覽器大小時，您新增的區段會維持其正確寬度。

   舉例來說，以下三個熒幕擷取畫面均使用相同影片。 請注意，每個區段的寬度會隨著「時間軸比例」設定而改變。

   ![chlimage_1-23](assets/chlimage_1-129.png)

   熒幕擷圖A

   上方的熒幕擷圖A顯示29秒產品視訊的預設檢視。 「時間軸比例」設定為預設值5秒。

   ![chlimage_1-130](assets/chlimage_1-130.png)

   熒幕擷圖B

   在上方的熒幕擷圖B中，「時間軸比例」滑桿已從5秒的預設值拖曳至3秒。 請注意，個別「時間軸比例」時間戳記現在都以3秒為間隔設定。

   ![chlimage_1-25](assets/chlimage_1-131.png)

   熒幕擷圖C

   在上方的熒幕擷圖C中，「時間軸比例」設定已移動到8秒。 請注意包含產品縮圖的區段縮小方式。 如果您有長影片，而且您想要能夠看到更多一般符合頁面寬度的區段概觀，以此方式縮小會很有用。

1. (選用) 執行以下任一操作：

   * 調整區段的開始時間和結束時間。

     選取區段，然後拖曳前導或尾隨的藍色橢圓以分別調整開始或結束時間。 顯示的視訊影格會根據您的調整移至視訊中的適當時間。 時間軸區段的移動會根據時間軸中任何相鄰區段而受限制。 允許的區段時間下限為一秒。

     使用下列導覽捷徑來快速檢查並微調視訊區段：

      * 若要直接尋找該區段開頭的視訊，請選取開頭的藍色橢圓形。
      * 若要直接搜尋視訊到該區段的結尾，請選取結尾的藍色橢圓形。
      * 若要將視訊播放傳回該區段的開頭，請選取整個區段。

   ![chlimage_1-26](assets/chlimage_1-132.png)

   重新定位時間軸區段的結尾

   * 若要刪除區段

     選取時間軸上的最後一個區段，然後在工具列上選取&#x200B;**[!UICONTROL 刪除區段]**。 如果選取了兩個或多個區段，則會停用&#x200B;**[!UICONTROL 刪除區段]**。

     您只能刪除最後一個區段。 例如，如果您想要刪除時間軸上的所有區段，您必須一律選取最後一個區段，然後選取&#x200B;**[!UICONTROL 刪除區段]**。

1. 選取您要關聯一或多個縮圖影像的時間區段。
1. 在視訊的右側，選取&#x200B;**[!UICONTROL 內容]**&#x200B;索引標籤。
1. 在「內容」標籤下，選取&#x200B;**[!UICONTROL 選取Assets]**，然後瀏覽並選取您要與視訊搭配使用的所有影像資產。 選取的資產會新增至「內容」標籤中的「資產選擇器」面板。

1. 在「內容」標籤下方的資產選取器中，執行下列任一項作業：

   <table>
      <tbody>
        <tr>
        <td>若要將縮圖與所選時間軸區段相關聯</td>
        <td><p>在右側的資產選擇器面板中選取影像。</p> <p>您可以對時間軸區段新增任意數量的縮圖。 對於您選取的每個影像，資產選取器中的影像上方都會顯示勾號。</p> </td>
        </tr>
        <tr>
        <td>若要從選取的時間表區段移除縮圖</td>
        <td><p>執行下列任一項作業：</p>
          <ul>
          <li>在資產選擇器面板中，選取帶有勾號的影像以取消選取。 影像資產已從時間軸區段中移除。<br /> </li>
          <li>在選取的時間表區段中，選取影像，然後在工具列上選取<strong>刪除產品</strong>。</li>
          </ul> </td>
        </tr>
      </tbody>
    </table>

   ![資產選取器](assets/chlimage_1-133.png)

   在資產選擇器面板中選取影像，可將其新增至所選的時間軸區段。

1. 選取其中一個時間表區段內的單一縮圖影像，然後選取「**[!UICONTROL 動作]**」標籤。
1. 執行下列任一項作業：
   <table> 
    <tbody> 
      <tr> 
      <td>若要將選取的縮圖影像與快速檢視產生關聯</td> 
      <td><p>在動作型別下，選取<strong>快速檢視</strong>。</p> <p>如果您是Experience Manager Sites和電子商務客戶：</p> 
       <ul> 
       <li>請注意，「SKU值」文字欄位已預先填入選取產品的SKU （庫存單位），這是您提供的每個不同產品或服務的唯一識別碼。 當影像與Experience Manager Commerce中的產品相關聯時，會自動填入此值。</li> 
       <li>如果預先填入的SKU不正確，請選取「產品挑選器」圖示（放大鏡）以開啟「選取產品」頁面。 選取您要使用的產品，然後選取頁面右上角的核取記號，即可返回互動式視訊編輯器。</li> 
       </ul> <p> 如果您<em>不是</em> Experience Manager Sites或電子商務客戶</p> 
       <ul> 
       <li>請參閱<a href="/help/assets/carousel-banners.md#identifying-hotspot-and-image-map-variables">識別熱點變數</a>。 必須定義變數。  </li> 
       <li>依預設，此SKU欄位會使用影像資產的檔案名稱，但不含副檔名。 如果您根據SKU遵循檔案的標準命名慣例，則此檔案名稱通常不需要任何其他編輯。 </li> 
       <li>否則，請編輯預設值並輸入正確的SKU值。 在「SKU值」文字欄位中，輸入產品的SKU （庫存單位），這是您提供的每個不同產品或服務的唯一識別碼。 輸入的SKU值會自動填入「快速檢視」範本的變數部分，讓系統知道要將選取的影像與特定SKU的「快速檢視」建立關聯。</li> 
       </ul> <p>（選擇性）如果快速檢視中有其他變數您必須用來進一步識別產品，請選取<strong>新增一般變數</strong>。 在文字欄位中，指定額外的變數。 例如，<code>category=Womens</code>是新增的變數。</p> <p> </p> </td> 
      </tr> 
      <tr> 
      <td>若要將選取的縮圖影像與超連結產生關聯</td> 
      <td><p>在「動作型別」下，選取<strong>超連結</strong>，然後執行下列任一項作業：</p> 
       <ul> 
       <li>如果您是Experience Manager Sites客戶，請選取「網站選擇器」圖示（資料夾）以導覽至網頁。 如果您的互動式內容有具有相對URL的連結，尤其是指向Experience Manager Sites頁面的連結，則無法採用URL型連結方法。</li> 
       <li>如果您是獨立Dynamic Media客戶，請在HREF文字欄位中指定連結網頁的完整URL路徑。</li> 
       </ul> <p>請務必指定是在新的瀏覽器分頁中還是在目前的分頁中開啟連結。</p> </td> 
      </tr> 
      <tr> 
      <td>若要將選取的縮圖影像與體驗片段建立關聯</td> 
      <td><p>在「動作型別」下，選取<strong>體驗片段</strong>，然後執行下列動作：<p> 
       <ul> 
       <li>如果您是Experience Manager Sites客戶，請選取「搜尋」圖示（放大鏡）以開啟「體驗片段」頁面。 選取您要使用的體驗片段，然後選取頁面右上角的<strong>選取「</strong>」，以便您可以返回上一頁的「動作」面板。<br />檢視<a href="/help/sites-authoring/experience-fragments.md">體驗片段</a>。</li> 
      </ul> 
       <ul> 
       <li>指定您要在影片中顯示的體驗片段寬度和高度。</li>
       </ul><strong>注意</strong>：當您將檢視器內嵌在體驗片段中時，不支援互動式視訊中的社群媒體分享工具。 若要解決此問題，您可以使用或建立沒有社群媒體分享工具的檢視器預設集。 這類檢視器預設集可讓您成功將其嵌入體驗片段中。</p></tr>&lt; 
      <tr> 
      <td>若要編輯已指派給縮圖影像的動作</td> 
      <td>在時間軸區段中，選取文字標籤右側具有鏈結連結的縮圖影像。 鏈結連結表示已為其指定動作。 選取<strong>動作</strong>標籤，以便您進行變更。</td> 
      </tr> 
      <tr> 
      <td>若要變更縮圖影像的文字標籤</td> 
      <td><p>依預設，文字標籤會使用縮圖影像的<code>Title</code>中繼資料欄位。 如果<code>Title</code>不存在，則會改用縮圖影像的檔案名稱，但不加上副檔名。</p> <p>若要變更縮圖影像的文字標籤，請在<strong>動作</strong>標籤下，直接在顯示的影像資產下方，輸入所要的文字。 請參閱下方的熒幕擷圖。</p> <p>新文字標籤僅供視訊播放器本身及時間軸區段中顯示的縮圖文字使用。 標籤變更不會影響縮圖影像的「標題」中繼資料欄位及其檔案名稱。</p> </td> 
      </tr> 
      <tr> 
      <td>還原變更：</td> 
      <td>在頁面的右上角附近，選取<strong>復原</strong>或<strong>取消復原</strong>。</td> 
      </tr> 
    </tbody> 
   </table>

   ![experiencefragment_interactivevideos](assets/experiencefragment_interactivevideos.png)

   新的文字標籤會新增至縮圖影像。

1. 執行下列任一項作業：

   * 重複步驟6至11，在視訊中的時間軸區段新增更多縮圖影像。
   * 繼續至可選步驟13。

1. （可選）執行下列任一項作業：

   * **[!UICONTROL 合併區段]** — 您可以將兩個相鄰的區段（無論是否指派了產品縮圖）合併為一個區段。

     在時間軸上，選取要合併成兩個或多個連續區段的區段。 下方熒幕擷圖中的兩個選取區段沒有藍色橢圓形拖曳控點。

     在工具列上選取&#x200B;**[!UICONTROL 合併區段]**。

   ![chlimage_1-134](assets/chlimage_1-134.png)

   將兩個選取的5秒區段合併為1個10秒區段。

   * **[!UICONTROL 分割區段]** — 您可以將單一區段分割成兩個相等的時間區段。 如果已有產品縮圖指派給區段，則縮圖會合併至左側區段。

     在時間軸上，選取您要分成兩半的區段，然後在工具列上選取&#x200B;**[!UICONTROL 分割區段]**。

     選取兩個或多個區段會停用&#x200B;**[!UICONTROL 分割區段]**&#x200B;功能。

   ![chlimage_1-135](assets/chlimage_1-135.png)

   將選取的十秒區段分割為兩個區段，每個區段五秒。

1. 在&#x200B;**[!UICONTROL 建立互動式視訊]**&#x200B;頁面的右上角附近，會顯示目前與視訊搭配使用的選取檢視器預設集名稱。 如果要選取不同的檢視器預設集，請選取名稱。

   例如，`Shoppable_Video_light`檢視器預設集可讓您播放視訊，並在視訊旁邊顯示白色區域。 顯示區域是播放期間顯示可選取縮圖影像的位置。 `Shoppable_Video_dark`檢視器預設集可讓您播放視訊，且視訊旁邊會顯示黑色區域。

   如果您建立了自己的互動式視訊檢視器預設集，您會在可供您選擇的預設集清單中看到該預設集。

   完成時，選取&#x200B;**[!UICONTROL 儲存]**。

   >[!NOTE]
   >
   >當您儲存互動式視訊時，會自動 `.vtt` 儲存相關的檔案。`.vtt`檔案已儲存至`_VTT`Assets **[!UICONTROL 根目錄的]**&#x200B;資料夾。 您的互動式視訊必須有檔案和資料夾才能在網站上正確播放。因此，請勿移動、編輯或刪除資料夾 `_VTT` 或其內容。

1. 發佈互動式視訊。 發佈作業會建立內嵌程式碼或URL，您最後會將其複製並貼到您的網站體驗中。

   如果您新增與「快速檢視」的互動，則只能使用內嵌程式碼；如果您新增與超連結網頁的互動，則也可以使用已發佈的URL。 但請注意，如果您的互動式內容有具有相對URL的連結，尤其是指向Experience Manager Sites頁面的連結，則無法採用URL型連結方法。

   請參閱[發佈資產](publishing-dynamicmedia-assets.md)。

   >[!NOTE]
   >
   >若要使用Quickview發佈可購物影片，請務必另外從商務區域發佈影片的相關影像資產。

   新增時間軸區段並發佈互動式視訊後，您就可以將其新增至您現有的網站登陸頁面。 請參閱[將互動式視訊與您的網站整合](#integrating-an-interactive-video-with-your-website)。

## 發佈互動式視訊資產 {#publishing-interactive-video-assets}

如需如何發佈互動式視訊資產的詳細資訊，請參閱[發佈資產](/help/assets/publishing-dynamicmedia-assets.md)。

## 將互動式視訊與您的網站整合 {#integrating-an-interactive-video-with-your-website}

上傳影片、新增時間軸區段及發佈互動式影片後，您現在就能將其新增至現有網站。

如果您是Experience Manager Sites客戶，可以將互動式媒體元件拖曳至頁面，以新增互動式視訊。 請參閱[將Dynamic Media資產新增至頁面](/help/assets/adding-dynamic-media-assets-to-pages.md)。

如果您是獨立Experience Manager Assets客戶，可以手動將互動式視訊新增至您的網站，如本節所述。

1. 複製已發佈互動式視訊的內嵌程式碼或URL。
請參閱[將視訊或影像檢視器嵌入網頁](/help/assets/embed-code.md)。
如果您新增與「快速檢視」的互動，則只能使用內嵌程式碼；如果您新增與超連結網頁的互動，則也可以使用已發佈的URL。 但請注意，如果您的互動式內容有具有相對URL的連結，尤其是指向Experience Manager Sites頁面的連結，則無法採用URL型連結方法。

1. 在目標之網頁程式碼中，識別靜態視訊的位置。
1. 移除靜態視訊，並以您從Experience Manager Assets複製的內嵌程式碼或URL取代程式碼（依現狀）。
複製的內嵌程式碼是針對回應式環境所設定，因此會自動符合先前由靜態視訊佔用的區域。

>[!NOTE]
>
>此時，如果您只新增超連結網頁的互動功能，也就完成了。
>
>不過，如果您新增任何互動來觸發快速檢視，互動視訊旁的縮圖僅供顯示，尚未與您現有的快速檢視整合。 在這種情況下，您必須將互動式視訊與網站上的現有快速檢視整合。

**範例**

以示範網站為例：

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html?lang=zh-Hant](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html?lang=zh-Hant)

請注意，內嵌程式碼為標準版：

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

整合就像移除視訊內嵌程式碼，並從Experience Manager將其取代為互動式視訊內嵌程式碼一樣簡單。 您可以在以下URL看到結果。 雖然它會顯示頁面上顯示的互動式視訊，但尚未與現有的快速檢視整合：

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-1.html?lang=zh-Hant](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-1.html?lang=zh-Hant)

## 將互動式視訊與現有的Quickview整合 {#integrating-an-interactive-video-with-an-existing-quickview}

>[!NOTE]
>
>此工作僅適用於獨立Experience Manager Assets客戶。

此程式的最後一步是將互動式視訊與網站上使用的現有Quickview實作整合。 整合沒有適用於所有情況的解決方案。 每個快速檢視實施都是獨一無二的。 因此，需要涉及前端IT人員協助的特定方法。

現有的快速檢視實施通常代表一連串在網頁上發生的相互關聯動作，其順序如下：

1. 使用者會在您網站的使用者介面中觸發元素。
1. 前端程式碼會根據步驟1所觸發的使用者介面元素來取得快速檢視URL。
1. 前端程式碼會使用步驟2中取得的URL傳送AJAX要求。
1. 後端邏輯會將對應的快速檢視資料或內容傳回前端程式碼。
1. 前端程式碼會載入快速檢視資料或內容。
1. 前端程式碼可選擇性將載入的Quickview資料轉換為HTML表示法。
1. 前端程式碼會顯示模型對話方塊或面板，並在畫面上為一般使用者呈現HTML內容。

這些呼叫不代表網頁邏輯可從任意步驟呼叫的獨立公用API呼叫。 相反地，這是一種鏈結呼叫，下個步驟的每一個都會隱藏在上一個步驟的最後一個階段（回撥）。

在互動視訊取代步驟1和部分步驟2的同時，當使用者在互動視訊內的縮圖上選取時，這類使用者互動由檢視器處理。 檢視器會將事件傳回至包含先前新增至Experience Manager之所有縮圖資料的網頁。

在此類事件處理常式中，前端程式碼會執行下列動作：

* 聆聽互動式視訊所發出的事件。
* 根據縮圖資料建構快速檢視URL。
* 觸發從後端載入快速檢視並在畫面上呈現以供顯示的程式。

此外，互動式視訊檢視器支援全熒幕操作模式。 一般使用者透過選擇縮圖而不離開全熒幕來觸發Quickview。 若要實現此功能，請修改前端程式碼，以便將「快速檢視」強制回應對話方塊附加至檢視器的容器。 請勿新增當檢視器處於全熒幕模式時無法使用的檔案BODY或其他網頁元素。 執行此工作的程式碼必須監聽一或多個檢視器回呼，這些回呼會在載入頁面上的檢視器之後傳送。

Experience Manager傳回的內嵌程式碼已備有立即可用的事件處理常式。 如下列醒目提示的程式碼片段所示，系統會將它標籤為已註解：

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
    //See your quickviewer plugin for the quickview call
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

因此，只需取消註解上述醒目提示的程式碼片段，並將虛擬處理常式本文取代為特定網頁的專屬程式碼。

標準內嵌程式碼中存在兩個預設的回呼處理常式： `quickViewActivate`和`initComplete`。 在檢視器中選取縮圖時，就會觸發`quickViewActivate`處理常式。 使用它來整合檢視器與Quickview啟用邏輯。 檢視器載入頁面時，`initComplete`處理常式只會觸發一次。 此處理常式可用來調整快速檢視對話方塊在網頁DOM中的位置。

建構快速檢視URL的程式與識別本主題先前所述縮圖變數的程式相反。 使用先前識別的快速檢視URL範例，您可以檢視快速檢視URL在各種情況下的建構方式：

<table>
  <tbody>
  <tr>
    <td><p>在查詢字串中找到單一SKU</p> </td>
    <td><code class="code">s7interactivevideoviewer.setHandlers(&lbrace;
      "quickViewActivate": function(inData) &lbrace;
      var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;source=100";
      &rbrace;,
      &rbrace;);</code></td>
  </tr>
  <tr>
    <td>在URL路徑中找到單一SKU</td>
    <td><code class="code">s7interactivevideoviewer.setHandlers(&lbrace;
      "quickViewActivate": function(inData) &lbrace;
      var quickViewUrl = "https://server/product/" + inData.sku;
      &rbrace;,
      &rbrace;);</code></td>
  </tr>
  <tr>
    <td><p>查詢字串中的SKU和類別ID</p> </td>
    <td><code class="code">s7interactivevideoviewer.setHandlers(&lbrace;
      "quickViewActivate": function(inData) &lbrace;
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;prodId=" + inData.sku;
      &rbrace;,
      &rbrace;);</code></td>
  </tr>
  </tbody>
</table>

觸發「快速檢視」URL及啟動「快速檢視」面板的最後一個步驟，極有可能需要您IT部門的前端IT人員協助。 他們最瞭解如何透過適當的步驟準確觸發Quickview實施，並擁有現成的Quickview URL。

您可以檢視這些步驟如何套用至示範網站，以將互動式視訊與快速檢視程式碼完全整合。 在本主題的前面，快速檢視URL的結構識別如下：

```xml
/datafeed/$CategoryId$-$SKU$.json
```

透過檢視器的程式碼，使用傳遞至處理常式的`quickViewActivate`物件中的`categoryId`和`sku`欄位，在`inData`處理常式中很容易重新建構此URL，如下所示：

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

示範網站正在使用簡單的`loadQuickView()`函式呼叫觸發Quickview對話方塊。 此函式僅接受一個引數，即快速檢視資料URL。 因此，整合互動式視訊的最後一步是將下列程式碼行新增到`quickViewActivate`處理常式：

```xml
loadQuickView(quickViewUrl);
```

最後，請確定您的「快速檢視」對話方塊已附加至檢視器的容器元素。 內嵌程式碼提供實現此功能的範例步驟。 若要取得檢視器容器元素的參考，您可以使用下列幾行程式碼：

```xml
var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
var inner_container = document.getElementById(sdkContainerId);
```

其中`inner_container`是檢視器所管理的`DIV`專案的參考。 您希望對話方塊成為該`DIV`的子項。

實際找到模型對話方塊元素並將其附加至上述容器的步驟會根據大小寫而定。 同樣地，您可以向熟悉您所需快速檢視實作的前端開發人員尋求協助。

如果您使用範例網站，快速檢視強制回應對話方塊會實作為`DIV`，且快速檢視強制回應ID會直接附加至檔案`BODY`。 因此，將該對話方塊移至檢視器容器的程式碼會直接顯示如下：

```xml
var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
var inner_container = document.getElementById(sdkContainerId);
inner_container.appendChild(document.getElementById("quickview-modal"));
```

完整的原始程式碼如下：

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

具備完全整合互動式視訊的最終示範網站看起來如下所示：

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-3.html?lang=zh-Hant](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-3.html?lang=zh-Hant)

## 使用 Quickview 建立自訂快顯視窗 {#using-quickviews-to-create-custom-pop-ups}

請參閱[使用Quickview](/help/assets/custom-pop-ups.md)建立自訂快顯視窗。
