---
title: 新增功能 [!DNL Experience Manager] 6.5 Service Pack 11
description: 新增功能 [!DNL Experience Manager] 6.5 Service Pack 11
contentOwner: AK
mini-toc-levels: 1
exl-id: 32470e6e-8a66-4670-82da-2259f6e001c3
source-git-commit: 092ba82ac645539fd0d4e2085c380025201914de
workflow-type: tm+mt
source-wordcount: '4399'
ht-degree: 1%

---

# 新增功能 [!DNL Adobe Experience Manager] 6.5 Service Pack 11 {#aem-whats-new-service-pack}

<!-- TBD: Downsample this image. We do not need as big an image since customers don't use as big a screen to view. Also, having a 700+ KB decorative image is bad for page load time.
-->

![Whats-new](assets/whatsnew.jpeg)

[!DNL Adobe Experience Manager] 6.5 Service Pack每季提供新功能、客戶要求的增強功能，以及效能、穩定性和安全性方面的改善。 每季的可用性使用戶能夠輕鬆訪問和採用新功能和創新。

本文重點說明最新Service Pack中包含的功能， [先前6.5版Service Pack中包含的主要功能](#key-features-previous-service-packs)，和 [自上次Service Pack以來的重要發行](#key-releases-since-last-sp) 發行。

## [!DNL Adobe Experience Manager Sites] {#aem-sites}

* 您可以使用 [SEO索引包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/sites-seo-index-content-1.0.0.zip). 它支援網站地圖、替代URL、機器人中繼標籤，以及 [!DNL Core Components].

* 新增多欄位支援多行文字資料類型。

* 增強功能，讓使用者了解目前在背景執行的非同步作業，以防止他們在相同路徑上觸發多個非同步作業。

## [!DNL Adobe Experience Manager Assets] {#aem-assets}

* 使用者體驗增強功能會顯示資料夾中存在的資產數量。 若是資料夾中超過1000個資產， [!DNL Assets] 顯示1000+。

   ![資料夾中的資產數](/help/assets/assets/browse-folder-number-of-assets.png)

* 提供下列協助工具增強功能：

   * 在 [!DNL Assets] 存放庫，當使用 `Tab` 若要將焦點移至開啟焦點快速動作的第一個項目，螢幕助讀程式會朗讀焦點項目的名稱。
   * 在 [!DNL Dynamic Media] [!UICONTROL 檢視器預設集編輯器]，如果陰影顏色和邊框顏色不存在，則使用禁用的屬性禁用輸入。 鍵盤使用者無法聚焦輸入，而螢幕助讀程式不會將控制項的狀態宣佈為已停用。
   * 在 [!DNL Dynamic Media]，在介面中建立新的視訊編碼設定檔時， [!UICONTROL 智慧型裁切比例] 選項會標示為協助工具，讓螢幕助讀程式能正確宣告。

### [!DNL Dynamic Media] {#dynamic-media}

* 您現在可以使用 [!DNL Dynamic Media] 來設定一般設定，而非必須完成 [!DNL Dynamic Media Classic] 案頭應用程式。 請參閱 [配置Dynamic Media一般設定](/help/assets/dm-general-settings.md).

   ![DM一般設定](/help/assets/assets-dm/dm-general-settings.png)

* 您現在可以使用 [!DNL Dynamic Media] 來設定發佈設定，而不需要完成 [!DNL Dynamic Media Classic] 案頭應用程式。 請參閱 [設定Dynamic Media發佈設定](/help/assets/dm-publish-settings.md).

   ![DM發佈設定](/help/assets/assets-dm/dm-publish-setup.png)

## [!DNL Adobe Experience Manager Forms] {#aem-forms}

>[!NOTE]
>
>* [!DNL Experience Manager Forms] 會在預定的 [!DNL Experience Manager] Service Pack 發行日期一週後發行附加元件的套件。


## 舊版的主要功能 [!DNL Experience Manager] 6.5 Service Pack {#key-features-previous-service-packs}

### [!DNL Experience Manager Sites] {#aem-sites-previous-service-packs}

#### AEM 6.5.10.0版包含的功能 {#features-sites-65100}

* **增強功能 [!DNL Content Fragment] 模型與編輯器**:您現在可以使用巢狀內容，為結構化內容建立複雜的自訂模型 [!DNL Content Fragment] 模型。 內容結構被模組化為基本元素，這些基本元素被建模為子片段。 較高層級片段會參考這些子片段。 進階驗證規則等更多資料類型增強功能，可進一步增強內容模型的彈性，具有 [!DNL Content Fragments]. 此 [!DNL Experience Manager] [!DNL Content Fragment] 編輯器支援通用編輯器工作階段中的巢狀片段結構，並增強功能，例如結構樹檢視和透過片段階層的標籤式階層連結導覽。

* **GraphQL API，適用於[!DNL Content Fragments]**:全新的GraphQL API是以JSON格式傳送結構化內容的標準方法。 GraphQL查詢可讓用戶端僅要求相關內容項目來呈現體驗。 這種選擇消除了需要在用戶端剖析內容的內容過傳送（在HTTP REST API中可能）。 GraphQL結構衍生自 [!DNL Content Fragment] 模型和API回應會以JSON格式產生。 在 [!DNL Experience Manager] as a [!DNL Cloud Service], [GraphQL查詢持續存在](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/graphql-api-content-fragments.html#persisted-queries-caching) 和處理快取友好GET請求。 在 [!DNL Experience Manager] 6.5。

* **階層管理與未來預覽**:使用者現在有介面可存取其內容結構 [!DNL Experience Manager] 啟動，包括在啟動中新增和移除頁面的功能。 此功能增強了 [!DNL Experience Manager] 啟動以製作鎖定於未來發佈的內容版本。 [時間扭曲功能](/help/sites-authoring/working-with-page-versions.md#timewarp) 可讓使用者將啟動預覽為未來的內容狀態。

* [!DNL Experience Manager] 直接在資料夾下顯示所有內容模型的清單，內容作者不必瀏覽檔案結構。 此功能現在需要的點擊次數更少，並且提高了製作效率。

* 路徑欄位 [!DNL Sites] 編輯器可讓作者從 [!DNL Content Finder].

* Platform提供幾項協助工具增強功能。 請參閱 [平台更新](/help/release-notes/sp-release-notes.md#platform-65100).

#### 能夠還原已刪除的頁和樹(6.5.9.0) {#ability-to-restore-pages-tree}

您現在可以還原已刪除的頁面，以及 [!DNL Experience Manager Sites] 頁面。

#### 排序可轉出的Live Copy頁面(6.5.8.0) {#sort-livecopy-pages}

您現在可以使用 [!UICONTROL 名稱], [!UICONTROL 上次修改日期]，和 [!UICONTROL 上次轉出日期] 屬性。 此 [!UICONTROL 上次轉出日期] 針對頁面是此版本中推出的新屬性。

#### 以非同步操作(6.5.7.0)提供頁面移動和MSM轉出 {#page-moves-msm-asynchronous}

您現在可以以非同步操作執行頁面移動和MSM轉出，以減少其對執行階段效能的影響。 您可以排程操作以立即執行或稍後執行。 相關作業和處理步驟的狀態會顯示在主控台中，這有助於監控大規模MSM轉出。

#### 非同步模式(6.5.6.0)中頁面移動操作的可用性 {#page-move-asynchronous}

「頁面移動」操作現在可以以非同步模式使用。 除了立即執行外，您還可以排程頁面移動操作，以供稍後執行。

#### 改善協助工具(6.5.5.0) {#accessibility-sites}

* 改善錯誤報告功能，新增文字資訊。

* 改善鍵盤導覽期間的使用者介面焦點。

* 改善各種使用者介面元素的對比率。

* 改善頁面影像的alt屬性一致性。

* 改善無障礙豐富網際網路應用程式(ARIA)標籤的一致性。

* 改善非視覺案頭存取(NVDA)功能。

* 改善螢幕助讀程式支援。

#### 其他重要增強功能(6.5.5.0) {#other-enhancements-sites}

* 不允許匿名訪問CRXDE Lite以增強安全性。 而是將使用者導向登入畫面。 請參閱 [使用CRXDE Lite開發](/help/sites-developing/developing-with-crxde-lite.md).

* 複製或貼上頁面樹時，您現在可以選擇貼上根頁面或使用樹的子頁面貼上根頁面。

* [!DNL Adobe Experience Manager Experience Fragments] 匯出至 [!DNL Adobe Target] 工作區現在會在中顯示為不重複的選件類型和選件來源 [!DNL Target].

* 多網站管理員 — 如果元件從來源頁面中刪除，則「發佈」觸發程式現在會從發佈的頁面中刪除元件。

* 多站點管理員 — 當 [!UICONTROL Live Copy] 與blueprint中元件的名稱相同，元件從blueprint中推出，然後再推出詞語 `_msm_moved` 現在已新增至本機元件的名稱。

#### 樣式系統增強功能(6.5.4.0) {#style-system-enhancements}

您現在可以使用增強樣式系統在元件對話方塊中選取樣式。

#### 不同領域的效能改善(6.5.4.0) {#performance-improvements}

* 縮短在網站內載入和初始化ContextHub的時間(`contexthub.kernel.js`)。 這會加快網站造訪期間的頁面載入速度。

* 縮短拖曳後重新整理頁面的時間 [!DNL Experience Fragments] to [!DNL Sites] 頁面編輯器。

* 縮短 [!DNL Sites] 超過200個即時副本的頁面 **[!UICONTROL 即時副本概述]**.

* 改善處理不完整或無效的URL。 這類URL會拖慢範本編輯器的速度。

### [!DNL Adobe Experience Manager Assets] {#aem-assets-previous-service-packs}

#### AEM 6.5.10.0版包含的功能 {#features-assets-65100}

* [!DNL Experience Manager] 將「連線資產」功能擴充至使用 [!DNL Dynamic Media] 影像。 請參閱 [使用連線資產](/help/assets/use-assets-across-connected-assets-instances.md).

* 將個別資產和集合共用為連結時(使用 [!UICONTROL 連結共用] 對話方塊)，使用者可以選擇讓接收者下載原始資產或其轉譯，或兩者。 請參閱 [透過連結共用資產](/help/assets/link-sharing.md).

   ![選項僅允許下載原始資產、僅允許轉譯，或同時允許](/help/release-notes/assets/share-assets-as-link.png)

* 當使用者下載以連結形式與他們共用的資產時，他們可以選擇下載原始資產、轉譯或兩者。

* **限制產生的子資產**:管理員可以限制 [!DNL Experience Manager] 為複合資產(如PDF、PowerPoint、InDesign和Keynote檔案)生成。

   ![限制子資產的產生](/help/assets/assets/sub-asset-limit.png)

* 新 [!DNL Camera Raw] 套件可支援 [!DNL Adobe Camera Raw] v10.4。見 [使用 [!DNL Camera Raw]](/help/assets/camera-raw.md).

#### 舊版 {#previous-releases-assets}

* 更新與香港、澳門及台灣相關的中文地區和地區的命名，使其與中國社會和政治觀點(6.5.9.0)一致。

* 導入了可選配置，以更改ACP API響應中的電子郵件ID的大小寫，其來源為 [!DNL Adobe Experience Manager] (6.5.9.0)。

   ![配置，在ACP響應中將電子郵件ID更改為小寫，從 [!DNL Experience Manager]](assets/email-lowcase-config.png)

* 針對各種功能，增強了背景中的文字和圖示對比度。 網頁內容可及性指引(WCAG)的這項實作可讓 [!DNL Assets] 視覺和顏色感知受限的使用者更容易存取。 請參閱 [協助工具增強功能 [!DNL Assets]](sp-release-notes.md#assets-accessibility-6590) (6.5.9.0)。
* 使用時 [連線資產功能](/help/assets/use-assets-across-connected-assets-instances.md)，您現在可以檢視 [!DNL Sites] 使用資產的頁面。 資產的這些參考可在資產的 [!UICONTROL 屬性] 頁面。 這可讓管理員、行銷人員和圖書館員全面了解資產使用情形，進而提供更佳的追蹤、管理和品牌一致性(6.5.8.0)。

* 刪除網頁中參考的資產時， [!DNL Experience Manager] 顯示警告。 您可以強制刪除參照的資產，或勾選並修改顯示在 [!DNL Properties] 頁面。 按一下參照會開啟本機和遠端 [!DNL Sites] 頁面(6.5.8.0)。

* [!DNL Assets] 和 [!DNL Dynamic Media] 提供多項協助工具增強功能。 這些增強功能與鍵盤導覽、螢幕助讀程式的使用、啟用輔助技術(AT)的類似增強功能有關。 請參閱 [[!DNL Assets] 增強功能](/help/release-notes/sp-release-notes.md#assets-6570) 和 [[!DNL Dynamic Media] 增強功能](/help/release-notes/sp-release-notes.md#dynamic-media-6570) (6.5.7.0)

* 使用者可以在「卡片」和「欄」檢視(6.5.7.0)中排序數位資產。

#### 協助工具增強功能(6.5.6.0) {#accessibility-assets-6560}

* **增強鍵盤導覽期間使用者介面的焦點**，例如，著重於：

   * `x` 圖示 [!UICONTROL 版本預覽] 中的資產對話方塊 [!UICONTROL 時間表].

   * 可操作的使用者介面選項。

   * 上的電子郵件欄位 [!UICONTROL 共用連結] 對話框和欄位，以在中添加封閉的用戶組 [!UICONTROL 權限] 資料夾標籤 [!UICONTROL 屬性].

* **使用鍵盤鍵的增強功能**

   使用者可以使用鍵盤鍵，在螢幕助讀程式的瀏覽模式中，拖曳中繼資料結構表單編輯器中的控制項。

* **增強螢幕助讀程式使用者的可用性**，原因如下：

   * 螢幕助讀程式會宣佈視訊和音訊播放器的用途。

   * 螢幕助讀程式會朗讀使用者介面選項的用途，以移除使用 [!UICONTROL 標籤選擇對話框] 在資產上 [!UICONTROL 屬性].

   * 螢幕助讀程式會朗讀表格的列標題和列項目，讓使用者知道哪些項目屬於同一列。

   * 搜尋頁面的描述性和有意義的頁面標題。

   * 螢幕助讀程式會將搜尋篩選器面板中的選項宣佈為可展開的折疊式訊息。

#### 中的其他增強功能 [!DNL Assets] (6.5.6.0) {#other-enhancements-assets-6560}

* 與資料夾（私人和非私人）相關聯的使用者群組現在會從 [刪除這些資料夾](/help/assets/private-folder.md#delete-private-folder). 不過，現有的備援、孤立、未使用和自動產生的使用者群組，可使用JMX從存放庫中移除。

#### 無障礙增強功能(位於 [!DNL Assets] (6.5.5.0) {#assets-accessibility}

[!DNL Experience Manager Assets] 現在，在符合網頁內容可及性指引(WCAG)的情況下，比以往更容易存取。 協助工具已改善，原因如下：

* 螢幕助讀程式可方便使用許多使用者介面元素、控制項、頁面和對話方塊。

* 許多使用者介面元素、控制項和輸入表單欄位都可使用鍵盤存取。

* 某些使用者介面元素的顏色和對比已更新，以便視力不良和無法分辨顏色的使用者區分這些使用者介面元素。例如，星級評等圖示的顏色(例如 [!UICONTROL 評等] 區段 [!UICONTROL 進階] 標籤 [!UICONTROL 屬性] 或卡片檢視中)已變更，以提供適當的對比。

   ![對比度改善的評等圖示](assets/star-rating-icons.png)

#### 增強的例外處理(6.5.5.0) {#exception-handling}

[!DNL Assets] 使用者介面流程的例外狀況處理較好。 如果資產的維度類型不完整，則觀察到的例外狀況會記錄在記錄檔中。

#### 設定 [!DNL Experience Manager Assets] with [!DNL Brand Portal] (6.5.4.0) {#configure-assets-bp}

之間的授權通道 [!DNL Experience Manager Assets] 和 [!DNL Brand Portal] 已變更。 之前， [!DNL Brand Portal] 是透過舊版OAuth閘道在傳統UI中設定，該閘道使用JWT權杖交換來取得IMS存取權杖以進行授權。 [!DNL Experience Manager Assets] 現在已設定為 [!DNL Brand Portal] through [!DNL Adobe I/O]，會擷取IMS代號以授權您的 [!DNL Brand Portal] 租用戶。

設定步驟 [!DNL Experience Manager Assets] with [!DNL Brand Portal] 視您的 [!DNL Experience Manager] 版本，以及您是第一次設定，還是升級現有設定。 請參閱 [使用Brand Portal設定Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html) 以取得詳細資訊。

#### 協助工具增強功能(6.5.4.0) {#accessibility-enhancements-6540}

[!DNL Experience Manager Assets] 包括下列協助工具增強功能：

* 鍵盤上的箭頭鍵可用於移動和平移縮放影像中的區域。 如需詳細資訊，請參閱 [僅使用鍵盤鍵預覽資產](../assets/manage-assets.md#previewing-assets).

* 螢幕助讀程式可讀取「篩選器」面板中的混合狀態核取方塊（除非您選取所有巢狀述詞，否則不會選取第一層核取方塊，且會經過）。

* 日期欄位的欄位標籤中提供日期和時間格式限制，以便用戶使用鍵盤以正確的格式輸入日期。
例如， `On Time (MM-DD-YYYY HH:mm)`. 此處MM為兩位數格式的月， YYYY為年，DD為兩位數格式的日，HH為24小時軍事格式的小時，而mm為分鐘。

* 螢幕助讀程式會朗讀移除所選標籤的選項(`X` 符號)和所選標籤的編號。

#### 清單檢視中資產建立日期的可排序欄(6.5.3.0) {#sortable-date-created-column}

DAM清單檢視和清單檢視的資產搜尋結果中，會新增可供排序的資產建立日期欄。

![建立日期的可排序列](assets/asset-created-date.png)

#### 視覺搜尋 [!DNL Adobe Experience Manager Assets] (6.5.2.0) {#visual-search}

[!DNL Assets] 使用者可以搜尋視覺上類似的影像。 Experience Manager會顯示來自DAM存放庫的智慧型標籤影像，這些影像類似於使用者選取的影像。 請參閱 [視覺搜尋](../assets/search-assets.md).

### Dynamic Media {#dynamic-media-previous-service-packs}

* 許多協助工具增強功能都在 [!DNL Dynamic Media] 用戶端，讓螢幕助讀程式能提供動作或使用者介面的更適當且實用的說明。 請參閱 [[!DNL Dynamic Media] 更新](/help/release-notes/sp-release-notes.md#dynamic-media-65100) (6.5.10.0)。

* [[!DNL Dynamic Media] 更容易存取](sp-release-notes.md#assets-accessibility-6590) 在以下方面：

   * 使用鍵盤鍵的易用性。
   * 對比（與背景）各種編輯器中的文字、預留位置文字和控制項。
   * 依螢幕助讀程式的協助工具和旁白。

* 借助智慧影像處理DPR（設備像素比率）和網路頻寬優化，在具有高解析度顯示器和受限網路頻寬的設備上高效地提供最佳質量影像。 請參閱 [智慧型影像處理常見問題集](/help/assets/imaging-faq.md) (6.5.9.0)。

* [!DNL Dynamic Media] 傳送(`fmt` URL修飾元)現在支援新一代影像格式AVIF（AV1影像格式）。 如需詳細資訊和時間表，請參閱 [影像提供與轉譯API fmt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html) (6.5.9.0)。

#### 支援3D資產，於 [!DNL Dynamic Media] (6.5.5.0) {#support-for-3d}

支援 [!DNL Dynamic Media] 可讓客戶發佈3D內容，並將其新增至網頁和應用程式。 支援包括：

* 發佈常見的3D資產格式並產生可用於網頁和其他應用程式的資產URL。

* 3D Web Viewer，由 [!DNL Adobe Dimension]，以互動方式檢視已發佈的3D資產。

* 在上發佈和檢視常見3D資產 [!DNL Experience Manager Sites] 頁面使用 [!DNL Sites] WCM元件。

#### 使CDN快取內容(6.5.6.0)無效 {#invalidate-cdn-cached-content}

您現在可以使用 [!DNL Dynamic Media] 使內容傳遞網路(CDN)快取內容無效的使用者介面。 因此，更新後的資產可立即使用，而無需等待快取過期。 您可以透過下列方式使CDN失效：

* 建立CDN失效範本：選取與範本相關聯的資產和表單

* 透過資產選擇器選取資產和相關的預設集

* 新增完整資產URL

#### 選擇性將資產發佈至 [!DNL Experience Manager] 和 [!DNL Dynamic Media] (6.5.6.0) {#selective-publishing}

您現在可以選擇選擇性地發佈或取消發佈資產至 [!DNL Experience Manager] 或 [!DNL Dynamic Media] 使用 [!UICONTROL 快速發佈] 或 [!UICONTROL 管理出版物] 嚮導。 您也可以設定 `Publish` 或 `Unpublish` 模式。

#### 適用於Dynamic Media的智慧型影像處理 {#smart-imaging}

智慧型影像處理使用每個使用者的獨特檢視特性，自動提供針對其體驗最佳化的適當影像，進而提升效能和參與度。 智慧型影像處理可與您現有的影像預設集搭配使用，並會在傳送時的最後毫秒內運用智慧，根據瀏覽器或網路連線速度進一步縮小影像檔案大小。 請參閱[智慧型影像](../assets/imaging-faq.md)。

#### Dynamic Media適用的視訊描述檔智慧型裁切(6.5.3.0) {#smart-crop-video}

智慧型裁切視訊 — 視訊描述檔中提供的選用功能 — 使用Adobe Sensei來自動偵測和裁切任何最適化視訊或漸進式視訊中的焦點（不論大小）。 請參閱 [關於在視訊設定檔中使用智慧型裁切](../assets/video-profiles.md).

### Experience Manager Forms {#aem-forms-previous-service-packs}

#### AEM 6.5.10.0版包含的功能 {#features-forms-65100}

>[!NOTE]
>
>的附加套件 [!DNL Experience Manager Forms] 在排程後一週內可供使用 [!DNL Experience Manager] Service Pack版本。

* 您現在可以使用Automated forms conversion服務 [以法文、德文、西班牙文、義大利文和葡萄牙文轉換PDF forms](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html#language-specific-meta-model) 最適化表單。

* **屬性瀏覽器中的錯誤訊息**:已針對適用性Forms屬性瀏覽器中的每個屬性新增錯誤訊息。 這些訊息有助於了解欄位的允許值。

* **支援使用常值選項來設定JSON類型變數的值**:您可以在AEM工作流程的設定變數步驟中使用文字選項來設定JSON類型變數的值。 文字選項可讓您以字串的形式指定JSON。

* [平台更新](../forms/using/aem-forms-jee-supported-platforms.md): [!DNL Adobe Experience Manager Forms] on JEE已新增對下列平台的支援：
   * [!DNL Adobe Acrobat 2020]
   * [!DNL Ubuntu 20.04]
   * [!DNL Open Office 4.1.10]
   * [!DNL Microsoft Office 2019]
   * [!DNL Microsoft Windows Server 2019]
   * [!DNL RHEL8]

* 新增 `GuideBridge#getGuidePath` API [!DNL AEM Forms].

#### 支援 [!DNL Azul Zulu OpenJDK] (6.5.9.0) {#support-azul-zulu}

您現在可以使用 [!DNL Azul Zulu] 組建 [!DNL OpenJDK] for [!DNL Experience Manager Forms] 在OSGi部署上。 如需詳細資訊，請參閱 [Experience Manager6.5 Service Pack 9發行說明](sp-release-notes.md) 和 [技術需求](../sites-deploying/technical-requirements.md).

#### 可使用 [!UICONTROL 分配任務] (6.5.9.0) {#group-notification-email}

您現在可以使用「指派工作」工作流程步驟，傳送通知電子郵件至群組電子郵件地址。

#### 修改源互動式通信(6.5.9.0)後檢索互動式通信草稿的功能 {#retrieve-draft-after-source-modifications}

您現在可以在變更來源互動式通訊後，擷取儲存為草稿的互動式通訊。

#### 為載入、呈現和驗證reCAPTCHA服務(6.5.9.0)設定自訂網域名稱 {#set-custom-domain-name-recaptcha}

reCAPTCHA服務使用 `https://www.recaptcha.net/` 作為預設網域。 您現在可以修改設定 `https://www.google.com/` 或任何要載入、呈現及驗證reCAPTCHA服務的自訂網域名稱。

#### 的輸入資料增強功能 [!UICONTROL 調用表單資料模型服務] 工作流程步驟(6.5.9.0) {#input-data-enhancements-fdm}

當您在 [!UICONTROL 調用表單資料模型服務] 工作流步驟，可為輸入資料指定服務參數。

如果您選取 [!UICONTROL 相對於裝載] 選項附加檔案作為服務參數，您現在可以指定包含檔案的資料夾路徑，而不是實際的檔案名。 定義資料夾名稱（而不是檔案附件名稱）可讓您重複使用工作流模型。 不將工作流模型限制為單個檔案附件名稱。

#### 在「記錄文檔」模板中使用多個首頁(6.5.9.0) {#use-multiple-master-pages-dor-template}

您現在可以在「記錄文檔」模板中使用多個首頁。 因此，您現在可以在標題頁面和範本的其他頁面上擁有不同的頁首、頁尾、字型、標誌資訊。

#### 記錄檔(6.5.9.0)中的支援分頁 {#support-page-breaks-dor}

您現在可以將分頁符新增至記錄檔。 因此，如果某個面板在頁面內斷開，您可以添加分頁符，以將該面板移動到「記錄文檔」中的新頁面。

#### 根據規則(6.5.8.0)在最適化表單中顯示或隱藏CAPTCHA元件 {#show-hide-captcha}

您現在可以在最適化表單提交或使用者動作上驗證驗證驗證碼。 您也可以新增條件來驗證使用者動作的驗證CAPTCHA，並根據規則在最適化表單中顯示或隱藏CAPTCHA元件。

#### 新增自訂驗證碼服務(6.5.8.0) {#add-custom-captcha-services}

[!DNL Experience Manager Forms] 提供立即可用的支援，將Google reCAPTCHA(需要Google reCAPTCHA API的個別授權)作為CAPTCHA驗證服務使用。 您也可以使用自訂驗證碼服務來驗證驗證驗證碼。

#### 其他增強功能(6.5.8.0) {#other-enhancements-forms-6580}

* 改善 [!DNL Experience Manager Forms] 日期選擇器元件。

* 新增支援，以使用PrintChannel API以PCL格式生成互動式通信。

* 執行PDFG轉換時，您現在可以啟用或停用 [!DNL Experience Manager Forms] 產生自訂書籤的註冊表變更。

#### 效能改善(6.5.7.0) {#performance-improvements-forms}

[!DNL Experience Manager] 6.5 Service Pack 7 Forms改善以下項目的效能：

* 在提交最適化表單時驗證伺服器上的欄位值。

* 使用將PDF表單轉換為最適化表單 [!DNL Automated Forms Conversion service].

#### 支援Microsoft SQL Server 2016始終在高可用性(6.5.7.0)的可用性組上 {#always-on-availability-groups}

[!DNL Experience Manager Forms] 現在支援 [!DNL Microsoft] SQL Server 2016始終處於可用性組中，以實現OSGi部署的高可用性。

#### 表單資料模型HTTP用戶端設定，以最佳化效能(6.5.7.0) {#fdm-http-client-config}

[!DNL Experience Manager Forms] 表單資料模型已與RESTful網站服務整合，可作為資料來源使用，現在包含可最佳化效能的HTTP用戶端設定。 請參閱 [設定資料來源](../../help/forms/using/configure-data-sources.md#fdm-http-client-configuration).

#### 在「佈局」模式(6.5.7.0)中，每個元件的「重置選項」的可用性 {#reset-option-layout-mode}

您現在可以在最適化表單的「版面」模式中，針對每個元件使用重設選項。 為面板定義多列佈局時，可以使用此功能重置面板內的各個元件。 請參閱 [使用版面模式調整元件大小](../../help/forms/using/resize-using-layout-mode.md#resize-components).

#### 在用戶端預填最適化表單(6.5.6.0) {#prefill-merge-data-at-client}

預填最適化表單時， [!DNL Experience Manager Forms] 伺服器將資料與最適化表單合併，並將填寫的表單傳送給您。 依預設，資料合併動作會在伺服器上發生。
您現在可以設定 [!DNL Experience Manager Forms] 伺服器 [在客戶端執行資料合併操作](../../help/forms/using/prepopulate-adaptive-form-fields.md) 而非伺服器。 大幅縮短預填及演算最適化表單的所需時間。

#### 透過雙向SSL實作(6.5.6.0)整合伺服器上的表單資料模型與RESTful API {#fdm-integration-rest-apis-two-way-ssl}

[!DNL Experience Manager Forms] 表單資料模型現在可以 [與伺服器上已實作雙向SSL的RESTful API整合](../../help/forms/using/configure-data-sources.md).

#### 新增 [!DNL Adobe Sign] automated forms conversion服務(6.5.6.0)中的文字標籤 {#sign-integration-acroform-afcs}

如果AcroForm包含 [!DNL Adobe Sign] 文字標籤中，這些欄位現在可辨識並顯示為 [!DNL Adobe Sign] 使用 [!DNL Automated Forms Conversion service]. 簽署者可在簽署最適化表單時填入此類欄位。

#### 支援將彩色PDF forms轉換為最適化表單(6.5.6.0) {#colored-PDF-forms}

您可以使用 [!DNL Automated Forms Conversion service] 將彩色PDF forms轉換為最適化表單。

#### 支援SMB 2和SMB 3協定(6.5.6.0) {#smb-support}

[!DNL Experience Manager Forms] 現在支援SMB 2和SMB 3協定。

#### 增強轉譯的最適化表單頁面快取功能(6.5.6.0) {#enhanced-caching-translated-adaptive-forms}

您現在可以指定 [地區設定為適用性表單URL中的選取器，而非適用性表單URL中的引數](../../help/forms/using/supporting-new-language-localization.md). 可協助您在 [!DNL Experience Manager Dispatcher]. 舊版無法快取轉譯的最適化表單。 如需在適用性表單URL中將區域設定為選取器的快取的詳細資訊，請參閱 [在Dispatcher設定最適化表單快取](../../help/forms/using/configure-adaptive-forms-cache.md).

#### 將表單資料模型服務的輸出儲存至變數(6.5.6.0) {#save-fdm-service-to-variable}

表單資料模型可讓您將表單資料模型服務的輸出儲存至變數。 [!DNL Experience Manager Forms] 現在會自動將表單資料模型服務的類型對應至變數的類型。

#### 為檔案附件元件(6.5.6.0)附加多個檔案 {#attach-multiple-files}

您現在可以 [附加多個檔案](../../help/forms/using/introduction-forms-authoring.md) 到 [!UICONTROL 檔案附件] 最適化表單的元件。

#### 自訂Adobe Experience Manager收件匣欄(6.5.5.0) {#customize-aem-inbox-columns}

您可以自訂 [!DNL Experience Manager] 收件箱：更改列的預設標題、重新排序列的位置，以及根據工作流的資料顯示其他列。 成員 `administrators` 或 `workflow-administrators` 群組可自訂欄。 如需詳細資訊，請參閱 [管理控制](../sites-authoring/inbox.md#inbox-admin-control).

![自訂Experience Manager收件匣欄](assets/customize-columns.gif)

#### 將互動式通訊儲存為草稿(6.5.5.0) {#save-as-draft}

您可以使用代理UI為每個互動式通訊儲存一或多個草稿，並稍後擷取草稿以繼續處理。 您可以為每個草稿指定不同的名稱以加以識別。 如需詳細資訊，請參閱 [將互動式通訊儲存為草稿](../forms/using/prepare-send-interactive-communication.md#save-as-draft).

![另存為草稿](assets/save-as-draft.gif)

#### [!DNL Oracle WebLogic] 應用程式伺服器支援(6.5.5.0) {#weblogic-support}

Adobe Experience Manager Forms已新增 [!DNL Oracle WebLogic 12] Adobe Experience Manager Forms的JEE版。 您可以從舊版升級，或在JEE伺服器上設定新的Experience Manager6.5 Forms [!DNL Oracle WebLogic] 12.2.1.4和更新版本。 稍後版本會與次要版本變更相對應，其中12.2.1.x中的x會以版本號碼取代。

#### 改善協助工具(6.5.5.0) {#accessibility-improvements}

Adobe Experience Manager Forms包含下列協助工具增強功能：

* 當使用者以HTML表單預覽最適化表單時， [!UICONTROL 手寫簽名] 欄位會保留標籤焦點。

* 提交最適化表單時顯示的錯誤訊息現在包含 `aria-describedBy` 屬性。 屬性會附加至錯誤訊息中參考的欄位。 此 `aria-describedby` 屬性表示描述對象的元素的ID。 它有助於建立介面工具集或組與描述它們的文本之間的關係。

* 如果適用性表單有一些必填欄位，則必填屬性會設為 `True` 在ARIA協助工具架構中的這些欄位。

#### X-509以憑證為基礎的驗證，適用於表單資料模型(6.5.5.0)中以SOAP為基礎的Web服務 {#x509-based-authentication-soap}

表單資料模型現在支援X-509憑證式驗證，同時使用SOAP網站服務作為資料來源。 如需詳細資訊，請參閱 [配置SOAP Web服務](../forms/using/configure-data-sources.md#configure-soap-web-services).

#### 其他重要改善項目(6.5.5.0) {#other-improvements}

* Experience Manager6.5 Forms JEE檔案安全性現在是以 [!DNL Apache Struts 2].

* 新增 [!DNL Oracle Real Applications Cluster (RAC) 19c].

#### 在Experience Manager Forms工作流程(6.5.4.0)中產生可列印的輸出 {#generate-printable-output}

「生成可打印輸出」(Generate Printable Output)工作流步驟允許您將源模板檔案與資料檔案整合。 此整合可讓您列印或儲存範本檔案的不同副本。 此步驟將生成PCL、PostScript、ZPL、IPL、TPCL或DPL輸出。 如需此功能的詳細資訊，請參閱 [Forms上以OSGi為中心的工作流程 — 步驟參考](../forms/using/aem-forms-workflow-step-reference.md).

![產生可列印的輸出](assets/generate-print-output-step.gif)

#### 以版面模式(6.5.4.0)支援最適化表單和互動式通訊的多欄 {#multi-column-adaptive-forms}

您現在可以在最適化表單和互動式通訊中定義面板的欄數。 切換至配置模式，以使用新的多欄選項。 如需詳細資訊，請參閱 [使用「版面」模式調整元件大小](../forms/using/resize-using-layout-mode.md).

![多欄配置](assets/multi-column-layout.gif)

#### Experience Manager收件匣自訂(6.5.4.0) {#aem-inbox}

新的「管理控制」選項可讓管理員：

* 自訂標題文字和標誌。

* 控制標題中可用導覽連結的顯示。

「管理控制」選項只對 `administrators` 或 `workflow-administrators` 群組。 如需此功能的詳細資訊，請參閱 [您的收件匣](../sites-authoring/inbox.md).

#### HTML5表單(6.5.4.0)的RTF支援 {#rich-text-support}

將XFA表單中的文字欄位轉換為HTML5表單中的RTF欄位。 如需詳細資訊，請參閱 [為HTML5表單設計表單模板](../forms/using/designing-form-template.md).

#### 協助工具增強功能(6.5.4.0) {#forms-accessibility-enhancements-6540}

Experience Manager Forms包含下列協助工具增強功能：

* 螢幕助讀程式會在最適化表單中正確宣佈核取方塊、連結、日期選取器和日期輸入欄位。

* 適用性表單的每個頁面現在都包含一個標題和一個主要地標標籤。

#### 共用並請求存取Experience Manager Forms使用者的收件匣項目(6.5.3.0) {#share-request-access}

您可以與其他使用者共用您的收件匣項目。 一旦其他使用者取得您收件匣項目的存取權，該使用者就可以對共用項目提出宣告並採取適當動作。 同樣地，您也可以向其他使用者申請「收件匣」項目的存取權。 請參閱 [共用並請求對用戶收件箱項的訪問](../forms/using/configure-shared-queues-osgi.md).

#### 為Experience Manager Forms使用者(6.5.3.0)的收件匣項目設定離職設定 {#configure-out-of-office}

如果您打算不在辦公室，您可以指定該期間分配給您的項目有何變化。
您可以選擇指定開始日期和時間，以及結束日期和時間，以便讓離職設定生效。 您可以設定將所有項目傳送至的預設人員。 請參閱 [配置外出設定](../forms/using/configure-out-of-office-settings.md).

#### 使用Experience Manager Forms適用的批次API(6.5.3.0)產生多種互動式通訊 {#generate-multiple-ic}

您可以使用批次API從範本產生多個互動式通訊。 範本是互動式通訊，不含任何資料。 批次API將資料與範本結合，以產生互動式通訊。 API在大量生產互動式通訊中很有用。 例如，電話單、多個客戶的信用卡對帳單。 請參閱 [使用批次API產生多種互動式通訊](../forms/using/generate-multiple-interactive-communication-using-batch-api.md).

<!-- TBD: Check if the wider team released anything in FY21.
-->

## 以下版本的重要發行 [!DNL Adobe Experience Manager] 6.5 SP9 {#key-releases-since-last-sp}

2021年5月27日至2021年8月26日期間，除了Service Pack外，Adobe還發行了下列內容：

* [!DNL Adobe Experience Manager] as a Cloud Service [2021.6.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/2021/release-notes-2021-6-0.html), [2021.7.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/2021/release-notes-2021-7-0.html)，和 [2021.8.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html).

* [[!DNL Experience Manager] 案頭應用程式2.1(2.1.3.3)](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html).

* [Experience Manager Screens:Feature Pack 202105](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/release-notes/release-notes-fp-202105.html)

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5檔案](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hant)
>* [的一般發行說明 [!DNL Experience Manager] 6.5](release-notes.md)
>* [適用於 [!DNL Experience Manager] 6.5](sp-release-notes.md)

