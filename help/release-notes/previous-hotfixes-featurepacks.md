---
title: AEM 6.5舊版Service Pack發行說明
description: Adobe Experience Manager 6.5 Service Pack 3及更舊版本的發行說明。
uuid: c7bc3705-3d92-4e22-ad84-dc6002f6fa6c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 25542769-84d1-459c-b33f-eabd8a535462
docset: aem65
translation-type: tm+mt
source-git-commit: 7345d629aa628c2e2e094a8194d9306d7c3d2d60

---


# 舊版Service Pack中包含的修補程式和功能套件 {#hotfixes-and-feature-packs-included-in-previous-service-packs}

## AEM 6.5.3.0

Adobe Experience Manager 6.5.3.0是重要的發行版本，其中包括自2019年4月6.5版全面推出以來的效能、穩定性、安全性和重要客戶修正與增強 **功能**。 它可安裝在Adobe Experience Manager(AEM)6.5之上。

此Service Pack版本的一些主要亮點是：

* 內建儲存庫(Apache Jackrabbit Oak)已更新至1.10.6版。

* Adobe Experience Manager Assets現在支援使用Deflate64演算法建立的ZIP封存。

* 已在DAM清單檢視中新增可排序的建立日期新欄，並在清單檢視中新增資產搜尋結果。

* 已在「清單」檢視中啟用「名稱」欄的資產排序。

* 動態媒體現在支援智慧型裁切視訊資產。 Smart Crop是機器學習驅動的功能，可在移動影格時重新裁切視訊，以跟隨場景的焦點。

* 動態媒體支援智慧型影像。

* 能夠在 [AEM工作流程中設定](../forms/using/configure-out-of-office-settings.md) 「Out of Office」偏好設定。

* 可在AEM工 [作流程中與其他使用者共用「收件匣](../forms/using/configure-shared-queues-osgi.md) 」或「收件匣」項目。

* 能夠在 [批次模式中產生互動式通訊](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)。

* ContextHub中已整合的jQuery更新版本至3.4.1。

### 資產 {#assets-6530-enhancements}

**產品增強功能**

* Experience Manager Assets現在支援使用Deflate 64演算法建立的ZIP封存(NPR-27573)。

* 已在DAM清單檢視中新增可排序的建立日期新欄，並在清單檢視中新增資產搜尋結果(NPR-31312)。

* 「清單」檢視中已允許根據「名稱」欄進行資產排序(NPR-31299)。

* GLB、GLTF、OBJ和STL資產檔案支援在DAM的「資產詳細資訊」頁面中預覽資產(CQ-4282277)。

* 在動態媒體中區塊上載期間，會針對區塊節點觸發ReplicationOnModifyListener事件(CQ-4281279)。

* 動態媒體現在支援智慧型裁切視訊資產。 Smart Crop是機器學習驅動的功能，可在移動影格時重新裁切視訊，以跟隨場景的焦點(CQ-4278995)。

* 動態媒體支援智慧型影像(CQ-422249)。

* 如果查詢參數傳入請求中，搜尋／瀏覽檢視已設為Foundation選擇器的預設檢視(NPR-31601)。

**修正**

* 某些PDF檔案的中繼資料不會在修改標題時更新並儲存至PDF(NPR-31629)。

* 資產共用不適用於名稱中加上&#39;+&#39;字元的資產(NPR-31547)。

* 預設搜尋表單「資產管理員*搜尋邊欄」中的編輯無法如預期般運作(NPR-31502)。

* 使用Omnisearch on assets view for searching assets時，不會顯示建議(NPR-31496)。

* 當參考的資產移至其他位置時，系列中的資產參考不會更新，因為不同的使用者會參考不同的資產(NPR-31486)。

* 重複的IPTC標籤會新增至資產中繼資料(NPR-31328)。

* 當從篩選邊欄觸發搜尋時，右上角的搜尋結果計數無法正確更新(NPR-31316)。

* 取消選擇「檔案類型」過濾器中的第二級複選框時，所有複選框都將被清除，搜索欄中的文本與所選／未選定的屬性不同步(NPR-31287)。

* 不能從資料夾的「成員」部分中刪除所有成員（用戶／組）;在嘗試移除所有使用者時，登入的使用者會新增至清單(NPR-31171)。

* 無法刪除檔案名稱中加上&#39;+&#39;符號的資產(NPR-31162)。

* 建立下拉式選單（在選取資料夾時，會在頂端選單中顯示）不會將「資料夾」顯示為建立選項(NPR-30877)。

* 當對用戶應用路徑上的ACL拒絕jcr:removeChildNodes和jcr:removeNode(NPR-30840)時，資料夾選擇「建立」>「檔案上載」操作項將丟失。

* 當某些mp4資產上傳時，DAM工作流程會進入過時狀態，導致所有剩餘的工作流程都進入過時狀態(NPR-30662)。

* 當大型PDF檔案（數GB）上傳至DAM並處理其子資產時，會出現記憶體不足錯誤(NPR-30614)。

* 大量移動資產失敗並顯示警告訊息(NPR-30610)。

* 在Dynamic Media Scene 7執行模式上執行的AEM中，當資產從一個檔案夾移至另一個檔案夾時，資產名稱會變更為小寫(NPR-31630)。

