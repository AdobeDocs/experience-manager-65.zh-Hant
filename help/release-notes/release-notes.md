---
title: 的發行說明 [!DNL Adobe Experience Manager] 6.5
description: 查找發行資訊、新功能、安裝操作說明，以及 [!DNL Adobe Experience Manager] 6.5。
mini-toc-levels: 3
source-git-commit: ea90bd913b437a564fb50e01af7719510fa22e74
workflow-type: tm+mt
source-wordcount: '2692'
ht-degree: 2%

---

# [!DNL Adobe Experience Manager] 6.5最新Service Pack發行說明 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/Documents/issue_tracker_sp_cfp_updates.xlsx?d=w3ea81ae4e6054153b132f2698c86f84e&csf=1&web=1&e=WRAZ43&nav=MTVfezk2OTJDQTNFLUI4QTQtNDY2RS05NEVCLUQ5QjcyNEVENkJDNn0 -->

## 發行資訊 {#release-information}

| 產品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.16.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 類型 | Service Pack發行 |
| 日期 | 2023年2月23日星期四 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 下載 URL | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]be/packages/cq650/servicepack/aem-service-pkg-6.5.16.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## 包含的項目 [!DNL Experience Manager] 6.5.16.0 {#what-is-included-in-aem-6516}

[!DNL Experience Manager] 6.5.16.0包含自2019年4月初次發行6.5以來所推出的新功能、客戶要求的重要增強功能、錯誤修正以及效能、穩定性和安全性等改善項目。 [安裝此Service Pack](#install) on [!DNL Experience Manager] 6.5。 <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

Dynamic Media的主要改善如下：

推出全新通訊協定DASH(Dynamic Adaptive Streaming over HTTP)支援，以在Dynamic Media視訊傳送中適用性位元速率串流（含CMAF） [常見媒體應用程式格式] 已啟用)。

* 最適化串流(DASH/HLS)可確保提供更佳的視訊使用者檢視體驗。
* DASH是自適應視頻流的國際標準協定，在業界得到廣泛的應用。
* 現在在北美推出（通過支援票啟用），很快將在亞太和歐洲 — 中東 — 非洲推出。

請參閱 [在您的帳戶上啟用DASH](/help/assets/video.md#enable-dash).

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets] {#assets-6516}

* 連線資產：當您為遠端DAM上的影像啟用「智慧型裁切」選項、將影像上傳至資料夾，以及將資料夾同步至本機網站時，本機Sites部署中不會開啟資料夾。 (NPR-39912)
* 依名稱排序集合時，清單檢視無法正常運作(ASSETS-19401)
* 將大型媒體檔案(JPEG)上傳至集合時，Experience Manager會停止回應。 (ASSETS-19387)
* 在內容樹狀結構窗格中，顯示的資產名稱不正確，因為資產的位置未正確呈現。 (ASSETS-18870)
* 使用連結共用集合時，URL中的資料會在資訊卡檢視和清單檢視的混洗之間不相符。 (ASSETS-18758)
* 對資料夾類型使用篩選器來執行Omnisearch時，搜尋結果會不一致。 (ASSETS-18227)
* 此 `dam:size` XMP回寫後屬性不會更新，這會導致從傳回的資訊不正確 `/platform/path/to/asset.jpg;resource=metadata` API。 (ASSETS-17631)
* 所有Experience Manager例項上無結尾標籤的資源解析器。 (ASSETS-16904)
* 即使您已獲指派 `create` 和 `modify` 權限。 (ASSETS-15956)
* 此 `move` 將資產從一個點移動至另一個點時，按鈕會隨機停用。 (ASSETS-14889)
* 螢幕助讀程式無法識別標題，因為文字未在標題標籤內定義，而是一般文字。 (ASSETS-6924)
* 影像下的替代文字並非強制性，但影像下顯示的文字會重複使用 `Type` 屬性。 (ASSETS-6915)


## [!DNL Assets] - [!DNL Dynamic Media] {#dm-6516}

* 表單元素不包含標籤。 有了NVDA和JAWS等螢幕助讀程式，表單標籤資訊無法正確宣佈。 (CQ-4344078)
* 當 `Escape` 鍵用於鍵盤。 (CQ-4344077)
* 提供無效輸入後，針對內嵌錯誤建議顯示的「資訊」圖示（字母「i」）無法使用鍵盤存取。 (CQ-4344076)
* `getManifestURI` 由於JCR屬性被讀取為，傳回null `toString` 而非 `getString`. (ASSETS-18674)
* SmartCrop視訊元件無法正常運作。 元件執行播放（而非串流），而VTT呼叫失敗，導致404錯誤。 (ASSETS-18468)
* 選取 **[!UICONTROL 屬性]** 在資產的「檢視器」頁面上，會造成Null指標例外狀況。 (ASSETS-18420)
* [!DNL Experience Manager] DASH串流的使用者介面變更，包含下列項目：
   * 在視訊設定檔編輯器中有可見的CMAF（通用媒體應用程式格式）欄位。
   * 具有視訊上傳程式會傳送CMAF標幟。
   * 選項 **[!UICONTROL 自動]**, **[!UICONTROL hls]**，和 **[!UICONTROL 破折號]** 現在可在檢視器預設集編輯器的播放下拉式清單中使用 **[!UICONTROL 行為]** 標籤。
(ASSETS-17428)
* 在導覽中選取 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]** > **[!UICONTROL 建立]** > **[!UICONTROL 轉盤集]**，則圖片表徵圖與「幻燈片1」文本字串重疊。 (ASSETS-18578)
* 系統會重新發佈未發佈的資產。 (ASSETS-16428)
* Experience Manager作者因載入問題而關閉，提示建立合成警報。 (ASSETS-15937)
* 在Dynamic Media「一般設定」頁面中，會顯示未翻譯的錯誤訊息 `Failed to fetch data` 框。 (ASSETS-15617)

