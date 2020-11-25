---
title: '[!DNL Adobe Experience Manager] 6.5 Service Pack發行說明'
description: ' [!DNL Adobe Experience Manager] 6.5 Service Pack 7的發行說明'
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 0389508f7870dd2ce6ed7bfc5fb8a9bc88fedffb
workflow-type: tm+mt
source-wordcount: '3796'
ht-degree: 0%

---


# [!DNL Adobe Experience Manager] 6.5 Service Pack發行說明 {#aem-service-pack-release-notes}

## Release information {#release-information}

| 產品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.7.0 |
| 類型 | Service Pack版本 |
| 日期 | 2020年11月26日 |
| 下載URL | [軟體散發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.7.zip) |

<!-- TBD: Update the SD link when SP7 is available. -->

## 6.5.7. [!DNL Adobe Experience Manager] 0包含的功能 {#what-s-included-in-aem}

[!DNL Adobe Experience Manager] 6.5.7.0是重要的更新，其中包括自2019年4月6.5版推出以來，新功能、主要客戶要求的增強功能，以及效能、穩定性和安全性增強功能。 Service Pack已安裝 [!DNL Adobe Experience Manager] 在6.5。

6.5.7.0中引進的主要功 [!DNL Adobe Experience Manager] 能和增強功能包括：

* 使用「名稱」、「上次修改日期」和「上次轉出日期 [!UICONTROL 」屬性，對可供轉出的即時]副本頁面 [!UICONTROL 進行排序] 。

* 執行頁面移動和MSM展開作為非同步操作，以降低它們對執行時期效能的影響。

* 使用者可以在「卡片」和「欄」檢視中排序數位資產。

