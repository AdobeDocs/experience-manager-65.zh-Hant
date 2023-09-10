---
title: 整合 Dynamic Media 檢視器與 Analytics 和 Adobe Experience Platform 標記
description: 瞭解適用於Experience Platform標籤的Dynamic Media Viewers擴充功能和Dynamic Media Viewers 5.13。它可讓Adobe Analytics和Experience Platform標籤的客戶在其Experience Platform標籤設定中，使用特定於Dynamic Media檢視器的事件和資料。
mini-toc-levels: 3
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
docset: aem65
feature: Viewers
role: User, Admin,Developer,Data Engineer,Data Architect
exl-id: 161dfe22-bc1c-4b60-8ab6-a19407a39e2e
source-git-commit: 04941e17054951bcf6264da957d951a5d1107896
workflow-type: tm+mt
source-wordcount: '6622'
ht-degree: 6%

---

# 整合 Dynamic Media 檢視器與 Analytics 和 Adobe Experience Platform 標記 {#integrating-dynamic-media-viewers-with-adobe-analytics-and-adobe-launch}

## 什麼是Dynamic Media Viewers與Adobe Analytics和Experience Platform標籤的整合？ {#what-is-dynamic-media-viewers-integration-with-adobe-analytics-and-adobe-launch}

<!-- Leave this hidden path here; it points to the topic source from Sasha https://wiki.corp.adobe.com/pages/viewpage.action?spaceKey=~oufimtse&title=Dynamic+Media+Viewers+integration+with+Adobe+Launch -->

*Dynamic Media檢視器* Experience Platform標籤和Dynamic Media檢視器5.13的擴充功能可讓Adobe Analytics和Experience Platform標籤客戶在其Experience Platform標籤設定中，使用特定於Dynamic Media檢視器的事件和資料。

此整合表示您可以使用Adobe Analytics追蹤網站上Dynamic Media Viewers的使用情況。 同時，您也可以將檢視器公開的事件和資料，與任何來自Adobe或協力廠商的其他Experience Platform標籤擴充功能搭配使用。

若要瞭解有關Adobe擴充功能或協力廠商擴充功能的詳細資訊，請參閱 [Adobe擴充功能](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/overview.html) 在Experience Platform標籤使用手冊中。

**本主題適用於下列內容：** Experience Platform的網站管理員、開發人員和營運人員。

### 整合的限制 {#limitations-of-the-integration}

