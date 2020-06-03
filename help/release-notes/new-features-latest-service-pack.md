---
title: Adobe Experience Manager 6.5 Service Pack 5的新增功能
description: Adobe Experience Manager 6.5 Service Pack 5的新增功能
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: cc423a199e860429e85895690f6c1a81c20d1a19
workflow-type: tm+mt
source-wordcount: '1853'
ht-degree: 2%

---


# AEM 6.5 Service Pack 5的新增功能 {#aem-whats-new-service-pack-5}

Adobe Experience Manager 6.5 Service Pack每季提供新功能、客戶要求的增強功能、效能和穩定性相關改進。 每季傳送模式讓存取和採用新功能與創新變得更輕鬆。

本文重點介紹最新6.5 Service Pack中的功能、 [舊版6.5 Service Pack中的主要功能](#key-features-previous-service-packs)，以及Experience Manager 6.5.4.0版以來的 [部分主要版本](#key-features-sice-sp3) 。

## AEM Sites {#aem-sites}

### 協助工具改進 {#accessibility-sites}

* 新增文字資訊以改善錯誤報告

* 改善鍵盤導覽時的UI焦點

* 改善的文字對比度（明度比）

* 改善頁面影像的alt屬性一致性

* 改善可存取Rich Internet Applications(ARIA)標籤的一致性

* 增強的非視覺化案頭存取(NVDA)功能

* 改良的螢幕閱讀器支援

### 其他重要增強功能 {#other-enhancements-sites}

* 複製或貼上頁面樹時，現在可以選擇貼上根頁面或貼上根頁面和樹的子頁面。

* AEM Experience Fragments exported to Adobe Target workspaces now appear as unique offer types and offer sources in [!DNL Target].

* 多網站管理器——如果從來源頁面刪除元件，「發佈」觸發器現在會成功從發佈頁面刪除元件。

* 多網站管理器——當LiveCopy中的本機元件名稱與Blueprint中的元件名稱相同且元件從Blueprint中推出時，_msm_moved一詞現在會成功新增至本機元件名稱。

## AEM Assets {#aem-assets}

### 資產中的協助工具增強功能 {#assets-accessibility}

[!DNL Adobe Experience Manager] 資產功能現在可依照網頁內容協助工具准則(WCAG)更容易存取。 無障礙環境支援在下列方面已改善：

* 使用者介面元素、控制項、頁面和對話方塊都適合螢幕閱讀程式。

* 使用者介面元素、控制項和輸入表單欄位都可使用鍵盤存取。

* 有些圖形的顏色和對比會有所改變，以利於視覺有限且對顏色沒有感知的使用者區分。 例如，星號分級圖示的顏色(例如在資產屬性( [!UICONTROL Properties] )或卡片檢視( [!UICONTROL Advanced Tab)的「分級(Rating] )」區段中)會變更，以取得適當的對比。

![星號分級圖示的顏色已變更以改善對比](assets/star-rating-icons.png)

### 增強的異常處理 {#exception-handling}

資產使用者介面流程有更好的例外處理。 之前，如果資產的維度沒有正確類型，則會發現無訊息擷取且記錄檔中沒有追蹤的例外。 此行為已變更，所有例外都會擷取到記錄檔中。

## [!DNL Dynamic Media] {#dynamic-media}

### 3D支援 [!DNL Dynamic Media] {#support-for-3d}

現在，3D支援 [!DNL Dynamic Media] 可讓客戶發佈3D內容，並將之新增至網頁和應用程式。 它包括：

* 發佈常用的3D資產格式，以產生資產URL。

* 使用Adobe Dimension支援的檢視器資料庫中提供的全新3D網頁檢視器，以互動方式檢 [!DNL Dynamic Media] 視已發佈的3D資產。

* 使用WCM元件在頁 [!DNL Experience Manager Sites] 面上發佈和 [!DNL Sites] 檢視3D。

## AEM Forms {#aem-forms}

### 自訂AEM收件匣欄 {#customize-aem-inbox-columns}

您可以自訂AEM收件匣，以變更欄的預設標題、重新排序欄位，並根據工作流程的資料顯示其他欄位。 您應是自訂欄的 `administrators` 成員 `workflow-administrators` 或群組成員。

![自訂AEM收件匣欄](assets/customize-columns.gif)

### 將互動式通訊儲存為草稿 {#save-as-draft}

您可以使用Agent UI為每個「互動式通訊」儲存一或多個草稿，並稍後擷取草稿以繼續處理。 您可以為每個草稿指定不同的名稱，以方便識別。

![另存為草稿](assets/save-as-draft.gif)

### [!DNL Oracle WebLogic] 應用程式伺服器支援 {#weblogic-support}

AEM Forms已新增對JEE上 [!DNL Oracle WebLogic 12] AEM Forms的支援。 您可以從舊版升級，或在 [!DNL Oracle WebLogic] 12.2.1.4和更新版本的JEE伺服器上設定新的AEM 6.5 Forms。 稍後的版本會與次要版本變更相對應，其中12.2.1.x中的x會以版本號碼取代。

### 協助工具改進 {#accessibility-improvements}

AEM Forms包含下列協助工具增強功能：

* 當使用者將最適化表單預覽為HTML表單時，「塗鴉 [!UICONTROL 簽名] 」欄位會保留標籤焦點。

* 提交最適化表單時顯示的錯誤訊息現在包含屬 `aria-describedBy` 性。 屬性會附加至錯誤訊息中參考的欄位。 該 `aria-describedby` 屬性表示描述對象的元素的ID。 它有助於建立介面工具集或群組與描述它們的文字之間的關係。

* 如果最適化表單有某些必填欄位，則ARIA無障礙環境支援架構中的 `True` 此類欄位必填屬性會設定為。

### X-509憑證式驗證，適用於表單資料模型中以SOAP為基礎的Web服務 {#x509-based-authentication-soap}

表單資料模型現在支援X-509憑證式驗證，同時使用SOAP web services做為資料來源。

### 其他主要改進 {#other-improvements}

* AEM 6.5 Forms on JEE Document Security現在是以為基礎 [!DNL Apache Struts 2]。

* 新增對的支 [!DNL Oracle Real Applications Cluster (RAC) 19c]援。

## 舊版AEM 6.5 Service Pack的主要功能 {#key-features-previous-service-packs}

### AEM Sites {#aem-sites-previous-service-packs}

#### 樣式系統增強功能(6.5.4.0) {#style-system-enhancements}

現在，您可以使用增強的「樣式系統」(Style System)在元件對話框中選取樣式。

#### 不同領域的效能改進(6.5.4.0) {#performance-improvements}

* 縮短在網站(`contexthub.kernel.js`)中載入和初始化ContextHub的時間。 這可縮短網站瀏覽時的頁面載入時間。

* 將「體驗片段」拖曳至「網站頁面編輯器」後，可縮短重新整理頁面的時間。

* 縮短「即時副本概述」中超過200個即時副本的「網站」頁面登入 **[!UICONTROL 時間]**。

* 已改善URL不完整或無效的處理。 這類URL會拖慢範本編輯器的速度。

### AEM Assets {#aem-assets-previous-service-packs}

#### Configure AEM Assets with Brand Portal (6.5.4.0) {#configure-assets-bp}

AEM Assets和品牌入口網站之間的授權渠道已變更。 之前，品牌入口網站是透過舊版OAuth閘道在傳統使用者介面中設定，該閘道使用JWT代號交換來取得IMS存取代號以進行授權。 AEM Assets現在已透過Adobe I/O設定品牌入口網站，Adobe I/O會購買IMS Token以授權您的品牌入口網站租用戶。

使用品牌入口網站設定AEM資產的步驟依您的AEM版本而異，以及您是首次設定或升級現有的設定。 如需詳 [細資訊，請參閱「設定AEM資產與品牌入口網站](https://docs.adobe.com/content/help/zh-Hant/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html) 」。

#### 協助工具增強功能(6.5.4.0) {#accessibility-enhancements}

Experience Manager Assets包含下列協助工具增強功能：

* 鍵盤上的箭頭鍵可用來移動和平移縮放影像中的區域。 如需詳細資訊，請參閱 [僅使用鍵盤按鍵預覽資產](../assets/managing-assets-touch-ui.md#previewing-assets)。

* 「篩選器」面板中的混合狀態複選框（除非您選擇了所有嵌套的謂詞，否則不會選擇並刪除第一級複選框）由螢幕閱讀器讀取。

* 日期和時間格式約束在日期欄位的欄位標籤中提供，使用戶能夠使用鍵盤以正確的格式輸入日期。

   For example, `On Time (MM-DD-YYYY HH:mm)`. 其中MM是兩位數格式的月份，YYYY是年份，DD是兩位數格式的日，HH是24小時軍用格式的小時，而mm是分鐘。

* 現在 `X` 螢幕閱讀程式會公佈用來移除目前選取標籤的按鈕符號，以及選取的標籤數。

#### AEM Assets的視覺搜尋(6.5.2.0) {#visual-search}

資產使用者可以搜尋視覺上類似的影像。 AEM會顯示來自DAM儲存庫的智慧型標籤影像，這些影像類似於使用者選取的影像。請參閱 [視覺搜尋](../assets/search-assets.md)。

### 動態媒體 {#dynamic-media-previous-service-packs}

#### 適用於動態媒體的智慧型影像 {#smart-imaging}

智慧型影像處理運用每位使用者獨特的檢視特性，自動提供最符合其體驗的影像，進而提高效能和參與度。 智慧型影像功能可與您現有的影像預設集搭配使用，並在傳送時的最後一毫秒使用智慧功能，根據瀏覽器或網路連線速度進一步降低影像檔案大小。 請參閱 [智慧型影像](../assets/imaging-faq.md)。

#### 動態媒體(6.5.3.0)的視訊設定檔智慧裁切 {#smart-crop-video}

智慧型裁切視訊（視訊描述檔中的選用功能）是一種工具，可運用Adobe Sensei中的人工智慧功能，自動偵測並裁切您上傳的任何最適化視訊或漸進式視訊中的焦點，不論其大小。 請參 [閱關於在視訊描述檔中使用智慧裁切](../assets/video-profiles.md)。

### AEM Forms {#aem-forms-previous-service-packs}

#### 在AEM Forms工作流程(6.5.4.0)中產生可列印的輸出 {#generate-printable-output}

使用「生成可打印輸出」工作流步驟，可以將源模板檔案與資料檔案整合。 此整合可讓您列印或儲存範本檔案的不同副本。 此步驟會產生PCL、PostScript、ZPL、IPL、TPCL或DPL輸出。 如需此功能的詳細資訊，請參 [閱「OSGi —— 步驟參考」上的「表單導向工作流程」](../forms/using/aem-forms-workflow-step-reference.md)。

![產生可列印的輸出](assets/generate-print-output-step.gif)

#### 多欄支援版面配置模式(6.5.4.0)中的自適應表單和互動式通訊 {#multi-column-adaptive-forms}

您現在可以在最適化表單和互動式通訊中，定義面板的欄數。 切換至版面模式，以使用新的多欄選項。 如需詳細資訊，請參 [閱「使用版面模式調整元件大小](../forms/using/resize-using-layout-mode.md)」。

![多欄版面](assets/multi-column-layout.gif)

#### AEM Inbox自訂(6.5.4.0) {#aem-inbox}

新的「管理控制」選項可讓管理員：

* 自訂標題文字和標誌

* 控制頁首中可用導覽連結的顯示

「管理控制」選項僅對管理員或工作流程管理員群組的成員顯示。 有關此功能的詳細資訊，請參 [閱收件箱](../sites-authoring/inbox.md)。

#### HTML5表格(6.5.4.0)的豐富式文字支援 {#rich-text-support}

將XFA表單中的文字欄位轉換為HTML5表單中的豐富式文字欄位。 如需詳細資訊，請 [參閱「設計HTML5表格的表格範本」](../forms/using/designing-form-template.md)。

#### 協助工具增強功能(6.5.4.0) {#forms-accessibility-enhancements-6540}

Experience Manager Forms包含下列協助工具增強功能：

* 螢幕閱讀程式會在最適化表單中正確發佈核取方塊、連結、「日期選擇器」和「日期輸入」欄位。

* 最適化表單的每一頁現在都包含一個標題和一個主要地標標籤。

#### 共用並要求存取AEM Forms使用者(6.5.3.0)的「收件匣」項目 {#share-request-access}

您可以與其他使用者共用您的收件匣項目。 當其他使用者存取您的「收件匣」項目時，使用者就可以對共用項目宣告並採取適當動作。 同樣地，您也可以請求其他使用者存取「收件匣」項目。 請參 [閱共用並請求訪問用戶的收件箱項目](../forms/using/configure-shared-queues-osgi.md)。

#### 為AEM Forms使用者(6.5.3.0)的「收件匣」項目設定不在辦公室的設定 {#configure-out-of-office}

如果您計畫離開辦公室，您可以指定該期間指派給您的項目會發生什麼情況。
您可以選擇指定開始日期和時間，以及結束日期和時間，讓您的離職設定生效。 您可以設定預設人員，將您的所有項目傳送至該人員。 請參 [閱「設定不在辦公室」設定](../forms/using/configure-out-of-office-settings.md)。

#### 使用適用於AEM Forms(6.5.3.0)的Batch API產生多種互動式通訊 {#generate-multiple-ic}

您可以使用Batch API，從範本產生多種互動式通訊。 範本是互動式通訊，不含任何資料。 批次API將資料與範本結合，以產生互動式通訊。 API在大量製作互動式通訊時很實用。 例如，電話帳單、多名客戶的信用卡帳單。 請參 [閱使用批次API產生多種互動式通訊](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)。

## 自AEM 6.5 SP4以來的主要版本 {#key-releases-since-last-sp}

在2020年3月5日至2020年6月04日期間，Adobe發佈了下列AEM核心交付內容以外的功能：

* AEM Cloud Manager [2020.3.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-3-0.html)、 [2020.4.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-4-0.html)和 [2020.5.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-current.html)

* [AEM Assets: 案頭應用程式2.0.2.0](https://docs.adobe.com/content/help/zh-Hant/experience-manager-desktop-app/using/release-notes.html)

* [AEM Screens: 功能套件202004](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/release-notes/release-notes-fp-202004.html)

## 實用資源

* [AEM 6.5使用指南](../user-guide/home.md)

* [Adobe Experience Manager 6.5的一般發行說明](release-notes.md)

* [Adobe Experience Manager 6.5的Service Pack發行說明](sp-release-notes.md)
