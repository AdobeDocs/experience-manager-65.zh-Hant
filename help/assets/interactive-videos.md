---
title: 互動式影片
description: 瞭解如何在Dynamic Media使用互動式視頻和可購物視頻
uuid: c3ff6839-fff5-4709-8163-5c4245b80e6d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 04be55f2-c7d8-45ef-89e5-58856b971de5
docset: aem65
feature: Interactive Videos
role: User, Admin
exl-id: d118879d-c17b-43f3-9cc8-0405531b4d9f
source-git-commit: 9052ed3e89fdc67d94fc60bbff64d42255565767
workflow-type: tm+mt
source-wordcount: '6036'
ht-degree: 3%

---

# 互動式視頻{#interactive-videos}

您可以輕鬆建立互動式視頻（也稱為可購物視頻），直接驅動視頻的轉換。 客戶對視頻的參與發生在視頻播放器旁邊的一個面板中，在該面板中，根據視頻中的內容滾動查看相關服務、資訊或產品縮略圖。 客戶可以選擇縮略圖並直接連結到服務，或將項目添加到購物車以便立即購買，或連結到網頁以獲取詳細資訊。

當視頻結束時，顯示所有產品的可視摘要以驅動對操作的調用。 客戶有另一個機會選擇他們想要的物料。 可操作且具體的經驗（如這些經驗）可增加客戶的約定和轉換。

另請參閱 [互動式影像](/help/assets/interactive-images.md)。

## 互動式視頻正在執行 {#interactive-video-in-action}

要查看互動式、可購物視頻的操作，請選擇 [現場演示](https://landing.adobe.com/tw/na/dynamic-media/ctir-2755/live-demos.html)，滾動到 **[!UICONTROL 可購物媒體]** 標題，然後選擇可購物視頻。

* 在回放期間，當視頻中使用產品時，相同的產品會以縮覽圖影像顯示在右側。

* 如果要暫停視頻並開啟產品的Quickview，請選擇縮略圖。 例如，選擇視頻中的KitchenAid縮覽圖影像以體驗混音器的360度旋轉視圖，或放大以查看混音器詳細資訊。

<!-- There was a link here that showed the video frame of an interactive video and when the reader selected the frame the video would play https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/AXIS/index.html. This now needs to call a new interactive video-->

![來自互動式可購物視頻的幀](assets/chlimage_1-126.png) *從互動式可購買視頻中捕獲視頻幀。*

>[!NOTE]
>
>如果在用戶選擇縮略圖時建立互動式視頻以啟動網頁，則某些設備會阻止彈出式網頁開啟。 在這種情況下，必須更改設備上的彈出窗口阻止程式設定。 例如，在AppleiPhone6上，導航至 **[!UICONTROL 設定]** > **薩法里** > **阻止彈出窗口**，然後將控制項滑到 **[!UICONTROL 關閉]**。 現在，當您播放互動式視頻並選擇縮略圖時，如果要開啟彈出窗口，系統會提示您。 如果接受，則會開啟網頁。

### 觀看如何建立互動式視頻 {#watch-how-interactive-videos-are-created}

在上播放漫步 [如何建立互動式視頻](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveVideo) （7分30秒）。
儘管視頻漫遊的品牌是Assets on Demand ，但這些原則和步驟仍然適用於Adobe Experience Manager資產的Interactive Video。

### Adobe客戶解決方案網路研討會 {#adobe-customer-success-webinar}

「在Experience Manager Assets使用互動式視頻、連結共用和YouTube共用」網路研討會教您如何使用互動式視頻和其他功能將轉換驅動事件與視頻營銷內容聯繫起來。

>[!NOTE]
>
>[在Experience Manager Assets使用互動式視頻、連結共用和YouTube共用](https://adobecustomersuccess.adobeconnect.com/p1yxzdo4aec/)。

## 快速啟動：互動式視頻 {#quick-start-interactive-videos}

下面的逐步工作流說明旨在幫助您快速啟動並運行Dynamic Media的互動式視頻。

查找 **示例** 標題。 它包含一個基於此啟動演示網頁的簡要教程 *不* 已添加交互功能：

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html)

範例 **可協助您說明** ，如何將互動式視訊整合在您自己的網站上。

在上一個示例部分中完成本教程後，使用完全整合的互動式視頻的最終演示網頁如下所示：

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-3.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-3.html)

互動式視頻步驟：

