---
title: Adobe Experience Manager 6.5 Service Pack發行說明
description: Adobe Experience Manager 6.5 Service Pack 5的發行說明。
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: a599a1c75a1933d6b21e60e96485f43a0aedd679
workflow-type: tm+mt
source-wordcount: '4496'
ht-degree: 0%

---


# Adobe Experience Manager 6.5 Service Pack發行說明 {#aem-service-pack-release-notes}

## Release information {#release-information}

| 產品 | Adobe Experience Manager 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.5.0 |
| 類型 | Service Pack版本 |
| 日期 | 2020年6月04日 |
| 下載URL | [軟體散發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.5.zip) |

## Adobe Experience Manager 6.5.5.0包含的功能 {#what-s-included-in-aem}

Adobe Experience Manager 6.5.5.0是重要的更新，其中包括自2019年4月6.5版正式發行以來，新功能、客戶要求的重要增強功能，以及效能、穩定性和安全性 **增強**。 它可安裝在Adobe Experience Manager 6.5之上。

Adobe Experience Manager 6.5.5.0中引進的一些主要功能和增強功能包括：

* 自訂顯示在Adobe Experience Manager收件匣中的欄名稱。

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

### [!DNL Assets] {#assets-6550}

**Experience Manager Assets中的協助工具增強功能**

* 現在，您可以將鍵盤焦點放在「 [!UICONTROL Comments] 」清單上，並在「在時間軸中建立資產的Create new version [!UICONTROL panel(NPR-33424)」下，將可點選的選項放在「] Comments  」版本的「注釋」下。

* 現在可以使用鍵盤 [!UICONTROL 按鍵，觸及資產的「檢視設定] 」選項，並變更「 [!UICONTROL 檢視設定] 」對話方塊中的設定(NPR-33420)。

* 組合方塊的清單方塊快顯視窗（位於不同頁面的各欄位中）現在會將項目顯示為螢幕閱讀程式可宣佈的選項清單(NPR-33516)。

* 螢幕閱讀程式現在會公佈可排序標題(在清單檢視、時間軸檢視和 [!UICONTROL Manage Publication] page)的排序功能，而欄標題的排序控制項可透過鍵盤存取(NPR-32979)。

* 可點選的元素，例如註解卡、版本更新、組合方塊和功能表的雪佛龍圖示，現在可以使用鍵盤加以關注並與之互動(NPR-33514)。

* 螢幕閱讀程式現在可正確宣佈前瞻分析檢視( [!UICONTROL Insights View] )上前瞻分析圖示（用途、印象和點按）的功能（或動作目的）(NPR-33513)。

* 唯讀表單欄位(例如，資產屬性 [!UICONTROL Basic] （基本）標籤上停用的欄位 )現在可以使用鍵盤(NPR-33493、CQ-4273031)加以集中。

* 各種輸入欄位中的標籤現在都是永久標籤（因此可存取），而不只是預留位置標籤，當輸入文字時就會消失(NPR-33475)。

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

* 如果Experience Manager的Dynamic Media Scene7執行模式預設停用 [!UICONTROL Dynamic Media同步模式] (CQ-4294200)，則不會發佈影像預設集。

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

### 工作流程 {#workflow-6550}

* 左側 [!UICONTROL 導軌中的] 「時間軸」選項的載入時間比預期要長(NPR-32851)。
* 重新啟動Experience Manager例項後，系列的審閱工作電子郵件會包含錯誤的裝載連結(NPR-32774)。

### [!DNL Forms] {#forms-6550}