* 編輯遠端影像集時，會針對與Scene 7公司名稱相同的資料夾中的影像，發現錯誤(NPR-31340)。

* 不會發佈包含參考的動態媒體資產(NPR-31180)。

* 從AEM Dynamic Media - Scene 7執行模式上傳至Scene 7的時間太長，無法完成(NPR-31048)。

* 新增至影像資產的熱點無法透過資產詳細資料頁面的互動式影像檢視器顯示(NPR-30979)。

* 當對AEM Assets中資產執行的動作傳遞至Scene 7時，會建立巨大的Sling工作，並重新顯示「處理」橫幅(NPR-30947)。

* 建立資產的語言副本時發生衝突，資產不會上傳至場景7(NPR-30932)。

* 從AEM下載的動態轉譯在「動態媒體混合」模式下執行會中斷（這些轉譯屬於文字類型，內容「找不到影像」而非影像內容類型）(NPR-30876)。

* 「動態媒體編碼視訊」工作流程無法針對從Scene 7移轉至Dynamic Media - Scene 7執行模式的視訊產生縮圖(CQ-4282011)。

* 使用不同的Scene 7公司ID(CQ-4280548)，將資產從一個例項移轉至另一個例項時觀察到IpsApiException。

* 當支援的3D模型已收錄到AEM中時，3D Asset縮圖不提供資訊(CQ-4283701)。

* 如果3D資產的相機檢視次數很少，檢視器中會顯示捲動按鈕(CQ-4283322)。

* 在「資產詳細資料」頁面的DimensionalViewer中預覽的已上傳3D模型容器高度不正確(CQ-4283309)。

* 無法在Internet Explorer 11和Safari上使用SmartCropVideoViewer播放視訊(CQ-4281422)。

* 使用「移動」按鈕，將多個資產從一個檔案夾移至另一個檔案夾時，在「動態媒體- scene7執行模式」上執行的AEM中會失敗(CQ-4280384)。

* 當MIME類型不是MP4時，資產詳細資料上會顯示扭曲的視訊(CQ-4279704)。

* 新收錄在具有視訊描述檔的資料夾中的視訊，即使編碼百分比完成到100%後，仍會維持處理狀態(CQ-4279389)。

* 從資料夾移動資產會建立大量的sling工作（Scene 7 API呼叫），而非理想的必要(CQ-4278664)。

* 當在DAM中建立影像集（或媒體集）並以適當的命名慣例命名時，影像集的名稱會在Scene 7中變更為小寫(CQ-4281112)。

* Scene 7 Migrator未正確設定發佈狀態(CQ-4263492)。

* 觸控UI搜尋（透過Omnisearch完成）結果頁面會自動捲動，並遺失使用者在內容片段中的捲動位置(CQ-4282898)。

* PDF檔案不會建立索引，而內容則無法搜尋(CQ-4278916)。

* 出現「Group not listed by user picker（組未由用戶選擇器列出）」錯誤：預期false為等於true」時，會在新增具有不同和(CQ-4278177) `principalName` 的封閉 `authorizableId` 使用者群組時觀察到。

* 資產UI欄檢視會顯示所有路徑，不論特定租用戶的dam根路徑為何(CQ-4278175)。

* 資產選擇器的搜尋無法如預期般運作(CQ-4275886)。

* 轉譯工作流程失敗(CQ-4271928)。

* DAM事件清除會刪除最新(maxSavedActivitys)事件資料，並保留先前建立的資料(NPR-31336)。

* 觸控式UI搜尋（透過Omnisearch完成）結果頁面會自動捲動並遺失使用者的捲動位置(NPR-31307)。

* 在Touch UI中選取全部然後取消選取某些項目（資料夾／個別資產）時，動作列和資產計數不會更新(NPR-31118)。

* 在輪詢資產的作業詳細資訊時，AEM中會顯示例外(CQ-4283569)。

### 網站 {#sites}

