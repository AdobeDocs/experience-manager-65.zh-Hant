---
title: 發行說明 [!DNL Adobe Experience Manager] 6.5
description: 查找發行資訊、新增內容、安裝方式和詳細的更改清單 [!DNL Adobe Experience Manager] 6.5
mini-toc-levels: 3
exl-id: fc7d3727-7cd4-47a4-8e75-840f9f9c0e62
source-git-commit: a95255594ec03c152cd96df48597ced5fce4b315
workflow-type: tm+mt
source-wordcount: '2972'
ht-degree: 3%

---

# [!DNL Adobe Experience Manager] 6.5最新Service Pack發行說明 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/Documents/issue_tracker_sp_cfp_updates.xlsx?d=w3ea81ae4e6054153b132f2698c86f84e&csf=1&web=1&e=WRAZ43&nav=MTVfezk2OTJDQTNFLUI4QTQtNDY2RS05NEVCLUQ5QjcyNEVENkJDNn0 -->

## 發行資訊 {#release-information}

| 產品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.16.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 類型 | Service Pack版本 |
| 日期 | 2023年2月23日星期四 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 下載 URL | [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]be/packages/cq650/servicepack/aem-service-pkg-6.5.16.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## 包含的內容 [!DNL Experience Manager] 6.5.16.0 {#what-is-included-in-aem-6516}

[!DNL Experience Manager] 6.5.16.0包括自2019年4月6.5首次發佈以來發佈的新功能、客戶要求的關鍵增強功能、錯誤修復以及效能、穩定性和安全性改進。 [安裝此Service Pack](#install) 上 [!DNL Experience Manager] 6.5 <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

Dynamic Media的一個關鍵改進是：

新協定DASH（動態自適應HTTP流）支援在Dynamic Media視頻傳輸中啟動自適應比特率流（帶CMAF） [通用媒體應用程式格式] 啟用)。

* 自適應串流 (DASH/HLS) 可確保更好的一般使用者觀看影片體驗.
* DASH 是自適應影片串流的國際標準通訊協定，在業界被廣泛採用.
* 現在可通過提交支援票證獲得。

請參閱 [啟用帳戶上的DASH](/help/assets/video.md#enable-dash)。

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets] {#assets-6516}

* 已連接資產：為遠程DAM上的映像啟用「智慧裁剪」選項、將映像上載到資料夾並將資料夾同步到本地站點時，該資料夾不會在本地站點部署中開啟。 (NPR-39912)
* 按名稱對集合排序時，清單視圖不能正常工作(ASSETS-19401)
* 將大型媒體檔案(JPEG)上載到集合時，Experience Manager停止響應。 (ASSETS-19387)
* 在內容樹窗格中，顯示的資產名稱不正確，因為資產的位置未正確呈現。 (ASSETS-18870)
* 使用連結共用集合時，URL中的資料在卡視圖洗牌和清單視圖之間不匹配。 (ASSETS-18758)
* 使用資料夾類型的篩選器執行搜索時，搜索結果不一致。 (ASSETS-18227)
* 的 `dam:size` 寫回後不更新XMP屬性，這會導致從中返回錯誤資訊 `/platform/path/to/asset.jpg;resource=metadata` API。 (ASSETS-17631)
* 在所有Experience Manager實例上取消關閉資源解析程式。 (ASSETS-16904)
* 即使分配了 `create` 和 `modify` 權限。 (ASSETS-15956)
* 的 `move` 按鈕在將資源從一個點移動到另一個點時被隨機禁用。 (ASSETS-14889)
* 螢幕閱讀器無法標識標題，因為文本不是在標題標籤內定義的，而是一般文本。 (ASSETS-6924)
* 影像下的替代文本不是必需的，但影像下顯示的文本與 `Type` 屬性。 (ASSETS-6915)


## [!DNL Assets] - [!DNL Dynamic Media] {#dm-6516}

* 窗體元素不包含標籤。 對於NVDA和JAWS等螢幕閱讀器，表單標籤資訊未正確宣佈。 (CQ-4344078)
* 當 `Escape` 鍵在鍵盤上使用。 (CQ-4344077)
* 在給定無效輸入後，為內聯錯誤建議顯示的「資訊」表徵圖（字母「i」）無法使用鍵盤訪問。 (CQ-4344076)
* `getManifestURI` 由於JCR屬性被讀取為，因此返回空值 `toString` 而不是 `getString`。 (ASSETS-18674)
* SmartCrop視頻元件未正確運行。 該元件正在執行回放，而不是流式播放，VTT呼叫失敗，導致404錯誤。 (ASSETS-18468)
* 選擇 **[!UICONTROL 屬性]** 在資產的「查看器」頁面上，將導致空指針異常。 (ASSETS-18420)
* [!DNL Experience Manager] DASH流的用戶介面更改，包括以下內容：
   * 在視頻配置檔案編輯器中具有可見的CMAF（公共媒體應用程式格式）欄位。
   * 使視頻上載過程發送CMAF標誌。
   * 選項 **[!UICONTROL 自動]**。 **[!UICONTROL 合肥]**, **[!UICONTROL 划線]** 現在可在查看器預設編輯器的播放下拉清單中找到 **[!UICONTROL 行為]** 頁籤。
(ASSETS-17428)
* 在導航中，選擇 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]** > **[!UICONTROL 建立]** > **[!UICONTROL 旋轉木馬集]**，圖片表徵圖與「幻燈片1」文本字串重疊。 (ASSETS-18578)
* 重新發佈未發佈的資產。 (ASSETS-16428)
* Experience Manager作者因負載問題而停止工作，提示建立合成警報。 (ASSETS-15937)
* 在「Dynamic Media常規設定」頁中，出現未翻譯的錯誤消息 `Failed to fetch data` 的子菜單。 (ASSETS-15617)

