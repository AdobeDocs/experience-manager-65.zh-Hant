---
title: Adobe Experience Manager 6.5 Service Pack 7的新增功能
description: Adobe Experience Manager 6.5 Service Pack 7的新增功能
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 1c633e87d773f864c65320d3ce658f61271d086d
workflow-type: tm+mt
source-wordcount: '2807'
ht-degree: 1%

---


# Adobe Experience Manager 6.5 Service Pack 7的新增功能{#aem-whats-new-service-pack}

![Whats-new](assets/whatsnew.jpeg)

[!DNL Adobe Experience Manager] 6.5 Service Pack每季提供新功能、客戶要求的增強功能，以及效能、穩定性和安全性的改善。每季的上市情況讓您輕鬆存取和採用新功能和創新。

本文著重說明最新版6.5 Service Pack中包含的功能、前6.5 Service Pack中包含的[主要功能，以及自上一版Service Pack](#key-releases-since-last-sp)以來的[主要AEM版本。](#key-features-previous-service-packs)

## Adobe [!DNL Experience Manager Sites] {#aem-sites}

### 排序可轉出的即時副本頁面{#sort-livecopy-pages}

您現在可以使用[!UICONTROL 名稱]、[!UICONTROL 上次修改日期]和[!UICONTROL 上次轉出日期]屬性，來排序可轉出的即時副本頁面。 頁面的[!UICONTROL 上次推出日期]是此發行中引入的新屬性。

### 頁面移動和MSM展開的可用性作為非同步操作{#page-moves-msm-asynchronous}

您現在可以將頁面移動和MSM展開作為非同步操作來執行，以降低它們對執行時期效能的影響。 您可以安排操作以立即執行或稍後執行。 關聯作業和流程步驟的狀態顯示在控制台中，這有助於監控大規模MSM部署。

## [!DNL Adobe Experience Manager Assets] {#aem-assets}

* [!DNL Assets] 並提供 [!DNL Dynamic Media] 多種協助工具增強功能。這些增強功能與鍵盤導覽、螢幕閱讀程式的使用，以及類似的增強功能，以利使用輔助技術(AT)有關。 請參閱[[!DNL Assets] 增強功能](/help/release-notes/sp-release-notes.md#assets-6570)和[[!DNL Dynamic Media] 增強功能](/help/release-notes/sp-release-notes.md#dynamic-media-6570)。

* 使用者可以在「卡片」和「欄」檢視中排序數位資產。

## [!DNL Adobe Experience Manager Forms] {#aem-forms}

>[!NOTE]
>
>[!DNL Experience Manager Forms] 附加套件在排程的 [!DNL Experience Manager] Service Pack發行一週後可供使用。

### 效能改進{#performance-improvements-forms}

[!DNL Experience Manager] 6.5 Service Pack 7 Forms改善了以下效能：

* 在提交自適應表單時驗證伺服器上的欄位值。

* 使用[!DNL Automated Forms Conversion service]將PDF表單轉換為最適化表單。

### 建立資料模型HTTP用戶端組態以最佳化效能{#fdm-http-client-config}

[!DNL Experience Manager Forms] 當與REST風格的Web服務整合作為資料源時，現在包括HTTP客戶端配置以實現效能優化。

### 在「佈局」模式{#reset-option-layout-mode}中，每個元件的「重置選項」可用性

現在，您可以針對最適化表單的「版面」模式中的每個元件使用重設選項。 當您為面板定義多欄版面時，可使用此功能來重設面板中的個別元件。

## 前[!DNL Experience Manager] 6.5版Service Packs {#key-features-previous-service-packs}中的主要功能

### [!DNL Experience Manager Sites] {#aem-sites-previous-service-packs}

#### 頁面移動操作在非同步模式(6.5.6.0){#page-move-asynchronous}下的可用性

「頁面移動」操作現在可在非同步模式下使用。 除了立即執行外，您還可以計畫頁面移動操作以便稍後執行。

#### 協助工具改進(6.5.5.0){#accessibility-sites}

* 透過新增文字資訊，改善錯誤報告。

* 已改善鍵盤導覽期間的使用者介面焦點。

* 已改善各種使用者介面元素的對比度。

* 已改善頁面影像的alt屬性一致性。

* 已改善可存取Rich Internet Applications(ARIA)標籤的一致性。

* 已改善非視覺化案頭存取(NVDA)功能。

* 已改善螢幕閱讀器支援。

#### 其他主要增強功能(6.5.5.0){#other-enhancements-sites}

* 不允許匿名存取CRXDE Lite以增強安全性。 而是將使用者導向登入畫面。 請參閱[使用CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)開發。

* 複製或貼上頁面樹時，現在可以選擇貼上根頁面或貼上根頁面和樹的子頁面。

* [!DNL Adobe Experience Manager Experience Fragments] 匯出至工 [!DNL Adobe Target] 作區的選件類型和選件來源現在會顯示在 [!DNL Target]中。

* 多網站管理器——如果從來源頁面刪除元件，「發佈」觸發器現在會從發佈頁面刪除元件。

* 多站點管理器——當[!UICONTROL 即時副本]中的本地元件名稱與藍圖中的元件名稱相同且從藍圖中推出該元件時，現在將`_msm_moved`術語添加到本地元件的名稱中。

#### 樣式系統增強功能(6.5.4.0){#style-system-enhancements}

現在，您可以使用增強的「樣式系統」(Style System)在元件對話框中選取樣式。

#### 不同領域(6.5.4.0){#performance-improvements}的效能改進

* 縮短載入和初始化網站(`contexthub.kernel.js`)中ContextHub的時間。 這可縮短網站瀏覽時的頁面載入時間。

* 將[!DNL Experience Fragments]拖曳至[!DNL Sites]頁面編輯器後，可縮短重新整理頁面的時間。

* 縮短[!DNL Sites]頁面上的登入時間，**[!UICONTROL 即時副本概述]**&#x200B;中有超過200個即時副本。

* 已改善URL不完整或無效的處理。 此類URL會拖慢範本編輯器的速度。

### [!DNL Adobe Experience Manager Assets] {#aem-assets-previous-service-packs}

#### 協助工具增強功能(6.5.6.0){#accessibility-assets-6560}

* **增強鍵盤導覽時的使用者介面焦點**，例如：

   * `x` 表徵圖， [!UICONTROL 在時] 間軸中顯示資產的「版本 [!UICONTROL 預覽」]。

   * 可操作的使用者介面選項。

   * [!UICONTROL Share Link]對話方塊上的電子郵件欄位，以及在資料夾[!UICONTROL Properties]的[!UICONTROL Permission]標籤中新增已關閉使用者群組的欄位。

* **使用鍵盤按鍵的增強功能**

   使用者可以使用鍵盤按鍵，在螢幕閱讀程式的瀏覽模式中，拖曳中繼資料結構表單編輯器中的控制項。

* **由於下列原因**，螢幕閱讀程式使用者的可用性增強：

   * 螢幕閱讀程式會宣佈視訊和音訊播放器的用途。

   * 螢幕閱讀程式會宣佈使用者介面選項的用途，以移除在資產[!UICONTROL 屬性]上使用[!UICONTROL 標籤選擇對話方塊]選取的標籤。

   * 螢幕閱讀程式會公佈表格的列標題和列項目，讓使用者知道哪些項目屬於同一列。

   * 搜尋頁面的描述性和有意義的頁面標題。

   * 螢幕閱讀程式會將搜尋篩選面板中的選項宣佈為可展開的收合式。

#### [!DNL Assets](6.5.6.0){#other-enhancements-assets-6560}中的其他增強功能

* 與資料夾（專用和非專用）關聯的用戶組現在從[刪除這些資料夾](/help/assets/private-folder.md#delete-private-folder)的儲存庫中刪除。 但是，可以使用JMX將現有的冗餘、孤立、未使用和自動生成的用戶組從儲存庫中刪除。

#### [!DNL Assets](6.5.5.0){#assets-accessibility}中的協助工具增強功能

[!DNL Experience Manager Assets] 現在可依照網頁內容協助工具准則(WCAG)更容易存取。協助工具已改善，因為下列增強功能：

* 許多使用者介面元素、控制項、頁面和對話方塊都適合螢幕閱讀程式。

* 許多使用者介面元素、控制項和輸入表單欄位都可使用鍵盤存取。

* 某些使用者介面元素的顏色和對比已更新，以便視力不良和無法分辨顏色的使用者區分這些使用者介面元素。例如，星型分級圖示的顏色（例如資產[!UICONTROL 屬性]或卡片檢視中[!UICONTROL 進階]標籤的[!UICONTROL Rating]區段）會因適當的對比而變更。

   ![對比度改善的圖示分級](assets/star-rating-icons.png)

#### 增強異常處理(6.5.5.0){#exception-handling}

[!DNL Assets] 用戶介面流具有更好的異常處理。如果資產的維度沒有類型，則會在日誌檔案中記錄觀察到的異常。

#### [!DNL Dynamic Media](6.5.5.0){#support-for-3d}中支援3D資產

[!DNL Dynamic Media]中支援3D影像，讓客戶可發佈3D內容，並將之新增至網頁和應用程式。 支援包括：

* 發佈常用的3D資產格式，並產生可用於網頁和其他應用程式的資產URL。

* 由[!DNL Adobe Dimension]提供支援的3D網頁檢視器，以互動方式檢視已發佈的3D資產。

* 使用[!DNL Sites] WCM元件，在[!DNL Experience Manager Sites]頁面上發佈及檢視常用的3D資產。

#### 將[!DNL Experience Manager Assets]配置為[!DNL Brand Portal](6.5.4.0){#configure-assets-bp}

[!DNL Experience Manager Assets]和[!DNL Brand Portal]之間的授權通道被更改。 之前，[!DNL Brand Portal]是透過舊版OAuth閘道在傳統UI中設定，該閘道使用JWT代號交換來取得IMS存取代號以進行授權。 [!DNL Experience Manager Assets] 現在已透過Adobe  [!DNL Brand Portal] I/O設定，而Adobe I/O會購買IMS Token以取得您的租用戶 [!DNL Brand Portal] 授權。

使用[!DNL Brand Portal]配置[!DNL Experience Manager Assets]的步驟因您的[!DNL Experience Manager]版本而異，取決於您是首次配置還是升級現有配置。 如需詳細資訊，請參閱[使用品牌入口網站設定Experience Manager資產。](https://docs.adobe.com/content/help/zh-Hant/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html)

#### 協助工具增強功能(6.5.4.0){#accessibility-enhancements}

[!DNL Experience Manager Assets] 包含下列協助工具增強功能：

* 鍵盤上的箭頭鍵可用來移動和平移縮放影像中的區域。 如需詳細資訊，請參閱[僅使用鍵盤按鍵預覽資產](../assets/manage-assets.md#previewing-assets)。

* 「篩選器」面板中的混合狀態複選框（除非您選擇了所有嵌套的謂詞，否則不會選擇並刪除第一級複選框）由螢幕閱讀器讀取。

* 日期和時間格式約束在日期欄位的欄位標籤中提供，使用戶能夠使用鍵盤以正確的格式輸入日期。
例如，`On Time (MM-DD-YYYY HH:mm)`。 其中MM是兩位數格式的月份，YYYY是年份，DD是兩位數格式的日，HH是24小時軍用格式的小時，而mm是分鐘。

* 螢幕閱讀程式會宣佈移除選取標籤（`X`符號）的選項，以及選取標籤的數目。

#### 清單檢視(6.5.3.0){#sortable-date-created-column}中資產建立日期的可排序欄

在DAM清單檢視中新增資產建立日期的可排序新欄，並在清單檢視中新增資產搜尋結果。

![建立日期的可排序列](assets/asset-created-date.png)

#### 視覺搜尋[!DNL Adobe Experience Manager Assets](6.5.2.0){#visual-search}

[!DNL Assets] 使用者可以搜尋外觀相似的影像。Experience Manager會顯示來自DAM存放庫的智慧標籤影像，與使用者選取的影像類似。 請參閱[視覺搜尋](../assets/search-assets.md)。

### 動態媒體 {#dynamic-media-previous-service-packs}

#### 使CDN快取內容(6.5.6.0){#invalidate-cdn-cached-content}無效

您現在可以使用[!DNL Dynamic Media]使用者介面，使內容傳送網路(CDN)快取內容失效。 因此，更新的資產可立即使用，而不需等待快取過期。 您可以透過下列方式使CDN失效：

* 建立CDN失效範本：選取資產和表單相關範本型URL

* 透過資產選擇器選取資產和相關的預設集

* 新增完整的資產URL

#### 選擇性發佈資產至[!DNL Experience Manager]和[!DNL Dynamic Media](6.5.6.0){#selective-publishing}

您現在可以選擇使用[!UICONTROL 快速發佈]或[!UICONTROL 管理出版物]精靈，選擇性地將資產發佈或取消發佈至[!DNL Experience Manager]或[!DNL Dynamic Media]。 您也可以在資料夾層級設定`Publish`或`Unpublish`模式。

#### 動態媒體的智慧映像{#smart-imaging}

智慧型影像處理運用每位使用者獨特的檢視特性，自動提供最符合其體驗的影像，進而提高效能和參與度。 智慧型影像功能可與您現有的影像預設集搭配使用，並在傳送時的最後一毫秒使用智慧功能，根據瀏覽器或網路連線速度進一步降低影像檔案大小。 請參閱[智慧型影像](../assets/imaging-faq.md)。

#### 動態媒體(6.5.3.0){#smart-crop-video}的視訊設定檔智慧裁切

智慧型裁切視訊（視訊描述檔中的選用功能）是一種工具，可運用Adobe Sensei中的人工智慧功能，自動偵測並裁切您上傳的任何最適化視訊或漸進式視訊中的焦點，不論其大小。 請參閱[關於在視訊描述檔中使用智慧裁切](../assets/video-profiles.md)。

### Experience Manager Forms {#aem-forms-previous-service-packs}

#### 在用戶端(6.5.6.0){#prefill-merge-data-at-client}預先填寫最適化表格

當您預先填寫最適化表格時，[!DNL Experience Manager Forms]伺服器會將資料與最適化表格合併，並將填寫的表格傳送給您。 依預設，資料合併動作會在伺服器上進行。
您現在可以將[!DNL Experience Manager Forms]伺服器配置為[在客戶端執行資料合併操作，而不是在伺服器上執行。 ](../../help/forms/using/prepopulate-adaptive-form-fields.md)它可大幅縮短預先填寫和轉換最適化表單的時間。

#### 在具備雙向SSL實作(6.5.6.0){#fdm-integration-rest-apis-two-way-ssl}的伺服器上，與REST風格的API整合表單資料模型

[!DNL Experience Manager Forms] 表單資料模型現 [在可與在具備雙向SSL的伺服器上的REST風格API整合](../../help/forms/using/configure-data-sources.md)。

#### 新增對Automated Forms Conversion Service(6.5.6.0){#sign-integration-acroform-afcs}中的[!DNL Adobe Sign]文字標籤的支援

如果AcroForm包含[!DNL Adobe Sign]文字標籤，這些欄位現在會在使用[!DNL Automated Forms Conversion service]轉換的最適化表單中辨識並表示為[!DNL Adobe Sign]欄位。 簽署者可在簽署最適化表單時填寫這些欄位。

#### 支援將彩色PDF表格轉換為最適化表格(6.5.6.0){#colored-PDF-forms}

您可以使用[!DNL Automated Forms Conversion service]將彩色PDF表單轉換為最適化表單。

#### 支援SMB 2和SMB 3協定(6.5.6.0){#smb-support}

[!DNL Experience Manager Forms] 現在支援SMB 2和SMB 3協定。

#### 增強轉譯的可調式表單頁面快取(6.5.6.0){#enhanced-caching-translated-adaptive-forms}

您現在可以在最適化表單URL中指定[地區設定為選擇器，而非最適化表單URL](../../help/forms/using/supporting-new-language-localization.md)中的引數。 它幫助快取[!DNL Experience Manager Dispatcher]上翻譯的自適應表單。 在舊版中無法快取轉換的最適化表單。 有關在自適應表單URL中配置將區域設定用作選擇器的快取的詳細資訊，請參見[在dispatcher](../../help/forms/using/configure-adaptive-forms-cache.md)中配置自適應表單快取。

#### 將表單資料模型服務的輸出儲存至變數(6.5.6.0){#save-fdm-service-to-variable}

表單資料模型可讓您將表單資料模型服務的輸出儲存至變數。 [!DNL Experience Manager Forms] 現在會自動將表單資料模型服務的類型對應至變數的類型。

#### 為檔案附件元件(6.5.6.0){#attach-multiple-files}附加多個檔案

現在，您可以[將多個檔案](../../help/forms/using/introduction-forms-authoring.md)附加到最適化表單的[!UICONTROL 檔案附件]元件。

#### 自訂Adobe Experience Manager收件箱欄(6.5.5.0){#customize-aem-inbox-columns}

您可以自訂[!DNL Experience Manager]收件匣，以變更欄的預設標題、重新排序欄位，並根據工作流程的資料顯示其他欄位。 `administrators`或`workflow-administrators`群組成員可以自訂欄。 如需詳細資訊，請參閱[管理控制](../sites-authoring/inbox.md#inbox-admin-control)。

![自訂Experience Manager收件匣欄](assets/customize-columns.gif)

#### 將互動式通訊儲存為草稿(6.5.5.0){#save-as-draft}

您可以使用Agent UI為每個「互動式通訊」儲存一或多個草稿，並稍後擷取草稿以繼續處理。 您可以為每個草稿指定不同的名稱以加以識別。 如需詳細資訊，請參閱[將互動式通訊另存為草稿](../forms/using/prepare-send-interactive-communication.md#save-as-draft)。

![另存為草稿](assets/save-as-draft.gif)

#### [!DNL Oracle WebLogic] 應用程式伺服器支援(6.5.5.0)  {#weblogic-support}

Adobe Experience Manager Forms已新增對JEE上Adobe Experience Manager Forms的[!DNL Oracle WebLogic 12]支援。 您可以從舊版升級，或在[!DNL Oracle WebLogic] 12.2.1.4及更新版本的JEE伺服器上設定新的Experience Manager 6.5 Forms。 稍後的版本會與次要版本變更相對應，其中12.2.1.x中的x會以版本號碼取代。

#### 協助工具改進(6.5.5.0){#accessibility-improvements}

Adobe Experience Manager Forms包含下列協助工具增強功能：

* 當使用者將最適化表單預覽為HTML表單時，[!UICONTROL 塗鴉簽名]欄位會保留標籤焦點。

* 提交最適化表單時顯示的錯誤訊息現在包含`aria-describedBy`屬性。 屬性會附加至錯誤訊息中參考的欄位。 `aria-describedby`屬性指示描述對象的元素的ID。 它有助於建立介面工具集或群組與描述它們的文字之間的關係。

* 如果最適化表單包含某些強制欄位，則ARIA協助工具模式中此類欄位的強制屬性會設為`True`。

#### X-509憑證式驗證，適用於表單資料模型(6.5.5.0){#x509-based-authentication-soap}的SOAP型網站服務

表單資料模型現在支援X-509憑證式驗證，同時使用SOAP web services做為資料來源。 如需詳細資訊，請參閱[設定SOAP web services](../forms/using/configure-data-sources.md#configure-soap-web-services)。

#### 其他主要改進(6.5.5.0){#other-improvements}

* Experience Manager 6.5 Forms on JEE Document Security現在是以[!DNL Apache Struts 2]為基礎。

* 新增對[!DNL Oracle Real Applications Cluster (RAC) 19c]的支援。

#### 在Experience Manager Forms工作流程(6.5.4.0){#generate-printable-output}中產生可列印的輸出

使用「生成可打印輸出」工作流步驟，可以將源模板檔案與資料檔案整合。 此整合可讓您列印或儲存範本檔案的不同副本。 此步驟會產生PCL、PostScript、ZPL、IPL、TPCL或DPL輸出。 有關此功能的詳細資訊，請參閱OSGi —— 步驟參考](../forms/using/aem-forms-workflow-step-reference.md)上的[表單導向工作流程。

![產生可列印的輸出](assets/generate-print-output-step.gif)

#### 在版面模式(6.5.4.0){#multi-column-adaptive-forms}中支援最適化表單和互動式通訊的多欄

您現在可以在最適化表單和互動式通訊中，定義面板的欄數。 切換至版面模式，以使用新的多欄選項。 如需詳細資訊，請參閱[使用版面模式來調整元件大小](../forms/using/resize-using-layout-mode.md)。

![多欄版面](assets/multi-column-layout.gif)

#### Experience Manager收件箱定制(6.5.4.0){#aem-inbox}

新的「管理控制」選項可讓管理員：

* 自訂標題文字和標誌。

* 控制頁首中可用導覽連結的顯示。

「管理控制」選項僅對`administrators`或`workflow-administrators`組的成員顯示。 有關此功能的詳細資訊，請參閱[收件箱](../sites-authoring/inbox.md)。

#### HTML5表單(6.5.4.0){#rich-text-support}的豐富式文字支援

將XFA表單中的文字欄位轉換為HTML5表單中的豐富式文字欄位。 如需詳細資訊，請參閱[設計HTML5表單的表單範本](../forms/using/designing-form-template.md)。

#### 協助工具增強功能(6.5.4.0){#forms-accessibility-enhancements-6540}

Experience Manager Forms包含下列協助工具增強功能：

* 螢幕閱讀程式會在最適化表單中正確發佈核取方塊、連結、「日期選擇器」和「日期輸入」欄位。

* 最適化表單的每一頁現在都包含一個標題和一個主要地標標籤。

#### 共用並請求存取Experience Manager Forms使用者(6.5.3.0){#share-request-access}的「收件匣」項目

您可以與其他使用者共用您的收件匣項目。 當其他使用者存取您的「收件匣」項目時，使用者就可以對共用項目宣告並採取適當動作。 同樣地，您也可以請求其他使用者存取「收件匣」項目。 請參閱[共用並請求訪問用戶](../forms/using/configure-shared-queues-osgi.md)的收件箱項目。

#### 為Experience Manager Forms用戶(6.5.3.0){#configure-out-of-office}的收件箱項目配置離職設定

如果您計畫離開辦公室，您可以指定該期間指派給您的項目會發生什麼情況。
您可以選擇指定開始日期和時間，以及結束日期和時間，讓您的離職設定生效。 您可以設定預設人員，將您的所有書籍項目傳送至該人員。 請參閱[設定不在辦公室的設定](../forms/using/configure-out-of-office-settings.md)。

#### 使用Experience Manager Forms(6.5.3.0){#generate-multiple-ic}的Batch API產生多種互動式通訊

您可以使用Batch API，從範本產生多種互動式通訊。 範本是互動式通訊，不含任何資料。 批次API將資料與範本結合，以產生互動式通訊。 API在大量製作互動式通訊時很實用。 例如，電話帳單、多名客戶的信用卡帳單。 請參閱[使用Batch API](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)產生多種互動式通訊。

## 自Adobe Experience Manager 6.5 SP6 {#key-releases-since-last-sp}以來的主要版本

在2020年9月03日至2020年11月26日期間，Adobe除了發行Service Pack和累積修補程式套件外，還發行下列產品：

* [!DNL Adobe Experience Manager] 作為雲服務 [2020.9.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-2020-9-0.html?lang=en#release-notes) 和 [2020.10.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-2020-10-0.html?lang=en#release-notes)。

* [[!DNL Experience Manager] 案頭應用程式2.0(2.0.3.2)](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html)。

* [WKND參考網站- 0.0.6](https://github.com/adobe/aem-guides-wknd/releases/tag/aem-guides-wknd-0.0.6)

* [Experience Manager畫面：功能套件202011](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/release-notes/release-notes-fp-202011.html)

* [Adobe Asset Link v2.2](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html)

>[!MORELIKETHIS]
>
>* [[!DNL Adobe Experience Manager] 6.5檔案](../user-guide/home.md)
>* [ [!DNL Adobe Experience Manager] 6.5的一般發行說明](release-notes.md)
>* [ [!DNL Adobe Experience Manager] 6.5版Service Pack發行說明](sp-release-notes.md)

