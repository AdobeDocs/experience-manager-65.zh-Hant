---
title: 版本注意事項 [!DNL Adobe Experience Manager] 6.5
description: 尋找版本資訊、新增功能、安裝作法和詳細的變更清單 [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: a52311b9-ed7a-432e-8f35-d045c0d8ea4c
source-git-commit: 4035bfae6a525292ca71b182ebed2ac9839426b8
workflow-type: tm+mt
source-wordcount: '3050'
ht-degree: 3%

---

# [!DNL Adobe Experience Manager] 6.5最新Service Pack發行說明 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, November 30, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## 發行資訊 {#release-information}

| 產品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.21.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 類型 | Service Pack發行 |
| 日期 | 2024年6月6日（星期四） <!-- UPDATE FOR EACH NEW RELEASE --> |
| 下載 URL | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.21.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## 包含的內容 [!DNL Experience Manager] 6.5.21.0 {#what-is-included-in-aem-6521}

[!DNL Experience Manager] 6.5.21.0包括新功能、客戶要求的重要增強功能和錯誤修正。 此外，還包含自2019年4月6.5首次推出以來的效能、穩定性和安全性改善專案。 [安裝此Service Pack](#install) 於 [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

## 主要功能和增強功能

<!-- * _6.5.21.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

此版本中的部分主要功能和增強功能包括：

* 新的、更易於使用伺服器對伺服器驗證的認證，取代現有的服務帳戶(JWT)認證。 (NPR-41994)

### [!DNL Assets]

#### 增強功能

以下是此版本中包含的增強功能清單：

* IPTC標籤現在支援 [!UICONTROL 替代文字] 和 [!UICONTROL 延伸說明] 文字欄位。 (ASSETS-34918)

#### 協助工具修正

以下是此版本中包含的協助工具修正清單：

* 如果資產的處理狀態為「失敗」或「中繼資料失敗」，註解和音訊追蹤UI將無法正常運作。 (ASSETS-37281)
* 當您儲存資產中繼資料並嘗試編輯時，語言名稱未顯示。 (ASSETS-37281)

<!-- ### [!DNL Forms]
* A -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## 已修正Service Pack 21中的問題 {#fixed-issues}

### [!DNL Sites]{#sites-6521}

#### 親和力 {#sites-accessibility-6521}

* 此 **[!UICONTROL 已儲存的搜尋]** 標籤不是永久性的。 預留位置是做為文字欄位的唯一視覺標籤。 (SITES-3050)

#### 管理員使用者介面{#sites-adminui-6521}

* 當您按一下 **[!UICONTROL 網站]** > **[!UICONTROL 核心元件]** > **[!UICONTROL 屬性]** > **[!UICONTROL 許可權]** 標籤> **[!UICONTROL 有效許可權]**，則 **有效許可權** 對話方塊無法在中開啟。 (SITES-17378)

<!-- #### Classic UI{#sites-classicui-6521} 

* A -->

#### [!DNL Content Fragments]{#sites-contentfragments-6521}

* 修正表單元素重複納入的問題。 (SITES-21109)
* 建立內容片段時，「關閉」按鈕有時會停止回應，導致整個頁面凍結，並需要重新整理頁面來關閉內容片段。 至於版本建立問題，系統正在建立內容片段的新版本。 即使使用者未進行任何變更，只要與RTE或文字欄位互動，就會發生此問題。 (SITES-21187)

#### [!DNL Content Fragments] - GRAPHQL API {#sites-graphql-api-6521}

* 將Adobe Experience Manager從6.5.19.0升級至6.5.20.0時，路徑為 `/libs/cq/graphql/sites/graphiql` 即將刪除。 (SITES-20098)

<!-- #### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6521}

* W -->

<!-- #### [!DNL Content Fragments] - REST API{#sites-restapi-6521}

* W -->

<!-- #### Core Backend{#sites-core-backend-6521}

* W -->

<!-- #### Core Components{#sites-core-components-6521}

* I -->

<!-- #### Campaign integration{#sites-campaign-integration-6521}

* A -->

#### 體驗片段{#sites-experiencefragments-6521}

* 從轉出體驗片段 `masters/language` 至 `country/language` 不會更新互動參照。 (SITES-21172)
* 範本不僅指定於 `cq:allowedTemplates`，但範本具有 `allowedPaths` 在範本層級設定，在建立新的體驗片段時顯示為選項。 (SITES-20855)

<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6521}

* T -->

<!-- #### Launches{#sites-launches-6521} -->

<!-- DELETED MAY 22, 2024 FROM TOTAL RELEASE CANDIDATE ISSUES * The `sourceRootResource` configured in the Launch configuration within CRXDE Lite points to content that no longer exists, leading to a malfunction when attempts are made to delete launches. Delete launches even if the page is deleted or if the path is not the same. (SITES-20750) -->

#### MSM — 即時副本{#sites-msm-live-copies-6521}

* 覆蓋頁面元件以在頁面屬性中新增索引標籤。 其中一個是頁面設定，並具有屬性以新增體驗片段URL。 在體驗片段的頁面屬性中設定的連結，不會為該頁面建立的任何語言副本變更。 設定的連結應該會隨著語言副本URL而變更。 (SITES-19580)

#### 頁面編輯器{#sites-pageeditor-6521}

* 編輯模式會以不一致的方式套用灰色背景，而無法符合WCAG （網頁內容可及性指引）色彩對比標準。 (SITES-20060)

### [!DNL Assets]{#assets-6521}

* 如果資產發佈至Brand Portal，發佈狀態仍會不一致。 (ASSETS-36807)
* 使用API呼叫從例項中刪除資產時，不會刪除資產。 (ASSETS-35131)
* 當您嘗試匯入中繼資料時， `question mark (?)` 會取代以英語以外的任何語言插入的字元。  (ASSETS-35091)
* 時間 `dc:title` 屬性會與資料型別字串搭配使用，安裝Service Pack 6.5.19後，資產內容樹狀結構無法正常運作。 (ASSETS-34684)
* 如果資產名稱中有任何特殊字元，便會顯示錯誤。 (ASSETS-33248)

#### [!DNL Dynamic Media]{#assets-dm-6521}

* 在AEM 6.5.18中，當您編輯熱點時，不會顯示新增至資產的所有熱點。 不過，所有熱點都可在已發佈的資產中運作，但如有需要，您稍後無法加以編輯。 (ASSETS-33609)
* 上傳的最新EPS檔案在重新處理後不會產生縮圖。 (ASSETS-32617)
* 在「工具」 > 「資產」 > 「Dynamic Media發佈設定」 > 「請求屬性」標籤中，輸入專案 `Width(px)` 和 `Height(px)` 西班牙文、義大利文和葡萄牙文的外觀會有所不同。 這些位置彼此不對齊。 (ASSETS-31896)
* 自2024年5月1日起，Adobe Dynamic Media停止支援下列專案：
   * SSL (安全通訊端層) 2.0
   * SSL 3.0
   * TLS (傳輸層安全性) 1.0 和 1.1
   * TLS 1.2 中的以下弱密碼：
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_RSA_WITH_AES_256_GCM_SHA384`
      * `TLS_RSA_WITH_AES_256_CBC_SHA256`
      * `TLS_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_AES_128_GCM_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
      * `TLS_RSA_WITH_SDES_EDE_CBC_SHA`

### [!DNL Forms]{#forms-6521}

中的修正 [!DNL Experience Manager] Forms會透過單獨的附加元件套件在排程一週後傳送 [!DNL Experience Manager] Service Pack發行日期。 在此案例中，AEM 6.5.21.0 Forms附加元件套件發行預計於2024年6月13日（星期四）推出。 此部分會在發行後新增Forms修正和增強功能的清單。

<!-- #### [!DNL Adaptive Forms]

* THIS BUG WAS ALREADY REPORTED IN THE 6.5.20.0 RELEASE NOTES. IS IT NEEDED AGAIN IN THE 6.5.21.0 RELEASE NOTES? (AEM Forms on JEE Only) The PDF Generator service fails to enumerate the fonts available on the server. Consequently, the font selection panel on the Adobe PDF Settings page in the PDFG Admin UI remains empty, effectively preventing (un)embedding of chosen fonts. (FORMS-12095) -->


<!-- #### [!DNL Forms Designer] {#forms-designer-6521}

* W -->

### Foundation {#foundation-6521}

#### Apache Felix {#foundation-apachefelix-6521}

* AEM 6.5 Service Pack 19 (SP19)的升級問題，其中在SP19安裝後，對Apache Felix發出的未經授權請求遺失應用程式伺服器內容根路徑。 Apache Felix Web Management Console 4.9.8的更新。 (NPR-41933)

#### 行銷活動{#foundation-campaign-6521}

* AEM 6.5 Service Pack 15會產生持續性錯誤記錄，其中包含重要的專案。 已報告下列問題：

   * 路徑中缺少資源時出現404 INFO錯誤 `/libs/granite/ui/content/shell/start.html`
   * 由於下列原因，未攔截到SlingException的錯誤記錄專案 `NullPointerException` 在 `CampaignsDataSourceServlet.java:147`

  錯誤記錄檔不應填入頻繁且大量的錯誤專案，AEM執行個體應可正常運作，而不會出現資源遺失或例外狀況的相關問題。 (CQ-4357064)

#### 雲端服務{#foundation-cloudservices-6521}

* 從AEMCloud Service中移除Google Guava。 (CQ-4356436)

<!-- #### Communities {#foundation-communities-6521}

* U -->

<!-- #### Content distribution{#foundation-content-distribution-6521}

* T -->

#### Granite{#foundation-granite-6521}

* 您無法選取 **刪除** 或 **修改** 不含 **瀏覽** 設定瀏覽器中的許可權。 (GRANITE-51002)

#### 整合{#foundation-integrations-6521}

* 相關 `cq-target-integration`，需要移除Google Guava的非測試使用方式。 (CQ-4357101)
* 以OAuth2伺服器對伺服器認證（也稱為服務主體）取代服務帳戶（JSON Web權杖或JWT）認證。 (NPR-41994)
* 建立對象請求因IMS (Identity Management系統)設定而失敗。 (NPR-41888)
* 當客戶嘗試檢視裝載頁面時，由於URL格式錯誤，內容未正確顯示；顯示404錯誤。 URL中查詢引數前缺少問號符號造成錯誤。 此問題需要客戶插入問號符號，才能正確檢視裝載頁面。 (NPR-41957)
* 從AEM 6.5中移除程式碼和AdobeSearch&amp;Promote的相依性（這已結束的生命週期為） [2022年9月（依通知）](https://experienceleague.adobe.com/en/docs/discontinued/using/search-promote). (NPR-41855)

#### 本地化{#foundation-localization-6521}

* 在範本編輯器中，文字字串 *`No video available.`* 未本地化。 (SITES-13190)
* 啟用或停用使用者後的字串不會在中本地化 **工具** > **安全性** > **使用者** > *any_user_name* > **啟動** > **確定**，並選取 *any_user_name* > **停用** > **確定**. (NPR-41737)

#### Oak {#foundation-oak-6521}

* 效能回歸修正 — 避免在類似條件上進行範圍查詢。 (OAK-9481)

* 新Oak版本為1.22.20。

#### Platform{#foundation-platform-6521}

* 此 `Unclosed resource resolver` 發生下列錯誤： `com.day.cq.mailer.impl.DefaultMailService`. 此 `MessageGatewayService` 類別（現成可用）在沒有資源解析程式的情況下使用。 任何具有表單提交按鈕的頁面上，發生使用此類別傳送電子郵件的問題。 (NPR-41853)
* 在 **關於Adobe Experience Manager** 對話方塊中，版權年份仍為2023。 (CQ-4356349)


<!-- #### Sling{#foundation-sling-6521}

* T -->

#### 轉換{#foundation-translation-6521}

* AEM 6.5.19現成可用翻譯狀態未依啟動預期更新的問題。 將已翻譯檔案匯入與AEM啟動相關聯的翻譯工作後，狀態應變更為 `Approved`. 相反地，狀態已變更為 `Ready for Review`，這不是預期行為。 (NPR-41756)
* 建立多個設定並前往翻譯Cloud Service設定時，並非所有元素都會顯示在UI中。 只會顯示前40個元素/資料夾；會觸發延遲載入，但不會新增更多內容。 (NPR-41829)
* 如果觸控使用者介面的「許可權」頁面上有日文，則會出現亂碼字元。 (NPR-41794)
* AEM 6.5.14和6.5.9不傳送要翻譯的emoji。 (CQ-4357000)

#### 使用者介面{#foundation-ui-6521}

* 在「工具>安全性>使用者」 > &lt;user_name> >設定檔，在 **編輯使用者設定** 對話方塊中，按一下「取消」並不會結束對話方塊。 (NPR-41793)
* Granite `pathfield` 元件於 `/libs/granite/ui/components/coral/foundation/form/pathfield` 無法啟用 **[!UICONTROL 選取]** 按鈕。 在路徑欄位彈出後，使用者選取資產核取方塊，然後 **[!UICONTROL 選取]** 按鈕未啟用；它不會從灰色變更為藍色。 (NPR-41970)
* AEM中的內容片段模型(CFM)參考欄位存在問題。 雖然CFM參考欄位已設為必要，系統仍可讓使用者按一下「儲存」 ，以在某些案例中使用非CFM值儲存內容。 「儲存」按鈕應該會變暗（無法使用）。 (NPR-41894)
* 標準Coral使用者介面對話方塊，使用 `successresponse` 動作必須在動作之後觸發成功回應。 但在AEM 6.5 Service Pack 19中，不會叫用重新載入動作，且不會顯示任何訊息。 (NPR-41797)
* AEM 6.5 Service Pack 18中的AEM通知連結無法運作。 升級至Service Pack 18時，透過通知按鈕選取訊息時，AEM通知連結無法運作。 (NPR-41792)

<!-- #### WCM{#foundation-wcm-6521}

* T -->

#### 工作流程{#foundation-workflow-6521}

* 在AEM 6.5.18中，在清除期間從使用者中繼資料快取中移除時出現重複錯誤。 (NPR-41762)

## 安裝 [!DNL Experience Manager] 6.5.21.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.21.0需要 [!DNL Experience Manager] 6.5.請參閱 [升級檔案](/help/sites-deploying/upgrade.md) 以取得詳細指示。 <!-- UPDATE FOR EACH NEW RELEASE -->
* Service Pack下載專案可在Adobe上取得 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.21.0.zip).
* 在具有MongoDB和多個執行個體的部署上，安裝 [!DNL Experience Manager] 使用封裝管理程式的其中一個Author執行個體上的6.5.21.0 。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe不建議您移除或解除安裝 [!DNL Experience Manager] 6.5.21.0套件。 因此，在安裝套件之前，您應該建立 `crx-repository` 以防您必須將其回覆。 <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### 安裝Service Pack於 [!DNL Experience Manager] 6.5{#install-service-pack}

1. 如果執行個體處於更新模式（從舊版更新執行個體時），請在安裝前重新啟動執行個體。 如果執行個體的目前運作時間很高，Adobe建議重新啟動。

1. 安裝之前，請拍攝快照或進行全新備份 [!DNL Experience Manager] 執行個體。

1. 從下載Service Sack [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.21.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. 開啟封裝管理員，然後選取 **[!UICONTROL 上傳套裝]** 以上傳套件。 若要瞭解更多，請參閱 [封裝管理員](/help/sites-administering/package-manager.md).

1. 選取封裝，然後選取 **[!UICONTROL 安裝]**.

1. 若要更新S3聯結器，請在安裝Service Pack後停止執行個體，將現有聯結器取代為安裝資料夾中提供的新二進位檔案，然後重新啟動執行個體。 另請參閱 [Amazon S3資料存放區](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Service Pack安裝期間，Package Manager UI上的對話方塊有時會退出。 Adobe建議您先等待錯誤記錄穩定下來，再存取部署。 等待與更新程式套件組合解除安裝相關的特定記錄，再確認安裝成功。 此問題通常發生在 [!DNL Safari] 瀏覽器，但可能間歇性地在任何瀏覽器中發生。

**自動安裝**

有兩種不同的安裝方法 [!DNL Experience Manager] 6.5.21.0。<!-- UPDATE FOR EACH NEW RELEASE -->

* 將套件置於 `../crx-quickstart/install` 資料夾（當伺服器線上上可用時）。 套件會自動安裝。
* 使用 [來自封裝管理員的HTTP API](/help/sites-administering/package-manager.md#package-share). 使用 `cmd=install&recursive=true` 以便安裝巢狀套件。

>[!NOTE]
>
>Experience Manager6.5.21.0不支援Bootstrap安裝。 <!-- UPDATE FOR EACH NEW RELEASE -->

**驗證安裝**

若要瞭解經過認證可搭配此版本使用的平台，請參閱 [技術需求](/help/sites-deploying/technical-requirements.md).

1. 產品資訊頁(`/system/console/productinfo`)顯示更新的版本字串 `Adobe Experience Manager (6.5.21.0)` 在 [!UICONTROL 已安裝的產品]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. 所有OSGi套件組合都是 **[!UICONTROL 作用中]** 或 **[!UICONTROL 片段]** 在OSGi主控台中(使用Web主控台： `/system/console/bundles`)。

1. OSGi套件 `org.apache.jackrabbit.oak-core` 為1.22.20版或更新版本(使用Web主控台： `/system/console/bundles`)。 <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### 安裝Service Pack for [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

如需在Experience Manager Forms上安裝Service Pack的說明，請參閱 [Experience Manager Forms Service Pack安裝指示](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>調適型表單功能 (適用於 [AEM 6.5 QuickStart](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/implementing/deploying/deploying/deploy)) 僅用於探索和評估目的。若要供生產使用，必須獲得 AEM Forms 的有效許可；調適型表單的功能需要適當許可才可使用。

### 安裝Experience Manager內容片段的GraphQL索引套件{#install-aem-graphql-index-add-on-package}

使用GraphQL的客戶必須安裝 [使用GraphQL索引套件1.1.1Experience Manager內容片段](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

如此一來，您就可以根據使用者實際使用的功能，新增必要的索引定義。

無法安裝此套件可能會導致GraphQL查詢變慢或失敗。

>[!NOTE]
>
>每個執行個體僅安裝此套件一次；不需要隨每個Service Pack重新安裝。

### UberJar{#uber-jar}

The UberJar for [!DNL Experience Manager] 6.5.21.0可在以下網址取得： [Maven中央存放庫](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.21/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

若要在Maven專案中使用UberJar，請參閱 [如何使用UberJar](/help/sites-developing/ht-projects-maven.md) 並在專案POM中加入下列相依性： <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.21</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar和其他相關成品可在Maven中央存放庫上使用，而不是Adobe公共Maven存放庫(`repo.adobe.com`)。 主要UberJar檔案已重新命名為 `uber-jar-<version>.jar`. 因此，不存在 `classifier`，使用 `apis` 作為值，針對 `dependency` 標籤之間。


## 過時和移除的功能{#removed-deprecated-features}

另請參閱 [過時和移除的功能](/help/release-notes/deprecated-removed-features.md/).

## 已知問題{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.-->

<!-- * **Page publishing not working in Page Editor after upgrading to Service Pack 18 (6.5.18.0)** -->

<!-- https://jira.corp.adobe.com/browse/SITES-15856 REMOVE FOR 6.5.19.0 -->
<!-- After you upgrade an instance of AEM 6.5.0.0&mdash;6.5.17.0 to AEM 6.5.19.0, when you click **Publish Page** inside the Page Editor, you are redirected to a URL that does not exist.

  To work around this issue, do one of the following:

  * Remove the following "path" property.

       `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/publish/granite:data`

  * Paste the correct URL directly into the browser.

       `http://localhost:4504/editor.html/libs/wcm/core/content/sites/publishpagewizard.html?item=/content/we-retail/language-masters/en/about-us.html` -->


* **與Oak相關**
從Service Pack 13及更高版本開始，下列錯誤記錄檔開始出現，這會影響持續性快取：

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.0.202/5]
  at org.h2.mvstore.DataUtils.newMVStoreException(DataUtils.java:1004)
      at org.h2.mvstore.MVStore.getUnsupportedWriteFormatException(MVStore.java:1059)
      at org.h2.mvstore.MVStore.readStoreHeader(MVStore.java:878)
      at org.h2.mvstore.MVStore.<init>(MVStore.java:455)
      at org.h2.mvstore.MVStore$Builder.open(MVStore.java:4052)
      at org.h2.mvstore.db.Store.<init>(Store.java:129)
  ```

  或

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.1.214/5].
  ```

  若要解決此例外狀況，請執行下列動作：

   1. 刪除以下兩個資料夾 `crx-quickstart/repository/`

      * `cache`
      * `diff-cache`

   1. 安裝Service Pack，或重新啟動Experience Manageras a Cloud Service。
的新資料夾 `cache` 和 `diff-cache` 都會自動建立，而您不會再遇到與相關的例外狀況 `mvstore` 在 `error.log`.

* 更新可能已使用您內容模型的自訂API名稱的GraphQL查詢，以改用內容模型的預設名稱。

* GraphQL查詢可能使用 `damAssetLucene` 索引而非 `fragments` 索引。 此動作可能會導致GraphQL查詢失敗或需要很長時間才能執行。

  若要修正問題， `damAssetLucene` 必須設定為包含下列兩個屬性： `/indexRules/dam:Asset/properties`：

   * `contentFragment`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/contentFragment"`
      * `propertyIndex="{Boolean}true"`
      * `type="Boolean"`
   * `model`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/data/cq:model"`
      * `ordered="{Boolean}true"`
      * `propertyIndex="{Boolean}true"`
      * `type="String"`

  在索引定義變更後，需要重新索引(`reindex` = `true`)。

  執行這些步驟後，GraphQL查詢應該可以更快執行。

* 嘗試移動、刪除或發佈內容片段、網站或頁面時，在擷取內容片段參考時出現問題。 背景查詢失敗。 也就是說，功能無法運作。
若要確保作業正確，您必須將下列屬性新增至索引定義節點 `/oak:index/damAssetLucene` （不需要重新索引）：

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* 如果您升級您的 [!DNL Experience Manager] 從6.5.0 - 6.5.4執行個體到Java™ 11上最新的Service Pack，您會看到 `RRD4JReporter` 中的例外狀況 `error.log` 檔案。 若要停止例外，請重新啟動您的執行個體， [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* 使用者可以在下列位置重新命名階層中的資料夾： [!DNL Assets] 並將巢狀資料夾發佈至 [!DNL Brand Portal]. 不過，資料夾的標題不會在中更新 [!DNL Brand Portal] 直到重新發佈根資料夾為止。

* 安裝期間可能會顯示下列錯誤和警告訊息 [!DNL Experience Manager] 6.5.x.x：
   * 「當在中設定Adobe Target整合時 [!DNL Experience Manager] 使用Target Standard API （IMS驗證），然後將體驗片段匯出至Target會導致建立錯誤的選件型別。 Target會建立多個具有「HTML」/來源「Adobe Target Classic」型別的選件，而不是「體驗片段」/來源「Adobe Experience Manager」。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在granite/operations/maintenance找不到維護時段。
   * 使用彙總函式(例如SUM、MAX和MIN)時，Adaptive Form伺服器端驗證會失敗(CQ-4274424)。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` ：在granite/operations/maintenance找不到維護時段。
   * 透過Shoppable Banner檢視器預覽資產時，不會顯示Dynamic Media互動影像中的熱點。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` ：等待登入變更完成解除登入逾時。

* 從AEM 6.5.15開始，Rhino JavaScript Engine由 ```org.apache.servicemix.bundles.rhino``` 捆綁有新的提升行為。 使用嚴格模式的指令碼(```use strict;```)必須宣告其正確的變數。 否則，它們不會執行，並最終擲回執行階段錯誤。

* 透過官方更新套件安裝與標籤相關的現成可用內容會重設的 `/content/cq:tags` 節點預設為。 此動作適用於Service Pack、Security Service Pack、Extended Feature Pack、Cumulative Feature Pack、修補程式等。 因此，在安裝之前，必須從屬性新增它。

### AEM Sites的已知問題 {#known-issues-aem-sites-6521}

* SITES-17934 - 內容片段 - 大型片段樹有 DoS 保護，因此預覽失敗。請參閱 [有關預設GraphQL查詢執行器設定選項的知識庫文章](https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-23945)

### AEM Forms的已知問題 {#known-issues-aem-forms-6521}

* 在以XDP為基礎且核取方塊上有內嵌指令碼的最適化表單中，此類核取方塊之後的元素不會執行指令碼。 (FORMS-14244)
* 使用者無法建立通訊管理信件。 當使用者建立字母時，出現說明錯誤&quot;`Object Object`「」出現，且字母未建立。 配置圖縮圖也無法載入字母建立畫面上。 您可以安裝 [最新AEM 6.5 Form Service Pack 20 (6.5.20.0)](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases) 以解決問題。 (FORMS-13496)
* 互動式通訊服務會建立PDF檔案，但使用者的資料不會自動填入表單欄位中。 預填服務未如預期運作。 您可以安裝 [最新AEM 6.5 Form Service Pack 20 (6.5.20.0)](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases) 以解決問題。 (FORMS-13413， FORMS-13493)
* 無法載入automated forms conversion服務的檢閱和修正(RnC)編輯器。 您可以安裝 [最新AEM 6.5 Form Service Pack 20 (6.5.20.0)](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases) 以解決問題。 (FORMS-13491)
* 從AEM 6.5 Forms Service Pack 18 (6.5.18.0)或AEM 6.5 Forms Service Pack 19 (6.5.19.0)更新至AEM 6.5 Forms Service Pack 20 (6.5.20.0)後，使用者會遇到JSP編譯錯誤。 他們無法開啟或建立最適化表單，且其他AEM介面(如頁面編輯器、AEM Forms UI和AEM Workflow編輯器)發生錯誤。 您可以安裝 [最新AEM 6.5 Form Service Pack 20 (6.5.20.0)](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases) 以解決問題。 (FORMS-13492)
* 在具有編輯/顯示模式的欄位中，在快顯Widget中瀏覽月份時，日期選擇器Widget中的列會被截斷。 (FORMS-13620)
* 嘗試在後端使用DOR （記錄檔案）服務時，表單提交失敗。 遇到的錯誤訊息為：「提交動作無法完成，因為未正確指派表單資源。」 (FORMS-13798)
* 從Adobe Experience Manager發佈執行個體提交最適化表單至Adobe Experience Manager Workflow時，工作流程無法儲存附件。 (FORMS-14209)
* 安裝AEM 6.5 Forms Service Pack 20套件(適用於SP20的AEM Forms附加元件套件)時，AEM Sites使用者介面(UI)效能大幅降低。 (FORMS-13791)
* 預填服務在互動式通訊中失敗，並出現Null指標例外狀況。 (CQDOC-21355)
* 最適化Forms可讓您搭配ECMAScript 5或更早版本使用自訂函式。 當自訂函式使用ECMAScript第6版或更新版本時，例如 `let`， `const`或箭頭功能，規則編輯器可能無法正確開啟。

## 包含的OSGi套件組合和內容套件{#osgi-bundles-and-content-packages-included}

下列文字檔案列出此套件中包含的OSGi套件組合和內容套件 [!DNL Experience Manager] 6.5 Service Pack版本：

* [Experience Manager6.5.21.0中包含的OSGi套件組合清單](/help/release-notes/assets/65210-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager6.5.21.0中包含的內容套件清單](/help/release-notes/assets/65210-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 受限制的網站{#restricted-sites}

這些網站僅供客戶使用。 如果您是客戶且需要存取權，請聯絡您的Adobe客戶經理。

* [產品下載網址為licensing.adobe.com](https://licensing.adobe.com/)
* [聯絡Adobe客戶支援](https://experienceleague.adobe.com/en/docs/customer-one/using/home).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 產品頁面](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5檔案](https://experienceleague.adobe.com/en/docs/experience-manager-65)
>* [訂閱Adobe優先產品更新](https://www.adobe.com/tw/subscription/priority-product-update.html)
