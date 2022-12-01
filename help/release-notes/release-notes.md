---
title: 的發行說明 [!DNL Adobe Experience Manager] 6.5
description: 查找發行資訊、新功能、安裝操作說明，以及 [!DNL Adobe Experience Manager] 6.5。
mini-toc-levels: 3
source-git-commit: 35595ffca9d2f6fd80bfe93bade247f5b4600469
workflow-type: tm+mt
source-wordcount: '3858'
ht-degree: 2%

---

# [!DNL Adobe Experience Manager] 6.5最新Service Pack發行說明 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession&cid=a915e87c-369a-480c-9daf-d13efc766798 -->

## 發行資訊 {#release-information}

| 產品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.15.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 類型 | Service Pack發行 |
| 日期 | 2022 年 11 月 24 日 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 下載 URL | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## 包含的項目 [!DNL Experience Manager] 6.5.15.0 {#what-is-included-in-aem-6515}

[!DNL Experience Manager] 6.5.15.0包含自2019年4月初次發行6.5以來所推出的新功能、客戶要求的重要增強功能、錯誤修正以及效能、穩定性和安全性等改善項目。 [安裝此Service Pack](#install) on [!DNL Experience Manager] 6.5。 <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_

* Added support for password reset for Dynamic Media Classic users within Experience Manager. (ASSETS-10298) -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets] {#assets-6515}

* 如果Experience Manager中的資產移動失敗，仍可重新命名資產。 (NPR-38753)
* 在 [!UICONTROL 清單檢視]，缺少部分標題。 (CQ-4345746)
* 螢幕助讀程式不會通知 [!UICONTROL 相關] 按鈕（位於「資產屬性」頁面上的「基本」頁簽上）。 (ASSETS-6938)
* 螢幕助讀程式會不正確地偵測「資產」導覽頁面上包含資料夾清單的資料夾圖示。 (ASSETS-6936)
* 複製集合時，影像缺少空白 `alt` 屬性或role=&quot;presentation&quot;。 因此，影像會公開給螢幕助讀程式使用者。 (ASSETS-6932)
* 為資產加上註解時顯示的文字沒有4:5:與背景顏色相比，有1個對比度。 (ASSETS-6931)
* 在「資產」屬性頁的「IPTC」頁簽上，當您調整頁寬時，頁面內容無法正常顯示，導致水準捲動。 (ASSETS-6929)
* 篩選資產時，會篩選 [!UICONTROL min] 和 [!UICONTROL max] 輸入值後欄位會消失。 (ASSETS-6925)
* 在Experience Manager集合中，螢幕助讀程式不會朗告 [!UICONTROL 電子郵件] 欄位。 (ASSETS-6923)
* 註解元素時遺失替代文字。 (ASSETS-6922)
* 如果文字在「小時」和「分鐘」中寫入日期選擇器欄位，則不會顯示文字錯誤訊息。 僅以紅色標識錯誤。 (ASSETS-6852、ASSETS-6921、ASSETS-6920、ASSETS-6907)
* 中的替代文字 `[role='img']` 檔案篩選器中缺少。 (ASSETS-6919)
* 螢幕助讀程式的公告不正確 [!UICONTROL 建立] 子菜單。 (ASSETS-6916)
* 在Experience Manager集合中，移除按鈕 `X` 沒有要為螢幕助讀程式朗讀的文字。 (ASSETS-6912)
* 在Experience Manager中使用Color Contrast Analyzer時，日曆介面工具集的日期選擇器中，目前日期與所選日期之間沒有顏色差異。 它的顏色與相鄰顏色的對比度至少為3:1。 (ASSETS-6911)
* 在「Experience Manager檔案」中，同時從 [!UICONTROL 排程] 「管理出版物」中的選項按鈕，螢幕助讀程式會公告選項選項名稱和狀態。 不過， **排程** 標籤未公告。 (ASSETS-6908、ASSETS-6906)
* 「排序」圖示缺少替代文字。 (ASSETS-6904)
* 在「資產屬性」頁面上，欄位名稱 `Person` 螢幕助讀程式不會公告IPTC擴充功能標籤中的標籤。 螢幕助讀程式只會朗讀可編輯且目前空白的欄位，但不會朗讀標籤名稱。 (ASSETS-6903、ASSETS-6848)
* 注釋工具無法使用鍵盤顯示。 用滑鼠繪製影像以顯示「注釋」工具。 (ASSETS-6899)
* 在Experience Manager集合中， **進階** 頁簽顯示邊界和相鄰顏色之間的對比度不正確。 (ASSETS-6895)
* 編輯資產時，某些元素的ARIA屬性值不正確。 (ASSETS-6894)
* 建立工作流程時，螢幕助讀程式無法正確識別標題。 (ASSETS-6892)
* 複製集合時，SVG影像移除按鈕 `X` with role=&quot;img&quot;缺少role=&quot;presentation&quot;。 因此，影像會公開給螢幕助讀程式使用者。 (ASSETS-6890)
* 在 **基本** 頁簽，螢幕助讀程式不會適當宣佈「標籤」欄位的展開或折疊狀態。 (ASSETS-6889)
* 此 **基本** 索引標籤（位於「資產屬性」下），其中包含ID重複的頁面。 (ASSETS-6888)
* 當您在文字方塊中指定值時，建立工作流程時，定義標題的文字欄位標籤會消失。 (ASSETS-6887)
* 共用連結時的收件者清單會顯示為含有標題的資料表格，但在語義上並未識別為螢幕助讀程式使用者的資料表格。 (ASSETS-6886)
* 中未顯示要表示空欄位的錯誤訊息 `Add Email Address` 欄位。 錯誤僅以顏色表示。 (ASSETS-6885、ASSETS-6843)
* 佔位符文本、路徑和替代文本與其背景顏色相比沒有至少4.5:1的對比度。 (ASSETS-6884、ASSETS-6865)
* 儲存智慧型集合時，某些ARIA屬性的值無效。 (ASSETS-6882)
* 儲存智慧型集合時，有些標籤無法適當地與螢幕助讀程式建立關聯。 (ASSETS-6881)
* 在資產屬性的IPTC索引標籤中，螢幕助讀程式不會宣佈關鍵字表單欄位的標籤。 (ASSETS-6879)
* 在Experience Manager集合中， [!UICONTROL 電子郵件] 欄位未識別為必填欄位，如果您未指定值，則不會顯示錯誤訊息。 (ASSETS-6877)
* 在Experience Manager檔案中， **連結共用** 畫面顯示於 `Add Email Address`. 僅在使用顏色時識別錯誤。 (ASSETS-6876、ASSETS-6875)
* [!UICONTROL 裁切和地圖] 編輯資產時，選項沒有程式化名稱。 (ASSETS-6874)
* 與背景顏色相比，「篩選」文字缺少4.5:1的合約比例。 (ASSETS-6873)
* 主導覽頁面上資料夾名稱的文字與背景顏色相比沒有4.5:1的對比度。 (ASSETS-6872)
* 執行 [!UICONTROL 複製] 集合的操作， **[!UICONTROL 添加用戶]** 組合框表單控制項未正確與其可見標籤關聯。 (ASSETS-6870)
* 螢幕助讀程式不會通知 [!UICONTROL 建立] 按鈕。 (ASSETS-6869)
* 與背景顏色相比，「範圍」、「工作流程」和「時區」選項沒有4.5:1的對比度。 (ASSETS-6868)
* 螢幕助讀程式會不正確地朗讀 **時間表** 欄。 (ASSETS-6864)
* 儲存智慧型集合時遺失部分ARIA角色的子元素。 (ASSETS-6862)
* 共用資產時，需要的ARIA屬性 `Search/Add Email Address` 欄位未指定。 (ASSETS-6860)
* 此 **地圖** 對話框。 而是需要按一下滑鼠，才能顯示地圖對話方塊。 (ASSETS-6859)
* 在「資產屬性」頁面的「基本」標籤上，遺失部分ARIA角色的子元素。 (ASSETS-6858)
* 在「資產」屬性的「IPTC」頁簽中可用的空文本輸入欄位與其相鄰顏色相比沒有3:1的對比度。 (ASSETS-6854、ASSETS-6847)
* 中的設定檔圖示 **時間表** 螢幕助讀程式未正確偵測區段。 (ASSETS-6850)
* 螢幕助讀程式不會宣佈「資產」屬性的「基本」索引標籤中提供的「檢閱狀態」下拉式方塊為唯讀欄位。 (ASSETS-6849)
* 螢幕助讀程式不會適當宣佈「全部選取」和「註解」核取方塊的標籤。 (ASSETS-6846)
* 鍵盤焦點跳過 `About Adobe Experience Manager` 選項 **顯示幫助** 功能表。 (ASSETS-6845)
* 在「卡片」檢視中使用鍵盤箭頭鍵瀏覽資料夾清單時，螢幕助讀程式無法正確宣告選取的資料夾。 (ASSETS-6844)
* 將PDF上傳至Experience Manager時，記憶體使用量持續增加。 (ASSETS-16889)
* 工作流程將.ZIP檔案轉換為「資產」中的資料夾名稱時，不會保留.ZIP檔案名稱的大小寫。 (ASSETS-16712)
* 從Brand Portal切換至Experience Manager6.5時，當您首次套用篩選時，使用者述詞篩選器不會顯示適當的結果。 (ASSETS-15932)
* 無法為視訊加上注釋。 (ASSETS-15217)
* **管理出版物** 選項會消失，而沒有復寫存取權的使用者則會消失， `READ` 和 `WRITE` 存取 `ETC` 和 `VAR`. (ASSETS-15007)
* 屬性頁面的載入時間會針對包含多個參考的資產而增加。 (ASSETS-14182)
* 從Brand Portal取消發佈影像時，Experience Manager也會從Dynamic Media取消發佈影像，因此即時網站上不會顯示影像。 (ASSETS-14118)
* Dynamic Media中智慧型裁切卡的XSS問題。 (ASSETS-14212、ASSETS-14208、ASSETS-13704)
* Dynamic Media中的檢視器預設集出現XSS問題。 (ASSETS-13822)
* 在AEM上預覽DM資產時驗證使用者存取權。 (CQ-4314757)


## 商務 {#commerce-6515}

* 建立商店頁面失敗，停止了整體目錄轉出程式。 (CQ-4347181)

## [!DNL Forms] {#forms-6515}

### 主要功能 {#keyfeatures}

* AEM Forms Designer現在可在 [西班牙語地區](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html). (LC-3920051)
* 您現在可以使用 [OAuth2用於通過Microsoft Office 365郵件伺服器協定（SMTP和IMAP）進行身份驗證](/help/forms/using/oauth2-support-for-mail-service.md). (NPR-35177)
* 您可以設定 [在伺服器上重新驗證](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-an-adaptive-form/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html#enabling-server-side-validation-br) 屬性設為true ，以識別伺服器端之記錄檔案中要排除的隱藏欄位。 (NPR-38149)
* AEM Forms Designer需要32位元版本的Visual C++ 2019 Redistributable(x86)。  (NPR-36690)

### 修正 {#fixes}

* 切換適用性表單的資料停用屬性時，選項按鈕和核取方塊群組的外觀不會變更。 (NPR-39368)
* 翻譯適用性表單時，部分翻譯會遺漏，且無法正確顯示。 (NPR-39367)
* 將頁面的屬性設定為隱藏時，不會從表單集中移除頁面。 (NPR-39325)
* 在記錄檔案中，頁面結尾的動態腳注區段不存在。 (NPR-39322)
* 為適用性表單產生記錄檔案時，選項按鈕和核取方塊僅允許垂直對齊。 用戶無法設定單選按鈕和複選框的水準對齊方式。 (NPR-39321)
* 部署通信管理後，如果多個使用者嘗試存取表單， org.apache.sling.i18n.impl.JcrResourceBundle.loadPetonialLanguageRoots就會成為瓶頸，且大部分執行緒會遭到觸發。 即使伺服器的負載很低，各種表單頁面請求也往往需要1分鐘以上的時間才能載入。 (NPR-39176、CQ-4347710)
* 在適用性表單中，當您在延遲載入適用性表單片段中使用RTF欄位時，會發生下列部分錯誤：
   * 您無法編輯內容或將任何內容附加至「RTF」欄位。
   * 套用至RTF的顯示模式不會執行。 
   * 提交表單時不會顯示最小欄位長度的錯誤訊息。
   * 此RTF欄位的內容在產生的submit-XML中已包括多次。 (NPR-39168)
* 在適用性表單中使用「日期」選擇器選項時，無法將值轉換為正確的格式。 (NPR-39156)
* 以HTML表單預覽適用性表單時，無法正確轉譯，因為部分子表單與父表單重疊。 (NPR-39046)
* 如果面板有隱藏的表格，且使用表格檢視轉譯適用性表單，則第一個標籤上的欄位無法正確顯示。 (NPR-39025)
* 此 `Body` OOTB（現成可用）範本缺少標籤。 (NPR-39022)
* 記錄檔案不會以最適化表單的語言產生。 它總是以英語產生。 (NPR-39020)
* 當適用性表單有多個面板，且部分面板使用現成可用的 **檔案附件** 元件， `Error occurred while draft saving` 發生錯誤。 (NPR-38978)
* 當 `=` 符號用於「適用性表單」的核取方塊、下拉式清單或選項按鈕欄位，並產生「記錄檔案」，然後 `=` 生成的記錄文檔中不顯示符號。(NPR-38859)
* 6.5.11.0 Service Pack升級後，通知批次處理錯誤的數量增加了數量多倍。 (NPR-39636)
* 若您未提供測試資料，通信管理信函無法載入代理程式UI中。 (CQ-4348702)
* 使用者從使用IBM® WebSphere®部署的AEM Forms套用AEM Forms Service Pack 14(SP14)時，啟動程式在初始化資料庫和 `java.lang.NoClassDefFoundError:org/apache/log4j/Logger` 發生錯誤。(NPR-39414)
* 在OSGi伺服器上的AEM表單中，當您使用檔案服務API來驗證PDF時，表單會失敗並出現錯誤：com.adobe.fd.signatures.truststore.errors.exception.CredentialRetrievalException:AEM-DSS-311-003。 (NPR-38855)
* 當使用者嘗試使用包裝服務來轉譯具有AEM 6.3 Forms的信函時， `java.lang.reflect.UndeclaredThrowableException` 發生錯誤。 (CQ-4347259)
* 當XDP呈現為HTML5表單時，無論對象在適用性表單中的位置如何，都會先呈現首頁的內容。 (CQ-4345218)
* 目標伺服器上的應用程式配置將更改為源伺服器上定義的設定，即使 **完成匯入時覆寫設定** 匯入應用程式時未核取選項。 (NPR-39044)
* 當使用者嘗試使用Configuration Manager更新連接器組態時，會失敗。(CQ-4347077)
* 當使用者在變更管理員使用者的預設密碼後，嘗試在JEE修補程式上執行AEM Forms時，會發生例外狀況 `com.adobe.livecycle.lcm.core.LCMException[ALC-LCM-200-003]: Failed to whitelist the classes` 發生。 (CQ-4348277)
* 在AEM Designer中，沒有標題的表單欄位會放置在表格儲存格中，包括核取方塊。(LC-3920410)
* 當使用者嘗試在AEM Forms Designer中開啟「說明」時，無法正確顯示。 (CQ-4341996)

## [!DNL Sites] {#sites-6515}

* Experience Manager Sites啟動主控台的顯示為空白。 (NPR-39188)
* 在頁面移動期間，也需要啟動具有參考的頁面時，參考未經過調整。 (NPR-39061)
* 使用父容器取消隱藏「配置」容器時，配置變更不會套用至巢狀容器內的所有元件。 (NPR-39041)
* 以320像素寬度顯示的內容現在不再與其他內容重疊。 (SITES-8885)
* 關閉對話方塊後新增焦點。 (SITES-8885)

### 協助工具 {#access-6515}

<!-- REMOVED FROM TOTAL RELEASE CANDIDATE LIST * The scrollable region of the Page Editor did not have keyboard access. (SITES-2936) -->
<!-- REMOVED FROM TOTAL RELEASE CANDIDATE LIST * The color input field of the Page Editor is not labeled or visible on the screen. (SITES-2925) -->
<!-- REMOVED FROM TOTAL RELEASE CANDIDATE LIST * The iframe in the Page Editor is missing a title attribute; it must have an accessible name. (SITES-2894) -->
* 此 **[!UICONTROL 註解]** 按鈕缺少其輔助功能名稱。 (SITES-2892)
* ACTIVE用戶介面元件的狀態(**[!UICONTROL 剪下]**, **[!UICONTROL 複製]**, **[!UICONTROL 貼上]**, **[!UICONTROL 插入元件]**, **[!UICONTROL 群組]**&#x200B;等)與內外相鄰背景之間沒有至少三對一的明度對比度。 (SITES-8889、SITES-8756、SITES-8885)
* 狀態消息未自動宣佈。 (SITES-8889、SITES-8756、SITES-8885)
* 文字內容缺少4.5:1的對比。 (SITES-8756、SITES-8885)
* 暫留或焦點上的連結或按鈕文字缺乏4.5:1的對比率。 (SITES-8756、SITES-8885)

### [!DNL Content Fragments] {#sites-contentfragments-6515}

* GraphQL引發異常。 例如，您無法從內容片段取得變異標籤。 「電氣」的名稱沒有變化。 此問題是由於呼叫 `getVariationTags` 對於引發例外的非現有變數。 (SITES-8898)
* 在「清單」檢視中排序標題順序（升序和降序），標題的順序為A、C、B。(SITES-7585)
* 新增內容片段變異的標籤支援。 (SITES-8168)
* 從Experience Manager6.5中識別並移除不必要的Odin特定程式碼。 (SITES-3574)
* 從內容片段編輯器使用者介面發佈語言副本片段時，系統會在英文資料夾下發佈相關的參考。 (NPR-39182)
* 日期欄位會預先填入日期。 (NPR-39124)
* 當您第二次選取選項按鈕選項時，標籤會消失。 (NPR-39071)

### Fluid XP {#sites-fluidxp-6515}

* 為客戶端庫啟用ES6編譯支援 `/libs/cq/gui/components/siteadmin/admin/restoretree/clientlibs/restoretree.js`. (NPR-39067)
* 內容片段模型中的多欄位無法清空和儲存，因為即使進行驗證 **[!UICONTROL 必填]** 未選取。 (NPR-39063)
* 在 **[!UICONTROL 複製]** 或 **[!UICONTROL Livecopy]** 任務， `cq:targetMetadata` 錯誤地複製資訊。 此功能造成Experience Manager中的兩個或多個體驗片段指向匯出至Target中的相同選件。 (NPR-38970)
* 執行「還原樹」操作後，消息 `Un-publication pending. #0 in the queue` 會顯示在使用者介面中，用於原本從未發佈過的頁面。 (NPR-38847)

### 頁面編輯器 {#sites-pageeditor-6515}

* 復原並未刪除對新增至元件中的文字所做的上次變更。 反之，重新整理頁面時，會刪除整個元件。 (SITES-8597)
* 升級 `jquery-ui` 至最新版本，導致頁面編輯器無法正常運作。 (NPR-38596)
* 以320像素寬度顯示的內容現在不再與其他內容重疊。 (SITES-8756)
* 在關閉對話方塊後新增焦點(SITES-8756)

## Sling {#sling-6515}

* `Repoinit` 不支援建立或管理主體名稱中包含空格的組，因為組名稱被視為字串，並且不支援引用。 (SLING-10952)
* 記錄檔不小心填入了錯誤訊息和例外。 (NPR-39024)

## 翻譯專案 {#translation-6515}

* 透過「專案」面板將目標頁面新增至更新語言副本的翻譯工作中；源頁面未更新。 (NPR-39278)
* 為翻譯專案中的所有頁面產生預覽時，翻譯程式失敗。 (NPR-39059)
* 如果語言區域設定不存在，則為事件配置引用規則時，仍會在區域設定資料夾中建立該語言區域。 (NPR-39054)

## 使用者介面 {#ui-6515}

* 檔案內發生JavaScript錯誤 `multifield.js` 針對內容片段模型編輯器中以及內容片段編輯器中的「內容片段」模型中的某些欄位。 (NPR-39350)

## 工作流程 {#workflow-6515}

* 在Experience Manager6.5.11上成功執行的工作流程，在Experience Manager的6.5.13上未一致地執行。 (NPR-39023)

## 安裝 [!DNL Experience Manager] 6.5.15.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.15.0要求 [!DNL Experience Manager] 6.5.見 [升級檔案](/help/sites-deploying/upgrade.md) 以取得詳細指示。 <!-- UPDATE FOR EACH NEW RELEASE -->
* Service Pack下載可在Adobe上取得 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* 在具有MongoDB和多個實例的部署上，安裝 [!DNL Experience Manager] 6.5.15.0，在使用套件管理器的其中一個製作執行個體上。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
>Adobe不建議您移除或解除安裝 [!DNL Experience Manager] 6.5.15.0包。 因此，在安裝該包之前，您應建立 `crx-repository` 以防你需要把它卷回去。 <!-- UPDATE FOR EACH NEW RELEASE -->

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

您可以使用兩種不同的方法來自動安裝 [!DNL Experience Manager] 6.5.15.0。<!-- UPDATE FOR EACH NEW RELEASE -->

* 將包裝放入 `../crx-quickstart/install` 資料夾。 程式包會自動安裝。
* 使用 [來自套件管理器的HTTP API](/help/sites-administering/package-manager.md#package-share). 使用 `cmd=install&recursive=true` 以便安裝嵌套包。

>[!NOTE]
>
>Experience Manager6.5.15.0不支援Bootstrap安裝。 <!-- UPDATE FOR EACH NEW RELEASE -->

**驗證安裝**

若要了解經認證可與此版本搭配使用的平台，請參閱 [技術要求](/help/sites-deploying/technical-requirements.md).

1. 產品資訊頁面(`/system/console/productinfo`)顯示更新的版本字串 `Adobe Experience Manager (6.5.15.0)` 在 [!UICONTROL 已安裝的產品]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. 所有OSGi套件組合 **[!UICONTROL 活動]** 或 **[!UICONTROL 片段]** 在OSGi控制台中(使用Web控制台： `/system/console/bundles`)。

1. OSGi捆綁 `org.apache.jackrabbit.oak-core` 為1.22.13版或更新版本(使用Web控制台： `/system/console/bundles`)。 <!-- NPR-39436 for 6.5.15.0 --> <!-- OAK VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### 安裝 [!DNL Experience Manager] Forms附加元件套件 {#install-aem-forms-add-on-package}

>[!NOTE]
>
>如果您未使用 [!DNL Experience Manager] Forms。

<!-- 
Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package a week after the scheduled [!DNL Experience Manager] Service Pack release.
-->

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

UberJar [!DNL Experience Manager] 6.5.15.0可在 [Maven Central存放庫](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.15/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

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
| Integrations | 此 **[!UICONTROL AEM雲端服務選擇加入]** 螢幕已過時，因為 [!DNL Experience Manager] 和 [!DNL Adobe Target] 整合已於 [!DNL Experience Manager] 6.5.整合支援Adobe Target Standard API。 API使用Adobe IMS驗證，並 [!DNL Adobe I/O Runtime]. 它支援AdobeLaunch在儀器方面日益發揮的作用 [!DNL Experience Manager] 分析和個人化的頁面，選擇加入精靈的功能與您無關。 | 設定系統連線、Adobe IMS驗證，以及 [!DNL Adobe I/O Runtime] 透過個別 [!DNL Experience Manager] 雲端服務。 |
| 連接器 | Microsoft® SharePoint 2010和Microsoft® SharePoint 2013的AdobeJCR Connector已於 [!DNL Experience Manager] 6.5。 | N/A |

## 已知問題 {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->

* [AEM內容片段搭配GraphQL索引套件1.0.5](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.5.zip)
使用GraphQL的客戶需要此軟體包；這可讓使用者根據實際使用的功能，新增所需的索引定義。

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

以下文字檔案列出包含在 [!DNL Experience Manager] 6.5.15.0: <!-- UPDATE FOR EACH NEW RELEASE -->

* [Experience Manager6.5.15.0中包含的OSGi套件組合清單](/help/release-notes/assets/65150_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager6.5.15.0中包含的內容套件清單](/help/release-notes/assets/65150_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 受限網站 {#restricted-sites}

這些網站僅供客戶使用。 如果您是Adobe，且需要存取權，請聯絡您的客戶經理。

* [透過licensing.adobe.com下載產品](https://licensing.adobe.com/)
* [聯絡Adobe客戶支援](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 產品頁面](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5檔案](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hant)
>* [訂閱 Adobe 優先產品更新](https://www.adobe.com/tw/subscription/priority-product-update.html)

