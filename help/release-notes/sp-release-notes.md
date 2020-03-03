---
title: AEM 6.5 Service pack發行說明
description: Adobe Experience Manager 6.5 Service Pack 3的發行說明。
uuid: c7bc3705-3d92-4e22-ad84-dc6002f6fa6c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 25542769-84d1-459c-b33f-eabd8a535462
docset: aem65
translation-type: tm+mt
source-git-commit: 9f4a460c7f64d86e35e950e512ed5b6cda1cbf2a

---


# Adobe Experience Manager 6.5 Service pack發行說明 {#aem-service-pack-release-notes}

## 發行資訊 {#release-information}

| 產品 | **Adobe Experience Manager 6.5** |
|---|---|
| 版本 | 6.5.3.0 |
| 類型 | Service pack版本 |
| 日期 | 2019年12月12日 |
| 下載URL | [PackageShare](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.3.0) |

## Adobe Experience Manager 6.5.3.0包含的功能 {#what-s-included-in-aem}

Adobe Experience Manager 6.5.3.0是重要的發行版本，其中包括自2019年4月6.5版全面推出以來的效能、穩定性、安全性和重要客戶修正與增強 **功能**。 它可安裝在Adobe Experience Manager(AEM)6.5之上。

此Service pack版本的一些主要亮點是：

* 內建儲存庫(Apache Jackrabbit Oak)已更新至1.10.6版。

* Experience Manager Assets現在支援使用Deflate 64演算法建立的ZIP封存。

* 已在DAM清單檢視中新增可排序的建立日期新欄，並在清單檢視中新增資產搜尋結果。

* 已在「清單」檢視中啟用「名稱」欄的資產排序。

* 動態媒體現在支援智慧型裁切視訊資產。 Smart Crop是機器學習驅動的功能，可在移動影格時重新裁切視訊，以跟隨場景的焦點。

* 動態媒體支援智慧型影像。

* 能夠在 [AEM工作流程中設定](../forms/using/configure-out-of-office-settings.md) 「Out of Office」偏好設定。

* 可在AEM工 [作流程中與其他使用者共用「收件匣](../forms/using/configure-shared-queues-osgi.md) 」或「收件匣」項目。

* 能夠在 [批次模式中產生互動式通訊](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)。

* ContextHub中已整合的jQuery更新版本至3.4.1。

### 變更清單 {#list-of-changes}

#### 資產 {#assets-6530-enhancements}

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

* DAM中的XSS弱點(NPR-31654)。

#### 網站 {#sites}