* 如果LiveCopy繼承中斷，即時副本頁面會顯示語言副本連結，而非LiveCopy連結(NPR-30980)。
* 對於新的Blueprint，如果記錄數超過40，則只會顯示前40個記錄。 Blueprint會為其餘的記錄顯示空白行(NPR-31182)。
* 當使用者在功能表的description屬性中新增日文或韓文字元時，功能表會顯示日文和韓文文字的扭曲字元。 (NPR-31331)。
* Rich Text Editor(RTE)不允許將嵌入的表作為清單項插入(NPR-30879)。
* 立即可用的Rich Text Editor(RTE)腳手架。 意外地將內嵌字型大小套用至元素(NPR-31284)。
* 當使用者專注在左側欄位並使用鍵盤快速鍵貼上內容時，會貼上頁面編輯器剪貼簿的內容，而非從左側欄位複製的內容(NPR-31172)。
* 當用戶將「檔案上傳」欄位添加到多欄位時，影像路徑儲存在元件節點中，而不是多欄位節點(NPR-30882)。
* ResponsiveGridExporter API不會傳回com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter介面。 com.day.cq.wcm.foundation.model.impl套件宣告為私用套件(NPR-31398)。
* 在非編輯器模式(在「作者」中(不含首碼和 `editor.html``wcmmode=disabled`，或在「發佈者」中)中開啟包含某些ExperienceFragments的頁面時，請求會以HTTP狀態錯誤碼500(NPR-30743)結束。
* 使用者無法變更密碼並存取其描述檔頁面(NPR-31161)。

### 搜尋與使用者介面 {#search-ui-interface}

* 從搜尋結果頁面的「卡片」檢視切換至「清單」檢視時，在可捲動頁面之前會有延遲(NPR-31286)。

* 「全選」核取方塊會隱藏在「網站UI」的「清單」檢視中(NPR-31614)。

* 搜尋結果頁面上的「全選」計數不正確(NPR-31120)。

* 中繼資料編輯器會顯示不存在的標籤(NPR-31119)。

### 轉換 {#translation}

* 在翻譯工作中選擇「到期日期」選項時，會出現兩個日曆彈出式選項(NPR-31270)。

### 平台 {#platform}

* Web控制台中的Mime類型選項無效(NPR-31108)。

* 在設定單一登入時不接受用戶端憑證(NPR-31165)。

* 不會儲存Jetty型HTTP服務緩衝區大小設定的更新(NPR-30925)。

* QueryBuilder現在支援 ``fn:name()`` xpath查詢中的orderby(NPR-31322)。

* 從AEM 6.3升級時會建立重複的啟動樹狀結構(NPR-31513)。

* 轉送的請求不會保留在sling驗證期間設定的回應標頭(NPR-30013)。

* 在機械臂元件中搜索無法工作(NPR-31692)。

* 由於Apache POI和Apache Tika搭售版本不同，將ZIP檔案附加至AEM Communities貼文時會顯示錯誤(NPR-31018)。

* 包 ``org.apache.sling.distribution.api`` 在配置管理器中隱藏，因此無法用於定制包(NPR-31720)。

### 專案 {#projects}

* 切換日曆視圖無效(NPR-31271)。

### 品牌入口網站 {#assets-brand-portal}

**產品增強功能**

* AEM Assets中的「資產來源補充」匯入工作流程已修改為僅將新建立的資產從品牌入口網站擷取至AEM，並略過NEW檔案夾中已存在的資產，以避免複製(CQ-4278527)。

**修正**

* 在「資產來源補充」功能中建立新的「貢獻」檔案夾時，會出現不正確的圖示(CQ-4282825)。
* 建立新的「貢獻」檔案夾時，「貢獻」檔案夾中不會顯示一或兩個子檔案夾（NEW和SHARED）(CQ-4282424)。
* 如果使用者在從品牌入口網站端接收「貢獻」檔案夾中的新資產後，嘗試從AEM將「貢獻」檔案夾重新發佈至品牌入口網站，系統會引發例外(CQ-4279740)。
* 禁止在「貢獻」檔案夾（巢狀檔案夾）中建立「貢獻」檔案夾，以避免複雜性(CQ-4278391)。
* 系統會在上傳從AEM Admin Console匯入的品牌入口網站使用者清單（.csv檔案）時引發例外。 .csv檔案中只有「電子郵件」、「名字」和「姓氏」欄位是必填欄位(CQ-4278390)。

### 社群 {#communities}

**修正**

* 社群管理員（群組管理員／網站管理員）看不到管理群組的快速連結（開啟／編輯／發佈／刪除群組）(NPR-31627)。
* 除非手動刷新／重新載入頁面，否則不會顯示已提交的部落格(NPR-31599)。
* 「提及次數」功能使用的JCR查詢區分大小寫，而且傳回結果需要太長時間(NPR-31475)。
* AEM 6.5 UberJar檔案拋出例 `cq-social-translation` 外，從AEM 6.5 UberJar檔案中遺失Bundle(NPR-31186)。
* Jackson Databind程式庫已更新至2.9.9.3版，以解決新的弱點(NPR-30967)。
* 活動和通知標題不一致(NPR-30941)。
* 在社群部落格中編頁無法正常運作(NPR-30914)。
* Analytics報表未填入AEM作者環境，空白頁面會出現(NPR-30913)。

### 奧克 {#oak}

* Lucene索引更新導致作者伺服器速度變慢(NPR-31548)。

### 表單 {#forms-6530}

>[!NOTE]
>
>AEM Service Pack不包含AEM Forms的修正。 它們是使用個別的Forms附加套件傳送。 此外，還會發行包含JEE上AEM Forms修正的累積安裝程式。 如需詳細資訊，請 [參閱「在JEE上安裝AEM Forms附加元件](#install-aem-forms-add-on-package)[和安裝AEM Forms」](#install-aem-forms-jee-installer)。

#### Forms附加套件 {#forms-add-on-package-6530}

**適用性表單**

* 字串包含在本地化最適化表單時的字典鍵(NPR-31110)。

**互動式通訊**

* **MissingNode.toString()** 在將Jackson庫升級至2.10.0(NPR-31549)後傳回不正確的結果。

* 文字編輯器會從從Microsoft Word複製的文字中隨機移除空格字元(NPR-31113)。

**信件管理**

* 從LiveCycle ES4SP1將字母移轉至AEM 6.5時，不會顯示標題和工具提示(NPR-31615)。

* **將字母儲存為草稿時** ，不會再顯示文字流格式錯誤訊息(NPR-30463)。

**工作流程**

* OSGi工作流程因CPU使用率100%而失敗(NPR-31233)。

**HTML5 Forms**

* 產生XDP表單的HTML5預覽會在新增子表單例項時顯示閃爍(NPR-30909)。

#### JEE安裝程式上的表格 {#forms-jee-installer-6530}

**表單——檔案服務**

* 在。NET專案中使用MTOM的SOAP web service會顯示AssemblerServiceClient叫用和HtmlToPDF2方法的例外(NPR-4281771)。

**Foundation JEE**

* 動作設定不會載入「叫用表單工作流程」提交動作的程式名稱(NPR-31478)。

### 隨附的功能套件 {#feature-packs-included-6530}

>[!NOTE]
>
>對於AEM Forms客戶，在安裝任何AEM Service Pack、Cumulative Fix Pack或Feature Pack後，必須安裝AEM Forms附加套件。

#### 表單- Foundation JEE {#forms-foundation-jee-feature}

* AEM Forms對Oracle 18c的支援(NPR-29155)。

## AEM 6.5.2.0

AEM 6.5.2.0是重要的發行版本，其中包括效能、穩定性、安全性，以及自2019年4月AEM 6.5全面推出以來的重要客戶修正和 **增強功能**。 它可安裝在AEM 6.5上。

此Service Pack版本的一些主要亮點是：

* 內建儲存庫(Apache Jackrabbit Oak)已更新至1.10.3版。
* 已新增設定屬性，以允許將體驗片段直接匯出至Adobe Target的使用者定義工作區。
* 資產使用者可以搜尋視覺上類似的影像。 AEM會顯示來自DAM儲存庫的智慧型標籤影像，這些影像類似於使用者選取的影像。請參閱 [視覺搜尋](../assets/search-assets.md#visualsearch)。

* 增強「已連線資產」功能，以新增從遠端DAM部署擷取檔案的支援。 網站作者現在可以在Content Finder中搜尋及篩選支援的檔案類型。 遠端檔案可新增至網頁上的「下載」元件。 請參 [閱使用連線資產](../assets/use-assets-across-connected-assets-instances.md)。

* EnhanceDocument類型篩選器，提供更多MIME類型，以支援多值選項。
* 為多資源支援引入外部「重新處理」工作流程。
* 使用複製的預設資產篩選器，最佳化動態媒體效能。
* 已回復DMS7的裁切／旋轉資產編輯選項。
* 已實作在VideoPlayer中載入時靜音視訊的選項。
* 修正以確保「資產UI」欄檢視僅顯示租用戶特定內容。
* 修正可讓樣式accordion變更反映在搜尋結果中。

### 資產 {#assets}

**產品增強功能**

* 增強「已連線資產」功能，以新增從遠端DAM部署擷取檔案的支援。 網站作者現在可以在Content Finder中搜尋及篩選支援的檔案類型。 遠端檔案可新增至網頁上的「下載」元件。 CQ-4270245的修補程式。 請參 [閱使用連線資產](/help/assets/use-assets-across-connected-assets-instances.md)。

* 資產使用者可以搜尋視覺上類似的影像。 AEM會顯示來自DAM儲存庫的智慧型標籤影像，這些影像類似於使用者選取的影像。請參閱 [視覺搜尋](../assets/search-assets.md#visualsearch)。

**修正**

* ACP API生成的URL和資料夾元資料中的資產路徑不進行URL編碼。 GRANITE-26198:CQ-4271814的修補程式
* 無法使用「資產」介面開啟具有名稱中含百分比符號(%)的檔案夾解壓縮。 NPR-29989:CQ-4270467的修補程式
* Touch UI:在管理出版物精靈中，會在貼文請求主體中的頁面之後新增參考，導致所有資產在頁面之後發佈，而當轉譯頁面時，發佈例項中的部分資產會遺失。 NPR-29985:CQ-4270724的修補程式
* 取消關聯資產功能不適用於名稱中具有特殊字元（變成URI編碼的字元）的相關資產。 NPR-30387:CQ-4274446的修補程式
* 在編輯內容片段時，會以錯誤的使用者建立版本。
* 在以租用戶為基礎的系統上建立系列時發生失敗。 NPR-30114:CQ-4272948的修補程式
* 資產UI欄檢視並不尊重目前租用戶的dam根路徑，而是存取所有租用戶dam路徑。 NPR-30636:CQ-4275481的修補程式
* 當您看到插入的影像時，可能會透過受限制的檔案警報視窗進行跨網站指令碼(XSS)攻擊。 NPR-30617:CQ-4270133的修補程式
* 多租用戶：租戶保存資料夾屬性時，會同時觀察成功提示和錯誤消息，說明操作未成功，「無法編輯屬性」。 權限不足。」 因此，令他們困惑。 NPR-30545:CQ-4275333的修補程式
* 資產選擇器對話框不允許選擇資產，因此無法使用相關來源取代功能來更新來源。 NPR-30502:CQ-4275029的修補程式
* DAM更新資產工作流程——上傳大型mp4檔案時處於過時狀態。 NPR-30480:CQ-4271352的修補程式
* 「建立審閱任務」功能無法運作，因為空負載導致所有後續審閱任務相關操作失敗。 NPR-30468:CQ-4274263的修補程式
* 透過Datapower的Adobe Smart Tag連線問題。 NPR-30026:CQ-4269457的修補程式
* 「資產UI欄檢視」嘗試開啟離開邊欄的篩選時會引發錯誤。 NPR-30501:CQ-4273862的修補程式
* 在資產資料夾的「已關閉使用者群組」(CUG)屬性中新增與LDAP同步的群組時，不會儲存並擷取群組。 NPR-30615:CQ-4274689的修補程式
* 篩選搜索樣式和方向欄位不會將自動完成的值應用於搜索查詢。 NPR-30620:CQ-4275724的修補程式
* 名稱中包含空格和&quot;&amp;&quot;字元之資料夾的資產共用連結，會為某些資產顯示空白的灰色卡片。 NPR-30557:CQ-4270187的修補程式
* 資料夾中繼資料結構表單不會自動偵測資料類型，因此不會在表單提交中建立相關的TypeHint。 NPR-30599:CQ-4275227的修補程式
* 裁切和旋轉資產編輯選項會從DMS7編寫UI中停用。 NPR-30118:CQ-4273221的修補程式
* 使用DMS7設定的AEM例項無法使用「共用連結」功能。 NPR-30080、NPR-30492:CQ-4273651的修補程式
* 將Dynamic Media Scene7元件新增至頁面，然後發佈頁面並不會每次觸發dmscene7設定。 NPR-30641:CQ-4275962的修補程式
* 在AEM中新增IPSJobJournal，以針對每個處理設定檔僅建立一個入侵防護系統(IPS)工作。 NPR-30490:CQ-4273614的修補程式
* 動態媒體：新增預設篩選條件，排除資產不會複製至AEM發佈節點。 NPR-30538:CQ-4274678的修補程式
* 引入外部「重新處理」工作流程，以支援多資源，以允許資料夾做為裝載。 工作流程有兩個步驟——透過中繼資料對應至下一個步驟，重新處理沒有控制代碼的資產，並在單一IPS工作中將所有沒有資產控制代碼的資產重新上傳至S7。 如需詳細資訊，請參閱設定動態媒體雲端服務。 NPR-30489:CQ-4272903的修補程式
* 在正確的CSV結束正確的CSV後，上傳錯誤的CSV。 CQ-4277694、CQ-4277814的修補程式
* 要移除的貢獻資料夾專屬的圖示不正確。 CQ-4277580的修補程式
* 在「資產貢獻」索引標籤的使用者選擇器中選取使用者時，使用者名稱不會出現在表格中，而「屬性」頁面上的「刪除使用者」對話方塊會顯示錯誤的文字。 CQ-4277875的修補程式
* 使用者選取使用者並按一下「新增」，就無法將參與者從使用者選擇器新增至「資產貢獻」檔案夾。 CQ-4277824、CQ-4278087的修補程式
* 按小寫搜索用戶名在用戶選擇器中不起作用。 CQ-4277958、CQ-4277930的修補程式
* 非管理員可將資產發佈至資產貢獻資料夾的新資料夾。 CQ-4278200的修補程式
* dam-user（非管理員）不能將參與者新增至「資產貢獻」檔案夾。 CQ-4278192的修補程式
* 「建立」按鈕會顯示在「資產貢獻」檔案夾中。 CQ-4277560的修補程式
* 依相關性排序搜尋查詢會傳回InDesign檔案以及InDesign範本。 CQ-4273864的修補程式
* 如果使用者有大寫電子郵件ID，使用者將無法登入先前已登出的資產。 CQ-4276575的修補程式
* 「刪除」操作僅適用於所選的預設集，如果螢幕在操作後自動刷新清單，則會顯示已刷新的其他預設集。 CQ-4261461的修補程式
* 在DMHybrid模式中設定Dynamic Media Cloud服務會導致在Analytics中建立多個空的報表套裝，而且AEM中未儲存任何報表套裝ID，導致報表套裝重複。 CQ-4249780的修補程式
* 將AEM資產中的作業重新命名為重複名稱無法同步至Scene7。 CQ-4276763的修補程式
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

* 如果LiveCopy繼承中斷，即時副本頁面會顯示語言副本連結，而非LiveCopy連結。 (NPR-30980)
* 對於新的Blueprint，如果記錄數超過40，則只會顯示前40個記錄。 Blueprint會為其餘的記錄顯示空白行。 (NPR-31182)
* 文本元件的富格文本編輯器(RTE)插件顯示日文和韓文文本的扭曲字元。 (NPR-31331)
* 富格文本編輯器(RTE)不允許將嵌入的表作為清單項插入。 (NPR-30879)
* 立即可用的架構Rich Text Editor(RTE)會意外地套用內嵌字型大小至元素。 (NPR-31284)
* 當使用者專注在左側欄位並使用鍵盤快速鍵貼上內容時，會貼上頁面編輯器剪貼簿的內容，而非從左側欄位複製的內容。 (NPR-31172)
* 當用戶將「檔案上載」欄位添加到多欄位時，影像路徑將儲存在元件節點中，而不是多欄位節點中。 (NPR-30882)
* ResponsiveGridExporter API不會傳回com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter介面。 com.day.cq.wcm.foundation.model.impl套件宣告為私用套件。 (NPR-31398)
* 在非編輯器模式（在「作者」中不含首碼，或在「發行者」中）中開啟包含某些ExperienceFragments的頁面時，請求會以HTTP狀態錯誤碼500結束。 `editor.html``wcmmode=disabled`(NPR-30743)

### WCM —— 頁面編輯器 {#wcm-page-editor-6520}

**產品增強功能**

* EnhanceDocument類型篩選器，提供更多MIME類型，以支援多值選項。 CQ-4270694的修補程式

### 內容片段管理 {#content-fragment-management-6520}

* 內容片段模型UI使用的查詢速度非常慢，最終導致錯誤。 CQ-4270807的修補程式

### UI - Foundation {#ui-foundation}

* 捷徑觸發器，可防止使用者在特定使用者介面中使用&#39;m&#39;、&#39;p&#39;、&#39;e&#39;。 NPR-30355:GRANITE-26346的修補程式
* 關閉資產搜尋UI不會將左側邊欄重設為「內容」選擇，以防止使用者在後續第二次開啟篩選邊欄。 NPR-30509:CQ-4274716的修補程式
* 多租用戶環境：資產UI頂端導覽無法使用，且會發生JavaScript錯誤。 NPR-30104:GRANITE-26344的修補程式

### 轉換 {#translation-6520}

* 翻譯問題——使用機器翻譯只能翻譯一些元件。 NPR-30079:CQ-4273764的修補程式

### 平台 {#platform-6520}

* AEM Default Mail Sender無法透過TLS v1.2將郵件傳送至遠端SMTP伺服器。NPR-30476:GRANITE-26605的修補程式

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
>AEM Service Pack不包含AEM Forms的修正。 它們是使用個別的Forms附加套件傳送。 此外，還會發行包含JEE上AEM Forms修正的累積安裝程式。 如需詳細資訊，請 [參閱「安裝AEM Forms附加元件](#install-aem-forms-add-on-package)[與安裝AEM Forms JEE安裝程式」](#forms-jee-installer)。

AEM 6.5.2.0表格的主要重點為：

* 在AEM Forms OSGi的 `RenderAtClient` API中新 `PDFFormRenderOptions` 增「自動」設定。

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
* 從AEM Forms Workbench叫用web services，新增或編輯Web Service連線會引發錯誤：ClassNotFoundException org.apache.axis.message.SOAPBodyElement。 NPR-30105:CQ-4273217的修補程式

### 隨附的功能套件 {#feature-packs-included}

>[!NOTE]
>
>對於AEM Forms客戶，在安裝任何AEM Service Pack、Cumulative Fix Pack或Feature Pack後，必須安裝AEM Forms附加套件。

#### 網站 {#sites-feature-packs-included}

* 已新增設定屬性，以允許將體驗片段直接匯出至Adobe Target的使用者定義工作區。 NPR-29189:CQ-4249782的修補程式

#### 表單——檔案服務 {#forms-document-services-1}

* 在AEM Forms OSGi的 `RenderAtClient` API中新 `PDFFormRenderOptions` 增「自動」設定。 NPR-30759:CQ-4278193的修補程式

## AEM 6.5.1.0 {#release-6510}

AEM 6.5.1.0是重要的發行版本，其中包括效能、穩定性、安全性，以及自2019年4月AEM 6.5全面推出以來的重要客戶修正和 *增強功能。* 它可安裝在AEM 6.5上。

此Service Pack版本的一些主要亮點是：

* 啟用動態UI狀態在追蹤事件時的自訂屬性。
* 包含在Dynamic Media Scene 7中傳送360度視訊資產的支援。
* 透過 *Rich Text Editor的樣式外掛程式* ，啟用日文繞字功能。 如需詳細資訊，請參 [閱設定日文換行](/help/sites-administering/configure-rich-text-editor-plug-ins.md#jpwordwrap)

### 資產

* 更新DAM DMGateway介面，以支援S3多部份。 NPR-29740:CQ-4226303的修補程式
* 轉譯預覽 `Only empty tenantId is currently supported` 在升級至AEM 6.5\後會產生錯誤。 NPR-29986:CQ-4272353的修補程式
* 不會顯示「刪除」對話框以允許刪除作業。 NPR-29720:CQ-4271074的修補程式
* 在屬性頁面中新增資產標題後，當使用者嘗試關閉頁面時，AEM會再次開啟屬性頁面。 NPR-29627:CQ-4264929的修補程式
* VersioningTimelineEventProvider應提供根版本和類型為nt的節點：版本。 GRANITE-26063的修補程式
* 已實作在AEM DM-Scene7模式中上傳及播放360個球形視訊的功能。 CQ-4265131的修補程式
* 如果編輯了源，即時副本將檢索不正確的狀態。 CQ-4265451的修補程式
* 啟用資產的多網站管理員支援。 CQ-4271453、CQ-4268621、CQ-4257491的修補程式
* AEM介面應會在時間軸歷史記錄中顯示資產目前版本的額外項目，並顯示Adobe Asset Link的最新登入注釋。 CQ-4262864的修補程式
* 內容片段時間軸在遺失屬性時顯示錯誤訊息。 CQ-4272560的修補程式
* Scene 7視訊播放器在展開為全螢幕時的問題。 CQ-4266700的修補程式
* ZoomVerticalViewer:如果使用單一影像資產，則不應顯示平移按鈕。 CQ-4264795的修補程式
* 刪除即時副本中的子節點應分離liveRelationship。 CQ-4270395的修補程式
* 中繼資料結構只包含全域設定中的項目，且遺失作用中租用戶中的項目。 formPath URL值即使在變更時也會回復為預設值。 NPR-29945:CQ-4262898的修補程式
* 發佈影像預設集至品牌入口網站失敗，並出現500錯誤碼。 NPR-29510:CQ-4268659的修補程式

### 網站

* 在轉出期間，空屬性和多個屬性不會從Blueprint傳播。 使用Blueprint重設即時副本無法用於元件。 NPR-29253:CQ-4264928、CQ-4264926、CQ-4267722的修補程式
* CoralUI搭配使用時 `Multifield`，會在元 `fileReferenceParameter` 件層級儲存，而非多欄位層級儲存。 NPR-29537:CQ-4266129的修補程式
* 將AEM文字元件和文字編輯器增強為日文。 NPR-29785:CQ-4265090的修補程式
* 使用「時間彎曲」還原的頁面，應參照版本修訂時的正確圖片。 NPR-29431:CQ-4262638的修補程式
* 樣式系統節點從父節點繼承到子節點的問題。 NPR-29516:CQ-4270330的修補程式
* 設定社交貼文至Facebook驗證時的錯誤訊息。 NPR-29211:CQ-4266630的修補程式
* 「內容片段」上轉譯的縮圖會顯示「日期」和「時間」欄位的內部日曆表示法。 NPR-29531:CQ-4269362的修補程式
* 在Coral2實作中開啟權限標籤時，不會顯示按鈕。 CQ-4269419的修補程式

### 商務

* 執行電子商務的延遲內容移轉時，ConstraintViolationException。 NPR-29247:CQ-4264383的修補程式

### 內容片段管理

* 開啟包含元和大括弧的字元的內容片段時 `($)` 發生解析錯誤 `({)`。 CQ-4270266的修補程式

### 體驗片段

* 將AEM體驗片段匯出至Adobe Target。 CQ-4265469的修補程式
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

* 升級至AEM 6.4.3讓Multi-Site Manager需要很長時間才能推出。 CQ-4271410的修補程式

### 整合

* BrightEdge憑據失敗，出現連線錯誤。 NPR-29168:CQ-4265872的修補程式

* 嘗試編輯並儲存AEM啟動設定時，會顯示例外訊息。 NPR-29176:CQ-4265782/CQ-4266153的修補程式

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

* 每次複製到品牌入口網站時，OAuth期間會話洩漏。 NPR-30001:GRANITE-26196的修補程式

### 專案

* 將資產從AEM Author /content/dam/mac資料夾發佈至品牌入口網站無法運作。 NPR-29819:CQ-4271118的修補程式

### 平台

* HtmlLibraryManager會在快取失效時刪除crx-quickstart的所有內容。 NPR-29863:GRANITE-26197的修補程式

### 費利克斯

* 使用Java11時，系統控制台中不會顯示「記憶體使用量」詳細資訊。 NPR-29669

### 表單

AEM 6.5.1.0表格的主要重點為：

* 僅限OSGi:在Output and Forms Service中新 `PAGECOUNT` 增屬性。

* 僅限OSGI:已啟用支援，可使用Forms Service建立靜態PDF檔案。
* 為管理員和根用戶啟用對XMLForm.exe的權限。
* 已啟用ADFS v3.0對Dynamics內部部署整合的支援。

#### Forms附加套件

**後端整合**

* 擷取受保護的網站服務定義語言(WSDL)時失敗。 NPR-29944:CQ-4270777的修補程式
* 當AEM Forms安裝在IBM WebSphere上時，建立以SOAP為基礎的表單資料模型會失敗。 CQ-4251134的修補程式
* 已針對Microsoft Dynamics內部部署整合啟用Active Directory Federation Services(ADFS)v3.0支援。 CQ-4270586的修補程式
* 當資料來源的標題變更時，表單資料模型不會顯示更新的標題。 CQ-4265599的修補程式
* 如果實體或屬性的名稱包含連字型大小或空格，表達式將無法計算此類實體和屬性。 CQ-4225129的修補程式

* 原始字串輸出中出現冒號時，會出現錯誤的輸出。 CQ-4260825的修補程式

* 即使REST API輸出中預期沒有內容，表單資料模型的叫用操作也會引發錯誤。 CQ-4268828的修補程式

**適用性表單**

* 無法在延遲載入期間在最適化表單片段中新增例項。 NPR-29818:CQ-4269875的修補程式
* 驗證元件不記錄或顯示記錄文檔模板的任何錯誤。 CQ-4272999的修補程式
* 新增支援，可停用最適化表單的版面編輯器。 CQ-4270810的修補程式
* 已還原AEM 6.5中最適化表單的驗證步驟。 CQ-4269583的修補程式

* 最適化表單欄位驗證失敗會中斷Adobe Sign。 CQ-4269463的修補程式
* 當AEM Forms例項有超過20個可調式表單片段，且所有表單片段的名稱都以相同字串開頭時，搜尋不會傳回或只傳回最近20個建立的片段。 CQ-4264414、CQ-4264914的修補程式

* 當Adaptive Forms應用程式與大型資料集搭配使用時的效能問題。. CQ-4235310的修補程式

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
* Adaptive Forms應用程式已放棄對Microsoft Windows 8.1的支援。 CQ-4265274的修補程式
* 當超過2 MB的影像附加為Android版AEM Forms應用程式中表單的欄位層級附件時，應用程式會當機。 CQ-4265578的修補程式

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

* AEM 6.5 Forms Create Conferrence UI(CCR UI)無法開啟使用AEM 6.3 Forms建立的對應。 CQ-4266392的修補程式
* 如果DDE資料類型為類型編號，則XDP中的Sum函式不起作用。 CQ-4227403的修補程式
* 要更新的記憶體中字母快取失效邏輯，因為當資產發佈時，其上次修改的時間不會更新。 CQ-4250465的修補程式
* 無法發佈檔案片段、DD和字母。 CQ-4272893的修補程式

#### Forms JEE安裝程式

**PDF產生器**

* 64位元JDK無法將CAD檔案轉換為PDF。 NPR-29924、NPR-29925:CQ-4272113的修補程式
* 已取代PhantomJS至WebToPDF的名稱，以進行HTML至PDF轉換。 NPR-29933:CQ-4234545的修補程式
* 將郵遞區號檔轉換為PDF時產生錯誤。 CQ-4268628的修補程式

**表單——設計人員**

* 當對使用AEM Form Designer建立的靜態PDF執行完整的協助工具檢查時，「主要語言」檢查會因為缺少語言屬性而失敗。 CQ-4272923、CQ-4271002的修補程式

**表單——檔案安全性**

* 使用硬體安全性模組(HSM)的數位簽章無法在Java 11和Java 8的OSGi Linux上運作。 NPR-29838:CQ-4270441的修補程式
* 具有硬體安全模組(HSM)的數字簽名在JEE Linux和所有受支援的應用程式伺服器（如JBoss和Websphere）上無法運行。 NPR-29839:CQ-4266721的修補程式
* 使用PDF進階電子簽名(PAdES)驗證PDF中的簽名會產生InvalidOperationException。 NPR-29842:CQ-4244837的修補程式
* 新增Document Security Extension對Office 2019的支援\。 CQ-4254369、CQ-4259764的修補程式

**表單——檔案服務**

* PDF無法轉換為「表單」欄位的PDF/A-1b，沒有外觀規定。 NPR-29940:CQ-4269618的修補程式

* OSGi:無法確定在渲染期間生成的頁數。 NPR-28922:CQ-4270870的修補程式
* 啟用AEM Forms OSGi中使用Forms Service的靜態PDF檔案支援。 NPR-28572:CQ-4270869的修補程式
* 無法更改XMLForm.exe的權限。 NPR-29828、NPR-29237:Q-4267080的修補程式
* 由AEM Forms伺服器輸出模組建立的靜態PDF不會以所建立檔案的語言填入語言屬性／標籤。 NPR-27332:CQ-4271002的修補程式

**表單- Foundation JEE**

* 在最終對象中無法使用pdfg_srt會導致安裝程式失敗。 NPR-29854:CQ-4270137的修補程式
* LCBackupMode.sh無法運作。 NPR-29840:CQ-4269424的修補程式
* 應從WebSphere的用戶介面(UI)中刪除UDP埠引用。 CQ-4264782的修補程式

### 隨附的功能套件

#### 資產——包含

* 啟用資產的多網站管理員支援。 如需詳細資訊，請參 [閱「使用MSM為資產重複使用資產」](https://helpx.adobe.com/experience-manager/6-5/help/assets/reuse-assets-using-msm.html)。 NPR-29199:CQ-4259922的修補程式

#### 網站——隨附

* 將AEM體驗片段匯出至Adobe Target。 如需詳細資訊，請 [參閱體驗片段連結重寫提供者- HTML](https://helpx.adobe.com/experience-manager/6-5/help/sites-developing/experience-fragments.html#TheExperienceFragmentLinkRewriterProviderHTML)。 CQ-4265469的修補程式

#### 表單——檔案服務——隨附

* 僅限OSGi:在Output and Forms Service中新增屬性PAGECOUNT。 NPR-28922:CQ-4270870的修補程式
* 僅限OSGi:已啟用支援，可使用Forms Service建立靜態PDF檔案。 NPR-28572:CQ-4270869的修補程式
* 為管理員和根用戶啟用對XMLForm.exe的權限。 NPR-29237:CQ-4267080的修補程式

### OSGi組合和內容套件

下列文字檔案列出AEM 6.5.1.0中包含的OSGi組合和內容套件

AEM 6.5.1.0隨附的OSGi搭售清單

[取得檔案](assets/6_5-bundle-list.txt)

AEM 6.5.1.0內容套件清單

[取得檔案](assets/6_5-content-package-list.txt)
