---
title: Adobe Experience Manager 6.5 Service Pack 5的新增功能
description: Adobe Experience Manager 6.5 Service Pack 5的新增功能
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: b2b8178f96d1e0a551a58ba649443aa03f0608ac
workflow-type: tm+mt
source-wordcount: '1849'
ht-degree: 1%

---


# Adobe Experience Manager 6.5 Service Pack 5的新增功能 {#aem-whats-new-service-pack-5}

Adobe Experience Manager 6.5服務套件每季提供新功能、客戶要求的增強功能以及效能、穩定性和安全性改進。 每季的上市情況讓您輕鬆存取和採用新功能和創新。

本文重點介紹最新6.5 Service Pack中的功能、 [舊版6.5 Service Pack中的主要功能](#key-features-previous-service-packs)，以及Experience Manager 6.5.4.0版以來的 [部分主要版本](#key-releases-since-last-sp) 。

## Adobe Experience Manager Sites {#aem-sites}

### 協助工具改進 {#accessibility-sites}

* 透過新增文字資訊，改善錯誤報告。

* 已改善鍵盤導覽期間的使用者介面焦點。

* 已改善各種使用者介面元素的對比度。

* 已改善頁面影像的alt屬性一致性。

* 已改善可存取Rich Internet Applications(ARIA)標籤的一致性。

* 已改善非視覺化案頭存取(NVDA)功能。

* 已改善螢幕閱讀器支援。

### 其他重要增強功能 {#other-enhancements-sites}

* 複製或貼上頁面樹時，現在可以選擇貼上根頁面或貼上根頁面和樹的子頁面。

* [!DNL Adobe Experience Manager Experience Fragments] 匯出至工 [!DNL Adobe Target] 作區的選件類型和選件來源現在會顯示在 [!DNL Target]中。

* 多網站管理器——如果從來源頁面刪除元件，「發佈」觸發器現在會從發佈頁面刪除元件。

* 多網站管理員——當即時副本中的本機元件名稱與 [!UICONTROL Blueprint中的元件名稱相同，且元件從Blueprint中推出時，現在]`_msm_moved` ,詞語會新增至本機元件的名稱。

## [!DNL Adobe Experience Manager Assets] {#aem-assets}

### 協助工具增強功能 [!DNL Assets] {#assets-accessibility}

[!DNL Experience Manager Assets] 現在可依照網頁內容協助工具准則(WCAG)更容易存取。 協助工具已改善，因為下列增強功能：

* 許多使用者介面元素、控制項、頁面和對話方塊都適合螢幕閱讀程式。

* 許多使用者介面元素、控制項和輸入表單欄位都可使用鍵盤存取。

* 更新某些使用者介面元素的色彩和對比度，以便視覺有限的使用者或沒有色彩感知的使用者能夠區分這些使用者介面元素。 例如，星號分級圖示的顏色(例如在資產屬性( [!UICONTROL Properties] )或卡片檢視( [!UICONTROL Advanced Tab)的「分級(Rating] )」區段中)會變更，以取得適當的對比。

   ![對比度改善的分級圖示](assets/star-rating-icons.png)

### 增強的例外處理 {#exception-handling}

[!DNL Assets] 用戶介面流具有更好的異常處理。 如果資產的維度沒有類型，則會在日誌檔案中記錄觀察到的異常。

### 支援 [!DNL Dynamic Media] {#support-for-3d}

支援中的3D影像， [!DNL Dynamic Media] 讓客戶可以發佈3D內容，並將之新增至網頁和應用程式。 支援包括：

* 發佈常用的3D資產格式，並產生可用於網頁和其他應用程式的資產URL。

* 由3D網頁檢視器提供支援， [!DNL Adobe Dimension]以互動方式檢視已發佈的3D資產。

* 使用WCM元件，在頁面上發 [!DNL Experience Manager Sites] 布及檢視常用 [!DNL Sites] 的3D資產。

## Adobe Experience Manager Forms {#aem-forms}

### 自訂Adobe Experience Manager收件匣欄 {#customize-aem-inbox-columns}

您可以自訂收件 [!DNL Experience Manager] 匣以變更欄的預設標題、重新排序欄位，並根據工作流程的資料顯示其他欄位。 成員 `administrators` 或 `workflow-administrators` 組可以自定義列。

![自訂Experience Manager收件匣欄](assets/customize-columns.gif)

### 將互動式通訊儲存為草稿 {#save-as-draft}

您可以使用Agent UI為每個「互動式通訊」儲存一或多個草稿，並稍後擷取草稿以繼續處理。 您可以為每個草稿指定不同的名稱以加以識別。

![另存為草稿](assets/save-as-draft.gif)

### [!DNL Oracle WebLogic] 應用程式伺服器支援 {#weblogic-support}

Adobe Experience Manager Forms已新增對JEE上 [!DNL Oracle WebLogic 12] Adobe Experience Manager Forms的支援。 您可以從舊版升級，或在 [!DNL Oracle WebLogic] 12.2.1.4和更新版本的JEE伺服器上設定新的Experience Manager 6.5 Forms。 稍後的版本會與次要版本變更相對應，其中12.2.1.x中的x會以版本號碼取代。

### 協助工具改進 {#accessibility-improvements}

Adobe Experience Manager Forms包含下列協助工具增強功能：

* 當使用者將最適化表單預覽為HTML表單時，「塗鴉 [!UICONTROL 簽名] 」欄位會保留標籤焦點。

* 提交最適化表單時顯示的錯誤訊息現在包含 `aria-describedBy` 屬性。 屬性會附加至錯誤訊息中參考的欄位。 該 `aria-describedby` 屬性表示描述對象的元素的ID。 它有助於建立介面工具集或群組與描述它們的文字之間的關係。

* 如果最適化表單有某些必填欄位，則ARIA無障礙環境支援架構中的 `True` 此類欄位必填屬性會設定為。

### X-509憑證式驗證，適用於表單資料模型中以SOAP為基礎的Web服務 {#x509-based-authentication-soap}

表單資料模型現在支援X-509憑證式驗證，同時使用SOAP web services做為資料來源。

### 其他主要改進 {#other-improvements}

* JEE Document Security上的Experience Manager 6.5 Forms現在是以為基礎 [!DNL Apache Struts 2]。

* 新增對的支 [!DNL Oracle Real Applications Cluster (RAC) 19c]援。

## 舊版Experience Manager 6.5 Service Pack的主要功能 {#key-features-previous-service-packs}

### Experience Manager Sites {#aem-sites-previous-service-packs}

#### 樣式系統增強功能(6.5.4.0) {#style-system-enhancements}

現在，您可以使用增強的「樣式系統」(Style System)在元件對話框中選取樣式。

#### 不同領域的效能改進(6.5.4.0) {#performance-improvements}

* 縮短在網站(`contexthub.kernel.js`)中載入和初始化ContextHub的時間。 這可縮短網站瀏覽時的頁面載入時間。

* 縮短拖曳至頁面編輯器後重新整理頁 [!DNL Experience Fragments] 面的 [!DNL Sites] 時間。

* 縮短「即時副本概述」中 [!DNL Sites] 包含超過200個即時副本之頁面的登 **[!UICONTROL 入時間]**。

* 已改善URL不完整或無效的處理。 此類URL會拖慢範本編輯器的速度。

### [!DNL Adobe Experience Manager Assets] {#aem-assets-previous-service-packs}

#### 配 [!DNL Experience Manager Assets] 置 [!DNL Brand Portal] 為(6.5.4.0) {#configure-assets-bp}

和之間的授 [!DNL Experience Manager Assets] 權通 [!DNL Brand Portal] 道已更改。 之前， [!DNL Brand Portal] 是透過舊版OAuth閘道在傳統使用者介面中設定，該閘道使用JWT代號交換來取得IMS存取代號以進行授權。 [!DNL Experience Manager Assets] 現在已透過Adobe [!DNL Brand Portal] I/O設定，Adobe會購買IMS Token以取得您的租用戶授 [!DNL Brand Portal] 權。

使用配置的步 [!DNL Experience Manager Assets] 驟會 [!DNL Brand Portal] 因您的版本、您是第 [!DNL Experience Manager] 一次進行配置還是升級現有配置而有所不同。 如需詳 [細資訊，請參閱設定Experience Manager資產與品牌入口](https://docs.adobe.com/content/help/zh-Hant/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html) 。

#### 協助工具增強功能(6.5.4.0) {#accessibility-enhancements}

[!DNL Experience Manager Assets] 包含下列協助工具增強功能：

* 鍵盤上的箭頭鍵可用來移動和平移縮放影像中的區域。 如需詳細資訊，請參閱 [僅使用鍵盤按鍵預覽資產](../assets/managing-assets-touch-ui.md#previewing-assets)。

* 「篩選器」面板中的混合狀態複選框（除非您選擇了所有嵌套的謂詞，否則不會選擇並刪除第一級複選框）由螢幕閱讀器讀取。

* 日期和時間格式約束在日期欄位的欄位標籤中提供，使用戶能夠使用鍵盤以正確的格式輸入日期。 For example, `On Time (MM-DD-YYYY HH:mm)`. 其中MM是兩位數格式的月份，YYYY是年份，DD是兩位數格式的日，HH是24小時軍用格式的小時，而mm是分鐘。

* 螢幕閱讀程式 `X` 會宣佈符號，以移除選取的標籤和選取的標籤數。

#### 視覺搜 [!DNL Adobe Experience Manager Assets] 尋(6.5.2.0) {#visual-search}

[!DNL Assets] 使用者可以搜尋外觀相似的影像。 Experience Manager會顯示來自DAM存放庫的智慧標籤影像，與使用者選取的影像類似。 請參閱 [視覺搜尋](../assets/search-assets.md)。

### 動態媒體 {#dynamic-media-previous-service-packs}

#### 適用於動態媒體的智慧型影像 {#smart-imaging}

智慧型影像處理運用每位使用者獨特的檢視特性，自動提供最符合其體驗的影像，進而提高效能和參與度。 智慧型影像功能可與您現有的影像預設集搭配使用，並在傳送時的最後一毫秒使用智慧功能，根據瀏覽器或網路連線速度進一步降低影像檔案大小。 請參閱 [智慧型影像](../assets/imaging-faq.md)。

#### 動態媒體(6.5.3.0)的視訊設定檔智慧裁切 {#smart-crop-video}

智慧型裁切視訊（視訊描述檔中的選用功能）是一種工具，可運用Adobe Sensei中的人工智慧功能，自動偵測並裁切您上傳的任何最適化視訊或漸進式視訊中的焦點，不論其大小。 請參 [閱關於在視訊描述檔中使用智慧裁切](../assets/video-profiles.md)。

### Experience Manager Forms {#aem-forms-previous-service-packs}

#### 在Experience Manager Forms工作流程(6.5.4.0)中產生可列印的輸出 {#generate-printable-output}

使用「生成可打印輸出」工作流步驟，可以將源模板檔案與資料檔案整合。 此整合可讓您列印或儲存範本檔案的不同副本。 此步驟會產生PCL、PostScript、ZPL、IPL、TPCL或DPL輸出。 如需此功能的詳細資訊，請參 [閱「OSGi —— 步驟參考」上的「表單導向工作流程」](../forms/using/aem-forms-workflow-step-reference.md)。

![產生可列印的輸出](assets/generate-print-output-step.gif)

#### 多欄支援版面配置模式(6.5.4.0)中的自適應表單和互動式通訊 {#multi-column-adaptive-forms}

您現在可以在最適化表單和互動式通訊中，定義面板的欄數。 切換至版面模式，以使用新的多欄選項。 如需詳細資訊，請參 [閱「使用版面模式調整元件大小](../forms/using/resize-using-layout-mode.md)」。

![多欄版面](assets/multi-column-layout.gif)

#### Experience Manager收件箱定制(6.5.4.0) {#aem-inbox}

新的「管理控制」選項可讓管理員：

* 自訂標題文字和標誌。

* 控制頁首中可用導覽連結的顯示。

「管理控制」選項僅對或群組的成員 `administrators` 顯 `workflow-administrators` 示。 有關此功能的詳細資訊，請參 [閱收件箱](../sites-authoring/inbox.md)。

#### HTML5表格(6.5.4.0)的豐富式文字支援 {#rich-text-support}

將XFA表單中的文字欄位轉換為HTML5表單中的豐富式文字欄位。 如需詳細資訊，請 [參閱「設計HTML5表格的表格範本」](../forms/using/designing-form-template.md)。

#### 協助工具增強功能(6.5.4.0) {#forms-accessibility-enhancements-6540}

Experience Manager Forms包含下列協助工具增強功能：

* 螢幕閱讀程式會在最適化表單中正確發佈核取方塊、連結、「日期選擇器」和「日期輸入」欄位。

* 最適化表單的每一頁現在都包含一個標題和一個主要地標標籤。

#### 共用並請求存取Experience Manager Forms使用者(6.5.3.0)的收件匣項目 {#share-request-access}

您可以與其他使用者共用您的收件匣項目。 當其他使用者存取您的「收件匣」項目時，使用者就可以對共用項目宣告並採取適當動作。 同樣地，您也可以請求其他使用者存取「收件匣」項目。 請參 [閱共用並請求訪問用戶的收件箱項目](../forms/using/configure-shared-queues-osgi.md)。

#### 為AEM Forms使用者(6.5.3.0)的「收件匣」項目設定不在辦公室的設定 {#configure-out-of-office}

如果您計畫離開辦公室，您可以指定該期間指派給您的項目會發生什麼情況。
您可以選擇指定開始日期和時間，以及結束日期和時間，讓您的離職設定生效。 您可以設定預設人員，將您的所有項目傳送至該人員。 請參 [閱「設定不在辦公室」設定](../forms/using/configure-out-of-office-settings.md)。

#### 使用適用於AEM Forms(6.5.3.0)的Batch API產生多種互動式通訊 {#generate-multiple-ic}

您可以使用Batch API，從範本產生多種互動式通訊。 範本是互動式通訊，不含任何資料。 批次API將資料與範本結合，以產生互動式通訊。 API在大量製作互動式通訊時很實用。 例如，電話帳單、多名客戶的信用卡帳單。 請參 [閱使用批次API產生多種互動式通訊](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)。

## Adobe Experience Manager 6.5 SP4以來的主要版本 {#key-releases-since-last-sp}

在2020年3月05日至2020年6月04日期間，Adobe除了發行Service Pack和累積修補程式套件外，還發行下列產品：

* [Software Distribution Portal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) is available to download Experience Manager Service Packs、cumulative Fix Packs、Hotfix和Feature Packs。

* [!DNL Adobe Experience Manager Cloud Manager] [2020.3.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-3-0.html)、 [2020.4.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-4-0.html)和 [2020.5.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-current.html)。

* [Experience Manager案頭應用程式2.0.2.0](https://docs.adobe.com/content/help/zh-Hant/experience-manager-desktop-app/using/release-notes.html)。

* [Experience Manager畫面： 功能套件202004](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/release-notes/release-notes-fp-202004.html)。

>[!MORELIKETHIS]
>
>* [Adobe Experience Manager 6.5檔案](../user-guide/home.md)
>* [Adobe Experience Manager 6.5的一般發行說明](release-notes.md)
>* [Adobe Experience Manager 6.5的Service Pack發行說明](sp-release-notes.md)

