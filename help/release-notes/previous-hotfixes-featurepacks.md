---
title: '[!DNL Adobe Experience Manager] 6.5舊版Service Pack發行說明'
description: ' [!DNL Adobe Experience Manager] 6.5 Service Pack的發行說明。'
contentOwner: AK
translation-type: tm+mt
source-git-commit: 131e564e4ed50c4f08412ba39c62f15b9c362b8c
workflow-type: tm+mt
source-wordcount: '17898'
ht-degree: 5%

---


# 舊版Service Pack{#hotfixes-and-feature-packs-included-in-previous-service-packs}包含的修補程式和功能套件

## [!DNL Adobe Experience Manager] 6.5.7.0  {#experience-manager-6570}

[!DNL Adobe Experience Manager] 6.5.7.0是重要的更新，其中包括自2019年4月6.5版推出以來，新功能、主要客戶要求的增強功能，以及效能、穩定性和安全性增強功能。[!DNL Adobe Experience Manager] 6.5上安裝了Service Pack。

[!DNL Adobe Experience Manager] 6.5.7.0中引入的主要功能和增強功能包括：

* 執行頁面移動和MSM展開作為非同步操作，以降低它們對執行時期效能的影響。

* 使用者可以在「卡片」和「欄」檢視中排序數位資產。