1. **（可選）標識Quickview變數**  — 首先確定現有Quickview實現所使用的動態變數。 建立互動式視頻時，可以使用變數將產品縮略圖映射到其相應的產品Quickview。 請參閱 [（可選）標識Quickview變數](#optional-identifying-quickview-variables)。
   *只有在以下所有情況均為真時，才需要此步驟*:
   * 要通過觸發到Quickview來向視頻添加交互性。
   * 您實施Experience Manager *不* 使用電子商務整合框架將產品資料從任何電子商務解決方案(如IBM® WebSphere® Commerce、Elastic Path、Hybris或Intershop)中拉入Experience Manager。 請參閱 [Experience Manager Assets電子商務概念](/help/commerce/cif-classic/administering/concepts.md)。

1. **（可選）建立互動式視頻查看器預設**  — 自定義構成播放器的各種元件（如視頻掃描器和互動式縮略圖）的外觀和行為。
如果要使用現成的互動式視頻查看器預設，則不需要建立您自己的互動式視頻查看器預設 `Shoppable_Video_Light` 或 `Shoppable_Video_Dark` 的雙曲餘切值。
請參閱 [建立查看器預設](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset) （可選）和 [建立互動式查看器預設的特殊注意事項](/help/assets/managing-viewer-presets.md#special-considerations-for-creating-an-interactive-viewer-preset)。

1. **上載視頻及其關聯的影像資產**  — 上載要進行交互的視頻和關聯影像。
請參閱 [上載視頻及其關聯的縮略圖資產](#uploading-a-video-and-its-associated-thumbnail-assets)。

   >[!NOTE]
   >
   >MXF視頻格式尚不支援用於Dynamic Media的互動式視頻。

1. **向視頻添加交互性**  — 向視頻添加一個或多個時間段。 然後，將這些時間段內的影像縮略圖關聯起來。 將每個影像縮略圖分配給超連結、Quickview或體驗片段等操作。
(如果您的交互內容具有與相對URL的連結，特別是與Experience Manager Sites頁面的連結，則無法使用基於URL的連結方法。)
最後發佈互動式視頻資產。 發佈會建立最終複製並應用於網站登錄頁的嵌入代碼或URL。 請參閱 [向視頻添加交互性](#adding-interactivity-to-your-video)。
請參閱 [發佈資產](/help/assets/publishing-dynamicmedia-assets.md)。

1. **將互動式視頻添加到您的網站或以Experience Manager形式添加到您的網站**  — 如果您使用Experience Manager Sites或電子商務，或同時使用兩者，則可以將互動式視頻添加到網頁。 將互動式媒體元件拖到頁面上，使用Experience Manager。 請參閱 [將Dynamic Media資產添加到頁面](/help/assets/adding-dynamic-media-assets-to-pages.md)。
使用嵌入代碼或URL將互動式視頻與您的網站體驗整合。 請參閱 [將互動式視頻與您的網站整合](#integrating-an-interactive-video-with-your-website)。
如果您使用第三方WCM（Web內容管理器），則必須將新的互動式視頻與網站上使用的現有Quickview實現整合。 請參閱 [將互動式視頻與現有Quickview整合](#integrating-an-interactive-video-with-an-existing-quickview)。
   [將Dynamic Media資產添加到頁面](/help/assets/adding-dynamic-media-assets-to-pages.md)

## （可選）標識Quickview變數 {#optional-identifying-quickview-variables}

>[!NOTE]
>
>僅當以下情況為真時，才需要此任務：
>
>* 要通過觸發到Quickview來向視頻添加交互性。
>* 您實施Experience Manager *不* 使用電子商務整合框架將產品資料從任何電子商務解決方案(如IBM® WebSphere® Commerce、Elastic Path、Hybris或Intershop)中拉入Experience Manager。 請參閱 [Experience Manager Assets電子商務概念](/help/commerce/cif-classic/administering/concepts.md)。
>
如果您的Experience Manager實施使用電子商務，則可以跳過此任務並繼續執行下一個任務。

首先確定現有Quickview實現所使用的動態變數，以便在互動式視頻建立過程中將產品縮略圖映射到其相應的產品Quickview。

在向視頻添加時段時，您會為添加到段的每個縮略圖分配SKU（庫存保管單位）和任何附加變數。 這些變數稍後用於顯示正確的Quickview產品。

正確確定唯一觸發產品Quickview所需的變數非常重要。

有時，與負責您現有Quickview實施的IT專家進行咨詢就足夠了。 他們可能知道系統中標識Quickview的最小資料集。 但是，也可以簡單地分析前端代碼的現有行為。

大多數Quickview實現都使用以下範例：

* 使用者在網站上啟動使用者介面元素。例如，選擇「快速視圖」按鈕。
* 如果需要，網站會向後端發送Ajax請求以載入Quickview資料或內容。
* Quickview資料被翻譯成內容以準備在網頁上呈現。
* 最後，前端代碼在螢幕上直觀地呈現這些內容。

因此，方法是訪問現有網站中實現Quickview的不同區域，觸發Quickview，並捕獲網頁發送的Ajax URL，以載入Quickview資料或內容。

通常，您不需要使用任何專用的調試工具。 現代Web瀏覽器具有能夠完成充分工作的Web檢查器。 以下是包括Web檢查器的Web瀏覽器的幾個示例：

* 要查看GoogleChrome中的所有傳出HTTP請求，請按 **F12** (Windows)或 **命令+選項+I** (Mac)開啟「開發人員工具」面板，然後選擇 **網路** 頁籤。

* 在Firefox中，您可以通過按 **F12** (Windows)或 **命令+選項+I** (Mac)及使用 **`[Net]`** 頁籤，或者可以使用內置的「檢查器」工具及其「網路」頁籤。

* 在Internet Explorer中，通過按 **F12**。

在瀏覽器中開啟網路監視時，在頁面上觸發Quickview。

現在，在網路日誌中查找Quickview Ajax URL，並複製記錄的URL以供將來分析。 通常，在觸發Quickview時，會向伺服器發送大量請求。 通常，Quickview Ajax URL是清單中的第一個URL之一。 它具有複雜的查詢字串部分或路徑，其響應MIME類型為 `text/html`。 `text/xml`或 `text/javascript`。

在此過程中，訪問您網站的不同區域、不同的產品類別和類型非常重要。 原因是，Quickview URL可以包含指定網站類別的公用部件，但僅當訪問網站的其他區域時才會更改。

在最簡單的情況下，Quickview URL中唯一的變數部分是產品SKU。 在這種情況下，產品SKU值是將縮略圖添加到互動式視頻Experience Manager中的時段所需的唯一資料段。

但是，在複雜情況下，Quickview URL除了產品SKU之外還有不同的元素，如類別ID、顏色代碼和大小代碼。 在這種情況下，每個此類元素都變成Experience Manager中縮略圖資料定義中的一個單獨變數。

請考慮以下Quickview URL及其生成的縮略圖變數示例：

<table>
  <tbody>
  <tr>
    <td><p>在查詢字串中找到的單個SKU。</p> </td>
    <td><p>錄制的Quickview URL包括以下內容：</p>
    <ul>
      <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>URL中唯一的變數部分是 <code>productId=</code> 查詢字串參數，它顯然是SKU值。 因此，縮略圖只需使用SKU欄位填充值，如 <strong><code>866558</code></strong>。 <strong><code>1196184</code></strong>。 <strong><code>1081492</code></strong>。 <strong><code>1898294</code></strong>。</p> </td>
  </tr>
  <tr>
    <td><p>單SKU，在URL路徑中找到。</p> </td>
    <td><p>錄制的Quickview URL包括以下內容：</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>變數部分位於路徑的最後一部分，它成為Experience Manager縮略圖的SKU值： <strong><code>6422350843</code></strong>。 <strong><code>1607745002</code></strong>。 <strong><code>0086724882</code></strong>。</p> </td>
  </tr>
  <tr>
    <td><p>查詢字串中的SKU和類別ID。</p> </td>
    <td><p>錄制的Quickview URL包括以下內容：</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>在這種情況下，URL中有兩個不同的部分。 SKU儲存在 <code>prodId</code> 參數和類別ID儲存在 <code>category=</code> 的下界。</p> <p>因此，縮略圖定義是對。 即，SKU值和一個稱為 <code>categoryId</code>。 結果對如下：</p>
    <ul>
      <li>SKU是 <code>305466</code> 和 <code>categoryId</code> 是 <code>1100004</code></li>
      <li>SKU是 <code>310181</code> 和 <code>categoryId</code> 是 <code>1100004</code></li>
      <li>SKU是 <code>308706</code> 和 <code>categoryId</code> 是 <code>1740148</code></li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**範例**

將上述方法應用到「示例」網站時，您的網頁中包含多個產品縮略圖，每個產品縮略圖都有一個「查看更多」按鈕：

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html)

激活該頁上所有可用的產品Quickview後，您將獲得向後端發出的以下Quickview請求清單：

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

查看伺服器呼叫時，您會看到特定於產品的資訊僅存在於請求路徑中。 您還注意到查詢字串根本未使用，並且涉及兩種不同類型的資料段：

* 第一種是蠟燭，墊子，家具，玻璃器皿。 您可以將此稱為「產品類別」。
* 第二類是產品代碼，如233916597。 您可以假設它是「產品SKU」。

根據此資訊，整個Quickview URL具有以下模式：

`/datafeed/$categoryId$-$SKU$.json`

基於此類分析，您得出的結論是，您可以為縮略圖使用以下兩個變數： `categoryId` 和 `SKU`。

您現在可以上傳視頻及其關聯的縮略圖資產。

## （可選）建立互動式視頻查看器預設 {#optional-creating-an-interactive-video-viewer-preset}

如果要使用預設的開箱即用Interactive Video Viewer預設類型之一，則可以跳過此任務並繼續下一步 `Shoppable_Video_dark` 或 `Shoppable_Video_light`。

在創作環境中選擇縮覽圖時，將顯示「快速視圖」(Quickview)對話框的預覽。

![chlimage_1-21](assets/chlimage_1-127.png)

您可以選擇建立自己的自定義互動式視頻查看器預設。 除其他外，您可以確定視頻播放器的樣式、互動式縮略圖和顯示在視頻末尾的縮略圖網格視圖。

互動式視頻查看器預設可正確呈現您添加的視頻和所有時間軸段。 在「預覽」模式下選擇產品縮略圖時，它還使用一個預設的Quickview示例，以便您可以在發佈前test其交互性。

保存查看器預設後，其狀態將自動設定為 **開** 的下界。 此狀態表示在動態媒體元件中及您使用它預覽視訊時，都可看到它。請確定您也手動發佈新的檢視器預設集。

請參閱 [建立新查看器預設](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset) 建立您自己的Interactive Video查看器預設。

## 上載視頻及其關聯的縮略圖資產 {#uploading-a-video-and-its-associated-thumbnail-assets}

如果您已上傳視頻和縮略圖資產，請繼續 [向視頻添加交互性](#adding-interactivity-to-your-video)。

>[!NOTE]
MXF視頻格式尚不支援用於Dynamic Media的互動式視頻。

如果上載了錯誤的視頻或影像，或者要刪除已上傳的不再需要的視頻或影像，請參閱 [刪除資產](/help/assets/manage-assets.md#deleting-assets)。

要上載視頻及其關聯的縮略圖資產，請執行以下操作：

1. 將視頻和關聯的縮略圖資產上載到所需資料夾或資料夾。

   請參閱 [上載資產](/help/assets/manage-assets.md)。
請參閱 [使用FTP作業計畫上載資產](/help/assets/manage-assets.md)。

   現在將交互性添加到視頻中。

## 向視頻添加交互性 {#adding-interactivity-to-your-video}

使用「建立互動式視頻」頁上的就地可視編輯器將時間線段添加到視頻。

添加時間線段後，可在每個段內添加縮略圖。 對於您添加的每個縮覽圖，都應用一個操作。 例如，您可以將Quickview應用於縮略圖，也可以為縮略圖分配超連結或體驗片段。

請參閱 [體驗片段](/help/sites-authoring/experience-fragments.md)。

>[!NOTE]
當您將查看器嵌入體驗片段時，不支援互動式視頻中的社交媒體共用工具。 要解決此問題，可以使用或建立沒有社交媒體共用工具的查看器預設。 這樣的查看器預設使您能夠成功將其嵌入「體驗片段」中。

>[!NOTE]
如果您的交互內容具有與相對URL的連結，特別是與Experience Manager Sites頁面的連結，則無法使用基於URL的連結方法。

在當前建立/編輯會話期間，支援在頁面右上角附近的「撤消」和「重做」選項。

保存互動式視頻後，該視頻會立即開啟到「預覽」中。 從中，您可以選擇互動式視頻查看器預設並播放視頻，以查看其對客戶的顯示方式的近似表示。

**向視頻添加交互性：**

1. 在「資產」視圖中，導航到您上載並要進行交互的視頻。
1. 執行下列任一項作業：

   * 懸停在影像上，然後選擇 **[!UICONTROL 選擇]** （複選標籤表徵圖）。 在工具欄上，選擇 **[!UICONTROL 編輯]**。

   * 懸停在影像上，然後選擇 **[!UICONTROL 更多操作]** （三點表徵圖） **[!UICONTROL >編輯]**。

   * 選擇影像，以便可以在「詳細資訊視圖」頁中開啟該影像。 在工具欄上，選擇 **[!UICONTROL 編輯]**。

1. 在「建立互動式視頻」頁上，執行下列任一操作：

   * 要開始播放視頻，請選擇 **[!UICONTROL 播放]** 按鈕 當要突出顯示的特定產品、服務或詳細資訊進入視圖時，選擇 **[!UICONTROL 添加段]** 的上界。 重複，直到您到達視頻的結尾。

      對於您添加的每個時段，為其分配一個或多個縮略圖，然後將這些縮略圖連結到供客戶購買的Quickview產品頁面或網頁以瞭解詳細資訊。

   * 要開始播放視頻，請選擇 **[!UICONTROL 播放]** 按鈕 當要突出顯示的特定產品、服務或詳細資訊進入視圖時，選擇 **[!UICONTROL 暫停]**。 選擇 **[!UICONTROL 添加段]**。

      繼續播放並在要添加段的時間線上的點暫停視頻，直到視頻結束。

1. （可選）拖動 **[!UICONTROL 時間軸縮放滑塊]** 向左放大或向右放大，以便控制已添加的段的詳細程度。

   ![chlimage_1-22](assets/chlimage_1-128.png)

   根據視頻的長度，段持續時間預設為以下值：

   <table>
      <tbody>
        <tr>
        <td><strong>如果視頻長度為……</strong></td>
        <td><strong>「段持續時間」(Segment Duration)設定預設為……</strong></td>
        </tr>
        <tr>
        <td>3分鐘或更久</td>
        <td>60 秒</td>
        </tr>
        <tr>
        <td>2-3分鐘</td>
        <td>30 秒</td>
        </tr>
        <tr>
        <td>1-2 分鐘</td>
        <td>20秒<br /> </td>
        </tr>
        <tr>
        <td>30-60秒</td>
        <td>10 秒</td>
        </tr>
        <tr>
        <td>30秒或更少</td>
        <td>5 秒</td>
        </tr>
      </tbody>
    </table>

   視頻時間線使用的螢幕空間與可供其使用的空間一樣多。 因此，當您調整瀏覽器大小時，您添加的段會保持其正確的寬度。

   為了說明，以下三個螢幕截圖使用同一視頻。 請注意，每個段的寬度會根據時間軸比例設定而改變。

   ![chlimage_1-23](assets/chlimage_1-129.png)

   螢幕截圖A

   上面的螢幕截圖A顯示29秒產品視頻的預設視圖。 時間軸比例設定為預設的5秒。

   ![chlimage_1-130](assets/chlimage_1-130.png)

   螢幕截圖B

   在上面的螢幕截圖B中，時間軸縮放滑塊從預設的5秒拖到3秒。 請注意，現在所有時間軸縮放時間戳都以3秒間隔設定。

   ![chlimage_1-25](assets/chlimage_1-131.png)

   螢幕截圖C

   在上面的螢幕截圖C中，時間軸縮放設定被移動到8秒。 注意包含產品縮略圖的段是如何收縮的。 如果您有長視頻，並且希望能夠查看通常適合頁面寬度的更多段的概覽，則以此方式進行放大非常有用。

1. （可選）執行下列任一操作：

   * 調整段的開始時間和結束時間。

      選擇一個段，然後拖動前導或尾隨的藍色橢圓，分別調整開始或結束時間。 顯示的視頻幀會根據您的調整移動到視頻中的適當時間。 基於時間線中的任何相鄰段來限制時間線段的移動。 最小允許段時間為1秒。

      使用以下導航快捷方式快速檢查和微調視頻段：

      * 要直接查找視頻到該段的開頭，請選擇前導藍色橢圓。
      * 要直接查找視頻到該段的末尾，請選擇尾隨的藍色橢圓。
      * 要將視頻回放返回到該段的開頭，請選擇整個段。

   ![chlimage_1-26](assets/chlimage_1-132.png)

   重新定位時間線段的結尾

   * 刪除段

      選擇時間軸上的最後一個段，然後在工具欄上，選擇 **[!UICONTROL 刪除段]**。 如果選取了兩個或多個段，則「刪除段」(Delete Segment)特徵將被禁用。

      只能刪除最後一個段。 例如，如果要刪除時間軸上的所有段，則必須始終選擇最後一個段，然後選擇 **[!UICONTROL 刪除段]**。


1. 選擇要將一個或多個縮略圖與其關聯的時間段。
1. 在視頻的右側，選擇 **[!UICONTROL 內容]** 頁籤。
1. 在「內容」頁籤下，選擇 **[!UICONTROL 選擇資產]**，然後瀏覽並選擇要用於視頻的所有影像資產。 選定的資產將添加到「內容」頁籤的「資產選擇器」面板中。

1. 在「內容」頁籤下的資產選擇器中，執行下列任一操作：

   <table>
      <tbody>
        <tr>
        <td>將縮覽圖與所選時間軸段關聯</td>
        <td><p>在右側的資產選擇器面板中選擇影像。</p> <p>可以添加任意數量的縮略圖到時間軸段。 對於您選擇的每個影像，資產選擇器中的影像上會出現複選標籤。</p> </td>
        </tr>
        <tr>
        <td>從所選時間線段中刪除縮略圖</td>
        <td><p>執行下列任一操作：</p>
          <ul>
          <li>在資產選擇器面板中，選擇帶複選標籤的影像以取消選擇它。 從時間線段中刪除影像資源。<br /> </li>
          <li>在選定的時間軸段中，選擇影像，然後在工具欄上，選擇 <strong>刪除產品</strong>。</li>
          </ul> </td>
        </tr>
      </tbody>
    </table>

   ![資產選取器](assets/chlimage_1-133.png)

   在資產選擇器面板中選擇影像會將其添加到選定的時間軸段。

1. 在時間軸段之一中選擇單個縮略圖，然後選擇 **[!UICONTROL 操作]** 頁籤。
1. 執行下列任一操作：
   <table> 
    <tbody> 
      <tr> 
      <td>將所選縮略圖影像與Quickview關聯</td> 
      <td><p>在操作類型下，選擇 <strong>快速視圖</strong>。</p> <p>如果您是Experience Manager Sites和電子商務客戶：</p> 
       <ul> 
       <li>請注意，「SKU值」文本欄位已預先填入選定產品的SKU（庫存保管單位），該SKU是您所提供的每個不同產品或服務的唯一標識符。 當影像與Experience ManagerCommerce中的產品關聯時，會自動填充此值。</li> 
       <li>如果預填充的SKU不正確，請選擇「產品選取器」表徵圖（放大鏡）以開啟「選擇產品」頁。 選擇要使用的產品，然後選擇頁面右上角的複選標籤，以便您可以返回到互動式視頻編輯器。</li> 
       </ul> <p> 如果 <em>不</em> Experience Manager Sites或電子商務客戶</p> 
       <ul> 
       <li>請參閱 <a href="/help/assets/carousel-banners.md#identifying-hotspot-and-image-map-variables">識別熱點變數</a>。 必須定義變數。  </li> 
       <li>預設情況下，此SKU欄位使用影像資產的檔案名，而不使用副檔名。 如果您根據SKU對檔案遵循標準命名約定，則此檔案名通常不需要任何其他編輯。 </li> 
       <li>否則，編輯預設值並輸入正確的SKU值。 在「SKU值」文本欄位中，鍵入產品的SKU（庫存保管單位），該SKU是您提供的每個不同產品或服務的唯一標識符。 輸入的SKU值會自動填充Quickview模板的可變部分，以便系統知道將選定映像與特定SKU的Quickview相關聯。</li> 
       </ul> <p>（可選）如果Quickview中有其它變數必須用於進一步標識產品，請選擇 <strong>添加泛型變數</strong>。 在文本欄位中，指定一個額外變數。 比如說， <code>category=Womens</code> 是已添加的變數。</p> <p> </p> </td> 
      </tr> 
      <tr> 
      <td>將所選縮略圖影像與超連結關聯</td> 
      <td><p>在操作類型下，選擇 <strong>超連結</strong>，然後執行以下操作之一：</p> 
       <ul> 
       <li>如果您是Experience Manager Sites客戶，請選擇「站點選擇器」表徵圖（資料夾）以導航至網頁。 如果您的交互內容具有與相對URL的連結，特別是與Experience Manager Sites頁面的連結，則無法使用基於URL的連結方法。</li> 
       <li>如果您是獨立的Dynamic Media客戶，請在HREF文本欄位中指定連結網頁的完整URL路徑。</li> 
       </ul> <p>請確保指定是在新瀏覽器頁籤中還是在當前頁籤中開啟連結。</p> </td> 
      </tr> 
      <tr> 
      <td>將所選縮略圖影像與體驗片段關聯</td> 
      <td><p>在操作類型下，選擇 <strong>體驗片段</strong>，然後執行以下操作：<p> 
       <ul> 
       <li>如果您是Experience Manager Sites客戶，請選擇「搜索」表徵圖（放大鏡）以開啟「體驗片段」頁。 選擇要使用的體驗片段，然後選擇 <strong>選擇 </strong>在頁面的右上角，以便您可以返回到上一頁上的「操作」面板。<br /> 請參閱 <a href="/help/sites-authoring/experience-fragments.md">體驗片段</a>。</li> 
      </ul> 
       <ul> 
       <li>指定希望在視頻中顯示體驗片段的寬度和高度。</li>
       </ul><strong>注釋</strong>:當您將查看器嵌入體驗片段時，不支援互動式視頻中的社交媒體共用工具。 要解決此問題，可以使用或建立沒有社交媒體共用工具的查看器預設。 這樣的查看器預設使您能夠成功將其嵌入「體驗片段」中。</p></tr>&lt; 
      <tr> 
      <td>編輯已分配給縮略圖的操作</td> 
      <td>在時間軸段中，選擇一個縮略圖，該縮略圖具有其文本標籤右側的連結。 連結指示已為其分配操作。 選擇 <strong>操作</strong> 頁籤，以便您可以進行更改。</td> 
      </tr> 
      <tr> 
      <td>更改縮略圖的文本標籤</td> 
      <td><p>預設情況下，文本標籤使用縮略圖 <code>Title</code> 元資料欄位。 如果 <code>Title</code> 不存在，而是使用縮略圖的檔案名，但沒有副檔名。</p> <p>要更改縮覽圖影像的文本標籤，請在 <strong>操作 </strong>頁籤，輸入所需文本。 請參閱下面的螢幕截圖。</p> <p>新文本標籤僅由視頻播放器本身和顯示在時間軸段中的縮略圖文本使用。 標籤更改不會影響縮略影像的標題元資料欄位及其檔案名。</p> </td> 
      </tr> 
      <tr> 
      <td>還原更改：</td> 
      <td>在頁面右上角附近，選擇 <strong>撤消</strong> 或 <strong>重做</strong>。</td> 
      </tr> 
    </tbody> 
   </table>

   ![體驗fragment_interactivevideo](assets/experiencefragment_interactivevideos.png)

   新文本標籤將添加到縮略圖中。

1. 執行下列任一項作業：

   * 重複步驟6-11，將更多縮略圖添加到視頻中的時間軸段。
   * 繼續執行可選步驟13。

1. （可選）執行下列任一操作：

   * **[!UICONTROL 合併段]**  — 可以將兩個相鄰段（分配了或不分配了產品縮略圖）合併到一個段中。

      在時間軸上，選擇要合併為一個的兩個或多個連續段。 下面螢幕抓圖中的兩個選定段上沒有藍色橢圓拖動手柄。

      選擇 **[!UICONTROL 合併段]** 的上界。
   ![chlimage_1-134](assets/chlimage_1-134.png)

   將兩個選定的五秒段合併為一個十秒段。

   * **[!UICONTROL 拆分段]**  — 可以將單個段分為兩個同等時間的段。 如果已將產品縮略圖分配給該段，則縮略圖會合併到左段。

      在時間軸上，選擇要分成半段的段，然後選擇 **[!UICONTROL 拆分段]** 的上界。

      選擇兩個或更多段將禁用 **[!UICONTROL 拆分段]** 的子菜單。
   ![chlimage_1-135](assets/chlimage_1-135.png)

   將選定的10秒段分割為兩段，每段5秒。

1. 靠近 **[!UICONTROL 建立互動式視頻]** 頁面中，將顯示與視頻一起使用的當前選定查看器預設的名稱。 如果要選擇其他查看器預設，請選擇名稱。

   例如， `Shoppable_Video_light` 查看器預設允許您使用視頻旁邊的白色顯示區域播放視頻。 顯示區域是在回放期間顯示可選縮略圖的位置。 的 `Shoppable_Video_dark` 查看器預設允許您使用視頻旁邊的黑色顯示區域播放視頻。

   如果建立了您自己的Interactive Video Viewer預設，則可以在您可以選擇的預設清單中看到它。

   完成後，選擇 **[!UICONTROL 保存]**。

   >[!NOTE]
   當您儲存互動式視訊時，會自動 `.vtt` 儲存相關的檔案。的 `.vtt` 檔案保存到 `_VTT` 根資料夾 **[!UICONTROL 資產]**。 您的互動式視訊必須有檔案和資料夾才能在網站上正確播放。因此，請勿移動、編輯或刪除資料夾 `_VTT` 或其內容。

1. 發佈互動式視頻。 發佈會建立最終將其複製並貼上到網站體驗的嵌入代碼或URL。

   如果添加了與Quickview的交互，則只使用嵌入代碼；如果添加了與超連結網頁的交互，則還可以使用已發佈的URL。 但是，請注意，如果您的交互內容具有與相對URL(特別是與Experience Manager Sites頁面的連結)的連結，則不可能使用基於URL的連結方法。

   請參閱 [發佈資產](publishing-dynamicmedia-assets.md)。

   >[!NOTE]
   要使用Quickview發佈可購買的視頻，請確保您還從您的商業區域單獨發佈視頻的每個相關影像資產。

   添加時間線段並發佈互動式視頻後，您可以將其添加到現有網站登錄頁。 請參閱 [將互動式視頻與您的網站整合](#integrating-an-interactive-video-with-your-website)。

## 發佈互動式視頻資產 {#publishing-interactive-video-assets}

請參閱 [發佈資產](/help/assets/publishing-dynamicmedia-assets.md) 的子菜單。

## 將互動式視頻與您的網站整合 {#integrating-an-interactive-video-with-your-website}

上傳視頻、向其中添加時間線段並發佈互動式視頻後，您現在可以將其添加到現有網站。

如果您是Experience Manager Sites客戶，則可以通過將互動式媒體元件拖到頁面來添加互動式視頻。 請參閱 [將Dynamic Media資產添加到頁面](/help/assets/adding-dynamic-media-assets-to-pages.md)。

如果您是Experience Manager Assets的獨立客戶，則可以按本節所述手動將互動式視頻添加到您的網站。

1. 複製已發佈的互動式視頻的嵌入代碼或URL。
請參閱 [將視頻或影像查看器嵌入網頁](/help/assets/embed-code.md)。
如果添加了與Quickview的交互，則只使用嵌入代碼；如果添加了與超連結網頁的交互，則還可以使用已發佈的URL。 但是，請注意，如果您的交互內容具有與相對URL(特別是與Experience Manager Sites頁面的連結)的連結，則不可能使用基於URL的連結方法。

1. 在目標的網頁代碼中，標識靜態視頻的位置。
1. 刪除靜態視頻，並將代碼替換為您從Experience Manager Assets複製的嵌入代碼或URL。
複製的嵌入代碼被設定用於響應環境，因此它自動適應先前由靜態視頻佔用的區域。

>[!NOTE]
此時，如果僅添加了超連結網頁的交互，則完成。
但是，如果添加任何交互性來觸發Quickview，則交互視頻旁的縮略圖僅用於顯示；它們尚未與您現有的Quickview整合。 在這種情況下，您現在必須將互動式視頻與網站上的現有Quickview整合。

**範例**

以演示網站為例：

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html)

請注意，嵌入代碼是標準的：

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

整合過程簡單，只需從Experience Manager中刪除視頻嵌入代碼，並用互動式視頻嵌入代碼代替它。 可以在以下URL上查看結果。 雖然它顯示頁面上存在的互動式視頻，但它尚未與現有Quickview整合：

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-1.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-1.html)

## 將互動式視頻與現有Quickview整合 {#integrating-an-interactive-video-with-an-existing-quickview}

>[!NOTE]
僅當您是獨立的Experience Manager Assets客戶時，此任務才適用。

此過程中的最後一個步驟是將互動式視頻與網站上使用的現有Quickview實現整合。 對於適用於所有案例的整合，沒有解決方案。 每個Quickview實現都是唯一的。 因此，需要一種需要前端IT人員協助的具體方法。

現有的Quickview實現通常表示網頁上發生的一系列相互關聯的操作，其順序如下：

1. 用戶在網站的用戶介面中觸發元素。
1. 前端代碼根據步驟1中觸發的用戶介面元素獲取Quickview URL。
1. 前端代碼使用步驟2AJAX中獲得的URL發送請求。
1. 後端邏輯將相應的Quickview資料或內容返回到前端代碼。
1. 前端代碼載入Quickview資料或內容。
1. 或者，前端代碼將載入的Quickview資料轉換為HTML表示。
1. 前端代碼顯示一個模式對話框或面板，並在螢幕上為最終用戶呈現HTML內容。

這些調用不表示可由網頁邏輯從任意步驟調用的獨立公共API調用。 相反，它是連結調用，在上一步的最後階段（回叫）中，每個下一步都被隱藏。

當用戶在互動式視頻內的縮略圖上選擇時，在互動式視頻正在替換步驟1和部分步驟2的同時，這種用戶交互由觀看者處理。 查看器將事件返回到包含先前添加到Experience Manager的所有縮略圖資料的網頁。

在此類事件處理程式中，前端代碼執行以下操作：

* 偵聽互動式視頻發出的事件。
* 基於縮略圖資料構建Quickview URL。
* 觸發從後端載入Quickview並將其呈現在螢幕上以供顯示的過程。

此外，互動式視頻查看器支援全屏操作模式。 最終用戶通過選擇縮略圖而不保留全屏來觸發Quickview。 要實現此功能，請更改前端代碼，以便將「快速視圖」模式對話框附加到查看器的容器。 不要添加當查看器處於全屏模式時不可用的文檔BODY或其他網頁元素。 執行此作業的代碼必須偵聽在載入到頁面上的查看器之後發送的一個或多個查看器回調。

Experience Manager返回的嵌入代碼已具有可使用的事件處理程式。 它被注釋掉，如以下突出顯示的代碼片段所示：

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

因此，只需取消對上面突出顯示的代碼段的注釋，並用特定網頁的特定代碼替換虛擬處理程式體。

標準嵌入代碼中存在兩個預設回調處理程式： `quickViewActivate` 和 `initComplete`。 的 `quickViewActivate` 在查看器中選擇縮略圖時，處理程式將觸發。 使用它將查看器與Quickview激活邏輯整合。 的 `initComplete` 當查看器載入到頁面中時，handler僅觸發一次。 此處理程式用於調整網頁DOM中的Quickview對話框位置。

構建Quickview URL的過程與標識本主題前面所涵蓋的縮略圖變數的過程相反。 使用先前標識的Quickview URL示例，您可以查看每種情況下如何構建Quickview URL:

<table>
  <tbody>
  <tr>
    <td><p>在查詢字串中找到的單一SKU</p> </td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;source=100";
      },
      });</code></td>
  </tr>
  <tr>
    <td>單SKU，在URL路徑中找到</td>
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

觸發Quickview URL並激活Quickview面板的最後一步很可能需要您的IT部門的前端IT人員的幫助。 他們知道如何從正確的步驟準確觸發Quickview實現，並擁有可供使用的Quickview URL。

您可以瞭解這些步驟如何應用到演示網站，以將互動式視頻與Quickview代碼完全整合。 在本主題的前面，Quickview URL的結構標識為：

```xml
/datafeed/$CategoryId$-$SKU$.json
```

在URL中重建此URL很容易 `quickViewActivate` 處理程式使用 `categoryId` 和 `sku` 中的 `inData` 通過查看器代碼傳遞給處理程式的對象，如下所示：

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

演示網站正在使用一個簡單的 `loadQuickView()` 函式。 此函式只採用一個參數，即Quickview資料URL。 所以整合互動式視頻的最後一步就是在 `quickViewActivate` 處理程式：

```xml
loadQuickView(quickViewUrl);
```

最後，確保「快速視圖」對話框已連接到查看器的容器元素。 預設嵌入代碼提供了實現此功能的示例步驟。 要獲取對查看器容器元素的引用，可使用以下代碼行：

```xml
var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
var inner_container = document.getElementById(sdkContainerId);
```

位置 `inner_container` 是對 `DIV` 由查看器管理的元素。 您希望對話框是該對話框的子項 `DIV`。

實際定位模態對話框元素並將其連接到上述容器的步驟是特定於大小寫的。 同樣，您也可以向熟悉所需Quickview實施的前端開發人員尋求幫助。

如果使用示例網站，則「快速視圖」模式對話框將作為 `DIV` 將快速視圖模式ID直接附加到文檔 `BODY`。 因此，將該對話框移到查看器容器的代碼與以下內容一樣簡單：

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

帶有完全整合互動式視頻的最終演示網站如下所示：

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-3.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-3.html)

## 使用 Quickview 建立自訂快顯視窗 {#using-quickviews-to-create-custom-pop-ups}

請參閱 [使用Quickview建立自定義彈出窗口](/help/assets/custom-pop-ups.md)。
