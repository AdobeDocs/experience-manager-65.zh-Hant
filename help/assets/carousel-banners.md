---
title: 旋轉木馬旗幟
description: 瞭解如何在Dynamic Media使用旋轉木馬橫幅
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

# 旋轉木馬旗幟{#carousel-banners}

轉盤橫幅使營銷人員能夠通過輕鬆建立互動式旋轉促銷內容並將其傳送到任何螢幕來推動轉換。

建立和修改促銷標語中的內容可能非常耗時，這限制了您快速發佈新內容或使其更具針對性的能力。 旋轉傳送條幅允許您快速建立或修改旋轉條幅。 您可以添加交互性，例如連結到產品詳細資訊或相關資源的熱點，並將它們提交到任何螢幕，從而讓您更快地將新促銷內容推向市場。

旋轉木馬橫幅由帶有文字的橫幅指定 **[!UICONTROL 卡魯塞]**

![chlimage_1-438](assets/chlimage_1-438.png)

在您的網站上，旋轉木馬橫幅可以如下所示：

![chlimage_1-439](assets/chlimage_1-439.png)

在此，您可以瀏覽影像（通過按一下數字）。 此外，幻燈片會根據您可以自定義的時間間隔自動旋轉。 您在旋轉木馬橫幅中添加的影像支援熱點和影像映射，用戶可以在其中選擇或轉到超連結或訪問Quickview窗口。

在此示例中，用戶點擊或按一下了影像映射，並訪問了手套的Quickview窗口：

![chlimage_1-440](assets/chlimage_1-440.png)

## 觀察如何建立旋轉木馬橫幅 {#watch-how-carousel-banners-are-created}

在上播放漫步 [旋轉傳送條幅的建立方法](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner)（10分33秒）。 您還將學習如何預覽、編輯和傳遞旋轉傳送布幅。

>[!NOTE]
>
>必須將非管理用戶添加到 **[!UICONTROL 大壩用戶]** 組，以便能夠建立或編輯旋轉傳送條幅。 如果您在建立或編輯時遇到問題，請咨詢系統管理員，該管理員可以將您添加到 **[!UICONTROL 大壩用戶]** 組。

## 快速啟動：旋轉木馬旗幟 {#quick-start-carousel-banners}

為了讓您快速啟動並運行，請開啟旋轉木馬橫幅：

