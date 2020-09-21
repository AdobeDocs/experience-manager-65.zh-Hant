---
title: '[!DNL Adobe Experience Manager] 6.5舊版Service Pack發行說明。'
description: ' [!DNL Adobe Experience Manager] 6.5 Service Pack的發行說明。'
contentOwner: AK
translation-type: tm+mt
source-git-commit: 5db4dd7ccc7d722f0503b22fdd5ff9e5508be4ea
workflow-type: tm+mt
source-wordcount: '11482'
ht-degree: 0%

---


# 舊版Service Pack中包含的修補程式和功能套件 {#hotfixes-and-feature-packs-included-in-previous-service-packs}

## [!DNL Adobe Experience Manager] 6.5.5.0 {#experience-manager-6550}

Adobe Experience Manager 6.5.5.0是重要的更新，其中包括自2019年4月6.5版正式發行以來，新功能、客戶要求的重要增強功能，以及效能、穩定性和安全性 **增強**。 它可安裝在Adobe Experience Manager 6.5之上。

6.5.5.0中引進的一些主要 [!DNL Adobe Experience Manager] 功能和增強功能包括：

* 不允許匿名存取CRXDE Lite。 而是將使用者導向登入畫面。 請參 [閱使用CRXDE Lite開發](/help/sites-developing/developing-with-crxde-lite.md)。

* 自訂顯示在「收件匣」中的欄 [!DNL Adobe Experience Manager] 名稱。

* 已改善Experience Manager Web Content Management(WCM)中各個區域的協助功能，例如頁面編輯器、核心元件、RTE和管理員使用者介面。

* 將草稿 [!DNL Interactive Communication] 另存為。

* 在JEE上 [!DNL Oracle WebLogic 12] 支援Experience Manager Forms。

* 已改善使用者介面流 [!DNL Adobe Experience Manager Assets] 程中的例外處理。

* 若要取得Dynamic Media Scene7的發佈URL，會在介面中新 `getRemoteAssetPublishURL` 增新的 `com.day.cq.dam.api.s7dam.scene7.ImageUrlApi` 方法。