* 如果LiveCopy繼承中斷，即時副本頁面會顯示語言副本連結，而非LiveCopy連結(NPR-30980)。
* 對於新的Blueprint，如果記錄數超過40，則只會顯示前40個記錄。 Blueprint會為其餘的記錄顯示空白行(NPR-31182)。
* 當使用者在功能表的description屬性中新增日文或韓文字元時，功能表會顯示日文和韓文文字的扭曲字元。 (NPR-31331)。
* Rich Text Editor(RTE)不允許將嵌入的表作為清單項插入(NPR-30879)。
* 立即可用的架構Rich Text Editor(RTE)。 意外地將內嵌字型大小套用至元素(NPR-31284)。
* 當使用者專注在左側欄位並使用鍵盤快速鍵貼上內容時，會貼上頁面編輯器剪貼簿的內容，而非從左側欄位複製的內容(NPR-31172)。
* 當用戶將「檔案上傳」欄位添加到多欄位時，影像路徑儲存在元件節點中，而不是多欄位節點(NPR-30882)。
* ResponsiveGridExporter API不會傳回com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter介面。 com.day.cq.wcm.foundation.model.impl套件宣告為私用套件(NPR-31398)。
* 在非編輯器模式(在「作者」中(不含首碼和 `editor.html``wcmmode=disabled`，或在「發佈者」中)中開啟包含某些ExperienceFragments的頁面時，請求會以HTTP狀態錯誤碼500(NPR-30743)結束。
* 使用者無法變更密碼並存取其描述檔頁面(NPR-31161)。
* 在伺服器端產生包含使用者資料的JavaScript檔案(NPR-30822)。
* AEM製作UI可讓您使用外部內容進行網路釣魚(NPR-29745)。
* AEM 6.5中繼資料編輯器中的運算式語言插入弱點(NPR-31017)。

#### 搜尋與使用者介面 {#search-ui-interface}

* 從搜尋結果頁面的「卡片」檢視切換至「清單」檢視時，在可捲動頁面之前會有延遲(NPR-31286)。

* 「全選」核取方塊會隱藏在「網站UI」的「清單」檢視中(NPR-31614)。

* 搜尋結果頁面上的「全選」計數不正確(NPR-31120)。

* 中繼資料編輯器會顯示不存在的標籤(NPR-31119)。

#### 轉換 {#translation}

* 在翻譯工作中選擇「到期日期」選項時，會出現兩個日曆彈出式選項(NPR-31270)。

#### 平台 {#platform}

* Web控制台中的Mime類型選項無效(NPR-31108)。

* 在設定單一登入時不接受用戶端憑證(NPR-31165)。

* 不會儲存Jetty型HTTP服務緩衝區大小設定的更新(NPR-30925)。

* QueryBuilder現在支援 ``fn:name()`` xpath查詢中的orderby(NPR-31322)。

* 從AEM 6.3升級時會建立重複的啟動樹狀結構(NPR-31513)。

* 轉送的請求不會保留在sling驗證期間設定的回應標頭(NPR-30013)。

* 在機械臂元件中搜索無法工作(NPR-31692)。

* 由於Apache POI和Apache Tika搭售版本不同，將ZIP檔案附加至AEM Communities貼文時會顯示錯誤(NPR-31018)。

* 包 ``org.apache.sling.distribution.api`` 在配置管理器中隱藏，因此無法用於定制包(NPR-31720)。

#### 專案 {#projects}

* 切換日曆視圖無效(NPR-31271)。

#### 品牌入口網站 {#assets-brand-portal}

**產品增強功能**

* AEM Assets中的「資產來源補充」匯入工作流程已修改為僅將新建立的資產從Brand Portal擷取至AEM，並略過NEW檔案夾中已存在的資產，以避免複製(CQ-4278527)。

**修正**

* 在「資產來源補充」功能中建立新的「貢獻」檔案夾時，會出現不正確的圖示(CQ-4282825)。
* 建立新的「貢獻」檔案夾時，「貢獻」檔案夾中不會顯示一或兩個子檔案夾（NEW和SHARED）(CQ-4282424)。
* 如果使用者在從品牌入口網站端接收「貢獻」檔案夾中的新資產後，嘗試從AEM將「貢獻」檔案夾重新發佈至品牌入口網站，系統會引發例外(CQ-4279740)。
* 禁止在「貢獻」檔案夾（巢狀檔案夾）中建立「貢獻」檔案夾，以避免複雜性(CQ-4278391)。
* 系統會在上傳從AEM Admin Console匯入的品牌入口網站使用者清單（.csv檔案）時引發例外。 .csv檔案中只有「電子郵件」、「名字」和「姓氏」欄位是必填欄位(CQ-4278390)。

#### 社群 {#communities}

**修正**

* 社群管理員（群組管理員／網站管理員）看不到管理群組的快速連結（開啟／編輯／發佈／刪除群組）(NPR-31627)。
* 除非手動刷新／重新載入頁面，否則不會顯示已提交的部落格(NPR-31599)。
* 「提及次數」功能使用的JCR查詢區分大小寫，而且傳回結果需要太長時間(NPR-31475)。
* AEM 6.5 uberJar檔案拋出例 `cq-social-translation` 外，從AEM 6.5 uberJar檔案中遺失Bundle(NPR-31186)。
* Jackson Databind程式庫已更新至2.9.9.3版，以解決新的弱點(NPR-30967)。
* 活動和通知標題不一致(NPR-30941)。
* 在社群部落格中編頁無法正常運作(NPR-30914)。
* Analytics報表未填入AEM作者環境，空白頁面會出現(NPR-30913)。

#### 奧克 {#oak}

* Lucene索引更新導致作者伺服器速度變慢(NPR-31548)。

#### 表單 {#forms-6530}

>[!NOTE]
>
>AEM Service pack不包含AEM Forms的修正。 它們是使用個別的Forms附加套件傳送。 此外，還會發行包含JEE上AEM Forms修正的累積安裝程式。 如需詳細資訊，請 [參閱「在JEE上安裝AEM Forms附加元件](#install-aem-forms-add-on-package)[和安裝AEM Forms」](#install-aem-forms-jee-installer)。

##### Forms附加套件 {#forms-add-on-package-6530}

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

##### JEE安裝程式上的表格 {#forms-jee-installer-6530}

**表單——檔案服務**

* 在。NET專案中使用MTOM的SOAP web service會顯示AssemblerServiceClient叫用和HtmlToPDF2方法的例外(NPR-4281771)。

**Foundation JEE**

* 動作設定不會載入「叫用表單工作流程」提交動作的程式名稱(NPR-31478)。
* JEE上的AEM Forms使用者在匯入。lca檔案或在管理控制台中設定LDAP時，會遇到類似下列的錯誤：

   `com.ibm.ws.webcontainer.filter.FilterInstanceWrapper doFilter SRVE8109W: Uncaught exception thrown by filter um: java.lang.NoClassDefFoundError: org/apache/commons/io/IOUtils at org.apache.commons.fileupload.util.Streams.copy`

   `Error 500: javax.servlet.ServletException: java.lang.NoClassDefFoundError: org.apache.commons.io.IOUtils` (NPR-30931)


### 隨附的功能套件 {#feature-packs-included-6530}

>[!NOTE]
>
>對於AEM Forms客戶，在安裝任何AEM Service Pack、Cumulative Fix Pack或Feature Pack後，必須安裝AEM Forms附加套件。

#### 表單- Foundation JEE {#forms-foundation-jee-feature}

* AEM Forms對Oracle 18c的支援(NPR-29155)。

## Install 6.5.3.0 {#install}

**設定需求**

* AEM 6.5.3.0需要AEM 6.5。請查看 [升級檔案](/help/sites-deploying/upgrade.md) ，以取得詳細指示。
* Adobe Package Share提供Service pack下載，您可以直接從AEM 6.5執行個體存取。
* 在使用MongoDB和多個執行個體的部署中，使用「套件管理員」將AEM 6.5.3.0安裝在其中一個「作者」執行個體上。
* 在安裝Service Pack之前，請確定您有AEM例項的快照或新鮮備份。
* 在安裝之前重新啟動實例。 雖然只有在實例仍處於更新模式時才需要此選項（這是從舊版更新實例時的情況），但建議在實例運行較長時段時使用此選項。

>[!CAUTION]
>
>Adobe不建議移除或解除安裝AEM 6.5.3.0套件。

### 透過Package Share安裝Service Pack {#install-service-pack-via-package-share}

請執行下列步驟，在現有的AEM 6.5執行個體上安裝Service Pack:

1. 從AEM登入至「Package Share」（封裝共用），或直接從您的瀏覽器登入並下載 [AEM 6.5.3.0套件](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.3.0)。

1. 使用Package Manager安裝下載的套件。

>[!NOTE]
>
>**在安裝6.5.3.0時，Package Manager UI上的對話有時會無法正常退出**
>
>因此，建議您先等待錯誤記錄穩定，再存取執行個體。 在確保安裝成功之前，用戶必須等待與卸載更新程式包相關的特定日誌。 通常在Safari上會發生，但在任何瀏覽器上都會偶爾發生。

**自動安裝**

有兩種方式可自動將AEM 6.5.3.0安裝至執行中的例項：

答：將套件放入……*/crx-quickstart/install* folder whe the server is available online. 軟體包會自動安裝。

B.使用 [Package Manager的HTTP API](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html) —— 請確定您使用cmd=install&amp;recursive=true —— 如此便會安裝巢狀封裝。

>[!NOTE]
>
>AEM 6.5.3.0不支援Bootstrap安裝。

**驗證安裝**

1. 「產品資訊」頁面(/system/console/ productinfo)會在「已安裝產品」下顯示更 `Adobe Experience Manager, Version 6.5.3.0` 新的版本字串。

1. 所有OSGi捆綁包都 **[!UICONTROL 是OSGi控制台中的]****[!UICONTROL ACTIVE或FRAGMENT]** (使用Web控制台：/system/console/bundles)。
1. OSGI套件org.apache.jackrabbit.oak-core是1.10.6版或更新版本(使用Web Console:/system/console/bundles)。

若要查看哪些平台已通過此版本的認證，請參閱技術 [要求](/help/sites-deploying/technical-requirements.md)。

### 安裝AEM Forms附加元件套件 {#install-aem-forms-add-on-package}

>[!NOTE]
>
>如果您不使用AEM Forms，請略過。 AEM Forms中的修正是透過個別的附加套件傳送。

>[!NOTE]
>
>AEM 6.5.3.0包含新版 [AEM Forms Compatibility套件](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/compatpack/AEM-FORMS-6.5.3.0-COMPAT)。 如果您使用舊版AEM Forms Compatibility套件並更新至AEM 6.5.3.0，請在安裝Forms Add-On套件後安裝最新版的AEM Forms Compatibility套件。

1. 請確定您已安裝AEM Service Pack。
1. 下載您作業系統的 [AEM Forms版本中列出的對應Forms附加元件套件](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 。
1. 如安裝AEM Forms附加元件套件中所述，安 [裝Forms附加元件套件](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package)。

### 在JEE上安裝AEM Forms {#install-aem-forms-jee-installer}

>[!NOTE]
>
>如果您未在JEE上使用AEM Forms，請略過。 JEE上的AEM Forms中的修正會透過個別安裝程式提供。

如需在JEE上安裝AEM Forms累積安裝程式和部署後設定的詳細資訊，請參閱修補程 [式0007的發行說明](https://helpx.adobe.com/aem-forms/quick-fixes/6-5/jee-patch-0007.html)。

#### 工作台安裝程式

由於是完整安裝程式，因此與修補程式版本相比，檔案大小更大。 在安裝新版本之前，請先解除安裝舊版Workbench。

## UberJar {#uber-jar}

Adobe Public Maven儲存庫中提供UberJar for AEM 6.5.3.0 [](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.3/)。

要在Maven項目中使用UberJar，請參閱 [How to use UberJar](/help/sites-developing/ht-projects-maven.md) and include the following dependency in your project POM:

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version>6.5.3.0</version>
      <classifier>apis</classifier>
      <scope>provided</scope>
</dependency>
```

## Deprecated Features {#removed-deprecated-features}

本節列出已標示為不再支援的AEM 6.5.3.0功能。計畫在未來版本中移除的功能會先設為不建議使用，並提供替代選項。

建議客戶在目前的部署中是否使用功能，並規劃變更實施以使用替代選項。

| 區域 | 功能 | 替代方案 |
|---|---|---|
| 整合 | AEM Cloud **[!UICONTROL Services選擇加入畫面已過時]** 。 隨著AEM 6.5中的AEM和Target整合更新，以支援Target Standard API（透過Adobe IMS和I/O使用驗證），以及Adobe Launch在檢測AEM頁面以進行分析和個人化方面的角色日漸增加，「選擇加入」精靈在功能上已變得無關緊要。 | 透過個別的AEM雲端服務，設定系統連線、Adobe IMS驗證和Adobe I/O整合 |

## 已知問題 {#known-issues}

* 如果 **Connected Assets configuration** wizard在安裝AEM 6.5.3.0後傳回404錯誤訊息，請使用Package Manager手動重新安裝 **cq-remotedam-client-ui-content** 和 **** cq-remotedam-client-ui-components套件。
* 在安裝AEM 6.5.x.x時，可能會顯示下列錯誤和警告訊息：
   * 「當使用Target Standard API（IMS驗證）在AEM中設定Target整合時，將「體驗片段」匯出至Target會導致建立錯誤的選件類型。 Target會以「HTML」/來源「Adobe Target Classic」類型建立數個選件，而非「Experience Fragment」/來源類型「Adobe Target Classic」。
   * com.adobe.granite.maintenance.impl.TaskScheduler:在granite/operations/maintenance中找不到維護視窗。
   * 當使用SUM、MAX和MIN等集合函式時，Adaptive Form伺服器端驗證將失敗。 CQ-4274424
   * com.adobe.granite.maintenance.impl.TaskScheduler —— 在granite/operations/maintenance找不到維護視窗。
   * 透過可購買橫幅檢視器預覽資產時，不會顯示動態媒體互動影像中的熱點。

## 隨附的OSGi組合和內容套件 {#osgi-bundles-and-content-packages-included}

下列文字檔案列出AEM 6.5.3.0隨附的OSGi組合和內容封裝

AEM 6.5.3.0隨附的OSGi搭售清單

[取得檔案](assets/6530_bundles.txt)

AEM 6.5.3.0內容套件清單

[取得檔案](assets/sp_6530_packages.txt)

## Helpful Resources {#helpful-resources}

* [AEM 6.5版本注意事項](/help/release-notes/release-notes.md)
* [AEM產品頁面](https://www.adobe.com/marketing/experience-manager.html)
* [AEM 6.5 檔案](https://helpx.adobe.com/support/experience-manager/6-5.html)
* 訂閱 [Adobe優先產品更新](https://www.adobe.com/subscription/priority-product-update.html)

## 受限制的網站 {#restricted-sites}

這些網站僅提供給客戶使用。 如果您是客戶，需要存取權，請連絡您的Adobe客戶經理。

* [產品下載，請造訪licensing.adobe.com](https://licensing.adobe.com/)
* [聯絡客戶支](https://daycare.day.com/public/contact.html)援如需有關存取支援入口網站的詳細資訊，請 [參閱存取支援入口網站](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html)。
