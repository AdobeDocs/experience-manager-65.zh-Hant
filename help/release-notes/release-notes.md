---
title: 的發行說明 [!DNL Adobe Experience Manager] 6.5
description: 查找發行資訊、新功能、安裝操作說明，以及 [!DNL Adobe Experience Manager] 6.5。
mini-toc-levels: 3
exl-id: 0288aa12-8d9d-4cec-9a91-7a4194dd280a
source-git-commit: 21cbb1df659c8ff82170bb953b05260219dc4970
workflow-type: tm+mt
source-wordcount: '3237'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager] 6.5最新Service Pack發行說明 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession&cid=a915e87c-369a-480c-9daf-d13efc766798 -->

## 發行資訊 {#release-information}

| 產品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.14.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 類型 | Service Pack發行 |
| 日期 | 2022 年 8 月 25 日 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 下載 URL | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.14.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## 包含的項目 [!DNL Experience Manager] 6.5.14.0 {#what-is-included-in-aem-6514}

[!DNL Experience Manager] 6.5.14.0包含自2019年4月初次發行6.5以來所推出的新功能、客戶要求的重要增強功能、錯誤修正以及效能、穩定性和安全性等改善項目。 [安裝此Service Pack](#install) on [!DNL Experience Manager] 6.5。 <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_

* Added support for password reset for Dynamic Media Classic users within Experience Manager. (ASSETS-10298) -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets] {#assets-6514}

* 無法為PDF檔案添加或查看標籤。 (NPR-38452)
* 當您設定「連線資產」、儲存設定、重新開啟設定頁面，並測試已儲存的設定時，測試連線會失敗。 (NPR-38507)
* 無法將具有數值用戶ID的用戶添加到集合。 (NPR-38538)
* Experience Manager無法處理安裝在製作執行個體上的FFmpeg。 (NPR-38568)
* PDF處理失敗，因為 `NoClassDefFoundError` 錯誤訊息。 (NPR-38741)
* 為建立資產報表時，自訂欄下方的新增按鈕無法正確顯示 `de_DE` 地區。 (ASSETS-10641)
* 將重複資產上傳至數位資產管理存放庫時，Experience Manager會偵測到並提供刪除重複資產的選項時，原始資產也會從存放庫中刪除。 (ASSETS-10826)
* 在多欄位中指定特殊字元時，Experience Manager無法正確儲存資料夾中繼資料。 (ASSETS-10721)
* 在您按一下「 **[!UICONTROL 儲存並關閉]** 兩次。 (ASSETS-12040)
* 螢幕助讀程式只會朗讀 `Relate` 按鈕。 不過， `Relate` 按鈕也包含子菜單，可以展開和折疊。 (ASSETS-6938)
* 必要的ARIA（可存取的Rich Internet Applications）屬性 `aria-expanded` for `role="combo box"` 缺少。 (ASSETS-6928)
* 在「卡片」視圖中，在主檔案導航區域中，文本內容 **[!UICONTROL 排序依據]** 其背景顏色的對比度不至少為4.5:1。 (ASSETS-6926)
* Experience Manager不識別 **[!UICONTROL 選擇工作流模型]** 建立工作流程模型時，將下拉式清單列為必要欄位。 (ASSETS-6871)

>[!NOTE]
>
>自2022年9月1日起，新的Experience Manager Assets內部部署客戶將無法使用智慧內容服務。 已啟用此功能的現有內部部署和Adobe Managed Services客戶不受影響。

### [!DNL Dynamic Media] {#dynamic-media-6514}

* 新增對Dynamic Media Classic使用者Experience Manager內密碼重設的支援。 (ASSETS-10298)
* 為具有透明背景的影像生成的智慧裁切具有白色背景。 (ASSETS-13148)
* Dynamic Media不會為EPS檔案產生縮圖。 (ASSETS-10959)
* 因為遺失上傳參數，資產無法上傳至Dynamic Media帳戶。 (ASSETS-13165)
* 允許將名稱超過127個字元的資產上傳至Dynamic Media。 (ASSETS-9991)
* 在Experience Manager6.5.14.0上為Dynamic Media檢視器啟用JavaScript ES6(ECMAScript 6)。 (NPR-38393)
* 在Dynamic Media中設定選項 **[!UICONTROL 一般設定]** 和 **[!UICONTROL 發佈設定]** 不應由非管理員使用者存取。 (ASSETS-8628)
* Dynamic Media **[!UICONTROL 一般設定]** 頁面未正確顯示已設定的上傳參數。 (ASSETS-10245)
* Experience Manager使用者介面不會顯示任何失敗訊息，以防集建立/更新失敗。 (ASSETS-10264)
* 無法將已儲存的原則套用至可編輯範本的其中一個容器，以讓您新增Dynamic Media元件。 (ASSETS-11044)
* 對作業處理不正確的資產執行「Dynamic Media重新處理資產」工作流程後，資產無法上傳至Dynamic Media帳戶。 (ASSETS-12084、ASSETS-9877)
* 螢幕助讀程式的使用者會受到 `title` 未為提供屬性 `<frame>` 和 `<iframe>` 在 **[!UICONTROL 要搜索的類型]** 對話框。 (ASSETS-5483)
* 在螢幕助讀程式中，相關且有意義 `alt=` 值應提供給下方顯示的多個影像 **[!UICONTROL 資產]** 標題。 (ASSETS-5644)
* 螢幕助讀程式未讀取 **[!UICONTROL 靜音]** 和 **[!UICONTROL 取消靜音]** 按鈕(在使用Dynamic Media元件的視訊上)。 (ASSETS-10169)

## 商務 {#commerce-6514}

* 未使用欄標題排序商務產品，而是使用 _遠端_ 排序模式；相反地，商務產品應使用欄標題和 _本地_ 排序模式。 (CQ-4343750、NPR-38498)

## [!DNL Forms] {#forms-6514}

* 將檔案附加至多面板最適化表單，並儲存最適化表單的草稿時，會發生錯誤。 (NPR-38978)
* 當使用者使用createPDF2 Java API搭配AdobePDF設定將RGB描述檔轉換為CMYK描述檔時，選項無法與Java API搭配使用。 該選項與獨立DistillerClient應用程式無關。 (NPR-38858、CQ-4346181)
* 安裝AEM 6.5 Forms Service Pack 12(6.5.12.0)後，除了關閉工作之外，所有選項都無法在AEM工作流程的「指派工作」步驟中使用。 (NPR-38743)
* 在記錄文檔(DoR)中，表中的某些值被截斷。 (NPR-38657)
* 使用資料XML預覽FormSet時，當XDP包含浮動欄位時，預覽FormSet時不會顯示任何資料，但使用「預覽PDF」選項時會顯示資料。
* 在適用性Forms中，選項按鈕和核取方塊未依索引標籤順序排列。 (NPR-38645)
* 若您使用 `Summary Step` 要在提交表單後為已翻譯的最適化表單生成記錄文檔(DoR)，不會翻譯為本地化語言。 (NPR-38567)
* AEM工作流程步驟中的停用重試選項未如預期運作。 問題似乎間歇性出現。 (NPR-38547)
* 使用RTF欄位提交適用性表單時， `an Internal Error while Submitting a Form` 發生錯誤。 當使用者在表單提交前將焦點放在RTF欄位上時，不會發生錯誤。 (NPR-38542)
* 錯誤 `sling-default-3-AdobeSignRefreshTokenScheduleJob com.adobe.forms.foundation.oauth.model.OAuthConfigSlingModel Refresh Token not present for: /conf/gws-eform/cashlite/settings/cloudconfigs/fdm/cashlite/jcr:content occurs` 已記錄。 (NPR-38541)
* 當使用者上傳PDF至適用性表單時，AEM Forms伺服器會停止回應。 (NPR-38398)
* 在OSGi伺服器上的AEM Forms上，當您使用檔案服務API來驗證PDF時，系統會失敗，並出現錯誤：com.adobe.fd.signatures.truststore.errors.exception.CredentialRetrievalException:AEM-DSS-311。 (CQ-4346252)
* 在提交信函草稿時， `Could not upload asset from xml input` 發生錯誤。 對功能沒有影響。 開啟草稿時，字母會正確轉譯。 (CQ-4345979、CQ-4344418)
* 以德文格式輸入日期時， `Preview with Data` 選項用於信函，則不會呈現「日期」欄位。 (CQ-4345783)
* 當您建立Web門戶並根據資料生成條形碼時，某些條形碼無法正確解碼。 (CQ-4345743)
* 轉換到PDF的Postscript不會以預期的顏色呈現輸出文檔。 (CQ-4345074)
* 資源解析器會造成間歇性提交失敗，並導致同一堆疊追蹤在單一提交中出現多次。 (CQ-4344764)
* 使用者無法開啟使用的修改草稿信函 `cmDataUrl` 參數。 草稿首次開啟。 問題會在後續嘗試中開始出現。 (CQ-4344418)
* 當使用者進入 `&` 在交互通信(IC)中的符號，相應IC的草稿無法載入。 (CQ-4343969)
* 使用AEM Forms Designer中的樣式選項生成PCL檔案時，指定的樣式不會應用於生成的檔案。 (CQ-4339573)
* 當頁數超過15時，將動態XDP表單自動轉換為最適化表單失敗。 當頁數小於15時，此功能可正常運作。 (NPR-35337)
* 使用「新增至我的最愛」選項時，不會指出切換至螢幕助讀程式的狀態。 (NPR-37137)
* 在表單資料模型中，資料庫支援的表單資料模型中小數後的值會因金錢和小額金錢資料類型而截斷。. (CQDOC-19509)
* 當您在HTML工作區中為工作流程選取導覽連結時，不會指出已選取導覽連結。 (NPR-37138)
* 手寫簽名功能與輔助工具指南不相容。 (NPR-37596)
* AEM Forms使用log4j 1.x。log4j 1.x支援已終止。 (NPR-38273)
* 在「表單資料模型」中將MSSQL資料庫用作資料源並檢索值時，檢索值中小數後的數字將被切換。 (CQ-4346190)
* 在Forms 6.5 Designer中，當您開啟以Forms 6.1 Designer建立的表單並編輯文本框時，段落間距超過指定的空間。 空間的所有先前設定都將被刪除，並且需要手動重新格式化文本框。 (CQ-4341899)
* 條形碼SSCC-18顯示的值不正確。 Forms伺服器會忽略條碼右側的值。 (CQ-4342400)
* 針對以Forms 6.5 Designer建立的靜態PDF forms,PDF協助工具會因錯誤而失敗 `Tab order entry in page with annotations not set to "S"`. (CQ-4343117)
* 新增在Forms Designer中為超連結指定「螢幕Reader文字」的功能。(NPR-36221)


## Integrations {#integrations-6514}

* 啟用JavaScript ES6（ECMAScript6模式或更佳）編譯支援，以縮制 `/libs/cq/analytics/widgets.js` 程式庫。 (NPR-38433)
* 啟用JavaScript ES6（ESMAScript6模式或更高）編譯支援，以縮制 `/libs/cq/testandtarget/clientlibs/testandtarget/util.js` 程式庫。 (NPR-38435)
* 中的內容越多 `/content/campaigns`，呼叫的時間會越久 `targeteditor.html` (`/libs/cq/personalization/touch-ui/content/targeteditor.html`)會在您開啟頁面編輯器時使用。 (NPR-38663)

## 平台 {#platform-6514}

* 無法登入套件管理器以部署更新。 (NPR-38646)
* 在資產標籤選取器使用者介面中，標籤會以其建立順序顯示。 不過，當有許多標籤時，檢視和管理標籤會很困難，因為無法排序。 (CQ-4344279)
* 當管理員或使用 **[!UICONTROL 模擬為]** 欄位。 (CQ-4345288)
* 在智慧型集合中，使用儲存的搜尋進行篩選時，會顯示所有資產。 (CQ-4345326)
* 針對顯示錯誤的選取資產計數 **[!UICONTROL 新增至集合]** when **[!UICONTROL 全選]** 中所有規則的URL。 (CQ-4345424)
* 使用 **[!UICONTROL 模擬為]** 欄位（包含群組或不存在的使用者）。 (CQ-4346098)

## [!DNL Sites] {#sites-6514}

* 將Experience Manager從6.5.12.0升級到6.5.13.0時，出現意外的路徑刪除。 (NPR-38532)

### 協助工具 {#access-6514}

* 在Experience Manager Sites中，當您將 **[!UICONTROL 切換顯示格式並調整顯示設定]** 按鈕，然後選取 **[!UICONTROL 清單檢視]**, **[!UICONTROL 拖放]** 按鈕缺少可存取的名稱。 (SITES-2863、NPR-38760)
* 螢幕助讀程式必須朗讀可存取的名稱，例如 `Show description for Archive` 或 `Show description for mini shopping cart`. 不過，目前可存取的名稱會宣佈為 `Info Circle button show description` for _all_ 工具提示資訊按鈕。 (SITES-3104)
* 改善沒有內嵌編輯或dropTarget功能的元件的還原，位於 `cq:editConfig`. (NPR-38361) <!-- version 2 (old) of the description above * When out of the box components that don't have inlineEditing or dropTarget feature in the _cq_editConfig file (navigation, breadcrumb, embed) are deleted > undeleted (by way of Undo), all configurations are lost and empty placeholder reappears. Component must be reconfigured from scratch. (NPR-38361) -->
* 對於使用的元件，樣式系統下拉式清單可能位於頁面頂端，而非元件的內容 `cq:editConfig` &quot;afteredit:REFRESH_PAGE」。 (NPR-38384) <!-- version 2 (old) of description above* When selecting a style option on a component, the Styles box shifts to the upper left corner of the screen, rather than staying put below the style icon. Happens for components that have  cq:editConfig "afteredit: REFRESH_PAGE". (NPR-38384) -->
* 新增至巢狀「版面容器」時，文字元件不會對齊。 (NPR-38193)
* 當元件沒有樣式系統配置時，將顯示空樣式頁簽。 現在，若未進行任何設定，則會隱藏索引標籤。 (NPR-38218) <!-- version 2 (old) of description above * Style tab is blank on components without styles/policies. (NPR-38218) -->
* 屬性 `useLegacyResponsiveBehaviour` 只有在通過驗證時才有效。 (NPR-37996)
* 將jquery-ui升級至最新版本導致編輯器中斷。 (SITES-5647)

### [!DNL Content Fragments] {#sites-contentfragments-6514}

* 內容片段列舉欄位在首次載入內容片段時發生驗證問題。 (SITES-7140)
* 需要在內容片段編輯器的RTF編輯器中新增Campaign個人化欄位。 (NPR-38526)
* 在內容片段編輯器中建立或編輯新內容片段時，透過Dispatcher時，不會儲存內容片段模型。 此外，內容片段編輯器未關閉，且瀏覽器記錄中會顯示錯誤。 (NPR-38691)
* 永久性查詢驗證錯誤。 (NPR-38523)
* 在「內容片段」對話方塊中，於 **[!UICONTROL 屬性]**, **[!UICONTROL 內容片段]** 欄位不會保留選取快顯視窗中儲存的路徑。 (NPR-38632)
* 當您建立內容片段模型並新增下拉式清單類型的列舉欄位時，會進行正確的驗證 _`is required`_失敗。 (NPR-38237)

### 核心元件 {#sites-corecomponents-6514}

* 編輯時，新的「頁面電子郵件」元件不應強制您進入傳統使用者介面 `/etc`. (NPR-38648)

### 頁面編輯器 {#sites-pageeditor-6514}

* 使用者無法將元件調整為所需欄數。 (NPR-38688)

### 範本編輯器 {#sites-templateeditor-6514}

* 遺失 **[!UICONTROL 刪除]** 和 **[!UICONTROL 剪下]** 按鈕(在 `cq:actions` 屬性已自訂。 (NPR-38521)
* 如果元件包含另一個元件，則無法刪除模板結構內的元件，因為 **[!UICONTROL 刪除]** 按鈕。 (NPR-38585)

## Sling {#sling-6514}

* 由於模組中出現記憶體洩漏，導致生產上開啟的檔案數量增加 `DiscoveryLiteDescriptor` in `org.apache.sling.discovery.commons`，版本1.0.20。 (NPR-38288)
* 在Experience Manager中，從 **[!UICONTROL 操作]** > **[!UICONTROL 診斷]**，您會在選取 **[!UICONTROL 下載狀態ZIP]** > **[!UICONTROL 下載]**. (NPR-38514)

## 翻譯專案 {#translation-6514}

* 在上層頁面中新增為參考之子頁面的啟動，在 `isDeep` 屬性設為 `false`. (NPR-38531)

## 使用者介面 {#ui-6514}

* 使用時 **[!UICONTROL 全選]** > **[!UICONTROL 快速發佈]**,Experience Manager不會發佈所有資產或顯示要發佈的資產數量 **[!UICONTROL 卡片]** 檢視或 **[!UICONTROL 清單]** 檢視。 (NPR-38546)
* 針對顯示的選取資產計數不正確 **[!UICONTROL 新增至集合]** in **[!UICONTROL 全選]** 案例。 (NPR-38633)
* 您仍可將已停用的使用者新增至集合和專案。 (NPR-38651)
* 刪除篩選器而未儲存搜尋表單會建立錯誤。 (NPR-38698)
* 使用者的工作階段無法取得 `ModifiableValueMap` 群組的例項，以建立直接群組成員資格。 (NPR-38710)

## 工作流程 {#workflow-6514}

* 啟用JavaScript ES6（ESMAScript6模式或更高）編譯支援，以縮制 `/libs/cq/inbox/gui/components/inbox/clientlibs/commons.js` 程式庫。 (NPR-38304)
* 工作流程執行且處理步驟完成後，會多次重複相同的註解。 (NPR-38364)

## 安裝 [!DNL Experience Manager] 6.5.14.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.14.0要求 [!DNL Experience Manager] 6.5.見 [升級檔案](/help/sites-deploying/upgrade.md) 以取得詳細指示。 <!-- UPDATE FOR EACH NEW RELEASE -->
* Service Pack下載可在Adobe上取得 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* 在具有MongoDB和多個實例的部署上，安裝 [!DNL Experience Manager] 6.5.14.0，在使用套件管理器的其中一個製作執行個體上。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!NOTE]
>
>Adobe不建議移除或解除安裝 [!DNL Experience Manager] 6.5.14.0包。 <!-- UPDATE FOR EACH NEW RELEASE -->

### 在上安裝Service Pack [!DNL Experience Manager] 6.5 {#install-service-pack}

1. 如果執行個體處於更新模式（從舊版更新執行個體時），請先重新啟動執行個體再進行安裝。 Adobe建議，如果執行個體的目前正常運行時間很長，則重新啟動。

1. 安裝之前，請拍攝快照或對 [!DNL Experience Manager] 例項。

1. 從下載Service Pack [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.14.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. 開啟「套件管理器」，然後選取 **[!UICONTROL 上傳套件]** 上傳套件。 要了解更多資訊，請參閱 [封裝管理員](/help/sites-administering/package-manager.md).

1. 選取套件，然後選取 **[!UICONTROL 安裝]**.

1. 若要更新S3連接器，請在安裝Service Pack後停止執行個體，以安裝資料夾中提供的新二進位檔案取代現有連接器，然後重新啟動執行個體。 請參閱 [Amazon S3 Data Store](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>安裝Service Pack時，有時會退出套件管理程式UI上的對話方塊。 Adobe建議您先等待錯誤記錄穩定，再存取部署。 請等待與卸載更新程式捆綁相關的特定日誌，然後確保安裝成功。 通常，此問題會發生在 [!DNL Safari] 瀏覽器，但可在任何瀏覽器上間歇性發生。

**自動安裝**

您可以使用兩種不同的方法來自動安裝 [!DNL Experience Manager] 6.5.14.0。<!-- UPDATE FOR EACH NEW RELEASE -->

* 將包裝放入 `../crx-quickstart/install` 資料夾。 程式包會自動安裝。
* 使用 [來自套件管理器的HTTP API](/help/sites-administering/package-manager.md#package-share). 使用 `cmd=install&recursive=true` 以便安裝嵌套包。

>[!NOTE]
>
>Experience Manager6.5.14.0不支援Bootstrap安裝。 <!-- UPDATE FOR EACH NEW RELEASE -->

**驗證安裝**

若要了解經認證可與此版本搭配使用的平台，請參閱 [技術要求](/help/sites-deploying/technical-requirements.md).

1. 產品資訊頁面(`/system/console/productinfo`)顯示更新的版本字串 `Adobe Experience Manager (6.5.14.0)` 在 [!UICONTROL 已安裝的產品]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. 所有OSGi套件組合 **[!UICONTROL 活動]** 或 **[!UICONTROL 片段]** 在OSGi控制台中(使用Web控制台： `/system/console/bundles`)。

1. OSGi捆綁 `org.apache.jackrabbit.oak-core` 為1.22.12版或更新版本(使用Web控制台： `/system/console/bundles`)。 <!-- NPR-38747 -->

### 安裝 [!DNL Experience Manager] Forms附加元件套件 {#install-aem-forms-add-on-package}

>[!NOTE]
>
>如果您未使用 [!DNL Experience Manager] Forms。

<!-- Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package a week after the scheduled [!DNL Experience Manager] Service Pack release. -->

1. 確認您已安裝 [!DNL Experience Manager] Service Pack。
1. 下載適用於您作業系統的 [AEM Forms 發行版本](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates)所列出的對應 Forms 附加套件。
1. 依照 [安裝AEM Forms附加元件套件](/help/forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).
1. 若您在Experience Manager6.5 Forms中使用信函，請安裝 [最新AEMFD相容性套件](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates).

### 安裝 [!DNL Experience Manager] Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>如果您沒有在JEE上使用AEM Forms，請略過。 中的修正 [!DNL Experience Manager] Forms on JEE是透過個別安裝程式提供。

有關為安裝累積安裝程式的資訊 [!DNL Experience Manager] Forms on JEE和部署後設定，請參閱 [發行說明](jee-patch-installer-65.md).

>[!NOTE]
>
>安裝的累積安裝程式後 [!DNL Experience Manager] Forms on JEE，安裝最新的Forms附加元件套件，從 `crx-repository\install` ，然後重新啟動伺服器。

### UberJar {#uber-jar}

UberJar [!DNL Experience Manager] 6.5.13.0可在 [Maven Central存放庫](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.13/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

>[!NOTE]
>
>在Experience Manager6.5.14.0中，請注意，UberJar版本(6.5.13.0)與舊版相同。

若要在Maven專案中使用UberJar，請參閱 [如何使用UberJar](/help/sites-developing/ht-projects-maven.md) 並在您的專案POM中加入下列相依性： <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.13</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar和其他相關成品可在Maven中央存放庫中取得，而非AdobePublic Maven存放庫(`repo.adobe.com`)。 主要UberJar檔案已重新命名為 `uber-jar-<version>.jar`. 所以，沒有 `classifier`，使用 `apis` 作為值，對於 `dependency` 標籤。

## 過時的功能 {#removed-deprecated-features}

以下是標示為過時的功能清單 [!DNL Experience Manager] 6.5.7.0。功能在日後的版本中已被標示為過時，且在稍後的版本中已移除。 提供替代選項。

查看您是否在部署中使用了功能。 此外，計畫變更實作以使用替代選項。

| 區域 | 功能 | 替代方案 |
|---|---|---|
| 整合 | 此 **[!UICONTROL AEM雲端服務選擇加入]** 螢幕已過時，因為 [!DNL Experience Manager] 和 [!DNL Adobe Target] 整合已於 [!DNL Experience Manager] 6.5.整合支援Adobe Target Standard API。 API使用Adobe IMS驗證，並 [!DNL Adobe I/O Runtime]. 它支援AdobeLaunch在儀器方面日益發揮的作用 [!DNL Experience Manager] 分析和個人化的頁面，選擇加入精靈的功能與您無關。 | 設定系統連線、Adobe IMS驗證，以及 [!DNL Adobe I/O Runtime] 透過個別 [!DNL Experience Manager] 雲端服務。 |
| 連接器 | Microsoft® SharePoint 2010和Microsoft® SharePoint 2013的AdobeJCR Connector已於 [!DNL Experience Manager] 6.5。 | N/A |

## 已知問題 {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THE LIST.
 -->

* [AEM內容片段，含GraphQL索引套件1.0.3](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.3.zip)

* As [!DNL Microsoft® Windows Server 2019] 不支援 [!DNL MySQL 5.7] 和 [!DNL JBoss® EAP 7.1], [!DNL Microsoft® Windows Server 2019] 不支援全包安裝 [!DNL AEM Forms 6.5.10.0].

* 如果您要升級 [!DNL Experience Manager] 執行個體(從6.5版到6.5.10.0版)，您可以檢視 `RRD4JReporter` 例外 `error.log` 檔案。 若要解決問題，請重新啟動執行個體。

* 如果您安裝 [!DNL Experience Manager] 6.5 Service Pack 10或上一個Service Pack [!DNL Experience Manager] 6.5，資產自訂工作流程模型的執行階段副本(在 `/var/workflow/models/dam`)。
若要擷取執行階段副本，Adobe建議使用HTTP API，將自訂工作流程模型的設計時間副本與其執行階段副本同步：
   `<designModelPath>/jcr:content.generate.json`。

* 使用者可以在 [!DNL Assets] 並將巢狀資料夾發佈至 [!DNL Brand Portal]. 不過，資料夾的標題不會在 [!DNL Brand Portal] 直到重新發佈根資料夾為止。

* 當使用者首次選取以最適化表單設定欄位時，「屬性瀏覽器」中不會顯示儲存設定的選項。 在相同編輯器中選取以設定最適化表單的其他一些欄位，即可解決問題。

* 安裝期間可能會顯示下列錯誤和警告訊息 [!DNL Experience Manager] 6.5.x.x:
   * 「當Adobe Target整合設定於 [!DNL Experience Manager] 使用Target Standard API（IMS驗證），然後將體驗片段匯出至Target會導致建立錯誤的選件類型。 Target會建立數個具有「HTML」/來源「Adobe Target Classic」類型的選件，而非「體驗片段」/來源「Adobe Experience Manager」。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`:在granite/operations/maintenance找不到維護窗口。
   * 使用SUM、MAX和MIN等匯總函式時(CQ-4274424)，適用性表單伺服器端驗證會失敗。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`  — 在granite/operations/maintenance處找不到維護窗口。
   * 透過Shopbable Banner檢視器預覽資產時，Dynamic Media互動式影像中的熱點不會顯示。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` :等待註冊更改完成未註冊的超時。

* 嘗試移動/刪除/發佈內容片段或網站/頁面時，當背景查詢失敗時，內容片段參考擷取時會發生問題；即功能無法運作。
為確保操作正確，必須將以下屬性添加到索引定義節點 `/oak:index/damAssetLucene` （不需要重新索引）:

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

## 包含的OSGi套件組合和內容套件 {#osgi-bundles-and-content-packages-included}

以下文字檔案列出包含在 [!DNL Experience Manager] 6.5.14.0: <!-- UPDATE FOR EACH NEW RELEASE -->

* [Experience Manager6.5.14.0中包含的OSGi套件組合清單](/help/release-notes/assets/65140_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager6.5.14.0中包含的內容套件清單](/help/release-notes/assets/65140_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 受限網站 {#restricted-sites}

這些網站僅供客戶使用。 如果您是Adobe，且需要存取權，請聯絡您的客戶經理。

* [透過licensing.adobe.com下載產品](https://licensing.adobe.com/)
* [聯絡Adobe客戶支援](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 產品頁面](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5檔案](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hant)
>* [訂閱 Adobe 優先產品更新](https://www.adobe.com/tw/subscription/priority-product-update.html)

