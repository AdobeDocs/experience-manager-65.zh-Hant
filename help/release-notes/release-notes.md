---
title: 發行說明 [!DNL Adobe Experience Manager] 6.5
description: 「查找發行資訊、新增內容、安裝how-tos和詳細的更改清單 [!DNL Adobe Experience Manager] 6.5」
mini-toc-levels: 3
source-git-commit: 783edcdf0f96426008b6f824a7aa0aa0deb5c613
workflow-type: tm+mt
source-wordcount: '2623'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager] 6.5最新Service Pack發行說明 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession&cid=a915e87c-369a-480c-9daf-d13efc766798 -->

## 發行資訊 {#release-information}

| 產品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.14.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 類型 | Service Pack版本 |
| 日期 | 2022 年 8 月 25 日 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 下載 URL | [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.14.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## 包含的內容 [!DNL Experience Manager] 6.5.14.0 {#what-is-included-in-aem-6514}

[!DNL Experience Manager] 6.5.14.0包括自2019年4月6.5首次發佈以來發佈的新功能、客戶要求的關鍵增強功能、錯誤修復以及效能、穩定性和安全性改進。 [安裝此Service Pack](#install) 上 [!DNL Experience Manager] 6.5 <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_

* Added support for password reset for Dynamic Media Classic users within Experience Manager. (ASSETS-10298) -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets] {#assets-6514}

* 無法添加或查看PDF檔案的標籤。 (NPR-38452)
* 配置連接的資產、保存配置、重新開啟配置頁並test已保存的配置時，test連接將失敗。 (NPR-38507)
* 無法將具有數字用戶ID的用戶添加到集合。 (NPR-38538)
* Experience Manager無法處理安裝在作者實例上的FFmpeg。 (NPR-38568)
* PDF處理失敗 `NoClassDefFoundError` 錯誤消息。 (NPR-38741)
* 在為建立資產報表時，「自定義列」下的「添加」按鈕未正確顯示 `de_DE` 區域設定。 (ASSETS-10641)
* 當您將重複資產上載到數字資產管理儲存庫時，Experience Manager會檢測並提供刪除重複資產的選項，原始資產也會從儲存庫中刪除。 (ASSETS-10826)
* Experience Manager在多欄位中指定特殊字元時無法正確保存資料夾元資料。 (ASSETS-10721)
* 在按一下之前無法保存資產屬性 **[!UICONTROL 保存並關閉]** 兩次。 (ASSETS-12040)
* 螢幕閱讀器僅宣佈 `Relate` 按鈕 然而， `Relate` 按鈕還包含子菜單，可展開和折疊。 (ASSETS-6938)
* 必需的ARIA（可訪問的富Internet應用程式）屬性 `aria-expanded` 為 `role="combo box"` 缺少。 (ASSETS-6928)
* 在「卡」視圖中，在主檔案導航區域中，文本內容 **[!UICONTROL 排序依據]** 與其背景色相比，沒有至少4.5:1的對比度。 (ASSETS-6926)
* Experience Manager不識別 **[!UICONTROL 選擇工作流模型]** 建立工作流模型時，將下拉清單作為必填欄位。 (ASSETS-6871)

>[!NOTE]
>
>從2022年9月1日起，新的Experience Manager Assets現場客戶將無法獲得智慧內容服務。 對已啟用此功能的現有內部部署和Adobe托管服務客戶沒有影響。

### [!DNL Dynamic Media] {#dynamic-media-6514}

* 添加對Experience Manager內Dynamic Media Classic用戶密碼重置的支援。 (ASSETS-10298)
* 為具有透明背景的影像生成的智慧作物具有白色背景。 (ASSETS-13148)
* Dynamic Media不為EPS檔案生成縮略圖。 (ASSETS-10959)
* 由於缺少上載參數，無法將資產上載到Dynamic Media帳戶。 (ASSETS-13165)
* 允許將名稱大於127個字元的資產上載到Dynamic Media。 (ASSETS-9991)
* 在6.5.14.0Experience Manager上為Dynamic Media查看器啟用JavaScript ES6(ECMAScript 6)。 (NPR-38393)
* 在Dynamic Media配置選項 **[!UICONTROL 常規設定]** 和 **[!UICONTROL 發佈設定]** 非管理員用戶不應訪問。 (ASSETS-8628)
* Dynamic Media **[!UICONTROL 常規設定]** 頁未正確顯示已配置的上載參數。 (ASSETS-10245)
* Experience Manager用戶介面在建立/更新失敗時不顯示任何失敗消息。 (ASSETS-10264)
* 無法將保存的策略應用於可編輯模板的一個容器，以便您添加Dynamic Media元件。 (ASSETS-11044)
* 對作業句柄不正確的資產運行「Dynamic Media重新處理資產」工作流後，未將資產上載到Dynamic Media帳戶。 (ASSETS-12084、ASSETS-9877)
* 螢幕閱讀器用戶受 `title` 未為提供屬性 `<frame>` 和 `<iframe>` 的 **[!UICONTROL 要搜索的類型]** 對話框。 (ASSETS-5483)
* 在螢幕閱讀器中，相關和有意義 `alt=` 應為以下的多個影像提供值 **[!UICONTROL 資產]** 的子菜單。 (ASSETS-5644)
* 螢幕閱讀器未讀取 **[!UICONTROL 靜音]** 和 **[!UICONTROL 取消靜音]** 按鈕，查看視頻中使用Dynamic Media元件的內容。 (ASSETS-10169)

## 商務 {#commerce-6514}

* 未使用列標題對商品進行排序，並且正在使用 _遠程_ 排序模式；相反，應使用列標題對Commerce產品排序 _本地_ 排序模式。 (CQ-4343750、NPR-38498)

## [!DNL Forms] {#forms-6514}

>[!NOTE]
>
>* [!DNL Experience Manager Forms] 會在預定的 [!DNL Experience Manager] Service Pack 發行日期一週後發行附加元件的套件。在這種情況下，附加包將於2022年9月1日星期四發佈。 此外，本節還將添加Forms修復和增強的清單。


## Integrations {#integrations-6514}

* 啟用JavaScript ES6（ECMAScript6模式或更好）編譯支援，以縮小 `/libs/cq/analytics/widgets.js` 的下界。 (NPR-38433)
* 啟用JavaScript ES6（ESMAScript6模式或更好）編譯支援，以縮小 `/libs/cq/testandtarget/clientlibs/testandtarget/util.js` 的下界。 (NPR-38435)
* 內容越多 `/content/campaigns`，呼叫的時間越長 `targeteditor.html` (`/libs/cq/personalization/touch-ui/content/targeteditor.html`)。 (NPR-38663)

## 平台 {#platform-6514}

* 無法登錄到包管理器以部署更新。 (NPR-38646)
* 在資產標籤選取器用戶介面中，標籤按建立順序顯示。 但是，當標籤很多時，查看和管理標籤會很困難，因為無法對它們進行排序。 (CQ-4344279)
* 當用戶被管理員模擬或使用 **[!UICONTROL 模擬為]** 的子菜單。 (CQ-4345288)
* 在智慧集合中，使用已保存的搜索進行篩選時顯示所有資產。 (CQ-4345326)
* 顯示的選定資產計數不正確 **[!UICONTROL 添加到集合]** 何時 **[!UICONTROL 全選]** 的子菜單。 (CQ-4345424)
* 使用 **[!UICONTROL 模擬為]** 組或不存在的用戶的欄位。 (CQ-4346098)

## [!DNL Sites] {#sites-6514}

* 將Experience Manager從6.5.12.0升級到6.5.13.0時發生意外路徑刪除。 (NPR-38532)

### 協助工具 {#access-6514}

* 在Experience Manager Sites，當你把 **[!UICONTROL 切換顯示格式及調整顯示設定]** ，然後選擇 **[!UICONTROL 清單視圖]**，也請參見Wiki頁。 **[!UICONTROL 拖放]** 按鈕缺少可訪問的名稱。 (SITES-2863、NPR-38760)
* 螢幕閱讀器必須宣佈可訪問的名稱，如 `Show description for Archive` 或 `Show description for mini shopping cart`。 但是，當前可訪問名稱將宣佈為 `Info Circle button show description` 為 _全部_ 工具提示資訊按鈕。 (SITES-3104)
* 改進中沒有inlineEditing或dropTarget功能的元件的撤消 `cq:editConfig`。 (NPR-38361) <!-- version 2 (old) of the description above * When out of the box components that don't have inlineEditing or dropTarget feature in the _cq_editConfig file (navigation, breadcrumb, embed) are deleted > undeleted (by way of Undo), all configurations are lost and empty placeholder reappears. Component must be reconfigured from scratch. (NPR-38361) -->
* 「樣式系統」下拉清單可能位於頁面頂部，而不是元件的上下文中 — 用於使用 `cq:editConfig` 「afteredit:REFRESH_PAGE」。 (NPR-38384) <!-- version 2 (old) of description above* When selecting a style option on a component, the Styles box shifts to the upper left corner of the screen, rather than staying put below the style icon. Happens for components that have  cq:editConfig "afteredit: REFRESH_PAGE". (NPR-38384) -->
* 將文本元件添加到嵌套的佈局容器時未對齊。 (NPR-38193)
* 當元件沒有「樣式系統」配置時，將顯示一個空樣式頁籤。 當沒有配置時，該頁籤現在隱藏。 (NPR-38218) <!-- version 2 (old) of description above * Style tab is blank on components without styles/policies. (NPR-38218) -->
* 屬性 `useLegacyResponsiveBehaviour` 只有經過驗證才能工作。 (NPR-37996)
* 將jquery-ui升級為最新版本導致編輯器斷開。 (SITES-5647)

### [!DNL Content Fragments] {#sites-contentfragments-6514}

* 內容片段枚舉欄位驗證首次載入內容片段時發出。 (SITES-7140)
* 需要在內容片段編輯器的富文本編輯器中添加市場活動個性化欄位。 (NPR-38526)
* 在內容片段編輯器中建立或編輯新內容片段時，通過Dispatcher不保存內容片段模型。 此外，內容片段編輯器未關閉，瀏覽器日誌中顯示錯誤。 (NPR-38691)
* 持久查詢驗證錯誤。 (NPR-38523)
* 在「內容片段」對話框中，在 **[!UICONTROL 屬性]**，也請參見Wiki頁。 **[!UICONTROL 內容片段]** 欄位不會在選擇彈出窗口中保留保存的路徑。 (NPR-38632)
* 建立內容片段模型並添加下拉類型的枚舉欄位時，正確驗證 _`is required`_失敗。 (NPR-38237)

### 核心元件 {#sites-corecomponents-6514}

* 編輯時，新的「頁面電子郵件」元件不應強制您進入傳統用戶介面 `/etc`。 (NPR-38648)

### 頁面編輯器 {#sites-pageeditor-6514}

* 用戶無法將元件調整到所需列數。 (NPR-38688)

### 範本編輯器 {#sites-templateeditor-6514}

* 缺少 **[!UICONTROL 刪除]** 和 **[!UICONTROL 剪切]** 按鈕 `cq:actions` 屬性已自定義。 (NPR-38521)
* 如果元件包含另一個元件，則無法刪除模板結構中的元件，因為 **[!UICONTROL 刪除]** 菜單欄中缺少。 (NPR-38585)

## Sling {#sling-6514}

* 由於模組記憶體洩漏，生產上開啟的檔案數量有所增加 `DiscoveryLiteDescriptor` 在 `org.apache.sling.discovery.commons`，版本1.0.20。 (NPR-38288)
* 在Experience Manager中，從 **[!UICONTROL 操作]** > **[!UICONTROL 診斷]**，在選擇 **[!UICONTROL 下載狀態ZIP]** > **[!UICONTROL 下載]**。 (NPR-38514)

## 翻譯項目 {#translation-6514}

* 在父頁中作為引用添加的子頁的啟動未升級 `isDeep` 屬性設定為 `false`。 (NPR-38531)

## 使用者介面 {#ui-6514}

* 使用時 **[!UICONTROL 全選]** > **[!UICONTROL 快速發佈]**,Experience Manager未發佈所有資產或顯示將在中發佈多少資產 **[!UICONTROL 卡]** 視圖 **[!UICONTROL 清單]** 的子菜單。 (NPR-38546)
* 顯示的選定資產計數不正確 **[!UICONTROL 添加到集合]** 在 **[!UICONTROL 全選]** 案例。 (NPR-38633)
* 禁用的用戶仍可添加到「集合」和「項目」中。 (NPR-38651)
* 在不保存搜索表單的情況下刪除篩選器會導致錯誤。 (NPR-38698)
* 用戶的會話無法獲取 `ModifiableValueMap` 組的實例，以建立直接組成員身份。 (NPR-38710)

## 工作流程 {#workflow-6514}

* 啟用JavaScript ES6（ESMAScript6模式或更好）編譯支援，以縮小 `/libs/cq/inbox/gui/components/inbox/clientlibs/commons.js` 的下界。 (NPR-38304)
* 在工作流運行和流程步驟完成後，同一注釋會重複多次。 (NPR-38364)

## 安裝 [!DNL Experience Manager] 6.5.14.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.14.0要求 [!DNL Experience Manager] 6.5請參閱 [升級文檔](/help/sites-deploying/upgrade.md) 的上界。 <!-- UPDATE FOR EACH NEW RELEASE -->
* Service Pack下載可在Adobe上獲得 [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)。
* 在具有MongoDB和多個實例的部署中，安裝 [!DNL Experience Manager] 6.5.14.0在使用包管理器的某個「作者」實例上。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!NOTE]
>
>Adobe不建議刪除或卸載 [!DNL Experience Manager] 6.5.14.0包。 <!-- UPDATE FOR EACH NEW RELEASE -->

### 在上安裝Service Pack [!DNL Experience Manager] 6.5 {#install-service-pack}

1. 如果實例處於更新模式（當實例從早期版本更新時），請在安裝前重新啟動該實例。 Adobe建議在實例的當前正常運行時間較長時重新啟動。

1. 在安裝之前，請拍攝快照或新備份 [!DNL Experience Manager] 實例。

1. 從下載Service Pack [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.14.0.zip)。 <!-- UPDATE FOR EACH NEW RELEASE -->

1. 開啟包管理器，然後選擇 **[!UICONTROL 上載包]** 上載包。 要瞭解更多資訊，請參閱 [包管理器](/help/sites-administering/package-manager.md)。

1. 選擇包，然後選擇 **[!UICONTROL 安裝]**。

1. 要更新S3連接器，請在安裝Service Pack後停止實例，用安裝資料夾中提供的新二進位檔案替換現有連接器，然後重新啟動實例。 請參閱 [AmazonS3資料儲存](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)。

>[!NOTE]
>
>在安裝Service Pack期間，有時會退出包管理器UI上的對話框。 Adobe建議您在訪問部署之前等待錯誤日誌穩定。 請等待與卸載更新程式包相關的特定日誌，然後確保安裝成功。 通常，此問題發生在 [!DNL Safari] 但在任何瀏覽器上都可能間歇性出現。

**自動安裝**

有兩種方法可用於自動安裝 [!DNL Experience Manager] 6.5.14.0。<!-- UPDATE FOR EACH NEW RELEASE -->

* 將包放入 `../crx-quickstart/install` 資料夾。 軟體包將自動安裝。
* 使用 [包管理器中的HTTP API](/help/sites-administering/package-manager.md#package-share)。 使用 `cmd=install&recursive=true` 以便安裝嵌套的軟體包。

>[!NOTE]
>
>Experience Manager6.5.14.0不支援Bootstrap安裝。 <!-- UPDATE FOR EACH NEW RELEASE -->

**驗證安裝**

要瞭解經認證可與此版本配合使用的平台，請參閱 [技術要求](/help/sites-deploying/technical-requirements.md)。

1. 產品資訊頁面(`/system/console/productinfo`)顯示更新的版本字串 `Adobe Experience Manager (6.5.14.0)` 在 [!UICONTROL 已安裝的產品]。 <!-- UPDATE FOR EACH NEW RELEASE -->

1. 所有OSGi捆綁包 **[!UICONTROL 活動]** 或 **[!UICONTROL 片段]** 在OSGi控制台(使用Web控制台： `/system/console/bundles`)。

1. OSGi捆綁 `org.apache.jackrabbit.oak-core` 版本1.22.12或更高版本(使用Web控制台： `/system/console/bundles`)。 <!-- NPR-38747 -->


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

UberJar [!DNL Experience Manager] 6.5.13.0在 [Maven中央儲存庫](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.13/)。 <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

>[!NOTE]
>
>在Experience Manager6.5.14.0中，請注意UberJar版本(6.5.13.0)與上一版本相同。

要在Maven項目中使用UberJar，請參見 [如何使用UberJar](/help/sites-developing/ht-projects-maven.md) 並在項目POM中包括以下依賴關係： <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

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
| 整合 | 的 **[!UICONTROL AEM雲服務選擇加入]** 螢幕已棄用，因為 [!DNL Experience Manager] 和 [!DNL Adobe Target] 整合更新於 [!DNL Experience Manager] 6.5整合支援Adobe Target標準API。 API使用Adobe IMS驗證， [!DNL Adobe I/O Runtime]。 它支援Adobe發射對儀器的作用日益增強 [!DNL Experience Manager] 頁面進行分析和個性化設定，選擇加入嚮導在功能上無關緊要。 | 配置系統連接、Adobe IMS驗證和 [!DNL Adobe I/O Runtime] 通過各個 [!DNL Experience Manager] 雲服務。 |
| 連接器 | Microsoft®SharePoint® 2010和Microsoft®SharePoint® 2013的AdobeJCR連接器不建議使用 [!DNL Experience Manager] 6.5 | N/A |

## 已知問題 {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THE LIST.
 -->

* [GraphQL索AEM引包1.0.3的內容片段](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.3.zip)

* 作為 [!DNL Microsoft® Windows Server 2019] 不支援 [!DNL MySQL 5.7] 和 [!DNL JBoss® EAP 7.1]。 [!DNL Microsoft® Windows Server 2019] 不支援對 [!DNL AEM Forms 6.5.10.0]。

* 如果要升級 [!DNL Experience Manager] 實例從6.5版到6.5.10.0版，您可以查看 `RRD4JReporter` 例外情況 `error.log` 的子菜單。 要解決此問題，請重新啟動實例。

* 如果安裝 [!DNL Experience Manager] 6.5 Service Pack 10或上一個Service Pack [!DNL Experience Manager] 6.5，資產自定義工作流模型的運行時副本(建立於 `/var/workflow/models/dam`)。
要檢索運行時副本，Adobe建議使用HTTP API將自定義工作流模型的設計時副本與其運行時副本同步：
   `<designModelPath>/jcr:content.generate.json`。

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

## 包括OSGi捆綁包和內容包 {#osgi-bundles-and-content-packages-included}

以下文本文檔列出了包含在 [!DNL Experience Manager] 6.5.14.0 : <!-- UPDATE FOR EACH NEW RELEASE -->

* [6.5.14.0Experience Manager中包含的OSGi捆綁包清單](/help/release-notes/assets/65140_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [6.5.14.0Experience Manager中包含的內容包清單](/help/release-notes/assets/65140_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 受限網站 {#restricted-sites}

這些網站僅供客戶訪問。 如果您是客戶，需要訪問，請與Adobe客戶經理聯繫。

* [產品下載，網址為licensing.adobe.com](https://licensing.adobe.com/)
* [聯繫Adobe客戶支援](https://experienceleague.adobe.com/docs/customer-one/using/home.html)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 產品頁](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5文檔](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hant)
>* [訂閱 Adobe 優先產品更新](https://www.adobe.com/tw/subscription/priority-product-update.html)