* Dynamic Media檢視器的Experience Platform標籤整合無法在Experience Manager作者節點中運作。 在發佈之前，您無法從WCM頁面看到任何追蹤。
* Dynamic Media檢視器的Experience Platform標籤整合不支援「快顯」作業模式，此模式是使用「資產詳細資料」頁面上的「URL」按鈕取得檢視器URL。
* Experience Platform標籤整合不能與舊版檢視器Analytics整合約時使用(透過 `config2=` 引數)。
* 視訊追蹤支援僅限於「核心播放」追蹤，如所述 [追蹤概述](https://experienceleague.adobe.com/docs/media-analytics/using/tracking/track-core-overview.html?lang=en). 特別不支援QoS、廣告、章節/區段或錯誤追蹤。
* 資料元素的儲存持續時間設定不支援使用下列專案的資料元素 *Dynamic Media檢視器* 副檔名。 儲存持續時間必須設定為 **[!UICONTROL 無]**.

### 整合的使用案例 {#use-cases-for-the-integration}

與Experience Platform標籤整合的主要使用案例是同時使用Adobe Experience Manager資產和Adobe Experience Manager Sites的客戶。 在這種情況下，您可以設定Experience Manager製作節點與Experience Platform標籤之間的標準整合，然後將您的Sites例項與Experience Platform標籤屬性建立關聯。 之後，新增至Sites頁面的任何Dynamic Media WCM元件都將追蹤檢視器的資料和事件。

另請參閱 [在Experience Manager Sites中追蹤Dynamic Media檢視器](#tracking-dynamic-media-viewers-in-aem-sites).

整合支援的次要使用案例為僅使用Experience Manager Assets或Dynamic Media Classic的客戶。 在這種情況下，您需要取得檢視器的內嵌程式碼，並將其新增至網站頁面。 接著，從Experience Platform標籤取得Experience Platform標籤程式庫生產URL，並手動將其新增至網頁程式碼。

另請參閱 [使用內嵌程式碼追蹤Dynamic Media檢視器](#tracking-dynamic-media-viewers-using-embed-code).

<!-- Path on internal wiki [About tracking Dynamic Media viewers using embed code](https://wiki.corp.adobe.com/display/~oufimtse/Dynamic+Media+Viewers+integration+with+Adobe+Launch#DynamicMediaViewersintegrationwithAdobeLaunch-TrackingDynamicMediaViewersusingEmbedcode). -->

## 資料和事件追蹤在整合中的運作方式 {#how-data-and-event-tracking-works-in-the-integration}

此整合採用兩種獨立的Dynamic Media檢視器追蹤型別： *Adobe Analytics* 和 *適用於音訊和視訊的Adobe Analytics*.

### 關於使用Adobe Analytics進行追蹤  {#about-tracking-using-adobe-analytics}

Adobe Analytics可讓您追蹤一般使用者在您網站上與Dynamic Media Viewers互動時所執行的動作。 Adobe Analytics也可讓您追蹤檢視器特定資料。 例如，您可以追蹤並記錄檢視載入事件以及資產名稱、任何已發生的縮放動作和視訊播放動作。

在Experience Platform標籤中， *資料元素* 和 *規則* 共同啟用Adobe Analytics追蹤。

#### 關於Experience Platform標籤中的資料元素 {#about-data-elements-in-adobe-launch}

Experience Platform標籤中的資料元素是一個已命名屬性，其值會以靜態方式定義，或根據網頁的狀態或Dynamic Media檢視器資料進行動態計算。

資料元素定義可用的選項取決於Experience Platform標籤屬性中安裝的擴充功能清單。 「核心」擴充功能已預先安裝，並可立即用於任何設定。 此「核心」擴充功能可定義資料元素，其值來自Cookie、JavaScript程式碼、查詢字串和許多其他來源。

如所述，針對Adobe Analytics追蹤，必須安裝其他數個擴充功能 [擴充功能的安裝和設定](#installing-and-setup-of-extensions). Dynamic Media Viewers擴充功能新增定義「資料元素」的功能，而該值的引數為動態檢視器事件。 例如，它可以參照檢視器型別，或檢視器載入時報告的資產名稱、一般使用者縮放時報告的縮放等級等等。

Dynamic Media Viewer擴充功能會自動使其資料元素的值保持最新。

定義資料元素後，您就可以使用資料元素選擇器Widget，將其用於Experience Platform標籤UI的其他位置。 尤其是，為了Dynamic Media檢視器追蹤而定義的資料元素，會由「規則」中Adobe Analytics擴充功能的「設定變數」動作參照（請參閱下文）。

另請參閱 [資料元素](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/data-elements.html).

#### 關於Experience Platform標籤中的規則 {#about-rules-in-adobe-launch}

Experience Platform標籤中的規則是一種不可知的設定，它定義了構成規則的三個區域： *活動*， *條件*、和 *動作*：

* *活動* (if)告知Experience Platform標籤何時觸發規則。
* *條件* (if)告知Experience Platform標籤在觸發規則時還應允許或禁止哪些其他限制。
* *動作* （接著）告訴Experience Platform標籤觸發規則時該做什麼。

「事件」、「條件」和「動作」區段中可用的選項取決於安裝在「Experience Platform標籤」屬性中的擴充功能。 此 *核心* 擴充功能已預先安裝，並可立即用於任何設定。 擴充功能提供數個事件選項，例如基本瀏覽器層級的動作。 這些動作包括焦點變更、按鍵和表單提交。 此外也包含條件的選項，例如Cookie值、瀏覽器型別等。 針對「動作」，只有「自訂程式碼」選項可用。

針對Adobe Analytics追蹤，必須安裝數個其他擴充功能，如所述 [擴充功能的安裝和設定](#installing-and-setup-of-extensions). 具體來說：

* Dynamic Media Viewers擴充功能可將支援的事件清單擴充至Dynamic Media檢視器專屬的事件，例如檢視器載入、資產交換、放大和視訊播放。
* Adobe Analytics擴充功能擴充了支援的動作清單，提供傳送資料至追蹤伺服器所需的兩個動作： *設定變數* 和 *傳送信標*.

若要追蹤Dynamic Media檢視器，您可以使用下列任何型別：

* Dynamic Media Viewers擴充功能、核心擴充功能或任何其他擴充功能中的事件。
* 規則定義中的條件。 或者，您也可以將條件區域保持空白。

在動作區段中，您必須具備 *設定變數* 動作。 此動作會告訴Adobe Analytics如何使用資料填入追蹤變數。 同時， *設定變數* 動作不會傳送任何內容至追蹤伺服器。

此 *設定變數* 動作後面必須跟有 *傳送信標* 動作。 此 *傳送信標* 動作實際上會將資料傳送至analytics追蹤伺服器。 這兩個動作， *設定變數* 和 *傳送信標*，來自Adobe Analytics擴充功能。

另請參閱 [規則](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/rules.html).

#### 設定範例 {#sample-configuration}

Experience Platform標籤內的下列設定範例示範如何在檢視器載入時追蹤資產名稱。

1. 從 **[!UICONTROL 資料元素]** 標籤，定義資料元素 `AssetName` 該參考專案 `asset` 的引數 `LOAD` Dynamic Media Viewers擴充功能中的事件。

   ![image2019-11](assets/image2019-11.png)

1. 從 **[!UICONTROL 規則]** 標籤，定義規則 *TrackAssetOnLoad*.

   在此規則中， **[!UICONTROL 事件]** 欄位使用 **[!UICONTROL 載入]** Dynamic Media Viewers擴充功能中的事件。

   ![image2019-22](assets/image2019-22.png)

1. 動作設定有Adobe Analytics擴充功能中的兩種動作型別：

   *設定變數*，將您選擇的analytics變數對應至 `AssetName` 資料元素。

   *傳送信標*，會將追蹤資訊傳送至Adobe Analytics。

   ![image2019-3](assets/image2019-3.png)

1. 產生的規則設定如下所示：

   ![image2019-4](assets/image2019-4.png)

### 關於適用於音訊和視訊的Adobe Analytics {#about-adobe-analytics-for-audio-and-video}

當Experience Cloud帳戶訂閱使用Adobe Analytics的音訊和視訊時，就足以在中啟用視訊追蹤 *Dynamic Media檢視器* 擴充功能設定。 視訊量度可在Adobe Analytics中使用。 視訊追蹤取決於Adobe Medium Analytics for Audio and Video擴充功能的存在。

另請參閱 [擴充功能的安裝和設定](#installing-and-setup-of-extensions).

目前，視訊追蹤支援僅限「核心播放」追蹤，如所述 [追蹤概觀](https://experienceleague.adobe.com/docs/media-analytics/using/tracking/track-core-overview.html?lang=en). 特別不支援QoS、廣告、章節/區段或錯誤追蹤。

## 使用Dynamic Media Viewers擴充功能 {#using-the-dynamic-media-viewers-extension}

如中所述 [整合的使用案例](#use-cases-for-the-integration)，即可透過Experience Manager Sites中的新Experience Platform標籤整合，並使用內嵌程式碼來追蹤Dynamic Media檢視器。

### 在Experience Manager Sites中追蹤Dynamic Media檢視器 {#tracking-dynamic-media-viewers-in-aem-sites}

若要在Experience Manager Sites中追蹤Dynamic Media檢視器， [設定所有整合專案](#configuring-all-the-integration-pieces) 區段必須執行。 具體來說，您必須建立IMS設定和Experience Platform標籤雲端設定。

在正確設定後，您使用Dynamic Media支援的WCM元件新增至網站頁面的任何Dynamic Media檢視器都會自動追蹤資料至Adobe Analytics或Adobe Analytics for Video，或兩者皆追蹤。

<!-- To be reviewed and updated although this is found live in the Experience ManageraaCS version:
See [Adding Dynamic Media Assets to Pages using Adobe Sites](https://helpx.adobe.com/experience-manager/6-5/help/assets/adding-dynamic-media-assets-to-pages.html).
-->

### 使用內嵌程式碼追蹤Dynamic Media檢視器 {#tracking-dynamic-media-viewers-using-embed-code}

客戶若未使用Experience Manager Sites或（或）將Dynamic Media檢視器內嵌至Experience Manager Sites以外的網頁，仍可使用Experience Platform標籤整合。

完成設定步驟，從 [設定Adobe Analytics](#configuring-adobe-analytics-for-the-integration) 和 [設定Experience Platform標籤](#configuring-adobe-launch-for-the-integration) 區段。 不過，不需要Experience Manager相關的設定步驟。

在正確設定後，您可以使用Dynamic Media檢視器將Experience Platform標籤支援新增至網頁。

另請參閱 [新增Experience Platform標籤內嵌程式碼](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/add-embed-code.html) 以進一步瞭解如何使用Experience Platform標籤程式庫內嵌程式碼。

<!-- To be reviewed and updated although this is found live in the Experience ManageraaCS version:
See [Embedding the Video or Image Viewer on a Web Page](https://helpx.adobe.com/experience-manager/6-5/help/assets/embed-code.html) to learn more about how to use the embed code feature of Experience Manager Dynamic Media.
-->

**使用內嵌程式碼追蹤Dynamic Media檢視器：**

1. 建立可內嵌Dynamic Media檢視器的網頁。
1. 先登入Experience Platform標籤，取得Experience Platform標籤程式庫的內嵌程式碼(請參閱 [設定Experience Platform標籤](#configuring-adobe-launch-for-the-integration))。
1. 選取 **[!UICONTROL 屬性]**，然後選取 **[!UICONTROL 環境]** 標籤。
1. 挑選與網頁環境相關的環境層級。 然後，在 **[!UICONTROL 安裝]** 欄中，選取方塊圖示。
1. **[!UICONTROL 在Web安裝指示中]** 對話方塊中，複製完整的Experience Platform標籤程式庫內嵌程式碼，以及周圍的程式碼 `<script/>` 標籤之間。

## Dynamic Media Viewers擴充功能參考指南 {#reference-guide-for-the-dynamic-media-viewers-extension}

### 關於Dynamic Media檢視器設定 {#about-the-dynamic-media-viewers-configuration}

如果下列條件為真，Dynamic Media Viewer擴充功能會自動與Experience Platform標籤程式庫整合：

* Experience Platform標籤程式庫全域物件( `_satellite`)會顯示在頁面上。
* Dynamic Media Viewers擴充功能函式 `_dmviewers_v001()` 定義於 `_satellite`.

* `config2=` 未指定檢視器引數，這表示檢視器不會使用舊版Analytics整合。

此外，也可以透過指定以下選項在檢視器中明確停用Experience Platform標籤整合 `launch=0` 引數來設定檢視器。 此引數的預設值為 `1`.

### 設定Dynamic Media Viewers擴充功能 {#configuring-the-dynamic-media-viewers-extension}

Dynamic Media Viewers擴充功能的唯一設定選項是 **[!UICONTROL 啟用音訊和視訊的Adobe Medium Analytics]**.

勾選（啟用）此選項，且已安裝並設定Adobe Medium Analytics for Audio and Video擴充功能時，視訊播放量度會傳送至Adobe Analytics for Audio and Video解決方案。 停用此選項會關閉視訊追蹤。

如果啟用此選項 *不含* 安裝Adobe Medium Analytics for Audio and Video擴充功能後，選項沒有作用。

![image2019-7-22_12-4-23](assets/image2019-7-22_12-4-23.png)

### 關於Dynamic Media檢視器擴充功能中的資料元素 {#about-data-elements-in-the-dynamic-media-viewers-extension}

「動態媒體檢視器」擴充功能提供的唯一「資料元素」類型是「資 **[!UICONTROL 料元素類型」下拉式清單中的「檢]****** 視器事件」。

選取後，資料元素編輯器會呈現包含兩個欄位的表單：

* **[!UICONTROL DM檢視器事件資料類型]** -一個下拉式清單，可識別動態媒體檢視器擴充功能支援的所有檢視器事件 (具有引數)，加上特殊的 **[!UICONTROL COMMON]** 項目。COMMON **** 項目代表檢視器所傳送之所有類型事件的共同事件參數清單。
* **[!UICONTROL 追蹤引數]**  — 所選Dynamic Media檢視器事件的引數。

![image2019-7-22_12-5-46](assets/image2019-7-22_12-5-46.png)

請參閱 [Dynamic Media檢視器參考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers.html#viewers-aem-assets-dmc) 如需各種檢視器型別支援的事件清單，請前往特定檢視器區段，然後選取「支援Adobe Analytics追蹤」子區段。 目前，Dynamic Media檢視器參考指南不會記錄事件引數。

現在來考慮Dynamic Media Viewers的生命週期 *資料元素*. 此資料元素的值會在頁面上發生對應的Dynamic Media檢視器事件後填入。 例如，假設資料元素指向 **[!UICONTROL 載入]** 事件及其「資產」引數。 在這種情況下，檢視器執行「 」後，此資料元素的值會收到有效資料 **[!UICONTROL 載入]** 第一次執行的事件。 如果資料元素指向 **[!UICONTROL 縮放]** 事件及其「縮放」引數，在檢視器傳送 **[!UICONTROL 縮放]** 第一次執行的事件。

同樣地，當檢視器在頁面上傳送對應事件時，資料元素的值也會自動更新。即使未在規則設定中指定特定事件，也會進行值更新。例如，假設資料元素 **[!UICONTROL 縮放比例]** 是針對ZOOM事件的「縮放」引數定義的。 不過，規則設定中唯一存在的規則是由 **[!UICONTROL 載入]** 事件。 的值 **[!UICONTROL 縮放比例]** 仍會在每次使用者在檢視器內執行縮放時更新。

任何動態媒體檢視器在網頁上都有唯一識別碼。資料元素會追蹤值本身，以及填入值的檢視器。 例如，假設同一頁面上有數個檢視器，且 **[!UICONTROL 資產名稱]** 資料元素指向 **[!UICONTROL 載入]** 事件及其「資產」引數。 此 **[!UICONTROL 資產名稱]** 「資料元素」會維護與頁面上載入的每個檢視器相關聯的資產名稱集合。

資料元素傳回的確切值取決於上下文。 若資料元素是在由Dynamic Media檢視器事件觸發的規則中要求，則會為啟動規則的檢視器傳回資料元素值。 此外，資料元素請求使用的規則是由某個其他Experience Platform標籤擴充功能中的事件所觸發。 此時，資料元素的值來自上次更新此資料元素的檢視器。

**考量下列範例設定：**

* 具有兩個Dynamic Media縮放檢視器的網頁： *檢視者1* 和 *檢視者2*.

* **[!UICONTROL 縮放比例]** 資料元素指向 **[!UICONTROL 縮放]** 事件及其「縮放」引數。
* **[!UICONTROL Trackpan]** 規則與下列專案：

   * 使用Dynamic Media檢視器 **[!UICONTROL 平移]** 作為觸發器的事件。
   * 傳送值 **[!UICONTROL 縮放比例]** 資料元素重新命名為Adobe Analytics。

* **[!UICONTROL TrackKey]** 規則與下列專案：

   * 使用核心Experience Platform標籤擴充功能的按鍵事件作為觸發器。
   * 傳送值 **[!UICONTROL 縮放比例]** 資料元素重新命名為Adobe Analytics。

現在，假設使用者透過兩個檢視器載入網頁。 在 *檢視者1*，然後放大至50%縮放比例；接著放大 *檢視者2*，會放大至25%的縮放比例。 在 *檢視者1*，然後平移影像，最後在鍵盤上選取鍵。

一般使用者的活動會導致系統對Adobe Analytics進行以下兩個追蹤呼叫：

* 發生第一個呼叫是因為 **[!UICONTROL Trackpan]** 當使用者進入時觸發規則 *檢視者1*. 該呼叫傳送50%作為的值 **[!UICONTROL 縮放比例]** 資料元素，因為資料元素知道規則是由以下觸發 *檢視者1* 並擷取對應的比例值；
* 第二個呼叫的發生是因為 **[!UICONTROL TrackKey]** 當使用者按下鍵盤上的按鍵時，就會觸發規則。 該呼叫傳送25%作為的值 **[!UICONTROL 縮放比例]** 資料元素，因為檢視器未觸發規則。 因此，資料元素會傳回最新值。

上述設定的範例也會影響資料元素值的生命週期。 即使檢視器本身已放置在網頁上，Dynamic Media檢視器所管理的「資料元素」值仍會儲存在Experience Platform標籤程式庫程式碼中。 此功能表示如果非Dynamic Media Viewer擴充功能觸發規則，並參考此類資料元素，資料元素會傳回最後一個已知值。 即使檢視器不再出現在網頁上。

無論如何，Dynamic Media檢視器所驅動的資料元素值不會儲存在本機儲存空間或伺服器上，而是只會儲存在使用者端Experience Platform標籤資料庫上。 網頁重新載入時，此資料元素的值會消失。

一般而言，資料元素編輯器支援 [儲存持續時間選擇](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/data-elements.html#create-a-data-element). 不過，使用Dynamic Media檢視器擴充功能的資料元素僅支援的儲存持續時間選項： **[!UICONTROL 無]**. 您可以在使用者介面中設定任何其他值，但在此情況下不會定義資料元素行為。 擴充功能會自行管理「資料元素」的值：「資料元素」會在整個檢視器生命週期中維護檢視器事件引數的值。

### 關於Dynamic Media檢視器擴充功能中的規則 {#about-rules-in-the-dynamic-media-viewers-extension}

在規則編輯器中，擴充功能會為事件編輯器新增設定選項。 此外，編輯器也提供在動作編輯器中手動參考事件引數的選項，作為簡易選項，而不使用預先設定的資料元素。

#### 關於事件編輯器 {#about-the-events-editor}

在「事件」編輯器中， Dynamic Media Viewers擴充功能會新增 **[!UICONTROL 事件型別]** 已呼叫 **[!UICONTROL 檢視器事件]**.

選取後，事件編輯器會呈現下拉式清單 **[!UICONTROL Dynamic Media Viewer事件]**，列出Dynamic Media檢視器支援的所有可用事件。

![image2019-8-2_15-13-1](assets/image2019-8-2_15-13-1.png)

#### 關於動作編輯器 {#about-the-actions-editor}

Dynamic Media檢視器擴充功能可讓您使用Dynamic Media檢視器的事件引數，對應至Adobe Analytics擴充功能的「設定變數」編輯器中的分析變數。

最簡單的方法是完成以下兩個步驟的流程：

* 首先，定義一或多個資料元素，其中每個資料元素代表Dynamic Media Viewer事件的引數。
* 最後，在Adobe Analytics擴充功能的設定變數編輯器中，選取 **[!UICONTROL 資料元素]** 選擇器圖示（三個棧疊的磁碟）以開啟「選取資料元素」對話方塊，然後從其中選取資料元素。

![image2019-7-10_20-41-52](assets/image2019-7-10_20-41-52.png)

不過，您也可以使用替代方法並略過「資料元素」的建立。您可以直接參照Dynamic Media Viewer事件的引數。 在「 」中輸入事件引數的完整名稱 **[!UICONTROL 值]** Analytics變數指派的輸入欄位。 請務必加上百分比(%)符號。 例如，

`%event.detail.dm.LOAD.asset%`

![image2019-7-12_19-2-35](assets/image2019-7-12_19-2-35.png)

使用資料元素與直接事件引數參考之間有重要的差異。 對於資料元素，哪個事件會觸發「設定變數」動作並不重要。 觸發規則的事件可能與動態檢視器無關。 例如，從核心擴充功能中選取網頁。 但是，使用直接引數參考時，請務必確保觸發規則的事件對應到它參考的事件引數。

例如，如果 `%event.detail.dm.LOAD.asset%` 規則是由動態媒體檢視器擴充功能的 **[!UICONTROL LOAD]** 事件觸發，則參照會傳回正確的資產名稱。但是，它會傳回任何其他事件的空白值。

下表列出Dynamic Media Viewer事件及其支援的引數：

<table>
 <tbody>
  <tr>
   <td>檢視器事件名稱</td>
   <td>引數參考</td>
  </tr>
  <tr>
   <td><code>COMMON</code></td>
   <td><code>%event.detail.dm.objID%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.compClass%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.instName%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.timeStamp%</code></td>
  </tr>
  <tr>
   <td><code>BANNER</code><br /> </td>
   <td><code>%event.detail.dm.BANNER.asset%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.BANNER.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.BANNER.label%</code></td>
  </tr>
  <tr>
   <td><code>HREF</code></td>
   <td><code>%event.detail.dm.HREF.rollover%</code></td>
  </tr>
  <tr>
   <td><code>ITEM</code></td>
   <td><code>%event.detail.dm.ITEM.rollover%</code></td>
  </tr>
  <tr>
   <td><code>LOAD</code></td>
   <td><code>%event.detail.dm.LOAD.applicationname%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.asset%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.company%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.sdkversion%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.viewertype%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.viewerversion%</code></td>
  </tr>
  <tr>
   <td><code>METADATA</code></td>
   <td><code>%event.detail.dm.METADATA.length%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.METADATA.type%</code></td>
  </tr>
  <tr>
   <td><code>MILESTONE</code></td>
   <td><code>%event.detail.dm.MILESTONE.milestone%</code></td>
  </tr>
  <tr>
   <td><code>PAGE</code></td>
   <td><code>%event.detail.dm.PAGE.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.PAGE.label%</code></td>
  </tr>
  <tr>
   <td><code>PAUSE</code></td>
   <td><code>%event.detail.dm.PAUSE.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>PLAY</code></td>
   <td><code>%event.detail.dm.PLAY.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>SPIN</code></td>
   <td><code>%event.detail.dm.SPIN.framenumber%</code></td>
  </tr>
  <tr>
   <td><code>STOP</code></td>
   <td><code>%event.detail.dm.STOP.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>SWAP</code></td>
   <td><code>%event.detail.dm.SWAP.asset%</code></td>
  </tr>
  <tr>
   <td><code>SWATCH</code></td>
   <td><code>%event.detail.dm.SWATCH.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.SWATCH.label%</code></td>
  </tr>
  <tr>
   <td><code>TARG</code></td>
   <td><code>%event.detail.dm.TARG.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.TARG.label%</code></td>
  </tr>
  <tr>
   <td><code>ZOOM</code></td>
   <td><code>%event.detail.dm.ZOOM.scale%</code></td>
  </tr>
 </tbody>
</table>

## 設定所有整合專案 {#configuring-all-the-integration-pieces}

**開始之前**

Adobe建議您詳閱本節之前的所有檔案，以便瞭解完整的整合。

本節說明整合Dynamic Media檢視器與Adobe Analytics和用於音訊與視訊的Adobe Analytics所需的設定步驟。 雖然Dynamic Media檢視器擴充功能可用於Experience Platform標籤中的其他用途，但本檔案不包含這類案例。

您即將使用下列Adobe產品來設定整合：

* Adobe Analytics — 用於設定追蹤變數和報表。
* Experience Platform標籤 — 用於定義屬性、一個或多個規則以及一個或多個資料元素，以啟用檢視器追蹤。

此外，如果此整合解決方案與Experience Manager Sites搭配使用，下列設定也必須完成：

* [!DNL Adobe Developer Console]  — 會為Experience Platform標籤建立整合。
* Experience Manager製作節點 — IMS設定和Experience Platform標籤雲端設定。

在設定中，請確定您有權存取Adobe Experience Cloud中已啟用Adobe Analytics和Experience Platform標籤的公司。

## 設定Adobe Analytics以進行整合 {#configuring-adobe-analytics-for-the-integration}

設定Adobe Analytics後，系統會針對整合設定下列專案：

* 報告套裝已就位並選取。
* Analytics變數可用來接收追蹤資料。
* 報表可用來檢視Adobe Analytics中收集的資料。

另請參閱 [Analytics實作指南](https://experienceleague.adobe.com/docs/analytics/implementation/home.html).

**若要設定Adobe Analytics以進行整合：**

1. 首先從Experience Cloud存取Adobe Analytics [首頁](https://experience.adobe.com/#/home). 在功能表列上，選取 **[!UICONTROL 解決方案]** 圖示（三乘三的點表格）在頁面右上角附近，然後選取「 」 **[!UICONTROL Analytics]**.

   ![2019-07-22_18-08-47](assets/2019-07-22_18-08-47.png)

   現在選取報表套裝。

### 選取報表套裝 {#selecting-a-report-suite}

1. 在Adobe Analytics頁面的右上角，「搜尋報表」欄位的右側，從下拉式清單中選取正確的報表套裝。****&#x200B;如果有多個報表套裝可供使用，而您不確定要使用哪個報表套裝，請連絡您的Adobe Analytics管理員，以協助您選取要使用哪個報表套裝。

   在下方熒幕擷圖中，使用者建立了報表套裝，並命名為 *DynamicMediaViewersExtensionDoc* 並從下拉式清單中選取。 報表套裝名稱僅為範例名稱。 您最終選取的報表套裝名稱由您決定。

   如果沒有可用的報表套裝，您或您的Adobe Analytics管理員必須先建立一個報表套裝，然後才能繼續進行設定。

   另請參閱 [報表與報表套裝](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/report-suites-admin.html) 和 [建立報表套裝](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/t-create-a-report-suite.html).

   在Adobe Analytics中，報表套裝是在 **[!UICONTROL 管理員]** > **[!UICONTROL 報表套裝]**.

   ![2019-07-22_18-09-49](assets/2019-07-22_18-09-49.png)

   現在設定Adobe Analytics變數。

### 設定Adobe Analytics變數 {#setting-up-adobe-analytics-variables}

1. 指定一或多個Adobe Analytics變數，用來追蹤網頁上的Dynamic Media檢視器行為。

   您可以使用Adobe Analytics支援的任何變數型別。 關於變數型別的決定（如自訂流量） [prop]，轉換 [eVar])，取決於Analytics實作的特定需求。

   另請參閱 [Prop和eVar概觀](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar.html#vars).

   就本檔案而言，僅會使用自訂流量(prop)變數，因為它們在網頁上發生動作後的幾分鐘內，就能在Analytics報表中使用。

   若要啟用新的自訂流量變數，請在Adobe Analytics的工具列中，前往 **[!UICONTROL 管理員]** > **[!UICONTROL 報表套裝]**.

1. 在 **[!UICONTROL 報表套裝管理員]** 頁面上，選取正確的報表，然後在工具列中導覽至 **[!UICONTROL 編輯設定]** > **[!UICONTROL 流量]** > **[!UICONTROL 流量變數]**.
1. 選取未使用的變數，為其提供描述性名稱(**[!UICONTROL 檢視器資產(prop 30)]**)，並在「已啟用」欄中將下拉式方塊變更為「已啟用」。

   以下熒幕擷圖為自訂流量變數( **[!UICONTROL prop30]**)以追蹤檢視器所使用的資產名稱：

   ![image2019-6-26_23-6-59](assets/image2019-6-26_23-6-59.png)

1. 在變數清單底部，選取 **[!UICONTROL 儲存]**.

### 設定報表 {#setting-up-a-report}

1. 一般而言，在Adobe Analytics中設定報表是受特定專案需求的驅動。 因此，詳細報告設定不在此整合的範圍之內。

   不過，只要您在中設定自訂流量變數後，就能在Adobe Analytics中自動使用自訂流量報表了 [設定Adobe Analytics變數](#setting-up-adobe-analytics-variables).

   例如，報表 **[!UICONTROL 檢視器資產(prop 30)]** 變數可從下方的「報表」功能表取得 **[!UICONTROL 自訂流量]** > **[!UICONTROL 自訂流量21-30]** > **[!UICONTROL 檢視器資產(prop 30)]**.

   在檢視器資產(prop 30)建 **[!UICONTROL 立後立即造訪此報表]** ，不會顯示任何資料；在這個整合階段，就是預期的。

   ![image2019-6-26_23-12-49](assets/image2019-6-26_23-12-49.png)

## 設定整合的Experience Platform標籤 {#configuring-adobe-launch-for-the-integration}

設定Experience Platform標籤後，系統就會針對整合進行下列設定：

* 建立新屬性以將您的所有設定保持在一起。
* 擴充功能的安裝和設定。 屬性中安裝的所有擴充功能的使用者端程式碼會一起編譯至程式庫中。 網頁稍後會使用此資料庫。
* 資料元素和規則的設定。 此設定會定義要從Dynamic Media檢視器擷取哪些資料、何時觸發追蹤邏輯，以及在Adobe Analytics中將檢視器資料傳送至何處。
* 程式庫的發佈。

**若要設定整合的Experience Platform標籤：**

1. 首先，從Experience Cloud存取Experience Platform標籤 [首頁](https://experience.adobe.com/#/home). 在功能表列上，選取 **[!UICONTROL 解決方案]** 圖示（三乘三點表）在頁面右上角附近，然後選取「 」 **[!UICONTROL 標籤]**.

   您也可以 [直接開啟Experience Platform標籤](https://launch.adobe.com/).

   ![image2019-7-8_15-38-44](assets/image2019-7-8_15-38-44.png)

### 在Experience Platform標籤中建立屬性 {#creating-a-property-in-adobe-launch}

Experience Platform標籤中的屬性是具名設定，可讓所有設定保持在一起。 系統會產生一個組態設定程式庫，並發佈至不同的環境層級（開發、測試和生產）。

另請參閱 [建立Tags屬性](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/initial-configuration/configure-tags.html).

1. 在Experience Platform標籤中，選取 **[!UICONTROL 新增屬性]**.
1. 在「建 **[!UICONTROL 立屬性]** 」對話方塊的「名稱 **** 」欄位中，輸入描述性名稱，例如網站的標題。例如 `DynamicMediaViewersProp.`
1. 在 **[!UICONTROL 網域]** 欄位，輸入您網站的網域。
1. 在 **[!UICONTROL 進階選項]** 下拉式清單，啟用 **[!UICONTROL 設定擴充功能開發（之後無法修改）]** 如果您想使用擴充功能，在本例中， *Dynamic Media檢視器* — 尚未發行。

   ![image2019-7-8_16-3-47](assets/image2019-7-8_16-3-47.png)

1. 選取&#x200B;**[!UICONTROL 儲存]**。

   選取新建立的屬性，然後繼續前往 *擴充功能的安裝和設定*.

### 安裝及設定擴充功能 {#installing-and-setup-of-extensions}

「Experience Platform標籤」中所有可用的擴充功能都會列於 **[!UICONTROL 擴充功能]** > **[!UICONTROL 目錄]**.

若要安裝擴充功能，請選取 **[!UICONTROL 安裝]**. 如有需要，請執行一次性擴充功能組態，然後選取「 」 **[!UICONTROL 儲存]**.

必要時，必須安裝並設定下列擴充功能：

* （必要） *Experience CloudID服務* 副檔名。

無需額外設定，接受任何建議值。 完成後，請務必選取 **[!UICONTROL 儲存]**.

另請參閱 [Adobe Experience Cloud Identity Service擴充功能](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/id-service/overview.html).

* （必要） *Adobe Analytics* 副檔名

若要設定此擴充功能，您需要在Adobe Analytics中找到的報表套裝ID，位於 **[!UICONTROL 管理員]** > **[!UICONTROL 報表套裝]**，位於 **[!UICONTROL 報告套裝ID]** 欄標題。

(僅供展示之用， **[!UICONTROL DynamicMediaViewersExtensionDoc]** 報表套裝用於下列熒幕擷取畫面中。 此ID已建立並用於 [選取報表套裝](#selecting-a-report-suite) 較早。)

![image2019-7-8_16-45-34](assets/image2019-7-8_16-45-34.png)

在「安裝擴充功能」頁面的「開發報表套裝」欄位中，輸入「報表套裝ID」。此欄位包括「 **[!UICONTROL 測試報表套裝」欄位和「]** 生產報表套裝 ******** 」欄位。

![image2019-7-8_16-47-40](assets/image2019-7-8_16-47-40.png)

*只有在您打算使用視訊追蹤時，才設定下列專案：*

在 **[!UICONTROL 安裝擴充功能]** 頁面，展開 **[!UICONTROL 一般]**，然後指定追蹤伺服器。 追蹤伺服器會遵循範本 `<trackingNamespace>.sc.omtrdc.net`，其中 `<trackingNamespace>` 是在布建電子郵件中取得的資訊。

選取&#x200B;**[!UICONTROL 儲存]**。

另請參閱 [Adobe Analytics擴充功能](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/analytics/overview.html).

* （選用；只有在需要視訊追蹤時才需要） *Adobe Medium Analytics for Audio and Video* 副檔名

填寫追蹤伺服器欄位。 的追蹤伺服器 *Adobe Medium Analytics for Audio and Video* 擴充功能與用於Adobe Analytics的追蹤伺服器不同。 它會依循範本 `<trackingNamespace>.hb.omtrdc.net`，其中 `<trackingNamespace>` 是來自布建電子郵件的資訊。

所有其他欄位都是選用的。

另請參閱 [Adobe Medium Analytics for Audio and Video擴充功能](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/media-analytics/overview.html).

* （必要） *Dynamic Media檢視器* 副檔名

選取 **[!UICONTROL 啟用Adobe Analytics for Video]** ，以啟用 (開啟) 視訊心率追蹤。

截至本文撰寫， *Dynamic Media檢視器* 擴充功能僅在建立Experience Platform標籤屬性以供開發時才能使用。

另請參閱 [在Experience Platform標籤中建立屬性](#creating-a-property-in-adobe-launch).

安裝並設定擴充功能後，擴充功能>已安裝區域至少會列出下列五個擴充功能（若您未追蹤視訊，則四個）。

![image2019-7-22_12-7-36](assets/image2019-7-22_12-7-36.png)

### 設定資料元素和規則 {#setting-up-data-elements-and-rules}

在Experience Platform標籤中，建立追蹤Dynamic Media檢視器所需的資料元素和規則。

另請參閱 [資料和事件追蹤在整合中的運作方式](#how-data-and-event-tracking-works-in-the-integration) 以取得使用Experience Platform標籤追蹤的概觀。

另請參閱 [設定範例](#sample-configuration) ，檢視Experience Platform標籤中示範如何在檢視器載入時追蹤資產名稱的設定範例。

另請參閱 [設定Dynamic Media Viewers擴充功能](#configuring-the-dynamic-media-viewers-extension) 以取得有關擴充功能功能的深入資訊。

### 發佈程式庫 {#publishing-a-library}

若要變更Experience Platform標籤設定（包括屬性、擴充功能、規則和設定的資料元素），您必須 *發佈* 這類變更。 從「屬性」設定下的「發佈」標籤中，執行「Experience Platform標籤」中的發佈。

Experience Platform標籤可能具有多個開發環境、一個測試環境及一個生產環境。 根據預設，Experience Manager中的「Experience Platform標籤雲端設定」會將Experience Manager作者節點指向Experience Platform標籤的「預備」環境。 「Experience Manager發佈」節點指向Experience Platform標籤的生產環境。 這種排列表示在預設Experience Manager設定下，必須將Experience Platform標籤程式庫發佈到測試環境。 如此可讓您在Experience Manager作者中使用它。 然後，您可以將其發佈到生產環境，以便用於Experience Manager發佈。

另請參閱 [環境](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/environments/environments.html?lang=zh-Hant) 以取得有關Experience Platform標籤環境的詳細資訊。

發佈程式庫需執行下列兩個步驟：

* 將所有必要的變更（新變更和更新）加入程式庫，以新增和建立新程式庫。
* 在不同環境層級（從開發到測試與生產）中向上移動程式庫。

#### 新增及建置新程式庫 {#adding-and-building-a-new-library}

1. 第一次在Experience Platform標籤中開啟「發佈」標籤時，資料庫清單是空的。

   在左欄中選取 **[!UICONTROL 新增程式庫]**.

   ![image2019-7-15_14-43-17](assets/image2019-7-15_14-43-17.png)

1. 在「建立新程式庫」頁面的 **[!UICONTROL 名稱]** 欄位，輸入新程式庫的描述性名稱。 例如，

   *DynamicMediaViewersLib*

   從「環境」下拉式清單中，選擇「環境」層級。 一開始，只有開發層級可供選取。 在頁面的左下角附近，選取 **[!UICONTROL 新增所有變更的資源]**.

   ![image2019-7-15_14-49-41](assets/image2019-7-15_14-49-41.png)

1. 在頁面的右上角附近，選取 **[!UICONTROL 儲存並為開發環境建置]**.

   幾分鐘後，程式庫就會建立並準備使用。

   ![image2019-7-15_15-3-34](assets/image2019-7-15_15-3-34.png)

   >[!NOTE]
   >
   >下次變更Experience Platform標籤設定時，請前往 **[!UICONTROL 發佈]** 標籤下的 **[!UICONTROL 屬性]** 設定，然後選取您先前建立的程式庫。
   >
   >
   >在程式庫發佈畫面中，選取「 」 **[!UICONTROL 新增所有變更的資源]**，然後選取 **[!UICONTROL 儲存並為開發環境建置]**.

#### 在環境層級中向上移動程式庫 {#moving-a-library-up-through-environment-levels}

1. 新增程式庫後，即可在開發環境中找到該程式庫。 若要將其移至中繼環境層級（與已提交欄相對應），請從程式庫的下拉式功能表中選取 **[!UICONTROL 提交以進行核准]**.

   ![image2019-7-15_15-52-37](assets/image2019-7-15_15-52-37.png)

1. 在確認對話方塊中選取 **[!UICONTROL 提交]**.

   程式庫移至已提交欄後，從程式庫的下拉式功能表中選取 **[!UICONTROL 為測試環境建置]**.

   ![image2019-7-15_15-54-37](assets/image2019-7-15_15-54-37.png)

1. 若要將程式庫從測試環境移至生產環境（亦即「已發佈」欄），請遵循類似的程式。

   首先，從下拉式功能表中選取 **[!UICONTROL 核准以發佈]**.

   ![image2019-7-15_16-7-39](assets/image2019-7-15_16-7-39.png)

1. 從下拉式功能表中選取 **[!UICONTROL 建置並發佈到生產環境]**.

   ![image2019-7-15_16-8-9](assets/image2019-7-15_16-8-9.png)

   另請參閱 [發佈](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/overview.html) 以取得Experience Platform標籤中發佈程式的詳細資訊。

## 設定Adobe Experience Manager以進行整合 {#configuring-adobe-experience-manager-for-the-integration}

先決條件:

* Experience Manager會執行作者和發佈執行個體。
* Experience Manager作者節點設定於Dynamic Media - Scene7執行模式(dynamicmedia_s7)
* Dynamic Media WCM元件會在Experience Manager Sites中啟用。

Experience Manager設定包含下列兩個主要步驟：

* Experience ManagerIMS的設定。
* Experience Platform標籤雲端的設定。

### 設定Experience ManagerIMS {#configuring-aem-ims}

1. 在Experience Manager作者中，選取 **[!UICONTROL 工具]** 圖示（槌子），然後前往 **[!UICONTROL 安全性]** > **[!UICONTROL Adobe IMS設定]**.

   ![2019-07-25_11-52-58](assets/2019-07-25_11-52-58.png)

1. 在「AdobeIMC設定」頁面的左上角附近，選取 **[!UICONTROL 建立]**.
1. 在 **[!UICONTROL Adobe IMS技術帳戶設定]** 頁面，在 **[!UICONTROL 雲端解決方案]** 下拉式清單，選取 **[!UICONTROL Experience Platform標籤]**.
1. 啟用 **[!UICONTROL 建立新憑證]**，然後在文字欄位中，為您的憑證輸入任何有意義的值。 例如， *AdobeLaunchIMSert*. 選取 **[!UICONTROL 建立憑證]**.

   會顯示下列資訊訊息：

   *若要擷取有效的存取Token，新憑證的公開金鑰會新增至Adobe Developer Console上的技術帳戶！*

   若要關閉「資訊」對話方塊，請選取 **[!UICONTROL 確定]**.

   ![2019-07-25_12-09-24](assets/2019-07-25_12-09-24.png)

1. 若要下載公開金鑰檔案(&#42;.crt)，選取 **[!UICONTROL 下載公開金鑰]**.

   >[!NOTE]
   >
   >此時， ***保持開啟*** 此 **[!UICONTROL Adobe IMS技術帳戶設定]** 頁面； ***不要*** 關閉頁面並 ***不要*** 選取「下一步」。 您稍後將在步驟中返回此頁面。

   ![2019-07-25_12-52-24](assets/2019-07-25_12-52-24.png)

1. 在新的瀏覽器標籤中，瀏覽至 [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/integrations).

1. 從 **[!UICONTROL Adobe Developer主控台整合]** 頁面，右上角附近，選取 **[!UICONTROL 新整合]**.
1. 在 **[!UICONTROL 建立新的整合]** 對話方塊，確認 **[!UICONTROL 存取API]** 已選取選項按鈕，然後選取 **[!UICONTROL 繼續]**.

   ![2019-07-25_13-04-20](assets/2019-07-25_13-04-20.png)

1. 於第二個 **[!UICONTROL 建立新的整合]** 頁面，啟用（開啟） **[!UICONTROL Experience Platform標籤API]** 選項按鈕。 在頁面的右下角，選取 **[!UICONTROL 繼續]**.

   ![2019-07-25_13-13-54](assets/2019-07-25_13-13-54.png)

1. 於第三個 **[!UICONTROL 建立新的整合]** 頁面，請執行下列動作：

   * 在 **[!UICONTROL 名稱]** 欄位，輸入描述性名稱。 例如， *DynamicMediaViewersIO*.

   * 在 **[!UICONTROL 說明]** 欄位，輸入整合的說明。

   * 在 **[!UICONTROL 公開金鑰憑證]** 區域，上傳您的公開金鑰檔案(&#42;.crt)之前，您在這些步驟中下載的檔案。

   * 在 **[!UICONTROL 選取Experience Platform標籤API的角色]** 標題，選取 **[!UICONTROL 管理員]**.

   * 在 **[!UICONTROL 為Experience Platform標籤API選取一或多個產品設定檔]** 標題，選取名為的產品設定檔 **[!UICONTROL 標籤 —  &lt;your_company_name>]**.

   ![2019-07-25_13-49-18](assets/2019-07-25_13-49-18.png)

1. 選取 **[!UICONTROL 建立整合]**.
1. 在 **[!UICONTROL 已建立整合]** 頁面，選取 **[!UICONTROL 繼續檢視整合詳細資訊]**.

   ![2019-07-25_14-16-33](assets/2019-07-25_14-16-33.png)

1. 整合詳細資訊頁面隨即顯示， **** 類似於以下內容：

   >[!NOTE]
   >
   >***請離開此「整合詳細資訊」頁面***。您將會需要 **[!UICONTROL 概觀]** 和 **[!UICONTROL JWT]** 快速定位。

   ![2019-07-25_14-35-30](assets/2019-07-25_14-35-30.png)

   整合詳細資訊頁面。

1. 返回您先前 **[!UICONTROL 未開啟的「Adobe IMS技術帳戶設定]** 」頁面。在頁面的右上角，選取 **[!UICONTROL 下一個]** 以開啟 **[!UICONTROL 帳戶]** 中的頁面 **[!UICONTROL Adobe IMS技術帳戶設定]** 視窗。

   (如果您先前關閉頁面，請返回Experience Manager作者，然後導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL Adobe IMS設定]**. 選擇 **[!UICONTROL 建立]**。在 **[!UICONTROL 雲端解決方案]** 下拉式清單，選取 **[!UICONTROL Experience Platform標籤]**. 在 **[!UICONTROL 憑證]** 下拉式清單，選取先前建立之憑證的名稱。)

   ![2019-07-25_20-57-50](assets/2019-07-25_20-57-50.png)

   Adobe IMS技術帳戶設定 — 憑證頁面。

1. 此 **[!UICONTROL 帳戶]** 頁面有五個欄位，您必須使用上一步驟整合詳細資訊頁面中的資訊來填寫。

   ![2019-07-25_20-42-45](assets/2019-07-25_20-42-45.png)

   Adobe IMS技術帳戶設定 — 帳戶頁面。

1. 在 **[!UICONTROL 帳戶]** 請填入下列欄位：

   * **[!UICONTROL 標題]**  — 輸入描述性科目標題。
   * **[!UICONTROL 授權伺服器]**  — 返回您先前開啟的整合詳細資訊頁面。 選取 **[!UICONTROL JWT]** 標籤。 複製伺服器名稱（不含路徑），如下方反白所示。

   返回「帳 **[!UICONTROL 戶]** 」頁面，然後將名稱貼到相應欄位。例如， `https://ims-na1.adobelogin.com/`
（伺服器名稱僅供範例使用）

   ![2019-07-25_15-01-53](assets/2019-07-25_15-01-53.png)

   整合詳細資訊頁面 — JWT索引標籤

1. **[!UICONTROL API金鑰]** -返回「整合詳細資訊」頁面。選取 **[!UICONTROL 概觀]** 標籤，然後在右側 **[!UICONTROL API金鑰（使用者端ID）]** 欄位，選取 **[!UICONTROL 複製]**.

   返回「帳 **[!UICONTROL 戶]** 」頁面，然後將金鑰貼入個別欄位。

   ![2019-07-25_14-35-333](assets/2019-07-25_14-35-333.png)

   整合詳細資訊頁面。

1. **[!UICONTROL 用戶端密碼]**-返回「整合詳細資訊」頁面。從 **[!UICONTROL 概觀]** 索引標籤，選取 **[!UICONTROL 擷取使用者端密碼]**. 右側 **[!UICONTROL 使用者端密碼]** 欄位，選取 **[!UICONTROL 複製]**.

   返回「帳 **[!UICONTROL 戶]** 」頁面，然後將金鑰貼入個別欄位。

1. **[!UICONTROL 裝載]**  — 返回「整合詳細資訊」頁面。 從 **[!UICONTROL JWT]** 索引標籤中的「JWT裝載」欄位，複製整個JSON物件程式碼。

   返回「帳 **[!UICONTROL 戶]** 」頁面，然後將程式碼貼至個別欄位。

   ![2019-07-25_21-59-12](assets/2019-07-25_21-59-12.png)

   整合詳細資訊頁面 — JWT索引標籤

   「帳戶」頁面（已填寫所有欄位）看起來類似以下內容：

   ![2019-07-25_22-08-30](assets/2019-07-25_22-08-30.png)

1. 靠近的右上角 **[!UICONTROL 帳戶]** 頁面，選取 **[!UICONTROL 建立]**.

   在設定Experience Manager IMS後，您現在有新的IMSAccount列於下 **[!UICONTROL Adobe IMS設定]**.

   ![image2019-7-15_14-17-54](assets/image2019-7-15_14-17-54.png)

## 設定Experience Platform標籤雲端以整合 {#configuring-adobe-launch-cloud-for-the-integration}

1. 在Experience Manager author的左上角附近，選取 **[!UICONTROL 工具]** 圖示（槌子），然後前往 **[!UICONTROL Cloud Service]** > **[!UICONTROL Experience Platform標籤設定]**.

   ![2019-07-26_12-10-38](assets/2019-07-26_12-10-38.png)

1. 在 **[!UICONTROL Experience Platform標籤設定]** 頁面，在左側面板中，選取您要套用Experience Manager標籤設定的Experience Platform網站。

   僅供範例使用， **`We.Retail`** 已選取底下熒幕擷圖中的網站。

   ![2019-07-26_12-20-06](assets/2019-07-26_12-20-06.png)

1. 在頁面的左上角附近，選取 **[!UICONTROL 建立]**.
1. 在 **[!UICONTROL 一般]** 頁面（1/3頁） **[!UICONTROL 建立Experience Platform標籤設定]** 視窗，填寫下列欄位：

   * **[!UICONTROL 標題]**  — 輸入描述性設定標題。 例如，`We.Retail Tags cloud configuration`。

   * **[!UICONTROL 相關聯的Adobe IMS設定]**  — 選取您先前在中建立的IMS設定 [設定Experience ManagerIMS](#configuring-aem-ims).

   * **[!UICONTROL 公司]**  — 從 **[!UICONTROL 公司]** 從下拉式清單中，選取您的Experience Cloud公司。 清單會自動填入。

   * **[!UICONTROL 屬性]**  — 從「屬性」下拉式清單中，選取您先前建立的「Experience Platform標籤」屬性。 清單會自動填入。

   完成所有欄位後，您的 **[!UICONTROL 一般]** 頁面外觀如下：

   ![image2019-7-15_14-34-23](assets/image2019-7-15_14-34-23.png)

1. 在左上角附近，選取 **[!UICONTROL 下一個]**.
1. 在 **[!UICONTROL 分段]** 頁面（2/3頁） **[!UICONTROL 建立Experience Platform標籤設定]** 視窗中，填寫下列欄位：

   在 **[!UICONTROL 資料庫URI]** （統一資源識別碼）欄位，檢查Experience Platform標籤程式庫的測試版本位置。 Experience Manager會自動填入此欄位。

   此步驟使用部署至Experience PlatformCDN的Adobe標籤程式庫僅供範例用途之用。

   >[!NOTE]
   >
   >檢查以確定自動填入的資料庫URI （統一資源識別碼）的格式不正確。 如有必要，請修正此錯誤，使URI代表協定相對URI。 也就是說，它會從雙正斜線開始。
   >
   >
   >例如：`//assets.adobetm.com/launch-xxxx`。

   您的 **[!UICONTROL 分段]** 頁面可能會顯示類似下列內容。 此 **[!UICONTROL 封存]** 和 **[!UICONTROL 非同步載入程式庫]** 選項包括 ***非*** 設定：

   ![image2019-7-15_15-21-8](assets/image2019-7-15_15-21-8.png)

1. 在右上角附近，選取 **[!UICONTROL 下一個]**.
1. 在 **[!UICONTROL 生產]** 頁面（3/3頁） **[!UICONTROL 建立Experience Platform標籤設定]** 視窗視需要修正自動填入的生產URI，就像在上一個視窗完成時一樣 **[!UICONTROL 分段]** 頁面。
1. 在右上角附近，選取 **[!UICONTROL 建立]**.

   您的新Experience Platform標籤雲端設定現已建立，並列於您的網站旁，類似於以下範例：

1. 選取您的新Experience Platform標籤雲端設定（選取時，設定標題左側會出現核取標籤）。 在工具列上，選取 **[!UICONTROL 發佈]**.

   ![image2019-7-15_15-47-6](assets/image2019-7-15_15-47-6.png)

目前，Experience Manager作者不支援整合Dynamic Media Viewers與Experience Platform標籤。

但是，Experience Manager發佈節點支援此功能。 使用Experience Platform標籤雲端設定的預設設定，Experience Manager發佈節點會使用Experience Platform標籤的生產環境。 因此，每次在測試期間，都必須將Experience Platform標籤程式庫更新從開發推送至生產環境。

您可以繞過此限制。 在上述Experience Manager發佈節點的Experience Platform標籤雲端設定中，指定Platform標籤程式庫的開發或預備URL。 這麼做會讓Experience Manager發佈節點使用Experience Platform標籤程式庫的開發或測試版本。

另請參閱 [透過以下方式整合Experience Manager與Experience Platform標籤 [!DNL Adobe Developer Console]](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-data-collection-tags/overview.html) 以取得關於設定Experience Platform標籤雲端設定的詳細資訊。
