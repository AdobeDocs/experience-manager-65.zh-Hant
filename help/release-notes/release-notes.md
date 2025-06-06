---
title: ' [!DNL Adobe Experience Manager] 6.5的發行說明'
description: 尋找 [!DNL Adobe Experience Manager] 6.5的版本資訊、新增功能、安裝操作說明和詳細變更清單。
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: 8cbf7188baf8cc997e0747be366f13c3b6c2c632
workflow-type: tm+mt
source-wordcount: '4590'
ht-degree: 2%

---

# [!DNL Adobe Experience Manager] 6.5最新Service Pack發行說明 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, May 29, 2025. In addition, a list of Forms fixes and enhancements is added to this section. -->

## 發行資訊 {#release-information}

| 產品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.23.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 類型 | Service Pack發行 |
| 日期 | 2025年5月22日（星期四）<!-- UPDATE FOR EACH NEW RELEASE --> |
| 下載 URL | [軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## [!DNL Experience Manager] 6.5.23.0包含的內容 {#what-is-included-in-aem-6523}

[!DNL Experience Manager] 6.5.23.0包含新功能、客戶要求的重要增強功能和錯誤修正。 此外，還包含自2019年4月6.5首次推出以來的效能、穩定性和安全性改善專案。 在[!DNL Experience Manager] 6.5上[安裝此Service Pack](#install)。

<!-- UPDATE FOR EACH NEW RELEASE -->

## 主要功能和增強功能

<!--### Sites {#sites}

* A () -->

<!--
### [!DNL Assets]

* A ()
-->

### Forms {#forms-sp23}

此版本中的主要功能和增強功能包括：

* [在靜態PDF中具有混合文字樣式的輔助功能超連結](https://helpx.adobe.com/tw/content/dam/help/en/experience-manager/6-5/forms/pdf/using-designer.pdf)：在靜態PDF中包含混合文字樣式的超連結，現在已標籤為單一輔助功能元素。 此增強功能簡化了標籤樹結構、改善了熒幕助讀程式導覽，並支援更出色的協助工具合規性。

* [已更新支援的平台矩陣](/help/forms/using/aem-forms-jee-supported-platforms.md)

  最新版本引進了支援平台對照表的更新，確保與更新技術相容。

   * IBM Content Manager Client 8.7

   * MongoDB Enterprise 7.0

   * MySQL 8.4

   * Microsoft® SQL Server 2022

   * Microsoft® SQL Server JDBC驅動程式12.8

   * Microsoft® Office 2021

   * Red Hat® Enterprise Linux® 9 （核心4.x，64位元） 



* [強化的檔案附件元件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment)：作為安全性測量，此元件現在會防止提交副檔名經過修改、嘗試略過允許的檔案型別檢查的檔案。 提交期間會封鎖這類檔案，以確保僅接受有效的檔案型別。

<!--* **Two-Factor authentication with SAML for AdminUI** 

  AdminUI in AEM Forms JEE now supports two-factor authentication using Security Assertion Markup Language (SAML) single sign-on (SSO), providing stronger security and a seamless login experience for administrators, similar to what is available in HTML Workspace. 

#### New GA features in AEM Forms {#ga-aem-forms-sp23}

* A ()

#### New Beta features in AEM Forms {#beta-aem-forms-sp23}
-->

## 已修正Service Pack 23中的問題 {#fixed-issues}

<!-- 6.5.23.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

### [!DNL Sites]{#sites-6523}

#### 協助工具 {#sites-accessibility-6523}

* AEM編輯器頁面中的畫布區段現在支援完整的鍵盤協助工具。 使用者可以僅使用鍵盤啟動區段標題和編輯按鈕，而不需依賴滑鼠懸停。 此更新確保符合WCAG 2.1.1，並改善各種元件（例如Teaser、影像、輪播、版面、時間扭曲和註解模組）的可用性。 (SITES-25256) <!-- 6.5 LTS SP1 -->
* 修正AEM頁面編輯器中的協助工具問題，該問題導致在啟動「角色」、「購物車」或「放棄」等按鈕後，鍵盤焦點意外地重設為「人口統計」工具列的開始。 焦點現在仍停留於已啟用的按鈕，以支援一致的鍵盤導覽和熒幕助讀程式工作流程。 (SITES-25306)
* 修正AEM頁面編輯器中的重大協助工具問題，該問題導致多個對話方塊和模式（例如，資產邊欄或版面預覽）中的畫布元素無法僅使用鍵盤操作。 所有互動式畫布元素現在支援僅鍵盤導覽，確保符合WCAG 2.1成功標準2.1.1 (SITE-25256)
* 修正Sites管理員UI中，建立快顯視窗中的互動式清單專案使用不正確ARIA角色的協助工具問題。 行為類似連結的元素被指派為`role="listitem"`而非`role="menuitem"`，這違反了ARIA設計模式並混淆熒幕閱讀器。 更新可確保所有清單元件都遵循適當的語意角色，以提升鍵盤和輔助技術支援的效能。 (SITES-24493)
* 修正頁面標題和標籤欄位的協助工具標籤關聯問題。 AEM介面現在會在使用JAWS等熒幕助讀程式時，正確地將協助工具標籤與「標題」和「頁面標題」欄位建立關聯。 此修正可確保正確讀取標籤，並改善頁面建立、屬性和移動工作流程中的ADA合規性。 (SITES-27149)
* 修正許可權對話方塊中表格識別的協助工具問題。 AEM中的許可權表格現在會使用正確的ARIA角色和屬性，以確保熒幕助讀程式（如JAWS）能正確將其識別為表格。 此修正可改善協助工具合規性，並確保使用者收到準確的導覽和內容公告。 (SITES-27140)
* 修正時間軸中註解輸入欄位缺少視覺標籤的問題。 修正時間軸區段下「註解」輸入欄位缺少視覺標籤的問題，以改善協助工具。 此更新可確保熒幕助讀程式可以準確地朗讀欄位標籤。 此體驗可增強所有使用者的表單導覽和提交功能，尤其是依賴輔助技術的個人。 (SITES-26903)
* 修正時間軸註解中省略符號按鈕的鍵盤協助工具。 啟用時間軸區段下註解旁的省略符號（三個點）按鈕的鍵盤導覽。 使用者現在可以使用Tab鍵存取並與按鈕互動，改善了依賴僅鍵盤導覽的使用者的協助工具。 (SITES-26891)
* 改善選擇對話方塊中搜尋結果的NVDA/朗讀程式宣告。 更新「開啟選取專案」對話方塊，以宣告在使用熒幕助讀程式（例如NVDA或「朗讀程式」）時是否找到搜尋結果。 這項改善可協助依賴輔助技術的使用者瞭解其搜尋動作的結果，而不需要視覺確認。 (SITES-26883)
* 修正評論輸入欄位旁省略符號圖示的ARIA角色。 更新評論輸入欄位旁的省略符號（三個點）圖示，以使用正確的ARIA角色，確保熒幕助讀程式可準確識別元素。 這項改善可增強協助工具的合規性，並改善依賴輔助技術的使用者的體驗。 (SITES-26881)
* 更正Coral UI元件中無效的ARIA屬性。 更新Coral UI元件，確保所有ARIA屬性都使用有效值，進而改善協助工具合規性。 特別是，已處理錯誤指派`aria-modal="dialog"`等無效值的案例。 此增強功能可讓熒幕助讀程式正確解讀對話方塊元素，協助依賴輔助技術的使用者提升協助工具。 (SITES-26873)
* 改善重排情境中圖示的可見度和工具提示。 已增強重排行為，以確保針對&#x200B;**下載**、**重新處理資產**&#x200B;和&#x200B;**簽出**&#x200B;圖示正確顯示工具提示。 著重於在檢視區調整大小或瀏覽器縮放設定變更時，圖示及其標籤會變成隱藏的協助工具問題。 此修正可維護可見度，並在重排期間提供適當的圖示說明，以支援視力缺佳的使用者。 (SITES-26871)

#### 管理員使用者介面{#sites-adminui-6523}

修正Universal Editor URL服務例外狀況，遺失Externalizer端點。 Universal Editor URL服務現在可處理遺漏的作者、發佈或本機外部化程式端點，而不會擲回例外狀況。 即使部分外部器設定不完整，管理員使用者也可以成功開啟頁面編輯器。 (SITES-28877) <!-- LTS -->

#### 傳統 UI{#sites-classicui-6523}

* 傳統UI對話方塊中的問題，其中切換按鈕會隱藏文字區域，且無法於後續點按時再次顯示。 此修正可確保在切換時文字區域正確地重新顯示，恢復預期行為並防止動態對話方塊工作流程中斷。 (SITES-30230)
* 修正Service Pack 22升級後Classic UI影像資產尋找器功能中斷的問題。 Classic UI影像資產尋找器現在可以正確處理包含空格或特殊字元的資產名稱。 此更新可確保資產尋找器可正確編碼檔案名稱、避免搜尋失敗，並允許作者找到並選取影像資產，而不會發生錯誤。 (SITES-29151)

#### [!DNL Content Fragments]{#sites-contentfragments-6523}

* 修正`DeleteVariationIT.testUpdateBasic`的驗證測試失敗。 `DeleteVariationIT.testUpdateBasic`測試在Service Pack驗證執行期間不再失敗。 此修正修正修正了JSON處理邏輯中缺少文字對應的問題，確保測試穩定性並避免不必要的測試中斷。 (SITES-28022)
* AEM現在可以防止影像資產中XMP中繼資料的格式錯誤導致效能降低。 Assets如果包含無效或不相容的XMP屬性名稱（例如具有數值區段或不合格結構的名稱），在處理期間將不再觸發重複的警告記錄。 系統會篩選掉有問題的中繼資料，以確保資產擷取和驗證完成且沒有錯誤。 (SITES-30683) <!-- AEM 6.5 LTS SP1 -->


<!-- #### [!DNL Content Fragments] - Admin{#sites-admin-6523}

* A () -->


#### [!DNL Content Fragments] — 片段編輯器{#sites-fragments-editor-6523}

其他作者仍可發佈內容片段，即使其他作者簽出它們，這違反了簽出功能的預期行為。 此修正可防止其他使用者在取出內容片段時，在製作介面中看見或使用發佈按鈕。 (SITES-30578) <!-- LTS -->

#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-6523}

修正了包含內容片段結構描述的GraphQL QueryValidationError。 重新整理`cq-dam-cfm-graphql`套件組合可更正使用內容片段參考時的結構描述驗證錯誤。 此修正可確保GraphQL查詢正常運作，不需要在部署套件後手動重新對齊結構描述或重新發佈。 (SITES-27001) <!-- LTS -->


<!-- #### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6523}

* A () -->

<!-- #### [!DNL Content Fragments] - REST API{#sites-restapi-6523}

* A () -->


#### 元件主控台{#sites-component-console-6523}

改善「元件即時使用情況」頁面載入作業。 最佳化AEM中的「元件即時使用情況」頁面，以防止在捲動大型資料集時顯示空白列。 載入包含大量使用參照之元件的使用者現在可以體驗持續資料載入，而不會出現不必要的空白或空白專案。 此體驗可改善跨元件使用報告的頁面導覽、追蹤準確度和管理效率。 (SITES-26454)

#### 核心後端{#sites-core-backend-6523}

* 已修正內容尋找器資產因無效資產名稱而列出失敗的問題。 內容尋找器現在會正確處理含有不可編碼字元的資產名稱。 遇到名稱有問題的資產時，頁面編輯器中的資產清單不再失敗或擲回例外狀況。 (SITES-28722)
* `SearchPathLimiter`元件在每個呼叫的ERROR層級列印訊息，產生過多記錄專案的問題。 這種行為始於Service Pack 17之後，並由於記錄磁碟區極高而導致效能問題。 此修正將記錄層級降級為DEBUG，大幅降低記錄雜訊並改善系統監控和診斷效率。 (SITES-29835)
* 處理`ValidationDataServlet`中的影像資產時，不正確格式化的XMP中繼資料觸發錯誤。 此修正可確保規範的中繼資料處理，並避免多餘剖析無效屬性。 (SITE-30683) <!-- LTS -->


<!-- #### Core Components{#sites-core-components-6523}

* A () -->

<!-- #### Campaign integration{#sites-campaign-integration-6523}

* A () -->

<!-- #### Experience Fragments{#sites-experiencefragments-6523}

* A () -->

<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6523}

* A () -->


#### 啟動{#sites-launches-6523}

* 修正12月25日到12月31日之間不正確的啟動日期顯示。 Launches UI現在會以正確的年份顯示12月25日至12月31日之間的日期。 此修正可確保日期不再錯誤地顯示下一年，避免在行銷活動規劃和排程期間產生混淆。 (SITES-28706)
* 修正Service Pack 22升級後損毀的AEM Launch範本。 Service Pack 22升級後，AEM Launch範本現在可正確載入。 此修正可更正內部啟動設定中的無效資料，讓使用者檢視、編輯和建立啟動，而不會出現錯誤或遺失欄位。 (SITES-28504)


<!-- #### Link Checker{#sites-link-checker-6523}

* A () -->

<!-- #### MSM - Live Copies{#sites-msm-live-copies-6523}

* A () -->


#### 頁面編輯器{#sites-pageeditor-6523}

* 修正較低熒幕解析度的AssetPicker載入問題。 現在，當使用者以較低熒幕解析度(1728×1117或更低)捲動時，AssetPicker會正確載入資產。 使用者在捲動時不再體驗缺少資產的情況，進而改善不同裝置中斷點的資產管理。 (SITES-28065)
* 修正頁面鎖定和解鎖動作遺失熒幕助讀程式宣告的問題。 現在，當使用者啟動鎖定/解鎖按鈕時，頁面編輯器會正確宣佈「資訊：頁面已鎖定/解鎖」訊息。 此修正可改善協助工具合規性，並確保熒幕助讀程式的使用者在頁面編輯期間會收到動態更新。 (SITES-27143)
* 改善AEM編寫中元件動作的鍵盤焦點行為。 AEM製作工具中的鍵盤導覽改良功能，可確保焦點在執行「設定」、「刪除」或「轉換」等動作後，仍位於新建立或選取的元件上。 先前，焦點會移至頁面頂端，造成協助工具法規遵循問題。 此更新改善了鍵盤和輔助技術使用者的使用者體驗。 它透過在編輯工作流程中維護邏輯焦點進度來達到此目的。 (SITES-26549)
* 改善「作者」對話方塊中的索引標籤導覽。 允許使用者在到達「說明」編輯方塊後繼續往前Tab鍵，藉以增強AEM Author對話方塊中的鍵盤導覽。 先前，在「說明」欄位中鎖定焦點會封鎖進一步的導覽，而不使用特殊按鍵組合。 此更新可確保使用者僅需使用Tab鍵，就能順暢地移動各欄位，進而改善協助工具合規性及使用者體驗。 (SITES-26524)
* AEM 6.5 Service Pack 22已引入回歸，防止使用者在Launch標題中納入空格。 此修正恢復使用空格的能力，讓團隊根據預期行為更靈活地定義及組織Launch名稱。 (SITES-29414)
* 修正在隱藏/取消隱藏動作後，配置容器內元件的大小調整問題。 現在隱藏和取消隱藏「版面容器」後，「頁面編輯器」可正確計算欄值。 使用者可以在沒有錯誤的情況下調整元件大小，且欄會在調整大小動作期間正確顯示。 (SITES-28463)
* 已修正頁面編輯器中的內容樹按鈕放置錯誤。 頁面編輯器現在會在預期的「Head Teaser」對話方塊下正確放置內容樹設定按鈕，而不是錯誤的區段。 此修正會更新內容樹狀結構對話方塊的CSS，以使用`top:0`而非`bottom:0`，確保按鈕位置正確。 (SITES-28448)


<!-- #### Replication{#sites-replication-6523}

* A () -->


#### RTF 編輯器{#sites-rte-6523}

使用純文字貼上模式修正RTF編輯器中未預期的`<br>`標籤。 RTF編輯器現在會在使用純文字`defaultPasteMode`時正確處理剪下和貼上操作。 此修正可防止使用者在RTE欄位中剪下並貼上文字時，插入未預期的`<br>`標籤，以確保在內容編輯期間可清除格式設定。 (SITES-27780)

#### Universal Editor {#sites-universal-editor-6523}

* 將包含查詢引數的多個請求傳送至AEM時，可能無法及時傳回登入權杖Cookie，進而導致登入失敗。 (SITES-30659) <!-- LTS -->
* 若要確保相容性並支援SAML處理常式，您必須設定`service.ranking`屬性，讓`Query Token Auth`處理常式在&#x200B;*`SAML Auth`處理常式之前*&#x200B;執行。 (SITES-29684)

### [!DNL Assets]{#assets-6523}

* 選取![Assets](/help/assets/assets/Smock_Asset_18_N.svg)**[!UICONTROL Assets ]**、瀏覽至**[!UICONTROL &#x200B;搜尋Adobe Stock ]**資料夾並選取庫存影像後，[!DNL AEM]內部部署(6.5.22.0)導覽頁面中會發生下列問題：
   * 選取的stock影像無法授權並儲存為按一下「**[!UICONTROL 授權並儲存]**」會顯示空白的下拉式清單。
   * 選取Stock影像或重新進入庫存頁面URL會重新導向至[!DNL AEM]首頁，導致無法存取Adobe Stock影像。 (ASSETS-48687)
* 如果資料夾名稱在[!DNL AEM]內部部署(6.5.22.0)導覽頁面上的名稱包含`/`，則管理資料夾時發生問題。 (ASSETS-46740)
* 在[!DNL AEM] 6.5上，由於記憶體使用量高，資產詳細資訊頁面未從![集合](/help/assets/assets/Smock_Collection_18_N.svg)**[!UICONTROL 集合&#x200B;]**檢視載入。 (ASSETS-46738)
* [!DNL InDesign]的整合問題為`Day CQ DAM Mime Type OSGI`服務錯誤將[!DNL InDesign]個檔案識別為`x-adobe-indesign`而非`x-indesign`。 (ASSETS-45953)
* [!DNL AEM 6.5.21]工作階段洩漏追蹤至現成可用的&#x200B;**[!UICONTROL 已排程發佈至Brand Portal]**&#x200B;工作流程步驟。 (ASSETS-44104)
* 處理和發佈影像時，[!DNL AEM]中顯示&#x200B;**[!UICONTROL 記憶體不足(OOM)]**&#x200B;錯誤。 此問題是因為工作流程中已棄用的方法，例如&#x200B;**[!DNL Dam Asset update]**&#x200B;和&#x200B;**[!DNL Dynamic Media: Reprocess assets]**。 (ASSETS-43343)
* 進行微幅變更後（例如更新標題），您會重新開啟並重新儲存本機Sites執行個體上的&#x200B;**[!DNL Connected Assets configuration]**。 然後，遠端執行個體會失去與本機執行個體的連線。 因此，它無法與本機Sites執行個體建立通訊。 (ASSETS-44484)
* 在[!DNL AEM 6.5.21]中，當清單檢視中的資產上傳被取消並執行第二次上傳時，[!DNL AEM]會顯示已上傳的&#x200B;**[!UICONTROL 0個NaN資產]**&#x200B;錯誤。 (ASSETS-44124)

#### [!DNL Dynamic Media]{#assets-dm-6523}

已將中繼資料屬性(`jcr:content/metadata/dam:scene7SmartCropStatus`)新增至資產，以識別失敗的智慧型裁切層代。 透過手動或自動化工作流程，有效率地搜尋、篩選及重新處理具有智慧型裁切問題的資產。 (ASSETS-46237)

#### [!DNL Dynamic Media] — 混合模式 {#assets-dm-hybrid-6523}

##### Dynamic Media — 混合附加元件套件(AEM 6.5.23和更新版本)

從AEM 6.5 Service Pack 23開始，Dynamic Media — 混合模式提供新的附加元件套件。 此套件包含與Dynamic Media — 混合執行模式特別相容的`cq-scene7-imaging`套件。

**包含金鑰修正**

修正Dynamic Media — 混合部署中，`/conf/global/settings/dam/dm/imageserver`底下`catalog.expiration`引數的更新未反映在伺服器或作者URL上的問題，儘管復寫成功且沒有錯誤。 此更新可確保CRX/DE、伺服器回應和公開傳送URL之間的過期值一致。 這進而會改善快取行為以及影像轉換的可靠性。 (ASSETS-44837)

**重要考量**

* 基礎AEM 6.5.23 （和更新版本）安裝中的`cq-scene7-imaging`套件組合是&#x200B;*與Dynamic Media — 混合執行模式不相容*。
* 單獨安裝Service Pack 23 （和更新版本）不會&#x200B;*在針對Dynamic Media — 混合式（`-r dynamicmedia`執行模式）設定的AEM執行個體上自動更新*&#x200B;現有的`cq-scene7-imaging`套件。

**何時安裝混合附加元件套件**

* 從AEM 6.5.19或更早版本直接升級至AEM 6.5.23 （及更新版本）時。
* 當需要Dynamic Media — 混合功能的特定修正時。
* 直接從AEM 6.5 GA （一般可用性）部署新的Dynamic Media — 混合執行個體到Service Pack 23 （及更新版本）時。

**下載混合附加元件套件**

自2025年5月22日星期四起，混合附加元件套件將在Adobe Software Distribution上公開提供，並正式發行AEM 6.5.23。使用者可以在Software Distribution中搜尋&#x200B;**AEM 6.5 Dynamic Media混合式附加元件套件**，找到它。


<!--### [!DNL Forms]{#forms-6523}


#### Forms Designer 

* When a user exports the data for an XFA-based PDF using the exportDataAPI, the resulting XML shows discrepancies when compared with the XML data exported manually using Acrobat Reader. Values of some fields were missing in the output compared to the output generated from Acrobat Reader. (LC-3922791).  

* On AEM Forms 6.5.22.0, when a user attempts to generate a tagged PDF using the Output Service in Workbench, the resulting PDF contains an extra label tag under the reference tag in the table of content item. (LC-3922756) 

* When a user places field captions with bottom or right alignment in AEM Forms Designer, the tag tree includes only the caption without the corresponding value, leading to incomplete accessibility tagging. (LC-3922619). 

* On upgrading from AEM Forms 6.5 Service Pack 6 to AEM Forms Service Pack 20, the QR codes in generated PDFs become unreadable. The alternative text for the QR codes also fails accessibility testing, affecting screen reader compatibility. (LC-3922551). 

* When a user renders a letter in Agent UI on AEM Forms Service Pack 18, the content fails to display correctly due to the FormService.render() API. (LC-3922461). 

 

#### Forms

* When a user enables "Allow Rich Text for Title" on the root panel in an AEM Forms Adaptive Form, the "Exclude Title from Document of Record" setting on a nested panel incorrectly hides the root panel's title in the auto-generated Document of Record. (FORMS-19696). 

* When a user attempts to assign a custom sling:resourceType to a core component using the aem:afProperties in a JSON schema on an on-premise AEM 6.5 instance, the custom resource type is not applied. (FORMS-19691). 

* When a user submits an Adaptive Form with prefilled attachments using URIs, the form submission fails with a NullPointerException due to missing binary data. (FORMS-19371) (FORMS-19486). 

* When a user uploads a PDF under the 'Forms and Documents' section in AEM 6.5 Forms, the timeline feature stops functioning. (FORMS-19407)(FORMS-19234). 

* When a user uploads files using the out-of-the-box (OOTB) file attachment component in AEM Forms, security vulnerabilities are identified. This leads to potential interception of the submission process by unauthorized entities. (FORMS-19271). 

* When a user configures an out-of-the-box Adaptive Form in AEM Forms to automatically generate a Document of Record (DoR), the "Title" field in Acrobat Reader's Document Properties does not display the captured DoR title, and the form title does not appear by default in place of the filename. (FORMS-19263). 

* When a user opens an Interactive Communication in Agent UI, the prefilled data cannot be completely erased; upon removal, it automatically refills with the same data. (FORMS-19151). 

* When a user previews a date field in the Agent UI, the date unexpectedly changes due to time zone discrepancies between the VM's UTC setting and the system's interpretation of the date. (FORMS-19115). 

* When a user submits a form, file attachments may duplicate leading to multiple uploads of the same file. (FORMS-19045)(FORMS-19051). 

* Adding coordinators to policy sets in AEM 6.5 Document Security fails across both production and lower environments. (FORMS-18603, FORMS-18212, FORMS-19697). 

* When a user clicks the "datepicker-calendar-icon" in desktop mode with an empty field in AEM Forms Service Pack 22, an error occurs due to the undefined _$focusedDate variable, disrupting associated custom scripts. (FORMS-18483)(FORMS-18268). 

* On AEM Forms Service Pack 19 (6.5.19.0), when a customer previews a letter, the 'Amount in words' field fails to display or update number values incorrectly, leading to misalignment and missing spaces in the content. (FORMS-18437, FORMS-17330, FORMS-18209, FORMS-18557, CTG-4150848,FORMS-19614, LC-3922004) 

* When a customer previews a saved letter in AEM Forms 6.5 SP19 on RHEL, the content misaligns, spaces are missing, and unexpected characters like 'x' appear. (FORMS-18422)(FORMS-17641). 

* When a user navigates between tabs in AEM Forms, selecting components on the first tab becomes unresponsive. (FORMS-18345). 

* In AEM Forms 6.5.21.0, when a user converts an HTML file to PDF using the WebToPDF option, the output PDF is missing the header section, including metadata and title tags. (FORMS-18223, FORMS-17835, FORMS-19642, FORMS-18224). 

* In the AEM JEE Process Manager SDK, when a user invokes the retryAction(long actionOid) method, the system incorrectly retries the first action found in the tb_action_instance table. This occurs even when a specific action ID is provided or when the ID is null, resulting in unintended behavior. (FORMS-18187). 

* After updating to SP22, a user encounters issues where the save draft and submission functionalities fail without displaying any error message. (FORMS-18069). 

* In AEM 6.5.21.0, transitioning from XSD-based foundation components to core components prevents the implementation of cross-file references in JSON schemas, impacting Adaptive Forms migration. (FORMS-18065). 

* When a user previews a letter in the Agent UI, the date field shows an incorrect value due to IC time conversion issues. These discrepancies arise from time zone differences between the VM environment and the system's interpretation of time (UTC vs. local time). (FORMS-17988) (FORMS-17248). 

* When a user previews letters using Notice IC templates in AEM Forms, PDF generation times vary significantly, from 1.5 seconds to more than 10 seconds, even on the same server. This inconsistency affects business critical workflows. (FORMS-17951). 

* When a user binds a Scribble Signature object in an Adaptive Form to an XDP using the 'Data Sources' option, changes cannot be saved due to persistent aspect ratio validation errors, even when using valid values. (FORMS-17587). 

* When a user uses a specific XDP with many hidden fields for document fragments, AEM creates CRX nodes with the cm:optional property set to false, which causes the Interactive Communication (IC) submission to fail. (FORMS-17538). 

* On AEM Forms 6.5.19.0, when a customer previews a letter, the numeric box field fails to handle negative values correctly when digit limits for Lead and Frac are defined. This issue occurs due to the use of parseFloat, which treats the minus sign as part of the number. (FORMS-17451). 

* On AEM Forms 6.5, when a letter is previewed, the use of the "*" wildcard in the Adobe.json file is noticed, raising a concern about its purpose and potential modification (FORMS-17317). 

* When a user uses a screen reader on the "Apply for a Fixed Rate Saver joint account", the headings are incorrectly announced as 'clickable', causing accessibility issues. (FORMS-17038). 

* When a form is embedded, the generated iframe is missing a title attribute, leading to an accessibility compliance issue. (FORMS-17010). 

* It is not possible to download a form using the Forms Manager UI without including associated dependencies such as themes and fragments. (FORMS-15811). 

* When a user accesses the form on mobile devices (iOS and Android), the 'next' and 'previous' buttons on the first page are disabled, but the screen reader does not identify them as disabled. (FORMS-15773). 

* When a user saves a large form with fragments and lazy loading enabled, it fails to retrieve drafts, disrupting the workflow. (FORMS-19890, FORMS-19808). 

 

#### Forms JEE 

* When a user reconfigures the database in AEM Forms, the connection fails due to hardcoded parameters. (FORMS-19568, FORMS-17621) 

* When a user sets up AEM 6.5 with MySQL 8.4 using the partial turnkey method, the LiveCycle Configuration Manager (LCM) fails to recognize the required MySQL connector driver during the database connection test, causing the setup to fail. (FORMS-19442). 

* When a user runs LCM with JDBC 12.8.1 on JRE 11 in a JEE environment, the setup fails due to incompatibility issues.(FORMS-19276). 

* When a user opens a task in AEM On-Premise, the system executes the Workspace Start Action Profile instead of the AssignedUserProfile. (FORMS-19065). 

* When a user uses the retryAction(long actionOid) method in the AEM JEE Process Manager, unexpected behavior occurs. (FORMS-18357)(FORMS-18187). 

* On AEM Forms 6.5.21.0, the PDFG conversion fails with the error below: (FORMS-16851)(FORMS-14613).   
 
#### Forms Captcha {#forms-captcha-6523} 

* Improved reCAPTCHA alerting in Adaptive Forms by updating submit error codes to 400. Also, refined log alerts to distinguish between timeouts, expirations, and bot detection failures, enhancing troubleshooting accuracy and system observability. (FORMS-19240) 
* Closed an unclosed `ResourceResolver` instance in `ReCaptchaConfigurationServiceImpl` to prevent potential resource leaks and improve system stability when using reCAPTCHA integrations in AEM Forms. (FORMS-19242) 
* Improved CAPTCHA configuration handling for AEM Forms by ensuring the correct configuration binds to each form when multiple entries exist in the `/conf/global` folder. Prevents unintended use of incorrect CAPTCHA settings when the configuration container is not explicitly selected. (FORMS-19239)-->


<!--
#### XMLFM {#forms-xmlfm-6523}

* A () -->

<!--
#### [!DNL Adaptive Forms] {#adaptive-forms-6523}

* A () -->

<!--
#### [!DNL Forms Designer] {#forms-designer-6523}

* A () -->


### 基礎 {#foundation-6523}

* 修正Coral警示橫幅在升級至Service Pack 21後，文字顏色顯示為白色而非黑色的問題。 確保套用正確的樣式，以維持介面中警報訊息的正確對比和可讀性。 (NPR-42359)
* 在智慧標籤設定中新增OAuth整合支援，以符合JWT （JSON Web權杖）的淘汰。 使用更新後的驗證方法確保智慧標籤功能繼續正常運作。 (NPR-42296)

#### Apache Felix {#foundation-apachefelix-6523}

修正將私密金鑰檔案上傳至CRX中的二進位型別屬性欄位時發生的NullPointerException，還原透過Service Pack 16呈現的相容性。 在AEM Managed Services中啟用安全的金鑰檔案上傳工作流程，而不會發生伺服器錯誤或中斷憑證續約流程。 (CQ-4359178)


<!--
#### Campaign{#foundation-campaign-6523}

* A () -->

<!--
#### Cloud Services{#foundation-cloudservices-6523}

* A () -->

<!--
#### Communities {#foundation-communities-6523}

* A () -->

<!--
#### Content distribution{#foundation-content-distribution-6523}

* A () -->

<!--
#### CRX {#foundation-crx-6523}

* A () -->


#### Granite{#foundation-granite-6523}

* 解決Apache Sling指令碼服務之間的OSGi相依性週期，其在升級至Service Pack 21後載入HTML頁面時造成延遲或失敗。 更新內部服務參考，以消除涉及`SightlyScriptingEngineFactory`和相關元件的循環相依性，改善指令碼引擎的可靠性和啟動行為。 (GRANITE-56808)
* 更新JS使用Apache Sling中的指令碼僅隨選載入，而不是在啟動時急切載入，消除執行緒爭用並降低發佈伺服器在載入時無回應的風險。 此變更可防止早期指令碼解析所導致的資源鎖定，因此可在高流量狀況下改善伺服器穩定性和回應時間。 (GRANITE-56611)
* 修正了AEM Omnisearch中，輸入欄位的預留位置錯誤地顯示為標籤，導致視覺混淆的問題。 確保跨篩選器欄位正確顯示預留位置，並保持一致且可存取的表單行為。 (GRANITE-51791)
* 解決在內容片段模式編輯器中選取超過30個具有多欄位參考的CFM （內容片段模式）時觸發的伺服器錯誤。 已增強篩選建議元件，以支援POST作業。 此功能允許在內容片段建立期間正確處理大型參考集，並改善高容量模型設定的穩定性。 (GRANITE-57164)
* 解決CFM中按一下靠近核取方塊時無意間切換其狀態的問題。 更新樣式，將點選啟動嚴格限制在核取方塊元素內，避免使用者意外互動，並改善表單可用性與協助工具。 (GRANITE-52384)


<!--
#### Integrations{#foundation-integrations-6523}

* A () -->


#### Jetty{#foundation-jetty-6523}

解決SNI驗證針對使用具有自訂主機標頭的Dispatcher SSL設定的AEM客戶，封鎖透過HTTPS進行的API呼叫的問題。 引入可停用SNI驗證的選項，作為Jetty組態的一部分，啟用與特定反向Proxy設定（其中`mod_proxy`不可行）的相容性。 (NPR-42614)


<!--
#### Localization{#foundation-localization-6523}

* A () -->

<!--
#### Oak {#foundation-oak-6523}

* A () -->


#### Platform{#foundation-platform-6523}

* 修正不一致標籤合併行為，確保合併的標籤值在資產間一律正確顯示，無論標籤是內嵌建立還是透過標準標籤建立方法建立。 防止`EN:title`欄位的剩餘值覆寫合併的標籤顯示。 (CQ-4358812)
* 修正標籤編輯對話方塊中，標籤值中的&amp;字元重複編碼的問題。 避免在每次儲存時附加額外的「&amp;」實體，確保編輯間的標籤值保持乾淨一致，並避免編寫內容出現顯示錯誤。 (CQ-4359048)
* 解決在WebSphere®上執行的AEM 6.5中，防止在提交最適化表單時傳送電子郵件的`ClassCastException`錯誤。 此修正可確保`com.sun.mail.handlers.text_plain`與`java.activation.DataContentHandler`之間的相容性，並與WebSphere®環境預期的郵件處理常式組態保持一致，以啟用成功的電子郵件傳輸。 (NPR-42500)
* 改善封裝管理員中的錯誤處理，方法是確保AEM在安裝失敗且錯誤回應為空時，顯示清楚的訊息。 此修正可防止無訊息失敗，並有助於在套件部署期間更快速地偵錯。 (NPR-42375)

<!--
#### Security{#foundation-security-6523}

* A -->

<!--
#### Sling{#foundation-sling-6523}

* A () -->


#### 翻譯{#foundation-translation-6523}

修正使用&#x200B;**更新語言副本**&#x200B;更新工作流程中的內容片段時觸發的NullPointerException (NPE)問題。 此修正可確保工作流程在編輯與翻譯參考繫結的內容時，不會進入失敗狀態或停滯在執行狀態。 (NPR-42115)

#### 使用者介面{#foundation-ui-6523}

將遺失的`title`屬性新增至Coral UI對話方塊按鈕，例如元件編輯對話方塊中的&#x200B;**Done**&#x200B;和&#x200B;**Cancel**，以改善協助工具並啟用自動驗證。 確保按鈕在標籤呈現中保留預期的屬性，以防止基於Selenium的UI測試失敗。 (NPR-42412)

#### WCM{#foundation-wcm-6523}

修正在具有Service Pack 19或更新版本的環境中使用&#x200B;**更新語言副本**&#x200B;時，無法新增頁面至翻譯工作的問題。 確保翻譯工作流程如預期般進行，以啟用語言副本之間的適當頁面轉移，無需手動干預。 (CQ-4357929)

#### 工作流程{#foundation-workflow-6523}

解決`EmailNotificationServiceProcessor`中`getSegmentId`方法在Hotfix部署後傳回`null`，導致電子郵件觸發程式在工作流程處理期間失敗的問題。 透過確保處理器擷取所需的`SegmentInfo`值，以支援跨AEM執行個體的電子郵件通知工作流程，藉此還原正確的區段ID解析邏輯。 (CQ-4359755)


## 安裝[!DNL Experience Manager] 6.5.23.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.23.0需要[!DNL Experience Manager] 6.5。如需詳細指示，請參閱[升級檔案](/help/sites-deploying/upgrade.md)。<!-- UPDATE FOR EACH NEW RELEASE -->
* Service Pack下載專案可在Adobe [軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip)上取得。
* 在具有MongoDB和多個執行個體的部署上，使用封裝管理員在其中一個作者執行個體上安裝[!DNL Experience Manager] 6.5.23.0。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe不建議您移除或解除安裝[!DNL Experience Manager] 6.5.23.0套件。 因此，在安裝套件之前，您應該建立`crx-repository`的備份，以備您必須復原它時使用。<!-- UPDATE FOR EACH NEW RELEASE -->

<!-- FORMS For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->

### 在[!DNL Experience Manager] 6.5上安裝Service Pack{#install-service-pack}

1. 如果執行個體處於更新模式（從舊版更新執行個體時），請在安裝前重新啟動執行個體。 如果執行個體的目前運作時間很高，Adobe建議重新啟動。

1. 安裝之前，請為您的[!DNL Experience Manager]執行個體建立快照或全新備份。

1. 從[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip)下載Service Sack。<!-- UPDATE FOR EACH NEW RELEASE -->

1. 開啟封裝管理員，然後選取&#x200B;**[!UICONTROL 上傳封裝]**&#x200B;以上傳封裝。 如需詳細資訊，請參閱[封裝管理員](/help/sites-administering/package-manager.md)。

1. 選取封裝，然後選取&#x200B;**[!UICONTROL 安裝]**。

1. 若要更新S3聯結器，請在安裝Service Pack後停止執行個體，將現有聯結器取代為安裝資料夾中提供的新二進位檔案，然後重新啟動執行個體。 請參閱[Amazon S3資料存放區](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)。

>[!NOTE]
>
>Service Pack安裝期間，Package Manager UI上的對話方塊有時會退出。 Adobe建議您先等待錯誤記錄穩定下來，再存取部署。 等待與更新程式套件組合解除安裝相關的特定記錄，再確認安裝成功。 此問題通常發生在[!DNL Safari]瀏覽器中，但可能間歇性地發生在任何瀏覽器中。

**自動安裝**

您可以使用兩種不同的方法來安裝[!DNL Experience Manager] 6.5.23.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* 伺服器上線時，請將封裝放入`../crx-quickstart/install`資料夾。 套件會自動安裝。
* 使用封裝管理員](/help/sites-administering/package-manager.md#package-share)的[HTTP API。 使用`cmd=install&recursive=true`安裝巢狀套件。

>[!NOTE]
>
>Experience Manager 6.5.23.0不支援Bootstrap安裝。<!-- UPDATE FOR EACH NEW RELEASE -->

**驗證安裝**

若要瞭解經過認證可搭配此版本使用的平台，請參閱[技術需求](/help/sites-deploying/technical-requirements.md)。

1. 產品資訊頁(`/system/console/productinfo`)會在[!UICONTROL 已安裝產品]下顯示更新的版本字串`Adobe Experience Manager (6.5.23.0)`。<!-- UPDATE FOR EACH NEW RELEASE -->

1. 在OSGi主控台中，所有OSGi套件組合均為&#x200B;**[!UICONTROL 作用中]**&#x200B;或&#x200B;**[!UICONTROL 片段]** （使用Web主控台： `/system/console/bundles`）。

1. OSGi套件`org.apache.jackrabbit.oak-core`是1.22.20或更新版本（使用Web主控台： `/system/console/bundles`）。<!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE. CHECK WITH SAMEER DHAWAN -->

### 安裝[!DNL Experience Manager] Forms的Service Pack{#install-aem-forms-add-on-package}

如需在Experience Manager Forms上安裝Service Pack的說明，請參閱[Experience Manager Forms Service Pack安裝說明](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)。

>[!NOTE]
>
>調適型表單功能 (適用於 [AEM 6.5 QuickStart](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/implementing/deploying/deploying/deploy)) 僅用於探索和評估目的。若要供生產使用，必須獲得 AEM Forms 的有效許可；調適型表單的功能需要適當許可才可使用。

### 安裝適用於Experience Manager內容片段的GraphQL索引套件{#install-aem-graphql-index-add-on-package}

使用GraphQL的客戶必須安裝[Experience Manager內容片段搭配GraphQL索引套件1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip)。

如此一來，您就可以根據使用者實際使用的功能，新增必要的索引定義。

無法安裝此套件可能會導致GraphQL查詢變慢或失敗。

>[!NOTE]
>
>每個執行個體僅安裝此套件一次；不需要隨每個Service Pack重新安裝。

### UberJar{#uber-jar}

[!DNL Experience Manager] 6.5.23.0的UberJar可在[Maven中央存放庫](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.22/)中使用。<!-- CHECK FOR UPDATE EACH NEW RELEASE -->

若要在Maven專案中使用UberJar，請參閱[如何使用UberJar](/help/sites-developing/ht-projects-maven.md)，並在您的專案POM中包含下列相依性： <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.23</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar和其他相關成品可在Maven中央存放庫上使用，而不是Adobe公共Maven存放庫(`repo.adobe.com`)。 主要UberJar檔案已重新命名為`uber-jar-<version>.jar`。 因此，`dependency`標籤沒有`classifier`，其值為`apis`。



## 過時和移除的功能{#removed-deprecated-features}

如需AEM 6.5已棄用或移除之所有功能的詳細清單，請參閱[已棄用和移除的功能](/help/release-notes/deprecated-removed-features.md/)。

### SPA 編輯器 {#spa-editor}

[從AEM 6.5版本6.5.23開始的新專案已棄用SPA編輯器](/help/sites-developing/spa-overview.md)。SPA Editor仍支援現有專案，但不應用於新專案。

目前，AEM 中用於管理 Headless 內容的首選編輯器為：

* [通用編輯器](/help/sites-developing/universal-editor/introduction.md)，用於視覺化編輯。
* [內容片段編輯器](/help/sites-developing/universal-editor/introduction.md)，用於表單型編輯。

## 已知問題{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

* **AEM 6.5.21-6.5.23和AEM 6.5 LTS GA中的JSP指令碼套件組合問題**
AEM 6.5.21、6.5.22、6.5.23和AEM 6.5 LTS GA隨附`org.apache.sling.scripting.jsp:2.6.0`套件，其中包含已知問題。 AEM執行個體處理許多並行請求時，高負載下通常會發生問題。

  發生此問題時，下列其中一個例外可能會與對`org.apache.sling.scripting.jsp:2.6.0`的參考一起出現在錯誤記錄中：

   * `java.io.IOException: classFile.delete() failed`
   * `java.io.IOException: tmpFile.renameTo(classFile) failed`
   * `java.lang.ArrayIndexOutOfBoundsException: Index 0 out of bounds for length 0`
   * `java.io.FileNotFoundException`

  發生此錯誤時，唯一的復原方法是重新啟動AEM執行個體。

  請聯絡Adobe客戶支援，並參閱此版本注意事項以尋求解決方案。

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

   1. 從`crx-quickstart/repository/`中刪除以下兩個資料夾

      * `cache`
      * `diff-cache`

   1. 安裝Service Pack，或重新啟動Experience Manager as a Cloud Service。
`cache`和`diff-cache`的新資料夾會自動建立，而您在`error.log`中不會再遇到與`mvstore`相關的例外狀況。

* 更新可能已使用您內容模型的自訂API名稱的GraphQL查詢，以改用內容模型的預設名稱。

* GraphQL查詢可以使用`damAssetLucene`索引，而不是`fragments`索引。 此動作可能會導致GraphQL查詢失敗或需要很長時間才能執行。

  若要修正問題，`damAssetLucene`必須設定為在`/indexRules/dam:Asset/properties`下包含下列兩個屬性：

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

  在變更索引定義之後，需要重新索引(`reindex` = `true`)。

  執行這些步驟後，GraphQL查詢應該可以更快執行。

* 嘗試移動、刪除或發佈內容片段、網站或頁面時，在擷取內容片段參考時出現問題。 背景查詢失敗。 也就是說，功能無法運作。
若要確保作業正確，您必須將下列屬性新增至索引定義節點`/oak:index/damAssetLucene` （不需要重新索引）：

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* 如果您將[!DNL Experience Manager]執行個體從6.5.0 - 6.5.4升級至Java™ 11上的最新Service Pack，您會在`error.log`檔案中看到`RRD4JReporter`例外狀況。 若要停止例外狀況，請重新啟動[!DNL Experience Manager]的執行個體。<!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* 使用者可以在[!DNL Assets]中重新命名階層中的資料夾，並將巢狀資料夾發佈至[!DNL Brand Portal]。 但是，在重新發佈根資料夾之前，[!DNL Brand Portal]中的資料夾標題不會更新。

* 安裝[!DNL Experience Manager] 6.5.x.x期間可能會顯示下列錯誤和警告訊息：
   * 「當使用Adobe Target API （IMS驗證）在[!DNL Experience Manager]中設定Target Standard整合時，將體驗片段匯出至Target會導致建立錯誤的選件型別。 Target會建立多個型別為「HTML」/來源「Adobe Target Classic」的選件，而非「體驗片段」/來源「Adobe Experience Manager」型別。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在`granite/operations/maintenance`找不到維護期間。
   * 使用彙總函式(例如SUM、MAX和MIN)時，Adaptive Form伺服器端驗證會失敗(CQ-4274424)。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` ：在`granite/operations/maintenance`找不到維護期間。
   * 透過Shoppable Banner檢視器預覽資產時，Dynamic Media互動式影像中的熱點不可見。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` ：等待登入變更完成解除登入逾時。

* 從AEM 6.5.15開始，```org.apache.servicemix.bundles.rhino```套件提供的Rhino JavaScript Engine有新的提升行為。 使用嚴格模式(```use strict;```)的指令碼必須宣告其正確的變數。 否則，它們不會執行，並最終擲回執行階段錯誤。

* 透過正式更新套件安裝標籤相關的現成可用內容會將`/content/cq:tags`節點的languages屬性重設為預設值。 此動作適用於Service Pack、Security Service Pack、Extended Feature Pack、Cumulative Feature Pack、修補程式等。 因此，在安裝之前，必須從屬性新增它。

### AEM Sites的已知問題 {#known-issues-aem-sites-6523}

內容片段 — 預覽失敗，因為大型片段樹受到DoS保護。 請參閱有關預設GraphQL查詢執行器組態選項](https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-23945)的[KB文章(SITES-17934)

<!--### Known issues for AEM Forms {#known-issues-aem-forms-6523}

* When a customer upgrades from Struts 2.x to 6.x, stricter type checking can cause silent failures—especially when checkbox components return false and are bound to a List *Integer*. This value mismatch must be handled explicitly to avoid deserialization errors.

* If the HTML to PDF conversion fails on a SUSE&reg; Linux&reg; (SLES 15 SP6 onwards) server with the following error:
  
  ```Auto configuration failed 4143511872:error:0E079065:configuration file routines:DEF_LOAD_BIO:missing equal sign:conf_def.c:362:line 57```
  then set the following environment variable and restart the server:
    `OPENSSL_CONF=/etc/ssl`

* After installing AEM Forms JEE Service Pack 21 (6.5.21.0), if you find duplicate entries of Geode jars `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)` under the `<AEM_Forms_Installation>/lib/caching/lib` folder (FORMS-14926), perform the following steps to resolve the issue:

  1. Stop the locators, if they are running.
  1. Stop the AEM Server. 
  1. Go to the `<AEM_Forms_Installation>/lib/caching/lib`. 
  1. Remove all the Geode patch files except `geode-*-1.15.1.2.jar`. Confirm that only the Geode jars with `version 1.15.1.2` are present.
  1. Open the command prompt in administrator mode.  
  1. Install the Geode patch using the `geode-*-1.15.1.2.jar` file. 

* If a user tries to preview a draft letter with saved XML data, it gets stuck in `Loading` state for some specific letters. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (FORMS-14521)
  
* After upgrading to AEM Forms Service Pack 6.5.21.0, the `PaperCapture` service fails to perform OCR (Optical Character Recognition) operations on PDFs. The service does not generate output in the form of a PDF or a log file. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (CQDOC-21680)

* When users upgraded from AEM 6.5 Forms Service Pack 18 or 19 to Service Pack 20 or 21, they encountered a JSP compilation error. This error prevented them from opening or creating adaptive forms. It also caused issues with other AEM interfaces. Those interfaces included the Page Editor, AEM Forms UI, Workflow editor, and System Overview UI. (FORMS-15256)

  If you face such an issue, perform the following steps to resolve it:
    1. Navigate to the directory `/libs/fd/aemforms/install/` in CRXDE.
    1. Delete the bundle with the name `com.adobe.granite.ui.commons-5.10.26.jar`.
    1. Restart your AEM Server.

* After updating to AEM Forms Service Pack 20 (6.5.20.0) with the Forms Add-On, configurations relying on the legacy Adobe Analytics Cloud Service using credential-based authentication stop working. This issue prevented analytics rules from executing correctly. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (FORMS-15428)

* When a user updates to AEM Forms Service Pack 20 (6.5.20.0) on the JEE server and generates PDFs using output services, the PDFs render with accessibility issues. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (LC-3922112)
* When a user generates Tagged PDFs using the output service on JEE, it shows "Inappropriate structure warning." To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (LC-3922038)
* When a form is submitted on AEM Forms JEE, the instances of a repeating XML element are removed from the data. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (LC-3922017)
* When a user in a Linux&reg; environment renders an Adaptive Form (on JEE) in HTML, it fails to render properly. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (LC-3921957)
* When a user converts an XTG file to PostScript format using the Output Service on AEM Forms JEE, it fails with the error: `AEM_OUT_001_003: Unexpected Exception: PAExecute Failure: XFA_RENDER_FAILURE`. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (LC-3921720)
* After upgrading to AEM Forms Service Pack 18 (6.5.18.0) on JEE server, when a user submits a form, it fails to render HTML5 or PDF Forms and XMLFM crashes. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (LC-3921718)
* In the Print Preview of the Interactive Communications Agent UI, the currency symbol (such as the dollar sign $) is inconsistently displayed for all field values. It appears for values up to 999 but is missing for values of 1000 and above. (FORMS-16557)
* Any modifications to nested layout fragments' XDP in an Interactive Communication are not reflected in the IC editor. (FORMS-16575)
* In the Print Preview of the Interactive Communications Agent UI, some calculated values are not displayed correctly. (FORMS-16603)
* When the letter is viewed in Print Preview, the content is changed. That is, some spaces disappear, and certain letters are replaced with `x`. (FORMS-15681)
* When a user configures a WebLogic 14c instance, the PDFG service in AEM Forms Service Pack 21 (6.5.21.0) on JEE running on JBoss&reg; fails due to classloader conflicts involving the SLF4J library. The error is displayed as follows (CQDOC-22178):
  
    ```java
    Caused by: java.lang.LinkageError: loader constraint violation: when resolving method "org.slf4j.impl.StaticLoggerBinder.getLoggerFactory()Lorg/slf4j/ILoggerFactory;"
    the class loader org.ungoverned.moduleloader.ModuleClassLoader @404a2f79 (instance of org.ungoverned.moduleloader.ModuleClassLoader, child of 'deployment.adobe-livecycle-jboss.ear'
    @7e313f80 org.jboss.modules.ModuleClassLoader) of the current class, org/slf4j/LoggerFactory, and the class loader 'org.slf4j.impl@1.1.0.Final-redhat-00001' @506ab52
    (instance of org.jboss.modules.ModuleClassLoader, child of 'app' jdk.internal.loader.ClassLoaders$AppClassLoader) for the method's defining class, org/slf4j/impl/StaticLoggerBinder,
    have different Class objects for the type org/slf4j/ILoggerFactory used in the signature-->

## 包含的OSGi套件組合和內容套件{#osgi-bundles-and-content-packages-included}

下列文字檔案列出此[!DNL Experience Manager] 6.5 Service Pack發行版本中包含的OSGi套件組合和內容套件：

* [Experience Manager中包含的OSGi套件組合清單6.5.23.0](/help/release-notes/assets/65230-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager中包含的內容套件清單6.5.23.0](/help/release-notes/assets/65230-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 受限制的網站{#restricted-sites}

這些網站僅供客戶使用。 如果您是客戶且需要存取權，請聯絡您的Adobe客戶經理。

* [產品下載網址為licensing.adobe.com](https://licensing.adobe.com/)
* [連絡Adobe客戶支援](https://experienceleague.adobe.com/en/docs/customer-one/using/home)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 產品頁面](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5檔案](https://experienceleague.adobe.com/en/docs/experience-manager-65)
>* [訂閱Adobe優先產品更新](https://www.adobe.com/tw/subscription/priority-product-update.html)