1. [識別熱點和影像映射變數](#identifying-hotspot-and-image-map-variables) (僅適用於使用Experience Manager Assets+Dynamic Media的客戶)

   首先，確定現有Quickview實現使用的動態變數，以便在Adobe Experience Manager資產的旋轉木馬橫幅建立過程中正確輸入熱點和影像映射資料。

   >[!NOTE]
   >
   >如果您是Experience Manager Sites或電子商務客戶，則可以使用內置功能導航至產品頁面並查找產品目錄中的現有SKU（庫存單位）。 無需手動輸入熱點或影像映射變數。 請參閱 [建立電子商務](/help/commerce/cif-classic/administering/generic.md)。
   >
   >
   >如果您是Experience Manager Assets和Dynamic Media的客戶，請手動輸入熱點和影像映射的資料，然後將發佈的URL或嵌入代碼與第三方內容管理系統整合。

1. 可選：視需 [要建立轉盤集檢視器預設](/help/assets/managing-viewer-presets.md)。

   如果您是管理員，則可以通過建立自己的「旋轉傳送器」查看器預設來定制旋轉傳送器的行為和外觀。 主要優點是，您可以為多個貽貝重複使用此自定義查看器預設。 但是，用戶可以選擇在創作旋轉木馬時直接定制旋轉木馬的行為和外觀。 當要為給定旋轉木馬進行特定設計時，此方法是首選方法。

1. [上載影像橫幅](#uploading-image-banners)。

   上載要進行交互的影像橫幅。

1. [建立旋轉軸集](#creating-carousel-sets)。

   在Carousels集中，用戶在標題影像中導航，並選擇熱點或影像映射以訪問相關內容。

   要在資產中建立旋轉選取集，請選擇 **[!UICONTROL 建立]**，然後選擇 **[!UICONTROL 旋轉木馬集]**。 將資源添加到幻燈片並選擇 **[!UICONTROL 保存]**。 您也可以直接在編輯器中編輯轉盤的外觀和行為。

1. [將熱點或影像映射添加到影像標題](#adding-hotspots-or-image-maps-to-an-image-banner)。

   將一個或多個熱點或影像映射添加到影像標題並將每個熱點或影像映射與連結、快速視圖或體驗片段等操作相關聯。 添加熱點或影像映射後，通過發佈傳送帶集完成此任務。 發佈建立可用於複製並應用於網站登錄頁的嵌入代碼。

   請參閱 [（可選）預覽旋轉傳送條幅](#optional-previewing-carousel-banners)  — 可選。 如果需要，可以查看旋轉選取集的表示形式並test其交互性。

1. [發佈旋轉木馬橫幅](#publishing-carousel-banners)。

   與發佈任何資產一樣，發佈旋轉選取集。 在資產中，定位至傳送帶集並選擇它，然後選擇 **[!UICONTROL 發佈]**。 發佈Carousel集將激活URL和嵌入字串。

1. 執行下列任一項作業：

   * [將旋轉傳送標題添加到網站頁](#adding-a-carousel-banner-to-your-website-page) 您可以將複製到網站頁面的傳送帶標題URL或嵌入代碼添加到網站頁面。

      * [將旋轉軸橫幅與現有Quickview整合](#integrating-the-carousel-banner-with-an-existing-quickview)。 如果您使用第三方Web內容管理系統，則必須將新的旋轉木馬橫幅與網站上現有的Quickview實現整合。
   * [將旋轉木馬橫幅添加到您的網站，以Experience Manager](/help/assets/adding-dynamic-media-assets-to-pages.md) 如果您是Experience Manager Sites客戶，則可以使用「交互媒體」元件將傳送帶集直接添加到Experience Manager中的頁面。


要編輯旋轉軸集，請參閱 [編輯旋轉軸集](#editing-carousel-sets)。 此外，您還可以查看和編輯 [旋轉木馬集屬性](manage-assets.md#editing-properties)。

## 識別熱點和影像映射變數 {#identifying-hotspot-and-image-map-variables}

首先，確定現有Quickview實現使用的動態變數，以便在Experience Manager Assets的旋轉軸集建立過程中正確輸入熱點或影像映射資料。

將熱點或影像映射添加到Experience Manager Assets的標題影像時，請為每個熱點或影像映射分配SKU和可選的附加變數。 這些變數稍後用於將熱點或影像映射與Quickview內容匹配。

>[!NOTE]
>
>如果您是Experience Manager Sites和/或Experience Manager電子商務客戶，請跳過此步驟。 無需手動識別熱點或影像映射變數；您可以使用與E-commerce的整合進行產品整合。 請參閱 [建立電子商務](/help/commerce/cif-classic/administering/generic.md)。 此外，您還可以使用Interactive元件並將其添加到網頁中。
>
>如果您是Experience Manager Assets或媒體客戶，請發佈URL或嵌入代碼，然後與第三方內容管理系統整合併手動識別熱點和影像映射。

正確識別與熱點或影像映射資料關聯的變數的數量和類型非常重要。 添加到橫幅影像的每個熱點或影像映射都必須攜帶足夠的資訊，以明確標識現有後端系統中的產品。 同時，每個熱點或影像映射不得包含超出需要的資料。 這是因為這樣會使資料輸入過程過於複雜，並且正在進行的熱點或影像地圖管理更容易出錯。

標識一組用於熱點或影像映射資料的變數的方法不同。

有時，與負責現有Quickview實施的IT專家進行咨詢就足夠了。 他們可能知道在系統中標識Quickview所需的最少一組資料。 但是，通常也可以簡單地分析前端代碼的現有行為。

大多數Quickview實現都使用以下範例：

* 使用者在網站上啟動使用者介面元素。例如，點擊 **[!UICONTROL 快速視圖]** 按鈕
* 如果需要，網站會向後端發送Ajax請求以載入Quickview資料或內容。
* Quickview資料被翻譯成內容以準備在網頁上呈現。
* 最後，前端代碼在螢幕上直觀地呈現這些內容。

然後，方法是訪問現有網站中實施Quickview功能的不同區域。 觸發Quickview，並捕獲網頁發送的Ajax URL，以載入Quickview資料或內容。

通常，您不需要使用任何專用的調試工具。 現代Web瀏覽器具有能夠完成充分工作的Web檢查器。 以下是包括Web檢查器的Web瀏覽器的幾個示例：

* 要在GoogleChrome中查看所有傳出HTTP請求，請按F12(Windows)或Command-Option-I(Mac)開啟「開發人員工具」面板，然後選擇「網路」頁籤。
* 在Firefox中，您可以按F12(Windows)或Command-Option-I(Mac)激活Firebug插件，然後使用其「網」頁籤，也可以使用內置的「檢查器」工具及其「網路」頁籤。

在瀏覽器中開啟網路監視時，在頁面上觸發Quickview。

現在，在網路日誌中查找Quickview Ajax URL，並複製記錄的URL以供將來分析。 通常，在觸發Quickview時，會向伺服器發送大量請求。 通常，Quickview Ajax URL是清單中的第一個URL之一。 它具有複雜的查詢字串部分或路徑，其響應MIME類型為 `text/html`。 `text/xml`或 `text/javascript`。

在此過程中，訪問您網站的不同區域、不同的產品類別和類型非常重要。 原因是，Quickview URL的部件對於給定網站類別是通用的，但只有在您訪問網站的其他區域時才會更改。

在最簡單的情況下，Quickview URL中唯一的變數部分是產品SKU。 在這種情況下，SKU值是向橫幅影像添加熱點或影像映射所需的唯一資料段。

但是，在複雜情況下，Quickview URL除了SKU之外還有不同的元素，例如類別ID、顏色代碼和大小代碼。 在這種情況下，每個元素都是熱點中的一個單獨變數，或旋轉木馬橫幅特徵中的影像映射資料定義。

請考慮以下Quickview URL及其生成的熱點或影像映射變數示例：

<table>
 <tbody>
  <tr>
   <td>在查詢字串中找到的單個SKU。</td>
   <td><p>錄制的Quickview URL包括以下內容：</p>
    <ul>
     <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>URL中唯一的變數部分是 <code>productId=</code> 查詢字串參數，它顯然是SKU值。 因此，熱點或影像映射只需要使用SKU欄位填充值，如 <code>866558,</code> <code>1196184,</code> <code>1081492,</code> <code>1898294.</code></p> </td>
  </tr>
  <tr>
   <td>單SKU，在URL路徑中找到。</td>
   <td><p>錄制的Quickview URL包括以下內容：</p>
    <ul>
     <li><p><code>https://server/product/6422350843</code></p> </li>
     <li><p><code>https://server/product/1607745002</code></p> </li>
     <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>變數部分位於路徑的最後一部分，它成為熱點/影像映射的SKU值：<strong><code>6422350843</code>。 <code>1607745002,</code> </strong><code>0086724882.</code></p> </td>
  </tr>
  <tr>
   <td>查詢字串中的SKU和類別ID。</td>
   <td><p>錄制的Quickview URL包括以下內容：</p>
    <ul>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>在這種情況下，URL中有兩個不同的部分。 SKU儲存在 <code>prodId</code> 參數和類別ID儲存在 <code>category=</code>的下界。</p> <p>因此，熱點/影像映射定義是對。 即，SKU值和一個稱為 <code>categoryId</code>。 結果對如下：</p>
    <ul>
     <li><p>SKU是 <strong><code>305466</code></strong> 和 <code>categoryId</code> 是 <code>1100004</code>。</p> </li>
     <li><p>SKU是 <strong><code>310181</code></strong> 和 <code>categoryId</code> 是 <strong><code>1100004</code></strong>。</p> </li>
     <li><p>SKU是 <strong><code>308706</code></strong> 和 <code>categoryId</code> 是 <strong><code>1740148</code></strong>。</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 上載影像橫幅 {#uploading-image-banners}

如果您已上傳了要使用的影像，請進入下一步， [建立旋轉軸集](#creating-carousel-sets)。 請注意，啟用Dynamic Media後，必須上載旋轉木馬中使用的影像。

要上載影像橫幅，請參閱 [上載資產](/help/assets/manage-assets.md)。

## 建立旋轉軸集 {#creating-carousel-sets}

>[!NOTE]
>
>必須將非管理用戶添加到 **[!UICONTROL 大壩用戶]** 組以建立或編輯旋轉傳送條幅。 如果您在建立或編輯時遇到問題，請咨詢系統管理員，該管理員可以將您添加到 **[!UICONTROL 大壩用戶]** 組。

**要建立旋轉軸集：**

1. 在「資產」中，導航到要建立旋轉傳送器集的資料夾並轉到 **[!UICONTROL 建立]** > **[!UICONTROL 旋轉木馬集]**。
1. 在旋轉軸標題編輯器頁面上，選擇 **[!UICONTROL 點擊以開啟資產選擇器]** 來修改標籤元素的屬性。

   在旋轉木馬橫幅編輯器頁面上，執行以下任一操作：

   * 在頁面左上角附近，選擇 **[!UICONTROL 添加幻燈片]** 表徵圖

   * 在頁面中部附近，選擇 **[!UICONTROL 點擊以開啟資產選擇器]**。
   選擇以選擇要包括在旋轉傳送器集中的資產。 選取的資產上面有核取標籤圖示。完成後，在頁面右上角附近，選擇 **[!UICONTROL 選擇]**。

   使用「資產選擇器」，您可以輸入關鍵字並點選或按一下「退貨」來搜尋 **[!UICONTROL 資產]**。您也可以套用篩選條件來調整搜尋結果。您可以依路徑、系列、檔案類型和標籤來篩選。選擇篩選器，然後選擇 **[!UICONTROL 篩選]** 的子菜單。 點選「檢視」圖示並選取「欄檢視」、「卡片檢視」或「清 **[!UICONTROL 單檢視」]**, **[!UICONTROL 以變更]**&#x200B;檢視 ****。

   請參閱 [使用選擇器](/help/assets/working-with-selectors.md) 的子菜單。

1. 繼續添加幻燈片，直到添加了要在「旋轉選取集」中旋轉的所有影像。
1. （可選）執行下列任一操作：

   * 如有必要，拖動幻燈片可重新排序集清單中的影像。
   * 要刪除影像，請選擇影像，然後選擇 **[!UICONTROL 刪除幻燈片]** 的上界。

   * 要應用預設，請在頁面右上角附近選擇預設下拉清單，然後選擇一個預設，以立即應用於該設定。
   要刪除幻燈片，請選擇幻燈片，然後在工具欄上，選擇 **[!UICONTROL 刪除幻燈片]**。 要移動幻燈片，請選擇重新排序表徵圖並按住並移動到所需位置。

1. 在幻燈片中添加影像後，可以將熱點、影像映射或兩者都添加到影像中。 請參閱 [將熱點或影像映射添加到影像標題](#adding-hotspots-or-image-maps-to-an-image-banner)。
1. 可以更改旋轉木馬集的可視設計和行為。 選擇 **[!UICONTROL 行為]** 和 **[!UICONTROL 外觀]** 頁籤，並調整旋轉傳送標題的顯示方式或特定元件的行為方式。 請參閱 [管理查看器預設](/help/assets/viewer-presets.md) 的子菜單。

   >[!NOTE]
   >
   >對於旋轉木馬橫幅，您可以調整以下內容：
   >
   >    * 影像顯示的持續時間。 預設情況下，每個影像顯示9秒。
   >    * 動畫. 預設情況下，每個幻燈片轉換都是淡出。 可以將其更改為幻燈片轉換。
   >    * 按鈕的樣式。 用戶可通過點擊每個點或數字來旋轉橫幅。 您可以更改設定指示器按鈕的顯示位置（如果它們是數字或虛線樣式）以及它們的大小。
   >    * 更改影像映射的加亮樣式或用於熱點的表徵圖。
   >    * 在編輯查看器預設之前，請根據需要的預設選擇樣式。 如果不選擇樣式，則當您開始編輯查看器預設時，如果您決定更改為其他預設，則會丟失所有更改。

   >
   >請參閱 [旋轉木馬橫幅的特殊注意事項](/help/assets/managing-viewer-presets.md#special-considerations-for-creating-a-carousel-banner-viewer-preset) 的子菜單。

   還可以預覽旋轉傳送帶的顯示方式。 請參閱 [（可選）預覽旋轉傳送條幅](#optional-previewing-carousel-banners)。

1. 選擇 **[!UICONTROL 保存]** 的子菜單。

## 將熱點或影像映射添加到影像標題 {#adding-hotspots-or-image-maps-to-an-image-banner}

可以使用「旋轉選取集」編輯器將熱點或影像映射添加到橫幅中。

添加熱點或影像映射時，可將其定義為Quickview彈出式顯示、超連結或體驗片段。

請參閱 [體驗片段](/help/sites-authoring/experience-fragments.md)。

>[!NOTE]
>
>將查看器嵌入體驗片段時，不支援旋轉木馬橫幅中的社交媒體共用工具。
>
>要解決此問題，可以使用或建立沒有社交媒體共用工具的查看器預設。 這樣的查看器預設使您能夠成功將其嵌入「體驗片段」中。

將熱點或影像映射添加到影像時，切記保存您所做的工作。 在當前建立/編輯會話期間，支援在頁面右上角附近的「撤消」和「重做」選項。

建立完旋轉傳送條幅後，您可以選擇使用「預覽」查看旋轉傳送條幅對客戶的顯示方式。

請參閱 [（可選）預覽旋轉傳送條幅](#optional-previewing-carousel-banners)。

>[!NOTE]
>
>將熱點添加到 [互動式影像](/help/assets/interactive-images.md) 或者旋轉傳送標題，熱點資訊儲存在同一元資料位置。 該位置與影像的位置相關，而不管它是互動式影像還是旋轉木馬橫幅。 此功能意味著您可以在任意一個查看器中輕鬆地重複使用同一影像及其定義的熱點資料。
但是，請注意，旋轉木馬橫幅支援也可以包含熱點的影像上的影像映射；互動式映像不會。 如果要建立使用相同影像的互動式影像或旋轉傳送標題，請記住此規則。 請考慮使用同一影像的單獨副本建立互動式影像和旋轉傳送條幅。

>[!NOTE]
如果您正在編輯具有熱點的交互影像並裁剪影像，則您的熱點將被刪除。

另請參閱 [添加影像映射](/help/assets/image-maps.md)。

**要將熱點或影像映射添加到影像標題：**

1. 在「資產」中，導航至要進行交互的傳送帶集。
1. 選取旋轉軸集並選取 **[!UICONTROL 編輯]**。 將開啟「旋轉選取器查看器編輯器」(Carousel Viewer Editor)。
1. 選擇要進行交互的幻燈片。
1. 在頁面左上角附近，選擇 **[!UICONTROL 熱點]** 或 **[!UICONTROL 影像映射]**。
1. 執行下列任一操作：

   * 對於熱點：在影像上，選擇希望熱點出現的位置。
   * 對於影像映射：在影像上，選擇，然後從左上角向右拖動，以建立影像映射區域。 可以通過拖動角來調整影像映射的大小。

   如有必要，請將熱點或影像映射拖動到新位置。 根據需要添加其他熱點或影像映射。

   要刪除熱點或影像映射，請選擇 **[!UICONTROL 操作]** 頁籤。 在「地 **[!UICONTROL 圖與熱點]** 」標題下，從「選定類型 **** 」下拉菜單中，選擇要刪除的熱點或影像映射的名稱。選擇 **[!UICONTROL 垃圾]** 表徵圖，然後選擇 **[!UICONTROL 刪除]**。

1. 在「名稱」文本欄位中，鍵入熱點或影像映射的名稱。 此名稱也出現在 **[!UICONTROL 地圖和熱點]** 的子菜單。 如果您決定在將來更改熱點或影像映射，則提供名稱可以輕鬆識別該熱點或影像映射。
1. 在 **[!UICONTROL 操作]** 頁籤：

   * 選擇 **[!UICONTROL 快速視圖]**。

      * 如果您是Experience Manager Sites和電子商務客戶，請選擇「產品選取器」表徵圖（放大鏡）以開啟「選擇產品」頁。 選擇要使用的產品，然後在頁面右上角選擇複選標籤，以便您可以返回到旋轉傳送帶橫幅編輯器。
      * 如果您不是Experience Manager Sites或電子商務客戶

         * 請參閱 [識別熱點變數](#identifying-hotspot-and-image-map-variables) 的子菜單。
         * 然後，手動輸入SKU值。 在「SKU值」文本欄位中，鍵入產品的SKU（庫存保管單位），該SKU是您提供的每個不同產品或服務的唯一標識符。 輸入的SKU值會自動填充Quickview模板的可變部分，以便系統知道將已點擊的熱點與特定SKU的Quickview相關聯。
         * （可選）如果Quickview中有其它變數必須用於進一步標識產品，請選擇 **[!UICONTROL 添加泛型變數]**。 在文本欄位中，指定一個額外變數。 例如，category=Mens是一個添加的變數。

         * 請參閱 [使用選擇器](/help/assets/working-with-selectors.md) 的子菜單。
   * 選擇 **[!UICONTROL 超連結]**。

      * 如果您是Experience Manager Sites客戶，請選擇「站點選擇器」表徵圖（資料夾）以導航到URL。
         >[!NOTE]
         如果您的交互內容具有與相對URL的連結，特別是與Experience Manager Sites頁面的連結，則無法使用基於URL的連結方法。

      * 如果您是獨立客戶，請在HREF文本欄位中指定連結網頁的完整URL路徑。

   請確保指定是在新瀏覽器頁籤（推薦的預設頁籤）或同一頁籤中開啟連結。

   請參閱 [使用選擇器](/help/assets/working-with-selectors.md) 的子菜單。

   * 選擇 **[!UICONTROL 體驗片段]**。

      * 如果您是Experience Manager Sites客戶，請選擇「搜索」表徵圖（放大鏡）以開啟「體驗片段」頁。 選擇要使用的體驗片段，然後選擇 **[!UICONTROL 選擇]** 在頁面的右上角，以便您可以返回熱點管理頁面。
請參閱 [體驗片段](/help/sites-authoring/experience-fragments.md)。

      * 指定在標題上顯示體驗片段的寬度和高度。

         >[!NOTE]
         將查看器嵌入體驗片段時，不支援旋轉木馬橫幅中的社交媒體共用工具。
         要解決此問題，請建立沒有社交媒體共用工具的查看器預設。 這樣的查看器預設使您能夠成功將其嵌入「體驗片段」中。
   ![experience_fragment_carouselbanner](assets/experience_fragment-carouselbanner.png)

   還可以預覽旋轉傳送帶的顯示方式。 請參閱 [（可選）預覽旋轉傳送條幅](#optional-previewing-carousel-banners)。

1. 選取&#x200B;**[!UICONTROL 儲存]**。
1. 發佈旋轉傳送器集。 發佈會建立可在網站頁上使用的嵌入代碼或URL。 如果您是Experience Manager Sites客戶，則可以直接將旋轉木馬集添加到您的網頁。

   請參閱 [發佈資產](/help/assets/publishing-dynamicmedia-assets.md)。

   請參閱 [將傳送帶集添加到網站登錄頁](#adding-a-carousel-banner-to-your-website-page)

## 編輯旋轉軸集 {#editing-carousel-sets}

>[!NOTE]
必須將非管理用戶添加到 **[!UICONTROL 大壩用戶]** 組，以便能夠建立或編輯旋轉傳送條幅。 如果您在建立或編輯時遇到問題，請咨詢系統管理員，該管理員可以將您添加到 **[!UICONTROL 大壩用戶]** 組。

可以對「旋轉傳送器集」執行各種編輯任務，如：

* 將幻燈片添加到旋轉軸集。 另請參閱 [使用選擇器](/help/assets/working-with-selectors.md)。
* 在「旋轉軸集」中重新排序幻燈片。
* 刪除旋轉軸集中的資產。
* 應用查看器預設。
* 刪除旋轉軸集。
* 添加或編輯熱點和影像映射。 另請參閱 [使用選擇器](/help/assets/working-with-selectors.md)。

**要編輯旋轉軸集：**

1. 執行下列任一操作：

   * 將滑鼠懸停在旋轉軸集資產上，然後選擇 **[!UICONTROL 編輯]** （鉛筆表徵圖）。
   * 將滑鼠懸停在旋轉軸集資產上，選擇 **[!UICONTROL 選擇]** （複選標籤表徵圖），然後選擇 **[!UICONTROL 編輯]** 的上界。

   * 選擇「旋轉軸集」資產，然後在頁面左上角選擇 **[!UICONTROL 編輯]** （鉛筆表徵圖）。

1. 要編輯「旋轉軸集」，請執行以下任一操作：

   * 要添加幻燈片，請選擇 **[!UICONTROL 添加幻燈片]** 表徵圖，然後導航到要添加到該幻燈片的資產，然後選擇複選標籤。
   * 要重新排序幻燈片，請將幻燈片拖到新位置（選擇重新排序表徵圖以移動項目）。
   * 要添加熱點或影像映射，請選擇熱點或影像映射表徵圖，並參閱 [添加熱點和影像映射](#adding-hotspots-or-image-maps-to-an-image-banner)。
   * 要編輯旋轉載具集的外觀或行為，請選擇 **[!UICONTROL 外觀]** 或 **[!UICONTROL 行為]** 頁籤。
   * 要編輯熱點或影像映射，請在相應的幻燈片上選擇熱點或影像映射，然後根據需要在 **[!UICONTROL 操作]** 頁籤。
   * 要刪除幻燈片，請選擇它，然後選擇 **[!UICONTROL 刪除幻燈片]** 的上界。
   * 要應用預設，請在頁面右上角附近選擇 **[!UICONTROL 預設]** 下拉清單，然後選擇查看器預設。
   * 要刪除整個旋轉選取集，請導航至旋轉選取集，選擇它，然後選擇 **[!UICONTROL 刪除]**。

   >[!NOTE]
   如果您正在編輯具有熱點的交互影像並裁剪影像，則您的熱點將被刪除。

## （可選）預覽旋轉傳送條幅 {#optional-previewing-carousel-banners}

您可以使用「預覽」(Preview)查看旋轉傳送條幅對客戶的顯示方式，並test旋轉傳送條幅熱點和影像映射以確保它們按預期的方式運行。

當您對旋轉木馬標題感到滿意時，可以發佈它。
請參閱 [在網頁上嵌入視頻或影像查看器](/help/assets/embed-code.md)。
請參閱 [將URL連結到Web應用程式](/help/assets/linking-urls-to-yourwebapplication.md)。 如果您的交互內容具有與相對URL的連結，特別是與Experience Manager Sites頁面的連結，則無法使用基於URL的連結方法。
請參閱 [將Dynamic Media資產添加到頁面](/help/assets/adding-dynamic-media-assets-to-pages.md)。

可以從「旋轉選取編輯器」(Carousel Editor)或 **[!UICONTROL 查看者]** 清單框。

**要預覽旋轉傳送條幅：**

1. 在 **[!UICONTROL 資產]**，導航至已建立的現有旋轉傳送欄，然後選擇將其開啟。
1. 選取&#x200B;**[!UICONTROL 編輯]**。
1. 在工具欄右角的查看器預設清單中，選擇查看器以預覽旋轉傳送標題。

   ![experience_fragment_carouselbanner-viewerdropdown](assets/experience_fragment-carouselbanner-viewerdropdown.png)

1. 選擇 **[!UICONTROL 預覽]**。
1. 選擇影像上的熱點或影像映射，以便可以test其關聯操作。

**要從「查看者」清單預覽旋轉傳送條幅：**

1. 在 **[!UICONTROL 資產]**，導航至已建立的現有旋轉傳送欄，然後選擇將其開啟。
1. 在「預覽」頁面的左上角附近，選擇「內容」表徵圖。
1. 在 **[!UICONTROL 查看者]** 清單中，選擇要使用的旋轉傳送帶橫幅查看器預設的名稱。
1. 選擇影像上的熱點或影像映射，以便可以test其關聯操作。

## 發佈旋轉木馬橫幅 {#publishing-carousel-banners}

發佈旋轉木馬，以便您使用它。 發佈傳送器集將激活URL和嵌入代碼。 它還將傳送帶發佈到Dynamic Media雲，該雲與CDN整合，以實現可擴展和效能交付。

>[!NOTE]
如果將具有熱點的現有互動式影像用於旋轉傳送帶橫幅，則必須在發佈旋轉傳送帶橫幅之後單獨發佈互動式影像。
此外，如果您修改了在旋轉傳送帶橫幅中使用的預先存在的已發佈交互影像，則必須在這些更改反映在旋轉傳送帶橫幅中之前發佈交互影像。

請參閱 [發佈Dynamic Media資產](/help/assets/publishing-dynamicmedia-assets.md) 的子菜單。

## 將旋轉傳送標題添加到網站頁 {#adding-a-carousel-banner-to-your-website-page}

上載了橫幅影像以建立傳送帶、將熱點和/或影像映射添加到該傳送帶並發佈傳送帶集後，您現在可以將其添加到現有網站頁面。

>[!NOTE]
如果您是Experience Manager Sites客戶，則可以將互動式媒體元件拖動到您的頁面中，將旋轉傳送標題直接添加到您的頁面。 請參閱 [將Dynamic Media資產添加到頁面](/help/assets/adding-dynamic-media-assets-to-pages.md)。

但是，如果您是獨立的Experience Manager資產客戶，則可以按本節所述將旋轉木馬橫幅手動添加到網站登錄頁。

1. 複製已發佈的傳送帶集的嵌入代碼。
請參閱 [將視頻或影像查看器嵌入網頁](/help/assets/embed-code.md)。

1. 將您從Experience Manager Assets複製的嵌入代碼添加到您的網頁。
複製的嵌入代碼是響應的，因此它必須自動適應頁面的嵌入區域。

## 將旋轉軸橫幅與現有Quickview整合 {#integrating-the-carousel-banner-with-an-existing-quickview}

>[!NOTE]
此步驟僅在您是獨立的Experience Manager Assets客戶時適用。

此過程中的最後一個步驟是將旋轉傳送帶橫幅與網站上的現有Quickview實現整合。 每個Quickview實施都是獨特的，需要一種特定的方法，需要前端IT人員的幫助。

現有的Quickview實現通常表示網頁上發生的一系列相互關聯的操作，其順序如下：

1. 用戶在網站的用戶介面中觸發元素。
1. 前端代碼根據步驟1中觸發的用戶介面元素獲取Quickview URL。
1. 前端代碼使用步驟2中獲得的URL發送Ajax請求。
1. 後端邏輯將相應的Quickview資料或內容返回到前端代碼。
1. 前端代碼載入Quickview資料或內容。
1. 或者，前端代碼將載入的Quickview資料轉換為HTML表示。
1. 前端代碼顯示一個模式對話框或面板，並在螢幕上為最終用戶呈現HTML內容。

這些調用不表示可由網頁邏輯從任意步驟調用的獨立公共API調用。 相反，它是連結調用，在上一步的最後階段（回叫）中，每個下一步都被隱藏。

當用戶點擊旋轉傳送橫幅內的熱點或影像地圖時，觀看者處理這種交互。 查看器將事件返回到包含先前添加的所有熱點或影像映射資料的網頁。

在此類事件處理程式中，前端代碼執行以下操作：

* 偵聽由旋轉木馬標題發出的事件。
* 基於熱點或影像映射資料構建Quickview URL。
* 觸發從後端載入Quickview並將其呈現在螢幕上以供顯示的過程。

Experience Manager Assets返回的嵌入代碼已具有一個可供使用的事件處理程式，該處理程式已被註銷。

因此，只需取消注釋代碼，用特定網頁的代碼替換虛擬處理程式主體即可。

構造Quickview URL的過程與用於識別先前覆蓋的熱點和影像映射變數的過程相反。

請參閱 [識別熱點和影像映射變數](#identifying-hotspot-and-image-map-variables)。

觸發Quickview URL並激活Quickview面板的最後一步很可能需要您的IT部門的前端IT人員的幫助。 他們知道如何從正確的步驟準確觸發Quickview實現，並擁有可供使用的Quickview URL。

## 使用 Quickview 建立自訂快顯視窗 {#using-quickviews-to-create-custom-pop-ups}

請參閱 [使用Quickview建立自定義彈出窗口](/help/assets/custom-pop-ups.md)。