>[!NOTE]
>
>Experience Manager Service Pack不包含修正 [!DNL Forms]。 它們是使用個別的Forms附加套件傳送。 此外，還會發行包含JEE上AEM Forms修正的累積安裝程式。 如需詳細資訊，請 [參閱「在JEE上安裝AEM Forms附加元件](#install-aem-forms-add-on-package)[和安裝AEM Forms」](#install-aem-forms-jee-installer)。

* 通信管理： 在提交信件(NPR-33359、NPR-33153)後，目標區域內資產的順序被混亂。
* 最適化表單： 當使用者編輯最適化表單時，「頁面資 [!UICONTROL 訊」選單中的「開始工作流程] 」選項無法運作(NPR-33004)。
* 最適化表單： 用戶無法保存具有多個附件的自適應表單(NPR-32997)。
* 最適化表單： 以最適化表單變更面板版面會導致錯誤(CQ-4293880)。
* 最適化表單： 自適應表單字典中字串的新行將字 `&#xa;` 符添加到字典(NPR-33266)。
* 最適化表單協助功能： 當使用者將最適化表單預覽為HTML表格時，「 [!UICONTROL Scribble Signature] 」欄位無法保留標籤焦點(NPR-33159)。
* 最適化表單協助功能： 提交最適化表單時顯示的錯誤訊息不會連結 `aria-describedBy` 至屬性(NPR-33071)。
* 最適化表單協助功能： 在ARIA無障礙環境支援架構中，在最適化表單中標示為強制的欄位沒有將強制屬性設定為True(NPR-33070)。
* PDFG服務： 當使用者將文字檔案轉換為PDF時，日文字元無法正確顯示(NPR-33238)。
* PDFG服務： `CreatePDF` 操作無法將PDF檔案轉換為PDF OCR格式(NPR-32994)。
* PDFG服務： 第200個檔案例項的PDF轉換失 [!DNL OpenOffice] 敗(NPR-32766)。
* 後端整合： 表單資料模型請求會因重新整理Token因非作用中狀態不正確而失敗(NPR-33169)。
* 設計人員： 螢幕閱讀程式會根據預設的地理順序來執行Tabbing順序，而非XDP檔案中定義的自訂Tabbing順序(NPR-32160)。
* 設計人員： 如果啟用標籤選項，子表單邊框會消失在產生的PDF輸出中(NPR-32778)。

## Install 6.5.5.0 {#install}

**設定需求**

* AEM 6.5.5.0需要AEM 6.5。 如需詳 [細指示](/help/sites-deploying/upgrade.md) ，請參閱升級檔案。
* Adobe軟體散發提供Service Pack下 [載](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)。
* 在使用MongoDB和多個執行個體的部署中，使用「套件管理員」將AEM 6.5.5.0安裝在其中一個「作者」執行個體上。
* 在安裝之前，請先拍下快照或AEM例項的新備份。
* 在安裝之前重新啟動實例。 雖然只有在實例仍處於更新模式時才需要此選項（這是從舊版更新實例時的情況），但建議在實例運行較長時段時使用此選項。

>[!NOTE]
>
>Adobe不建議移除或解除安裝Adobe Experience Manager 6.5.5.0套件。

### 安裝Service Pack {#install-service-pack}

執行下列步驟，將Service Pack安裝在現有的Adobe Experience Manager 6.5實例上：

1. 從「軟體散發」下載 [Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.5.zip)。

1. 開啟「套件管理員」，然後按 **[!UICONTROL 一下「上傳套件]** 」以上傳套件。 要瞭解如何使用它，請參 [閱Package Manager](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html)。

1. 選擇軟體包，然後按一下 **[!UICONTROL 安裝]**。

>[!NOTE]
>
>在安裝Service Pack時，有時會退出Package Manager UI的對話方塊。 Adobe建議您在存取部署之前，先等待錯誤記錄穩定下來。 請等待與解除安裝更新程式套件相關的特定記錄，然後確定安裝成功。 通常，這會在任何瀏 [!DNL Safari] 覽器上發生，但是偶爾會發生。

**自動安裝**

在工作實例上自動安裝Adobe Experience Manager 6.5.5.0有兩種方法：

答： 當伺服器聯機 `../crx-quickstart/install` 時，將軟體包放入資料夾。 軟體包會自動安裝。

B. 使用套 [件管理員的HTTP API](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html)。 使 `cmd=install&recursive=true` 用以安裝巢狀包。

>[!NOTE]
>
>Adobe Experience Manager 6.5.5.0不支援啟動載入。

**驗證安裝**

1. 產品資訊頁面(`/system/console/productinfo`)會在「已安裝產品」下顯示更 `Adobe Experience Manager (6.5.5.0)` 新 [!UICONTROL 的版本字串]。

1. 所有OSGi捆綁包都 **[!UICONTROL 是OSGi控制台中的]****[!UICONTROL ACTIVE或FRAGMENT]** (使用Web控制台： `/system/console/bundles`)。

1. OSGI搭售版 `org.apache.jackrabbit.oak-core` 本為1.22.3或更高版本(使用Web Console: `/system/console/bundles`)。

若要瞭解經過認證可與此版本搭配使用的平台，請參閱 [技術需求](/help/sites-deploying/technical-requirements.md)。

### 安裝Adobe Experience Manager Forms附加套件 {#install-aem-forms-add-on-package}

>[!NOTE]
>
>如果您不使用AEM Forms，請略過。 Adobe Experience Manager Forms中的修正是透過個別的附加套件提供。

1. 請確定您已安裝Adobe Experience Manager Service Pack。
1. 下載您作業系統的 [AEM Forms版本中列出的對應Forms附加元件套件](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 。
1. 如安裝AEM Forms附加元件套件中所述，安 [裝Forms附加元件套件](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package)。

### 在JEE上安裝Adobe Experience Manager Forms {#install-aem-forms-jee-installer}

>[!NOTE]
>
>如果您未在JEE上使用AEM Forms，請略過。 JEE上的Adobe Experience Manager Forms修正可透過個別的安裝程式提供。

如需在JEE上安裝Experience Manager Forms累積安裝程式和部署後設定的詳細資訊，請參閱修補程 [式0014的發行說明](https://helpx.adobe.com/aem-forms/quick-fixes/6-5/jee-patch-0014.html)。

### UberJar {#uber-jar}

UberJar for Experience Manager 6.5.5.0可在 [Adobe Public Maven儲存庫中取得](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.5/)。

要在Maven項目中使用UberJar，請 [瞭解如何使用UberJar](/help/sites-developing/ht-projects-maven.md) ，並在項目POM中包括以下相關性：

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version>6.5.5</version>
      <classifier>apis</classifier>
      <scope>provided</scope>
</dependency>
```

## 過時的功能 {#removed-deprecated-features}

本節列出已標示為不再支援的AEM 6.5.5.0功能。 計畫在未來版本中移除的功能會先設為不建議使用，並提供替代選項。

建議客戶在目前的部署中是否使用功能，並規劃變更實施以使用替代選項。

| 區域 | 功能 | 替代方案 |
|---|---|---|
| 整合 | AEM Cloud **[!UICONTROL Services選擇加入畫面已過時]** 。 隨著AEM 6.5中的AEM和Target整合更新，以支援Target Standard API（透過Adobe IMS和I/O使用驗證），以及Adobe Launch在檢測AEM頁面以進行分析和個人化方面的角色日漸增加，「選擇加入」精靈在功能上已變得無關緊要。 | 透過個別的AEM雲端服務，設定系統連線、Adobe IMS驗證和Adobe I/O整合。 |
| 連接器 | AEM 6.5不再支援Adobe JCR Connector for Microsoft SharePoint 2010和Microsoft SharePoint 2013。 | N/A |

## 已知問題 {#known-issues}

* 如果要安裝 [!DNL Experience Manager] 6.5.5.0和11，請在安裝Service Pack後 [!DNL Java] 重新啟動伺服器。 如果要安裝帶有 [!DNL Java] 8的Service Pack，則無需重新啟動。

* 如果階層中的檔案夾已重新命 [!DNL Experience Manager Assets] 名，且包含資產的巢狀檔案夾已發佈至 [!DNL Brand Portal]，則在中不會更新檔案夾的標題，直到 [!DNL Brand Portal] 根檔案夾再次發佈為止。

* 在安裝AEM 6.5.5.0時，83版的更新 [!DNL Chrome] 會造成建立封裝時發生問題。 使用其他可用的瀏覽器(例如 [!DNL Internet Explorer] 和 [!DNL Firefox]或其他AEM標準套件安裝選項)來解決問題。 安裝AEM 6.5.5.0後，問題就會解決。

* 無法使用AEM預設郵件寄件者，將電子郵件傳送至遠端SMTP伺服器，因為它僅允許使用TLS v1.2進行通訊。 從中刪 `javax.mail:mail:1.5.0-b01` 除包 `system/console` 並刷新包以解決問題。

* 當使用者第一次選擇以最適化表單來設定欄位時，儲存設定的選項不會顯示在「屬性瀏覽器」中。 在相同編輯器中選取以設定最適化表單的其他欄位，可解決此問題。

* 如果 [!UICONTROL Connected assets configuration] wizard在安裝後傳回404錯誤訊息，請使用Package Manager手動重新 `cq-remotedam-client-ui-content` 安裝 `cq-remotedam-client-ui-components` 和套件。

* 在安裝AEM 6.5.x.x時，可能會顯示下列錯誤和警告訊息：
   * 「當使用Target Standard API（IMS驗證）在AEM中設定Target整合時，將「體驗片段」匯出至Target會導致建立錯誤的選件類型。 Target會以「HTML」/來源「Adobe Target Classic」類型建立數個選件，而非「Experience Fragment」/來源類型「Adobe Target Classic」。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: 在granite/operations/maintenance中找不到維護視窗。
   * 當使用SUM、MAX和MIN等集合函式時，Adaptive Form伺服器端驗證將失敗。 CQ-4274424
   * `com.adobe.granite.maintenance.impl.TaskScheduler` -在granite/operations/maintenance中找不到維護視窗。
   * 透過可購買橫幅檢視器預覽資產時，不會顯示動態媒體互動影像中的熱點。

## 隨附的OSGi組合和內容套件 {#osgi-bundles-and-content-packages-included}

下列文字檔案列出AEM 6.5.5.0中包含的OSGi組合和內容套件：

* [AEM 6.5.5.0隨附的OSGi搭售清單](assets/6550_bundles.txt)

* [AEM 6.5.5.0內容套件清單](assets/6550_packages.txt)

## 受限制的網站 {#restricted-sites}

這些網站僅提供給客戶使用。 如果您是客戶，需要存取權，請連絡您的Adobe客戶經理。

* [產品下載，請造訪licensing.adobe.com](https://licensing.adobe.com/)
* [聯絡客戶支](https://docs.adobe.com/content/help/en/customer-one/using/home.html)援如需有關存取支援入口網站的詳細資訊，請 [參閱存取支援入口網站](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html)。

>[!MORELIKETHIS]
>
>* [AEM 6.5版本注意事項](/help/release-notes/release-notes.md)
>* [AEM產品頁面](https://www.adobe.com/solutions/web-experience-management.html)
>* [AEM 6.5 檔案](https://helpx.adobe.com/tw/support/experience-manager/6-5.html)
>* 訂閱 [Adobe優先產品更新](https://www.adobe.com/subscription/priority-product-update.html)

