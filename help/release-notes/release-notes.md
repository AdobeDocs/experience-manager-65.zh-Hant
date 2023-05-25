---
title: 版本注意事項 [!DNL Adobe Experience Manager] 6.5
description: 尋找版本資訊、新增功能、安裝作法和詳細的變更清單 [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 3
source-git-commit: f8af806bbb78623d5ba12379fc547a2cffc03841
workflow-type: tm+mt
source-wordcount: '2606'
ht-degree: 2%

---

# [!DNL Adobe Experience Manager] 6.5最新Service Pack發行說明 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/Documents/issue_tracker_sp_cfp_updates.xlsx?d=w3ea81ae4e6054153b132f2698c86f84e&csf=1&web=1&e=7yhrWb&nav=MTVfe0U0RjdDQUM3LTZCQ0EtNDk1Qy04Mjc1LTM2MUJEMzE1OEVGN30 -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, June 1, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## 發行資訊 {#release-information}

| 產品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.17.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 類型 | Service Pack發行 |
| 日期 | 2023年5月25日（星期四） <!-- UPDATE FOR EACH NEW RELEASE --> |
| 下載 URL | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.17.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## 包含在 [!DNL Experience Manager] 6.5.17.0 {#what-is-included-in-aem-6517}

[!DNL Experience Manager] 6.5.17.0包括自2019年4月6.5版首次發行以來所推出的新功能、客戶要求的重要增強功能、錯誤修正，以及效能、穩定性和安全性改善專案。 [安裝此Service Pack](#install) 於 [!DNL Experience Manager] 6.5. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

此版本中的部分主要功能和改進如下：

* **搜尋體驗增強功能**  — 您現在可以對搜尋結果中顯示的資產快速執行下列操作：
   * 建立工作流程
   * 建立版本
   * 建立資產關聯或取消關聯

   您不需要導覽至資產位置並檢視其屬性，即可執行這些作業。
* **Dynamic Media _快照_**— 實驗測試影像或Dynamic Media URL，以檢視不同影像修飾元的輸出，以及針對檔案大小（使用WebP和AVIF傳送）、網路頻寬和裝置畫素比的智慧型影像最佳化。 另請參閱 [Dynamic Media快照](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html).
* **使用Dynamic Media進行DASH串流**  — 新通訊協定(DASH - Dynamic Adaptive Streaming over HTTP)已針對Dynamic Media視訊傳送中的最適化資料流推出（已啟用CMAF）支援。 現在所有地區都可使用， [透過支援票證啟用](/help/assets/video.md#enable-dash-on-your-account-enable-dash).

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets]{#assets-6517}

* 當您同時發佈40個以上的PDF時， [!DNL Experience Manager] 會停止回應，並在一段時間內無法使用。 (ASSETS-21789)
* 如果您以測試使用者身分登入，當您按一下資產的屬性時，看不到與特定資產相關的資產。 (ASSETS-21648)
* 使用編輯資產時 `Desktop Actions`，如果您嘗試一次簽入超過五個資產， `Limit Reached` 隨即顯示錯誤並出庫選取的資產。 (ASSETS-21121)
* 無法依集合中的名稱排序資產。 (ASSETS-20924)
* 無法在影像格式型別的資產上設定尺寸。 (ASSETS-20835)
* 共用連結時，「搜尋/新增電子郵件地址」欄位上的工具提示文字及其背景未顯示適當的對比率。 (ASSETS-17347)
* 當您展開時 `Notifications`，因為段落間距，文字無法正確顯示。 (ASSETS-17345)
* 當您在集合中複製資產時， `Public Collection` 核取方塊未正確顯示。 (ASSETS-17343)
* 元素會使用ARIA屬性，但沒有角色。 (ASSETS-17325，ASSETS-17323)
* 展開時連結不是描述性的 `Notifications`. (ASSETS-17283)
* 當您導覽並展開 [!DNL Smart Crop] 按鈕時，內容看起來類似清單，但並未標示為未排序清單。 因此，熒幕助讀程式無法辨識未排序清單，並將它讀為純文字。 (ASSETS-17247)
* 此 `Sort By` 標籤未與其對應的下拉式清單相關聯。 因此，熒幕助讀程式無法辨識下拉式選項。 (ASSETS-17239)
* 嘗試使用新增使用者時，無法使用鍵盤Tab鍵或方向鍵向前或向後移動 `Add user` 下拉式方塊。 (ASSETS-17233)
* 熒幕助讀程式無法正確傳達工作流程步驟的資訊(ASSETS-17285)。
* 當您導覽至 `Saved Searches` 下拉式方塊中，名稱和角色均沒有任何指派的標籤。 (ASSETS-17329)
* 當您導覽時 `Collection` 並暫留在文字上 *成員*，文字不會顯示為已標示。 因此，熒幕助讀程式無法辨識標題文字，並將它讀為純文字。 (ASSETS-17245)
* 無法存取 `View Settings` 選項使用鍵盤的向下或向上捲動鍵。 (ASSETS-17257)
* 無法為使用搜尋篩選條件找到的多個選定資產觸發工作流程。 (ASSETS-7689)
* 當您從搜尋結果中選取資產（或多個資產）時，「建立關係」或「取消關係」選項不可見。 但此選項可供使用，否則會失敗。 (ASSETS-7679)
* 搜尋篩選器面板在登入後只會開啟一次，如果您退出搜尋頁面並重新執行搜尋，則不會開啟。 (ASSETS-7671)

<!-- REMOVED BY ENGINEERING FROM TOTAL RELEASE CANDIDATE LIST 
* When you select any file in a Collection and click `Download`, and then navigate to the email checkbox and expand it, regular text and email link is not recognizable due to background color. (ASSETS-17349) 
* When you navigate to `Smart Crop` option, the screen reader does not announce the expand or collapse state of the button. (ASSETS-17335)-->

## [!DNL Assets] - [!DNL Dynamic Media]{#dm-6517}

* 當Dynamic Media雲端設定已存在時，與Dynamic Media的連線已中斷。 (ASSETS-23057)
* 提高使用大量Dynamic Media影片瀏覽資料夾時的效能，解決無法在資料夾卡片檢視中載入的問題。 (ASSETS-23016)
* 預覽Token會從中移除 `error.log` 這可用來向安全測試伺服器要求安全內容。 (ASSETS-22685)
* PDF縮圖演算新增陰影。 升級Gibson lib 4.0.1680232194版，解決PDF縮圖轉譯問題。 (ASSETS-22585)
* Dynamic Media混合模式現在與New Relic Agent 8.0.1版(ASSETS-22578)相容。
* 在Experience Manager上預覽Dynamic Media檔案時，現在會考慮Experience ManagerACL （存取控制清單）。 (ASSETS-21628)
* 當使用者嘗試使用向下鍵或Tab鍵導覽時，熒幕朗讀程式未導覽至隱藏元素。 (ASSETS-5617)
* 「影像設定檔」使用者介面限製為使用相同名稱、相同維度或兩者的智慧型裁切。 (ASSETS-16997)
* 「影像設定檔上的智慧型裁切」使用者介面的預設寬度和高度現在設為50畫素。 (ASSETS-16997)

## [!DNL Commerce]{#commerce-6517}

* 已移動的標籤為垃圾收集，但仍由下的產品參照 `/var`. (CQ-4351337)

## [!DNL Forms]{#forms-6517}

>[!NOTE]
>
>中的修正 [!DNL Experience Manager] Forms會在排程一週後透過個別附加元件套件傳送 [!DNL Experience Manager] Service Pack發行日期。 在此情況下，附加元件套件將於2023年6月1日星期四發行。 此外，本節還新增了Forms修正和增強功能的清單。

## 整合{#integrations-6517}

* 將Adobe Target IMS設定轉換為舊版雲端設定中的使用者認證時， `connectedWhen` 屬性不會變更。 此問題會使所有呼叫看起來好像設定仍以IMS為基礎。 (CQ-4352810)
* 新增 `modifyProperties` 許可權： `fd-cloudservice` 用於Adobe Sign設定的系統使用者。 (FORMS-6164)
* 透過Experience Manager與Adobe Target整合，當您建立AB測試活動時，它不會將與其關聯的對象同步至Target。 (NPR-40085)

## Platform{#platform-6517}

* 在Experience ManagerTag Management使用者介面(/aem/tags/)中，名稱空間和標籤會以建立的順序顯示。 但是，當有許多名稱空間和標籤時，很難檢視和管理它們。 此問題是因為它們無法以任何其他方式排序。 (NPR-39620)
* 需要Google關閉版本更新，因為縮制js無法用於某些使用者端程式庫。 (NPR-40043)

## [!DNL Sites]{#sites-6517}

* LinkCheckerTransformer效能下降。 (SITES-11661)
* 頁面的語言副本未按預期更新。 (SITES-11191)
* 開啟非行銷活動頁面呼叫 `targeteditor.html` 不必要的。 移除 `targeteditor` 不需要時呼叫。 (SITES-12469)
* 無法為有註解的頁面建立即時副本。 (SITES-12154)
* Experience Manager6.5.16正在轉出頁面。 (SITES-12008)
* 記憶體不足；高記憶體回收活動是由於 `NotificationManagerImpl`. `NotificationManager` 套件升級至AEM 6.5。 (SITES-11440)
* 修正封鎖Service Pack 17的WCM IT測試。 (SITES-13089)
* 在servlet上擷取網站參考失敗。 (SITES-10901)

### [!DNL Sites]  — 管理員使用者介面{#sites-adminui-6517}

* 無法關閉縮圖影像選擇器的預覽視窗。 (SITES-10459)

### [!DNL Sites] - [!DNL Content Fragments]{#sites-contentfragments-6517}

* 用於連線至Polaris服務物件的設定（URL、認證、回呼等）。 (SITES-12149)
* 使用方式 `SemanticDataType.REFERENCE` 應該支援「Remote-Asset-IDs」。 (SITES-12127)
* 將Polaris資產選擇器整合至內容片段編輯器中。 (SITES-12125)
* 必須有http標頭才能存取中繼資料服務端點。 (SITES-13068)
* GraphQL 6.5的實作不與Cloud Service（主要）相同；已識別的問題已修正。 (SITES-13096)
* GraphQL分頁/排序和混合篩選應該可以在AEM 6.5/AMS上使用。 (SITES-9154)

### [!DNL Sites] - 核心元件{#sites-core-components-6517}

* 屬性 `cq-msm-lockable` Foundation頁面元件中的重新導向值錯誤。 (SITES-10904)
* 遠端資產選取器一律會重新導向至IMS中繼環境。 (SITES-13433)

### [!DNL Sites] - [!DNL Experience Fragments]{#sites-experiencefragments-6517}

* 當您匯出至Adobe Target時，在體驗片段中選取外部化程式設定會導致傳送不正確的外部化URL。 (SITES-12402)
* 移除非包含性詞語；套用包含性詞語准則。 (SITES-11244)

### [!DNL Sites]  — 頁面編輯器{#sites-pageeditor-6517}

* Experience Manager內容尋找器側邊欄中的輪播集未顯示任何縮圖。 (SITES-8593)

## Sling{#sling-6517}

* Sling `ResourceMerger` 提供虛擬路徑時會佔用大量CPU，造成拒絕服務。 (NPR-40338)

## 翻譯專案{#translation-6517}

<!-- REMOVED BY ENGINEERING FROM TOTAL RELEASE CANDIDATE LIST * The `translationrules.xml` is sorted poorly when adding a rule to a property by way of the translation configuration user interface. (NPR-40431) -->
* 使用者未設定非必要欄位時，不會建立語言副本。 (NPR-40036)

## 使用者介面{#ui-6517}

* 「頁面屬性」中的「取消」按鈕為非作用中；它應該會將您帶到「網站管理員」使用者介面。 (NPR-40501)

<!-- ## WCM{#wcm-6517}

* TEXT -->

## 工作流程{#workflow-6517}

* 工作流程主控台變更。 (NPR-40502)
* `SegmentNotfound errors` 在生產製作執行個體的記錄中，由類別中未關閉的資源解析器所造成 `com.day.cq.workflow.impl.email.EMailNotificationServic`. (NPR-40187)
* 已關閉的未關閉 `ResourceResolver` 例外狀況已記錄。 (ASSETS-22495)
* Experience Manager作者當具有巨大的PSD/PDF時當機 `DocumentAncestors` 中繼資料屬性已上傳。 (ASSETS-22966)
* 類別中的工作階段洩漏 `InboxSharingCache` 替換為 `user-reader-service`. (CQ-4352513)
* 當「工作流程發起人參與者選擇器」步驟列出「參與者」步驟的使用者和群組時，會顯示不完整的使用者和群組清單。 當一個群組同時是另一個群組成員時，就會發生此問題。 (NPR-40055)
* 增強工作流程的清除功能。 (NPR-40459)

## 安裝 [!DNL Experience Manager] 6.5.17.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.17.0需要 [!DNL Experience Manager] 6.5.請參閱 [升級檔案](/help/sites-deploying/upgrade.md) 以取得詳細指示。 <!-- UPDATE FOR EACH NEW RELEASE -->
* Service Pack下載專案可在Adobe取得 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.17.0.zip).
* 在具有MongoDB和多個執行個體的部署上，安裝 [!DNL Experience Manager] 使用封裝管理器的其中一個Author執行個體上的6.5.17.0。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe不建議您移除或解除安裝 [!DNL Experience Manager] 6.5.17.0套件。 因此，在安裝套件之前，您應該建立 `crx-repository` 以防您必須將其回覆。 <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for AEM Forms, see [AEM Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### 在上安裝Service Pack [!DNL Experience Manager] 6.5{#install-service-pack}

1. 如果執行個體處於更新模式（執行個體是從舊版更新時），請在安裝前重新啟動執行個體。 如果執行個體的目前運作時間很高，Adobe建議重新啟動。

1. 安裝之前，請先拍攝快照或進行全新備份 [!DNL Experience Manager] 執行個體。

1. 下載Service Pack，從 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.17.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. 開啟封裝管理員，然後選取 **[!UICONTROL 上傳套裝]** 以上傳套件。 若要瞭解更多，請參閱 [封裝管理員](/help/sites-administering/package-manager.md).

1. 選取套件，然後選取 **[!UICONTROL 安裝]**.

1. 若要更新S3聯結器，請在安裝Service Pack後停止執行個體，以安裝資料夾中提供的新二進位檔案取代現有的聯結器，然後重新啟動執行個體。 另請參閱 [Amazon S3資料存放區](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>安裝Service Pack期間，套件管理員UI上的對話方塊有時會結束。 Adobe建議您在存取部署之前，先等待錯誤記錄穩定下來。 等待與更新程式套件組合解除安裝相關的特定記錄，再確認安裝成功。 此問題通常發生於 [!DNL Safari] 瀏覽器，但可能間歇性地在任何瀏覽器上發生。

**自動安裝**

您可以使用兩種方法自動安裝 [!DNL Experience Manager] 6.5.17.0。<!-- UPDATE FOR EACH NEW RELEASE -->

* 將套件置於 `../crx-quickstart/install` 資料夾（當伺服器線上上可用時）。 套件會自動安裝。
* 使用 [套件管理器的HTTP API](/help/sites-administering/package-manager.md#package-share). 使用 `cmd=install&recursive=true` 以便安裝巢狀套件。

>[!NOTE]
>
>Experience Manager6.5.17.0不支援Bootstrap安裝。 <!-- UPDATE FOR EACH NEW RELEASE -->

**驗證安裝**

若要瞭解經過認證可搭配此版本使用的平台，請參閱 [技術需求](/help/sites-deploying/technical-requirements.md).

1. 產品資訊頁(`/system/console/productinfo`)顯示更新的版本字串 `Adobe Experience Manager (6.5.17.0)` 在 [!UICONTROL 已安裝產品]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. 所有OSGi套件組合都可以 **[!UICONTROL 作用中]** 或 **[!UICONTROL 片段]** 在OSGi主控台中(使用Web主控台： `/system/console/bundles`)。

1. OSGi套件 `org.apache.jackrabbit.oak-core` 是1.22.15版或更新版本(使用Web主控台： `/system/console/bundles`)。 <!-- NPR-40398 for 6.5.17.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### 安裝Service Pack for [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

如需在AEM Forms上安裝Service Pack的說明，請參閱 [AEM Forms Service Pack安裝指示](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

### 安裝適用於Experience Manager內容片段的GraphQL索引套件{#install-aem-graphql-index-add-on-package}

使用GraphQL的客戶必須安裝 [具有GraphQL索引套件1.1.1的AEM內容片段](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

如此一來，您就可以根據實際使用的功能，新增所需的索引定義。

若未安裝此套件，可能會導致GraphQL查詢緩慢或失敗。

>[!NOTE]
>
>每個執行個體僅安裝此套件一次；不需要隨每個Service Pack重新安裝此套件。

### UberJar{#uber-jar}

The UberJar for [!DNL Experience Manager] 6.5.17.0可在以下網址取得： [Maven中央存放庫](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.17/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

若要在Maven專案中使用UberJar，請參閱 [如何使用UberJar](/help/sites-developing/ht-projects-maven.md) 並在您的專案POM中包含下列相依性： <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.17</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar和其他相關成品可在Maven中央存放庫上使用，而不是Adobe公共Maven存放庫(`repo.adobe.com`)。 主要UberJar檔案已重新命名為 `uber-jar-<version>.jar`. 因此，沒有 `classifier`，搭配 `apis` 作為值，針對 `dependency` 標籤之間。

## 過時的功能{#removed-deprecated-features}

底下列出標示為過時的功能 [!DNL Experience Manager] 6.5.7.0。功能最初會標示為過時，之後會在未來版本中移除。 提供替代選項。

檢閱是否在部署中使用功能或功能。 此外，計畫變更實作以使用替代選項。

| 區域 | 功能 | 替代方案 |
|---|---|---|
| 整合 | 畫面 **[!UICONTROL AEM Cloud Services選擇加入]** 已過時，因為 [!DNL Experience Manager] 和 [!DNL Adobe Target] 整合更新於 [!DNL Experience Manager] 6.5.整合支援Adobe Target Standard API。 API透過Adobe IMS和以下方式使用驗證 [!DNL Adobe I/O Runtime]. 它可支援Adobe Launch在樂器領域日益增加的作用 [!DNL Experience Manager] 頁面進行分析和個人化時，選擇加入精靈在功能上並不相關。 | 設定系統連線、Adobe IMS驗證和 [!DNL Adobe I/O Runtime] 透過個別 [!DNL Experience Manager] 雲端服務。 |
| 連接器 | Microsoft®SharePoint 2010和Microsoft®SharePoint 2013的AdobeJCR聯結器已過時 [!DNL Experience Manager] 6.5. | N/A |

## 已知問題{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->
<!-- REMOVED AS PER CQDOC-20022, JANUARY 23, 2023 * If you install [!DNL Experience Manager] 6.5 Service Pack 10 or a previous service pack on [!DNL Experience Manager] 6.5, the runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) is deleted.
To retrieve your runtime copy, Adobe recommends to synchronize the design-time copy of the custom workflow model with its runtime copy using the HTTP API:
`<designModelPath>/jcr:content.generate.json`. -->

* 將可能已使用您內容模型的自訂API名稱的GraphQL查詢更新為改用內容模型的預設名稱。

* GraphQL查詢可使用 `damAssetLucene` 索引而非 `fragments` 索引。 此動作可能會導致GraphQL查詢失敗或需要很長時間才能執行。

   若要修正問題， `damAssetLucene` 必須設定為包含下列兩個屬性：

   * `contentFragment`
   * `model`

   在索引定義變更後，需要重新索引(`reindex` = `true`)。

   執行這些步驟後，GraphQL查詢的執行速度應該會更快。

* 作為 [!DNL Microsoft® Windows Server 2019] 不支援 [!DNL MySQL 5.7] 和 [!DNL JBoss® EAP 7.1]， [!DNL Microsoft® Windows Server 2019] 不支援以下專案的turnkey安裝 [!DNL AEM Forms 6.5.10.0].

* 如果您升級您的 [!DNL Experience Manager] 從6.5.0 - 6.5.4執行個體到Java™ 11上的最新Service Pack，您會看到 `RRD4JReporter` 中的例外狀況 `error.log` 檔案。 若要停止例外，請重新啟動您的執行個體 [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* 使用者可以在下列位置重新命名階層中的資料夾： [!DNL Assets] 並將巢狀資料夾發佈至 [!DNL Brand Portal]. 但是，資料夾的標題不會更新於 [!DNL Brand Portal] 直到重新發佈根資料夾為止。

* 當使用者選擇在最適化表單中首次設定欄位時，儲存設定的選項未顯示在屬性瀏覽器中。 選擇在相同編輯器中設定最適化表單的其他欄位即可解決問題。

* 安裝期間可能會顯示下列錯誤和警告訊息 [!DNL Experience Manager] 6.5.x.x：
   * 「當在中設定Adobe Target整合時 [!DNL Experience Manager] 使用Target Standard API （IMS驗證），然後將體驗片段匯出至Target會導致建立錯誤的選件型別。 Target不會使用「體驗片段」/來源「Adobe Experience Manager」型別，而是會建立多個具有「HTML」/來源「Adobe Target Classic」型別的選件。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在granite/operations/maintenance找不到維護時段。
   * 使用SUM、MAX和MIN等彙總函式時，Adaptive Form伺服器端驗證會失敗(CQ-4274424)。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`  — 在granite/operations/maintenance找不到維護時段。
   * 透過Shoppable Banner檢視器預覽資產時，Dynamic Media互動影像中的熱點不可見。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` ：等待登入變更完成解除登入逾時。

* 嘗試移動、刪除或發佈內容片段、網站或頁面時，由於背景查詢失敗，擷取內容片段參考時會發生問題。 也就是說，功能無法運作。
若要確保作業正確，您必須將下列屬性新增至索引定義節點 `/oak:index/damAssetLucene` （不需要重新索引）：

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

* 在AEM Forms中，POP3通訊協定不適用於Microsoft® Office 365的電子郵件端點。
* 在JBoss® 7.1.4平台上，當使用者安裝AEM 6.5.16.0 Service Pack時， `adobe-livecycle-jboss.ear` 部署失敗。

## 包含的OSGi套件組合和內容套件{#osgi-bundles-and-content-packages-included}

下列文字檔案列出中包含的OSGi套件組合和內容套件 [!DNL Experience Manager] 6.5.17.0： <!-- UPDATE FOR EACH NEW RELEASE -->

* [Experience Manager6.5.17.0中包含的OSGi套件組合清單](/help/release-notes/assets/65170_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager6.5.17.0中包含的內容套件清單](/help/release-notes/assets/65170_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 受限制的網站{#restricted-sites}

這些網站僅供客戶使用。 如果您是客戶且需要存取權，請聯絡您的Adobe客戶經理。

* [產品下載網址為licensing.adobe.com](https://licensing.adobe.com/)
* [聯絡Adobe客戶支援](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 產品頁面](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5檔案](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hant)
>* [訂閱 Adobe 優先產品更新](https://www.adobe.com/tw/subscription/priority-product-update.html)

