---
title: 版本注意事項 [!DNL Adobe Experience Manager] 6.5
description: 尋找版本資訊、新增功能、安裝作法和詳細的變更清單 [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
source-git-commit: f00d2c88ba6727f8f8597fefeb467b612b23dea3
workflow-type: tm+mt
source-wordcount: '3524'
ht-degree: 2%

---

# [!DNL Adobe Experience Manager] 6.5最新Service Pack發行說明 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, November 30, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## 發行資訊 {#release-information}

| 產品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.20.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 類型 | Service Pack發行 |
| 日期 | 2024年2月22日星期四 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 下載 URL | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## 包含的內容 [!DNL Experience Manager] 6.5.20.0 {#what-is-included-in-aem-6520}

[!DNL Experience Manager] 6.5.20.0包括自2019年4月6.5首次發行以來所推出的新功能、客戶要求的重要增強功能、錯誤修正，以及效能、穩定性和安全性改善專案。 [安裝此Service Pack](#install) 於 [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

## 主要功能和增強功能

<!-- * _6.5.20.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

此版本中的部分主要功能和增強功能包括：

* Dynamic Media現在支援Apple iOS/iPadOS的無損HEIC影像格式。 另請參閱 [fmt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html?lang=en) Dynamic Media影像提供與轉譯API中。

* 多站台管理員(MSM)現在支援體驗片段結構，包括資料夾和子資料夾，以便有效地將體驗片段大量轉出到即時副本。

### [!DNL Forms]

* **JEE版AEM Forms中的Transaction Reporting**：我們已在JEE上為AEM Forms引入交易報告功能，以便全面記錄檔案交易，例如轉換、轉譯和提交。 此增強功能可提高效率，並有助於更好地儲存記錄。 此功能預設為停用。 您可以從管理員UI啟用它。
* **支援ECDSA的增強安全性**：AEM Forms現在對JEE和OSGi棧疊的橢圓曲線數位簽名演演算法(ECDSA)提供完善支援。 使用者現在可以透過增強的安全性來簽署、認證及驗證PDF檔案。 支援的EC曲線演演算法包括：
   * 使用SHA256摘要演演算法的ECDSA橢圓曲線P256
   * 使用SHA384摘要演演算法的ECDSA橢圓曲線P384
   * 使用SHA512摘要演演算法的ECDSA橢圓曲線P512
* **與Forms Designer適用的Windows 11緊密相容**：AEM Forms Designer現在支援Windows 11，確保順利安裝和操作。 使用者可以放心地升級至Windows 11，不必重新安裝Forms Designer，也不用擔心相容性問題，確保工作流程不會中斷。
* **AEM Forms Designer中的自訂「Caption」角色可增強協助工具**： AEM Forms Designer現在包含名為「Caption」的自訂協助工具角色，讓使用者能夠使用個人化的字幕元素建立XDP。 此功能可讓使用者將自訂註解整合到其檔案設計中，藉此增強協助工具，進而改善包容性和使用者體驗。

<!-- ### [!DNL Forms]

* text -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## 已修正Service Pack 20中的問題 {#fixed-issues}

### [!DNL Sites]{#sites-6520}

<!--#### Accessibility{#sites-accessibility-6520}

* text -->

#### 管理員使用者介面{#sites-adminui-6520}

* 此 `Workflow Title` 欄位標有 `*` 視需要，但沒有驗證。 (SITES-16491)

<!--#### Classic UI{#sites-classicui-6520}

* text -->

#### [!DNL Content Fragments]{#sites-contentfragments-6520}

* 升級到AEM 6.5.18或AEM 6.5.19後，不再支援巢狀設定資料夾，並且內容片段模型資料夾不再可見。 (SITES-18110)
* 某些子資料夾無法從繼承的內容片段模型中挑選。 它必須支援資料夾，但不具備 `jcr:content` 屬性，即使透過使用者介面建立的DAM資料夾有這類節點。 (SITES-17943)

#### [!DNL Content Fragments] - GRAPHQL API {#sites-graphql-api-6520}

<!-- REMOVED AS PER EMAIL FROM SAMEER DHAWAN FEBRUARY 19, 2024 * When upgrading AEM from 6.5.19.0 to 6.5.20.0, the path `/libs/cq/graphql/sites/graphiql` was getting deleted. (SITES-19530) CRITICAL -->
* 執行GraphQL查詢時 [篩選結果](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#filtering) 使用選擇性變數(若特定值為 **非** 若為選用變數，則篩選器評估中會忽略變數。 (SITES-17051)

<!--#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6520}

* text -->

#### [!DNL Content Fragments] - REST API{#sites-restapi-6520}

* 透過升級 `org.json` 程式庫中，小數點的還原序列化方式有所變更。 之前，它們「預設」轉換為雙面，現在則轉換為大十進位。 相反地，透過REST API儲存的中繼資料屬性值應該從BigDecimal轉換為Double。 (SITES-16857)

#### 核心後端{#sites-core-backend-6520}

* 使用內容片段的快速發佈時，它會繼續載入且不會發佈。 也就是說，從AEM 6.5.7升級至AEM 6.5.17的Service Pack後，快速發佈無法用於內容片段。當使用者嘗試Managed發佈時，就成功了。 但是，當他們嘗試快速發佈時，它並未發佈。 具體來說， `com.day.cq.wcm.core.impl.reference.ActivationReferenceSearchBuilder` 導致系統崩潰。 (SITES-17311)
* 無法使用Jackson匯出工具序列化內容片段：當頁面中有參照的內容片段（使用Jackson匯出工具程式碼）和任何標籤新增到內容片段時，頁面載入會中斷。 (SITES-18096)

#### 核心元件{#sites-core-components-6520}

* 在CIF上安裝AEM核心元件套件導致 `:type` 要變更的現有元件的值。 此變更表示這些變數不再於已新增至的頁面上呈現。 (SITES-17601)

#### Campaign整合{#sites-campaign-integration-6520}

* AEM使用允許清單(也稱為 `whitelist` — 由於弱點報告。 允許清單導致客戶無法使用所需功能。 (SITES-16822)

#### 體驗片段{#sites-experiencefragments-6520}

* 體驗片段的MSM現在支援大量轉出至體驗片段的內容結構，包括資料夾和子資料夾。 (SITES-16004)

<!--#### Foundation Components (Legacy){#sites-foundation-components-legacy-6520}

* text

#### Launches{#sites-launches-6520}

* text -->

#### MSM — 即時副本{#sites-msm-live-copies-6520}

* 一個&quot;`Is not modifiable`轉出元件時擲回「例外狀況。 具體而言， `org.apache.sling.servlets.post.impl.operations.ModifyOperation` 在回應處理期間發生例外狀況。 (SITES-18809)
* 無法將變更轉出至體驗片段的特定即時副本。 (SITES-17930)
* 當使用者將註解新增到Blueprint頁面上的元件，然後轉出時，即時副本上的註解計數顯示不正確。 (SITES-17099)
* 在觸控式圖形使用者介面中，從父頁面到子頁面的「MSM轉出」按鈕會損毀；選取時，會顯示下列錯誤： `Uncaught TypeError: _g.shared is undefined`. (SITES-16991)

#### 頁面編輯器{#sites-pageeditor-6520}

* Forms主題編輯器預覽已中斷。 選取「預覽」時，只會顯示載入圖示。 (SITES-17164)

### [!DNL Assets]{#assets-6520}

* 無法驗證中繼資料編輯器協助程式中規則型欄位，且顯示錯誤訊息「缺少必填欄位」。 (ASSETS-31396)
* 將PDF移至另一個位置後， **[!UICONTROL 檢視頁面]** 選項會消失。 (ASSETS-30538)
* 無法選取具有讀取許可權的影像。 (ASSETS-32199)
* 無法在檢視設定中變更卡片大小。 (ASSETS-31667)
* 上傳.oft檔案型別時上傳失敗。 (ASSETS-30109)
* 當您嘗試新增自訂中繼資料欄位作為報告的其他欄時，未選取核取方塊。 (ASSETS-31671)
* 資產移動作業在Experience Manager Service Pack 16中無法正常運作。 (ASSETS-30598)

#### [!DNL Dynamic Media]{#assets-dm-6520}

* 將資產上傳至AEM時， `Update_asset` 工作流程已觸發。 不過，工作流程永遠不會完成。 工作流程最多只會在產品上傳步驟前完成。 下一個步驟是Scene7批次上傳，但該程式無法提取至AEM。 (ASSETS-30443)
* 需要更好的方式在Dynamic Media元件中妥善處理非Dynamic Media影片。 此問題提供例外具現化 `dynamicmedia_sly.js`. (ASSETS-31301)
* 預覽適用於所有資產、最適化視訊集和視訊。 但是，它會擲回403錯誤 `.m3u8` 檔案（順便說一下，這些檔案仍可透過公用連結運作）。 (ASSETS-31882)
* 此 `scene7SmartCropProcessingStatus` 已更正狀態。 智慧型裁切視訊中繼資料即使成功也可用來顯示失敗。 (ASSETS-31255)

### [!DNL Forms]{#forms-6520}

<!--Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the AEM 6.5.20.0 Forms add-on package release is scheduled for Thursday, February 29, 2024. A list of Forms fixes and enhancements is added to this section post the release.-->

#### [!DNL Adaptive Forms]

* 當使用者嘗試將AEM Forms整合到具有AEM已發佈URL的郵寄平台時，AEM Forms未新增 `method=post` 轉譯頁面時。 即使發生此問題 `POST` 在具有URL的提交動作中設定。 這會導致郵寄平台無法將此識別為表單。 (FORMS-12614)
* 當使用者在AEM Form Service Pack 6.5.18.0上選取具有顯示模式的日期欄位時，使用者無法使用鍵盤選取目前日期。 (FORMS-12736)
* 在AEM Forms Service Pack 6.5.17.0和Service Pack 6.5.18.0上，當使用者在行事曆Widget中的月份之間切換時，日期選擇器元件會顯示額外的列。 (FORMS-11869)
* 當使用者在iOS裝置上的附件元件中使用「拍攝影片」按一下影像時，所有影像都會新增到具有相同名稱的資料夾中。 (FORMS-12224)
* 當使用者更新單選按鈕群組中的現有選項時，會發佈不正確的翻譯值。 (FORMS-12575)
* 當使用者在Android™裝置上將字元新增到最適化表單時，使用者在Android™裝置上聚焦時可以在文字欄位中輸入超過定義的最大字元數。 但是，當使用者選取HTML5輸入型別時，它就會運作。 (FORMS-12748)
* 由於相符的標籤Arial® labelledby和Arial® label，熒幕助讀程式無法區分這兩者。 為了解決問題 — 表單欄位的「aria-labelledby」標籤已取代為「aria-describedby」。 (FORMS-12436)
* 當作者使用「最適化Forms — 內嵌(v2)」元件在其網站頁面中嵌入最適化表單，且內嵌表單包含驗證碼元件時（驗證碼服務 — > reCAPTCHA，設定 — > reCAPTCHA-v2），當使用者嘗試在作者執行個體上使用「以發佈的形式檢視」來檢視網站頁面時，網站頁面未轉譯。 下列錯誤顯示為(FORMS-11859)：
  `Failed to construct 'URL': Invalid base URL at Object.renderRecaptcha`

* 當使用者嘗試使用日期選擇器元件選擇日期時，值未更新並顯示NULL。 (FORMS-12742， FORMS-12736)

* 當使用者升級至AEM Form Service Pack 6.5.19.0，在將新語言更新到現有字典後，它沒有與「guideContainer」列合併以將地區設定新增到表單。 (FORMS-12947)

* 在AEM Forms Service Pack 6.5.19.0上，在Java™ 11上叫用的Web服務操作會失敗並出現錯誤(FORMS-12329)：
  `java.lang.NoClassDefFoundError message:sun/misc/BASE64Decoder`

* 當使用者在AEM Forms Service Pack 6.5.18.0上呼叫「EmailService」的「接收」作業時，會發生例外狀況(FORMS-12050)：
  `java.util.ServiceConfigurationError: javax.mail.Provider: Provider com.sun.mail.imap.IMAPProvider not a subtype`

* 在AEM Forms Service Pack 6.5.18.0上啟用FIPS模式時，在預設DOM下建立使用者會失敗並出現錯誤(FORMS-11857)：
  `com.adobe.idp.cx.a: error seeding random number generator`

* 當使用者在ADMINUI中選取路徑下的字型時 `Home>Services>PDF Generator>Adobe PDF Settings`，則不會加以選取。 此外，在標準或個人化設定檔中，可用的字型清單方塊是空的。 因此，無法個人化的 **永遠內嵌** 或 **永不內嵌**. 使用者無法使用PDF Generator設定其PDF的字型。 記錄檔不會顯示任何相關的錯誤訊息。 (FORMS-12095)

* 在AEM Forms Service Pack 6.5.18.0上，使用者無法建立安全性設定，不會顯示錯誤或伺服器記錄，但畫面上會顯示快顯錯誤訊息。 (FORMS-12212)

* 當AEM Forms Service Pack 6.5.18.0的使用者在JEE工作流程提交最適化表單時，最適化表單中的附件未傳送到JEE程式，導致應用程式失敗。 (FORMS-12232， FORMS-12228)

* 當使用者將PDF轉換為PDF/A-2b或PDF/A-3B時，轉換失敗，錯誤顯示為：(FORMS-12790)

  ```
  OCCD contains Order key that does not reference all layers.
  -> Optional content configuration dictionary has no Name entry.
  -> Font not embedded (and text rendering mode not 3).
  obj(65, 0)
  Page: 1
  -> Font not embedded (and text rendering mode not 3).
  obj(67, 0)
  Page: 1
  -> PDF/A entry missing. 
  -> PDF/A entry missing.
  ```

* 在AEM Forms 6.5.18.0上，發佈調適型表單時，其所有相依性（包括原則）都會重新發佈，即使未進行任何修改亦然。 (FORMS-10454)

* 當使用者在具有JBoss® Turnkey設定的AEM Forms 6.5.19.1上執行設定管理員時選取「Microsoft SharePoint」時，LiveCycleJBoss® EAR安裝會失敗，並顯示以下錯誤：(FORMS-12463)

  ` Caused by: org.jboss.as.server.deployment.DeploymentUnitProcessingException: WFLYEE0031: Unable to process modules in application.xml for EAR ["/C:/AEM/jboss/bin/content/ adobe-livecycle-jboss.ear "], module file adobe-connectorformssharepoint-config-ejb.jar not found.`

#### [!DNL Forms Designer] {#forms-designer-6520}


* 當使用者升級到AEM Forms Service Pack 6.5.18.0時，由於缺少例外狀況處理，透過已啟用標籤PDF選項的輸出服務傳遞的XDP失敗。 (LC-3921757)

* 當使用者使用AEM Forms Designer產生PDF時，在協助工具樹狀結構中會標籤標題層級與圖形元素，例如矩形方塊。 (LC-3921687)

* 透過Workbench安裝的AEM Forms Designer版本資訊在 `Control Panel/Programs/Programs and Features`. (LC-3921976)

<!--* When a user creates an XDP on AEM Forms Designer, the user is not able to add the custom Caption Tag. (LC-3921246)-->

* 當使用者在AEM Forms Designer上建立XDP時，在PDF輸出上，Button Form標籤未巢狀內嵌在父段落標籤(p-tag)中。 (LC-3921719)

* 當使用者在AEM Forms Designer上建立XDP時，當使用者導覽表單標籤時，也會在PDF輸出上標籤背景物件。 (LC-3921687)

### Foundation {#foundation-6520}

#### 社群 {#communities-6520}

* 使用者同步診斷在成功設定使用者同步後失敗。 (NPR-41693)

<!-- #### Content distribution{#foundation-content-distribution-6520}

* text -->

#### 整合{#integrations-6520}

* 從AEM 6.5中移除AdobeSearch&amp;Promote的所有程式碼和相依性。 (NPR-40856)

#### 本地化{#localization-6520}

* Aria標籤「關閉」未在中本地化 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**，選取資料夾，然後在工具列上選取 **[!UICONTROL 屬性]** > **[!UICONTROL 許可權]** 標籤>成員名稱。 (NPR-41705)
* 「 」的工具提示已截斷 **[!UICONTROL 金鑰庫密碼]** ENG、FRA、KOR、DEU和PTB語言環境的「SSL設定」頁面上的欄位。 (NPR-41367)

#### Platform{#foundation-platform-6520}

* 因/api servlet未在href json中傳回正確的配置而導致將Campaign與AEM整合的問題。 原因在於AEM未收到X-Forward-Proto標頭，該標頭會強制要求以HTTP配置而非HTTPS回應。 因此，應新增根據OSGI設定切換配置選擇的功能。 (GRANITE-48454)

#### Sling{#foundation-sling-6520}

* 此 `org.apache.sling.resourceMerger` bundle 1.4.2從AEM 6.5、Service Pack 17及更新版本擲回例外狀況。 Service Pack 20應包含Sling resource merger 1.4.4。 (NPR-41630)

#### 轉換{#foundation-translation-6520}

* 部署AEM 6.5 Service Pack 18後，翻譯規則編輯器中的篩選器索引標籤發生問題。 選取「前後關聯」時，按一下「編輯>儲存」，下次您開啟相同的「前後關聯」時，會出現一個雙引號作為HTML字元。 基本上，翻譯規則無法正確儲存。 (NPR-41624)
* 與內容片段翻譯相關的問題，其中翻譯的字串從翻譯提供者傳回AEM，但卡在 `/content/projects` 層級，且不會更新內容片段。 (NPR-41516)
* 建立語言副本時會顯示錯誤訊息。 其發生於具有使用內容片段模型的頁面屬性中所參考的內容片段的頁面上。 (NPR-41441)
* 在語言複製期間，體驗片段中的連結未調整為正確的語言。 體驗片段會指向主要地區設定。 (NPR-41343)

#### 使用者介面{#foundation-ui-6520}

* 升級至AEM 6.5 Service Pack 18後出現主控台錯誤。 錯誤位於 `coralUI3.js` 檔案，當您在AEM中選取任何下拉式清單時，就會發生檔案。 更具體地說，這會發生在使用 `onOverlayToggle` 事件。 錯誤 `Uncaught TypeError: Cannot read properties of null (reading 'innerText')` 隨即顯示。 (NPR-41467)
* 在AEM中 **[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL 標籤]** > **[!UICONTROL 建立]** > **[!UICONTROL 建立標籤]**，在中輸入非拉丁字元 **標題** 欄位會導致 **名稱** 僅以連字型大小字元( `-` )。 (NPR-41623)
* 中的版權年度不正確 `About Adobe Experience Manager` 對話方塊。 (NPR-41526)
* 有未翻譯的 **[!UICONTROL 設定檔屬性]** 字串。 發生在所有地區設定中。 (NPR-41365)

<!-- #### WCM{#wcm-6520}

* text

#### Workflow{#foundation-workflow-6520}

* text -->

## 安裝 [!DNL Experience Manager] 6.5.20.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.20.0需要 [!DNL Experience Manager] 6.5.請參閱 [升級檔案](/help/sites-deploying/upgrade.md) 以取得詳細指示。 <!-- UPDATE FOR EACH NEW RELEASE -->
* 您可在Adobe上取得Service Pack下載 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip).
* 在具有MongoDB和多個執行個體的部署上，安裝 [!DNL Experience Manager] 使用封裝管理程式的其中一個Author執行個體上的6.5.20.0 。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe不建議您移除或解除安裝 [!DNL Experience Manager] 6.5.20.0套件。 因此，在安裝套件之前，您應該建立 `crx-repository` 以防您必須將其回覆。 <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### 在上安裝Service Pack [!DNL Experience Manager] 6.5{#install-service-pack}

1. 如果執行個體處於更新模式（從舊版更新執行個體時），請在安裝前重新啟動執行個體。 如果執行個體的目前運作時間很高，Adobe建議重新啟動。

1. 安裝之前，請拍攝快照或進行全新備份 [!DNL Experience Manager] 執行個體。

1. 下載Service Pack，從 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. 開啟封裝管理員，然後選取 **[!UICONTROL 上傳套裝]** 以上傳套件。 若要瞭解更多，請參閱 [封裝管理員](/help/sites-administering/package-manager.md).

1. 選取封裝，然後選取 **[!UICONTROL 安裝]**.

1. 若要更新S3聯結器，請在安裝Service Pack後停止執行個體，將現有聯結器取代為安裝資料夾中提供的新二進位檔案，然後重新啟動執行個體。 另請參閱 [Amazon S3資料存放區](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>在安裝Service Pack期間，套件管理員UI上的對話方塊有時會退出。 Adobe建議您先等待錯誤記錄穩定下來，再存取部署。 等待與更新程式套件組合解除安裝相關的特定記錄，再確認安裝成功。 此問題通常發生在 [!DNL Safari] 瀏覽器，但可能間歇性地在任何瀏覽器上發生。

**自動安裝**

您可以使用兩種不同的方法來自動安裝 [!DNL Experience Manager] 6.5.20.0。<!-- UPDATE FOR EACH NEW RELEASE -->

* 將套件置於 `../crx-quickstart/install` 資料夾（當伺服器線上上可用時）。 套件會自動安裝。
* 使用 [來自封裝管理員的HTTP API](/help/sites-administering/package-manager.md#package-share). 使用 `cmd=install&recursive=true` 以便安裝巢狀套件。

>[!NOTE]
>
>Experience Manager6.5.20.0不支援Bootstrap安裝。 <!-- UPDATE FOR EACH NEW RELEASE -->

**驗證安裝**

若要瞭解經過認證可搭配此版本使用的平台，請參閱 [技術需求](/help/sites-deploying/technical-requirements.md).

1. 產品資訊頁(`/system/console/productinfo`)顯示更新的版本字串 `Adobe Experience Manager (6.5.20.0)` 在 [!UICONTROL 已安裝的產品]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. 所有OSGi套件組合都是 **[!UICONTROL 作用中]** 或 **[!UICONTROL 片段]** 在OSGi主控台中(使用Web主控台： `/system/console/bundles`)。

1. OSGi套件 `org.apache.jackrabbit.oak-core` 為1.22.18版或更新版本(使用Web主控台： `/system/console/bundles`)。 <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### 安裝Service Pack for [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

如需在Experience Manager Forms上安裝Service Pack的說明，請參閱 [Experience Manager Forms Service Pack安裝指示](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>調適型表單功能 (適用於 [AEM 6.5 QuickStart](https://experienceleague.adobe.com/docs/experience-manager-65/content/implementing/deploying/deploying/deploy.html)) 僅用於探索和評估目的。若要供生產使用，必須獲得 AEM Forms 的有效許可；調適型表單的功能需要適當許可才可使用。

### 安裝Experience Manager內容片段的GraphQL索引套件{#install-aem-graphql-index-add-on-package}

使用GraphQL的客戶必須安裝 [使用GraphQL索引套件1.1.1Experience Manager內容片段](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

如此一來，您就可以根據使用者實際使用的功能，新增必要的索引定義。

無法安裝此套件可能會導致GraphQL查詢變慢或失敗。

>[!NOTE]
>
>每個執行個體僅安裝此套件一次；不需要隨每個Service Pack重新安裝。

### UberJar{#uber-jar}

The UberJar for [!DNL Experience Manager] 6.5.20.0可在以下網址取得： [Maven中央存放庫](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.20/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

若要在Maven專案中使用UberJar，請參閱 [如何使用UberJar](/help/sites-developing/ht-projects-maven.md) 並在專案POM中加入下列相依性： <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.20</version>
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

* 嘗試移動、刪除或發佈內容片段、網站或頁面時，在擷取內容片段參考時出現問題，因為背景查詢失敗。 也就是說，功能無法運作。
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
   * `com.adobe.granite.maintenance.impl.TaskScheduler`  — 在granite/operations/maintenance找不到維護時段。
   * 透過Shoppable Banner檢視器預覽資產時，不會顯示Dynamic Media互動影像中的熱點。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` ：等待登入變更完成解除登入逾時。

* 從AEM 6.5.15開始，Rhino JavaScript Engine由 ```org.apache.servicemix.bundles.rhino``` 捆綁有新的提升行為。 使用嚴格模式的指令碼(```use strict;```)必須正確宣告其變數，否則不會執行，而會擲回執行階段錯誤。


### AEM Forms的已知問題 {#known-issues-aem-forms-6520}

* 從AEM 6.5 Forms Service Pack 18 (6.5.18.0)或AEM 6.5 Forms Service Pack 19 (6.5.19.0)更新至AEM 6.5 Forms Service Pack 20 (6.5.20.0)後，使用者會遇到JSP編譯錯誤。 他們無法開啟或建立最適化表單，且其他AEM介面(如頁面編輯器、AEM Forms UI和AEM Workflow編輯器)發生錯誤。 出現類似以下內容的錯誤訊息：

  `Unable to compile class for JSP: An error occurred at line: 162 in the jsp file: /libs/granite/ui/components/coral/foundation/anchorbutton/anchorbutton.jsp The method transformLinkInUriIfExternal(String) is undefined for the type ComponentHelper`

  若要解決該問題：

   1. 下載作業系統的Hotfix：

      * [Microsoft Windows的Hotfix](/help/release-notes/assets/Hotfix-windows.zip)
      * [Linux適用的Hotfix](/help/release-notes/assets/Hotfix-Linux.zip)
      * [Apple macOS的Hotfix](/help/release-notes/assets/Hotfix-osx.zip)

   1. 透過上傳並安裝套件(.zip) [封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=en#accessing).

   1. 重新啟動AEM伺服器，並在重新啟動程式完成後驗證所有套裝的啟用狀態。 您可以透過存取以下專案來監視套裝的狀態： `https://server:host/system/console/bundles`. 繼續進行進一步的工作之前，請確定所有套件組合皆為作用中。

* 預填服務在互動式通訊中失敗，並出現Null指標例外狀況。 (CQDOC-21355)

<!--Known issues in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the AEM 6.5.20.0 Forms add-on package release is scheduled for Thursday, February 29, 2024. A list of known issues for forms is added to this section post the release.-->

<!--
#### Install the servlet fragment (AEM Service Pack 6.5.14.0 or earlier)

* If you are upgrading to AEM Service Pack 6.5.15.0 or higher, and your AEM instance is operating on Tomcat 8.5.88, it is mandatory that you install the servlet fragment *before* you proceed with the installation of Service Pack 6.5.15.0 or higher.
* It is mandatory that you install the servlet fragment for all application servers except those running on JBoss&reg; EAP 7.4.0.

**To install the servlet fragment:**

1. Download the servlet fragment from [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar).
1. Start the application server. 
1. Wait for the logs to stabilize and check the bundle state.
1. Open Web Console Bundles. The default URL is `http://[Server]:[Port]/system/console/bundles`.
1. Select **[!UICONTROL Install]** or **[!UICONTROL Update]**. 
1. Select the downloaded fragment 
`org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar` 
1. Select **[!UICONTROL Install]** or **[!UICONTROL Update]**. 
1. Wait for the application server to stabilize.
1. Stop the application server.

-->

## 包含的OSGi套件組合和內容套件{#osgi-bundles-and-content-packages-included}

下列文字檔案列出此套件中包含的OSGi套件組合和內容套件 [!DNL Experience Manager] 6.5 Service Pack版本：

* [Experience Manager6.5.20.0中包含的OSGi套件組合清單](/help/release-notes/assets/65200-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager6.5.20.0中包含的內容套件清單](/help/release-notes/assets/65200-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 受限制的網站{#restricted-sites}

這些網站僅供客戶使用。 如果您是客戶且需要存取權，請聯絡您的Adobe客戶經理。

* [產品下載網址為licensing.adobe.com](https://licensing.adobe.com/)
* [聯絡Adobe客戶支援](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 產品頁面](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5檔案](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hant)
>* [訂閱Adobe優先產品更新](https://www.adobe.com/tw/subscription/priority-product-update.html)