* [符合Web內容協助](#assets-6550)[!DNL Adobe Experience Manager Assets] 工具准則(WCAG)的協助工具增強功能。

* 已從Adobe Experience Manager移除套件共用整合。

* 內建儲存庫(Apache Jackrabbit Oak)已更新至1.22.3版。

如需Experience Manager 6.5 Service Pack 5中新增功能、主要重點、主要功能的完整清單，請參閱「 [Adobe Experience Manager 6.5 Service Pack 5的新增功能」](new-features-latest-service-pack.md) 。

以下是6.5.5.0版中提供 [!DNL Experience Manager] 的修正清單。

### [!DNL Sites] {#sites-6550}

* Experience Manager Sites提供從別名發佈或取消發佈頁面的選項。 該選項無效(NPR-33415)。
* 從包含多個範本的範本刪除版面容器時，範本無法正確呈現(NPR-33347)。
* 當Experience Manager Sites頁面是包含多個即時副本的大型內容集的一部分時，頁面版本歷史記錄預覽無法載入(NPR-33311)。
* 當您使用「移動」命令來重新命名Experience Manager Sites頁面時，不會更新頁面標題(NPR-33264)。
* 當您在欄檢視中移動頁面時，欄會消失(NPR-33216)。
* 當語言副本中的本地元件名稱與Blueprint中的元件名稱相同且從Blueprint中推出該元件時，不會將該術語添加到本地元件的名稱中( `_msm_moved` NPR-33208)。
* 「頁面重新導向servlet」會附加。html至Experience Manager Sites URL，而ResourceType則不 `cq:Page` 在此URL中(NPR-33176)。
* 貼上子樹時，沒有選項可決定是否貼上相應的子頁(NPR-33149)。
* 元件即時使用結果的數目限制為49(NPR-33058)。
* 當內容片段以架構為基礎且包含強制文字區域或路徑欄位時，內容片段無法儲存(NPR-33007)。
* 當您使用預設的Experience Fragment元件建立自訂元件並在Experience Manager Sites頁面中使用時，Experience Manager不會顯示自訂元件的參考（使用）(NPR-32852)。
* 當更名具有大量引用的資料夾時，不會更新該資料夾的許多引用(NPR-32765)。
* 當您啟用來源編輯選項時，它將可用於內嵌全螢幕選項，但在富格文本編輯器的編輯對話框和全螢幕選項中仍會遺失(NPR-32763)。
* 如果您有多欄位，且其在Blueprint的頁面屬性中包含必填欄位（例如下拉式清單或路徑欄位），則當卷出包含此多欄位的頁面時，即時副本的頁面屬性不會儲存(NPR-32751)。
* 螢幕閱讀程式無法使用標題結構來導覽頁面。 此外，「元件」標籤有錯誤的標籤(NPR-32648)。
* 當分頁開始時，「體驗片段選擇器」不會載入所有項目(NPR-32605)。
* 讀取、修改、建立和刪除即時副本的作者權限將被撤銷。 每個作者都必須明確提供讀取和修改權限，才能在Blueprint中移動頁面(NPR-32550)。
* 內容作者無法針對與Adobe Analytics整合的頁面建立Launch(NPR-32548)。
* 當使用者以同步方式繼承時，父頁面的即時副本不會與Blueprint同步，並顯示不正確的狀態(NPR-32500)。
* 載入Experience Manager Sites編輯器頁面需要超過15秒(NPR-32413)。
* 某些欄位不顯示取消繼承選項(NPR-32362)。
* 當您選取「體驗片段」元件的路徑並選取「開啟選取對話方塊」核取方塊時，不會導覽至「路徑瀏覽器」中的選取路徑(NPR-32308)。
* 從Experience Manager 6.2升級至Experience Manager 6.5時，靜態範本的Parsys元件無法正確顯示。 Parsys元件的高度設定為0，其內部元件不可見(NPR-33663)。
* 當使用者複製並貼上相同頁面上的「版面容器」時，「版面容器」中的元件不會顯示(NPR-33648)。
* Dispatcher health check在日 `Invalid cookie header` 志檔案中顯示警告消息(NPR-33629)。
* PreferencesServlet中反映的XSS(NPR-33438)。
* 匿名使用者可存取CRXDE Lite功能(GRANITE-27790)。

### [!DNL Assets] {#assets-6550}

>[!IMPORTANT]
>
>建議Windows使 [!DNL Experience Manager desktop app] 用者升級至 [案頭應用程式版本2.0.3.2](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/release-notes.html#whats-new-added) ，以存取例項上的DAM存放 [!DNL Adobe Experience Manager 6.5.5.0] 庫。 因為他們在使用案頭應用程式2.0.2版存取 [!DNL Adobe Experience Manager] 6.5.5.0例項上的DAM儲存庫時可能會遇到問題。

**Experience Manager Assets中的協助工具增強功能**

* 現在，您可以將鍵盤焦點放在「 [!UICONTROL Comments] 」清單上，並在「在時間軸中建立資產的Create new version [!UICONTROL panel(NPR-33424)」下，將可點選的選項放在「] Comments  」版本的「注釋」下。

* 現在可以使用鍵盤 [!UICONTROL 按鍵，觸及資產的「檢視設定] 」選項，並變更「 [!UICONTROL 檢視設定] 」對話方塊中的設定(NPR-33420)。

* 組合方塊的清單方塊快顯視窗（位於不同頁面的各欄位中）現在會將項目顯示為螢幕閱讀程式可宣佈的選項清單(NPR-33516)。

* 螢幕閱讀程式現在會公佈可排序標題(在清單檢視、時間軸檢視和 [!UICONTROL Manage Publication] page)的排序功能，而欄標題的排序控制項可透過鍵盤存取(NPR-32979)。

* 可點選的元素，例如註解卡、版本更新、組合方塊和功能表的雪佛龍圖示，現在可以使用鍵盤加以關注並與之互動(NPR-33514)。

* 螢幕閱讀程式現在可正確宣佈前瞻分析檢視( [!UICONTROL Insights View] )上前瞻分析圖示（用途、印象和點按）的功能（或動作目的）(NPR-33513)。

* 唯讀表單欄位(例如，資產屬性 [!UICONTROL Basic] （基本）標籤上停用的欄位 )現在可以使用鍵盤(NPR-33493、CQ-4273031)加以集中。

* 現在，各種輸入欄位中的標籤都是永久標籤（因此可存取），而不只是預留位置標籤，在輸入文字時就會消失(NPR-33475)。

* 不同的標題級別（如頁標題和部分標題）現在被視為螢幕閱讀器用戶具有不同級別的標題(NPR-33471)。

* 互動式使用者介面元素，例如連結和選項（在資產頁面的標題和縮放選項、檔案夾導覽），現在可使用鍵盤存取(NPR-33468、CQ-4271412)。

* 「管 [!UICONTROL 理出版物]頁面」螢幕上的「選項」、「範圍」和「工作流程」進度指  標現在可正確讀出為「管理出版物頁面」讀取器，而非標籤(NPR-33416)。

* 星號分級圖示的顏色(例如在資產 [!UICONTROL Properties] （屬性） [!UICONTROL Advanced（屬性）標籤的Rating] （評分）區段或在卡片檢視中)會變更，以便視覺有限且無色彩感知的使用者可看見適當的對比(NPR-33414)。

* 現在，使用鍵盤 [!UICONTROL 鍵(NPR-33397)可存取資產詳細資訊頁面上「Comment] 」（註解）欄位旁的Chevron向上箭頭。

* 畫面閱讀程式現在可正確 [!UICONTROL 宣佈資產屬性(] Properties  )和左側導軌導覽（在資產使用者介面上）上的「標籤(Tags)」對話方塊的展開和收合狀態(NPR-33396)。

* Titles of all the browsed pages on [!DNL Adobe Experience Manager] Assets are now unique (NPR-33343).

* 當導覽樹狀結構時，螢幕閱讀程式現在會正確宣佈樹狀檢視控制的各種元素(NPR-33304)。

* 使用鍵盤按鍵，現 [!UICONTROL 在可存取資產詳細資訊頁面上] 「時間軸」檢視中不同版本的資產(NPR-33283)。

* 現在螢幕閱讀程式在使用搜尋功能時，會公佈顯示在Omnisearch組合方塊中的搜尋建議名稱(NPR-33280)。

* 螢幕閱讀程式 [!UICONTROL 現在會將可點按的元素和] 「跳至  參考」邊欄中的連結宣佈為可點按的元素(NPR-33278)。

* 當對話方塊開啟時，螢幕閱讀程式不會再公佈「共用連結  」對話方塊的表格結構資訊（例如列1、儲存格1、表格）(NPR-33268)。

* 螢幕閱讀程式現在可正確宣佈各種組合方塊元素（例如「路徑」欄位和在「資產屬性」的「基本」索引標籤中開啟「選擇」對話方塊的選項）的用途(NPR-33235)。

* 現在，當鍵盤焦點位於螢幕閱讀器用戶上時，會將清單視圖表中可選擇的行的資訊發送給螢幕閱讀器用戶。 當指針懸停在行上時，螢幕閱讀器會宣佈該資訊(NPR-33234)。

* 現在，螢幕閱讀器( [!UICONTROL NPR-33206])可以訪問用於刪除Basic [!UICONTROL （屬性）頁籤的Basic] （基本）選 [!UICONTROL 項卡中Basic] （屬性）頁籤下的Selected Tags(Basic(Basic  )欄位下的每個選定標籤的選項（具有x）。

* 日曆日期選擇器現在可由螢幕閱讀器使用者和有視覺的鍵盤使用者使用鍵盤進行集中和操作(NPR-33200)。

* 切換以在清單檢視和卡片檢視之間切換，現在可正確將其功能（調整檢視）顯示給螢幕閱讀程式(NPR-33069)。

* 現在可存取左側導軌中的功能表。 螢幕閱讀程式已適當宣佈擴充功能表的功能與用途(NPR-33068)。

* 清單方塊和許多其他使用者介面元素現在可供無視的螢幕閱讀程式使用者存取，螢幕閱讀程式會公佈下列相關資訊(NPR-33040):

   * 在提交表單之前，是否需要在元素上輸入使用者。
   * 元素是否不可編輯。
   * 是否選取介面工具集。

* 開啟篩選邊欄的選項現在可使用鍵盤存取(NPR-32842、CQ-4273018)。

* 現在可存取清單檢視欄標題中的核取方塊控制項，螢幕閱讀程式已宣佈使用此控制項的目的(NPR-32722、NPR-33005)。

* 日曆日期選擇器中小時(HH)和分鐘(mm)欄位的標籤現在是永久標籤，而非預留位置標籤，而且當使用者在這些欄位中輸入文字時，不會消失(NPR-32720)。

* 通知的連結文字（在按一下鐘鈴圖示後出現）現在會向螢幕閱讀程式使用者宣佈，讓使用者使用標籤來存取每個連結(NPR-32645)。

* [!UICONTROL 現在]，您可 [!UICONTROL 以使用鍵盤(NPR-32609)，在Asset cards](資產卡 [!UICONTROL )中選擇「下載」、「屬性」和「更多操作」選項(More Actions] on asset cards in Hinsights View Are access)。

* 當使用鍵盤存取時，螢幕閱讀程式不會再公佈視覺化隱藏內容（例如搜尋結果上標題選單列的內容）(NPR-32606)。

* 螢幕閱讀程式現在已宣佈，控制項標籤在日曆日期選擇器中移至下個月和前幾個月的用途(NPR-32604)。

* 星號分級圖示現在可以使用鍵盤按鍵來集中執行(NPR-32513)。

* 控制視訊音量的功能現在可透過標籤（聚焦在音量滑桿上）和鍵盤上的箭頭鍵（調整音量）存取(NPR-32065)。

* 「檔案大小」篩選器的下界([!UICONTROL From])和上界(To)輸入欄位的用途現在已向無視螢幕閱讀器使用者宣佈(NPR-32064)。

* 現在 [!UICONTROL 瀏覽模式] ，螢幕閱讀者可以存取「  建立和翻譯」表單中的「語言」功能表(CQ-4293906)。

* 現 [!UICONTROL 在可存取] 「參考」面板，並具備下列增強功能(NPR-33261、CQ-4293798):

   * 在瀏覽模式中，螢幕閱讀程式的焦點不會再移至「網站參考」、「資產參考」、「復本」和「表單參考」區段下的隱藏多行編輯欄位 [!UICONTROL (Site]References [!UICONTROL )、「]Copies [!UICONTROL 」和「] Form References」區段下。

   * 螢幕閱讀程式現在會宣佈網站參 [!UICONTROL 考和語言][!UICONTROL 復本元素的角色] 。

   * 瀏覽模式中螢幕閱讀器的焦點以有意義的順序轉移到各種元素。

* [!UICONTROL 中繼資料結構編輯器] (Metadata Schema Editor)頁面及其元素現在可使用鍵盤存取，而且螢幕閱讀器方便使用(CQ-4290962、CQ-4272953)。

* 螢幕閱 `X` 讀程式現在會宣佈移除選取標籤的符號用途，以及選取標籤的數目(CQ-4273017)。

* 為避免使用螢幕閱讀程式的無視使用者混淆，螢幕閱讀程式現在會忽略裝飾性圖示和影像(CQ-4272944)。

**Experience Manager Assets中修正的問題**

[!DNL Adobe Experience Manager] 6.5.5.0 Assets可修正下列問題：

* [!UICONTROL 系列中] 「建立工  作流程」對話方塊上的「開始」選項已停用，因此無法觸發工作流程(NPR-32471)。

* 在中繼資料結構中使用階層式快顯功能時，在選取並儲存包含縮寫符號的下拉式選項（從子下拉式清單）時，在重新開啟資產 [!UICONTROL Properties] (NPR-32649)後，選取的縮寫符號選項就會消失。

* [!UICONTROL 如果Asset Insights Sync Job遇到無效項目（在Analytics端）而未移至下一個項目(NPR-32674)，則會停止Asset Insights Sync Job] （資產分析同步工作）並失敗。

* 由於全景檢視器中的行動瀏覽器預設會停用運動感應器，因此陀螺儀無法運作(CQ-4272937)。

* [!UICONTROL 在6.5.1上安裝6.5.3時] ,「Connected Assets Configuration（連接的資產配置）」嚮導無法處理404錯誤(NPR-32730)。

* 在XMP回寫程式中，所有自訂命名空間中繼資料屬性都會將自訂命名空間首碼變更為ns2，而非設定的命名空間首碼(NPR-32748)。

* 不會觸發延遲載入，在選取來檢閱通知收件匣中的工作時，只會顯示100個資產(NPR-32750)。

* `NullPointerException` 會因為新建立的使用者描述檔(SAML/SSO)中遺失節點偏好設定而觀察到。 此錯誤會阻止新登入的使用者 [!DNL Adobe Experience Manager Stock] 使用整合(NPR-32777)。

* 在開啟包含超過10,000個資產的智慧型系列時，記錄檔會出現遍歷警告(NPR-32980)。

* 在使用Dynamic Media Scene7執行模式時，將資產從一個檔案夾移至另一個檔案夾時， [!DNL Adobe Experience Manager] 資產名稱會變更為小寫(NPR-32995)。

* 從搜尋結果導覽至其屬性，然後返回搜尋結果以刪除已搜尋的資產後，無法刪除該資產(NPR-32998)。

* [!UICONTROL 在「移動] Assets」介面中選取目標資料夾時，「下一個」選項 [!UICONTROL 仍會停用] (NPR-33356)。

* [!UICONTROL 在選擇父節點] （其中顯示單個子資料夾），然後選擇子資料夾時，未啟用「下一步」選項(NPR-33275)。

* 即使已授予讀取、建立或修改等其他權限，Adobe Asset Link(AAL)的使用者也會停用登入和登出權限(AAL)。(NPR-33272)

* 智慧型裁切轉譯無法在資產下載對話方塊中使用(NPR-33167)。

* 在具有智慧型裁切設定檔的檔案夾下開啟PDF轉譯邊欄的記錄檔中，會發現異常(CQ-4294201)。

* 如果Experience Manager的Dynamic Media Scene7執行模式預設為停用 [!UICONTROL 「動態媒體同步模式」] (CQ-4294200)，則不會發佈影像預設集。

* 大量上傳時的資產處理會停滯，而工作流程例項則會顯示DAM更新資產的停滯例項(CQ-4293916)。

* 在Experience Manager上建立動態媒體設定有效，但在使用者介面上，選取「儲存」時不會發生任何情況(CQ-4292442)。

* 在Safari/Mac上漸進式播放時，F4V視訊資產的預覽無法運作(CQ-4289844)。

* 在智慧型裁切資產時會建立額外的資料夾，該資產位於父資料夾內， `.` 名稱中含點字元(CQ-4289337)。

* 縮圖中斷，而視訊處理橫幅在複製視訊時不會顯示(CQ-4284125)。

* Dimensional檢視器會針對某些具有空白相機檢視的機型，在Firefox中錯誤顯示空白縮圖(CQ-4283447)。

* 6.5.5.0中修正的效能問題有：(CQ-4279206):

   * 將大型二進位檔上傳至動態媒體影像處理伺服器需要太長時間。

   * Experience Manager的縮圖產生時間因為Dynamic Media Scene7架構而增加。

* 對於擁有大量資產的客戶，動態Media Scene7移轉問題會失敗(CQ-4279206)。

* 視訊360檢視器的版面配置如果使 `setVideo` 用則會中斷，而視訊會在使用時 `video= modifier` 向下移動(CQ-4263201)。

* 安裝Experience Manager SDL軟體包時顯示錯誤資訊(NPR-33175)。

* Experience Manager中的SSRF弱點(NPR-33435)。

### 平台 {#platform-6550}

* 如果 [!DNL Sling] 在下面建立了 `sling:match` 映射條目，則不會調 `/etc/maps` 用篩選器(NPR-33362)。
* Experience Manager因區段錯誤而當機( [!DNL Apache Lucene] NPR-32988)。
* [!DNL Jackson] Experience Manager uberjar檔案中遺失核心套件(NPR-32848)。
* CRXDE Lite不會在未取得節點屬性讀取權限的情 `jcr:primaryType` 況下，為使用者載入內容(NPR-32611)。
* [!DNL Granite] 維護任務調度程式在Experience Manager部署期間重新初始化的頻率過高(CQ-4294627)。
* 當SQL查詢長時間執行（例如7小時）時，Experience Manager停止響應(NPR-33044)。

### 使用者介面{#ui-6550}

* 多欄位中不會持續選擇選項按鈕(NPR-33309)。
* 清單檢視無法使用延遲載入限制(NPR-33124)。
* 如果沒有相符項目，Omnisearch結果頁面不會顯示訊息(NPR-32974)。
* Omnisearch篩選器會在節點下傳 `/content` 回忽略所選位置的所有相符項目(NPR-32849)。

### 整合 {#integrations-6550}

* 當發佈含有Adobe Target元件的頁面時，會清除內部快取(NPR-33162)。
* 與Adobe Target的整合無法在 [!DNL Windows Internet Explorer] 11上運作(NPR-33111)。
* 設定Adobe Target時，在選 [!UICONTROL 擇報表來源時] ,「公司」和「報  表套裝」欄位不會出現(NPR-32502)。
* 使用Adobe [!DNL Experience Fragments] I/O匯出時，「來源產品」等中繼資料不會匯出至Adobe Target(NPR-32159)。
* 本機Experience Manager管理員群組中的授權IMS使用者無法建立或修改IMS組態(NPR-33045)。
* Adobe Launch設定頁面不會顯示所有記錄(NPR-33011)。
* 內容作者群組中的使用者無法編輯Adobe Target元件的屬性，因為發生JavaScript錯誤(NPR-32996)。
* JSON的跨網站指令碼(NPR-32744)。

### 翻譯專案 {#translation-6550}

* 翻譯的標籤不會從協力廠商翻譯服務匯入到Experience Manager(NPR-33154)。
* 翻譯配置頁顯示的翻譯提供程式與用於翻譯的翻譯提供程式不正確(NPR-32971)。
* 將體驗片段資料夾新增至現有的翻譯專案，會建立新專案(NPR-32843)。
* 在運 `NullPointerException` 行翻譯作業的日誌中出現錯誤(NPR-32628)。

### WCM {#wcm-6550}

* 頁面編輯器 [!DNL Sites] -頁面編輯器不允許僅限鍵盤的使用者略過主要內容，而不是透過標題中的所有可用選項來切換標籤焦點(CQ-4293883)。
* 頁面編輯器——使用Well元件並包含已儲存資料的面板不會因為更新版本 [!DNL Chrome] 而 [!DNL Firefox] 顯示(CQ-4292995)。
* MSM —— 從頁面刪除元件並不會從頁面的發佈版本中刪除元件(CQ-4292360)。

### [!DNL Brand Portal] {#assets-brand-portal-6550}

* 從中移除已發佈的中繼 [!DNL Brand Portal] 資料架構會導致錯誤(CQ-4292063)。
* 如果管理員透過 [!DNL Experience Manager Assets] Adobe Developer Console設定品牌入口網站為 [!DNL Brand Portal] 6.5.4，則使用者無法將貢獻資料夾的資產從發佈 [!DNL Brand Portal] 到 [!DNL Experience Manager] (NPR-33046)。
* 重複複製父資料夾導致衝突(NPR-33001)。

### [!DNL Communities] {#communities-6550}

* 無法使用快速編輯功能表選項刪除協調主控台中的資訊卡(NPR-33117)。
* 存取「活動串流」頁 [!UICONTROL 面時發生錯誤] (NPR-33146)。
* 在作者例項上刪除的群組不會從所有發佈例項中移除(NPR-33199)。
* 建立新群組後，作者不會重新導向至 [!DNL Internet Explorer] 11號的「社群群組」區段(NPR-33205)。
* 在Experience Manager收件箱中訪問留言不會將留言的狀態更改為「已讀取」(NPR-32764)。
* 編輯群 [!DNL Communities] 組並變更縮圖影像並不會更新群組縮圖影像(NPR-32599)。
* 使用者無法傳送電子郵件給社群中的其他使用者(NPR-32598)。
* 提交的部落格在使用者重新整理頁面之前不會顯示(NPR-32391)。
* 建立使用者產生的內容(UGC)的通知和訂閱版本時，會儲存來源頁面的錯誤ID(CQ-4279355、CQ-4289703)。
* 跨網站指令碼問題(NPR-33203)。

### 工作流程 {#workflow-6550}

* 左側 [!UICONTROL 導軌中的] 「時間軸」選項的載入時間比預期要長(NPR-32851)。
* 重新啟動Experience Manager例項後，系列的審閱工作電子郵件會包含錯誤的裝載連結(NPR-32774)。

### [!DNL Forms] {#forms-6550}

>[!NOTE]
>
>Experience Manager Service Pack不包含修正 [!DNL Forms]。 它們是使用個別的Forms附加套件傳送。 此外，還會發行包含JEE上AEM Forms修正的累積安裝程式。 如需詳細資訊，請 [參閱「在JEE上安裝AEM Forms附加元件](#install-aem-forms-add-on-package)[和安裝AEM Forms」](#install-aem-forms-jee-installer)。

* 通信管理：在提交信件(NPR-33359、NPR-33153)後，目標區域內資產的順序被混亂。
* 最適化表單：當使用者編輯最適化表單時，「頁面資 [!UICONTROL 訊」選單中的「開始工作流程] 」選項無法運作(NPR-33004)。
* 最適化表單：用戶無法保存具有多個附件的自適應表單(NPR-32997)。
* 最適化表單：以最適化表單變更面板版面會導致錯誤(CQ-4293880)。
* 最適化表單：自適應表單字典中字串的新行將字 `&#xa;` 符添加到字典(NPR-33266)。
* 最適化表單協助功能：當使用者將最適化表單預覽為HTML表格時，「 [!UICONTROL Scribble Signature] 」欄位無法保留標籤焦點(NPR-33159)。
* 最適化表單協助功能：提交最適化表單時顯示的錯誤訊息不會連結 `aria-describedBy` 至屬性(NPR-33071)。
* 最適化表單協助功能：在ARIA無障礙環境支援模式中，在最適化表單中標示為強制的欄位，沒有將強制屬性設為True(NPR-33070)。
* PDFG服務：當使用者將文字檔案轉換為PDF時，日文字元無法正確顯示(NPR-33238)。
* PDFG服務： `CreatePDF` 操作無法將PDF檔案轉換為PDF OCR格式(NPR-32994)。
* PDFG服務：第200個檔案例項的PDF轉換失 [!DNL OpenOffice] 敗(NPR-32766)。
* 後端整合：表單資料模型請求會因重新整理Token因非作用中狀態不正確而失敗(NPR-33169)。
* 設計人員：螢幕閱讀程式會根據預設的地理順序來執行Tabbing順序，而非XDP檔案中定義的自訂Tabbing順序(NPR-32160)。
* 設計人員：如果啟用標籤選項，子表單邊框會消失在產生的PDF輸出中(NPR-32778)。
* 將XSS與GuideSOMProviderServlet一起儲存(NPR-32700)。

## Adobe Experience Manager 6.5.4.0 {#experience-manager-6540}

Adobe Experience Manager 6.5.4.0是重要的更新，其中包含新功能、客戶要求的重要增強功能以及自2019年4月6.5版全面推出以來的效能、穩定性、安全性 **增強**。 它可安裝在Adobe Experience Manager 6.5之上。

Adobe Experience Manager 6.5.4.0中引進的一些主要功能和增強功能包括：

* Adobe Experience Manager Assets現在已透過Adobe I/O Console設定品牌入口網站。

* Adobe Experience Manager Forms工 [作流程現在提供新的「產生可列印的輸出](../forms/using/aem-forms-workflow-step-reference.md) 」步驟。

* [多欄支援](../forms/using/resize-using-layout-mode.md) ，以版面配置模式建立最適化表單和互動式通訊。

* 支援 [HTML](../forms/using/designing-form-template.md) 5表單中的Rich Text。

* [Experience Manager](new-features-latest-service-pack.md#accessibility-enhancements) Assets中的協助工具增強功能。

* 內建儲存庫(Apache Jackrabbit Oak)已更新至1.10.8版。

* 您現在可以將選擇性內容子樹狀結構同步 *至Dynamic Media - Scene7模式* ，而不是所有可在取得 `content/dam`。

* 與SOAP web service整合的表單資料模型現在支援元素上的選擇群組或屬性。

* SOAP輸入或輸出和複雜的資料結構現在支援動態群組替代。

如需最新Service Pack中新增的完整功能和重點說明清單，請參閱「 [Adobe Experience Manager 6.5 Service Pack的新增功能」](new-features-latest-service-pack.md)。

### 網站 {#sites-fixes}

* 當Adobe Experience Manager Sites頁面的URL包含冒號(`:`)或百分比符號(`%`)時，瀏覽器會停止回應，而CPU使用量尖峰(NPR-32369、NPR-31918)。

* 當開啟Experience Manager Sites頁面進行編輯並複製元件時，貼上動作仍無法用於某些預留位置(NPR-32317)。

* 當「管理出版物」精靈開啟時，連結至核心元件的體驗片段不會顯示在發佈的參考清單中(NPR-32233)。

* Touch UI中的即時文案總覽要比Classic UI演算的時間長得多(NPR-32149)。

* 當伺服器時間和機器時間位於不同時區時，排程的發佈時間會在Touch UI中顯示伺服器時間，而在Classic UI中，則會顯示機器時間(NPR-32077)。

* Experience Manager Sites無法開啟URL中含有尾碼的頁面(NPR-32072)。

* 當用戶編輯內容片段時，內容片段的已刪除變化被恢復(NPR-32062)。

* 使用者可以儲存內容片段，而不需在必填欄位中提供任何資訊(NPR-31988)。

* kernel.js和ui.js未預先編譯或快取。 這會增加轉換頁面的時間(NPR-31891)。

* 啟用PageEventAuditListener時，提交隊列的長度將增加。 它影響許多操作的效能，如批量發佈、導航、批量資產移動(NPR-31890)。

* 拖曳「體驗片段」時，會觀察到高回應時間(NPR-31878)。

* 當您在回應式格線的預留位置中選取「拖曳元件到此處」選項時，會傳送GET要求，並導致HTTP 403錯誤(NPR-31845)。

* 在相同資料夾中移動內容時，會停用頁面移動選項(NPR-31840)。

* 在可編輯的範本結構模式中，版面容器中允許的元件清單會顯示不正確的結果。 版面容器中只會顯示具有設計對話方塊的元件(NPR-31816)。

* 當頁面具有使用者的唯讀權限時，Open屬性選項會顯示在sites.html中，但不會顯示在editor.html中(NPR-31770)。

* 當使用者按一下「建立」按鈕時，頁面選項就無法使用(NPR-31756)。

* 無法同步包含OOTB（現成可用）設計匯入工具元件的Adobe促銷活動(NPR-31728)。

* 當您嘗試將項目符號清單變更為編號清單時，僅會變更清單的前兩個項目(NPR-31636)。

* 當頁面未編寫且選取子節點時，選擇對話方塊仍會顯示初始節點。 當製作頁面並使用者按一下瀏覽時，頁面會重新導向至根節點，而非製作的節點(NPR-31618)。

* 「查看配置」對話框對於「收件箱」自定義工作流功能（NPR-32503和NPR-32492）無法正常工作。

* 使用「收件箱」(CQ-4282168)查看工作流資訊時，會顯示錯誤消息。

### 資產 {#assets-6540-enhancements}

* 資產收集頁面上觸發工作流程的按鈕已停用(NPR-32471)。

* 在Experience Manager中使用Dynamic Media Scene7設定將資產從一個檔案夾移至另一個檔案夾(NPR-32440)時，在SPS(Scene7 Publishing System)中建立無名稱的檔案夾。

* 將所有資產（使用「全選」然後移動）移至包含已發佈資產的檔案夾的動作會失敗並出現錯誤(NPR-32366)。

* 產生具有${extension}的資產的轉譯失敗(NPR-32294)。

* 版本歷史記錄URL顯示在資產屬性頁面上的「參考者」欄位下(NPR-31889)。

* 無法從DAM下載的ZIP檔案，無法使用WinZip開啟(NPR-32293)。

* 當開啟「檔案夾設定」以變更檔案夾標題或縮圖影像，然後儲存檔案夾的原始權限時，會更新檔案夾的權限(NPR-32292)。

* 已排程啟動的日曆圖示不會顯示在「狀態」欄（位於DAM資產清單的傳統UI中）中，以取得已排程在日後日期和時間啟動的資產(NPR-32291)。

* 使用程式碼片段範本建立程式碼片段會在程式碼片段建立程式期間搜尋系列時發生錯誤(NPR-32290)。

* 從搜尋篩選器選取多個標籤時，會引發多個搜尋查詢(NPR-32143)。

* 當上傳檔案名稱中超過50個字元的資產時，Experience Manager Assets UI會顯示截斷的檔案名稱(NPR-32054)。

* 當Adobe Stock中核取方塊樹狀結構的第2級核取方塊被選取時，「篩選」面板中的所有核取方塊都會被清除(NPR-31919)。

* 使用Omnisearch Facets的檔案和資料夾搜尋會產生例外(NPR-31872)。

* 即使在相應元資料模式表單中設定相關性規則時，在元資料編輯器中用於強制欄位選擇的欄位突出顯示也不會被刪除(NPR-31834)。

* 葉層級標籤的完整名稱（來自標籤階層）不會顯示在資產屬性頁面中(NPR-31820)。

* 使用Safari瀏覽器上資產屬性頁面的back命令會顯示錯誤(NPR-31753)。

* 觸控式UI搜尋（透過Omnisearch完成）結果頁面會自動捲動並遺失使用者的捲動位置(NPR-31307)。

* PDF資產的資產詳細資料頁面不會顯示動作按鈕，但Experience Manager中在Dynamic Media Scene7執行模式中執行的「至系列」和「新增轉譯」按鈕除外(CQ-4286705)。

* 資產在完成Scene7的批次上傳程式時需要太長時間處理(CQ-4286445)。

* 當使用者未在動態媒體用戶端的設定編輯器中進行任何變更時，儲存按鈕不會匯入遠端設定(CQ-4285690)。

* 當支援的3D模型已收錄到Experience Manager(CQ-4283701)中時，3D資產縮圖不提供資訊。

* 智慧型裁切影片檢視器預設集的未處理狀態會在橫幅文字上與預設名稱一起顯示兩次(CQ-4283517)。

* 在資產的詳細資料頁面(CQ-4283309)上，會發現在3D檢視器中預覽的已上傳3D模型容器高度不正確。

* 在IE 11中，Experience Manager Dynamic Media Hybrid模式(CQ-4255590)的轉盤編輯器無法開啟。

* 鍵盤焦點會卡在「下載」對話方塊、Chrome和Safari瀏覽器的「電子郵件」下拉式清單中(NPR-32067)。

* 嘗試在Experience Manager上新增DM雲端設定時，預設不會啟用「同步所有內容」核取方塊(CQ-4288533)。

### Foundation UI {#foundation-ui-6540}

* 滑鼠控制項會移至先前的篩選欄位，而非在使用「篩選」面板搜尋資產時保留在現有的篩選欄位中(NPR-32538)。

* 平台標籤：在標籤欄位中輸入以搜尋標籤，會顯示根邊界以外的標籤，而不會 `rootPath` 尊重標籤欄位的屬性(NPR-31895)。

* 平台UI:如果在文字欄位中新增無效路徑，路徑瀏覽器會中斷(NPR-31884)。

* 通知會隱藏在頁面選擇的嚴格功能表後方(NPR-31628)。

### 平台 {#platform-sling-6540}

* (HTL)底線取代URL路徑區段中的冒號(NPR-32231)。

### 專案 {#projects-6540}

* 即使使用者有權在子資料夾中建立專案，使用者也看不到「建立」按鈕(NPR-31832)。

### 專案轉譯 {#projects-translation-6540}

* 在中激活「修剪空間」選項時，翻譯項目建立會中斷 `Apache Sling JSP Script Handler` UI(NPR-32154)。

* 將任何要翻譯的標籤添加到翻譯項目時，UI中出現錯誤，錯誤日誌中出現Null點異常(NPR-31896)。

### 整合 {#integrations-6540}

* 啟動程式庫URL的產生只 `path` 是以 `library_name` Launch API中的值為基礎，而不是 `library_path` 以值為基礎(NPR-31550)。

* 處理LiveFyre相關項目(FYR-12420)時會顯示錯誤訊息。

* ReportSuitesServlet易受SSRF的攻擊(NPR-32156)。

### WCM範本編輯器 {#wcm-template-editor-6540}

* 在可編輯的範本結構模式中，版面容器中允許的元件清單不會顯示連結按鈕元件(CQ-4282099)。

### WCM頁面編輯器 {#wcm-page-editor-6540}

* 選取覆蓋，然後選取回應式格點拖曳元件時，會出現錯誤(CQ-4283342)。

### 促銷活動定位 {#campaign-targeting-6540}

* Target雲端設定失敗，並出現錯誤get mbox請求失敗(CQ-4279880)。

### 品牌入口網站 {#assets-brand-portal-6540}

* 在Experience Manager 6.5.4上，品牌入口網站的使用者無法 [!DNL Assets] 將貢獻資料夾資產發佈至Adobe I/O(CQDOC-15655)。 如需Experience Manager 6.5.4的立即修正，建議您下載 [修補程式](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/hotfix/cq-6.5.0-hotfix-33041) ，並安裝在您的作者實例上。

* 中繼資料結構彈出式值在資產屬性中不可見(CQ-4283287)。

* 中繼資料子架構不會根據資產屬性中的mimetype顯示標籤(CQ-4283288)。

* 取消發佈中繼資料結構會填入錯誤訊息，雖然結構已在後端移除。

* 預覽影像不會針對已發佈的資產顯示(CQ-4285886)。

* 使用者無法發佈或取消發佈名稱中包含單引號的資產(CQ-4272686)。

* 下載多個資產時不會顯示條款與條件(CQ-4281224)。

* 已解決次要安全性弱點。

### 社群 {#communities-6540}

* 「建立成員」表單顯示為空白頁(NPR-31997)。

* 使用者無法檢視作者例項的Analytics報表(NPR-30913)。

### Oak-索引與查詢 {#oak-indexing-6540}

* 使用Tika剖析器剖析包含JPEG影像的MS Word和MS Excel檔案時，無法剖析，並發現類別找不到錯誤(NPR-31952)。

### 表單 {#forms-6540}

>[!NOTE]
>
>Experience Manager Service Pack不包含Experience Manager Forms的修正。 它們是使用個別的Forms附加套件傳送。 此外，還會發行包含JEE上Adobe Experience Manager Forms修正的累積安裝程式。 如需詳細資訊，請 [參閱在JEE上安裝Experience Manager Forms附加元件](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package)[和安裝Experience Manager Forms](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer)。

* 通信管理：信件在提交至後置處理工作流程後會顯示額外的字元(NPR-32626)。

* 通信管理：信件在提交至後處理工作流程後，會將下拉式預留位置顯示為文字元件(NPR-32539)。

* 通信管理：字母模板中定義的預設值不會顯示在預覽模式(NPR-32511)中。

* 行動表單：在HTML版本中轉譯XDP表單時，提交按鈕會顯示為已擴充的大小(NPR-32514)。

* 檔案服務：在套用Service Pack 2後，Letters和某些其他頁面的URL存取問題(NPR-32508、NPR-32509)。

* 檔案服務：如果伺服器上的交易數超過特定限制，HTML至PDF的轉換會失敗，而且檔案類型設定會從伺服器 [!DNL Forms] 移除(NPR-32204)。

* 最適化表單：瀏覽器協助工具會根據WCAG2 Level AA准則，報告調適性表單的失敗(NPR-32312、NPR-32309、CQ-4285439)。

* 最適化表單：Chrome瀏覽器協助工具報告最佳實務失敗(NPR-32310)。

* 最適化表單：在Experience Manager Sites頁面中設定內嵌的最適化表單時發生轉換問題(NPR-32168)。

* 工作台：使用「取得PDF公用程式」服務的「PDF屬性」作業時，會顯示錯誤訊息(NPR-32150)。

* 檔案安全性：將DisableGlobalOfflineSynchronizationData選項設為True時，受保護的PDF檔案無法離線開啟(NPR-32078)。

* 設計人員：如果啟用標籤選項，子表單邊框會消失在產生的PDF輸出中(NPR-32547、NPR-31983、NPR-31950)。

* 設計人員：如果表格中有合併的儲存格，則無障礙環境支援測試會失敗，無法針對使用輸出服務(CQ-4285372)從XDP表單轉換的輸出PDF檔案進行協助功能測試。

* Foundation JEE:如果Experience Manager Forms伺服器已與叢集中斷開連線，快取問題會使它無法重新連線至伺服器(NPR-32412)。

## Adobe Experience Manager 6.5.3.0 {#experience-manager-6530}

[!DNL Adobe Experience Manager] 6.5.3.0是重要的版本，其中包括效能、穩定性、安全性，以及自2019年4月6.5版全面推出以來所發行的重要客戶修 **正與增強**。 它可安裝在 [!DNL Adobe Experience Manager] 6.5之上。

此Service Pack版本的一些主要亮點是：

* 內建儲存庫(Apache Jackrabbit Oak)已更新至1.10.6版。

* [!DNL Experience Manager Assets] 現在支援使用Deflate64演算法建立的ZIP封存。

* 已在DAM清單檢視中新增可排序的建立日期新欄，並在清單檢視中新增資產搜尋結果。

* 已在「清單」檢視中啟用「名稱」欄的資產排序。

* [!DNL Dynamic Media] 現在支援智慧型裁切視訊資產。 Smart Crop是機器學習驅動的功能，可在移動影格時重新裁切視訊，以跟隨場景的焦點。

* [!DNL Dynamic Media] 支援智慧映像。

* 能夠在工 [作流程中設定](../forms/using/configure-out-of-office-settings.md) 「不在Office中 [!DNL Experience Manager] 」偏好。

* 能夠在工 [作流程中與其他用戶共用「收件匣](../forms/using/configure-shared-queues-osgi.md) 」或「收件匣」 [!DNL Experience Manager] 項目。

* 能夠在 [批次模式中產生互動式通訊](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)。

* ContextHub中已整合的jQuery更新版本至3.4.1。

### 資產 {#assets-6530-enhancements}

**產品增強功能**

* [!DNL Experience Manager Assets] 現在支援使用Deflate64演算法建立的ZIP封存(NPR-27573)。

* 在DAM清單檢視中新增可排序的建立日期欄，並在清單檢視中新增資產搜尋結果欄(NPR-31312)。

* 在清單檢視中，使用者可以使用「名稱」欄來 [!UICONTROL 排序資產清單] (NPR-31299)。

* DAM的「資產詳細資料」頁面中可預覽GLB、GLTF、OBJ和STL [!UICONTROL 檔案] (CQ-4282277)。

* `ReplicationOnModifyListener` 事件會在區塊上傳期間針對區塊節點 [!DNL Dynamic Media] 觸發(CQ-4281279)。

* [!DNL Dynamic Media] 現在支援智慧型裁切視訊資產。 Smart Crop是機器學習驅動的功能，可在移動影格時重新裁切視訊，以跟隨場景的焦點(CQ-4278995)。

* [!DNL Dynamic Media] 支援Smart Imaging(CQ-422249)。

* 如果查詢參數傳入請求中，搜尋或瀏覽檢視會設為Foundation選擇器中的預設檢視(NPR-31601)。

**修正**

* 某些PDF檔案的中繼資料在標題修改時不會更新並儲存至PDF(NPR-31629)。

* 資產共用不適用於檔案名稱中加上(`+`)字元的資產(NPR-31547)。

* 預設搜尋表單中的「資產管理搜尋邊欄」編輯無法如預期般運作(NPR-31502)。

* 當使用Omnisearch on assets view for serching assets時，不會顯示建議(NPR-31496)。

* 當參考的資產移至其他位置時，系列中的資產參考不會更新，因為不同的使用者會參考不同的資產(NPR-31486)。

* 重複的IPTC標籤會新增至資產中繼資料(NPR-31328)。

* 當從過濾器邊欄觸發搜索時，搜索結果計數不會準確更新(NPR-31316)。

* 取消選擇「檔案類型」過濾器中的第二級複選框時，所有複選框都會被清除，搜索欄中的文本與選定或取消選擇的屬性不同步(NPR-31287)。

* 不能從資料夾的「成員」部分中刪除所有成員（用戶／組）;在嘗試移除所有使用者時，登入的使用者會新增至清單(NPR-31171)。

* 無法刪除檔案名稱中`+`加號()的資產(NPR-31162)。

* 建立下拉式選單（在選取資料夾時，會在頂端選單中顯示）不會將「資料夾」顯示為建立選項(NPR-30877)。

* 對用戶應用拒絕和路徑上的ACL時，資料夾選 `jcr:removeChildNodes` 擇 `jcr:removeNode` 「建立」>「檔案上載」操作項目丟失(NPR-30840)。

* 當某些mp4資產上傳時，DAM工作流程會進入過時狀態，導致所有剩餘的工作流程都進入過時狀態(NPR-30662)。

* 當大型PDF檔案（數GB）上傳至DAM並處理其子資產時，會出現記憶體不足錯誤(NPR-30614)。

* 大量移動資產失敗並顯示警告訊息(NPR-30610)。

* 在 [!DNL Experience Manager][!DNL Dynamic Media]-Scene7模式中，將資產從一個檔案夾移至另一個檔案夾時，資產名稱會變更為小寫(NPR-31630)。

* 編輯遠端影像集時，會針對與Scene7公司名稱相同的資料夾中的影像，發現錯誤(NPR-31340)。

* [!DNL Dynamic Media] 包含參考的資產不會發佈(NPR-31180)。

* 從 [!DNL Dynamic Media]7-Scene7模式上傳到的 [!DNL Dynamic Media Classic] 時間太長，無法完成(NPR-31048)。

* 新增至影像資產的熱點無法透過資產詳細資料頁面的互動式影像檢視器顯示(NPR-30979)。

* 當中對資產執行的動作傳遞至Scene7時，會建立巨大的sling工作，並重新顯 [!DNL Experience manager Assets] 示「處理」橫幅(Processing banner)。

* 建立資產的語言副本時發生衝突，資產不會上傳至Scene7(NPR-30932)。

* 從以 [!DNL Experience Manager][!DNL Dynamic Media]-Hybrid模式執行下載的動態轉譯會中斷（這些轉譯是文字類型，內容為「找不到影像」，而非影像內容類型）(NPR-30876)。

* [!DNL Dynamic Media] 「編碼視訊」工作流程無法針對從Adobe Experience Manager的 [!DNL Dynamic Media Classic][!DNL Dynamic Media]-Scene7模式移轉至視訊的縮圖產生(CQ-4282011)。

* 使用不同的Scene7公司ID(CQ-4280548)，將資產從一個例項移轉至另一個例項時觀察到IpsApiException。

* 當支援的3D模型已收錄至(CQ-4283701)時，「3D資產」縮圖 [!DNL Experience Manager] 不會提供資訊。

* 如果3D資產的相機檢視次數很少，檢視器中會顯示捲動按鈕(CQ-4283322)。

* 在「資產詳細資料」頁面的DimensionalViewer中預覽的已上傳3D模型容器高度不正確(CQ-4283309)。

* 無法在Internet Explorer 11和Safari上使用SmartCropVideoViewer播放視訊(CQ-4281422)。

* 在 [!DNL Experience Manager][!DNL Dynamic Media]-Scene7執行模式上執行時，使用移動按鈕將多個資產從一個檔案夾移至另一個檔案夾時失敗(CQ-4280384)。

* 當MIME類型不是MP4時，資產詳細資料上會顯示扭曲的視訊(CQ-4279704)。

* 新收錄在具有視訊描述檔的資料夾中的視訊，即使編碼百分比完成到100%後，仍會維持處理狀態(CQ-4279389)。

* 從資料夾移動資產會建立大量的sling工作（Scene7 API呼叫），而非理想的必要(CQ-4278664)。

* 當在DAM中建立影像集（或媒體集）並使用適當的命名慣例命名時，影像集的名稱會在Scene7中變更為小寫(CQ-4281112)。

* Scene7 Migrator會錯誤設定發佈狀態(CQ-4263492)。

* 觸控UI搜尋（透過Omnisearch完成）結果頁面會自動捲動，並遺失使用者在內容片段中的捲動位置(CQ-4282898)。

* PDF檔案不會建立索引，而內容則無法搜尋(CQ-4278916)。

* 出現「Group not listed by user picker（組未由用戶選擇器列出）」錯誤：預期false為等於true」時，會在新增具有不同和(CQ-4278177) `principalName` 的封閉 `authorizableId` 使用者群組時觀察到。

* 資產UI欄檢視會顯示所有路徑，不論特定租用戶的dam根路徑為何(CQ-4278175)。

* 資產選擇器的搜尋無法如預期般運作(CQ-4275886)。

* 轉譯工作流程失敗(CQ-4271928)。

* DAM事件清除會刪除最新(`maxSavedActivities`)的事件資料並保存先前建立的資料(NPR-31336)。

* 觸控式UI搜尋（透過Omnisearch完成）結果頁面會自動捲動並遺失使用者的捲動位置(NPR-31307)。

* 在Touch UI中選取全部然後取消選取某些項目（資料夾／個別資產）時，動作列和資產計數不會更新(NPR-31118)。

* 在輪詢資產 [!DNL Experience Manager] 的作業詳細資訊時，會顯示例外(CQ-4283569)。

### 網站 {#sites}

* 如果LiveCopy繼承中斷，即時副本頁面會顯示語言副本連結，而非LiveCopy連結(NPR-30980)。
* 對於新的Blueprint，如果記錄數超過40，則只會顯示前40個記錄。 Blueprint會為其餘的記錄顯示空白行(NPR-31182)。
* 當使用者在功能表的description屬性中新增日文或韓文字元時，功能表會顯示日文和韓文文字的扭曲字元(NPR-31331)。
* 富格文本編輯器(RTE)不允許將嵌入的表作為清單項插入(NPR-30879)。
* 立即可用的架構Rich Text Editor(RTE)。 意外地將內嵌字型大小套用至元素(NPR-31284)。
* 當使用者專注在左側欄位並使用鍵盤快速鍵貼上內容時，會貼上頁面編輯器剪貼簿的內容，而非從左側欄位複製的內容(NPR-31172)。
* 當用戶將「檔案上傳」欄位添加到多欄位時，影像路徑儲存在元件節點中，而不是多欄位節點(NPR-30882)。
* API `ResponsiveGridExporter` 不會傳回介 `com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter` 面。 該 `com.day.cq.wcm.foundation.model.impl` 包聲明為私有包(NPR-31398)。

<!-- Review: NPR-31398 has fixVersion as 6530. However, it is mentioned twice in 6530 and 6520 as fixed. 
Remove one mention of this fix.
-->

* 在非編輯器模式(在「作者」中(不含首碼和 `editor.html``wcmmode=disabled`，或在「發佈者」中)中開啟包含某些「體驗片段」的頁面時，請求會以HTTP狀態錯誤碼 `500` (NPR-30743)結束。
* 使用者無法變更密碼並存取其描述檔頁面(NPR-31161)。

### 搜尋與使用者介面 {#ui-interface-and-search}

* 從卡片檢視切換至搜尋結果頁面上的清單檢視時，在可捲動頁面之前會有延遲(NPR-31286)。

* 「 [!UICONTROL 全選] 」核取方塊會隱藏在使用者介面的 [!DNL Sites] 清單檢視中(NPR-31614)。

* 搜 [!UICONTROL 尋結果頁面上的] 「全選」計數不正確(NPR-31120)。

* 中繼資料編輯器會顯示不存在的標籤(NPR-31119)。

### 轉換 {#translation}

* 在翻譯工作中選擇「到期日期」選項時，會出現兩個日曆彈出式選項(NPR-31270)。

### 平台 {#platform}

* Web控制台中的Mime類型選項無效(NPR-31108)。

* 在設定單一登入時不接受用戶端憑證(NPR-31165)。

* 不會儲存Jetty型HTTP服務緩衝區大小設定的更新(NPR-30925)。

* QueryBuilder現在支援 `fn:name()` xpath查詢中的orderby(NPR-31322)。

* 從 [!DNL Experience Manager] 6.3升級時會建立重複的啟動樹(NPR-31513)。

* 轉送的請求不會保留在sling驗證期間設定的回應標頭(NPR-30013)。

* 在機械臂元件中搜索無法工作(NPR-31692)。

* 由於Apache POI和Apache Tika搭售的不同版本，將ZIP檔案附 [!DNL Experience Manager Communities] 加至貼文時會顯示錯誤(NPR-31018)。

* 包 `org.apache.sling.distribution.api` 在配置管理器中隱藏，因此無法用於定制包(NPR-31720)。

### 專案 {#projects}

* 切換日曆視圖無效(NPR-31271)。

### 品牌入口網站 {#assets-brand-portal-6530}

**產品增強功能**

* 中的「資產來源補充」 [!DNL Experience Manager Assets][!DNL Brand Portal][!DNL Experience Manager]匯入工作流程已修改為只從中擷取新建立的資產，並略過NEW檔案夾中已存在的資產，以避免複製(CQ-4278527)。

**修正**

* 在「資產來源補充」功能中建立新的「貢獻」檔案夾時，會出現不正確的圖示(CQ-4282825)。
* 建立新的「貢獻」檔案夾時，「貢獻」檔案夾中不會顯示一或兩個子檔案夾（NEW和SHARED）(CQ-4282424)。
* 當使用者從結尾處接收「貢獻」檔案夾中的新資產後，嘗試 [!DNL Experience Manager] 從 [!DNL Brand Portal] 發佈「貢獻」檔案夾時，系統會 [!DNL Brand Portal] 引發例外(CQ-4279740)。
* 禁止在「貢獻」檔案夾（巢狀檔案夾）中建立「貢獻」檔案夾，以避免複雜性(CQ-4278391)。
* 系統上傳從「管理控制台」 [!DNL Brand Portal] 匯入的使用者清單（.csv檔案）時發 [!DNL Experience Manager] 生異常。 .csv檔案中只有「電子郵件」、「名字」和「姓氏」欄位是必填欄位(CQ-4278390)。

### 社群 {#communities-6530}

**修正**

* 社群管理員（群組管理員／網站管理員）看不到管理群組的快速連結（開啟／編輯／發佈／刪除群組）(NPR-31627)。
* 除非手動刷新／重新載入頁面，否則不會顯示已提交的部落格(NPR-31599)。
* 「提及次數」功能使用的JCR查詢區分大小寫，而且傳回結果需要太長時間(NPR-31475)。
* [!DNL Experience Manager] 6.5 UberJar檔案拋出異常， `cq-social-translation` 從 [!DNL Experience Manager] 6.5 UberJar檔案中遺失Bundle(NPR-31186)。
* Jackson Databind程式庫已更新至2.9.9.3版，以解決新的弱點(NPR-30967)。
* 活動和通知標題不一致(NPR-30941)。
* 在部落格中編頁 [!DNL Communities] 無法正常運作(NPR-30914)。
* Analytics報表未填入作 [!DNL Experience Manager] 者環境，會顯示空白頁面(NPR-30913)。

### 奧克 {#oak}

* Lucene索引更新導致作者伺服器速度變慢(NPR-31548)。

### 表單 {#forms-6530}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack不包含修正 [!DNL Experience Manager Forms]。 它們是使用個別的Forms附加套件傳送。 此外，還會發行包含JEE修正的累 [!DNL Experience Manager Forms] 積安裝程式。 如需詳細資訊，請 [參閱在JEE上安裝Experience Manager Forms附加元件](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package)[和安裝Experience Manager Forms](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer)。

#### Forms附加套件 {#forms-add-on-package-6530}

**適用性表單**

* 字串包含在本地化最適化表單時的字典鍵(NPR-31110)。

**互動式通訊**

* **MissingNode.toString()** 在將Jackson庫升級至2.10.0(NPR-31549)後傳回不正確的結果。

* 文字編輯器會從從Microsoft Word複製的文字中隨機移除空格字元(NPR-31113)。

**信件管理**

* 從LiveCycle ES4SP1將字母轉換至 [!DNL Experience Manager] 6.5時，不會顯示標題和工具提示(NPR-31615)。

* **將字母儲存為草稿時** ，不會再顯示文字流格式錯誤訊息(NPR-30463)。

**工作流程**

* OSGi工作流程因CPU使用率100%而失敗(NPR-31233)。

**HTML5 Forms**

* 產生XDP表單的HTML5預覽會在新增子表單例項時顯示閃爍(NPR-30909)。

#### JEE安裝程式上的表格 {#forms-jee-installer-6530}

**表單——檔案服務**

* 在。NET專案中使用MTOM的SOAP web service會顯示AssemblerServiceClient叫用和HtmlToPDF2方法的例外(NPR-4281771)。

* AXIS 1.4 jar中發現的安全性弱點2012-5784和2014-3596，以及 [AXIS1.4.1 jar中提供的修正](https://helpx.adobe.com/aem-forms/quick-fixes/6-5/jee-patch-0014.html) (NPR-31015)。

**Foundation JEE**

* 動作設定不會載入「叫用表單工作流程」提交動作的程式名稱(NPR-31478)。

### 隨附的功能套件 {#feature-packs-included-6530}

>[!NOTE]
>
>對 [!DNL Experience Manager Forms] 於客戶，在安裝任何 [!DNL Experience Manager Forms] Service Pack、Cumulative Fix Pack或Feature Pack後，必須安裝附加 [!DNL Experience Manager] 套件。

#### 表單- Foundation JEE {#forms-foundation-jee-feature}

* [!DNL Experience Manager] 對Oracle 18c的表單支援(NPR-29155)。

## Adobe Experience Manager 6.5.2.0 {#experience-manager-6520}

[!DNL Adobe Experience Manager] 6.5.2.0是重要的發行版本，其中包括效能、穩定性、安全性，以及自2019年4月 [!DNL Adobe Experience Manager] 6.5正式推出以來所發佈的重要客戶修 **正和增強**。 它可安裝在 [!DNL Experience Manager] 6.5之上。

此Service Pack版本的一些主要亮點是：

* 內建儲存庫(Apache Jackrabbit Oak)已更新至1.10.3版。
* 已新增設定屬性，以允許將體驗片段直接匯出至使用者定義的工作區 [!DNL Adobe Target]。
* 資產使用者可以搜尋視覺上類似的影像。 [!DNL Experience Manager]會顯示來自DAM儲存庫的智慧型標籤影像，這些影像類似於使用者選取的影像。請參閱 [視覺搜尋](../assets/search-assets.md#visualsearch)。

* 增強「已連線資產」功能，以新增從遠端DAM部署擷取檔案的支援。 網站作者現在可以在Content Finder中搜尋及篩選支援的檔案類型。 遠端檔案可新增至網頁上的「下載」元件。 請參 [閱使用連線資產](../assets/use-assets-across-connected-assets-instances.md)。

* EnhanceDocument類型篩選器，提供更多MIME類型，以支援多值選項。
* 為多資源支援引入外部「重新處理」工作流程。
* 使用 [!DNL Dynamic Media] 複製的預設資產篩選器優化效能。
* 已回復DMS7的裁切／旋轉資產編輯選項。
* 已實作在VideoPlayer中載入時靜音視訊的選項。
* 修正以確保「資產UI」欄檢視僅顯示租用戶特定內容。
* 修正可讓樣式accordion變更反映在搜尋結果中。

### 資產 {#assets}

**產品增強功能**

* 增強「已連線資產」功能，以新增從遠端DAM部署擷取檔案的支援。 網站作者現在可以在Content Finder中搜尋及篩選支援的檔案類型。 遠端檔案可新增至網頁上的「下載」元件。 CQ-4270245的修補程式。 請參 [閱使用連線資產](/help/assets/use-assets-across-connected-assets-instances.md)。

* [!DNL Experience Manager Assets] 使用者可以搜尋外觀相似的影像。 [!DNL Experience Manager]會顯示來自DAM儲存庫的智慧型標籤影像，這些影像類似於使用者選取的影像。請參閱 [視覺搜尋](../assets/search-assets.md#visualsearch)。

**修正**

* ACP API生成的URL和資料夾元資料中的資產路徑不進行URL編碼。 GRANITE-26198:CQ-4271814的修補程式
* 無法使用介面來開啟具有名稱中百分比符號(%)的檔案夾的解壓縮 [!DNL Experience Manager Assets] 檔案。 NPR-29989:CQ-4270467的修補程式
* Touch UI:在管理出版物精靈中，會在貼文請求主體中的頁面之後新增參考，導致所有資產在頁面之後發佈，而當轉譯頁面時，發佈例項中的部分資產會遺失。 NPR-29985:CQ-4270724的修補程式
* 取消關聯資產功能不適用於名稱中具有特殊字元（變成URI編碼的字元）的相關資產。 NPR-30387:CQ-4274446的修補程式
* 在編輯內容片段時，會以錯誤的使用者建立版本。
* 在以租用戶為基礎的系統上建立系列時發生失敗。 NPR-30114:CQ-4272948的修補程式
* 資產UI欄檢視並不尊重目前租用戶的dam根路徑，而是存取所有租用戶dam路徑。 NPR-30636:CQ-4275481的修補程式
* 當您看到插入的影像時，可能會透過受限制的檔案警報視窗進行跨網站指令碼(XSS)攻擊。 NPR-30617:CQ-4270133的修補程式
* 多租用戶：租戶保存資料夾屬性時，會同時觀察成功提示和錯誤消息，說明操作未成功，「無法編輯屬性」。 權限不足。」 因此，令他們困惑。 NPR-30545:CQ-4275333的修補程式
* 資產選擇器對話框不允許選擇資產，因此無法使用相關來源取代功能來更新來源。 NPR-30502:CQ-4275029的修補程式
* [!UICONTROL DAM更新資產] -上傳大型mp4檔案時處於過時狀態。 NPR-30480:CQ-4271352的修補程式
* 「建立審閱任務」功能無法運作，因為空負載導致所有後續審閱任務相關操作失敗。 NPR-30468:CQ-4274263的修補程式
* 透過Datapower的Adobe Smart Tag連線問題。 NPR-30026:CQ-4269457的修補程式
* 「資產UI欄檢視」嘗試開啟離開邊欄的篩選時會引發錯誤。 NPR-30501:CQ-4273862的修補程式
* 在資產資料夾的「已關閉使用者群組」(CUG)屬性中新增與LDAP同步的群組時，不會儲存並擷取群組。 NPR-30615:CQ-4274689的修補程式
* 篩選搜索樣式和方向欄位不會將自動完成的值應用於搜索查詢。 NPR-30620:CQ-4275724的修補程式
* 名稱中包含空格和&quot;&amp;&quot;字元之資料夾的資產共用連結，會為某些資產顯示空白的灰色卡片。 NPR-30557:CQ-4270187的修補程式
* 資料夾中繼資料結構表單不會自動偵測資料類型，因此不會在表單提交中建立相關的TypeHint。 NPR-30599:CQ-4275227的修補程式
* 裁切和旋轉資產編輯選項會從DMS7編寫UI中停用。 NPR-30118:CQ-4273221的修補程式
* 使用DMS7配置的實例 [!DNL Experience Manager] 無法使用共用連結功能。 NPR-30080、NPR-30492:CQ-4273651的修補程式
* 將 [!DNL Dynamic Media]-Scene7元件新增至頁面，然後發佈頁面並不會每次都觸發dmscene7設定。 NPR-30641:CQ-4275962的修補程式
* 在中添加了IPSJobJournal, [!DNL Experience Manager] 以為每個處理配置檔案僅建立一個入侵防護系統(IPS)作業。 NPR-30490:CQ-4273614的修補程式
* [!DNL Dynamic Media]:新增預設篩選條件，排除資產不會複製至發 [!DNL Experience Manager] 布節點。 NPR-30538:CQ-4274678的修補程式
* 引入外部「重新處理」工作流程，以支援多資源，以允許資料夾做為裝載。 工作流程有兩個步驟——透過中繼資料對應至下一個步驟，重新處理沒有控制代碼的資產，並在單一IPS工作中將所有沒有資產控制代碼的資產重新上傳至S7。 如需詳細資訊，請參閱「設定 [!DNL Dynamic Media] 雲端服務」。 NPR-30489:CQ-4272903的修補程式
* 在正確的CSV結束正確的CSV後，上傳錯誤的CSV。 CQ-4277694、CQ-4277814的修補程式
* 要移除的貢獻資料夾專屬的圖示不正確。 CQ-4277580的修補程式
* 在「資產貢獻」索引標籤的使用者選擇器中選取使用者時，使用者名稱不會出現在表格中，而「屬性」頁面上的「刪除使用者」對話方塊會顯示錯誤的文字。 CQ-4277875的修補程式
* 使用者選取使用者並按一下「新增」，就無法將參與者從使用者選擇器新增至「資產貢獻」檔案夾。 CQ-4277824、CQ-4278087的修補程式
* 按小寫搜索用戶名在用戶選擇器中不起作用。 CQ-4277958、CQ-4277930的修補程式
* 非管理員可將資產發佈至資產貢獻資料夾的新資料夾。 CQ-4278200的修補程式
* dam-user（非管理員）不能將參與者新增至「資產貢獻」檔案夾。 CQ-4278192的修補程式
* 「建立」按鈕會顯示在「資產貢獻」檔案夾中。 CQ-4277560的修補程式
* 依相關性排序搜尋查詢會傳 [!DNL InDesign] 回檔案和范 [!DNL InDesign] 本。 CQ-4273864的修補程式
* 如果使用者有大寫電子郵件ID，使用者將無法登入先前已登出的資產。 CQ-4276575的修補程式
* 「刪除」操作僅適用於所選的預設集，如果螢幕在操作後自動刷新清單，則會顯示已刷新的其他預設集。 CQ-4261461的修補程式
* 以混 [!DNL Dynamic Media] 合模式設定雲端服務會導致在中建立多個空白的報表套裝 [!DNL Dynamic Media]，且報表套裝ID未儲存在其中， [!DNL Analytics][!DNL Experience Manager]導致報表套裝重複。 CQ-4249780的修補程式
* 將資產中的 [!DNL Experience Manager] 作業重新命名為重複名稱無法同步至Scene7。 CQ-4276763的修補程式
* 使用者產生的內容會在搜尋篩選面板中錯誤顯示。 CQ-4273875的修補程式
* TIFF影像無法使用「尋找類似項目」選項。 CQ-4278238的修補程式
* 在VideoPlayer中載入時將視訊靜音的實作選項。 CQ-4266465的修補程式
* 檢視器- VideoViewer:poster=none在使用外部視訊時運作不正確。 CQ-4265536的修補程式
* 在IE11和MS Edge瀏覽器上播放視訊時，會顯示等待圖示。 CQ-4251539的修補程式
* 3.8 SDK和5.13檢視器README檔案未更新，且包含舊版資訊。 CQ-4273737的修補程式
* 內容片段在儲存變更之前即會更新版本。 NPR-30616:CQ-4273088的修補程式
* 在縮圖處理中，以Asset#getMetadataValueFromJcr(String)取代Asset#getMetadata(String)。 NPR-30491:CQ-4273067的修補程式
* 上傳jpg會導致訊息出現多個例項：對每個資產執行「ReplicateOnModifyWorker Replicating UPDATED 」操作，導致效能降級。
* 使用「解壓縮封存檔」功能解壓縮郵遞區號檔案會導致檔案夾名稱在其標題中包含百分比(%)的問題。 NPR-29990:CQ-4270467的修補程式

### 網站 {#sites-6520}

* 如果LiveCopy繼承中斷，即時副本頁面會顯示語言副本連結，而非LiveCopy連結(NPR-30980)。
* 對於新的Blueprint，如果記錄數超過40，則只會顯示前40個記錄。 Blueprint會為其餘的記錄顯示空白行(NPR-31182)。
* 文本元件的富格文本編輯器(RTE)插件顯示日文和韓文文本的扭曲字元(NPR-31331)。
* 富格文本編輯器(RTE)不允許將嵌入的表作為清單項插入(NPR-30879)。
* 立即可用的架構Rich Text Editor(RTE)會意外地套用內嵌字型大小至元素(NPR-31284)。
* 當使用者專注在左側欄位並使用鍵盤快速鍵貼上內容時，會貼上頁面編輯器剪貼簿的內容，而非從左側欄位複製的內容(NPR-31172)。
* 當用戶將「檔案上傳」欄位添加到多欄位時，影像路徑儲存在元件節點中，而不是多欄位節點(NPR-30882)。
* API `ResponsiveGridExporter` 不會傳回介 `com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter` 面。 該 `com.day.cq.wcm.foundation.model.impl` 包聲明為私有包(NPR-31398)。
* 在非編輯器模式(在「作者」中(不含首碼和 `editor.html``wcmmode=disabled`，或在「發佈者」中)開啟包含某些體驗片段的頁面時，請求會以HTTP狀態錯誤碼500(NPR-30743)結束。

### WCM —— 頁面編輯器 {#wcm-page-editor-6520}

**產品增強功能**

* EnhanceDocument類型篩選器，提供更多MIME類型，以支援多值選項。 CQ-4270694的修補程式

### 內容片段管理 {#content-fragment-management-6520}

* 內容片段模型UI使用的查詢速度非常慢，最終導致錯誤。 CQ-4270807的修補程式

### UI - Foundation {#ui-foundation}

* 捷徑觸發器，可防止使用者在特定使用者介面中使用&#39;m&#39;、&#39;p&#39;、&#39;e&#39;。 NPR-30355:GRANITE-26346的修補程式
* 關閉 [!DNL Experience Manager Assets] 搜尋使用者介面不會將左側邊欄重設為內容選擇，防止使用者在後續第二次開啟篩選邊欄。 NPR-30509:CQ-4274716的修補程式
* 多租用戶環境： [!DNL Experience Manager Assets] 無法使用UI頂端導覽，並發生JavaScript錯誤。 NPR-30104:GRANITE-26344的修補程式

### 轉換 {#translation-6520}

* 翻譯問題——使用機器翻譯只能翻譯一些元件。 NPR-30079:CQ-4273764的修補程式

### 平台 {#platform-6520}

* [!DNL Experience Manager] 預設郵件發送者無法通過TLS v1.2向遠程SMTP伺服器發送郵件。NPR-30476:GRANITE-26605的修補程式

### 專案 {#projects-6520}

* dam:folderThumbnailPaths值即使刪除資料夾中的資產，也不會重新整理並顯示舊的縮圖。 NPR-30424:CQ-4273667的修補程式
* 完成「移動」選項時，資產的「標題」和「名稱」保持不變。 NPR-30647:CQ-4276265的修補程式

### 社群 {#communities-6520}

* 用戶同步診斷完全中斷，無法正常工作。 NPR-30004、NPR-29943:CQ-4270287、CQ-4271348的修補程式

### Sling {#sling}

* 從6.3.3.2升級到6.5的實例會導致OSGi配置重複。 NPR-30130:CQ-4274016的修補程式

### Integration {#integration}

* 在重新啟動執行個體之前，自訂內容無法正確顯示在發佈執行個體上。 NPR-30377:CQ-4273706的修補程式
* 在網站上設定啟動時，程式庫位址會加上斜線(/)，導致每次手動干預。 NPR-30694:CQ-4275501的修補程式

### 表單 {#forms-6520}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack不包含修正 [!DNL Experience Manager Forms]。 它們是使用個別的附 [!DNL Forms] 加套件傳送。 此外，還會發行包含JEE修正的累 [!DNL Experience Manager Forms] 積安裝程式。 如需詳細資訊，請 [參閱安裝Experience Manager Forms附加元件](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package)[和安裝Experience Manager Forms JEE安裝程式](#forms-jee-installer)。

6.5.2.0表 [!DNL Experience Manager] 格的主要重點為：

* 在 `RenderAtClient` Forms OSGi的API中新增「自動」 `PDFFormRenderOptions`[!DNL Experience Manager] 設定。

#### Forms附加套件 {#forms-add-on-package}

**後端整合**

* 無法使用AWS托管的負載平衡URL配置表單資料模型。 NPR-30123:CQ-4273359的修補程式
* 使用Web服務定義語言(WSDL)建立表單資料模型(FDM)時，會返回錯誤 `Caused by: com.adobe.aem.dermis.exception.DermisException: java.lang.Exception: Unable to handle content type` 消息：NPR-30477:CQ-4272921的修補程式

**信件管理**

* 「建立對應UI(CCR UI)轉譯會間歇性失敗，主控台發生以下錯誤：
   `- Uncaught Error: variable [object Object]is already known the letter`- NPR-30127

**互動式通訊**

* 表單資料模型中標示為必填的欄位，會依「建立對應UI」(CCR UI)的要求顯示。 NPR-30623:CQ-4274902的修補程式

**表單——工作流程**

* 「監看資料夾」上未映射的輸出變數會導致呼叫失敗。 CQ-4264451的修補程式

**HTML5 Forms**

* 第二次部署自訂程式碼或專案時，頁面不會呈現，並發生下列錯誤：

   `org.apache.sling.scripting.sightly.SightlyException.`

   NPR-30539:CQ-4272509的修補程式

* 當在瀏覽模式中使用非視覺案頭存取來讀取HTML5表格時，Chrome瀏覽器會在表單設計中的每個可縮放向量圖形(SVG)之前讀取「圖形」。 NPR-30449:CQ-4274732的修補程式

#### Forms JEE安裝程式 {#forms-jee-installer}

**表單——檔案安全性**

* 套用具有時間戳記的簽名失敗，並出現錯誤：ALC-DSC-003-000:com.adobe.idp.dsc.DSCIndisignationException:調用錯誤。 NPR-30820:CQ-4275852的修補程式

**表單——檔案服務**

* 如果&quot;SubmitURL&quot;包含&amp;符號，則當對轉譯pdf servlet提出POST請求時，在記錄檔中會出現解析錯誤。 NPR-30865:CQ-4278232的修補程式

**表單- Foundation JEE**

* HTMLtoPDF服務在JMX主控台中不會顯示maxReuseCount。 NPR-30134、NPR-30304:CQ-4273763的修補程式
* 從 [!DNL Experience Manager Forms] Workbench叫用web services，新增或編輯Web Service連線會引發錯誤：ClassNotFoundException org.apache.axis.message.SOAPBodyElement。 NPR-30105:CQ-4273217的修補程式

### 隨附的功能套件 {#feature-packs-included}

>[!NOTE]
>
>對 [!DNL Experience Manager Forms] 於客戶，在安裝任何 [!DNL Experience Manager Forms] Service Pack、Cumulative Fix Pack或Feature Pack後，必須安裝附加 [!DNL Experience Manager] 套件。

#### 網站 {#sites-feature-packs-included}

* 已新增設定屬性，以允許將體驗片段直接匯出至使用者定義的工作區 [!DNL Adobe Target]。 NPR-29189:CQ-4249782的修補程式

#### 表單——檔案服務 {#forms-document-services-1}

* 在OSGi的 `RenderAtClient``PDFFormRenderOptions` API中新增「自動」 [!DNL Experience Manager Forms] 設定。 NPR-30759:CQ-4278193的修補程式

## Adobe Experience Manager 6.5.1.0 {#experience-manager-6510}

[!DNL Adobe Experience Manager] 6.5.1.0是重要的發行版本，其中包括效能、穩定性、安全性，以及自2019年4月 [!DNL Adobe Experience Manager] 6.5正式推出以來所發行的重要客戶修 *正和增強。* 它可安裝在 [!DNL Experience Manager] 6.5之上。

此Service Pack版本的一些主要亮點是：

* 啟用動態UI狀態在追蹤事件時的自訂屬性。
* 包含支援以 [!DNL Dynamic Media]-Scene7模式傳送360度視訊資產。
* 透過 *Rich Text Editor的樣式外掛程式* ，啟用日文繞字功能。 如需詳細資訊，請參 [閱設定日文換行](/help/sites-administering/configure-rich-text-editor-plug-ins.md#jpwordwrap)

### 資產

* 更新DAM DMGateway介面，以支援S3多部份。 NPR-29740:CQ-4226303的修補程式
* 轉譯預覽在 `Only empty tenantId is currently supported` 升級至 [!DNL Experience Manager] 6.5後會產生錯誤。NPR-29986:CQ-4272353的修補程式
* 不會顯示「刪除」對話框以允許刪除作業。 NPR-29720:CQ-4271074的修補程式
* 在屬性頁面中新增資產標題後，當使用者嘗試關閉頁面時， [!DNL Experience Manager] 會再次開啟屬性頁面。 NPR-29627:CQ-4264929的修補程式
* VersioningTimelineEventProvider應提供根版本和類型為nt的節點：版本。 GRANITE-26063的修補程式
* 已實作在 [!DNL Experience Manager] DM-Scene7模式下上傳及播放360個球形視訊的功能。 CQ-4265131的修補程式
* 如果編輯了源，即時副本將檢索不正確的狀態。 CQ-4265451的修補程式
* 已啟用對的多站點管理器支 [!DNL Experience Manager Assets]持。 CQ-4271453、CQ-4268621、CQ-4257491的修補程式
* [!DNL Experience Manager] 介面應在時間軸歷程記錄中顯示資產目前版本的額外項目，並顯示最新的登入註解 [!DNL Adobe Asset Link]。 CQ-4262864的修補程式
* 內容片段時間軸在遺失屬性時顯示錯誤訊息。 CQ-4272560的修補程式
* Scene7視訊播放器在展開為全螢幕時的問題。 CQ-4266700的修補程式
* ZoomVerticalViewer:如果使用單一影像資產，則不應顯示平移按鈕。 CQ-4264795的修補程式
* 刪除即時副本中的子節點應分離liveRelationship。 CQ-4270395的修補程式
* 中繼資料結構只包含全域設定中的項目，且遺失作用中租用戶中的項目。 formPath URL值即使在變更時也會回復為預設值。 NPR-29945:CQ-4262898的修補程式
* 發佈影像預設集失敗， [!DNL Brand Portal] 並加上500錯誤碼。 NPR-29510:CQ-4268659的修補程式

### 網站

* 在轉出期間，空屬性和多個屬性不會從Blueprint傳播。 使用Blueprint重設即時副本無法用於元件。 NPR-29253:CQ-4264928、CQ-4264926、CQ-4267722的修補程式
* CoralUI搭配使用時 `Multifield`，會在元 `fileReferenceParameter` 件層級儲存，而非多欄位層級儲存。 NPR-29537:CQ-4266129的修補程式
* 將文字元 [!DNL Experience Manager] 件和文字編輯器增強為日文。 NPR-29785:CQ-4265090的修補程式
* 使用「時間彎曲」還原的頁面，應參照版本修訂時的正確圖片。 NPR-29431:CQ-4262638的修補程式
* 樣式系統節點從父節點繼承到子節點的問題。 NPR-29516:CQ-4270330的修補程式
* 將社交貼文設定為驗證時的錯誤 [!DNL Facebook] 訊息。 NPR-29211:CQ-4266630的修補程式
* 「內容片段」上轉譯的縮圖會顯示「日期」和「時間」欄位的內部日曆表示法。 NPR-29531:CQ-4269362的修補程式
* 在Coral2實作中開啟權限標籤時，不會顯示按鈕。 CQ-4269419的修補程式

### 商務

* 執行電子商務的延遲內容移轉時，ConstraintViolationException。 NPR-29247:CQ-4264383的修補程式

### 內容片段管理

* 開啟包含元和大括弧的字元的內容片段時 `($)` 發生解析錯誤 `({)`。 CQ-4270266的修補程式

### 體驗片段

* 將體 [!DNL Experience Manager] 驗片段匯出至 [!DNL Adobe Target]。 CQ-4265469的修補程式
* 使用智慧型影像匯出至目標的體驗片段失敗。 CQ-4269606的修補程式

* 當使用者嘗試在資訊卡檢視中透過Omnisearch移動體驗片段時，會觸及到死衚衕。 CQ-4263848的修補程式

### WCM —— 頁面編輯器

* 使用無效選擇器時的反映式跨網站指令碼(XSS)。 CQ-4270397的修補程式

### 複寫

* 在元件輸出時，不會逸出使用者提供的 `cq/replication/components/agent` 資料，造成儲存的跨網站指令碼(XSS)弱點。 CQ-4266263的修補程式

### 工作流程

* 對話框參與者的日曆選擇器欄位已損壞。 NPR-29727:CQ-4270423的修補程式

### WCM - SPA編輯器

* 已啟用從遠程端點提取預呈現內容。 CQ-4270238的修補程式
* 開啟SPA模板頁面在伺服器端顯示時的日誌警告。 CQ-4270238的修補程式

### WCM - MSM

* 升級 [!DNL Experience Manager] 至6.4.3讓Multi-Site Manager需要很長時間才能推出。 CQ-4271410的修補程式

### 整合

* BrightEdge憑據失敗，出現連線錯誤。 NPR-29168:CQ-4265872的修補程式

* 嘗試編輯並儲存啟動設定時，會顯示例外 [!DNL Experience Manager] 訊息。 NPR-29176:CQ-4265782/CQ-4266153的修補程式

### 使用者介面

* 新增支援在追蹤基礎追蹤API中特定事件時，將dynamic-UI-states追蹤為自訂屬性。 GRANITE-26283的修補程式
* 無法在提交按鈕上設定追蹤功能。 GRANITE-26326的修補程式
* 精靈無法在提交按鈕上設定追蹤功能。 NPR-29995、NPR-30025:CQ-4264289的修補程式

### 社群

* 無法在成員配置檔案頁面上的下拉菜單中對齊新標章。 NPR-29381:CQ-4267987的修補程式
* 沒有協調者權限的訪客和成員可以透過貼上URL來查看未核准／待審貼文。 NPR-29724:CQ-4271124、CQ-4271441的修補程式
* 使用者登入社群時，可觀察到高達40-50秒的高回應時間。 NPR-29677:CQ-4269444的修補程式

### 複寫

* Replication Agent元件容易受到向未授權用戶洩漏敏感資訊的漏洞的攻擊。 NPR-29611:GRANITE-25070的修補程式

* 在OAuth期間，每次複製時都會發生會話洩 [!DNL Brand Portal]漏。 NPR-30001:GRANITE-26196的修補程式

### 專案

* 從「 [!DNL Experience Manager Assets] 作者 [!DNL Experience Manager] /content/dam/mac」資料夾發佈至 [!DNL Brand Portal] 無法運作。 NPR-29819:CQ-4271118的修補程式

### 平台

* HtmlLibraryManager會在快取失效時刪除crx-quickstart的所有內容。 NPR-29863:GRANITE-26197的修補程式

### 費利克斯

* 使用Java11時，系統控制台中不會顯示「記憶體使用量」詳細資訊。 NPR-29669

### 表單

6.5.1.0的主 [!DNL Experience Manager Forms] 要亮點是：

* 僅限OSGi:在Output and Forms Service中新 `PAGECOUNT` 增屬性。

* 僅限OSGI:已啟用支援，可使用Forms Service建立靜態PDF檔案。
* 為管理員和根用戶啟用對XMLForm.exe的權限。
* 已啟用ADFS v3.0對Dynamics內部部署整合的支援。

#### Forms附加套件

**後端整合**

* 擷取受保護的網站服務定義語言(WSDL)時失敗。 NPR-29945:CQ-4270777的修補程式
* 在IBM [!DNL Experience Manager Forms] WebSphere上安裝時，基於SOAP建立表單資料模型失敗。 CQ-4251134的修補程式
* 已針對Microsoft Dynamics內部部署整合啟用Active Directory Federation Services(ADFS)v3.0支援。 CQ-4270586的修補程式
* 當資料來源的標題變更時，表單資料模型不會顯示更新的標題。 CQ-4265599的修補程式
* 如果實體或屬性的名稱包含連字型大小或空格，表達式將無法計算此類實體和屬性。 CQ-4225129的修補程式

* 原始字串輸出中出現冒號時，會出現錯誤的輸出。 CQ-4260825的修補程式

* 即使REST API輸出中預期沒有內容，表單資料模型的叫用操作也會引發錯誤。 CQ-4268828的修補程式

**適用性表單**

* 無法在延遲載入期間在最適化表單片段中新增例項。 NPR-29818:CQ-4269875的修補程式
* 驗證元件不記錄或顯示記錄文檔模板的任何錯誤。 CQ-4272999的修補程式
* 新增支援，可停用最適化表單的版面編輯器。 CQ-4270810的修補程式
* 已恢復 [!DNL Experience Manager] 6.5中最適化表單的驗證步驟。CQ-4269583的修補程式

* 最適化表單欄位驗證失敗中斷 [!DNL Adobe Sign]。 CQ-4269463的修補程式
* 當例項 [!DNL Experience Manager Forms] 有超過20個可調式表單片段，且所有表單片段的名稱都以相同字串開頭時，搜尋不會傳回或只傳回最近20個建立的片段。 CQ-4264414、CQ-4264914的修補程式

* Adaptive Forms應用程式與大型資料集搭配使用時的效能問題。. CQ-4235310的修補程式

* 透過發佈例項上的匿名帳戶存取時，GuideRuntime指令碼無法載入。 CQ-4268679的修補程式

**表單——互動式通訊**

* 「互動式通訊」範本不會在允許的元件清單中列出頁首和頁尾元件。 CQ-4237895的修補程式
* 當您建立包含影像欄位的互動式通訊列印範本時，圖表的標題會設為空白。 CQ-4264772的修補程式
* 圖表的線條顏色在刪除時設為未定義。 CQ-4264762的修補程式
* 在「檔案片段」上所做的版面圖層變更，在執行保持同步的變更時會消失。 CQ-4266054的修補程式
* 綁定到文本欄位的「文檔片段」中的表單資料模型元素不顯示繼承表徵圖並允許綁定。 CQ-4261089的修補程式
* 列印頻道演算API沒有將資料作為參數傳入API的選項。 CQ-4263540的修補程式
* 當系結類型從「字串」欄位／變數的「文字片段」變更為「無／資料模型物件」時，「由代理編輯」核取方塊會取消勾選，因此不會顯示代理設定。 CQ-4261953的修補程式
* 在提交代理UI時，產生的Web資料json檔案會儲存繼承取消未系結欄位的資訊。 CQ-4265621的修補程式

**表單——工作流程**

* 從最適化表單應用程式的外框重新送出表單時，會造成資料遺失。 NPR-28345:CQ-4260929的修補程式
* 針對非變數案例儲存時，不會關閉檔案。 CQ-4269784的修補程式
* Adaptive Forms應用程式已放棄對Microsoft Windows 8.1的支援。CQ-4265274的修補程式
* 當超過2 MB的影像附加為Android版應用程式表單的欄位層級附件時，應用程 [!DNL Experience Manager Forms] 式會當機。 CQ-4265578的修補程式

* 為「指派」任務中的「互動式通信打印通道」啟用預填充選項。 CQ-4265577的修補程式
* 在用戶成為分配了該任務的組的成員之前，他們無法查看共用任務。 CQ-4248733的修補程式
* 在Windows上，在Adaptive Form應用程式上儲存或送出JEE應用程式會遭到封鎖。 CQ-4268704的修補程式
* 與表單資料模型變數相關聯的表單資料模型不可見。 CQ-4266554的修補程式
* 不支援使用變數支援的檔案簽署狀態變數。 CQ-4266312的修補程式
* 從工作區提交時，無法顯示變母字元。 CQ-4263172的修補程式
* 在升級的設定中，如果開啟工作流程進行編輯，在監看資料夾使用者介面(UI)中會顯示錯誤，而非工作流程名稱。 CQ-4238579的修補程式

**表單——管理**

* 上傳xsd或schema.json以外的副檔名時，不會上傳，且不會產生錯誤訊息。 CQ-4266716的修補程式

**表單——信件管理**

* [!DNL Experience Manager Forms] 6.5建立對應UI(CCR UI)無法開啟使用 [!DNL Experience Manager Forms] 6.3建立的對應。CQ-4266392的修補程式
* 如果DDE資料類型為類型編號，則XDP中的Sum函式不起作用。 CQ-4227403的修補程式
* 要更新的記憶體中字母快取失效邏輯，因為當資產發佈時，其上次修改的時間不會更新。 CQ-4250465的修補程式
* 無法發佈檔案片段、DD和字母。 CQ-4272893的修補程式

#### Forms JEE安裝程式

**PDF產生器**

* 64位元JDK無法將CAD檔案轉換為PDF。 NPR-29924、NPR-29925:CQ-4272113的修補程式
* 已取代PhantomJS至WebToPDF的名稱，以進行HTML至PDF轉換。 NPR-29933:CQ-4234545的修補程式
* 將郵遞區號檔轉換為PDF時產生錯誤。 CQ-4268628的修補程式

**表單——設計人員**

* 當對使用建立的靜態PDF執行完整的協助工具檢查時，「主要語言」 [!DNL Experience Manager Forms Designer]檢查會因缺少語言屬性而失敗。 CQ-4272923、CQ-4271002的修補程式

**表單——檔案安全性**

* 使用硬體安全性模組(HSM)的數位簽章無法在Java 11和Java 8的OSGi Linux上運作。 NPR-29838:CQ-4270441的修補程式
* 具有硬體安全模組(HSM)的數字簽名在JEE Linux和所有受支援的應用程式伺服器（如JBoss和Websphere）上無法運行。 NPR-29839:CQ-4266721的修補程式
* 使用PDF進階電子簽名(PAdES)驗證PDF中的簽名會產生InvalidOperationException。 NPR-29842:CQ-4244837的修補程式
* 新增Document Security Extension對Office 2019的支援\。 CQ-4254369、CQ-4259764的修補程式

**表單——檔案服務**

* PDF無法轉換為「表單」欄位的PDF/A-1b，沒有外觀規定。 NPR-29940:CQ-4269618的修補程式

* OSGi:無法確定在渲染期間生成的頁數。 NPR-28922:CQ-4270870的修補程式
* 在中啟用使用Forms Service的靜態PDF檔案支援 [!DNL Experience Manager Forms OSGi]。 NPR-28572:CQ-4270869的修補程式
* 無法更改XMLForm.exe的權限。 NPR-29828、NPR-29237:Q-4267080的修補程式
* 由伺服器輸出模 [!DNL Experience Manager Forms] 組建立的靜態PDF不會以所建立檔案的語言填入語言屬性／標籤。 NPR-27332:CQ-4271002的修補程式

**表單- Foundation JEE**

* 在最終對象中無法使用pdfg_srt會導致安裝程式失敗。 NPR-29854:CQ-4270137的修補程式
* LCBackupMode.sh無法運作。 NPR-29840:CQ-4269424的修補程式
* 應從WebSphere的用戶介面(UI)中刪除UDP埠引用。 CQ-4264782的修補程式

### 隨附的功能套件

#### 資產——包含

* 已啟用對的多站點管理器支 [!DNL Experience Manager Assets]持。 如需詳細資訊，請參 [閱「使用MSM為Experience Manager Assets重複使用資產」](https://helpx.adobe.com/experience-manager/6-5/help/assets/reuse-assets-using-msm.html)。 NPR-29199:CQ-4259922的修補程式

#### 網站——隨附

* 將體 [!DNL Experience Manager] 驗片段匯出至 [!DNL Adobe Target]。 如需詳細資訊，請 [參閱體驗片段連結重寫提供者- HTML](https://helpx.adobe.com/experience-manager/6-5/help/sites-developing/experience-fragments.html#TheExperienceFragmentLinkRewriterProviderHTML)。 CQ-4265469的修補程式

#### 表單——檔案服務——隨附

* 僅限OSGi:在Output and Forms Service中新增屬性PAGECOUNT。 NPR-28922:CQ-4270870的修補程式
* 僅限OSGi:已啟用支援，可使用Forms Service建立靜態PDF檔案。 NPR-28572:CQ-4270869的修補程式
* 為管理員和根用戶啟用對XMLForm.exe的權限。 NPR-29237:CQ-4267080的修補程式

### OSGi組合和內容套件

以下文字檔案列出 [!DNL Experience Manager] 6.5.1.0中包含的OSGi組合和內容封裝

6.5.1.0中包含 [!DNL Experience Manager] 的OSGi捆綁包清單

[取得檔案](assets/6_5-bundle-list.txt)

6.5.1.0中包含的 [!DNL Experience Manager] 內容套件清單

[取得檔案](assets/6_5-content-package-list.txt)