* [!DNL Assets] 並提供 [!DNL Dynamic Media] 多種協助工具增強功能。 這些增強功能與鍵盤導覽、螢幕閱讀程式的使用，以及讓使用者使用類似的輔助技術(AT)有關。 請參 [[!DNL Assets] 閱增強](#assets-6570) 和 [[!DNL Dynamic Media] 增強功能](#dynamic-media-6570)。

* 內建儲存庫(Apache Jackrabbit Oak)已更新至1.22.5版。

如需 [!DNL Experience Manager] 6.5.7.0中推出的完整功能與增強功能清單，請參 [閱 [!DNL Adobe Experience Manager] 6.5 Service Pack 7的新增功能](new-features-latest-service-pack.md)。

以下是6.5.7.0版中提供 [!DNL Experience Manager] 的修正清單。

### [!DNL Sites] {#sites-6570}

* 當您開啟頁面的 [!UICONTROL Timewrap] (繞圖排時 [!UICONTROL )選項、保持「時間軸」側邊欄選項的開啟，並導覽至] Sites `Failed to Load` Console時，會發生錯誤(NPR-34951)。

* 「 [!UICONTROL 繞時] 」選項不會顯示所選日期和時間範圍的影像(NPR-34951)。

* 當從含有內 `getHeader()` 容片段的頁面呼叫篩選器時， `java.lang.AbstractMethodError` 會發生錯誤(NPR-34942)。

* 當頁面的路徑包含多個內容子字串時，預覽無法轉譯，而版本比較功能也會失敗(NPR-34740)。

* 為元件的類型標籤屬性設 `String` 置數值時，可以刪除元件並撤消刪除操作。 但是，撤消刪除後，label屬性將從 `String` 變 `Long` 為(NPR-34739)。

* 根據具有鎖定版面的範本新增體驗片段至頁面時發生下列例外(NPR-34632):

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.mozilla.javascript.EcmaError: TypeError: Cannot call method "getChildren" of null
   ```

* 移動資料夾時，會導致遍歷問題，並出現以下錯誤(NPR-34554):

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript. org.apache.jackrabbit.oak.query.RuntimeNodeTraversalException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped
   ```

* 當建立、發佈新資產並移至新位置時，工作流程 `Request to complete move operation` 就會建立並導致「已中止」狀態。 上傳新資產並執行 `move` 操作會導致建立處於待 `Request to complete move operation` 定狀態的工作流(NPR-34543)。

* 從 [!DNL Experience Manager] 6.5.2環境將體驗片段匯出至 [!DNL Target] Standard時，API呼叫會失敗，因為工作區屬性不適用於 [!DNL Target] Standard(NPR-34557)。

* 使用者無法透過「管 [!UICONTROL 理出版物] 」選項發佈頁面，因  為「發佈」選項消失(NPR-34542)。

* 當您在文字中新增一些樣式時， `<div>` 會在文字中新增標籤，而且樣式無法再套用至文字(NPR-34531)。

* 當您在彈出式選單中選取項目並更新所需檔案時，它不允許儲存對話方塊值，因為其他選單有空的必填欄位(NPR-34529)。

* 當您從自訂範本建立頁面並在Blueprint階層中移動時，先前從頁面刪除的元件會開始顯示在即時副本階層中的頁面上(NPR-34527)。

* 文章樣式套用至內容後，就無法移除(NPR-34486)。

* 體驗片段的所有即時副本和副本都指向相同的 [!DNL Adobe Target] 選件ID(NPR-34469)。

* 項目符號清單項除了編號清單外還顯示(NPR-34455)。

* 比較來源選項無法顯示來源頁面與編輯過的頁面版本之間的差異(NPR-34285)。

* 刪除頁面時，版本控制詳細資訊不可配置(NPR-34159)。

* 當使用者選取「開啟選 [!UICONTROL 取範圍] 」對話方塊選項時，鍵盤焦點會移至頁面上顯示的隱藏控制項(CQ-4307779、CQ-4293601)。

* 當您在「作者」上移動已發佈的檔案夾時，「發佈」例項上的檔案夾路徑不會相應更新(CQ-4305144)。

* 當使用者在「全選 `Enter` 」選項中選 [!UICONTROL 取鍵時，鍵盤焦點不會移至「] Create Control  」（建立控制）選項(CQ-4293599)。

* 當您選取 `Esc` 金鑰時，焦點不會還原至父項控制項(CQ-4293593、CQ-4293590)。

* 已改善UI和核 [!DNL Sites] 心元件的WCAG相容性(CQ-4293448)。

* [!UICONTROL 頁面的縮放] (Zoom [!UICONTROL )和縮放(Scale] )功能 [!DNL Sites Editor] 已停用(CQ-4282353)。

* 使用「向右旋轉」選項後，螢幕閱讀程式會停止旁白目前旋轉或反向狀態(CQ-4282128)。

* 「完成」和「取消設定」對話方塊按鈕有多個制表位(CQ-4274601)。

* 不允許在相同層級移動具有類似名稱的頁面(NPR-35041)。

* 選取「清除(x)」選項後，鍵盤焦點不會移至「篩選 [!UICONTROL 器] 」欄位(CQ-4293581)。

* 升級至 [!DNL Experience Manager] 6.5.6.0時，繼承段落系統的行為會改變，而且無法正常運作(NPR-35117)。

* 在選取頁面上的「動作」區段後，鍵盤使用者無法以適當順序 [!DNL AEM Sites] 移動標籤焦點(CQ-4307786)。

* 在編輯內容片段時，在RTE工具列的連結目標選單清單中選取選項後，內容片段作者對話會開始閃爍(CQ-4305532)。

* 鍵盤使用者無法使用向下鍵( [!UICONTROL CQ-4295097)，在「新增元件] 」下拉式清單中選取選項。

* 從頁面「資產」標籤的「日曆」功能表選取日期時，標籤焦點不會 [!DNL Sites] 以適當順序移動(CQ-4293600)。

* 刪除編輯網站頁面時可用的連結或文字選項後，標籤焦點不會移至鍵盤使用者的下一個或上一個選項(CQ-4293597)。

* 在檢視可用選項並按鍵後，鍵盤使用者無法將標籤焦點移回「 [!UICONTROL Actions] 」（動作）區 `Esc` 段中的「More」（更多）選項(CQ-4293592)。

* 當您在「編輯」模式中啟 [!UICONTROL 動影像的「旋轉] 」選項時，標籤焦點會移至鍵盤使用者的「重做」選項(CQ-4293587)，而非停留在「旋轉」上。

* 在「連結 [!UICONTROL 與動作」標籤上的「開啟選取範圍] 」對話方塊中，標籤焦點會在「取消」選項( [!UICONTROL Cancel] )後移至頁面中的隱藏元素(CQ-4293579)。

* 當鍵盤使用者編輯影像、導覽至 [!UICONTROL Finish] （完成）選項，然後按Enter鍵時，螢幕閱讀程式不會宣佈完成(CQ-4282351)。

* 螢幕閱讀程式和鍵盤使用者無法使用「 [!UICONTROL Link and Actions] 」（連結和動作）對話方塊中的「Move up and Move down」（上移和下移）選項(CQ-4281120)。

* 在導覽至「屬性」頁面上的「關閉(X)」選項( [!UICONTROL Properties] (CQ-4293581、NPR-34653)後，鍵盤使用者無法還原標籤焦點。

### [!DNL Assets] {#assets-6570}

[!DNL Adobe Experience Manager] 6.5.7.0修 [!DNL Assets] 正了下列問題並提供下列增強功能。

* 本版次針對協助工具執行下 [!DNL Experience Manager Assets] 列增強功能。 如需詳細資訊，請參 [閱中的協助功能 [!DNL Assets]](/help/assets/accessibility.md)。

   * 使用鍵盤導覽時間軸時， `Esc` 鍵可以收合「全 [!UICONTROL 部顯示] 」選項，而不會失去焦點(CQ-4293598)。
   * 使用鍵盤標籤鍵導覽時，從新增的標籤移除最後一個標籤後，標籤欄位會保留焦點(NPR-35109)。
   * [!DNL Experience Manager] 元件現在包含螢幕閱讀程式使用之名稱、角色和值的適當資訊(NPR-34255)。
   * 刪除「文字／大小」組合框、「連結」組合框、「語言」組合框或「文本」編輯框後，鍵盤焦點將返回下一個或上一個用戶介面元素或更相關的用戶介面元素(CQ-4293585)。
   * 當將指標暫留在各種選項上時，會出現「選取」和「下載」等提示。 使用螢幕放大率的使用者可能會因懸停而無法檢視檔案縮圖，因為顯示的內容。 現在，在使用鍵移除選項後，可以保 `Escape` 留焦點(CQ-4293554)。
   * 從頁面中顯示的格線選取格線儲存格後，焦點會移至螢幕上顯示的動作列(CQ-4282127)。
   * 視覺使用者可區分一般文字和連結，因為首頁中所有解決方案的連結會顯示視覺線索（底線和雪佛龍圖示）( [!DNL Experience Manager] CQ-4282072)。

* 下列使用者體驗增強功能可在下列位置進行 [!DNL Assets]:

   * 啟用卡片檢視和欄檢視中資產排序(NPR-35097)。

* 升級至6.5後，如果使用Assets HTTP API產生JSON檔案，則檔案中使用的編碼會發生問題(NPR-35129)。

* 未提供建立系列權限的群組的使用者（「建立系列」選項無法使用）仍可以直接存取URL來建立系 `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/collections/createcollectionwizard.html/content/dam/collections?contentPath=/content/dam/collections` 列(NPR-35115)。

* 依名稱排序時，搜尋的資產會以區分大小寫的方式排序。 這會根據在搜尋結果中以順序顯示的外框，建立兩個不同的排序清單(NPR-35068)。

* 在編輯器中開啟內容片段時，警告訊息(`Invalid value specified for a metadata property`)會記錄在錯誤記錄檔中(NPR-35012)。

* 沒有管理員權限的使用者可以使用 [Experience Manager] desktop應用程式編輯過期的資產。 (NPR-34993)。

* 當在「資產」使用者介面上拖曳相同的「資產」並建立新版本時，中繼資料中的變更不會持續存在(NPR-34940)。

* 編輯系列時，使用者可以刪除系列的標題並成功儲存變更(NPR-34889)。

* 上傳重複影像時，會顯示刪除選項。 選取刪除可讓影像上傳。 也會觸發DAM更新資產工作流程(NPR-34744)。

* 搭配使 [!DNL Adobe Asset Link] 用 [!DNL Adobe InDesign]時，搜尋結果不包含資料夾和系列，但僅包含資產(NPR-34699、CQ-4303666)。

* 將滑鼠指標暫留在卡片檢視上，讓螢幕捲動的結果是（自動）將焦點放在卡片中可用的快速動作(NPR-34514)。

* 大量編輯多個資產的屬性時，選取「儲存」 [!UICONTROL 選項] ，會關閉大量編輯器檢視並重新導向至主 [!DNL Assets] 頁面。 此行為與「儲存並關閉」選 [!UICONTROL 項的行為相同] ，且不預期出現(NPR-34546)。

* 智慧型系列在儲存後未顯示正確的使用者介面設定。 查詢已正確保存，但介面始終顯示上次添加的Option謂語(NPR-34539)。

* 將資產新增至 [!DNL Experience Manager]時，沒有命名空間的中繼資料不會匯入(NPR-34530)。

* 拖曳資料夾上的資產以移動資產時，使用者介面也會顯示「放入燈箱 [!UICONTROL 」和「放] 入系列」選項 。 即使取消移動操作，用戶介面仍繼續顯示後兩個選項(NPR-34526)。

* 符號會 `%>` 顯示在系列頁面上(NPR-34499)。

* 在欄檢視中， [!DNL Assets] 在向上和向下捲動所有資產之前，顯示重複的資料夾和資產名稱(NPR-34464)。

* 如果在建立公用資料夾後立即建立專用資料夾，則公用資料夾使用專用資料夾設定(NPR-34415)。

* 在卡片檢視中，卡片未以字母順序列出，而且卡片無法以字母順序排序(NPR-34234)。

* 重新開啟階層式規則時，使用者介面上不會保留這些選項(CQ-4301452)。

#### [!DNL Dynamic Media] {#dynamic-media-6570}

* 下列增強功能適用於協助工具( [!DNL Dynamic Media] CQ-4290306)。 如需詳細資訊，請參 [閱中的協助功能 [!DNL Dynamic Media]](/help/assets/accessibility-dm.md)。

   * 螢幕閱讀程式（JAWS，旁白）會在「內嵌大小」功能表選項(CQ-4290927)中，說明功能表項目的名稱、角色和狀態。
   * 使用者可使用金鑰來導覽「電子郵件 `Tab` 連結」對話方塊(CQ-4290926)。
   * 建立視訊編碼設定檔的工作流程更容易使用，因為螢幕閱讀器增強功能(CQ-4290623、CQ-4290622)。
   * 使用鍵導 `Tab` 覽時，焦點會移至工作流程中適當的使用者介面元素，以建立互動式視訊(CQ-4290621、CQ-4290620、CQ-4290619)。
   * 「發佈」頁、「編輯資產」頁、「編輯智慧裁切」頁和「影像集編輯器」頁已經過改良，以符合Web標準。 協助技術(AT)使用者現在可輕鬆導覽這些頁面，並採取裁切影像等動作(CQ-4290617、CQ-4290616、CQ-4290613、CQ-4290612、CQ-4290610、CQ-4290614)。
   * 檢視器已改良，可讓使用者使用鍵盤進行導覽(CQ-4290615)。
   * 鍵盤和螢幕閱讀程式使用者可使用裁切功能(CQ-4290609)。
   * 鍵盤用戶可以更好地管理熱點(CQ-4290604、CQ-4290603)。

* 如果公司名稱和資料夾 [!DNL Experience Manager] 名稱相同，則無法編輯遠端影像集(NPR-31340)。

* 在將熱點新增至影像或編輯視訊或包含影像後，嘗試預覽 [!DNL Dynamic Media][!DNL Dynamic Media][!DNL Experience Fragment] 輸出時，z索引順序不正確(CQ-4307267)。

* [!DNL Dynamic Media] 重新處理混合媒體集時同步失敗(CQ-4307184)。

* 如果資產移至已設定自動同步至的資 [!DNL Dynamic Media] 料夾，則資產不會同步(CQ-4307122)。

* [!DNL Dynamic Media] 使用原生HTML5視訊控制項(CQ-4306977、CQ-4306727)的iOS裝置上無法播放視訊。

* 無法下載應用SmartCrop的映像(CQ-4304558)。

* 無法選擇性地發佈資料夾至動態媒體(CQ-4304526)。

* 從中取消發佈視訊檔 [!DNL Experience Manager] 案時，不會從已設定的Scene7部署中解除發佈最適化視訊集(CQ-4304405)。

* 在全景媒體元件中新增全景影像資產並重新整理頁面會 `Uncaught ReferenceError: $ is not defined` 導致錯誤(CQ-4302810)。

* 在檢視 [!UICONTROL 器預設集編輯器中]，編輯 [!UICONTROL PanoramicImage/PanoramicImage_VR] 預設集時，元件中不提供 `PanoramicView``PANORAMICVIEW_AUTOROTATE` 修飾元標籤(CQ-4302443)。

* 如果視訊不是MixedMediaSet中的第一個視訊標題，則不會顯示視訊標題(CQ-4298161)。

* iPhone行動裝置上的HTML5 eCatalog檢視器無法翻頁或翻頁(CQ-4296611)。

* 在行動裝置上捲動色票時，色票會捲動至可見區域的右側和外側數秒，然後再捲動回檢視(CQ-4296439)。

* 當建立檢視器預設集主要記錄時，不會發佈CSS和圖稿，只會發佈檢視器預設集(CQ-4262205)。

* 嘗試在互動式視訊／影像元件中連結特定熱點的體驗片段時  ，不會顯示選取的體驗片段路徑。 而是從路徑欄位傳回空值(NPR-35146、CQ-4298136)。

* 無法在IVV編輯器中預覽體驗片段(CQ-4308560)。

* 將熱點新增至影像並選取「體驗片段」時，無法選取子檔案夾和「體驗片段」的變體(CQ-4307455)。

* 上傳後，非影像資產不會顯示為已發佈(CQ-4306415)。

#### [!DNL Experience Manager] 3D資產 {#three-d-assets-6570}

* `DAM CQ MIME Type` 服務會將不正確的MIME類型套用至3D資產，導致不正確的轉譯(NPR-34731)。

### [!DNL Commerce] {#commerce-6570}

* 「商務」產品收集使用者介面不會列出一個系列中超過15種產品(NPR-34502)。

### 平台 {#platform-6570}

* HTTP會話通過HTTPS不會失效(NPR-35083)。
* 從用 `NullPointerException` 戶介面啟動每日或每週維護任務時返回(NPR-34953)。
* W3C驗證器會報告相容用戶端程式庫JavaScript檔案的警告(NPR-34898)。
* 此函 `AudienceOmniSearchHandler` 數使用不建議使用的索引(NPR-34870)。
* 從Experience Manager登出無法清除Cookie(NPR-34743)。
* 如 `findByTitle` 果標籤名 `TagManager` 稱包含特殊字元(NPR-34357),API的函式就無法運作。
* 導入用戶同步包的過程失敗(NPR-34399)。
* 新增對元 `ariaLabel` 件和 `ariaLabelledby` 屬性的 `Coral.Masonry` 支援(GRANITE-29962)。
* 安裝最新核心元件封裝後，不會重新整理含有內容片段的頁面的Dispatcher快取(CQ-4306788)。
* 使用者介面上無法正確顯`"`示帶引號()的本地化標籤名稱(CQ-4305439)。

### 使用者介面{#ui-6570}

* 元件 [!UICONTROL 屬性中的] 「連結至」欄位會顯示不符合指定字串的自動完成建議(NPR-34865)。

* AEM會在您排程2天之間散發的每日維護視窗時顯示下列錯誤訊息(NPR-35280):

   ```TXT
   ERROR The start time must precede (be less than) the end time
   ```

### 整合 {#integrations-6570}

* 編輯現有 [!DNL Adobe Launch] 配置失敗(NPR-35045)。
* 如果使 [!DNL Experience Fragments] 用 [!DNL Adobe Target] IMS組態和環境，則無 [!DNL Adobe Target Standard] 法匯出至(NPR-34555)。
* 當從資 [!UICONTROL 料夾導覽至「觀眾」頁面時，「建立] 」選項會出現在「觀眾」頁面上(NPR  -35151)。

### Sling {#sling-6570}

* 預設登錄運行狀況檢查會驗證不存在的用戶的憑據(NPR-34686)。

### 翻譯專案 {#translation-6570}

* 在中取消翻譯項 [!DNL Experience Manager]目時，取消該項目的請求不會發送給翻譯提供商(NPR-34433)。

### [!DNL Communities] {#communities-6570}

* 產品中所有不公平術語的例子都被接受的等價物(NPR-34311)取代。
* [!DNL Google+] 已從社交共用選項清單中移除(NPR-33877)。

### [!DNL Brand Portal] {#brandportal-6570}

* 在選取清單檢視中的資產時，使用者介面 [!UICONTROL 不會回應] (NPR-34728)。

### [!DNL Forms] {#forms-6570}

>[!NOTE]
>
>[!DNL Experience Manager Forms] 在計畫的Service Pack發行日期後一週發行附 [!DNL Experience Manager] 加軟體包。

如需安全性更新的詳細資訊，請參 [閱Experience Manager安全性公告頁面](https://helpx.adobe.com/security/products/experience-manager.html)。

## Install 6.5.7.0 {#install}

**設定需求和詳細資訊**

* AEM 6.5.7.0需要AEM 6.5。如需詳 [細指示](/help/sites-deploying/upgrade.md) ，請參閱升級檔案。
* Adobe軟體散發提供Service Pack下 [載](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)。
* 在使用MongoDB和多個執行個體的部署中，使用「套件管理員」將AEM 6.5.7.0安裝在其中一個「作者」執行個體上。

>[!NOTE]
>
>Adobe不建議移除或解除安裝 [!DNL Adobe Experience Manager] 6.5.7.0套件。

### 安裝Service Pack {#install-service-pack}

執行下列步驟，將Service Pack安裝在現有的Adobe Experience Manager 6.5實例上：

1. 如果實例處於更新模式，則在安裝之前重新啟動實例（在從舊版更新實例時也是如此）。 Adobe也建議在執行個體目前的正常運作時間較長時重新啟動。

1. 在安裝之前，請拍下快照或 [Experience Manager實例的新備份] 。

1. 從「軟體散發」下載 [Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.7.zip)。

1. 開啟「套件管理員」，然後按 **[!UICONTROL 一下「上傳套件]** 」以上傳套件。 如需詳細資訊，請參 [閱套件管理器](/help/sites-administering/package-manager.md)。

1. 選擇軟體包，然後按一下 **[!UICONTROL 安裝]**。

1. 要更新S3連接器，請在安裝Service Pack後停止實例，用安裝資料夾中提供的新二進位檔案替換現有連接器，然後重新啟動實例。 請參 [閱Amazon S3 Data Store](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)。

>[!NOTE]
>
>在安裝Service Pack時，有時會退出Package Manager UI的對話方塊。 Adobe建議您在存取部署之前，先等待錯誤記錄穩定下來。 請等待與解除安裝更新程式套件相關的特定記錄，然後確定安裝成功。 通常，這會在任何瀏 [!DNL Safari] 覽器上發生，但是偶爾會發生。

**自動安裝**

在工作實例上自動安裝Adobe Experience Manager 6.5.7.0有兩種方法：

答：當伺服器聯機 `../crx-quickstart/install` 時，將軟體包放入資料夾。 軟體包會自動安裝。

B.使用套 [件管理員的HTTP API](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html)。 使 `cmd=install&recursive=true` 用以安裝巢狀包。

>[!NOTE]
>
>Adobe Experience Manager 6.5.7.0不支援啟動載入。

**驗證安裝**

1. 產品資訊頁面(`/system/console/productinfo`)會在「已安裝產品」下顯示更 `Adobe Experience Manager (6.5.7.0)` 新 [!UICONTROL 的版本字串]。

1. 所有OSGi捆綁包都 **[!UICONTROL 是OSGi控制台中的]****[!UICONTROL ACTIVE或FRAGMENT]** (使用Web控制台： `/system/console/bundles`)。

1. OSGi套件 `org.apache.jackrabbit.oak-core` 版本為1.22.3或更新版本(使用Web Console: `/system/console/bundles`)。

若要瞭解經過認證可與此版本搭配使用的平台，請參閱 [技術需求](/help/sites-deploying/technical-requirements.md)。

### 安裝Adobe Experience Manager Forms附加套件 {#install-aem-forms-add-on-package}

>[!NOTE]
>
>[!DNL Experience Manager Forms] 在計畫的Service Pack發行日期後一週發行附 [!DNL Experience Manager] 加軟體包。

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

如需在JEE上安裝Experience Manager Forms累積安裝程式和部署後設定的詳細資訊，請參閱版 [本說明](jee-patch-installer-65.md)。

### UberJar {#uber-jar}

UberJar for Experience Manager 6.5.7.0可在 [Maven Central儲存庫中取得](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.7/)。

要在Maven項目中使用UberJar，請 [瞭解如何使用UberJar](/help/sites-developing/ht-projects-maven.md) ，並在項目POM中包括以下相關性：

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.7</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar和其他相關對象可在Maven Central Repository(而不是Adobe Public Maven Repository(`repo.adobe.com`)上使用。 主UberJar檔案已更名為 `uber-jar-<version>.jar`。 因此，標籤 `classifier`沒 `apis` 有值的 `dependency` 存在。

## 過時的功能 {#removed-deprecated-features}

以下是標示為不再提倡的 [!DNL Experience Manager] 6.5.7.0功能清單。功能已標示為不建議使用，未來版本會先移除。 通常會提供替代選項。

檢視您在部署中是否使用功能。 此外，您也打算將實施變更為使用替代選項。

| 區域 | 功能 | 替代方案 |
|---|---|---|
| 整合 | AEM Cloud **[!UICONTROL Services選擇加入畫面已過時]** 。 隨著AEM 6.5中的AEM和Target整合更新，以支援Target Standard API（透過Adobe IMS和I/O使用驗證），以及Adobe Launch在檢測AEM頁面以進行分析和個人化方面的角色日漸增加，「選擇加入」精靈在功能上已變得無關緊要。 | 透過個別的AEM雲端服務，設定系統連線、Adobe IMS驗證和Adobe I/O整合。 |
| 連接器 | AEM 6.5不再支援Adobe JCR Connector for Microsoft SharePoint 2010和Microsoft SharePoint 2013。 | N/A |

## 已知問題 {#known-issues}

* 在安裝Experience Manager 6.5.7.0 `error.log` 期間，請忽略檔案中的下列錯誤：

   ```TXT
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy] :  Cannot register component (org.osgi.service.component.ComponentException: The component name 'com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy' has already been registered by Bundle 331 (com.day.cq.dam.cq-dam-core) as Component of Class com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy(1314)] : Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy (java.lang.ClassNotFoundException: com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy not found by com.day.cq.dam.cq-dam-core [331])
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy(1316)] : Could not load implementation object class com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy (java.lang.ClassNotFoundException: com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy not found by com.day.cq.dam.cq-dam-core [331])
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy(1315)] : Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy (java.lang.ClassNotFoundException: com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy not found by com.day.cq.dam.cq-dam-core [331])
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)BundleComponentActivator : Unexpected failure enabling component holder com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy (java.lang.IllegalStateException: Could not load implementation object class com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)BundleComponentActivator : Unexpected failure enabling component holder com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy (java.lang.IllegalStateException: Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy] :  Cannot register component (org.osgi.service.component.ComponentException: The component name 'com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy' has already been registered by Bundle 331 (com.day.cq.dam.cq-dam-core) as Component of Class com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy] :  Cannot register component (org.osgi.service.component.ComponentException: The component name 'com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy' has already been registered by Bundle 331 (com.day.cq.dam.cq-dam-core) as Component of Class com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)BundleComponentActivator : Unexpected failure enabling component holder com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy (java.lang.IllegalStateException: Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy)
   ```

* 如果您要將實 [!DNL Experience Manager] 例從6.5版升級至6.5.7.0版，則可以在檔案中查 `RRD4JReporter` 看異常 `error.log` 情況。 重新啟動實例以解決問題。

* 如果您在 [!DNL Experience Manager][!DNL Experience Manager] 6.5上安裝 `/var/workflow/models/dam`6.5 Service Pack 5或舊版Service Pack，則會刪除資產自訂工作流程模型（在中建立）的執行時期副本。
若要擷取您的執行時期副本，Adobe建議使用HTTP API，將自訂工作流程模型的設計時副本與其執行時期副本同步化：
   `<designModelPath>/jcr:content.generate.json`。

* 如果您在使用「定義規則」對話方塊在「資料夾中繼資料結構表單編輯器」和「中繼資料結構表單編輯器」中編輯和建立階層式規則時，遇到問題，請與Adobe客戶服務聯絡。  已建立和儲存的規則會如預期般運作。

* 如果階層中的檔案夾已重新命 [!DNL Experience Manager Assets] 名，且包含資產的巢狀檔案夾已發佈至 [!DNL Brand Portal]，則在中不會更新檔案夾的標題，直到 [!DNL Brand Portal] 根檔案夾再次發佈為止。

* 當使用者第一次選擇以最適化表單來設定欄位時，儲存設定的選項不會顯示在「屬性瀏覽器」中。 在相同編輯器中選取以設定最適化表單的其他欄位，可解決此問題。

* 如果 [!UICONTROL Connected assets configuration] wizard在安裝後傳回404錯誤訊息，請使用Package Manager手動重新 `cq-remotedam-client-ui-content` 安裝 `cq-remotedam-client-ui-components` 和套件。

* 在安裝AEM 6.5.x.x時，可能會顯示下列錯誤和警告訊息：
   * 「當使用Target Standard API（IMS驗證）在AEM中設定Target整合時，將「體驗片段」匯出至Target會導致建立錯誤的選件類型。 Target會以「HTML」/來源「Adobe Target Classic」類型建立數個選件，而非「Experience Fragment」/來源類型「Adobe Target Classic」。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`:在granite/operations/maintenance中找不到維護視窗。
   * 當使用SUM、MAX和MIN等集合函式時，Adaptive Form伺服器端驗證將失敗。 CQ-4274424
   * `com.adobe.granite.maintenance.impl.TaskScheduler` -在granite/operations/maintenance中找不到維護視窗。
   * 透過可購買橫幅檢視器預覽資產時，不會顯示動態媒體互動影像中的熱點。

## 隨附的OSGi組合和內容套件 {#osgi-bundles-and-content-packages-included}

下列文字檔案列出AEM 6.5.7.0中包含的OSGi組合和內容套件：

* [AEM 6.5.7.0隨附的OSGi搭售清單](assets/6570_bundles.txt)

* [AEM 6.5.7.0內容套件清單](assets/6570_packages.txt)

## 受限制的網站 {#restricted-sites}

這些網站僅提供給客戶使用。 如果您是客戶，需要存取權，請連絡您的Adobe客戶經理。

* [產品下載，請造訪licensing.adobe.com](https://licensing.adobe.com/)
* 瞭解 [如何聯絡客戶支援](https://experienceleague.adobe.com/docs/customer-one/using/home.html)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5發行說明](/help/release-notes/release-notes.md)
>* [[!DNL Experience Manager] 產品頁面](https://www.adobe.com/tw/marketing/experience-manager.html)
>* [[!DNL Experience Manager] 6.5檔案](https://experienceleague.adobe.com/docs/experience-manager-65.html)
>* 訂閱 [Adobe優先產品更新](https://www.adobe.com/subscription/priority-product-update.html)