* [!DNL Assets] 並提供 [!DNL Dynamic Media] 多種協助工具增強功能。這些增強功能與鍵盤導覽、螢幕閱讀程式的使用，以及讓使用者使用類似的輔助技術(AT)有關。 請參閱[[!DNL Assets] 增強功能](#assets-6570)和[[!DNL Dynamic Media] 增強功能](#dynamic-media-6570)。

* [建立資料模型HTTP用戶端](../../help/forms/using/configure-data-sources.md#fdm-http-client-configuration) 組態以最佳化效能。

* [在「配置」模式下，每個組](../../help/forms/using/resize-using-layout-mode.md#resize-components) 件的「重置選項」可用性

* [!DNL Experience Manager] 6.5 Service Pack 7Forms改進了以下效能：

   * 在提交自適應表單時驗證伺服器上的欄位值。

   * 使用[!DNL Automated Forms Conversion service]將PDF表單轉換為最適化表單。

* [!DNL Experience Manager Forms]支援[!DNL Microsoft SQL Server] 2019。

* 內建存放庫 (Apache Jackrabbit Oak) 更新至 1.22.5 版。

如需[!DNL Experience Manager] 6.5.7.0中推出的完整功能與增強功能清單，請參閱[6.5 Service Pack 7](new-features-latest-service-pack.md)中的新增功能。 [!DNL Adobe Experience Manager] 

以下是[!DNL Experience Manager] 6.5.7.0版中提供的修正清單。

### [!DNL Sites] {#sites-6570}

* 當您開啟頁面的[!UICONTROL Timewrap]選項時，請保持「時間軸」側邊欄選項的開啟，並導覽至[!UICONTROL Sites]主控台時，會發生`Failed to Load`錯誤(NPR-34951)。

* [!UICONTROL Timewrap]選項不顯示所選日期和時間範圍的影像(NPR-34951)。

* 當篩選器從包含內容片段的頁面呼叫`getHeader()`時，會出現`java.lang.AbstractMethodError`錯誤(NPR-34942)。

* 當頁面的路徑包含多個內容子字串時，預覽無法轉譯，而版本比較功能也會失敗(NPR-34740)。

* 為元件的`String`類型標籤屬性設定數值時，可以刪除該元件並撤消刪除操作。 但是，撤消刪除後，標籤屬性從`String`更改為`Long`(NPR-34739)。

* 根據具有鎖定版面的範本新增體驗片段至頁面時發生下列例外(NPR-34632):

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.mozilla.javascript.EcmaError: TypeError: Cannot call method "getChildren" of null
   ```

* 移動資料夾時，會導致遍歷問題，並出現以下錯誤(NPR-34554):

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript. org.apache.jackrabbit.oak.query.RuntimeNodeTraversalException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped
   ```

* 當建立、發佈新資產並移至新位置時，會建立`Request to complete move operation`工作流程，並導致「已中止」狀態。 上傳新資產並執行`move`作業會導致建立處於待定狀態的`Request to complete move operation`工作流程(NPR-34543)。

* 當您將體驗片段從[!DNL Experience Manager] 6.5.2環境匯出至[!DNL Target]標準版時，API呼叫會失敗，因為工作區屬性不適用於[!DNL Target]標準版(NPR-34557)。

* 使用者無法透過[!UICONTROL manage publication]選項發佈頁面，因為[!UICONTROL Publish]選項消失(NPR-34542)。

* 當您在文字中新增一些樣式時，會在文字中新增`<div>`標籤，而且樣式無法再套用至文字(NPR-34531)。

* 當您在彈出式選單中選取項目並更新所需檔案時，它不允許儲存對話方塊值，因為其他選單有空的必填欄位(NPR-34529)。

* 當您從自訂範本建立頁面並在Blueprint階層中移動時，先前從頁面刪除的元件會開始顯示在即時副本階層中的頁面上(NPR-34527)。

* 文章樣式套用至內容後，就無法移除(NPR-34486)。

* 體驗片段的所有即時副本和副本都指向相同的[!DNL Adobe Target]選件ID(NPR-34469)。

* 項目符號清單項除了編號清單外還顯示(NPR-34455)。

* 比較來源選項無法顯示來源頁面與編輯過的頁面版本之間的差異(NPR-34285)。

* 刪除頁面時，版本控制詳細資訊不可配置(NPR-34159)。

* 當使用者選取「開啟選取範圍」對話方塊選項時，鍵盤焦點會移至頁面上顯示的隱藏控制項(CQ-4307779、CQ-4293601)。

* 當您在「作者」上移動已發佈的檔案夾時，「發佈」例項上的檔案夾路徑不會相應更新(CQ-4305144)。

* 當使用者在[!UICONTROL 選擇全部]選項上選擇`Enter`鍵時，鍵盤焦點不會移至[!UICONTROL 建立控制]選項(CQ-4293599)。

* 當您選取`Esc`鍵時，焦點不會還原至父項控制項(CQ-4293593、CQ-4293590)。

* 已改善[!DNL Sites] UI和核心元件的WCAG相容性(CQ-4293448)。

* [!UICONTROL 頁] 面的Zoomand   Scalefunctions已停 [!DNL Sites Editor] 用(CQ-4282353)。

* 使用「向右旋轉」選項後，螢幕閱讀程式會停止旁白目前旋轉或反向狀態(CQ-4282128)。

* 「完成」和「取消設定」對話方塊按鈕有多個制表位(CQ-4274601)。

* 不允許在相同層級移動具有類似名稱的頁面(NPR-35041)。

* 選取「清除(x)」選項後，鍵盤焦點不會移至[!UICONTROL Filter]欄位(CQ-4293581)。

* 當您升級至[!DNL Experience Manager] 6.5.6.0時，繼承段落系統的行為會改變，而且無法正常運作(NPR-35117)。

* 在[!DNL AEM Sites]頁面上選擇[!UICONTROL Action]區段後，鍵盤使用者無法以適當順序移動標籤焦點(CQ-4307786)。

* 在編輯內容片段時，在RTE工具列的連結目標選單清單中選取選項後，內容片段作者對話會開始閃爍(CQ-4305532)。

* 鍵盤使用者無法使用向下鍵(CQ-4295097)在[!UICONTROL 新增元件]下拉式清單中選取選項。

* 從[!DNL Sites]頁面的[!UICONTROL Assets]標籤中的「日曆」選單選擇日期時，標籤焦點不會以適當順序移動(CQ-4293600)。

* 刪除編輯網站頁面時可用的連結或文字選項後，標籤焦點不會移至鍵盤使用者的下一個或上一個選項(CQ-4293597)。

* 在檢視可用選項並按`Esc`鍵後，鍵盤使用者無法將標籤焦點移回[!UICONTROL Actions]區段中的「更多」選項(CQ-4293592)。

* 當您在[!UICONTROL 編輯]模式中為影像啟動[!UICONTROL 旋轉]選項時，標籤焦點會移至鍵盤使用者的[!UICONTROL 重做]選項(CQ-4293587)，而非停留在旋轉。

* 在[!UICONTROL 連結與動作]標籤上的[!UICONTROL 開啟選擇]對話方塊中，標籤焦點會移至[!UICONTROL 取消]選項(CQ-4293579)後頁面中的隱藏元素。

* 當鍵盤使用者編輯影像時，導覽至[!UICONTROL 完成]選項，然後按Enter鍵，螢幕閱讀程式不會宣佈完成(CQ-4282351)。

* 螢幕閱讀程式和鍵盤使用者無法使用[!UICONTROL 連結和動作]對話方塊上的「上移和下移」選項(CQ-4281120)。

* 在導覽至[!UICONTROL 屬性]頁面上的關閉(X)選項(CQ-4293581、NPR-34653)後，鍵盤使用者無法還原標籤焦點。

### [!DNL Assets] {#assets-6570}

[!DNL Adobe Experience Manager] 6.5.7.0修正 [!DNL Assets] 下列問題，並提供下列增強功能。

* 本版次針對[!DNL Experience Manager Assets]的協助功能進行下列增強功能。 如需詳細資訊，請參閱 [!DNL Assets]](/help/assets/accessibility.md)中的[協助功能。

   * 使用鍵盤導覽時間軸時，`Esc`鍵可收合[!UICONTROL 顯示全部]選項，而不會失去焦點(CQ-4293598)。
   * 使用鍵盤標籤鍵導覽時，從新增的標籤移除最後一個標籤後，標籤欄位會保留焦點(NPR-35109)。
   * [!DNL Experience Manager] 元件現在包含螢幕閱讀程式使用之名稱、角色和值的適當資訊(NPR-34255)。
   * 刪除「文字／大小」組合框、「連結」組合框、「語言」組合框或「文本」編輯框後，鍵盤焦點將返回下一個或上一個用戶介面元素或更相關的用戶介面元素(CQ-4293585)。
   * 當將指標暫留在選項上時，會顯示「選取」和「下載」等提示。 使用螢幕放大鏡的使用者可能看不到檔案縮圖，因為這些提示。 現在，在使用`Escape`鍵移除選項後，可以保留焦點。 (CQ-4293554).
   * 從頁面中顯示的格線選取格線儲存格後，焦點會移至螢幕上顯示的動作列(CQ-4282127)。
   * 視覺使用者可區分一般文字和連結，因為在[!DNL Experience Manager]首頁中顯示所有解決方案連結的視覺線索（底線和雪佛龍圖示）(CQ-4282072)。

* 以下是在[!DNL Assets]中進行的使用者體驗增強：

   * 啟用卡片檢視和欄檢視中資產排序(NPR-35097)。

* 升級至6.5後，如果使用Assets HTTP API產生JSON檔案，則檔案中使用的編碼會發生問題(NPR-35129)。

* 未提供建立系列權限的群組的使用者（「建立系列」選項無法使用）仍可以直接存取URL `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/collections/createcollectionwizard.html/content/dam/collections?contentPath=/content/dam/collections`來建立系列(NPR-35115)。

* 依名稱排序時，搜尋的資產會以區分大小寫的方式排序。 這會根據在搜尋結果中以順序顯示的外框，建立兩個不同的排序清單(NPR-35068)。

* 在編輯器中開啟內容片段時，警告消息(`Invalid value specified for a metadata property`)將記錄在錯誤日誌中(NPR-35012)。

* 不具管理員權限的使用者可使用[Experience Manager]案頭應用程式編輯過期的資產。 (NPR-34993).

* 當在「資產」使用者介面上拖曳相同的「資產」並建立新版本時，中繼資料中的變更不會持續存在(NPR-34940)。

* 編輯系列時，使用者可以刪除系列的標題並成功儲存變更(NPR-34889)。

* 上傳重複影像時，會顯示刪除選項。 選取刪除可讓影像上傳。 也會觸發DAM更新資產工作流程(NPR-34744)。

* 將[!DNL Adobe Asset Link]與[!DNL Adobe InDesign]搭配使用時，搜尋結果不包含資料夾和系列，但僅包含資產(NPR-34699、CQ-4303666)。

* 將滑鼠指標暫留在卡片檢視上，讓螢幕捲動的結果是（自動）將焦點放在卡片中可用的快速動作(NPR-34514)。

* 批量編輯多個資產的屬性時，選擇「保存」選項會關閉批量編輯器視圖並重定向到主[!DNL Assets]頁。 此行為與[!UICONTROL Save &amp; Close]選項的行為相同，不預期(NPR-34546)。

* 智慧型系列在儲存後未顯示正確的使用者介面設定。 查詢已正確保存，但介面始終顯示上次添加的Option謂語(NPR-34539)。

* 將資產新增至[!DNL Experience Manager]時，無名稱空間的中繼資料不會匯入(NPR-34530)。

* 拖曳資料夾上的資產以移動資產時，使用者介面也會顯示[!UICONTROL 「放入燈箱」]和[!UICONTROL 「放入系列」]的選項。 即使取消移動操作，用戶介面仍繼續顯示後兩個選項(NPR-34526)。

* 符號`%>`會顯示在系列頁面上(NPR-34499)。

* 在欄檢視中，當向上和向下捲動時，[!DNL Assets]會顯示重複的資料夾和資產名稱，然後才會顯示所有資產(NPR-34464)。

* 如果在建立公用資料夾後立即建立專用資料夾，則公用資料夾使用專用資料夾設定(NPR-34415)。

* 在卡片檢視中，卡片未以字母順序列出，而且卡片無法以字母順序排序(NPR-34234)。

* 重新開啟階層式規則時，使用者介面上不會保留這些選項(CQ-4301452)。

#### [!DNL Dynamic Media] {#dynamic-media-6570}

* 在[!DNL Dynamic Media](CQ-4290306)中，已針對協助工具執行下列增強功能。 如需詳細資訊，請參閱 [!DNL Dynamic Media]](/help/assets/accessibility-dm.md)中的[協助功能。

   * 螢幕閱讀程式（JAWS，旁白）會在「內嵌大小」功能表選項(CQ-4290927)中，說明功能表項目的名稱、角色和狀態。
   * 使用者可使用`Tab`鍵來導覽「電子郵件連結」對話方塊(CQ-4290926)。
   * 建立視訊編碼設定檔的工作流程更容易使用，因為螢幕閱讀器增強功能(CQ-4290623、CQ-4290622)。
   * 使用`Tab`鍵導覽時，焦點會移至工作流程中適當的使用者介面元素，以建立互動式視訊(CQ-4290621、CQ-4290620、CQ-4290619)。
   * 「發佈」頁、「編輯資產」頁、「編輯智慧裁切」頁和「影像集編輯器」頁已經過改良，以符合Web標準。 協助技術(AT)使用者現在可輕鬆導覽這些頁面，並採取裁切影像等動作(CQ-4290617、CQ-4290616、CQ-4290613、CQ-4290612、CQ-4290610、CQ-4290614)。
   * 檢視器已改良，可讓使用者使用鍵盤進行導覽(CQ-4290615)。
   * 鍵盤和螢幕閱讀程式使用者可使用裁切功能(CQ-4290609)。
   * 鍵盤用戶可以更好地管理熱點(CQ-4290604、CQ-4290603)。

* 如果公司名稱和資料夾名稱相同，則遠端影像集在[!DNL Experience Manager]中無法編輯(NPR-31340)。

* 在將熱點添加到[!DNL Dynamic Media]影像或在編輯[!DNL Dynamic Media]視頻或具有影像的[!DNL Experience Fragment]之後嘗試預覽輸出時，z索引順序不正確(CQ-4307267)。

* [!DNL Dynamic Media] 重新處理混合媒體集時同步失敗(CQ-4307184)。

* 如果資產移至已設定自動同步至[!DNL Dynamic Media]的資料夾，則資產不會同步(CQ-4307122)。

* [!DNL Dynamic Media] 使用原生HTML5視訊控制項(CQ-4306977、CQ-4306727)的iOS裝置上無法播放視訊。

* 無法下載應用SmartCrop的映像(CQ-4304558)。

* 無法選擇性地發佈資料夾至Dynamic Media(CQ-4304526)。

* 從[!DNL Experience Manager]取消發佈視訊檔案時，不會從已設定的Scene7部署中取消發佈最適化視訊集(CQ-4304405)。

* 在全景媒體元件中新增全景影像資產並重新整理頁面會導致`Uncaught ReferenceError: $ is not defined`錯誤(CQ-4302810)。

* 在[!UICONTROL 檢視器預設集編輯器]中，編輯[!UICONTROL PanoramicImage/PanoramicImage_VR]預設集時，在`PanoramicView`元件中，`PANORAMICVIEW_AUTOROTATE`修飾元標籤不可用(CQ-4302443)。

* 如果視訊不是MixedMediaSet中的第一個視訊標題，則不會顯示視訊標題(CQ-4298161)。

* iPhone行動裝置上的HTML5 eCatalog檢視器無法翻頁或翻頁(CQ-4296611)。

* 在行動裝置上捲動色票時，色票會捲動至可見區域的右側和外側數秒，然後再捲動回檢視(CQ-4296439)。

* 當建立檢視器預設集主要記錄時，不會發佈CSS和圖稿，只會發佈檢視器預設集(CQ-4262205)。

* 嘗試在[!UICONTROL 互動式視訊／影像]元件中連結特定熱點的體驗片段時，不會顯示選取的體驗片段路徑。 而是從路徑欄位傳回空值(NPR-35146、CQ-4298136)。

* 無法在IVV編輯器中預覽體驗片段(CQ-4308560)。

* 將熱點新增至影像並選取「體驗片段」時，無法選取子檔案夾和「體驗片段」的變體(CQ-4307455)。

* 上傳後，非影像資產不會顯示為已發佈(CQ-4306415)。

#### [!DNL Experience Manager] 3D資產  {#three-d-assets-6570}

* `DAM CQ MIME Type` 服務會將不正確的MIME類型套用至3D資產，導致不正確的轉譯(NPR-34731)。

### [!DNL Commerce] {#commerce-6570}

* 「商務」產品收集使用者介面不會列出一個系列中超過15種產品(NPR-34502)。

### 平台 {#platform-6570}

* HTTP會話通過HTTPS不會失效(NPR-35083)。
* 從用戶介面啟動每日或每週維護任務時返回`NullPointerException`(NPR-34953)。
* W3C驗證器會報告相容用戶端程式庫JavaScript檔案的警告(NPR-34898)。
* `AudienceOmniSearchHandler`函式使用不建議使用的索引(NPR-34870)。
* 從Experience Manager登出無法清除Cookie(NPR-34743)。
* 如果標籤名稱包含特殊字元，`TagManager` API的`findByTitle`函式將無法運作(NPR-34357)。
* 導入用戶同步包的過程失敗(NPR-34399)。
* 新增對`ariaLabel`和`ariaLabelledby`屬性的支援至`Coral.Masonry`元件(GRANITE-29962)。
* 安裝最新核心元件封裝後，不會重新整理含有內容片段的頁面的Dispatcher快取(CQ-4306788)。
* 使用者介面上無法正確顯示帶引號(`"`)的本地化標籤名稱(CQ-4305439)。

### 使用者介面 {#ui-6570}

* 元件屬性中的[!UICONTROL 連結至]欄位會顯示不符合指定字串的自動完成建議(NPR-34865)。

* 當AEM計畫在2天之間分發的每日維護窗口時，顯示以下錯誤消息(NPR-35280):

   ```TXT
   ERROR The start time must precede (be less than) the end time
   ```

### Integrations {#integrations-6570}

* 編輯現有[!DNL Adobe Launch]配置失敗(NPR-35045)。
* 如果使用IMS配置和[!DNL Adobe Target Standard]環境，則無法將[!DNL Experience Fragments]導出到[!DNL Adobe Target](NPR-34555)。
* 當從資料夾導覽至[!UICONTROL 觀眾]頁面時，[!UICONTROL 建立]選項會出現在[!UICONTROL 觀眾]頁面(NPR-35151)。

### Sling {#sling-6570}

* 預設登錄運行狀況檢查會驗證不存在的用戶的憑據(NPR-34686)。

### 翻譯項目{#translation-6570}

* 在[!DNL Experience Manager]中取消翻譯項目時，取消該項目的請求不會發送到翻譯提供商(NPR-34433)。

### [!DNL Communities] {#communities-6570}

* 產品中所有不公平術語的例子都被接受的等價物(NPR-34311)取代。
* [!DNL Google+] 已從社交共用選項清單中移除(NPR-33877)。

### [!DNL Brand Portal] {#brandportal-6570}

* 在選擇[!UICONTROL 清單檢視]中的資產時，使用者介面不會回應(NPR-34728)。

### [!DNL Forms] {#forms-6570}

>[!NOTE]
>
>[!DNL Experience Manager Forms] 會在排程的[!DNL Experience Manager] Service Pack 發行日期一週後發行附加元件的套件。

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack不包含修正 [!DNL Forms]。它們是使用單獨的[!DNL Forms]附加軟體包傳遞的。 此外，還發行了包含JEE上[!DNL Experience Manager Forms]修正的累積安裝程式。 如需詳細資訊，請參閱「安裝AEM Forms附加元件](#install-aem-forms-add-on-package)」和「在JEE上安裝AEM Forms」。[[](#install-aem-forms-jee-installer)

**調適型表單**

* 在套用[!DNL Experience Manager] Service Pack 6(NPR-35126)後，無法使用Classic UI編輯最適化表單。

* 將PDF轉換為最適化表單時，無法使用標籤式版面上的表單資料模型來設定巢狀面板的值。 此外，使用程式碼編輯器動態設定靜態陣列的「選項按鈕群組」值時，也會發生問題(NPR-35062)。

* 在文本欄位元件中以自適應格式輸入日文字元時，可以指定的字元數超過35個字元的上限(NPR-35039)。

* 最適化表單會在提交表單後顯示的&#x200B;**[!UICONTROL 感謝]**&#x200B;頁面上顯示不想要的參數，例如`owner`和`status`(NPR-34989)。

* [!UICONTROL [!UICONTROL Attachment]元件的檔案選擇]對話框顯示不支援的檔案類型以及在自適應表單提交過程中導致錯誤的選擇(NPR-34970)。

* 當您在[!DNL Experience Manager Sites]頁面中插入一個在表單之前包含文字的最適化表單時，游標焦點會直接移至表單而非表單之前的文字(NPR-34947)。

* [!UICONTROL 使用] Data選項預覽使用 [!DNL Experience Manager] 6.2資料XML檔案來預填最適化表單無法正常運作(NPR-35087)。

* 當您更新最適化表單的資料字典時，不會轉譯表單，因為最適化表單會傳回快取值(NPR-34845)。

* 由於快取失效，片段以最適化形式載入所花的時間較長(NPR-34567)。

* 標籤導覽無法適合最適化表單的螢幕閱讀程式(NPR-34544)。

**通信管理**

* 無法將包含浮點類型之數值資料的XML標籤值儲存為草稿(NPR-35050)。

* 從ES3移轉資產時，資產包含兩個不可編輯的預設條件(NPR-34972)。

* 當您在字母中編輯資料字典時，[!UICONTROL Lent Content]區段會顯示旋轉矩形，而非有用資訊(NPR-34853)。

**互動式通訊**

* 在安裝[!DNL Forms]附加元件套件後，Interactive Communication的轉出組態名稱會複製標準的轉出組態名稱(NPR-34976)。

**文件安全性**

* 當您儲存新的檔案安全性政策時，FormsExperience Manager會顯示`Relative validity period is required`錯誤訊息(NPR-34679)。

* Document Security無法保護PDF 2.0檔案(CQ-4305851)。

如需安全性更新的詳細資訊，請參閱[Experience Manager安全性公告頁面](https://helpx.adobe.com/security/products/experience-manager.html)。

## [!DNL Adobe Experience Manager] 6.5.6.0  {#experience-manager-6560}

Adobe Experience Manager6.5.6.0是重要的更新，其中包括自2019年4月&#x200B;**推出6.5版以來發佈的新功能、主要客戶要求的增強功能以及效能、穩定性和安全性增強功能。**&#x200B;它可安裝在Adobe Experience Manager6.5之上。

Adobe Experience Manager6.5.6.0中引入的主要功能和增強功能包括：

* 使用「快速發佈」(Quick Publish)[!UICONTROL 或「管理出版物」(Manage Publication)]精靈，選擇性地將資產發佈或取消發佈至[!DNL Experience Manager]或[!DNL Dynamic Media]。][!UICONTROL 

* 使用[!DNL Dynamic Media]使用者介面，使內容傳送網路(CDN)快取內容無效。

* 現在也支援透過Proxy伺服器，將資產貢獻資料夾從品牌入口網站發佈至Experience Manager資產。

* 現在，在刪除[!DNL Experience Manager Assets]中的專用資料夾時，將清除自動生成的專用資料夾組。

* 視訊[!UICONTROL Viewer]預設編輯器中修飾元的說明已在[!DNL Dynamic Media]中更新。

* 提供新的公司設定以反映[!DNL Dynamic Media]連接器的狀態。

* `test`和`aiprocess`的預設選項會從Dynamic Media的`Rasterize`先前更新為`Thumbnail`，以確保使用者只需建立縮圖，並略過頁面擷取和關鍵字擷取。

* [在用戶端預先填寫最適化表格](../../help/forms/using/prepopulate-adaptive-form-fields.md#prefill-at-client)。

* [在具有雙向SSL實作的伺服器上，與REST風格的API整合，以建立資料模型](../../help/forms/using/configure-data-sources.md)。

* [增強轉譯的可調式表單頁面快取](../../help/forms/using/configure-adaptive-forms-cache.md)。

* 支援Automated forms conversion服務[中的「Adobe Sign文字標籤」。](https://docs.adobe.com/content/help/en/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html)

* 支援使用[!DNL Automated Forms Conversion service]將彩色表單轉換為最適化表單](https://docs.adobe.com/content/help/en/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html)。[

* 支援SMB 2和SMB 3協定。

* 內建存放庫 (Apache Jackrabbit Oak) 更新至 1.22.4 版。

如需Experience Manager6.5.6.0中推出的完整功能和增強功能清單，請參閱[Adobe Experience Manager6.5 Service Pack 6](new-features-latest-service-pack.md)的新增功能。

以下是[!DNL Experience Manager] 6.5.6.0版中提供的修正清單。

### [!DNL Sites] {#sites-6560}

* 在[!DNL Sites]或[!DNL Screens]中，選擇項目並按一下[!UICONTROL 管理出版物]。 由於用戶介面錯誤，用戶無法在[!UICONTROL 管理出版物]嚮導中前進。 具體來說，[!UICONTROL Publish]選項無法運作(NPR-34099)。
* 取消選擇[!UICONTROL 取消繼承]或[!UICONTROL 禁用繼承]選項後，iParsys（繼承段落系統）的位置不會恢復為其原始預設位置(NPR-34097)。
* 如果`RolloutConfigManagerFactoryImpl`無法載入轉出設定，則不會嘗試載入遺失的設定。 它會傳回快取的組態(NPR-34092)。
* 在Text核心元件中，使用來源HTML編輯選項後，`em`標籤中的類別會被移除(NPR-34081)。
* 從Experience Manager6.3.3升級至Experience Manager6.5.3後，推出程式會耗時更久，而且轉出會因逾時錯誤而失敗(NPR-34049)。
* `htmlwriter`不會將屬性值編碼回去。 XF標籤中存在的標籤以解碼屬性值導出（即`"`而不是`&#34`）。 它會在使用XF匯出的Visual Experience Composer的Target端造成問題(NPR-34048)。
* 當在[!DNL Experience Manager Sites]中移動頁面時，請加強記錄功能，以擷取版本建立失敗的原因(NPR-34014)。
* 在[!DNL Rich Text Editor]中，如果所有文本都被刪除，則段落標籤也會被刪除(NPR-33976)。
* 當`siteadmin`頁面（在Classic UI）開啟或重新整理時，`New`功能表中的選項會停用(NPR-33949)。

   ![螢幕擷取，以說明Classic UI中遺失功能表的問題](assets/33949_missing_menu.png)

* [!DNL Content Fragment]不能用作`TemplatedResource`，因為它在`ContentFragmentUsePojo`中失敗(NPR-33911)。
* 同步和非同步移動操作可能會導致併發傳輸導致錯誤。 頁面移動操作僅限非同步移動。 它可防止頁面同時移動(NPR-33875)。
* [!UICONTROL 管理] 發佈作業，將內容從作者複製至發佈例項失敗並產生JavaScript錯誤(NPR-33872)。
* 當選取多個頁面或資產以建立版本時，新版本僅會針對最後選取的頁面或資產建立(NPR-33866)。
* 將含即時副本的Blueprint頁面移至另一個檔案夾。 將資料夾移動到原始資料夾時，移動操作將失敗而無任何錯誤(NPR-33864)。
* 當在[!DNL Sites]控制台中使用移動操作來更名網頁時，該操作會在嚮導的最後一個步驟中顯示兩個重疊對話框(NPR-33831)。

   ![螢幕擷取以說明NPR-33831重疊移動對話的問題](assets/33831_rename_dialog.png)

* 複製和貼上操作期間，複製中`cq:acLinks`和`cq:acUUID`的[!DNL Adobe Campaign]屬性將被刪除(NPR-33794)。
* 當嘗試在已分離父即時副本的子頁面上轉出時，[!DNL Experience Manager]會產生空指針異常(NPR-33676)。
* 當版面容器再次複製並貼上至頁面時，版面容器中的[!DNL RTE]元件不可見。 [!DNL RTE]元件不可編輯，但會在頁面重新整理時顯示(NPR-33662)。
* 針對不同的中斷點（中型和大型）調整版面元件大小時，版面的運作不如預期(NPR-33608)。
* 在[!DNL RTE]的內嵌編輯模式中，拖曳影像對文字元件無法運作(NPR-33602)。
* 您可以在藍圖頁面中建立與頁面名稱同名的元件。 在轉出期間，`_msm_moved`會加上後尾以重新命名元件。 將元件移至[!UICONTROL 段落系統]的末尾(NPR-33535)。
* 當在許多頁或資產上設定offTime或onTime時，會耗費大量資源，並會在啟動和關閉期間減慢系統速度(NPR-33482)。
* 對`/content/experience-fragment`具有CRUD權限的用戶無法刪除資料夾(NPR-33436)。
* 您可以在[!DNL Experience Fragments]區段的父資料夾中，選取[!UICONTROL HTML &amp; JSON]作為[!UICONTROL Adobe Target匯出格式]的選項。 此父資料夾的子資料夾在啟用觸控的UI中會顯示相同的屬性。 但是，在CRXDE中，對於`cq:adobeTargetExportFormat`，它只顯示HTML而不顯示`html,json`(NPR-33423)。
* 不支援從頁面別名發佈或取消發佈。 刪除看似否的選項(NPR-33415)。
* 在[!DNL Experience Manager]中，可將特定標籤從一個位置移動到另一個位置。 移動前後也可套用至不同的頁面。 編輯頁面屬性時，即使標籤相同，標籤也不會顯示以供編輯(NPR-33353)。
* 從包含多個版面容器的範本刪除版面容器時，頁面範本無法正確呈現(NPR-33347)。
* 在範本編輯器中，嘗試刪除`/content/`下超過10000個頁面所使用的範本。 未顯示任何錯誤資訊時顯示錯誤(NPR-33312)。
* 使用錨點重新導向至[!DNL Experience Manager]頁面在「作者」例項上無法運作，因為`PageRedirectServlets`會在URL片段或錨點後放置查詢字串(NPR-34288)。
* 在`/content/campaign`下建立品牌會產生不允許建立促銷活動的結構。 [!UICONTROL Create ] Brandoption會讓新建立的品牌無法建立選件 [!UICONTROL 和] 活動，因為沒有  Createoption(NPR-34113)。
* 您可以暫停頁面的[!DNL Live Copy]，繼承會中斷，如編輯器模式所示。 在頁面屬性中，表示繼承的表徵圖錯誤地指示繼承存在且未中斷(NPR-34017)。
* 具有多個參考的頁面無法非同步移動，有時移動操作會失敗(CQ-4297969)。
* 在編寫時，URL中具有`/`字元的網頁會停止回應。 在製作時新增元件時，CPU使用量會增加，瀏覽器會停止回應(CQ-4295749)。
* 在瀏覽模式中，NVDA不會對從「類型／大小」菜單選項中選擇的值進行旁白。 視覺焦點不在選取的元素上。 依賴螢幕閱讀程式的使用者無法使用瀏覽模式(CQ-4294993)。
* 建立網頁時，使用者可以選取[!UICONTROL 內容頁面]範本。 在[!UICONTROL 社交媒體]標籤中，使用者選擇[!UICONTROL 偏好的XF變數]。 若要在NVDA瀏覽模式中選取體驗片段，使用者無法使用鍵盤按鍵(CQ-4292669)。
* 將車把庫更新為更安全的v4.7.3(NPR-34484)。
* [!DNL Experience Manager Sites]元件中有多個跨網站指令碼執行個體(NPR-33925)。
* 建立新資料夾時的資料夾名稱欄位易受儲存的跨站點指令碼攻擊(GRANITE-30094)。
* [!UICONTROL  Welcome]頁面和路徑完成模板上的搜索結果易受跨站點指令碼攻擊(NPR-33719、NPR-33718)。
* 在非結構化節點上建立二進位屬性會導致在二進位屬性對話框上執行跨站點指令碼(NPR-33717)。
* 在CRX DE介面上使用[!UICONTROL 訪問控制測試]選項時跨站點指令碼(NPR-33716)。
* 當向客戶端發送資訊時，用戶輸入不適當地編碼各種元件(NPR-33695)。
* 「日曆」視圖中的「Experience Manager收件箱」跨站點指令碼(NPR-33545)。
* 以`childrenlist.html`結尾的URL會顯示HTML頁面，而非404回應。 此類URL容易受到跨網站指令碼的攻擊(NPR-33441)。


### [!DNL Assets] {#assets-6560}

**Experience Manager資產中的協助工具增強功能**

* 使用鍵盤按鍵，使用者現在可存取並專注在[!UICONTROL References]資產清單中的互動式使用者介面選項(NPR-34115)。

* 螢幕閱讀程式現在會宣佈搜尋頁面上謂詞的預期動作(NPR-34104)。

* 搜尋頁面和搜尋結果頁面現在提供更多資訊標題，以更好地瞭解螢幕閱讀程式使用者(NPR-34093)。

* 螢幕閱讀程式現在會宣佈在資產[!UICONTROL 屬性]頁面的[!UICONTROL Basic]標籤中刪除選取標籤的選項(NPR-33972)。

* 現在，螢幕閱讀程式會將清單檢視中每一列的元素宣佈為同一列的元素(NPR-33932)。

* 使用`Tab`鍵導覽時的使用者焦點現在會移至版本預覽中的關閉選項(NPR-33863)。

* Omnisearch關閉後，使用者焦點現在會移至搜尋圖示(NPR-33705)。

* 可操作的使用者介面選項現在使用鍵盤按鍵進行導覽時，視覺焦點更突出，對比也更強。 鍵盤使用者可識別重點區域(NPR-33542)。

* 使用鍵盤的拖曳功能現在可在[!UICONTROL 中繼資料結構編輯器]的螢幕閱讀程式瀏覽模式中運作(CQ-4296326)。

* 在連結共用對話方塊中，當在瀏覽模式中導覽時，會顯示螢幕閱讀程式，

   * 不會在載入對話方塊後立即對表格資訊進行旁白。

   * 可導覽至所有列出的自動建議。

   * 針對[!UICONTROL 新增電子郵件地址／搜尋](CQ-4294232)顯示的自動建議旁白。

* 使用`Esc`鍵從卡片檢視中移除快速動作圖示時，鍵盤焦點不會再從最後一個焦點項目移除(CQ-4293554)。

* 針對使用者介面上的互動式選項，螢幕閱讀程式現在會宣佈其用途，而非圖示的文字名稱(CQ-4272943)。

* 鍵盤焦點現在可成功移至[!UICONTROL Flyout]、[!UICONTROL InlineZoom]、[!UICONTROL Shopbable_Banner]、[!UICONTROL Zoom_dark]、[!UICONTROL Zoom_light]、[!UICONTROL ZoomVertical_darka11/>和[!UICONTROL ZoomVertical_light]選項。當在[!DNL Dynamic Media]中使用鍵盤Tab鍵導覽資產詳細資訊[!UICONTROL Viewers]時(CQ-4290605)。]

* [!UICONTROL 現在，您] 可以使用鍵盤  鍵存取資產屬性頁面上的儲存與關閉選項(NPR-34107)。

* 現在，每次發生錯誤時，螢幕閱讀程式會宣佈因使用者名稱和密碼組合不正確而導致的錯誤訊息(NPR-33722)。

* 在[!DNL Experience Manager]標題區段中，當在瀏覽模式中導覽時，螢幕閱讀程式現在會宣佈，

   * 在[!UICONTROL Omnisearch中自動編輯建議，鍵入以搜尋]。

   * [!UICONTROL Solutions]、[!UICONTROL Help]、[!UICONTROL Inbox]和[!UICONTROL User]選項的展開或收合狀態。

   * 當用戶在[!UICONTROL 搜索幫助]欄位的[!UICONTROL 幫助]選項下輸入搜索字串時，將顯示[!UICONTROL 搜索幫助]狀態消息。

   ![頁首中的說明功能表](assets/Help_aem_header.png)

   *圖： [!UICONTROL 搜索幫] 助  菜單。*

   * 如果在[!UICONTROL Impersonate as]欄位中，在[!UICONTROL User]選項下輸入錯誤值，則錯誤訊息會正確移至文字欄位(NPR-33804)。

   ![頁首中的用戶菜單](assets/User_aem_header.png)

   *圖： [!UICONTROL 標題中] 「用戶」  菜單中的Impersonate asfield。*

* 使用者現在可以使用鍵盤來變更焦點：

   * [!UICONTROL 在「連結共用」對話] 方塊中搜尋／新增 [!UICONTROL 電子郵件] 地址欄。

   * [!UICONTROL 在資料夾屬] 性的「權限」(Permissions)表的「 [!UICONTROL Closed User ]     Group」（已關閉的用戶組）下添加用戶或組欄位(NPR-34452)。

**修正Experience Manager資產的問題**

[!DNL Adobe Experience Manager] 6.5.6.0提供 [!DNL Assets] 下列問題的修正：

* 從資產時間軸選取註解時，不會反白顯示(CQ-4302422)。

* 預覽使用[!DNL Adobe InDesign]範本建立的行銷文宣資產（例如手冊、傳單和名片）不會顯示換行和分段(NPR-34268)。

* 文字擷取，因此無法完整搜尋已上傳的PDF檔案(NPR-34164)。 要修復它，請在安裝Service Pack 6後重新啟動[!DNL sAdobe Experience Manager]部署。

* 多頁資產的時間軸會在時間軸檢視中瀏覽資產時顯示套用至所有子資產的註解，而非顯示特定子資產的註解(NPR-34100)。

* 如果資料夾包含JavaScript、CSS或JSON檔案格式的資源，則不會使用[!UICONTROL 管理出版物]選項來發佈資產資料夾(NPR-34090)。

* 取消選取或移除Omnisearch中套用的標籤或篩選器會多次執行搜尋查詢，這會導致搜尋時間增加(NPR-34078)。

* 在卡片檢視中，當工作流程（在資料夾中的資產上）進行中或待定時，頁面會重新載入，直到工作流程完成或終止為止。 因此，作者無法處理資料夾中必須向下捲動的資產(NPR-33986)。

* 如果使用者將已發佈的資產移至新位置，則即使取消選取「重新發佈」選項，也會重新發佈資產。 這會導致發佈例項上有許多孤立的資產。 不過，預設行為是，已發佈資產上的移動操作會自動取消發佈；如果作者在移動資產時選擇[!UICONTROL Republish]選項，則會重新發佈此資產(NPR-33934)。

* 系列中資產的[!UICONTROL 移動資產]頁面不會載入所有HTML內容，例如[!UICONTROL 調整／重新發佈]選項。 因此，用戶無法完成移動操作(NPR-33860)。

* 移動資產並在移動資產的名稱和標題中添加特殊字元會在資產的新位置(NPR-33826)建立一個額外的資料夾（同名）。

* [!UICONTROL 當在] Downloadialog（下載）上選取  Emailoption時，資產的下載按鈕  會停用(NPR-33730)。

* 在對資產執行大量作業（例如批量中繼資料編輯）時，會發現「請求-URI過長」錯誤(NPR-33723)。

* 出現JavaScript錯誤，如果上傳的JSON檔案有空格或特殊字元值(NPR-3371)，則使用者無法透過[!UICONTROL 資料夾中繼資料結構表單編輯器中的「透過JSON路徑]新增」功能，選取或刪除在[!UICONTROL 下拉式清單欄位中產生的選擇。2)。]

* 使用[!DNL desktop app]或[!DNL Adobe Asset Link]中的[!UICONTROL Open]選項更新資產時，資產的靜態轉譯不會更新，並會同步回[!DNL Adobe Experience Manager](CQ-4296279)。

* 在列視圖中，對一組資產的移動操作也會移動在為它們使用[!UICONTROL Filter]選項之前選定的資產。 請注意，使用[!UICONTROL Filter]選項會取消選取先前的選擇(NPR-34018)。

* 資產的搜尋建議會在特殊字元之前加入反斜線，其名稱中有特殊字元(NPR-33834)。

* 在[!UICONTROL 資料夾元資料結構表單]中建立下拉式清單規則時，用戶無法從[!UICONTROL 欄位選擇]列中選擇值(CQ-4297530)。

* 當您在[!DNL Experience Manager] 6.5上安裝[!DNL Experience Manager] 6.5 Service Pack 5或舊版 6.5(NPR-34532)時，會刪除資產自訂工作流程模型（在`/var/workflow/models/dam`中建立）的執行時期副本。 若要擷取執行時期副本，請使用HTTP API將工作流程模型的設計時副本與執行時期副本同步：
   `<designModelPath>/jcr:content.generate.json`。

**在Dynamic Media修正的問題**

* 如果使用者在建立視訊描述檔後在編輯中定義編碼設定，則智慧型裁切設定會從視訊描述檔中移除(CQ-4299177)。

* 當使用者在資產詳細資訊頁面上的側欄選項（例如[!UICONTROL Overview]、[!UICONTROL Timeline]、[!UICONTROL Viewers]）之間切換時，頁面載入時資產會閃爍(NPR-34235)。

* 重新處理作業時會發現下列問題：

   * 重新處理工作傳回的工作處理代碼中遺失工作ID。

   * 僅重新處理視訊記錄檔的檔案名稱，而非完整路徑。

   * 重新處理作業沒有將資產類型設定為靜態的選項。

   * `ExcludeFromAVS` 選項(CQ-4298401)。

* 當將影像描述檔新增至具有多個（例如11）外觀比例的資料夾時，智慧型裁切功能會失敗並出現錯誤(NPR-34082)。

* 當使用者在以Dynamic MediaScene7(CQ-4299727)設定之[!UICONTROL Tools]的[!DNL Adobe Experience Manager][!UICONTROL Workflow Archive]頁面上向下捲動[!UICONTROL Workflow]標籤時，觸發DAM更新資產工作流程。

* [!UICONTROL 檢視器預設集編輯器]的「行為」標籤中的符號未本地化(CQ-4299026)。

* 如果檢視器處於回應模式，則主檢視會以不正確的版面顯示影像，而檢視器則無法配合。(CQ-4298293)

* 對[!UICONTROL Adobe Experience Manager]中影像預設集的變更不會同步至Scene7出版系統(CQ-4299713)。

### [!DNL Commerce] {#commerce-6560}

* 當資產移動時，不會重新分解產品中資產的連結(NPR-34098)。

### 平台 {#platform-6560}

* 無法使用升級的Experience Manager實例上的診斷工具下載日誌(NPR-34336)。
* 升級失敗，但因為依賴特定版本的`cq-wcm-api`基礎套件(CQ-4300520)而出現錯誤。
* 未指定預設代理（發佈）配置的&#x200B;**[!UICONTROL 連接超時]**&#x200B;和&#x200B;**[!UICONTROL 套接字超時]**&#x200B;設定的預設值(NPR-33707)。
* `/etc/map.publish`下映射組態的更新不會反映在網站頁面上(NPR-34015)。
* [API參考](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html) 檔案不包含套件的 `com.day.cq.tagging` 檔案(CQ-4295864)。

### 使用者介面{#ui-6560}

* 卸載瀏覽器介面不顯示所有作業主題(NPR-34308)。
* [配置瀏覽器](/help/sites-administering/configurations.md)介面不顯示所有配置(NPR-33644)。
* 在搜索要模擬的用戶時按`Esc`鍵時，**[!UICONTROL User]**&#x200B;對話框將關閉，而不是用戶清單(NPR-34084)。

### 整合{#integrations-6560}

* 長名稱的活動不與[!DNL Adobe Target]同步(NPR-34254)。

* 在建立新Adobe啟動配置時選擇屬性會導致以下錯誤消息(NPR-33947):

   ```javascript
   GET http://hostname:Port/libs/cq/dtm-reactor/content/configurations/createcloudconfigwizard/jcr:content/body/items/form/items/wizard/items/general/items/fixedcolumns/items/container/items/general/items/property/data.html?query=&start=0&end=25&imsConfigurationId=Adobe%20Launch&companyId=&_charset_=utf-8 400 (Bad Request)
   ```

### 翻譯專案 {#translation-6560}

* 如果用戶的`authorizableID`包含特殊字元(NPR-33828)，則不建立翻譯項目。

### Sling {#sling-6560}

* Health Check and Pattern Detector具有重疊功能。 因此，Heath檢查從產品中刪除(NPR-33928)。

### WCM {#wcm-6560}

* 基礎元件——將基礎映像元件添加到頁面並引用映像時，`Undo`操作無法運行(NPR-34516)。

* 無法使用「頁面移動」操作(CQ-4303028)。

### [!DNL Communities] {#communities-6560}

* 在社交媒體上分享貼文時，會顯示過時的Google+選項(NPR-33877)。

* 社群成員無法修改群組範本或其他群組功能設定(NPR-33530)。

* 影像上的超連結標籤在論壇貼文中無法正確產生(NPR-33464)。

* 無障礙環境支援功能在社群指派功能中識別(NPR-33442)。

* 透過管理控制台新增的社群群組現有使用者會從社群群組主控台中任何修改的使用者清單中移除(NPR-34315)。

* `TagFilterServlet`會洩漏潛在敏感資料(NPR-33868)。

<!--
* Tag filters are vulnerable to sensitive information disclosure (NPR-33868).
-->

### [!DNL Forms] {#forms-6560}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack不包含修正 [!DNL Forms]。它們是使用單獨的[!DNL Forms]附加軟體包傳遞的。 此外，還發行了包含JEE上[!DNL Experience Manager Forms]修正的累積安裝程式。 如需詳細資訊，請參閱「安裝AEM Forms附加元件](#install-aem-forms-add-on-package)」和「在JEE上安裝AEM Forms」。[[](#install-aem-forms-jee-installer)

安裝[!DNL Experience Manager Forms] 6.5.6.0附加軟體包後：

* 停止[!DNL Experience Manager Forms]實例。

* 從`crx-repository\launchpad\ext`目錄中刪除`bcpkix-1.51`、`bcmail-1.51`和`bcprov-1.51` JAR檔案。

* 從`sling.properties`檔案中刪除` sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider`屬性。

* 重新啟動[!DNL Experience Manager Forms]實例。

**調適型表單**

* 當缺少自適應表單片段時，自適應表單無法轉換(NPR-34302)。

* 最適化表單欄位的說明內容說明會顯示段落HTML標籤(NPR-34116)。

* 當您選擇&#x200B;**[!UICONTROL Revalidate on Server]**&#x200B;屬性時，自適應表單無法提交(NPR-33876)。

* **[!UICONTROL 提交到REST端點]**&#x200B;提交操作不適用於自適應表單(CQ-4299044)。

* 協助功能：當您嘗試提交最適化表單而未上傳強制欄位的附件時，焦點不會自動移至附件欄位(CQ-4298065)。

* 將行添加到最適化表單的表格時，**[!UICONTROL 添加到頂部]**&#x200B;和&#x200B;**[!UICONTROL 添加到底部]**&#x200B;選項不顯示適當的結果(CQ-4297511)。

* [!UICONTROL Value Commit]指令碼觸發不正確，導致資料以最適化形式遺失(CQ-4296874)。

* 日期選擇器無法正確運作於本地化的最適化表單(NPR-34333)。

* 當檔案名稱中有底線或空格時，您無法將檔案附加至最適化表單(CQ-4301001)。

* 當巢狀可重複面板的發生次數多於其父面板時，此類巢狀可重複面板的所有發生次數都無法預先填滿(NPR-33666)。

* 最適化表單有一些開放資源解析器。 這會導致提交失敗。 間歇性出現問題(CQ-4299407)。

* 首次開啟欄位設定時，不會顯示屬性圖示(CQ-4296284)。

* 在提交最適化表單時，使用者可以編輯提交中繼資料，例如`afPath`、`afSubmissionTime`和`signers`。 為瞭解決此問題，會從用戶端的表單提交資料中移除中繼資料值。 使用者可使用`FormSubmitInfo`物件從伺服器擷取這些值(NPR-33654)。

* 當向客戶端發送資訊時，用戶輸入未對[!DNL Forms]元件進行適當編碼(NPR-33611)。

**工作流程**

* 當工作流程批准者上傳附件時，附件會重新命名為`undefined`(NPR-33699)。

* [!DNL Experience Manager] 「Workflow Purge（工作流清除）」操作失敗，並顯示以下錯誤消息(NPR-33575):

   `java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory`

* [!DNL Experience Manager Forms] 應用程 [!DNL Windows] 式，以在送出表格後停止回覆(NPR-34409)。

* 當您安AEM裝Service Pack時，**To Do**&#x200B;項目清單不會顯示為連結。 **To Do**&#x200B;項目的文字包含HTML標籤(NPR-34317)。

**互動式通訊**

* 當您包含含有巢狀可重複元件的文字檔案片段時，互動式通訊無法儲存(NPR-34095)。

**通信管理**

* 當您修改包含資料字典值的文字檔案片段時，代理UI會停止回應(NPR-33930)。

* 從[!DNL Microsoft Word]檔案複製貼上內容至字母中的文字檔案片段，會造成格式問題(NPR-33536)。

**文件服務**

* 當您使用「輸出」和「Forms」服務從XDP檔案產生PDF檔案時，會造成遺失和重疊的文字(NPR-34237、CQ-4299331)。

* 將HTML檔案轉換為PDF時，無法設定`MaxReuseCount`屬性(NPR-33470)。

* 當您下載包含Reader擴充功能的PDF檔案時，無法使用[!DNL Adobe Reader]將附件新增至PDF檔案(NPR-33729)。

**文件安全性**

* 在安裝[!DNL Experience Manager] Service Pack(NPR-34310)後，無法在PDF檔案中使用HSM憑證執行簽署作業。

**設計人員**

* 無法在Designer 6.5.x版(CQ-4295322)中開啟XForms。

* 當您開啟Designer時，「歡迎」畫面會顯示錯誤的年份(CQ-4295289)。

* 當您在伺服器上安裝[!DNL Acrobat DC]時，**[!UICONTROL Distribute Form]**&#x200B;選項會停用(CQ-4296304)。

如需安全性更新的詳細資訊，請參閱[Experience Manager安全性公告頁面](https://helpx.adobe.com/security/products/experience-manager.html)。

## [!DNL Adobe Experience Manager] 6.5.5.0  {#experience-manager-6550}

Adobe Experience Manager6.5.5.0是重要的更新，其中包括自2019年4月&#x200B;**推出6.5版以來發佈的新功能、主要客戶要求的增強功能以及效能、穩定性和安全性增強功能。**&#x200B;它可安裝在Adobe Experience Manager6.5之上。

[!DNL Adobe Experience Manager] 6.5.5.0中引入的一些主要功能和增強功能包括：

* 不允許匿名存取CRXDE Lite。 而是將使用者導向登入畫面。 請參閱[使用CRXDE Lite開發](/help/sites-developing/developing-with-crxde-lite.md)。

* 自定義顯示在[!DNL Adobe Experience Manager]收件箱中的列名。

* 已改善Experience Manager網頁內容管理(WCM)中各個區域的協助功能，例如頁面編輯器、核心元件、RTE和管理員使用者介面。

* 將[!DNL Interactive Communication]儲存為草稿。

* 支援[!DNL Oracle WebLogic 12]Experience ManagerJEE上的Forms。

* 已改善[!DNL Adobe Experience Manager Assets]使用者介面流程中的例外處理。

* 若要取得Dynamic Media·Scene7的發佈URL，會在`com.day.cq.dam.api.s7dam.scene7.ImageUrlApi`介面中新增`getRemoteAssetPublishURL`方法。

* [協助功](#assets-6550) 能增強 [!DNL Adobe Experience Manager Assets] 功能，以符合Web內容協助功能指南(WCAG)。

* 已從Adobe Experience Manager移除Package Share整合。

* 內建存放庫 (Apache Jackrabbit Oak) 更新至 1.22.3 版。

有關6.5 Service Pack 5Experience Manager中介紹的完整功能、主要亮點和主要功能的清單，請參閱[Adobe Experience Manager6.5 Service Pack 5](new-features-latest-service-pack.md)的新增功能。

以下是[!DNL Experience Manager] 6.5.5.0版中提供的修正清單。

### [!DNL Sites] {#sites-6550}

* Experience Manager網站提供從別名發佈或取消發佈頁面的選項。 該選項無效(NPR-33415)。
* 從包含多個範本的範本刪除版面容器時，範本無法正確呈現(NPR-33347)。
* 當「Experience Manager網站」頁面是包含多個即時副本的大型內容集的一部分時，無法載入頁面版本歷史記錄預覽(NPR-33311)。
* 使用「移動」命令更名Experience Manager站點頁面時，不更新頁面標題(NPR-33264)。
* 當您在欄檢視中移動頁面時，欄會消失(NPR-33216)。
* 當語言副本中的本地元件名稱與Blueprint中的元件名稱相同且從Blueprint中推出該元件時，術語`_msm_moved`不添加到本地元件的名稱中(NPR-33208)。
* 「頁面重新導向servlet」會附加。html至ResourceType不是`cq:Page`的Experience Manager網站URL(NPR-33176)。
* 貼上子樹時，沒有選項可決定是否貼上相應的子頁(NPR-33149)。
* 元件即時使用結果的數目限制為49(NPR-33058)。
* 當內容片段以架構為基礎且包含強制文字區域或路徑欄位時，內容片段無法儲存(NPR-33007)。
* 當您使用預設的「體驗片段」元件建立自訂元件並在「Experience Manager網站」頁面中使用時，Experience Manager不會顯示自訂元件的參考（使用）(NPR-32852)。
* 當更名具有大量引用的資料夾時，不會更新該資料夾的許多引用(NPR-32765)。
* 當您啟用來源編輯選項時，它將可用於內嵌全螢幕選項，但在富格文本編輯器的編輯對話框和全螢幕選項中仍會遺失(NPR-32763)。
* 如果您有多欄位，且其在Blueprint的頁面屬性中包含必填欄位（例如下拉式清單或路徑欄位），則當卷出包含此多欄位的頁面時，即時副本的頁面屬性不會儲存(NPR-32751)。
* 螢幕閱讀程式無法使用標題結構來導覽頁面。 此外，「元件」標籤有錯誤的標籤(NPR-32648)。
* 當分頁開始時，「體驗片段選擇器」不會載入所有項目(NPR-32605)。
* 讀取、修改、建立和刪除即時副本的作者權限將被撤銷。 每個作者都必須明確提供讀取和修改權限，才能在Blueprint中移動頁面(NPR-32550)。
* 內容作者無法針對與Adobe Analytics整合的頁面建立Launch(NPR-32548)。
* 當使用者以同步方式繼承時，父頁面的即時副本不會與Blueprint同步，並顯示不正確的狀態(NPR-32500)。
* Experience Manager網站編輯器頁面需要超過15秒的時間來載入(NPR-32413)。
* 某些欄位不顯示取消繼承選項(NPR-32362)。
* 當您選取「體驗片段」元件的路徑並選取「開啟選取對話方塊」核取方塊時，不會導覽至「路徑瀏覽器」中的選取路徑(NPR-32308)。
* 從Experience Manager6.2升級到Experience Manager6.5時，靜態模板的Parsys元件無法正確顯示。 Parsys元件的高度設定為0，其內部元件不可見(NPR-33663)。
* 當使用者複製並貼上相同頁面上的「版面容器」時，「版面容器」中的元件不會顯示(NPR-33648)。
* Dispatcher Health check在日誌檔案中顯示`Invalid cookie header`警告消息(NPR-33629)。
* PreferencesServlet中反映的XSS(NPR-33438)。
* 匿名使用者可存取CRXDE Lite功能(GRANITE-27790)。

### [!DNL Assets] {#assets-6550}

>[!IMPORTANT]
>
>建議[!DNL Experience Manager desktop app]的Windows使用者升級至[案頭應用程式版本2.0.3.2](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/release-notes.html#whats-new-added)，以存取[!DNL Adobe Experience Manager 6.5.5.0]例項上的DAM存放庫。 因為他們在使用案頭應用程式2.0.2版存取[!DNL Adobe Experience Manager] 6.5.5.0實例上的DAM儲存庫時可能會遇到問題。

**Experience Manager資產中的協助工具增強功能**

* 現在可將鍵盤焦點放在[!UICONTROL Comments]清單上，並可點選選項至[!UICONTROL [!UICONTROL [!UICONTROL Timeline]資產面板中「建立新版本]」下的「建立]版本註解」(NPR-33424)。

* 現在可以觸及[!UICONTROL 資產的檢視設定]選項，並使用鍵盤按鍵變更[!UICONTROL 檢視設定]對話方塊中的設定(NPR-33420)。

* 組合方塊的清單方塊快顯視窗（位於不同頁面的各欄位中）現在會將項目顯示為螢幕閱讀程式可宣佈的選項清單(NPR-33516)。

* 螢幕閱讀程式現在已宣佈可排序標題的排序功能（在清單檢視中，[!UICONTROL Timeline]檢視和[!UICONTROL 管理出版物]頁面），而欄標題的排序控制項可透過鍵盤存取(NPR-32979)。

* 可點選的元素，例如註解卡、版本更新、組合方塊和功能表的雪佛龍圖示，現在可以使用鍵盤加以關注並與之互動(NPR-33514)。

* 螢幕閱讀程式現在可正確宣佈[!UICONTROL 前瞻分析檢視]的前瞻分析圖示（用於使用、印象和點按）的功能（或用途）(NPR-33513)。

* 唯讀表單欄位（例如資產[!UICONTROL 屬性]的[!UICONTROL Basic標籤]上停用的欄位）現在可使用鍵盤(NPR-33493, CQ-4273031)加以集中。

* 各種輸入欄位中的標籤現在都是永久標籤（因此可存取），而不只是預留位置標籤，當輸入文字時就會消失(NPR-33475)。

* 不同的標題級別（如頁標題和部分標題）現在被視為螢幕閱讀器用戶具有不同級別的標題(NPR-33471)。

* 互動式使用者介面元素，例如連結和選項（在資產頁面的標題和縮放選項、檔案夾導覽），現在可使用鍵盤存取(NPR-33468、CQ-4271412)。

* [!UICONTROL 管理出版物]頁面上的[!UICONTROL 選項]、[!UICONTROL 範圍]和[!UICONTROL 工作流程]進度指示符現在由螢幕閱讀器正確讀取為進度指示符，而非標籤(NPR-33416)。

* 星級分級表徵圖的顏色（例如在資產[!UICONTROL 屬性]或在卡片視圖中的[!UICONTROL 高級]標籤的[!UICONTROL Rating]部分）被改變，以使視覺有限且沒有顏色感知的用戶能夠看到相應的對比度(NPR-33414)。

* 現在，您可以使用鍵盤按鍵來存取資產詳細資料頁面上[!UICONTROL Comment]欄位旁的Chevron向上箭頭(NPR-33397)。

* 畫面閱讀程式現在可正確宣佈資產[!UICONTROL 屬性]和左側導軌導覽（在資產使用者介面上）的[!UICONTROL 標籤]對話方塊的展開和收合狀態(NPR-33396)。

* [!DNL Adobe Experience Manager]資產上所有已瀏覽頁面的標題現在都是唯一的(NPR-33343)。

* 當導覽樹狀結構時，螢幕閱讀程式現在會正確宣佈樹狀檢視控制的各種元素(NPR-33304)。

* 資產詳細資訊頁面上的[!UICONTROL 時間軸]檢視中不同版本的資產現在可使用鍵盤按鍵存取(NPR-33283)。

* 現在螢幕閱讀程式在使用搜尋功能時，會公佈顯示在Omnisearch組合方塊中的搜尋建議名稱(NPR-33280)。

* 螢幕閱讀程式現在將[!UICONTROL 參考導覽]中的可點按元素和[!UICONTROL 前往連結]宣佈為可點按元素(NPR-33278)。

* 當對話方塊開啟時，螢幕閱讀程式不再公佈[!UICONTROL 共用連結]對話方塊的表格結構資訊（例如列1、儲存格1、表格）(NPR-33268)。

* 螢幕閱讀程式現在可正確宣佈各種組合方塊元素（例如「路徑」欄位和在「資產屬性」的「基本」索引標籤中開啟「選擇」對話方塊的選項）的用途(NPR-33235)。

* 現在，當鍵盤焦點位於螢幕閱讀器用戶上時，會將清單視圖表中可選擇的行的資訊發送給螢幕閱讀器用戶。 當指針懸停在行上時，螢幕閱讀器會宣佈該資訊(NPR-33234)。

* 螢幕閱讀器現在可以訪問用於刪除[!UICONTROL Properties]的[!UICONTROL Basic]標籤中[!UICONTROL Tags]欄位下的每個選定標籤的選項（具有[!UICONTROL x]）(NPR-33206)。

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

* [!UICONTROL 選擇]Download [!UICONTROL （下載）]、Properties（屬性）和More  [!UICONTROL Actions（更多）選項，在Adobe Vieware中，使用鍵盤(NPR-32609)的Asset ]    Insights（查看資產）。

* 當使用鍵盤存取時，螢幕閱讀程式不會再公佈視覺化隱藏內容（例如搜尋結果上標題選單列的內容）(NPR-32606)。

* 螢幕閱讀程式現在已宣佈，控制項標籤在日曆日期選擇器中移至下個月和前幾個月的用途(NPR-32604)。

* 星號分級圖示現在可以使用鍵盤按鍵來集中執行(NPR-32513)。

* 控制視訊音量的功能現在可透過標籤（聚焦在音量滑桿上）和鍵盤上的箭頭鍵（調整音量）存取(NPR-32065)。

* 「檔案大小」篩選器的下界([!UICONTROL From])和上界([!UICONTROL To])輸入欄位的目的現在已向無視螢幕閱讀器使用者宣佈(NPR-32064)。

* [!UICONTROL Create and Translate]表單中的[!UICONTROL Languages]功能表現在可供瀏覽模式的螢幕閱讀器訪問(CQ-4293906)。

* [!UICONTROL References]面板現在可透過下列增強功能存取(NPR-33261、CQ-4293798):

   * 在瀏覽模式中，螢幕閱讀程式焦點不再移至[!UICONTROL 網站參考]、[!UICONTROL 資產參考]、[!UICONTROL 復本]和[!UICONTROL 表單參考]章節下的隱藏多行編輯欄位。

   * 螢幕閱讀程式現在宣佈[!UICONTROL 網站參考]和[!UICONTROL 語言副本]元素的角色。

   * 瀏覽模式中螢幕閱讀器的焦點以有意義的順序轉移到各種元素。

* [!UICONTROL 中繼資料] 結構編輯器頁面及其元素現在可使用鍵盤存取，而且螢幕閱讀器方便使用(CQ-4290962、CQ-4272953)。

* 螢幕閱讀程式現在會宣佈`X`符號移除選取標籤的目的，以及選取標籤的數目(CQ-4273017)。

* 為避免使用螢幕閱讀程式的無視使用者混淆，螢幕閱讀程式現在會忽略裝飾性圖示和影像(CQ-4272944)。

**修正Experience Manager資產的問題**

[!DNL Adobe Experience Manager] 6.5.5.0 Assets可修正下列問題：

* [!UICONTROL 系] 列中資 [!UICONTROL 產的「建] 立工作流程」對話方塊的「開始」已停用，因此無法觸發工作流程(NPR-32471)。

* 在中繼資料結構中使用階層式快顯功能時，在選取並儲存包含縮寫符號的下拉式選項（從子下拉式清單）時，在重新開啟資產[!UICONTROL Properties](NPR-32649)後，選取的縮寫符號選項就會消失。

* [!UICONTROL Asset Insights Sync ] Jobstops在遇到無效項目（在Analytics端）而非移至下一個項目時失敗(NPR-32674)。

* 由於全景檢視器中的行動瀏覽器預設會停用運動感應器，因此陀螺儀無法運作(CQ-4272937)。

* [!UICONTROL 在6.5.1] 上安裝6.5.3時，「Connected Assets Configuration」（連接的資產配置）嚮導無法處理404錯誤(NPR-32730)。

* 在回寫程XMP序中，所有自定義命名空間元資料屬性都將自定義命名空間前置詞更改為ns2，而不是配置的命名空間前置詞(NPR-32748)。

* 不會觸發延遲載入，在選取來檢閱通知收件匣中的工作時，只會顯示100個資產(NPR-32750)。

* `NullPointerException` 會因為新建立的使用者描述檔(SAML/SSO)中遺失節點偏好設定而觀察到。此錯誤會阻止新登入的使用者使用[!DNL Adobe Experience Manager Stock]整合(NPR-32777)。

* 在開啟包含超過10,000個資產的智慧型系列時，記錄檔會出現遍歷警告(NPR-32980)。

* 在[!DNL Adobe Experience Manager]的Dynamic MediaScene7執行模式中，當資產從一個資料夾移至另一個資料夾時，資產名稱會變更為小寫(NPR-32995)。

* 從搜尋結果導覽至其屬性，然後返回搜尋結果以刪除已搜尋的資產後，無法刪除該資產(NPR-32998)。

* [!UICONTROL 在「] 移動資產」介面中選取目標資料 [!UICONTROL 夾時，] 「下一步」仍會停用(NPR-33356)。

* [!UICONTROL 在選] 擇父節點（其中顯示單個子資料夾），然後選擇子資料夾時，未啟用「下一步」(NPR-33275)。

* 對於具有刪除權限的用戶，即使已授予讀取、建立或修改等其他權限，簽入和簽出權限在Adobe資產連結(AAL)上也會被禁用(NPR-33272)。

* 智慧型裁切轉譯無法在資產下載對話方塊中使用(NPR-33167)。

* 在具有智慧型裁切設定檔的檔案夾下開啟PDF轉譯邊欄的記錄檔中，會發現異常(CQ-4294201)。

* 如果與Dynamic MediaScene7執行模式Experience Manager時，預設停用[!UICONTROL Dynamic Media同步模式]，影像預設集就不會發佈(CQ-4294200)。

* 大量上傳時的資產處理會停滯，而工作流程例項則會顯示DAM更新資產的停滯例項(CQ-4293916)。

* 在Experience Manager上建立Dynamic Media配置有效，但在用戶介面上選擇「保存」時不會發生任何情況(CQ-4292442)。

* 在Safari/Mac上漸進式播放時，F4V視訊資產的預覽無法運作(CQ-4289844)。

* 在智慧型裁切資產時，會建立額外的資料夾，該資產位於父資料夾內，名稱中包含點`.`字元(CQ-4289337)。

* 縮圖中斷，而視訊處理橫幅在複製視訊時不會顯示(CQ-4284125)。

* Dimensional檢視器會針對某些具有空白相機檢視的機型，在Firefox中錯誤顯示空白縮圖(CQ-4283447)。

* 6.5.5.0中修正的效能問題有：(CQ-4279206):

   * 將大型二進位檔上傳至Dynamic Media影像處理伺服器需要太長的時間。

   * 由於Dynamic Media·Scene7的架構，Experience Manager的縮圖產生時間增加。

* Dynamic MediaScene7移轉問題對擁有大量資產的客戶來說失敗(CQ-4279206)。

* 如果使用`setVideo`，則視訊360檢視器的版面會中斷，而視訊會使用`video= modifier`向下移動(CQ-4263201)。

* 安裝Experience ManagerSDL軟體包時顯示錯誤資訊(NPR-33175)。

* SSRF在Experience Manager的漏洞(NPR-33435)。

### 平台 {#platform-6550}

* 如果在`/etc/maps`下建立`sling:match`映射條目，則不調用[!DNL Sling]過濾器(NPR-33362)。
* Experience Manager因[!DNL Apache Lucene]的分段錯誤而當機(NPR-32988)。
* [!DNL Jackson] Experience Manageruberjar檔案中缺少核心軟體包(NPR-32848)。
* CRXDE Lite不會在沒有節點`jcr:primaryType`屬性讀取權限的情況下為用戶載入內容(NPR-32611)。
* [!DNL Granite] 維護任務調度程式在Experience Manager部署期間重新初始化的頻率過高(CQ-4294627)。
* 當SQL查詢長時間執行（例如7小時）時，Experience Manager停止響應(NPR-33044)。

### 使用者介面{#ui-6550}

* 多欄位中不會持續選擇選項按鈕(NPR-33309)。
* 清單檢視無法使用延遲載入限制(NPR-33124)。
* 如果沒有相符項目，Omnisearch結果頁面不會顯示訊息(NPR-32974)。
* Omnisearch篩選器會在忽略所選位置的`/content`節點下傳回所有相符項目(NPR-32849)。

### 整合{#integrations-6550}

* 當發佈具有Adobe Target元件的頁面時，會清除內部快取(NPR-33162)。
* 與Adobe Target的整合在[!DNL Windows Internet Explorer] 11(NPR-33111)上不起作用。
* 在設定Adobe Target時，在選擇報告來源時，[!UICONTROL 公司]和[!UICONTROL 報表套裝]欄位不會出現(NPR-32502)。
* 使用[!DNL Adobe I/O]匯出[!DNL Experience Fragments]時，像「來源產品」這樣的中繼資料不會匯出至Adobe Target(NPR-32159)。
* 本機Experience Manager管理群組中的授權IMS使用者無法建立或修改IMS組態(NPR-33045)。
* Adobe啟動配置頁面不會顯示所有記錄(NPR-33011)。
* 內容作者群組中的使用者無法編輯Adobe Target元件的屬性，因為JavaScript錯誤(NPR-32996)。
* JSON的跨網站指令碼(NPR-32744)。

### 翻譯專案 {#translation-6550}

* 翻譯的標籤不會從第三方翻譯服務導入Experience Manager(NPR-33154)。
* 翻譯配置頁顯示的翻譯提供程式與用於翻譯的翻譯提供程式不正確(NPR-32971)。
* 將體驗片段資料夾新增至現有的翻譯專案，會建立新專案(NPR-32843)。
* 在運行翻譯作業的日誌中出現`NullPointerException`錯誤(NPR-32628)。

### WCM {#wcm-6550}

* 頁面編輯器- [!DNL Sites]頁面編輯器不允許僅限鍵盤的使用者略過至主要內容，而不允許在標題中的所有選項間切換標籤焦點(CQ-4293883)。
* 頁面編輯器——使用Well元件並包含已儲存資料的面板不會顯示，因為[!DNL Chrome]和[!DNL Firefox]版本的更新(CQ-4292995)。
* MSM —— 從頁面刪除元件並不會從頁面的發佈版本中刪除元件(CQ-4292360)。

### [!DNL Brand Portal] {#assets-brand-portal-6550}

* 從[!DNL Brand Portal]移除已發佈的中繼資料結構會導致錯誤(CQ-4292063)。
* 如果管理員透過Adobe開發人員主控台設定[!DNL Experience Manager Assets] 6.5.4與品牌入口網站，[!DNL Brand Portal]使用者無法將貢獻資料夾的資產從[!DNL Brand Portal]發佈至[!DNL Experience Manager](NPR-33046)。
* 重複複製父資料夾導致衝突(NPR-33001)。

### [!DNL Communities] {#communities-6550}

* 無法使用快速編輯功能表選項刪除協調主控台中的資訊卡(NPR-33117)。
* 存取[!UICONTROL 活動串流]頁面時發生錯誤(NPR-33146)。
* 在作者例項上刪除的群組不會從所有發佈例項中移除(NPR-33199)。
* 建立新群組後，作者不會重新導向至[!DNL Internet Explorer] 11上的[!UICONTROL 社群群組]區段(NPR-33205)。
* 在Experience Manager收件箱中訪問留言不會將留言的狀態更改為「已讀取」(NPR-32764)。
* 編輯[!DNL Communities]群組並變更縮圖影像並不會更新群組縮圖影像(NPR-32599)。
* 使用者無法傳送電子郵件給社群中的其他使用者(NPR-32598)。
* 提交的部落格在使用者重新整理頁面之前不會顯示(NPR-32391)。
* 建立使用者產生的內容(UGC)的通知和訂閱版本時，會儲存來源頁面的錯誤ID(CQ-4279355、CQ-4289703)。
* 跨網站指令碼問題(NPR-33203)。

### 工作流程 {#workflow-6550}

* 左側導軌中的[!UICONTROL 時間軸]選項的載入時間比預期要長(NPR-32851)。
* 重新啟動Experience Manager例項後，系列的審閱工作電子郵件會包含錯誤的裝載連結(NPR-32774)。

### [!DNL Forms] {#forms-6550}

>[!NOTE]
>
>Experience Manager服務包不包含[!DNL Forms]的修正。 它們是使用單獨的Forms附加套件傳送的。 此外，還發行了包含AEM FormsJEE修正的累積安裝程式。 如需詳細資訊，請參閱[安裝Experience ManagerForms附加元件](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package)和[在JEE上安裝Experience ManagerForms元件。](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer)

* 通信管理：在提交信件(NPR-33359、NPR-33153)後，目標區域內資產的順序被混亂。
* 適應性Forms:當用戶編輯自適應表單時，[!UICONTROL 頁面資訊]菜單中可用的[!UICONTROL 啟動工作流]選項無效(NPR-33004)。
* 適應性Forms:用戶無法保存具有多個附件的自適應表單(NPR-32997)。
* 適應性Forms:以最適化表單變更面板版面會導致錯誤(CQ-4293880)。
* 適應性Forms:自適應表單字典中字串的新行將`&#xa;`字元添加到字典(NPR-33266)。
* 適應性Forms無障礙環境：當使用者將最適化表單預覽為HTML表單時，[!UICONTROL 塗鴉簽名]欄位無法保留標籤焦點(NPR-33159)。
* 適應性Forms無障礙環境：提交最適化表單時顯示的錯誤訊息不會連結至`aria-describedBy`屬性(NPR-33071)。
* 適應性Forms無障礙環境：在ARIA無障礙環境支援模式中，在最適化表單中標示為強制的欄位，沒有將強制屬性設為True(NPR-33070)。
* PDFG服務：當使用者將文字檔案轉換為PDF時，日文字元無法正確顯示(NPR-33238)。
* PDFG服務：`CreatePDF`操作無法將PDF檔案轉換為PDF OCR格式(NPR-32994)。
* PDFG服務：第200個[!DNL OpenOffice]檔案例項的PDF轉換失敗(NPR-32766)。
* 後端整合：表單資料模型請求會因重新整理Token因非作用中狀態不正確而失敗(NPR-33169)。
* 設計人員：螢幕閱讀程式會根據預設的地理順序來執行Tabbing順序，而非XDP檔案中定義的自訂Tabbing順序(NPR-32160)。
* 設計人員：如果啟用標籤選項，子表單邊框會消失在產生的PDF輸出中(NPR-32778)。
* 將XSS與GuideSOMProviderServlet一起儲存(NPR-32700)。

## Adobe Experience Manager6.5.4.0 {#experience-manager-6540}

Adobe Experience Manager6.5.4.0是重要的更新，其中包括自2019年4月&#x200B;**推出6.5版以來所發佈的新功能、主要客戶要求的增強功能和效能、穩定性、安全性改進。**&#x200B;它可安裝在Adobe Experience Manager6.5之上。

Adobe Experience Manager6.5.4.0中引進的一些主要功能和增強功能包括：

* Adobe Experience Manager資產現在已透過[!DNL Adobe I/O]主控台設定品牌入口網站。

* 新的[產生可列印的輸出](../forms/using/aem-forms-workflow-step-reference.md)步驟現在適用於Adobe Experience Manager Forms工作流程。

* [多欄支援](../forms/using/resize-using-layout-mode.md) 最適化表單和互動式通訊的版面模式。

* 支援HTML5表單中的[Rich Text](../forms/using/designing-form-template.md)。

* [協助工具](new-features-latest-service-pack.md#accessibility-enhancements) 可增強Experience Manager資產。

* 內建存放庫 (Apache Jackrabbit Oak) 更新至 1.10.8 版。

* 您現在可以將選擇性內容子樹同步到&#x200B;*Dynamic Media-Scene7模式*，而不是所有`content/dam`的可用模式。

* 與SOAP web service整合的表單資料模型現在支援元素上的選擇群組或屬性。

* SOAP輸入或輸出和複雜的資料結構現在支援動態群組替代。

有關最新Service Pack中介紹的完整功能和重點介紹的清單，請參閱[《Adobe Experience Manager6.5 Service Packs的新增功能》](new-features-latest-service-pack.md)。

### 網站 {#sites-fixes}

* 當Adobe Experience Manager Sites頁面的URL包含冒號(`:`)或百分比符號(`%`)時，瀏覽器停止響應，CPU使用尖峰(NPR-32369, NPR-31918)。

* 當開啟「Experience Manager網站」頁面進行編輯並複製元件時，某些預留位置仍無法使用貼上動作(NPR-32317)。

* 當「管理出版物」精靈開啟時，連結至核心元件的體驗片段不會顯示在發佈的參考清單中(NPR-32233)。

* Touch UI中的即時文案總覽要比Classic UI演算的時間長得多(NPR-32149)。

* 當伺服器時間和機器時間位於不同時區時，排程的發佈時間會在Touch UI中顯示伺服器時間，而在Classic UI中，則會顯示機器時間(NPR-32077)。

* Experience Manager網站無法開啟URL中含有尾碼的頁面(NPR-32072)。

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

* 無法同步包含OOTB（現成）設計匯入工具元件的Adobe促銷活動中的促銷活動(NPR-31728)。

* 當您嘗試將項目符號清單變更為編號清單時，僅會變更清單的前兩個項目(NPR-31636)。

* 當頁面未編寫且選取子節點時，選擇對話方塊仍會顯示初始節點。 當製作頁面並使用者按一下瀏覽時，頁面會重新導向至根節點，而非製作的節點(NPR-31618)。

* 「查看配置」對話框對於「收件箱」自定義工作流功能（NPR-32503和NPR-32492）無法正常工作。

* 使用「收件箱」(CQ-4282168)查看工作流資訊時，會顯示錯誤消息。

### 資產 {#assets-6540-enhancements}

* 資產收集頁面上觸發工作流程的按鈕已停用(NPR-32471)。

* 在SPS(Scene7出版系統)中建立無名稱的檔案夾，同時將資產從一個檔案夾移至另一個檔案夾(與Dynamic MediaScene7組態Experience Manager)(NPR-32440)。

* 將所有資產（使用「全選」然後移動）移至包含已發佈資產的檔案夾的動作會失敗並出現錯誤(NPR-32366)。

* 產生具有${extension}的資產的轉譯失敗(NPR-32294)。

* 版本歷史記錄URL顯示在資產屬性頁面上的「參考者」欄位下(NPR-31889)。

* 無法從DAM下載的ZIP檔案，無法使用WinZip開啟(NPR-32293)。

* 當開啟「檔案夾設定」以變更檔案夾標題或縮圖影像，然後儲存檔案夾的原始權限時，會更新檔案夾的權限(NPR-32292)。

* 已排程啟動的日曆圖示不會顯示在「狀態」欄（位於DAM資產清單的傳統UI中）中，以取得已排程在日後日期和時間啟動的資產(NPR-32291)。

* 使用程式碼片段範本建立程式碼片段會在程式碼片段建立程式期間搜尋系列時發生錯誤(NPR-32290)。

* 從搜尋篩選器選取多個標籤時，會引發多個搜尋查詢(NPR-32143)。

* Experience Manager資產使用者介面會在上傳檔案名稱中超過50個字元的資產時，顯示截斷的檔案名稱(NPR-32054)。

* 在選中Adobe Stock的複選框樹的第2級複選框時，清除第一個複選框和第二個複選框時，會清除「過濾器」面板中的所有複選框(NPR-31919)。

* 使用Omnisearch Facets的檔案和資料夾搜尋會產生例外(NPR-31872)。

* 即使在相應元資料模式表單中設定相關性規則時，在元資料編輯器中用於強制欄位選擇的欄位突出顯示也不會被刪除(NPR-31834)。

* 葉層級標籤的完整名稱（來自標籤階層）不會顯示在資產屬性頁面中(NPR-31820)。

* 使用Safari瀏覽器上資產屬性頁面的back命令會顯示錯誤(NPR-31753)。

* 觸控式UI搜尋（透過Omnisearch完成）結果頁面會自動捲動並遺失使用者的捲動位置(NPR-31307)。

* PDF資產的資產詳細資料頁面不會顯示動作按鈕，但在Dynamic MediaScene7執行模式(CQ-4286705)上執行的Experience Manager中，「至系列」和「新增轉譯」按鈕除外。

* 資產在完成Scene7的批次上傳程式(CQ-4286445)後，處理時間過長。

* 當用戶未在Dynamic Media客戶端的設定編輯器中進行任何更改時，保存按鈕不導入遠程設定(CQ-4285690)。

* 當支援的3D模型已收錄到Experience Manager中時，3D資產縮圖不提供資訊(CQ-4283701)。

* 智慧型裁切影片檢視器預設集的未處理狀態會在橫幅文字上與預設名稱一起顯示兩次(CQ-4283517)。

* 在資產的詳細資料頁面(CQ-4283309)上，會發現在3D檢視器中預覽的已上傳3D模型容器高度不正確。

* 在IE 11中Experience ManagerDynamic Media混合模式(CQ-4255590)的轉盤編輯器未開啟。

* 鍵盤焦點會卡在「下載」對話方塊、Chrome和Safari瀏覽器的「電子郵件」下拉式清單中(NPR-32067)。

* 嘗試在Experience Manager上添加DM雲配置時，預設情況下未啟用「同步所有內容」複選框(CQ-4288533)。

### Foundation UI {#foundation-ui-6540}

* 滑鼠控制項會移至先前的篩選欄位，而非在使用「篩選」面板搜尋資產時保留在現有的篩選欄位中(NPR-32538)。

* 平台標籤：在標籤欄位中輸入以搜尋標籤會顯示根邊界以外的標籤，而不會尊重標籤欄位的`rootPath`屬性(NPR-31895)。

* 平台UI:如果在文字欄位中新增無效路徑，路徑瀏覽器會中斷(NPR-31884)。

* 通知會隱藏在頁面選擇的嚴格功能表後方(NPR-31628)。

### 平台 {#platform-sling-6540}

* (HTL)底線取代URL路徑區段中的冒號(NPR-32231)。

### 專案 {#projects-6540}

* 即使使用者有權在子資料夾中建立專案，使用者也看不到「建立」按鈕(NPR-31832)。

### 項目翻譯{#projects-translation-6540}

* 在`Apache Sling JSP Script Handler`中啟動「修剪空間」選項時，翻譯項目建立會中斷UI(NPR-32154)。

* 將任何要翻譯的標籤添加到翻譯項目時，UI中出現錯誤，錯誤日誌中出現Null點異常(NPR-31896)。

### 整合{#integrations-6540}

* 啟動程式庫URL的產生僅以啟動API的`path`和`library_name`值為基礎，並非以`library_path`值為基礎(NPR-31550)。

* 處理LiveFyre相關項目(FYR-12420)時會顯示錯誤訊息。

* ReportSuitesServlet 容易遭受 SSRF 攻擊 (NPR-32156)。

### WCM模板編輯器{#wcm-template-editor-6540}

* 在可編輯的範本結構模式中，版面容器中允許的元件清單不會顯示連結按鈕元件(CQ-4282099)。

### WCM頁面編輯器{#wcm-page-editor-6540}

* 選取覆蓋，然後選取回應式格點拖曳元件時，會出現錯誤(CQ-4283342)。

### Campaign 目標定位 {#campaign-targeting-6540}

* Target雲端設定失敗，並出現錯誤get mbox請求失敗(CQ-4279880)。

### 品牌入口網站 {#assets-brand-portal-6540}

* 品牌入口網站使用者無法在升級至6.5.4Experience Manager(CQDOC-15655)上的[!DNL Adobe I/O]時，將貢獻資料夾資產發佈至[!DNL Assets]。 有關6.5.4Experience Manager的立即修正，建議您下載修補程式](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/hotfix/cq-6.5.0-hotfix-33041)並安裝在您的作者實例上。[

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

### Oak-索引與查詢{#oak-indexing-6540}

* 使用Tika剖析器剖析包含JPEG影像的MS Word和MS Excel檔案時，無法剖析，並發現類別找不到錯誤(NPR-31952)。

### 表單 {#forms-6540}

>[!NOTE]
>
>Experience Manager服務包不包含Experience ManagerForms的修正。 它們是使用單獨的Forms附加套件傳送的。 此外，還發行了包含Adobe Experience Manager FormsJEE修正的累積安裝程式。 如需詳細資訊，請參閱[安裝Experience ManagerForms附加元件](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package)和[在JEE上安裝Experience ManagerForms元件。](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer)

* 通信管理：信件在提交至後置處理工作流程後會顯示額外的字元(NPR-32626)。

* 通信管理：信件在提交至後處理工作流程後，會將下拉式預留位置顯示為文字元件(NPR-32539)。

* 通信管理：字母模板中定義的預設值不會顯示在預覽模式(NPR-32511)中。

* 行動Forms:在HTML版本中轉譯XDP表單時，提交按鈕會顯示為已擴充的大小(NPR-32514)。

* 檔案服務：在套用Service Pack 2後，Letters和某些其他頁面的URL存取問題(NPR-32508、NPR-32509)。

* 檔案服務：如果伺服器上的交易數超過特定限制，HTML至PDF的轉換會失敗，而且檔案類型設定會從[!DNL Forms]伺服器移除(NPR-32204)。

* 適應性Forms:瀏覽器協助工具會根據WCAG2 Level AA准則，報告調適性表單的失敗(NPR-32312、NPR-32309、CQ-4285439)。

* 適應性Forms:Chrome瀏覽器協助工具報告最佳實務失敗(NPR-32310)。

* 適應性Forms:在配置嵌入Experience Manager站點頁面的自適應表單時的翻譯問題(NPR-32168)。

* 工作台：使用「取得PDF公用程式」服務的「PDF屬性」作業時，會顯示錯誤訊息(NPR-32150)。

* 檔案安全性：將DisableGlobalOfflineSynchronizationData選項設為True時，受保護的PDF檔案無法離線開啟(NPR-32078)。

* 設計人員：如果啟用標籤選項，子表單邊框會消失在產生的PDF輸出中(NPR-32547、NPR-31983、NPR-31950)。

* 設計人員：如果表格中有合併的儲存格，則無障礙環境支援測試會失敗，無法針對使用輸出服務(CQ-4285372)從XDP表單轉換的輸出PDF檔案進行協助功能測試。

* Foundation JEE:如果Experience ManagerForms伺服器與群集斷開連接，快取問題會阻止其重新連接到伺服器(NPR-32412)。

## Adobe Experience Manager6.5.3.0 {#experience-manager-6530}

[!DNL Adobe Experience Manager] 6.5.3.0是重要的版本，其中包括效能、穩定性、安全性，以及自2019年4月6.5版全面推出以來所發行的重要客戶修 **正與增強**。它可安裝在[!DNL Adobe Experience Manager] 6.5之上。

此Service Pack版本的一些主要亮點是：

* 內建存放庫 (Apache Jackrabbit Oak) 更新至 1.10.6 版。

* [!DNL Experience Manager Assets] 現在支援使用Deflate64演算法建立的ZIP封存。

* 已在DAM清單檢視中新增可排序的建立日期新欄，並在清單檢視中新增資產搜尋結果。

* 已在「清單」檢視中啟用「名稱」欄的資產排序。

* [!DNL Dynamic Media] 現在支援智慧型裁切視訊資產。Smart Crop是機器學習驅動的功能，可在移動影格時重新裁切視訊，以跟隨場景的焦點。

* [!DNL Dynamic Media] 支援智慧映像。

* [在[!DNL Experience Manager]工作流程中設定Out of Office](../forms/using/configure-out-of-office-settings.md)偏好設定。

* [可與[!DNL Experience Manager]工作流程中的其他使用者共用收件匣或收件匣項目](../forms/using/configure-shared-queues-osgi.md)。

* 能夠[以批次模式](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)生成互動式通信。

* ContextHub中已整合的jQuery更新版本至3.4.1。

### 資產 {#assets-6530-enhancements}

**產品增強功能**

* [!DNL Experience Manager Assets] 現在支援使用Deflate64演算法建立的ZIP封存(NPR-27573)。

* 在DAM清單檢視中新增可排序的建立日期欄，並在清單檢視中新增資產搜尋結果欄(NPR-31312)。

* 在清單檢視中，使用者可使用[!UICONTROL Name]欄來排序資產清單(NPR-31299)。

* DAM的[!UICONTROL Asset Details]頁面中可預覽GLB、GLTF、OBJ和STL檔案(CQ-4282277)。

* `ReplicationOnModifyListener` 事件會在區塊上傳期間針對區塊節點 [!DNL Dynamic Media] 觸發(CQ-4281279)。

* [!DNL Dynamic Media] 現在支援智慧型裁切視訊資產。Smart Crop是機器學習驅動的功能，可在移動影格時重新裁切視訊，以跟隨場景的焦點(CQ-4278995)。

* [!DNL Dynamic Media] 支援Smart Imaging(CQ-422249)。

* 如果查詢參數傳入請求中，搜尋或瀏覽檢視會設為Foundation選擇器中的預設檢視(NPR-31601)。

**修正**

* 某些PDF檔案的中繼資料不會在標題修改時更新並儲存至PDF(NPR-31629)。

* 資產共用不適用於檔案名稱中有加號(`+`)的資產(NPR-31547)。

* 預設搜尋表單中的「資產管理搜尋邊欄」編輯無法如預期般運作(NPR-31502)。

* 當使用Omnisearch on assets view for serching assets時，不會顯示建議(NPR-31496)。

* 當參考的資產移至其他位置時，系列中的資產參考不會更新，因為不同的使用者會參考不同的資產(NPR-31486)。

* 重複的IPTC標籤會新增至資產中繼資料(NPR-31328)。

* 當從過濾器邊欄觸發搜索時，搜索結果計數不會準確更新(NPR-31316)。

* 取消選擇「檔案類型」過濾器中的第二級複選框時，所有複選框都會被清除，搜索欄中的文本與選定或取消選擇的屬性不同步(NPR-31287)。

* 不能從資料夾的「成員」部分中刪除所有成員（用戶／組）;在嘗試移除所有使用者時，登入的使用者會新增至清單(NPR-31171)。

* 無法刪除檔案名稱中加號(`+`)的資產(NPR-31162)。

* 建立下拉式選單（在選取資料夾時，會在頂端選單中顯示）不會將「資料夾」顯示為建立選項(NPR-30877)。

* 當對用戶應用路徑上拒絕`jcr:removeChildNodes`和`jcr:removeNode`的ACL時，資料夾選擇「建立」>「檔案上載」操作項目丟失(NPR-30840)。

* 當某些mp4資產上傳時，DAM工作流程會進入過時狀態，導致所有剩餘的工作流程都進入過時狀態(NPR-30662)。

* 當大型PDF檔案（數GB）上傳至DAM並處理其子資產時，會出現記憶體不足錯誤(NPR-30614)。

* 大量移動資產失敗並顯示警告訊息(NPR-30610)。

* 在[!DNL Dynamic Media]-Scene7模式中，在[!DNL Experience Manager]的中，資產名稱會變更為小寫(NPR-31630)。

* 編輯遠程映像集時，對於與Scene7公司名稱相同的資料夾中的映像，會出現錯誤(NPR-31340)。

* [!DNL Dynamic Media] 包含參考的資產不會發佈(NPR-31180)。

* 從[!DNL Dynamic Media]7-Scene7模式到[!DNL Dynamic Media Classic]的上載過長而無法完成(NPR-31048)。

* 新增至影像資產的熱點無法透過資產詳細資料頁面的互動式影像檢視器顯示(NPR-30979)。

* 當在[!DNL Experience manager Assets]中對資產執行的動作傳遞至Scene7時，就會建立巨大的sling工作，並重新顯示「處理」橫幅(NPR-30947)。

* 在建立不上傳到Scene7的資產和資產的語言副本時發生衝突(NPR-30932)。

* 從[!DNL Dynamic Media]-Hybrid模式中執行的[!DNL Experience Manager]下載的動態轉譯會中斷（它們是具有內容「找不到影像」而非影像內容類型的文字類型）(NPR-30876)。

* [!DNL Dynamic Media] 「編碼視訊」工作流程無法產生從Adobe Experience Manager移轉 [!DNL Dynamic Media Classic] 至 [!DNL Dynamic Media]Scene7模式的視訊縮圖(CQ-4282011)。

* 使用不同的Scene7公司ID(CQ-4280548)，將資產從一個實例遷移到另一個實例時觀察到IpsApiException。

* 當支援的3D模型已收錄至[!DNL Experience Manager](CQ-4283701)時，「3D資產」縮圖不提供資訊。

* 如果3D資產的相機檢視次數很少，檢視器中會顯示捲動按鈕(CQ-4283322)。

* 在「資產詳細資料」頁面的DimensionalViewer中預覽的已上傳3D模型容器高度不正確(CQ-4283309)。

* 無法在Internet Explorer 11和Safari上使用SmartCropVideoViewer播放視訊(CQ-4281422)。

* 使用移動按鈕將多個資產從一個資料夾移至另一個資料夾時，在[!DNL Dynamic Media]-Scene7執行模式(CQ-4280384)上執行的[!DNL Experience Manager]中失敗。

* 當MIME類型不是MP4時，資產詳細資料上會顯示扭曲的視訊(CQ-4279704)。

* 新收錄在具有視訊描述檔的資料夾中的視訊，即使編碼百分比完成到100%後，仍會維持處理狀態(CQ-4279389)。

* 從資料夾移動資產會建立大量的sling工作(Scene7API呼叫)，而非理想的必要作業(CQ-4278664)。

* 當在DAM中建立影像集（或mediaset）並使用適當的命名慣例命名時，影像集的名稱會變更為Scene7的小寫(CQ-4281112)。

* Scene7遷移程式錯誤地設定發佈狀態(CQ-4263492)。

* 觸控UI搜尋（透過Omnisearch完成）結果頁面會自動捲動，並遺失使用者在內容片段中的捲動位置(CQ-4282898)。

* PDF檔案不會建立索引，而內容則無法搜尋(CQ-4278916)。

* 出現「Group not listed by user picker（組未由用戶選擇器列出）」錯誤：在新增具有不同`principalName`和`authorizableId`的封閉使用者群組時，會觀察到expected false to equal true&quot;(CQ-4278177)。

* 資產UI欄檢視會顯示所有路徑，不論特定租用戶的dam根路徑為何(CQ-4278175)。

* 資產選擇器的搜尋無法如預期般運作(CQ-4275886)。

* 轉譯工作流程失敗(CQ-4271928)。

* DAM事件清除會刪除最新(`maxSavedActivities`)的事件資料並保存先前建立的資料(NPR-31336)。

* 觸控式UI搜尋（透過Omnisearch完成）結果頁面會自動捲動並遺失使用者的捲動位置(NPR-31307)。

* 在Touch UI中選取全部然後取消選取某些項目（資料夾／個別資產）時，動作列和資產計數不會更新(NPR-31118)。

* 在輪詢資產的作業詳細資訊時，[!DNL Experience Manager]中顯示例外(CQ-4283569)。

### 網站

* 如果LiveCopy繼承中斷，即時副本頁面會顯示語言副本連結，而非LiveCopy連結(NPR-30980)。
* 對於新的Blueprint，如果記錄數超過40，則只會顯示前40個記錄。 Blueprint會為其餘的記錄顯示空白行(NPR-31182)。
* 當使用者在功能表的description屬性中新增日文或韓文字元時，功能表會顯示日文和韓文文字的扭曲字元(NPR-31331)。
* 富格文本編輯器(RTE)不允許將嵌入的表作為清單項插入(NPR-30879)。
* 立即可用的架構Rich Text Editor(RTE)。 意外地將內嵌字型大小套用至元素(NPR-31284)。
* 當使用者聚焦於左方邊欄的欄位，並使用鍵盤快速鍵貼上內容時，貼上了頁面編輯器剪貼簿的內容，而非左方邊欄的欄位內容 (NPR-31172)。
* 當用戶將「檔案上傳」欄位添加到多欄位時，影像路徑儲存在元件節點中，而不是多欄位節點(NPR-30882)。
* `ResponsiveGridExporter` API不會傳回`com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter`介面。 `com.day.cq.wcm.foundation.model.impl`軟體包聲明為專用軟體包(NPR-31398)。

<!-- Review: NPR-31398 has fixVersion as 6530. However, it is mentioned twice in 6530 and 6520 as fixed. 
Remove one mention of this fix.
-->

* 在非編輯器模式（在「作者」中不含`editor.html`前置詞和`wcmmode=disabled`，或在「發佈者」中）中開啟包含某些「體驗片段」的頁面時，請求會以HTTP狀態錯誤碼`500`結束(NPR-30743)。
* 使用者無法變更密碼並存取其描述檔頁面(NPR-31161)。

### 搜索和用戶介面{#ui-interface-and-search}

* 從卡片檢視切換至搜尋結果頁面上的清單檢視時，在可捲動頁面之前會有延遲(NPR-31286)。

* [!UICONTROL 選擇所有]複選框隱藏在[!DNL Sites]用戶介面的清單視圖中(NPR-31614)。

* 搜索結果頁上的[!UICONTROL 選擇全部]計數不正確(NPR-31120)。

* 中繼資料編輯器會顯示不存在的標籤(NPR-31119)。

### 轉換 {#translation}

* 在翻譯工作中選擇「到期日期」選項時，會出現兩個日曆彈出式選項(NPR-31270)。

### 平台

* Web控制台中的Mime類型選項無效(NPR-31108)。

* 在設定單一登入時不接受用戶端憑證(NPR-31165)。

* 未儲存 Jetty 型 HTTP 服務的緩衝區大小設定更新 (NPR-30925)。

* QueryBuilder現在支援xpath查詢中的orderby `fn:name()`(NPR-31322)。

* 從[!DNL Experience Manager] 6.3升級時會建立重複的啟動樹(NPR-31513)。

* 轉送的請求不會保留在sling驗證期間設定的回應標頭(NPR-30013)。

* 在機械臂元件中搜索無法工作(NPR-31692)。

* 由於Apache POI和Apache Tika搭售的不同版本，將ZIP檔案附加至[!DNL Experience Manager Communities]貼文時，會顯示錯誤(NPR-31018)。

* `org.apache.sling.distribution.api`捆綁包隱藏在配置管理器中，因此無法用於定制捆綁包(NPR-31720)。

### 專案

* 切換日曆視圖無效(NPR-31271)。

### 品牌入口網站 {#assets-brand-portal-6530}

**產品增強功能**

* [!DNL Experience Manager Assets]中的資產來源補充匯入工作流程已修改為僅將新建立的資產從[!DNL Brand Portal]擷取至[!DNL Experience Manager]，並略過NEW檔案夾中已存在的資產以避免複製(CQ-4278527)。

**修正**

* 在「資產來源補充」功能中建立新的「貢獻」檔案夾時，會出現不正確的圖示(CQ-4282825)。
* 建立新的「貢獻」檔案夾時，「貢獻」檔案夾中不會顯示一或兩個子檔案夾（NEW和SHARED）(CQ-4282424)。
* 當使用者從[!DNL Brand Portal]結尾接收「貢獻」檔案夾中的新資產後，嘗試將「貢獻」檔案夾從[!DNL Experience Manager]重新發佈至[!DNL Brand Portal]時，系統會引發例外(CQ-4279740)。
* 禁止在「貢獻」檔案夾（巢狀檔案夾）中建立「貢獻」檔案夾，以避免複雜性(CQ-4278391)。
* 系統上載從[!DNL Experience Manager]Admin Console導入的[!DNL Brand Portal]用戶清單（.csv檔案）時引發異常。 .csv檔案中只有「電子郵件」、「名字」和「姓氏」欄位是必填欄位(CQ-4278390)。

### 社群 {#communities-6530}

**修正**

* 社群管理員（群組管理員／網站管理員）看不到管理群組的快速連結（開啟／編輯／發佈／刪除群組）(NPR-31627)。
* 除非手動刷新／重新載入頁面，否則不會顯示已提交的部落格(NPR-31599)。
* 「提及次數」功能使用的JCR查詢區分大小寫，而且傳回結果需要太長時間(NPR-31475)。
* [!DNL Experience Manager] 6.5 UberJar檔案拋出異常， `cq-social-translation` 從 [!DNL Experience Manager] 6.5 UberJar檔案中遺失Bundle(NPR-31186)。
* Jackson Databind程式庫已更新至2.9.9.3版，以解決新的弱點(NPR-30967)。
* 活動與通知標題不一致 (NPR-30941)。
* 在[!DNL Communities]部落格中編頁無法正常運作(NPR-30914)。
* [!DNL Experience Manager]作者環境中未填入Analytics報表，會顯示空白頁面(NPR-30913)。

### Oak {#oak}

* Lucene索引更新導致作者伺服器速度變慢(NPR-31548)。

### 表單 {#forms-6530}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack不包含修正 [!DNL Experience Manager Forms]。它們是使用單獨的Forms附加套件傳送的。 此外，還發行了包含JEE上[!DNL Experience Manager Forms]修正的累積安裝程式。 如需詳細資訊，請參閱[安裝Experience ManagerForms附加元件](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package)和[在JEE上安裝Experience ManagerForms元件。](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer)

#### Forms 附加元件套件 {#forms-add-on-package-6530}

**調適型表單**

* 字串包含在本地化最適化表單時的字典鍵(NPR-31110)。

**互動式通訊**

* **MissingNode.toString()在將Jackson** 程式庫升級至2.10.0(NPR-31549)後傳回不正確的結果。

* 文字編輯器會從從Microsoft Word複製的文字中隨機移除空格字元(NPR-31113)。

**通信管理**

* 將字母從LiveCycleES4SP1遷移到[!DNL Experience Manager] 6.5時，不顯示標題和工具提示(NPR-31615)。

* **將字母儲存為草稿時，** 不會再顯示支援的文字流格式(NPR-30463)。

**工作流程**

* OSGi工作流程因CPU使用率100%而失敗(NPR-31233)。

**HTML5 表單**

* 新增子表單的例項時，產生 XDP 表單的 HTML5 預覽後出現閃爍畫面 (NPR-30909)。

#### FormsJEE安裝程式{#forms-jee-installer-6530}

**Forms - 文件服務**

* 在。NET專案中使用MTOM的SOAP web service會顯示AssemblerServiceClient叫用和HtmlToPDF2方法的例外(NPR-4281771)。

* AXIS 1.4 jar中發現的安全漏洞2012-5784和2014-3596，並修正了[AXIS1.4.1 jar](https://helpx.adobe.com/aem-forms/quick-fixes/6-5/jee-patch-0014.html)(NPR-31015)。

**Foundation JEE**

* 操作配置不載入調用Forms Workflow提交操作的進程名(NPR-31478)。

### 包含的 Feature Pack {#feature-packs-included-6530}

>[!NOTE]
>
>對於[!DNL Experience Manager Forms]客戶，在安裝[!DNL Experience Manager] Service Pack、Cumulative Fix Pack或Feature Pack後，必須安裝[!DNL Experience Manager Forms]附加套件。

#### Forms- Foundation JEE {#forms-foundation-jee-feature}

* [!DNL Experience Manager] Forms支援第18c號Oracle(NPR-29155)。

## Adobe Experience Manager6.5.2.0 {#experience-manager-6520}

[!DNL Adobe Experience Manager] 6.5.2.0是重要的發行版本，其中包括效能、穩定性、安全性，以及自2019年4月 [!DNL Adobe Experience Manager] 6.5正式推出以來所發佈的重要客戶修 **正和增強**。它可安裝在[!DNL Experience Manager] 6.5之上。

此Service Pack版本的一些主要亮點是：

* 內建存放庫 (Apache Jackrabbit Oak) 更新至 1.10.3 版。
* 已新增設定屬性，以允許將體驗片段直接匯出至[!DNL Adobe Target]的使用者定義工作區。
* 資產使用者可以搜尋視覺上類似的影像。 [!DNL Experience Manager]會顯示來自DAM儲存庫的智慧型標籤影像，這些影像類似於使用者選取的影像。請參閱[視覺搜尋](../assets/search-assets.md#visualsearch)。

* 增強「已連線資產」功能，以新增從遠端DAM部署擷取檔案的支援。 網站作者現在可以在Content Finder中搜尋及篩選支援的檔案類型。 遠端檔案可新增至網頁上的「下載」元件。 請參閱[使用已連接的資產](../assets/use-assets-across-connected-assets-instances.md)。

* EnhanceDocument類型篩選器，提供更多MIME類型，以支援多值選項。
* 為多資源支援引入外部「重新處理」工作流程。
* 使用複製的預設資產篩選器優化了[!DNL Dynamic Media]效能。
* 已回復DMS7的裁切／旋轉資產編輯選項。
* 已實作在VideoPlayer中載入時靜音視訊的選項。
* 修正以確保「資產UI」欄檢視僅顯示租用戶特定內容。
* 修正可讓樣式accordion變更反映在搜尋結果中。

### 資產

**產品增強功能**

* 增強「已連線資產」功能，以新增從遠端DAM部署擷取檔案的支援。 網站作者現在可以在Content Finder中搜尋及篩選支援的檔案類型。 遠端檔案可新增至網頁上的「下載」元件。 CQ-4270245 的 Hotfix. 請參閱[使用已連接的資產](/help/assets/use-assets-across-connected-assets-instances.md)。

* [!DNL Experience Manager Assets] 使用者可以搜尋外觀相似的影像。[!DNL Experience Manager]會顯示來自DAM儲存庫的智慧型標籤影像，這些影像類似於使用者選取的影像。請參閱[視覺搜尋](../assets/search-assets.md#visualsearch)。

**修正**

* ACP API生成的URL和資料夾元資料中的資產路徑不進行URL編碼。 GRANITE-26198:CQ-4271814的修補程式
* 無法使用[!DNL Experience Manager Assets]介面開啟包含名稱中具有百分比符號(%)的資料夾的歸檔檔案。 NPR-29989：CQ-4270467 的 Hotfix
* Touch UI:在管理出版物精靈中，會在貼文請求主體中的頁面之後新增參考，導致所有資產在頁面之後發佈，而當轉譯頁面時，發佈例項中的部分資產會遺失。 NPR-29985：CQ-4270724 的 Hotfix
* 取消關聯資產功能不適用於名稱中具有特殊字元（變成URI編碼的字元）的相關資產。 NPR-30387：CQ-4274446 的 Hotfix
* 在編輯內容片段時，會以錯誤的使用者建立版本。
* 在以租用戶為基礎的系統上建立系列時發生失敗。 NPR-30114：CQ-4272948 的 Hotfix
* 資產UI欄檢視並不尊重目前租用戶的dam根路徑，而是存取所有租用戶dam路徑。 NPR-30636：CQ-4275481 的 Hotfix
* 當您看到插入的影像時，可能會透過受限制的檔案警報視窗進行跨網站指令碼(XSS)攻擊。 NPR-30617：CQ-4270133 的 Hotfix
* 多租用戶：租戶保存資料夾屬性時，會同時觀察成功提示和錯誤消息，說明操作未成功，「無法編輯屬性」。 權限不足。」 因此，令他們困惑。 NPR-30545：CQ-4275333 的 Hotfix
* 資產選擇器對話框不允許選擇資產，因此無法使用相關來源取代功能來更新來源。 NPR-30502：CQ-4275029 的 Hotfix
* [!UICONTROL DAM更新] 資產流量——上傳大型mp4檔案時處於過時狀態。NPR-30480：CQ-4271352 的 Hotfix
* 「建立審閱任務」功能無法運作，因為空負載導致所有後續審閱任務相關操作失敗。 NPR-30468：CQ-4274263 的 Hotfix
* Adobe 智慧標記透過 Datapower 連線的問題。NPR-30026：CQ-4269457 的 Hotfix
* 「資產UI欄檢視」嘗試開啟離開邊欄的篩選時，會引發錯誤。 NPR-30501：CQ-4273862 的 Hotfix
* 在資產資料夾的「已關閉使用者群組」(CUG)屬性中新增與LDAP同步的群組時，不會儲存並擷取群組。 NPR-30615：CQ-4274689 的 Hotfix
* 篩選搜索樣式和方向欄位不會將自動完成的值應用於搜索查詢。 NPR-30620：CQ-4275724 的 Hotfix
* 名稱中包含空格和&quot;&amp;&quot;字元之資料夾的資產共用連結，會為某些資產顯示空白的灰色卡片。 NPR-30557：CQ-4270187 的 Hotfix
* 資料夾中繼資料結構表單不會自動偵測資料類型，因此不會在表單提交中建立相關的TypeHint。 NPR-30599：CQ-4275227 的 Hotfix
* 裁切和旋轉資產編輯選項會從DMS7編寫UI中停用。 NPR-30118：CQ-4273221 的 Hotfix
* 使用DMS7配置的[!DNL Experience Manager]實例無法使用共用連結功能。 NPR-30080、NPR-30492：CQ-4273651 的 Hotfix
* 將[!DNL Dynamic Media]-Scene7元件新增至頁面，然後發佈頁面並不會每次都觸發dmscene7組態。 NPR-30641：CQ-4275962 的 Hotfix
* 在[!DNL Experience Manager]中新增IPSJobJournal，為每個處理配置檔案僅建立一個入侵防護系統(IPS)作業。 NPR-30490：CQ-4273614 的 Hotfix
* [!DNL Dynamic Media]:新增預設篩選條件，排除資產不會複製至 [!DNL Experience Manager] 發佈節點。NPR-30538：CQ-4274678 的 Hotfix
* 引入外部「重新處理」工作流程，以支援多資源，以允許資料夾做為裝載。 工作流程有兩個步驟——透過中繼資料對應至下一個步驟，重新處理沒有控制代碼的資產，並在單一IPS工作中將所有沒有資產控制代碼的資產重新上傳至S7。 如需詳細資訊，請參閱設定[!DNL Dynamic Media]Cloud Services。 NPR-30489：CQ-4272903 的 Hotfix
* 在正確的CSV結束正確的CSV後，上傳錯誤的CSV。 CQ-4277694、CQ-4277814
* 要移除的貢獻資料夾專屬的圖示不正確。 CQ-4277580 的 Hotfix
* 在「資產貢獻」索引標籤的使用者選擇器中選取使用者時，使用者名稱不會出現在表格中，而「屬性」頁面上的「刪除使用者」對話方塊會顯示錯誤的文字。 CQ-4277875 的 Hotfix
* 使用者選取使用者並按一下「新增」，就無法將參與者從使用者選擇器新增至「資產貢獻」檔案夾。 CQ-4277824、CQ-4278087
* 按小寫搜索用戶名在用戶選擇器中不起作用。 CQ-4277958、CQ-4277930
* 非管理員可將資產發佈至資產貢獻資料夾的新資料夾。 CQ-4278200 的 Hotfix
* dam-user（非管理員）不能將參與者新增至「資產貢獻」檔案夾。 CQ-4278192 的 Hotfix
* 「建立」按鈕會顯示在「資產貢獻」檔案夾中。 CQ-4277560 的 Hotfix
* 依相關性排序搜尋查詢會傳回[!DNL InDesign]檔案以及[!DNL InDesign]範本。 CQ-4273864 的 Hotfix
* 如果使用者有大寫電子郵件ID，使用者將無法登入先前已登出的資產。 CQ-4276575 的 Hotfix
* 「刪除」操作僅適用於所選的預設集，如果螢幕在操作後自動刷新清單，則會顯示已刷新的其他預設集。 CQ-4261461 的 Hotfix
* 在[!DNL Dynamic Media]-Hybrid模式中設定[!DNL Dynamic Media]Cloud Services會產生在[!DNL Analytics]中建立的多個空報表套裝，而且沒有在[!DNL Experience Manager]中儲存報表套裝ID，導致報表套裝重複。 CQ-4249780 的 Hotfix
* 將[!DNL Experience Manager]資產中的操作更名為重複名稱失敗，無法與Scene7同步。 CQ-4276763 的 Hotfix
* 使用者產生的內容會在搜尋篩選面板中錯誤顯示。 CQ-4273875 的 Hotfix
* TIFF影像無法使用「尋找類似項目」選項。 CQ-4278238 的 Hotfix
* 在VideoPlayer中載入時將視訊靜音的實作選項。 CQ-4266465 的 Hotfix
* 檢視器- VideoViewer:poster=none在使用外部視訊時運作不正確。 CQ-4265536 的 Hotfix
* 在IE11和MS Edge瀏覽器上播放視訊時，會顯示等待圖示。 CQ-4251539 的 Hotfix
* 3.8 SDK和5.13檢視器README檔案未更新，且包含舊版資訊。 CQ-4273737 的 Hotfix
* 內容片段在儲存變更之前即會更新版本。 NPR-30616：CQ-4273088 的 Hotfix
* 在縮圖處理中，以Asset#getMetadataValueFromJcr(String)取代Asset#getMetadata(String)。 NPR-30491：CQ-4273067 的 Hotfix
* 上傳jpg會導致訊息出現多個例項：對每個資產執行「ReplicateOnModifyWorker Replicating UPDATED 」操作，導致效能降級。
* 使用「解壓縮封存檔」功能解壓縮郵遞區號檔案會導致檔案夾名稱在其標題中包含百分比(%)的問題。 NPR-29990：CQ-4270467 的 Hotfix

### 網站 {#sites-6520}

* 如果LiveCopy繼承中斷，即時副本頁面會顯示語言副本連結，而非LiveCopy連結(NPR-30980)。
* 對於新的Blueprint，如果記錄數超過40，則只會顯示前40個記錄。 Blueprint會為其餘的記錄顯示空白行(NPR-31182)。
* 文本元件的富格文本編輯器(RTE)插件顯示日文和韓文文本的扭曲字元(NPR-31331)。
* 富格文本編輯器(RTE)不允許將嵌入的表作為清單項插入(NPR-30879)。
* 立即可用的架構Rich Text Editor(RTE)會意外地套用內嵌字型大小至元素(NPR-31284)。
* 當使用者專注在左側欄位並使用鍵盤快速鍵貼上內容時，會貼上頁面編輯器剪貼簿的內容，而非從左側欄位複製的內容(NPR-31172)。
* 當用戶將「檔案上傳」欄位添加到多欄位時，影像路徑儲存在元件節點中，而不是多欄位節點(NPR-30882)。
* `ResponsiveGridExporter` API不會傳回`com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter`介面。 `com.day.cq.wcm.foundation.model.impl`軟體包聲明為專用軟體包(NPR-31398)。
* 當在非編輯器模式（在「作者」中不含`editor.html`前置詞和`wcmmode=disabled`，或在「發佈者」中）開啟包含某些「體驗片段」的頁面時，請求會以HTTP狀態錯誤碼500(NPR-30743)結束。

### WCM - 頁面編輯器 {#wcm-page-editor-6520}

**產品增強功能**

* EnhanceDocument類型篩選器，提供更多MIME類型，以支援多值選項。 CQ-4270694 的 Hotfix

### 內容片段管理{#content-fragment-management-6520}

* 內容片段模型UI使用的查詢速度非常慢，最終導致錯誤。 CQ-4270807 的 Hotfix

### UI - Foundation {#ui-foundation}

* 捷徑觸發器，可防止使用者在特定使用者介面中使用&#39;m&#39;、&#39;p&#39;、&#39;e&#39;。 NPR-30355：GRANITE-26346 的 Hotfix
* 關閉[!DNL Experience Manager Assets]搜尋UI不會將左側邊欄重設為「內容」選項，防止使用者隨後第二次開啟篩選邊欄。 NPR-30509：CQ-4274716 的 Hotfix
* 多租用戶環境：[!DNL Experience Manager Assets] UI頂端導覽無法使用，並發生JavaScript錯誤。 NPR-30104：GRANITE-26344 的 Hotfix

### 轉換 {#translation-6520}

* 翻譯問題——使用機器翻譯只能翻譯一些元件。 NPR-30079：CQ-4273764 的 Hotfix

### 平台 {#platform-6520}

* [!DNL Experience Manager] 預設郵件發送者無法通過TLS v1.2向遠程SMTP伺服器發送郵件。NPR-30476:GRANITE-26605的修補程式

### 專案 {#projects-6520}

* dam:folderThumbnailPaths值即使刪除資料夾中的資產，也不會重新整理並顯示舊的縮圖。 NPR-30424：CQ-4273667 的 Hotfix
* 完成「移動」選項時，資產的「標題」和「名稱」保持不變。 NPR-30647：CQ-4276265 的 Hotfix

### 社群 {#communities-6520}

* 用戶同步診斷完全中斷，無法正常工作。 NPR-30004、NPR-29943：CQ-4270287、CQ-4271348 的 Hotfix

### Sling {#sling}

* 從6.3.3.2升級到6.5的實例會導致OSGi配置重複。 NPR-30130：CQ-4274016 的 Hotfix

### 整合

* 在重新啟動執行個體之前，自訂內容無法正確顯示在發佈執行個體上。 NPR-30377：CQ-4273706 的 Hotfix
* 在網站上設定啟動時，程式庫位址會加上斜線(/)，導致每次手動干預。 NPR-30694：CQ-4275501 的 Hotfix

### 表單 {#forms-6520}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack不包含修正 [!DNL Experience Manager Forms]。它們是使用單獨的[!DNL Forms]附加軟體包傳遞的。 此外，還發行了包含JEE上[!DNL Experience Manager Forms]修正的累積安裝程式。 如需詳細資訊，請參閱[安裝Experience ManagerForms附加元件](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package)和[在JEE上安裝Experience ManagerForms元件。](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer)

[!DNL Experience Manager] 6.5.2.0表格的主要亮點是：

* 在`PDFFormRenderOptions` API中為[!DNL Experience Manager]FormsOSGi的`RenderAtClient`新增「自動」設定。

#### Forms 附加元件套件

**後端整合**

* 無法使用AWS托管的負載平衡URL配置表單資料模型。 NPR-30123：CQ-4273359 的 Hotfix
* 使用Web服務定義語言(WSDL)建立表單資料模型(FDM)時，返回錯誤消息`Caused by: com.adobe.aem.dermis.exception.DermisException: java.lang.Exception: Unable to handle content type`:NPR-30477:CQ-4272921的修補程式

**通信管理**

* 「建立對應UI(CCR UI)轉譯會間歇性失敗，主控台發生以下錯誤：
   `- Uncaught Error: variable [object Object]is already known the letter`- NPR-30127

**互動式通訊**

* 表單資料模型中標示為必填的欄位，會依「建立對應UI」(CCR UI)的要求顯示。 NPR-30623：CQ-4274902 的 Hotfix

**Forms - 工作流程**

* 「監看資料夾」上未映射的輸出變數會導致呼叫失敗。 CQ-4264451 的 Hotfix

**HTML5 表單**

* 第二次部署自訂程式碼或專案時，頁面不會呈現，並發生下列錯誤：

   `org.apache.sling.scripting.sightly.SightlyException.`

   NPR-30539：CQ-4272509 的 Hotfix

* 以瀏覽模式使用 NonVisual Desktop Access 來讀取 HTML5 表單時，Chrome 瀏覽器在表單設計中的每個可縮放向量圖形 (SVG) 之前讀到「graphic」。NPR-30449：CQ-4274732 的 Hotfix

#### FormsJEE安裝程式

**Forms - 文件安全性**

* 套用具有時間戳記的簽名失敗，並出現錯誤：ALC-DSC-003-000:com.adobe.idp.dsc.DSCIndisignationException:調用錯誤。 NPR-30820：CQ-4275852 的 Hotfix

**Forms - 文件服務**

* 如果&quot;SubmitURL&quot;包含&amp;符號，則當對轉譯pdf servlet提出POST請求時，在記錄檔中會出現解析錯誤。 NPR-30865：CQ-4278232 的 Hotfix

**Forms- Foundation JEE**

* HTMLtoPDF服務在JMX主控台中不會顯示maxReuseCount。 NPR-30134、NPR-30304：CQ-4273763 的 Hotfix
* 從[!DNL Experience Manager Forms] Workbench叫用web services，新增或編輯Web服務連線會引發錯誤：ClassNotFoundException org.apache.axis.message.SOAPBodyElement。 NPR-30105：CQ-4273217 的 Hotfix

### 包含的 Feature Pack

>[!NOTE]
>
>對於[!DNL Experience Manager Forms]客戶，在安裝[!DNL Experience Manager] Service Pack、Cumulative Fix Pack或Feature Pack後，必須安裝[!DNL Experience Manager Forms]附加套件。

#### 網站 {#sites-feature-packs-included}

* 已新增設定屬性，以允許將體驗片段直接匯出至[!DNL Adobe Target]的使用者定義工作區。 NPR-29189：CQ-4249782 的 Hotfix

#### Forms - 文件服務 {#forms-document-services-1}

* 在`PDFFormRenderOptions` OSGi的API中，將「自動」設定新增至`RenderAtClient`。 [!DNL Experience Manager Forms]NPR-30759：CQ-4278193 的 Hotfix

## Adobe Experience Manager6.5.1.0 {#experience-manager-6510}

[!DNL Adobe Experience Manager] 6.5.1.0是重要的發行版本，其中包括效能、穩定性、安全性，以及自2019年4月 [!DNL Adobe Experience Manager] 6.5全面上市以來所發行的重要客戶修 *正和增強。* 它可安裝在 [!DNL Experience Manager] 6.5之上。

此Service Pack版本的一些主要亮點是：

* 啟用動態UI狀態在追蹤事件時的自訂屬性。
* 包含支援以[!DNL Dynamic Media]-Scene7模式傳送360度視訊資產。
* 透過Rich Text Editor的樣式外掛程式，啟用&#x200B;*日文繞圖排文功能。*&#x200B;如需詳細資訊，請參閱[設定日文換行字詞](/help/sites-administering/configure-rich-text-editor-plug-ins.md#jpwordwrap)

### 資產

* 更新 DAM DMGateway 介面以提供 S3 多部分支援。NPR-29740：CQ-4226303 的 Hotfix
* 轉譯預覽在升級至[!DNL Experience Manager] 6.5後會產生`Only empty tenantId is currently supported`錯誤。NPR-29986:CQ-4272353的修補程式
* 不會顯示「刪除」對話框以允許刪除作業。 NPR-29720：CQ-4271074 的 Hotfix
* 在屬性頁面中新增資產標題後，當使用者嘗試關閉頁面時，[!DNL Experience Manager]會再次開啟屬性頁面。 NPR-29627：CQ-4264929 的 Hotfix
* VersioningTimelineEventProvider應提供根版本和類型為nt的節點：版本。 GRANITE-26063的修補程式
* 已實作在[!DNL Experience Manager] DM-Scene7模式下上傳和播放360個球形視訊的功能。 CQ-4265131 的 Hotfix
* 如果編輯了源，即時副本將檢索不正確的狀態。 CQ-4265451 的 Hotfix
* 已啟用[!DNL Experience Manager Assets]的多站點管理器支援。 CQ-4271453、CQ-4268621、CQ-4257491的修補程式
* [!DNL Experience Manager] 介面應在時間軸歷程記錄中顯示資產目前版本的額外項目，並顯示最新的登入註解 [!DNL Adobe Asset Link]。CQ-4262864 的 Hotfix
* 內容片段時間軸在遺失屬性時顯示錯誤訊息。 CQ-4272560 的 Hotfix
* Scene7視訊播放器展開為全螢幕時的問題。 CQ-4266700 的 Hotfix
* ZoomVerticalViewer:如果使用單一影像資產，則不應顯示平移按鈕。 CQ-4264795 的 Hotfix
* 刪除即時副本中的子節點應分離liveRelationship。 CQ-4270395 的 Hotfix
* 中繼資料結構只包含全域設定中的項目，且遺失作用中租用戶中的項目。 formPath URL值即使在變更時也會回復為預設值。 NPR-29945：CQ-4262898 的 Hotfix
* 將影像預設集發佈至[!DNL Brand Portal]失敗，並顯示500錯誤碼。 NPR-29510：CQ-4268659 的 Hotfix

### 網站

* 在轉出期間，空屬性和多個屬性不會從Blueprint傳播。 使用Blueprint重設即時副本無法用於元件。 NPR-29253：CQ-4264928、CQ-4264926、CQ-4267722 的 Hotfix
* CoralUI搭配`Multifield`使用時，會將`fileReferenceParameter`儲存在元件層級，而非多欄位層級。 NPR-29537：CQ-4266129 的 Hotfix
* 將[!DNL Experience Manager]文字元件和文字編輯器增強為日文。 NPR-29785：CQ-4265090 的 Hotfix
* 使用「時間彎曲」還原的頁面，應參照版本修訂時的正確圖片。 NPR-29431：CQ-4262638 的 Hotfix
* 樣式系統節點從父節點繼承到子節點的問題。 NPR-29516：CQ-4270330 的 Hotfix
* 將社交貼文設定為[!DNL Facebook]驗證時發出錯誤訊息。 NPR-29211：CQ-4266630 的 Hotfix
* 「內容片段」上轉譯的縮圖會顯示「日期」和「時間」欄位的內部日曆表示法。 NPR-29531：CQ-4269362 的 Hotfix
* 在Coral2實作中開啟權限標籤時，不會顯示按鈕。 CQ-4269419 的 Hotfix

### 商務

* 執行電子商務的延遲內容移轉時，ConstraintViolationException。 NPR-29247：CQ-4264383 的 Hotfix

### 內容片段管理

* 開啟包含美元`($)`和大括弧`({)`字元的內容片段時發生解析錯誤。 CQ-4270266 的 Hotfix

### 體驗片段

* 將[!DNL Experience Manager]體驗片段匯出至[!DNL Adobe Target]。 CQ-4265469 的 Hotfix
* 使用智慧型影像匯出至目標的體驗片段失敗。 CQ-4269606 的 Hotfix

* 當使用者嘗試在資訊卡檢視中透過Omnisearch移動體驗片段時，會觸及到死衚衕。 CQ-4263848 的 Hotfix

### WCM - 頁面編輯器

* 使用無效的選擇器時出現反射型跨網站指令碼 (XSS)。CQ-4270397 的 Hotfix

### 複寫

* `cq/replication/components/agent` 元件中，使用者提供的資料沒有在輸出上逸出，導致儲存型跨網站指令碼 (XSS) 漏洞。CQ-4266263 的 Hotfix

### 工作流程

* 對話框參與者的日曆選擇器欄位已損壞。 NPR-29727：CQ-4270423 的 Hotfix

### WCM —— 編SPA輯器

* 已啟用從遠程端點提取預呈現內容。 CQ-4270238 的 Hotfix
* 開啟轉譯為伺服器端的「范SPA本頁面」時，記錄檔中的警告。 CQ-4270238 的 Hotfix

### WCM - MSM

* 升級至[!DNL Experience Manager] 6.4.3讓多網站管理員需要很長時間才能推出。 CQ-4271410 的 Hotfix

### 整合

* BrightEdge憑據失敗，出現連線錯誤。 NPR-29168：CQ-4265872 的 Hotfix

* 嘗試編輯並保存[!DNL Experience Manager]啟動配置時，將顯示例外消息。 NPR-29176：CQ-4265782/CQ-4266153 的 Hotfix

### 使用者介面

* 新增支援在追蹤基礎追蹤API中特定事件時，將dynamic-UI-states追蹤為自訂屬性。 GRANITE-26283的修補程式
* 無法在提交按鈕上設定追蹤功能。 GRANITE-26326的修補程式
* 精靈無法在提交按鈕上設定追蹤功能。 NPR-29995、NPR-30025：CQ-4264289 的 Hotfix

### 社群

* 無法在成員配置檔案頁面上的下拉菜單中對齊新標章。 NPR-29381：CQ-4267987 的 Hotfix
* 沒有協調者權限的訪客和成員可以透過貼上URL來查看未核准／待審貼文。 NPR-29724：CQ-4271124、CQ-4271441 的 Hotfix
* 觀察到使用者登入 Community 時出現 40-50 秒的長回應時間。NPR-29677：CQ-4269444 的 Hotfix

### 複寫

* 複寫代理元件疑似為漏洞，向未獲授權的使用者洩漏了敏感資訊。NPR-29611：GRANITE-25070 的 Hotfix

* 在OAuth期間，每次複製至[!DNL Brand Portal]的作業階段都會洩漏。 NPR-30001：GRANITE-26196 的 Hotfix

### 專案

* 從[!DNL Experience Manager] Author /content/dam/mac資料夾發佈[!DNL Experience Manager Assets]至[!DNL Brand Portal]無法運作。 NPR-29819：CQ-4271118 的 Hotfix

### 平台

* HtmlLibraryManager會在快取失效時刪除crx-quickstart的所有內容。 NPR-29863：GRANITE-26197 的 Hotfix

### Felix

* 使用Java11時，系統控制台中不會顯示「記憶體使用量」詳細資訊。 NPR-29669

### 表單

[!DNL Experience Manager Forms] 6.5.1.0的主要亮點是：

* 僅限OSGi:在「輸出」和「Forms服務」中新增`PAGECOUNT`屬性。

* 僅限OSGI:啟用支援，以使用Forms服務建立靜態PDF檔案。
* 為管理員和根用戶啟用對XMLForm.exe的權限。
* 已啟用ADFS v3.0對Dynamics內部部署整合的支援。

#### Forms 附加元件套件

**後端整合**

* 擷取受保護的網站服務定義語言(WSDL)時失敗。 NPR-29944：CQ-4270777 的 Hotfix
* 當[!DNL Experience Manager Forms]安裝在IBM WebSphere上時，基於SOAP建立表單資料模型失敗。 CQ-4251134 的 Hotfix
* 已針對Microsoft Dynamics內部部署整合啟用Active Directory Federation Services(ADFS)v3.0支援。 CQ-4270586 的 Hotfix
* 當資料來源的標題變更時，表單資料模型不會顯示更新的標題。 CQ-4265599 的 Hotfix
* 如果實體或屬性的名稱包含連字型大小或空格，表達式將無法計算此類實體和屬性。 CQ-4225129 的 Hotfix

* 原始字串輸出中出現冒號時，會出現錯誤的輸出。 CQ-4260825 的 Hotfix

* 即使REST API輸出中預期沒有內容，表單資料模型的叫用操作也會引發錯誤。 CQ-4268828 的 Hotfix

**調適型表單**

* 無法在延遲載入期間在最適化表單片段中新增例項。 NPR-29818：CQ-4269875 的 Hotfix
* 驗證元件不記錄或顯示記錄文檔模板的任何錯誤。 CQ-4272999 的 Hotfix
* 新增支援，可停用最適化Forms的版面編輯器。 CQ-4270810 的 Hotfix
* 已恢復[!DNL Experience Manager] 6.5中最適化Forms的驗證步驟。CQ-4269583的修補程式

* 最適化表單欄位驗證失敗中斷[!DNL Adobe Sign]。 CQ-4269463 的 Hotfix
* 當[!DNL Experience Manager Forms]例項包含20個以上的最適化表單片段，且所有表單片段的名稱都以相同字串開頭時，搜尋不會傳回或只傳回最近20個建立的片段。 CQ-4264414、CQ-4264914

* Adaptive Forms應用程式與大型資料集搭配使用時的效能問題。. CQ-4235310 的 Hotfix

* 透過發佈例項上的匿名帳戶存取時，GuideRuntime指令碼無法載入。 CQ-4268679 的 Hotfix

**Forms -互動式通訊**

* 「互動式通訊」範本不會在允許的元件清單中列出頁首和頁尾元件。 CQ-4237895 的 Hotfix
* 當您建立包含影像欄位的互動式通訊列印範本時，圖表的標題會設為空白。 CQ-4264772 的 Hotfix
* 圖表的線條顏色在刪除時設為未定義。 CQ-4264762 的 Hotfix
* 在「檔案片段」上所做的版面圖層變更，在執行保持同步的變更時會消失。 CQ-4266054 的 Hotfix
* 綁定到文本欄位的「文檔片段」中的表單資料模型元素不顯示繼承表徵圖並允許綁定。 CQ-4261089 的 Hotfix
* 列印頻道演算API沒有將資料作為參數傳入API的選項。 CQ-4263540 的 Hotfix
* 當系結類型從「字串」欄位／變數的「文字片段」變更為「無／資料模型物件」時，「由代理編輯」核取方塊會取消勾選，因此不會顯示代理設定。 CQ-4261953 的 Hotfix
* 在提交代理UI時，產生的Web資料json檔案會儲存繼承取消未系結欄位的資訊。 CQ-4265621 的 Hotfix

**Forms - 工作流程**

* 從最適化表單應用程式的外框重新送出表單時，會造成資料遺失。 NPR-28345：CQ-4260929 的 Hotfix
* 針對非變數案例儲存時，不會關閉檔案。 CQ-4269784 的 Hotfix
* 最適化Forms應用程式已放棄對Microsoft Windows 8.1的支援。CQ-4265274的修補程式
* 當超過2 MB的影像附加為[!DNL Experience Manager Forms]應用程式Android版表單的欄位層級附件時，應用程式會當機。 CQ-4265578 的 Hotfix

* 為「指派」任務中的「互動式通信打印通道」啟用預填充選項。 CQ-4265577 的 Hotfix
* 在用戶成為分配了該任務的組的成員之前，他們無法查看共用任務。 CQ-4248733 的 Hotfix
* 在Windows上，在Adaptive Form應用程式上儲存或送出JEE應用程式會遭到封鎖。 CQ-4268704 的 Hotfix
* 與表單資料模型變數相關聯的表單資料模型不可見。 CQ-4266554 的 Hotfix
* 不支援使用變數支援的檔案簽署狀態變數。 CQ-4266312 的 Hotfix
* 從工作區提交時，無法顯示變母字元。 CQ-4263172 的 Hotfix
* 在升級的設定中，如果開啟工作流程進行編輯，在監看資料夾使用者介面(UI)中會顯示錯誤，而非工作流程名稱。 CQ-4238579 的 Hotfix

**表單 - 管理**

* 上傳xsd或schema.json以外的副檔名時，不會上傳，且不會產生錯誤訊息。 CQ-4266716 的 Hotfix

**Forms-通信管理**

* [!DNL Experience Manager Forms] 6.5建立對應UI(CCR UI)無法開啟使用 [!DNL Experience Manager Forms] 6.3建立的對應。CQ-4266392的修補程式
* 如果DDE資料類型為類型編號，則XDP中的Sum函式不起作用。 CQ-4227403 的 Hotfix
* 要更新的記憶體中字母快取失效邏輯，因為當資產發佈時，其上次修改的時間不會更新。 CQ-4250465 的 Hotfix
* 無法發佈檔案片段、DD和字母。 CQ-4272893 的 Hotfix

#### FormsJEE安裝程式

**PDF 產生器**

* 64位元JDK無法將CAD檔案轉換為PDF。 NPR-29924、NPR-29925：CQ-4272113 的 Hotfix
* 已取代PhantomJS至WebToPDF的名稱，以進行HTML至PDF轉換。 NPR-29933：CQ-4234545 的 Hotfix
* 將郵遞區號檔轉換為PDF時產生錯誤。 CQ-4268628 的 Hotfix

**Forms-設計師**

* 當對使用[!DNL Experience Manager Forms Designer]建立的靜態PDF執行完整的協助工具檢查時，「主要語言」檢查會因語言屬性遺失而失敗。 CQ-4272923、CQ-4271002

**Forms - 文件安全性**

* 使用硬體安全性模組(HSM)的數位簽章無法在Java 11和Java 8的OSGi Linux上運作。 NPR-29838：CQ-4270441 的 Hotfix
* 具有硬體安全模組(HSM)的數字簽名在JEE Linux和所有受支援的應用程式伺服器（如JBoss和Websphere）上無法運行。 NPR-29839：CQ-4266721 的 Hotfix
* 使用PDF進階電子簽名(PAdES)驗證PDF中的簽名會產生InvalidOperationException。 NPR-29842：CQ-4244837 的 Hotfix
* 新增Document Security Extension對Office 2019的支援\。 CQ-4254369、CQ-4259764

**Forms - 文件服務**

* PDF無法轉換為「表單」欄位的PDF/A-1b，沒有外觀規定。 NPR-29940：CQ-4269618 的 Hotfix

* OSGi:無法確定在渲染期間生成的頁數。 NPR-28922：CQ-4270870 的 Hotfix
* 已啟用[!DNL Experience Manager Forms OSGi]中使用Forms服務的靜態PDF檔案支援。 NPR-28572：CQ-4270869 的 Hotfix
* 無法更改XMLForm.exe的權限。 NPR-29828、NPR-29237:Q-4267080的修補程式
* 由[!DNL Experience Manager Forms]伺服器輸出模組建立的靜態PDF不會以所建立檔案的語言填入語言屬性／標籤。 NPR-27332：CQ-4271002 的 Hotfix

**Forms- Foundation JEE**

* 在最終對象中無法使用pdfg_srt會導致安裝程式失敗。 NPR-29854：CQ-4270137 的 Hotfix
* LCBackupMode.sh無法運作。 NPR-29840：CQ-4269424 的 Hotfix
* 應從WebSphere的用戶介面(UI)中刪除UDP埠引用。 CQ-4264782 的 Hotfix

### 包含的 Feature Pack

#### 資產——包含

* 已啟用[!DNL Experience Manager Assets]的多站點管理器支援。 如需詳細資訊，請參閱[使用MSM重複使用資產以Experience Manager資產](https://docs.adobe.com/content/help/en/experience-manager-65/assets/using/reuse-assets-using-msm.html)。 NPR-29199：CQ-4259922 的 Hotfix

#### 網站——隨附

* 將[!DNL Experience Manager]體驗片段匯出至[!DNL Adobe Target]。 如需詳細資訊，請參閱[體驗片段連結重新寫入器提供者- HTML](https://helpx.adobe.com/experience-manager/6-5/help/sites-developing/experience-fragments.html#TheExperienceFragmentLinkRewriterProviderHTML)。 CQ-4265469 的 Hotfix

#### Forms-檔案服務——已包含

* 僅限OSGi:在「輸出」和「Forms服務」中新增屬性PAGECOUNT。 NPR-28922：CQ-4270870 的 Hotfix
* 僅限OSGi:啟用支援，以使用Forms服務建立靜態PDF檔案。 NPR-28572：CQ-4270869 的 Hotfix
* 為管理員和根用戶啟用對XMLForm.exe的權限。 NPR-29237：CQ-4267080 的 Hotfix

### OSGi組合和內容套件

以下文本文檔列出了[!DNL Experience Manager] 6.5.1.0中包含的OSGi組合和內容包

[!DNL Experience Manager] 6.5.1.0中包含的OSGi捆綁包清單

[取得檔案](assets/6_5-bundle-list.txt)

[!DNL Experience Manager] 6.5.1.0內容包清單

[取得檔案](assets/6_5-content-package-list.txt)