## [!DNL Forms] {#forms-6516}

### [!DNL Forms] 關鍵功能 {#forms-features-6516}

* [無頭自適應Forms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) 使您的開發人員能夠建立、發佈和管理可通過API訪問和交互的互動式表單，而不是通過傳統的圖形用戶介面。

* [自適應Forms核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#features) 是一組24個開源、符合BEM規範的元件，它們構建在Adobe Experience ManagerWCM核心元件的基礎上。 這些元件是開源的，使開發人員能夠輕鬆定制和擴展這些元件，以滿足其組織的特定需求。 任何具備定制技能的人 [WCM核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/authoring.html?lang=en) 可輕鬆定制和設計這些元件的樣式。

* OSGi上的Reader擴展服務現在提供了單獨的選項，以啟用PDF的進出口使用權，以在Adobe Acrobat Reader進口或導出資料。 (NPR-39909)

### [!DNL Forms] 修復 {#forms-fixes-6516}

* 使用 **分配任務** 為已分配任務發送通知的步驟是發送兩封電子郵件，而不是發送一封給已分配的個人。 (NPR-40078)
* 當用戶隱藏表標題時，它會取消設定先前設定的列寬，並且所有列都保留相同的寬度。 (NPR-40063)
* 如果更改了管理員用戶的預設密碼 `admin`，執行時 `Prepare Adobe Experience Manager Server For DSC deployment` 檢查AEM FormsJEE服務包是否失敗。 (NPR-40062)、(NPR-39387)
* OutputService和AssemblerService API無法將PDF表單轉換為PDF/A。(NPR-39990)
* AssemblerService無法將PDF轉換為PDF/A。當用戶將PDF轉換為PDF/A時，將出現以下錯誤： `PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Summary" ignoreUnusedResources="true" allowCertificationSignatures="true"> <Violation count="6" key="PDFA_CS_001_NOT_DEVICE_INDEPENDENT" description="ColorSpace is not device independent`。 (NPR-39956)
* 當GuideSubmitServlet API調用的伺服器端驗證失敗時，在發送到客戶端的響應中不會返回錯誤。 (NPR-39925)
* 升級到AEMWindows伺服器上的6.5.15.0 Service Pack後，用戶會遇到多條錯誤消息，電子郵件服務無法正常工作。(NPR-39919)
* 升級到AEM6.5.14.0並使用importData服務將PDF與XML合併時，會出現以下錯誤： `Caused by: java.lang.NoSuchMethodError: com.adobe.xfa.form.FormModel.isXFABarcode(Lcom/adobe/xfa/Node;)Ljava/lang/Boolean`。(NPR-39807)
* 用戶安裝時 **文檔安全辦公室** 擴展，出現以下問題：
   * Microsoft® Excel頻繁崩潰。
   * 開啟安全文檔時， **文檔安全辦公室** 未檢測到電腦上安裝了擴展。 指示用戶下載並安裝安全擴展。 (NPR-39768)
* 用戶升級到AEM6.5.15.0 Service Pack後，PostScript到Pdf的轉換將不工作。 (NPR-39765)、(NPR-39764)
* 當用戶嘗試在開啟自適應表單後開啟教程螢幕時，該螢幕將失敗，出現NullPointer異常：`[172.17.0.1[1662032923933]GET/libs/fd/af/content/editors/form/tour/content.htmlHTTP/1.1]com.day.cq.wcm.core.impl.WCMDebugFilterException:org.apache.sling.api.scripting.ScriptEvaluationException:"` (NPR-39654)
* 在Windows中，當用戶啟用高對比度黑色設定時，HTML5Forms內容在瀏覽器中呈現為HTML預覽時將變得不清晰。 (NPR-39018)
* 當用戶嘗試添加元資料時，「保存」按鈕將對「草稿」和「提交」元件都不起作用。(CQ-4349601)
* 升級到AEM6.5.15.0 Service Pack後，在可視編輯器中，相對URL的重定向不再有效。 (NPR-39947)
* 當用戶升級到AEM6.5.15.0 Service Pack時，重定向將停止與Internet Explorer一起工作。 (CQ-4351745)
* 用戶升級到AEM6.5.15.0 Service Pack後，無法識別HTML標題標籤。 標題標籤的HTML代碼在HTML窗體中顯示為文本。 (NPR-39915)
* 當用戶嘗試提交自適應表單時，會出現一個類型錯誤： `ERROR [10.207.64.167 [1668589530607] POST /app/LS4/content/forms/af/revalidate/jcr:content/guideContainer.af.submit.jsp HTTP/1.1]`(NPR-39809)
* 當用戶使用 **發送電子郵件** 提交操作，它未正確顯示。 郵件模板嵌入到「記錄文檔」的預覽中。 (CQ-4352155)
* 當用戶以IE相容模式在Microsoft邊緣瀏覽器上將自適應表單作為HTML預覽時，它將無法正確顯示。(CQ-4352216)
* 詞典需要包括帶有特殊字元（如下划線或連字元）的新語言環境，才能啟用翻譯。 (NPR-40088)

安裝AEM6.5.16.0Forms附加服務包後，客戶面臨以下所列問題。 所以， [AEM6.5.16.0Forms附加服務包 — 6.0.914](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 的子菜單。 Adobe建議使用更新的Service Pack:
* 當用戶嘗試在forms-users組中與用戶一起建立自適應表單時，不存在選擇任何模板的選項，並且出現類似以下錯誤：內部伺服器錯誤：java.lang.NullPointerException，位於com.adobe.aem.formsndocuments.servlet.ThemeClientLibraryDataSourceServlet.lambda$getThemeClientLibCategoryList$3(ThemeClientLibraryDataSourceServlet.java:76)，位於java.base/java.util.stream.Referencepipeline$2$1.accept(ReferencePipeline.java:176)，地址為java.base/java.util.Iterator.forEachRemaining(Iterator.java:133)(FORMS.-7629)
* 未保存在代碼編輯器規則中所做的更改。(FORMS-7532)

## 整合 {#integrations-6516}

* 從Adobe6.5中刪除Search&amp;Promote代碼和依賴項。AdobeSearch&amp;Promote於2022年9月到期。 請參閱 [AdobeSearch&amp;Promote服務終了公告](https://experienceleague.adobe.com/docs/discontinued/using/search-promote.html?lang=en)。 (NPR-39706)

## [!DNL Sites] {#sites-6516}

* 當前 `cq-wcm-core` 藝術工廠的發佈沒有POM。 (SITES-10983)
* 推廣預覽操作不應列出要建立的頁面。 (SITES-10355、CQ-4266213)
* 在MSM分離後重新建立分離的頁面。 (SITES-9841)
* 推出新產品就是提前；用戶必須在載入螢幕上等待多分鐘，然後才能超時請求。 (SITES-9051)
* 「展示頁」用戶介面顯示不存在的父頁路徑。 您可以使用成功消息來展開頁面，但子頁面不會展開，因為父頁面從來就不會展開。 (SITES-8621)

### [!DNL Sites] - 核心元件 {#sites-core-components-6516}

* 將連結處理集中到電子郵件頁面上，以便不再需要模型自定義。 (SITES-9002)

### [!DNL Sites]  — 管理用戶介面 {#sites-adminui-6516}

* CSV導出未導出選定頁面下的所有頁面。 (SITES-9390)

### [!DNL Sites] - [!DNL Content Fragments] {#sites-contentfragments-6516}

* 無法打印內容片段的JSON。 原因是開啟內容片段的「預覽」頁面時無法生成GraphQL查詢。 (SITES-8619)
* 重新開啟內容片段模型編輯器時，所有 **[!UICONTROL 日期和時間]** 欄位預設為「日期和時間」類型。 (SITES-8401)

### [!DNL Sites] - [!DNL Experience Fragments] {#sites-experiencefragments-6516}

* 即使模板列在允許的模板下，您也無法將體驗片段移動到另一個資料夾。 (SITES-8601)
* (SITES-7989)


### [!DNL Sites]  — 頁面編輯器 {#sites-pageeditor-6516}

* 更新SITES-8464中資源解析器改進的相關性，其中以創作模式呈現的頁建立了大量 `TemplatedResourceImpl` 對象。 (SITES-9350)


## Sling {#sling-6516}

* Experience Manager在啟動時陷入僵局。 (NPR-39832)
* 當Experience Manager的版本儲存中存在許多虛榮路徑時，Experience Manager無法啟動。 (NPR-38955)


## 翻譯項目 {#translation-6516}

* 在 `MicrosoftTranslationServiceImpl`，查詢字串參數 `Category` 不正確。 (NPR-39828)
* 建立翻譯項目時顯示錯誤 *母版頁資源不存在*;未建立轉換項目。 (NPR-39762)
* 無法在使用人工翻譯連接器的翻譯項目上設定到期日期。 (NPR-39593)

## 使用者介面 {#ui-6516}

* 更改為較小的解析度時，不顯示DatePicker，並且AM/PM選擇不會顯示或明顯更改。 (NPR-39948)
* 使用minify js（JavaScript的最小化）時，它不會因為分析錯誤而處理小化。 (NPR-39650)
* 標籤欄位(`/libs/cq/gui/components/coral/common/form/tagfield`)與時間線衝突。 (CQ-4350751)


## WCM {#wcm-6516}

* 推廣預覽操作不應列出要建立的頁面。 (CQ-4266213, SITES-10355)

## 工作流程 {#workflow-6516}

* 手動從中刪除可編輯的工作流模型 `/conf` 使延遲運行時模型實例不具有可編輯模型。 (CQ-4349365)


## 安裝 [!DNL Experience Manager] 6.5.16.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.16.0要求 [!DNL Experience Manager] 6.5請參閱 [升級文檔](/help/sites-deploying/upgrade.md) 的上界。 <!-- UPDATE FOR EACH NEW RELEASE -->
* Service Pack下載可在Adobe上獲得 [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)。
* 在具有MongoDB和多個實例的部署中，安裝 [!DNL Experience Manager] 6.5.16.0在使用包管理器的某個「作者」實例上。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe不建議您刪除或卸載 [!DNL Experience Manager] 6.5.16.0包。 因此，在安裝包之前，應建立 `crx-repository` 以防你需要把它卷回去。 <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for AEM Forms, see [AEM Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### 在上安裝Service Pack [!DNL Experience Manager] 6.5 {#install-service-pack}

1. 如果實例處於更新模式（當實例從早期版本更新時），請在安裝前重新啟動該實例。 Adobe建議在實例的當前正常運行時間較長時重新啟動。

1. 在安裝之前，請拍攝快照或新備份 [!DNL Experience Manager] 實例。

1. 從下載Service Pack [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip)。 <!-- UPDATE FOR EACH NEW RELEASE -->

1. 開啟包管理器，然後選擇 **[!UICONTROL 上載包]** 上載包。 要瞭解更多資訊，請參閱 [包管理器](/help/sites-administering/package-manager.md)。

1. 選擇包，然後選擇 **[!UICONTROL 安裝]**。

1. 要更新S3連接器，請在安裝Service Pack後停止實例，用安裝資料夾中提供的新二進位檔案替換現有連接器，然後重新啟動實例。 請參閱 [AmazonS3資料儲存](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)。

>[!NOTE]
>
>在安裝Service Pack期間，有時會退出包管理器UI上的對話框。 Adobe建議您在訪問部署之前等待錯誤日誌穩定。 請等待與卸載更新程式包相關的特定日誌，然後確保安裝成功。 通常，此問題發生在 [!DNL Safari] 但在任何瀏覽器上都可能間歇性出現。

**自動安裝**

有兩種方法可用於自動安裝 [!DNL Experience Manager] 6.5.16.0。<!-- UPDATE FOR EACH NEW RELEASE -->

* 將包放入 `../crx-quickstart/install` 資料夾。 軟體包將自動安裝。
* 使用 [包管理器中的HTTP API](/help/sites-administering/package-manager.md#package-share)。 使用 `cmd=install&recursive=true` 以便安裝嵌套的軟體包。

>[!NOTE]
>
>Experience Manager6.5.16.0不支援Bootstrap安裝。 <!-- UPDATE FOR EACH NEW RELEASE -->

**驗證安裝**

要瞭解經認證可與此版本配合使用的平台，請參閱 [技術要求](/help/sites-deploying/technical-requirements.md)。

1. 產品資訊頁面(`/system/console/productinfo`)顯示更新的版本字串 `Adobe Experience Manager (6.5.16.0)` 在 [!UICONTROL 已安裝的產品]。 <!-- UPDATE FOR EACH NEW RELEASE -->

1. 所有OSGi捆綁包 **[!UICONTROL 活動]** 或 **[!UICONTROL 片段]** 在OSGi控制台(使用Web控制台： `/system/console/bundles`)。

1. OSGi捆綁 `org.apache.jackrabbit.oak-core` 版本1.22.14或更高版本(使用Web控制台： `/system/console/bundles`)。 <!-- NPR-39939 for 6.5.16.0 --> <!-- NPR-39436 for 6.5.15.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### 安裝Service Pack [!DNL Experience Manager] Forms {#install-aem-forms-add-on-package}

有關在AEM Forms上安裝Service Pack的說明，請參見 [AEM FormsService Pack安裝說明](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)。

### 安裝GraphQL索引包以Experience Manager內容片段 {#install-aem-graphql-index-add-on-package}

使用GraphQL的客戶應安裝 [包含AEMGraphQL索引包1.0.5的內容片段](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.5.zip)。

這使您能夠根據實際使用的功能添加所需的索引定義。

安裝此包失敗可能導致查詢速度慢或失敗的GraphQL。

>[!NOTE]
>
>每個實例只能安裝一次此軟體包；不需要隨每個Service Pack重新安裝它。

### UberJar {#uber-jar}

UberJar [!DNL Experience Manager] 6.5.16.0在 [Maven中央儲存庫](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.15/)。 <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

>[!NOTE]
>
>在Experience Manager6.5.16.0中，UberJar版本(6.5.15.0)與上一版本相同。


要在Maven項目中使用UberJar，請參見 [如何使用UberJar](/help/sites-developing/ht-projects-maven.md) 並在項目POM中包括以下依賴關係： <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.15</version>
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
| 整合 | 的 **[!UICONTROL AEM雲服務選擇加入]** 螢幕已棄用，因為 [!DNL Experience Manager] 和 [!DNL Adobe Target] 整合更新於 [!DNL Experience Manager] 6.5整合支援Adobe Target標準API。 API使用Adobe IMS驗證， [!DNL Adobe I/O Runtime]。 它支援Adobe發射對儀器的作用日益增強 [!DNL Experience Manager] 頁面進行分析和個性化設定，選擇加入嚮導在功能上無關緊要。 | 配置系統連接、Adobe IMS驗證和 [!DNL Adobe I/O Runtime] 通過各個 [!DNL Experience Manager] 雲服務。 |
| 連接器 | Microsoft®SharePoint® 2010和Microsoft®SharePoint® 2013的AdobeJCR連接器不建議使用 [!DNL Experience Manager] 6.5 | N/A |

## 已知問題 {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->
<!-- REMOVED AS PER CQDOC-20022, JANUARY 23, 2023 * If you install [!DNL Experience Manager] 6.5 Service Pack 10 or a previous service pack on [!DNL Experience Manager] 6.5, the runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) is deleted.
To retrieve your runtime copy, Adobe recommends to synchronize the design-time copy of the custom workflow model with its runtime copy using the HTTP API:
`<designModelPath>/jcr:content.generate.json`. -->

* 請更新可能已使用內容模型的自定義API名稱的GraphQL查詢，以改用內容模型的預設名稱。

* GraphQL查詢可能使用 `damAssetLucene` 索引而不是 `fragments` 。 這可能導致GraphQL查詢失敗，或需要很長時間才能執行。

   為瞭解決問題， `damAssetLucene` 必須配置為包括以下兩個屬性：

   * `contentFragment`
   * `model`

   更改索引定義後，需要重新編製索引(`reindex` = `true`)。

   完成這些步驟後，GraphQL查詢應執行得更快。

* 作為 [!DNL Microsoft®® Windows Server 2019] 不支援 [!DNL MySQL 5.7] 和 [!DNL JBoss®® EAP 7.1]。 [!DNL Microsoft®® Windows Server 2019] 不支援對 [!DNL AEM Forms 6.5.10.0]。

* 如果升級 [!DNL Experience Manager] 實例6.5.0 - 6.5.4到Java™ 11上的最新Service Pack, `RRD4JReporter` 例外情況 `error.log` 的子菜單。 要停止異常，請重新啟動實例 [!DNL Experience Manager]。 <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* 用戶可以在中更名層次結構中的資料夾 [!DNL Assets] 將嵌套資料夾發佈到 [!DNL Brand Portal]。 但是，資料夾的標題未在中更新 [!DNL Brand Portal] 直到重新發佈根資料夾。

* 當用戶首次以自適應格式選擇配置欄位時，「屬性瀏覽器」中不會顯示保存配置的選項。 選擇以在同一編輯器中配置自適應表單的其它一些欄位可解決此問題。

* 在安裝期間可能顯示以下錯誤和警告消息 [!DNL Experience Manager] 6.5.x.x:
   * &quot;當Adobe Target整合配置在 [!DNL Experience Manager] 使用目標標準API（IMS驗證），然後將體驗片段導出到目標會導致建立錯誤的提供類型。 Target不是「體驗片段」/源「Adobe Experience Manager」，而是建立多個「HTML」/源「Adobe Target經典」類型的產品。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`:未在花崗岩/操作/維護中找到維護窗口。
   * 當使用SUM、MAX和MIN等集合函式(CQ-4274424)時，Adaptive Form伺服器端驗證失敗。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`  — 在花崗岩/操作/維護處找不到維護窗口。
   * 通過Sobler Banner查看器預覽資產時，Dynamic Media互動式影像中的熱點不可見。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` :等待註冊更改完成註銷時超時。

* 當嘗試移動/刪除/發佈內容片段或站點/頁面時，當回遷內容片段引用時會出現問題，因為後台查詢失敗；即，該功能不起作用。
要確保正確操作，必須將以下屬性添加到索引定義節點 `/oak:index/damAssetLucene` （不需要重新索引）:

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

* 在AEM Forms,POP3協定不適用於Microsoft® Office 365的電子郵件端點。
* 在JBoss® 7.1.4平台上，當用戶安裝AEM6.5.16.0 Service Pack時， `adobe-livecycle-jboss.ear` 部署失敗。

## 包括OSGi捆綁包和內容包 {#osgi-bundles-and-content-packages-included}

以下文本文檔列出了包含在 [!DNL Experience Manager] 6.5.16.0 : <!-- UPDATE FOR EACH NEW RELEASE -->

* [6.5.16.0Experience Manager中包含的OSGi捆綁包清單](/help/release-notes/assets/65160_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [6.5.16.0Experience Manager中包含的內容包清單](/help/release-notes/assets/65160_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 受限網站 {#restricted-sites}

這些網站僅供客戶訪問。 如果您是客戶，需要訪問，請與Adobe客戶經理聯繫。

* [產品下載，網址為licensing.adobe.com](https://licensing.adobe.com/)
* [聯繫Adobe客戶支援](https://experienceleague.adobe.com/docs/customer-one/using/home.html)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 產品頁](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5文檔](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hant)
>* [訂閱 Adobe 優先產品更新](https://www.adobe.com/tw/subscription/priority-product-update.html)