## [!DNL Forms] {#forms-6516}

### [!DNL Forms] 主要功能 {#forms-features-6516}

* [無頭式適用性Forms](https://experienceleague.corp.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) 可讓您的開發人員建立、發佈及管理可透過API存取和互動的互動式表單，而非透過傳統的圖形使用者介面。

* [適用性Forms核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#features) 是一組24個開放原始碼、符合BEM規範的元件，建置於Adobe Experience Manager WCM核心元件之上。 這些元件是開放原始碼，讓開發人員能夠輕鬆自訂和擴充這些元件，以符合其組織的特定需求。 任何具備定制技能的人 [WCM核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/authoring.html?lang=en) 可輕鬆自訂和設定這些元件的樣式。

* OSGi上的Reader擴充功能服務現在提供個別選項，以啟用PDF的匯入和匯出使用權，以在Adobe Acrobat Reader中匯入或匯出資料。 (NPR-39909)

### [!DNL Forms] 修正 {#forms-fixes-6516}

* 使用「指派任務」**步驟來傳送指派任務的通知時，會傳送兩封電子郵件，而非一封給指派的個人。 (NPR-40078)
* 當使用者隱藏表格標題時，會取消設定先前設定的欄寬，而所有欄會保留相同的寬度。 (NPR-40063)
* 如果您將管理員使用者的預設密碼從 `admin`，同時執行 `Prepare Adobe Experience Manager Server For DSC deployment` 檢查AEM Forms JEE service pack失敗。 (NPR-40062)、(NPR-39387)
* OutputService和AssemblerService API無法將PDF表單轉換為PDF/A。(NPR-39990)
* 組合器服務無法將PDF轉換為PDF/A。當使用者將PDF轉換為PDF/A時，會發生下列錯誤： `PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Summary" ignoreUnusedResources="true" allowCertificationSignatures="true"> <Violation count="6" key="PDFA_CS_001_NOT_DEVICE_INDEPENDENT" description="ColorSpace is not device independent`. (NPR-39956)
* 當GuideSubmitServlet API呼叫的伺服器端驗證失敗時，傳送至用戶端的回應中不會傳回錯誤。 (NPR-39925)
* 在Windows伺服器上升級至AEM 6.5.15.0 Service Pack後，使用者遇到多個錯誤訊息，且電子郵件服務無法運作。(NPR-39919)
* 升級至AEM 6.5.14.0並使用importData服務來將PDF與XML合併時，會發生下列錯誤： `Caused by: java.lang.NoSuchMethodError: com.adobe.xfa.form.FormModel.isXFABarcode(Lcom/adobe/xfa/Node;)Ljava/lang/Boolean`.(NPR-39807)
* 使用者安裝時 **文檔安全辦公室** 擴充功能，發生下列問題：
   * Microsoft® Excel經常當機。
   * 開啟安全文檔時， **檔案安全辦公室** 未在電腦上檢測到已安裝擴展。 指示使用者下載並安裝安全性擴充功能。 (NPR-39768)
* 使用者升級至AEM 6.5.15.0 Service Pack後，PostScript轉Pdf轉換無法運作。 (NPR-39765)、(NPR-39764)
* 當使用者在開啟適用性表單後嘗試開啟導覽畫面時，畫面會因NullPointer例外狀況而失敗：`[172.17.0.1[1662032923933]GET/libs/fd/af/content/editors/form/tour/content.htmlHTTP/1.1]com.day.cq.wcm.core.impl.WCMDebugFilterException:org.apache.sling.api.scripting.ScriptEvaluationException:”` (NPR-39654)
* 在Windows中，當使用者啟用高對比黑色設定時，當HTML5 Forms內容在瀏覽器中以HTML預覽呈現時變得不清楚。 (NPR-39018)

## 整合 {#integrations-6516}

* 從Experience Manager6.5中移除AdobeSearch&amp;Promote程式碼和相依性。AdobeSearch&amp;Promote於2022年9月終止服務。 請參閱 [AdobeSearch&amp;Promote服務終止公告](https://experienceleague.adobe.com/docs/discontinued/using/search-promote.html?lang=en). (NPR-39706)

## [!DNL Sites] {#sites-6516}

* 目前 `cq-wcm-core` artifactory版本沒有POM。 (SITES-10983)
* 轉出預覽動作不應列出要建立的頁面。 (SITES-10355、CQ-4266213)
* MSM分離重新建立分離的頁面後轉出。 (SITES-9841)
* 建立啟動是逾時；使用者必須在載入畫面上等候多分鐘，請求才會逾時。 (SITES-9051)
* 轉出頁面使用者介面顯示不存在的上層頁面路徑。 您可以轉出含有成功訊息的頁面，但子頁面不會轉出，因為父頁面原本不會轉出。 (SITES-8621)

### [!DNL Sites] - 核心元件 {#sites-core-components-6516}

* 將電子郵件頁面上的連結處理集中，因此不再需要模型自訂。 (SITES-9002)

### [!DNL Sites]  — 管理員使用者介面 {#sites-adminui-6516}

* 「CSV匯出」不會匯出所選頁面下的所有頁面。 (SITES-9390)

### [!DNL Sites] - [!DNL Content Fragments] {#sites-contentfragments-6516}

* 無法列印內容片段的JSON。 原因在於開啟內容片段的「預覽」頁面時無法產生GraphQL查詢。 (SITES-8619)
* 重新開啟內容片段模型編輯器時，所有 **[!UICONTROL 日期和時間]** 欄位預設為「日期和時間」類型。 (SITES-8401)

### [!DNL Sites] - [!DNL Experience Fragments] {#sites-experiencefragments-6516}

* 即使範本列在允許的範本下，您仍無法將體驗片段移動至其他資料夾。 (SITES-8601)
* (SITES-7989)


### [!DNL Sites]  — 頁面編輯器 {#sites-pageeditor-6516}

* 更新SITES-8464中資源解析器改良的相依性，其中以製作模式呈現的頁面會產生大量 `TemplatedResourceImpl` 對象。 (SITES-9350)


## Sling {#sling-6516}

* Experience Manager在啟動時死鎖。 (NPR-39832)
* 當Experience Manager的版本儲存中存在許多虛名路徑時，Experience Manager無法啟動。 (NPR-38955)


## 翻譯專案 {#translation-6516}

* 在 `MicrosoftTranslationServiceImpl`，查詢字串參數 `Category` 不正確。 (NPR-39828)
* 建立翻譯專案時會顯示錯誤 *主版頁資源不存在*;不會建立翻譯專案。 (NPR-39762)
* 無法在使用人工翻譯連接器的翻譯專案上設定到期日。 (NPR-39593)

## 使用者介面 {#ui-6516}

* 變更為較小的解析度時，不會顯示DatePicker，而AM/PM選取不會顯示或以可見方式變更。 (NPR-39948)
* 使用縮制js（JavaScript最小化）時，不會因剖析錯誤而處理縮制。 (NPR-39650)
* 標籤欄位(`/libs/cq/gui/components/coral/common/form/tagfield`)與時間軸衝突。 (CQ-4350751)


## WCM {#wcm-6516}

* 轉出預覽動作不應列出要建立的頁面。 (CQ-4266213、SITES-10355)

## 工作流程 {#workflow-6516}

* 手動從中刪除可編輯的工作流模型 `/conf` 留下延遲的執行階段模型例項，而沒有可編輯的模型。 (CQ-4349365)


## 安裝 [!DNL Experience Manager] 6.5.16.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.16.0要求 [!DNL Experience Manager] 6.5.見 [升級檔案](/help/sites-deploying/upgrade.md) 以取得詳細指示。 <!-- UPDATE FOR EACH NEW RELEASE -->
* Service Pack下載可在Adobe上取得 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* 在具有MongoDB和多個實例的部署上，安裝 [!DNL Experience Manager] 6.5.16.0，在使用套件管理器的其中一個製作執行個體上。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe不建議您移除或解除安裝 [!DNL Experience Manager] 6.5.16.0包。 因此，在安裝該包之前，您應建立 `crx-repository` 以防你需要把它卷回去。 <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for AEM Forms, see [AEM Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### 在上安裝Service Pack [!DNL Experience Manager] 6.5 {#install-service-pack}

1. 如果執行個體處於更新模式（從舊版更新執行個體時），請先重新啟動執行個體再進行安裝。 Adobe建議，如果執行個體的目前正常運行時間很長，則重新啟動。

1. 安裝之前，請拍攝快照或對 [!DNL Experience Manager] 例項。

1. 從下載Service Pack [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. 開啟「套件管理器」，然後選取 **[!UICONTROL 上傳套件]** 上傳套件。 要了解更多資訊，請參閱 [封裝管理員](/help/sites-administering/package-manager.md).

1. 選取套件，然後選取 **[!UICONTROL 安裝]**.

1. 若要更新S3連接器，請在安裝Service Pack後停止執行個體，以安裝資料夾中提供的新二進位檔案取代現有連接器，然後重新啟動執行個體。 請參閱 [Amazon S3 Data Store](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>安裝Service Pack時，有時會退出套件管理程式UI上的對話方塊。 Adobe建議您先等待錯誤記錄穩定，再存取部署。 請等待與卸載更新程式捆綁相關的特定日誌，然後確保安裝成功。 通常，此問題會發生在 [!DNL Safari] 瀏覽器，但可在任何瀏覽器上間歇性發生。

**自動安裝**

您可以使用兩種不同的方法來自動安裝 [!DNL Experience Manager] 6.5.16.0。<!-- UPDATE FOR EACH NEW RELEASE -->

* 將包裝放入 `../crx-quickstart/install` 資料夾。 程式包會自動安裝。
* 使用 [來自套件管理器的HTTP API](/help/sites-administering/package-manager.md#package-share). 使用 `cmd=install&recursive=true` 以便安裝嵌套包。

>[!NOTE]
>
>Experience Manager6.5.16.0不支援Bootstrap安裝。 <!-- UPDATE FOR EACH NEW RELEASE -->

**驗證安裝**

若要了解經認證可與此版本搭配使用的平台，請參閱 [技術要求](/help/sites-deploying/technical-requirements.md).

1. 產品資訊頁面(`/system/console/productinfo`)顯示更新的版本字串 `Adobe Experience Manager (6.5.16.0)` 在 [!UICONTROL 已安裝的產品]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. 所有OSGi套件組合 **[!UICONTROL 活動]** 或 **[!UICONTROL 片段]** 在OSGi控制台中(使用Web控制台： `/system/console/bundles`)。

1. OSGi捆綁 `org.apache.jackrabbit.oak-core` 為1.22.14版或更新版本(使用Web控制台： `/system/console/bundles`)。 <!-- NPR-39939 for 6.5.16.0 --> <!-- NPR-39436 for 6.5.15.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### 安裝Service Pack [!DNL Experience Manager] Forms {#install-aem-forms-add-on-package}

如需在AEM Forms上安裝Service Pack的指示，請參閱 [AEM Forms Service Pack安裝指示](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

### 安裝適用於Experience Manager內容片段的GraphQL索引套件 {#install-aem-graphql-index-add-on-package}

使用GraphQL的客戶應安裝 [AEM內容片段搭配GraphQL索引套件1.0.5](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.5.zip). 這可讓使用者根據實際使用的功能，新增所需的索引定義。

>[!NOTE]
>
>每個實例只能安裝一次此包；不需要隨每個Service Pack重新安裝它。

### UberJar {#uber-jar}

UberJar [!DNL Experience Manager] 6.5.16.0可在 [Maven Central存放庫](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.15/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

>[!NOTE]
>
>在Experience Manager6.5.16.0中，UberJar版本(6.5.15.0)與舊版相同。


若要在Maven專案中使用UberJar，請參閱 [如何使用UberJar](/help/sites-developing/ht-projects-maven.md) 並在您的專案POM中加入下列相依性： <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

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
>UberJar和其他相關成品可在Maven中央存放庫中取得，而非AdobePublic Maven存放庫(`repo.adobe.com`)。 主要UberJar檔案已重新命名為 `uber-jar-<version>.jar`. 所以，沒有 `classifier`，使用 `apis` 作為值，對於 `dependency` 標籤。

## 過時的功能 {#removed-deprecated-features}

以下是標示為過時的功能清單 [!DNL Experience Manager] 6.5.7.0。功能在日後的版本中已被標示為過時，且在稍後的版本中已移除。 提供替代選項。

查看您是否在部署中使用了功能。 此外，計畫變更實作以使用替代選項。

| 區域 | 功能 | 替代方案 |
|---|---|---|
| 整合 | 此 **[!UICONTROL AEM雲端服務選擇加入]** 螢幕已過時，因為 [!DNL Experience Manager] 和 [!DNL Adobe Target] 整合已於 [!DNL Experience Manager] 6.5.整合支援Adobe Target Standard API。 API使用Adobe IMS驗證，並 [!DNL Adobe I/O Runtime]. 它支援AdobeLaunch在儀器方面日益發揮的作用 [!DNL Experience Manager] 分析和個人化的頁面，選擇加入精靈的功能與您無關。 | 設定系統連線、Adobe IMS驗證，以及 [!DNL Adobe I/O Runtime] 透過個別 [!DNL Experience Manager] 雲端服務。 |
| 連接器 | Microsoft® SharePoint 2010和Microsoft® SharePoint 2013的AdobeJCR Connector已於 [!DNL Experience Manager] 6.5。 | N/A |

## 已知問題 {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->
<!-- REMOVED AS PER CQDOC-20022, JANUARY 23, 2023 * If you install [!DNL Experience Manager] 6.5 Service Pack 10 or a previous service pack on [!DNL Experience Manager] 6.5, the runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) is deleted.
To retrieve your runtime copy, Adobe recommends to synchronize the design-time copy of the custom workflow model with its runtime copy using the HTTP API:
`<designModelPath>/jcr:content.generate.json`. -->

* 請更新您的GraphQL查詢（可能已使用內容模型的自訂API名稱），改為使用內容模型的預設名稱。

* GraphQL查詢可使用 `damAssetLucene` 索引，而非 `fragments` 索引。 這可能會導致GraphQL查詢失敗，或需花很長時間才能執行。

   為了糾正問題， `damAssetLucene` 必須設定為包含下列兩個屬性：

   * `contentFragment`
   * `model`

   更改索引定義後，需要重新索引(`reindex` = `true`)。

   執行這些步驟後，GraphQL查詢的執行速度應該會更快。

* As [!DNL Microsoft®® Windows Server 2019] 不支援 [!DNL MySQL 5.7] 和 [!DNL JBoss®® EAP 7.1], [!DNL Microsoft®® Windows Server 2019] 不支援全包安裝 [!DNL AEM Forms 6.5.10.0].

* 如果您升級 [!DNL Experience Manager] 從6.5.0到6.5.4的執行個體到Java™ 11上最新的Service Pack，您會看到 `RRD4JReporter` 例外 `error.log` 檔案。 若要停止例外，請重新啟動您的例項 [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

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

* 在AEM Forms中，POP3通訊協定無法用於Microsoft® Office 365的電子郵件端點。
* 在JBoss® 7.1.4平台上，當使用者安裝AEM 6.5.16.0 Service Pack時， `adobe-livecycle-jboss.ear` 部署失敗。

## 包含的OSGi套件組合和內容套件 {#osgi-bundles-and-content-packages-included}

以下文字檔案列出包含在 [!DNL Experience Manager] 6.5.16.0: <!-- UPDATE FOR EACH NEW RELEASE -->

* [Experience Manager6.5.16.0中包含的OSGi套件組合清單](/help/release-notes/assets/65160_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager6.5.16.0中包含的內容套件清單](/help/release-notes/assets/65160_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 受限網站 {#restricted-sites}

這些網站僅供客戶使用。 如果您是Adobe，且需要存取權，請聯絡您的客戶經理。

* [透過licensing.adobe.com下載產品](https://licensing.adobe.com/)
* [聯絡Adobe客戶支援](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 產品頁面](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5檔案](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hant)
>* [訂閱 Adobe 優先產品更新](https://www.adobe.com/tw/subscription/priority-product-update.html)

