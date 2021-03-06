---
title: 發行說明 [!DNL Adobe Experience Manager] 6.5
description: '"[!DNL Adobe Experience Manager] 6.5說明，概述發行資訊、新增功能、安裝方式和詳細的更改清單。」'
mini-toc-levels: 3
exl-id: 0288aa12-8d9d-4cec-9a91-7a4194dd280a
source-git-commit: 9f957175573eeb2b40d79a5087dc3034c56819cc
workflow-type: tm+mt
source-wordcount: '3742'
ht-degree: 5%

---

# [!DNL Adobe Experience Manager] 6.5最新Service Pack發行說明 {#aem-service-pack-release-notes}

## 發行資訊 {#release-information}

| 產品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.13.0 |
| 類型 | Service Pack版本 |
| 日期 | 2022 年 5 月 26 日 |
| 下載 URL | [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.13.0.zip) |

## 包含的內容 [!DNL Experience Manager] 6.5.13.0 {#what-is-included-in-aem}

[!DNL Experience Manager] 6.5.13.0包括自2019年4月6.5首次推出以來發佈的新功能、客戶要求的關鍵增強功能以及效能、穩定性和安全性改進。 [安裝此Service Pack](#install) 上 [!DNL Experience Manager] 6.5

中介紹的關鍵功能和增強功能 [!DNL Adobe Experience Manager] 6.5.13.0是：

* 在自適應形式中使用不可見的驗證碼：現在，您只能在可疑活動時使用看不見的驗證碼顯示驗證碼挑戰。 如果未發現可疑活動，則不顯示驗證碼質詢。 它有助於評估人形表單的完成情況，而無需複選框要求，減少定制工作，並改善最終用戶體驗。 (NPR-38500)

* 已添加對在表單資料模型後處理器中讀取REST端點的響應標頭的支援。 (NPR-38275)

* 現在，在生成自適應表單轉換檔案時，生成的XLIFF檔案的文本序列與相應自適應表單中的元件序列相同。 (NPR-37700)

* 當您本地化自適應表單，並對基本語言的文本進行哪怕很小的更改時，所有其他語言都會丟失完整的翻譯。 此問題已在 [!DNL Experience Manager] 6.5.13.0。 (NPR-37189)

* Forms的無障礙性改進：

   * 增加了對螢幕閱讀器的支援，以將表的標題和正文識別為連續和連接的實體。 它幫助螢幕閱讀器正確導航表。 (NPR-37139)
   * 添加了對螢幕閱讀器的支援，以停止導航HTML工作區，直到開啟對話框。 (NPR-37134)
   * 增加了在Forms設計器中為超連結指定螢幕Reader文本的功能。(NPR-36221)

中介紹了以下錯誤修復、關鍵功能和增強 [!DNL Experience Manager] 6.5.13.0:

<!-- The following issues are fixed in [!DNL Experience Manager] 6.5.13.0: -->

## [!DNL Assets] {#assets-6513}

* 嘗試編輯只讀下拉欄位時，下拉值將重置為空。 (NPR-38389)
* 如果視頻檔案中沒有音頻，則用戶無法接收視頻(.mp4)資產。 DAM更新資產工作流失敗並反映錯誤消息。 (NPR-38116)
* 使用「移動資產嚮導」移動包含資產的資料夾時，工作流將失敗並反映錯誤消息。 (NPR-38061)
* FLV視頻配置檔案的FMPEG轉碼工作流失敗。 (CQ-4343249)
* 更新到後 [!DNL Experience Manager] 6.5 SP10，資產元資料編輯器無法正常工作。 (CQ-4341359)
* 開啟智慧集合時，搜索篩選器會自動更改為「未發佈」。 (CQ-4341191)
* 在中切換語言時 **[!UICONTROL 用戶首選項]**，則 **[!UICONTROL 排序依據]**、下拉按鈕和「資產」首頁的排序選項中的其他選項不會反映在所選語言中。 (CQ-4339306)
* 將規則添加到中的下拉欄位時 **[!UICONTROL 元資料架構]**，也請參見Wiki頁。 **[!UICONTROL 依賴]** 清單不反映下拉清單的欄位標籤。 (ASSETS-9442)
* 「資產元資料已禁用」下拉清單不保留值。 (ASSETS-8918)
* 當使用 **[!UICONTROL 詳細資訊]** 選項 **[!UICONTROL 列]** 視圖，顯示不正確的注釋。 (ASSETS-8851)
* 建立具有不同版本的重複資產時，不會生成格式副本。 (ASSETS-8607)

* 非管理員用戶能夠發佈已由其他用戶簽出的資產。 (NPR-38128)
* Chrome 97上的維查看器無法正常工作。 (CQ-4340456)
* 資產下載按鈕不會在資產詳細資訊頁面上顯示完整菜單。 (CQ-4336703)
* 使用「連結共用」時，連結共用窗口中的某些字串未本地化。 (CQ-4330540)
* 在管理發布中添加項時，反映選定項計數的字串不會本地化。 (CQ-4330491)

### [!DNL Dynamic Media] {#dynamic-media-6513}

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Zero day exploit with the Java™ Spring Core Framework (CVE-2022-22963) impacting Experience Manager 6.5.12. (ASSETS-9031) -->
* AEM作者上Dynamic Media資產的基於令牌的安全預覽。 (ASSETS-4995)
* 為中的Dynamic Media建立影像預設時 [!DNL Experience Manager]，允許的最大值限制為用戶介面中的2000x2000像素。 當值在寬度或高度上增大到2001像素時， **[!UICONTROL 保存]** 按鈕。 (ASSETS-5691)
* 用戶可以阻止某些檔案格式上載到Dynamic Media。 (ASSETS-5693)
* 輔助功能 — 如果Image預設用戶介面上的影像上未實現Alt屬性，則依賴螢幕閱讀器的視覺障礙用戶將受到影響。 (ASSETS-9817)
* 輔助功能 — 當螢幕閱讀器以向下箭頭模式導航到時，螢幕閱讀器會為「時間軸段」和「操作」頁籤中顯示的影像敘述未標籤的影像，從而影響螢幕閱讀器。 (ASSETS-5651)
* 輔助功能 — 當使用（瀏覽/游標）模式導航時，螢幕閱讀器(NVDA/JAWS)在視頻播放器的「EmailLink」對話框中未說明「Send E-mail」（發送電子郵件）按鈕的描述性名稱(「Send E-mail」)時，螢幕閱讀器會受到影響。 (ASSETS-5641)
* 輔助功能 — 使用鍵盤上的TAB鍵導航時，鍵盤焦點不會移到「恢復」按鈕，該按鈕在調用「影像集編輯器」頁中的「撤消」按鈕後顯示。 (ASSETS-5582)
* 輔助功能 — 依賴螢幕閱讀器的用戶將受到影響，因為未為「屬性」標題下顯示的影像集影像提供Alt屬性。 (ASSETS-5576)
* 輔助功能 — 螢幕閱讀器未說明標題角色 `Cannot save this set` 文本 `Cannot save this set` 警報，使用標題快捷鍵導航時 `H`和下箭頭鍵。 (ASSETS-5569)
* 輔助功能 — 依賴螢幕閱讀器的用戶在表單中導航受到影響。 如果NVDA沒有為「寬度和高度」旋轉控制項描述標籤資訊，則他們發現很難理解有關表單控制項的資訊。 在NVDA窗體模式「F」中導航時，這些控制項出現在「響應影像裁剪」標題下。 (ASSETS-5393)
* 在站點上添加Dynamic Media元件並發佈該頁面後，新添加的Dynamic Media資產在發佈的頁面上不可見，在預覽頁面中也不可見。 影像和視頻資產類型均出現此問題。 (ASSETS-9467)

## 商務 {#commerce-6513}

* &quot;每個人&quot;有jcr：寫入 `/content/usergenerated/etc/commerce/smartlists`。 (NPR-35230)
* Commerce Products的本地排序不再有效。 (CQ-4343750)
* 更改屬性後，無法從搜索結果頁面快速發佈產品。 (CQ-4343318)

## CRX {#crx-6513}

* 如果包具有特殊字元，則無法下載 `+` 的子菜單。 (NPR-38102)

## [!DNL Forms] {#forms-65130}

<!-- * When you use the prefill service to fill an adaptive form that contains a fragment and the fragment contains a Text box that supports rich text, the form fails to submit, and the following error occurs:

  `[AF] [AEM-AF-901-004]: Encountered an internal error while submitting the form.` (NPR-38542) -->

* 單選按鈕、複選框和檔案上載元件未正確從德語翻譯為英語。 (NPR-38527)
* PDF417條形碼編碼 [!DNL Experience Manager] Forms對單選按鈕組無效。 (NPR-38525)
* 提交自適應表單時出現以下錯誤。
   `WARN [10.172.114.236 [1650871578492] POST /lc/content/forms/af/public/DHS-3754-ENG/jcr:content/guideContainer.af.internalsubmit.jsp HTTP/1.1] com.adobe.aemds.guide.internal.impl.utils.SubmitDataCollector TemplateKey not found in merge json:cq:responsive` (NPR-38520)
* 「從記錄文檔中排除隱藏欄位」選項無效。 (NPR-38512)
* 將Forms容器元件添加到「站點」頁後，用戶無法遍歷到其他「站點」頁，某些情況下「站點」頁掛起。 出現間歇性問題。 (NPR-38506)
* 應用後，用戶在自適應Forms中體驗到重疊文本 [!DNL Experience Manager] 6.5 Service Pack 11。 (NPR-38376、CQ-4342472)
* 用戶在將自適應表單面板移動到新的響應佈局時遇到異常。 (NPR-38369)
* 未為客戶端庫啟用ECMASCRIPT 6(ES6)支援 ` /libs/fd/expeditor/clientlibs/view`。 (NPR-38358)
* 使用 [!DNL Experience Manager] 用希伯來語發送電子郵件的工作流，在用戶端收到的電子郵件包含問號(??)，而不是希伯來語文本(NPR-38296)。
* 用戶隨機從 [!DNL Experience Manager] 發佈實例和自適應表單無法提交。 問題出現在 [!DNL Experience Manager] 使用Dispatcher的實例。 (NPR-38285)
* 在Adobe啟動規則中使用getFormDataString選項捕獲自適應表單資料時，該選項不返回自適應Forms資料。 (NPR-38283)
* [!DNL Experience Manager] 6.5Forms不建議使用的java.acl.與組相關的API，錯誤.log檔案中顯示以下錯誤消息：
   ` *WARN* [default task-36] org.apache.jackrabbit.oak.spi.security.principal.AclGroupDeprecation use of deprecated java.acl.Group-related API - this method is going to be removed in future Oak releases - see OAK-7358 for details` (NPR-38282)
* Forms用德語創作，但無法翻譯成英語或其他任何語言。 (NPR-38280)
* 使用自適應表單的本地化版本時，相應的記錄文檔(DoR)不會本地化。 (NPR-38235)
* 使用「發送電子郵件」步驟將附件與電子郵件一起發送時，附件不會保留在「工作流」步驟中指定的名稱。 (NPR-38216)
* 當新版本的信件發佈時，用戶無法開啟以前版本的信件草稿。 (NPR-38215、CQ-4342515)
* 在按一下配置為自適應表單規則的按鈕上調用AEM FormsJEE服務SOAP端點服務方法時，SOAP服務將失敗，但出現以下異常：
   `ERROR* [0:0:0:0:0:0:0:1 [1624362360493] POST /content/forms/af/testsoapwsdl/jcr:content/guideContainer.af.dermis HTTP/1.1] com.adobe.aemds.guide.addon expeditor.servlet.ExpEditorServiceManager Error while making web service related call java.lang.Exception: createSOAPParam: JSONException`
* 使用com.adobe.fd.pdfutility.services.PDFUtilityService#convertPDFtoXDP將PDF轉換為XDP格式時，將返回無效的XDP檔案。 (NPR-38140、CQ-4342099)
* 當多個用戶使用「通信管理」生成不同的字母時，在預覽時，會向某些用戶顯示錯誤的字母。 (NPR-38134)
* 嵌入在SITES頁中的AEM Forms元件使用width屬性，該屬性的值以%為單位，且根據W3CHTML驗證無效。 用戶在HTML驗證過程中遇到錯誤的分析錯誤。 (NPR-38124)
* 自適應格式中大多數OOTB主題的單選按鈕和複選框項不屬於Tabbing順序(NPR-38108)
* 當用戶在執行工作流時向注釋部分添加HTML標籤時，將呈現HTML標籤。 (NPR-37591)
* 在導入和發佈包含新XDP檔案的字母時，這些字母無法在「發佈」實例上預覽。 但是，如果使用同一CMP檔案導入並第二次發佈字母，則會成功預覽字母。 (CQ-4343599)
* 具有「準備資料處理」屬性集的表單無法在HTML工作區中呈現。 (CQ-4343294)
* 對於使用Forms6.5設計器建立的靜態PDF forms,PDF輔助功能失敗並出現錯誤 `Tab order entry in page with annotations not set to "S"`。 (CQ-4343117)
* 在應用AEMForms-6.5.0-0038(log4jv2.16)修補程式後，無法使用PDFG服務和OCR將影像轉換為PDF。 (CQ-4342450)
* 條形碼SSCC-18顯示的值不正確。 Forms伺服器忽略條形碼右側的值。 (CQ-4342400)
* 無法將Microsoft® Word檔案導入Forms設計器。 用戶遇到錯誤 `Word (version XP or onwards) could not be found on the machine`。 (CQ-4342146)
* 在Forms6.5設計器中，開啟使用Forms6.1設計器建立的表單並編輯文本框時，段落間距超過指定的空間。 將刪除空間的所有先前設定，並需要手動重新格式化文本框。 (CQ-4341899)
* 用戶無法在作業清除計畫程式中設定自定義時間。 (CQ-4339192)
* 用戶無法更新終結點管理UI下的任何配置，並遇到錯誤 ` Uncaught ReferenceError: updateEndpoint_required is not defined`。 (CQ-4331523)
* 對於無效標籤，錯誤消息的正常處理不按預期工作。 （NPR-38106和CQ-4337173）

>[!NOTE]
>
>* [!DNL Experience Manager Forms] 會在預定的 [!DNL Experience Manager] Service Pack 發行日期一週後發行附加元件的套件。


## Granite {#granite-6513}

* Omnisearch為沒有讀取權限的用戶返回結果。 (NPR-38373)
* 啟用ES6 `/libs/granite/configurations/clientlibs/confbrowser`。 (NPR-38300)

## Integrations {#integrations-6513}

* 已棄用的UserInfoServlet中Test和目標服務上的資源解析器會話洩漏。 (NPR-38112)

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * AEM‑OP‑13 ‑ HTTP Parameter Pollution in `com.day.cq.searchpromote.impl.servlet`. (NPR-38033) -->
<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Analytics 2.0 IMS support added to Experience Manager 6.5. (NPR-37914) -->

## Oak — 索引和查詢 {#oak-6513}

* Oak版6.5.13.0現在更新為1.22.11。 (NPR-38084) -->

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Create a CFP based on latest 6.5.12 and update Oak-related bundle versions. (NPR-38144) -->

## 平台 {#platform-6513}

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * RTC : Universal XSS through cq-rewriter HtmlParser. (NPR-38064) -->
* 升級依賴項 `org.apache.httpcomponents.httpclient` 在 [!DNL Experience Manager] 6.5 (NPR-37999)
* 由於路徑欄位建議而導致的作者負載較高。 (CQ-4341826)
* 當用戶將項目從「卡」視圖更改為「日曆」視圖時，必須刷新頁面。 (CQ-4340368)
* 由於權限限制，標籤丟失。 (CQ-4339543)
* 路徑選擇中搜索和篩選報告的多個問題無效。 (CQ-4339402)
* 停止在6.5上使用DTM — 切換到Launch for Omega Instrumentation並添加Gainsight支援。 (CQ-4337809)
* 基於設定的路徑欄位篩選器屬性限制路徑欄位元件搜索函式。 (CQ-4309556)
* [!DNL Experience Manager] 6.5號站台：中文區域設定命名修復。 (CQ-4308978)
* 切換到Omega工具的啟動。 (NPR-38377)
* [!DNL Experience Manager] 6.5號站台：中文區域命名修復。 (CQ-4308978)

## 複寫 {#replication-6513}

* 從「作者」到「發佈者」的用戶節點發佈失敗。 (NPR-38005)

## [!DNL Sites] {#sites-6513}

### 管理員 {#sites-admin-6513}

* 修復SP 12引入的在移動頁面時可能導致問題的回歸。 (SITES-5298)

### 經典用戶介面 {#sites-classicui-6513}

* RTE:將新影像拖到現有影像上時，更新的影像不可見。 (NPR-38141)

<!-- version 2 of description above * Updated Image is not visible When a new image is dragged on top of an existing image the updated image is not visible in RTE - Classic UI. (NPR-38141) -->

### 內容片段 {#sites-contentfragments-6513}

* 支援在子配置中建立內容片段模型。 (NPR-38054)

<!-- version 2 of description above * The Configuration Manager now allows you to set the Content Fragment Model config on a sub-config folder. (NPR-38054) -->
* 在內容片段模型中使用「唯一欄位」驗證時提高效能。 (NPR-38142)

<!-- version 2 of description above * The unique field validation query is now fixed. (NPR-38142) -->
* 開啟內容片段模型編輯器時縮短響應時間。 在Assets中有大量碎片的客戶在開啟時可能發現錯誤。 (SITES-6284)

<!-- version 2 of description above * If the customer is trying to access the editor of the content fragment models, they get a query error because of too many fragments on the dam. (SITES-6284) -->
* 修復從6.5.11到6.5.12更新時引入的回歸，這可能導致內容片段模型編輯器錯誤。 （SITES-5088和SITES-4967）

<!-- version 2 of description above * Paths were getting deleted when AEM 6.5.12.0 was installed on existing 6.5.11.0 instance. (SITES-5088)
* Apple 6.5.10 system crashing when using CF model editor, due to erroneous feature toggle check. (SITES-4967) -->
* 改進內容片段模型編輯器用戶介面的本地化。 (NPR-38126)

<!-- version 2 of description above * Some strings in the Content Fragment Model editor are not localized. (NPR-38126) -->
* 修復關閉內容片段編輯器在Dispatcher中使用Author伺服器時可能導致錯誤的問題。 (NPR-38205)

<!-- version 2 of description above * Update of Content Fragment references is returning an invalid JSON response via Dispatcher. (NPR-38205) -->
* 解決在RTE欄位上使用驗證時無法保存模型的問題。 (NPR-38210)

<!--version 2 of description above * Content Fragment Model Rich Text Validation Prevents Blocks Saving a Content Fragment Model. (NPR-38210) -->
* 布爾屬性未在「title」中顯示欄位文本，而在「Property Name」中顯示內容片段問題。 (NPR-38244)
* 使用查詢變數通過Postman運行永續查詢時出錯。 (NPR-38251、NPR-38057)
<!--version 2 of description above * An unexpected error message is coming in Postman, when executing the graphQL persisted query having query variables. (NPR-38251) -->
* 內容片段元件：「將標題作為段落處理」選項中的回歸已修復為6.5 SP7。 (NPR-38055)

<!--version 2 of description above * After applying SP11 to the Publish instance of AEM 6.5.6, the display result of the Content Fragment set in the published page changes. (NPR-38055) -->
* 修復6.5.11中引入的可能導致資產搜索錯誤的回歸。 (SITES-4784)

<!--version 2 of description above * Adapt external index package to use selection Policy (fragment versus asset index). (SITES-4784) -->
* 使用 **[!UICONTROL 編輯]** 搜索結果會導致 `Not Found` 錯誤。 (NPR-37810)

<!--version 2 of description above * When editing Content Fragment from the Assets Search Rail results page, it throws 'Not Found' error. (NPR-37810) -->

### 內容集線器 {#sites-contenthub-6513}

* 沒有硬頁刷新，上下文中心UI模型無法正確呈現。 (NPR-38212)

### 電子郵件編輯器 {#sites-emaileditor-6513}

* 支援即將發佈的電子郵件核心元件 [https://github.com/adobe/aem-core-email-components](https://github.com/adobe/aem-core-email-components)。 （NPR-38445和NPR-38204）

<!-- version 2 of description above * Allow new email templated under campaign and ambit. (NPR-38445) * The "Approve for Adobe Campaign" workflow was only running for pages which are of type or extending the resource types: "mcm/neolane/components/newsletter", "mcm/campaign/components/newsletter" and "mcm/campaign/components/campaign_newsletterpage". (NPR-38204) -->

### 體驗片段 {#sites-experiencefragments-6513}

* 使用「體驗片段的引用」中的「導航到頁面」操作時，會開啟錯誤的頁面。 (NPR-38062)
* 未在頁面側觀察到來自XF模板的佈局屬性。 (NPR-38214)
* 改進了XF參考計算的效能。 (NPR-38269)

<!-- version 2 of description above * Job queue configuration is incorrect - The OSGi configuration for the reference updater job queue has not been ported back to 6.5. This issue leads to jobs being run in the main queue, which has a higher priority and allows more jobs to run in parallel. This flow can lead to CPU exhaustion. (NPR-38269) -->

### 頁面編輯器 {#sites-pageeditor-6513}

* 改進中沒有inlineEditing或dropTarget功能的元件的撤消 `cq:editConfig`。 (NPR-38361)

<!-- version 2 of the description above * When out of the box components that don't have inlineEditing or dropTarget feature in the _cq_editConfig file (navigation, breadcrumb, embed) are deleted > undeleted (by way of Undo), all configurations are lost and empty placeholder reappears. Component must be reconfigured from scratch. (NPR-38361) -->
* 「樣式系統」下拉清單可能位於頁面頂部，而不是元件的上下文中 — 用於使用 `cq:editConfig` 「afteredit:REFRESH_PAGE」。 此問題現在已解決。 (NPR-38384)

<!-- version 2 of description above* When selecting a style option on a component, the Styles box shifts to the upper left corner of the screen, rather than staying put below the style icon. Happens for components that have  cq:editConfig “afteredit: REFRESH_PAGE”. (NPR-38384) -->
* 添加到嵌套的佈局容器時，文本元件未對齊。 (NPR-38193)
* 當沒有元件的「樣式系統」配置時，將顯示一個空樣式頁籤；當沒有配置時，該頁籤現在處於隱藏狀態。 (NPR-38218)
<!-- version 2 of description above * Style tab is blank on components without styles/policies. (NPR-38218) -->
* 屬性 `useLegacyResponsiveBehaviour` 只有經過驗證才能工作。 (NPR-37996)
* 將jquery-ui升級為最新版本導致編輯器斷開。 (SITES-5647)

### 安全性 {#sites-security-6513}

* 用戶組管理用戶介面有時無法刪除用戶，特別是在具有+20用戶的組中。 (NPR-38041)

<!--version 2 of description above * Cannot remove users from user groups. (NPR-38041) -->

### SEO {#sites-seo-6513}

* Sitemap生成器和規範標籤添加對不帶.html的URL的支援。 (CIF-2647)
* 添加對使用noindex配置刪除其他語言的支援。 (CIF-2496)
* 添加支援以提供自定義URL，以覆蓋內容接近相同的頁面的預設規範URL。 (CIF-2747)

### 編SPA輯器和SDK {#sites-spa-sdk-6513}

* 從6.5.13開始，在通過編輯器進行編輯之前，不必再在JCR中建立容器元件節SPA點。 A `virtual container` 在通過SDK保存之前建立。 (SITES-5762)

<!-- version 2 of description above * Virtual container support - Adding a child component to a virtual container that is not yet present in the database implies the creation of a node to represent the container in content structure. (SITES-5762) -->

### 範本編輯器 {#sites-templateeditor-6513}

* 修復發佈更改的模板未發佈所有依賴關係的回歸。 (NPR-38274)

<!-- version 2 of description above * Template changes do not get published until you publish a page that uses that template. (NPR-38274) -->
* TemlitaddResource valueMap應允許根據ValueMap API進行深讀。 (NPR-38439)

## Sling {#sling-6513}

<!-- OBSOLETE BASED ON CQDOC-19400 * Memory leak in `DiscoveryLiteDescriptor`. (NPR-38288) -->
* 更新 `sling-javax.activation` 捆綁包，固定SLING-8777。 (NPR-38077)

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Security issues reported under `org.apache.sling.scripting.jst`. (NPR-38067) -->

## 翻譯項目 {#translation-6513}

* 為引用的頁/xf建立多個啟動。 (NPR-38263)
* 自Service Pack 10以來向翻譯項目添加頁面的行為已更改。 翻譯項目不包含新建立的頁面 [例如：test頁 — 婦女–2] 清單中，當新建立的頁面的選定父項 [不是直接新建的頁面]。 (NPR-38256)
* 添加 `cq:isTranslationLaunch` 屬性。 (NPR-38224)
* 正在為具有引用的XF且其中包含資產的頁面建立啟動。 (NPR-38199)
* [!DNL Experience Manager] 更新翻譯記憶庫無效。 (NPR-38196)
* 啟用ES6 `/libs/cq/gui/components/projects/admin/translation/job/addcontent/clientlibs.js`。 (NPR-38306)
* 最新18n軟體包，用於翻譯 [!DNL Experience Manager] 6.5 (CQ-4339505)

## 使用者介面 {#ui-6513}

* 更新到 `favicon.ico` 用於Experience Manager。 (CQ-4315324)
* 在「開始」頁>「工具」部分上，按一下 [!DNL Experience Manager] 表徵圖 [!DNL Experience Manager] 導航螢幕應彈出。 (NPR-38417)
* 啟用ES6 `/libs/granite/ui/references/clientlibs/coral/references`。 (NPR-38303)
* 啟用ES6 `/libs/granite/datavisualization/clientlibs/d3-3.x`。 (NPR-38302)
<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * AEM‑OP‑09 ‑ Persistent cross‑site scripting selecting paths in templates. (NPR-38301) -->
* 觸摸屏中的日期選取器以韓語顯示。 (NPR-38079)
* 在重新排序欄位時，使用多個欄位創作對話框，從而忽略單選按鈕選擇值。 (NPR-38063)

## WCM {#wcm-6513}

* [!DNL Experience Manager] MCM(Campagment)6.5:中文區域設定命名修復。 (CQ-4308973)
* com.day.cq.wcm.workflow.impl.WcmWorkflowServiceImpl.autoSubmitPageAfterModification中未關閉的ResourceResolver(NPR-38286)

## 安裝 [!DNL Experience Manager] 6.5.13.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback -->

* [!DNL Experience Manager] 6.5.13.0要求 [!DNL Experience Manager] 6.5請參閱 [升級文檔](/help/sites-deploying/upgrade.md) 的上界。
* Service Pack下載可在Adobe上獲得 [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)。
* 在具有MongoDB和多個實例的部署中，安裝 [!DNL Experience Manager] 6.5.13.0在使用包管理器的某個「作者」實例上。

>[!NOTE]
>
>Adobe不建議刪除或卸載 [!DNL Experience Manager] 6.5.13.0包。

### 在上安裝Service Pack [!DNL Experience Manager] 6.5 {#install-service-pack}

1. 如果實例處於更新模式（當實例從早期版本更新時），請在安裝前重新啟動該實例。 Adobe建議在實例的當前正常運行時間較長時重新啟動。

1. 在安裝之前，請拍攝快照或新備份 [!DNL Experience Manager] 實例。

1. 從下載Service Pack [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.13.0.zip)。

1. 開啟套件管理器，然後按一下&#x200B;**[!UICONTROL 「上傳套件」]**&#x200B;即可上傳套件。要瞭解更多資訊，請參閱 [包管理器](/help/sites-administering/package-manager.md)。

1. 選擇包並按一下 **[!UICONTROL 安裝]**。

1. 要更新S3連接器，請在安裝Service Pack後停止實例，用安裝資料夾中提供的新二進位檔案替換現有連接器，然後重新啟動實例。 請參閱 [AmazonS3資料儲存](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)。

>[!NOTE]
>
>在安裝Service Pack期間，有時會退出包管理器UI上的對話框。 Adobe建議您在訪問部署之前等待錯誤日誌穩定。 請等待與卸載更新程式包相關的特定日誌，然後確保安裝成功。 通常，此問題發生在 [!DNL Safari] 但在任何瀏覽器上都可能間歇性出現。

**自動安裝**

有兩種方法可用於自動安裝 [!DNL Experience Manager] 6.5.13.0。

* 將包放入 `../crx-quickstart/install` 資料夾。 軟體包將自動安裝。
* 使用 [包管理器中的HTTP API](/help/sites-administering/package-manager.md#package-share)。 使用 `cmd=install&recursive=true` 以便安裝嵌套的軟體包。

>[!NOTE]
>
>[!DNL Experience Manager] 6.5.13.0不支援Bootstrap安裝。

**驗證安裝**

要瞭解經認證可與此版本配合使用的平台，請參閱 [技術要求](/help/sites-deploying/technical-requirements.md)。

1. 產品資訊頁面(`/system/console/productinfo`)顯示更新的版本字串 `Adobe Experience Manager (6.5.13.0)` 在 [!UICONTROL 已安裝的產品]。

1. 所有OSGi捆綁包 **[!UICONTROL 活動]** 或 **[!UICONTROL 片段]** 在OSGi控制台(使用Web控制台： `/system/console/bundles`)。

1. OSGi捆綁 `org.apache.jackrabbit.oak-core` 版本1.22.3或更高版本(使用Web控制台： `/system/console/bundles`)。


### 安裝 [!DNL Experience Manager] Forms附加包 {#install-aem-forms-add-on-package}

>[!NOTE]
>
>如果不使用 [!DNL Experience Manager] Forms。 修復 [!DNL Experience Manager] Forms在預定時間後一週通過單獨的附加包遞送 [!DNL Experience Manager] Service Pack版本。

1. 確保已安裝 [!DNL Experience Manager] 服務包。
1. 下載適用於您作業系統的 [AEM Forms 發行版本](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates)所列出的對應 Forms 附加套件。
1. 按中所述安裝Forms附加程式包 [安裝AEM Forms附加軟體包](/help/forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package)。
1. 如果在Forms6.5Experience Manager中使用字母，請安裝 [最新的AEMFD相容性包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates)。

### 安裝 [!DNL Experience Manager] FormsJEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>如果JEE上沒有使用AEM Forms，則跳過。 修復 [!DNL Experience Manager] JEE上的Forms通過單獨的安裝程式提供。

有關為安裝累積安裝程式的資訊 [!DNL Experience Manager] Forms的JEE和部署後配置，請參閱 [發行說明](jee-patch-installer-65.md)。

>[!NOTE]
>
>安裝累積安裝程式後 [!DNL Experience Manager] Forms在JEE上，安裝最新的Forms載入項軟體包，從 `crx-repository\install` 資料夾，然後重新啟動伺服器。

### UberJar {#uber-jar}

UberJar [!DNL Experience Manager] 6.5.13.0在 [Maven中央儲存庫](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.13/)(https://)。

要在Maven項目中使用UberJar，請參見 [如何使用UberJar](/help/sites-developing/ht-projects-maven.md) 並在項目POM中包括以下依賴關係：

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
>UberJar和其他相關工件可在Maven Central Repository（Maven中央儲存庫）上找到，而不是AdobePublic Maven儲存庫(`repo.adobe.com`)。 主UberJar檔案已更名為 `uber-jar-<version>.jar`。 所以，沒有 `classifier`, `apis` 值，對於 `dependency` 標籤。

## 過時的功能 {#removed-deprecated-features}

下面是標籤為不建議使用的功能和功能的清單 [!DNL Experience Manager] 6.5.7.0。功能在以後的版本中被標籤為已棄用，稍後將刪除。 提供了備用選項。

查看是否在部署中使用了功能或功能。 此外，計畫更改實施以使用替代選項。

| 區域 | 功能 | 替代方案 |
|---|---|---|
| 整合 | 的 **[!UICONTROL AEM雲服務選擇加入]** 螢幕已棄用，因為 [!DNL Experience Manager] 和 [!DNL Adobe Target] 整合更新於 [!DNL Experience Manager] 6.5整合支援Adobe Target標準API。 API使用Adobe IMS驗證， [!DNL Adobe I/O]。 它支援Adobe發射對儀器的作用日益增強 [!DNL Experience Manager] 頁面進行分析和個性化設定，選擇加入嚮導在功能上無關緊要。 | 配置系統連接、Adobe IMS驗證和 [!DNL Adobe I/O] 通過各個 [!DNL Experience Manager] 雲服務。 |
| 連接器 | Microsoft®SharePoint® 2010和Microsoft®SharePoint® 2013的AdobeJCR連接器不建議使用 [!DNL Experience Manager] 6.5 | N/A |

## 已知問題 {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THE LIST.
 -->

<!-- VULNERABILITY ISSUE - REMOVED MAY 23, 2022 AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * If you are using Content Fragments and GraphQL, Adobe recommends that you install the following packages on top of 6.5.12.0:

  * [AEM 6.5.12 Sites HotFix-NPR-38144](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2Faem-service-pkg-6.5.12.0-NPR-38144-B0002.zip) (this hot fix replaces SP12, but can be installed on top of SP12) -->

* [GraphQL索AEM引包1.0.3的內容片段](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.3.zip)

* 作為 [!DNL Microsoft® Windows Server 2019] 不支援 [!DNL MySQL 5.7] 和 [!DNL JBoss® EAP 7.1]。 [!DNL Microsoft® Windows Server 2019] 不支援對 [!DNL AEM Forms 6.5.10.0]。

* 如果要升級 [!DNL Experience Manager] 實例從6.5版到6.5.10.0版，您可以查看 `RRD4JReporter` 例外情況 `error.log` 的子菜單。 要解決此問題，請重新啟動實例。

* 如果安裝 [!DNL Experience Manager] 6.5 Service Pack 10或上一個Service Pack [!DNL Experience Manager] 6.5，資產自定義工作流模型的運行時副本(建立於 `/var/workflow/models/dam`)。
要檢索運行時副本，Adobe建議使用HTTP API將自定義工作流模型的設計時副本與其運行時副本同步：
   `<designModelPath>/jcr:content.generate.json`。

* 用戶可以在中更名層次結構中的資料夾 [!DNL Assets] 將嵌套資料夾發佈到 [!DNL Brand Portal]。 但是，資料夾的標題未在中更新 [!DNL Brand Portal] 直到重新發佈根資料夾。

* 當用戶首次以自適應格式選擇配置欄位時，「屬性瀏覽器」中不會顯示保存配置的選項。 選擇以在同一編輯器中配置自適應表單的其它一些欄位可解決此問題。

* 在安裝期間可能顯示以下錯誤和警告消息 [!DNL Experience Manager] 6.5.x.x:
   * &quot;當Adobe Target整合配置在 [!DNL Experience Manager] 使用目標標準API（IMS驗證），然後將體驗片段導出到目標會導致建立錯誤的提供類型。 Target不是「體驗片段」/源「Adobe Experience Manager」，而是建立「HTML」/源「Adobe Target經典」類型的幾個產品。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`:未在花崗岩/操作/維護中找到維護窗口。
   * 當使用SUM、MAX和MIN等集合函式(CQ-4274424)時，Adaptive Form伺服器端驗證失敗。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`  — 在花崗岩/操作/維護處找不到維護窗口。
   * 通過Sobler Banner查看器預覽資產時，Dynamic Media互動式影像中的熱點不可見。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` :等待註冊表更改完成註銷時超時。

* 當嘗試移動/刪除/發佈內容片段或站點/頁面時，當回遷內容片段引用時會出現問題，因為後台查詢失敗；即，該功能不起作用。
要確保正確操作，必須將以下屬性添加到索引定義節點 `/oak:index/damAssetLucene` （不需要重新索引）:

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

## 包括OSGi捆綁包和內容包 {#osgi-bundles-and-content-packages-included}

以下文本文檔列出了包含在 [!DNL Experience Manager] 6.5.13.0:

* [6.5.13.0Experience Manager中包含的OSGi捆綁包清單](/help/release-notes/assets/65130_bundles.txt)

* [6.5.13.0Experience Manager中包含的內容包清單](/help/release-notes/assets/65130_packages.txt)

## 受限網站 {#restricted-sites}

這些網站僅供客戶訪問。 如果您是客戶，需要訪問，請與Adobe客戶經理聯繫。

* [產品下載，網址為licensing.adobe.com](https://licensing.adobe.com/)
* [聯繫Adobe客戶支援](https://experienceleague.adobe.com/docs/customer-one/using/home.html)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 產品頁](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5文檔](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hant)
>* [訂閱 Adobe 優先產品更新](https://www.adobe.com/tw/subscription/priority-product-update.html)

