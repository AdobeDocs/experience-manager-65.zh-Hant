---
title: ' [!DNL Adobe Experience Manager] 6.5的發行說明'
description: 尋找 [!DNL Adobe Experience Manager] 6.5的版本資訊、新增功能、安裝操作說明和詳細變更清單。
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: 3f64cfa688ef1f0090b7ce0d821324593cbea693
workflow-type: tm+mt
source-wordcount: '6707'
ht-degree: 1%

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

[!DNL Experience Manager] 6.5.23.0包含新功能、客戶要求的重要增強功能和錯誤修正。 此外，還包含自2019年4月6.5首次推出以來的效能、穩定性和安全性改善專案。 在[ 6.5上](#install)安裝此Service Pack[!DNL Experience Manager]。

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

   * IBM® Content Manager Client 8.7

   * MongoDB Enterprise 7.0

   * MySQL 8.4

   * Microsoft® SQL Server 2022

   * Microsoft® SQL Server JDBC驅動程式12.8

   * Red Hat® Enterprise Linux® 9 （核心4.x，64位元） 

* [強化的檔案附件元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment)：作為安全性測量，此元件現在會防止提交副檔名經過修改、嘗試略過允許的檔案型別檢查的檔案。 提交期間會封鎖這類檔案，以確保僅接受有效的檔案型別。

* Forms-20533、FORMS-20532： AEM Forms現在包含從2.5.33升級至6.x的Struts版本。已透過[Hotfix](/help/release-notes/aem-forms-hotfix.md)新增支援，您可以[下載並安裝](/help/release-notes/aem-forms-hotfix.md)以新增對最新版本Struts的支援。

* **LC-3922769**：某些AEM Forms功能現在需要OpenSSL 3才能正常運作。 系統必須安裝OpenSSL 3以及資料庫`libcrypto.so.3`和`libssl.so.3`。 由於安全性更新僅在具有OpenSSL 3.0.14的版本中提供，且SafeLogic支援將於2025年2月結束，因此我們已移除bsafe，現在使用OpenSSL 3來符合安全性規範。 如需平台相容性和詳細需求，請參閱[JEE上的AEM Forms支援平台](/help/forms/using/aem-forms-jee-supported-platforms.md)和[技術需求](/help/sites-deploying/technical-requirements.md)。

  **驗證OpenSSL 3安裝：**

   * **RHEL/CentOS/Fedora型系統**： `rpm -qa | grep   openssl3`
   * **Ubuntu/Debian型系統**： `dpkg -l | grep openssl3`
   * **替代驗證**： `ldd /path/to/XMLForm |   grep -E 'libcrypto.so.3|libssl.so.3'` （如果程式庫位於LD_LIBRARY_PATH）





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

* AEM編輯器頁面中的畫布區段現在支援完整的鍵盤協助工具。 使用者可以僅使用鍵盤啟動區段標題和編輯按鈕，而不需依賴滑鼠懸停。 此更新確保符合WCAG 2.1.1，並改善跨元件（例如Teaser、影像、輪播、版面、時間扭曲和註解模組）的可用性。 (SITES-25256) <!-- 6.5 LTS SP1 -->
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
* 改進重排情境中圖示的可見度和工具提示。 已增強重排行為，以確保工具提示可正確顯示給&#x200B;**下載**、**重新處理資產**&#x200B;和&#x200B;**簽出**&#x200B;圖示。 著重於在檢視區調整大小或瀏覽器縮放設定變更時，圖示及其標籤會變成隱藏的協助工具問題。 此修正可透過維護可見度並在Reflow期間提供適當的圖示說明，支援視力缺佳的使用者。 (SITES-26871)

#### 管理員使用者介面{#sites-adminui-6523}

修正Universal Editor URL服務例外狀況，遺失Externalizer端點。 Universal Editor URL服務現在可處理遺漏的作者、發佈或本機外部化程式端點，而不會擲回例外狀況。 即使部分外部器設定不完整，管理員使用者也可以成功開啟頁面編輯器。 (SITES-28877) <!-- LTS -->

#### 傳統 UI{#sites-classicui-6523}

* 傳統UI對話方塊中的問題，其中切換按鈕會隱藏文字區域，且無法於後續點按時再次顯示。 此修正可確保在切換時文字區域正確地重新顯示，恢復預期行為並防止動態對話方塊工作流程中斷。 (SITES-30230)
* 修正Service Pack 22升級後Classic UI影像資產尋找器功能中斷的問題。 Classic UI影像資產尋找器現在可以正確處理包含空格或特殊字元的資產名稱。 此更新可確保資產尋找器可正確編碼檔案名稱、避免搜尋失敗，並允許作者找到並選取影像資產，而不會發生錯誤。 (SITES-29151)

#### [!DNL Content Fragments]{#sites-contentfragments-6523}

* 修正`DeleteVariationIT.testUpdateBasic`的驗證測試失敗。 `DeleteVariationIT.testUpdateBasic`測試在Service Pack驗證執行期間不再失敗。 此修正修正修正了JSON處理邏輯中缺少文字對應的問題，確保測試穩定性並避免不必要的測試中斷。 (SITES-28022)
* AEM現在可以防止影像資產中XMP中繼資料的格式錯誤導致效能降低。 Assets如果包含無效或不相容的XMP屬性名稱（例如具有數值區段或不合格結構的名稱），在處理期間將不再觸發重複的警告記錄。 系統會篩選掉有問題的中繼資料，以確保資產擷取和驗證完整無誤。 (SITES-30683) <!-- AEM 6.5 LTS SP1 -->


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
* 若要確保相容性並支援SAML處理常式，您必須設定`service.ranking`屬性，讓`Query Token Auth`處理常式在&#x200B;**&#x200B;處理常式之前`SAML Auth`執行。 (SITES-29684)

### [!DNL Assets]{#assets-6523}

* 選取[!DNL AEM]Assets6.5.22.0Assets![、瀏覽至](/help/assets/assets/Smock_Asset_18_N.svg)**[!UICONTROL 搜尋Adobe Stock &#x200B;]**&#x200B;資料夾並選取庫存影像後，**[!UICONTROL &#x200B;內部部署(]**)導覽頁面中會發生下列問題：
   * 選取的stock影像無法授權並儲存為按一下「**[!UICONTROL 授權並儲存]**」會顯示空白的下拉式清單。
   * 選取Stock影像或重新進入庫存頁面URL會重新導向至[!DNL AEM]首頁，導致無法存取Adobe Stock影像。 (ASSETS-48687)
* 如果資料夾名稱在`/`內部部署([!DNL AEM])導覽頁面上的名稱包含6.5.22.0，則管理資料夾時發生問題。 (ASSETS-46740)
* 在[!DNL AEM] 6.5上，由於記憶體使用量高，資產詳細資訊頁面未從![集合](/help/assets/assets/Smock_Collection_18_N.svg)**[!UICONTROL 集合&#x200B;]**&#x200B;檢視載入。 (ASSETS-46738)
* [!DNL InDesign]的整合問題為`Day CQ DAM Mime Type OSGI`服務錯誤將[!DNL InDesign]個檔案識別為`x-adobe-indesign`而非`x-indesign`。 (ASSETS-45953)
* [!DNL AEM 6.5.21]工作階段洩漏追蹤至現成可用的&#x200B;**[!UICONTROL 已排程發佈至Brand Portal]**&#x200B;工作流程步驟。 (ASSETS-44104)
* 處理和發佈影像時，**[!UICONTROL 中顯示]**&#x200B;記憶體不足(OOM) [!DNL AEM]錯誤。 此問題是因為工作流程中已棄用的方法，例如&#x200B;**[!DNL Dam Asset update]**&#x200B;和&#x200B;**[!DNL Dynamic Media: Reprocess assets]**。 (ASSETS-43343)
* 進行微幅變更後（例如更新標題），您會重新開啟並重新儲存本機Sites執行個體上的&#x200B;**[!DNL Connected Assets configuration]**。 然後，遠端執行個體會失去與本機執行個體的連線。 因此，它無法與本機Sites執行個體建立通訊。 (ASSETS-44484)
* 在[!DNL AEM 6.5.21]中，當清單檢視中的資產上傳被取消並執行第二次上傳時，[!DNL AEM]會顯示已上傳的&#x200B;**[!UICONTROL 0個NaN資產]**&#x200B;錯誤。 (ASSETS-44124)

#### [!DNL Dynamic Media]{#assets-dm-6523}

已將中繼資料屬性(`jcr:content/metadata/dam:scene7SmartCropStatus`)新增至資產，以識別失敗的智慧型裁切層代。 透過手動或自動化工作流程，有效率地搜尋、篩選及重新處理具有智慧型裁切問題的資產。 (ASSETS-46237)

#### [!DNL Dynamic Media] — 混合模式 {#assets-dm-hybrid-6523}

##### Dynamic Media — 混合附加元件套件(AEM 6.5.23和更新版本)

從AEM 6.5 Service Pack 23開始，Dynamic Media — 混合模式提供新的附加元件套件。 此套件包含與Dynamic Media — 混合執行模式特別相容的`cq-scene7-imaging`套件。

**包含金鑰修正**

修正Dynamic Media — 混合部署中，`catalog.expiration`底下`/conf/global/settings/dam/dm/imageserver`引數的更新未反映在伺服器或作者URL上的問題，儘管復寫成功且沒有錯誤。 此更新可確保CRX/DE、伺服器回應和公開傳送URL之間的過期值一致。 這進而會改善快取行為以及影像轉換的可靠性。 (ASSETS-44837)

**重要考量**

* 基礎AEM 6.5.23 （和更新版本）安裝中的`cq-scene7-imaging`套件組合是&#x200B;*與Dynamic Media — 混合執行模式不相容*。
* 單獨安裝Service Pack 23 （和更新版本）不會&#x200B;*在針對Dynamic Media — 混合式（*&#x200B;執行模式）設定的AEM執行個體上自動更新`cq-scene7-imaging`現有的`-r dynamicmedia`套件。

**何時安裝混合附加元件套件**

* 從AEM 6.5.19或更早版本直接升級至AEM 6.5.23 （及更新版本）時。
* 當需要Dynamic Media — 混合功能的特定修正時。
* 直接從AEM 6.5 GA （一般可用性）部署新的Dynamic Media — 混合執行個體到Service Pack 23 （及更新版本）時。

**下載混合附加元件套件**

自2025年5月22日星期四起，混合附加元件套件將在Adobe Software Distribution上公開提供，並正式發行AEM 6.5.23。使用者可以在Software Distribution中搜尋&#x200B;**AEM 6.5 Dynamic Media混合式附加元件套件**，找到它。


### [!DNL Forms]{#forms-6523}

#### Forms Designer

* 當使用者使用exportDataAPI匯出以XFA為基礎的PDF的資料時，產生的XML與使用Acrobat Reader手動匯出的XML資料相比，會顯示差異。 與Acrobat Reader產生的輸出相比，輸出中缺少某些欄位的值。 (LC-3922791)

* 在AEM Forms 6.5.22.0中，使用Workbench中的輸出服務產生已標籤PDF會在目錄專案的參考標籤下新增非預期的標籤標籤。 (LC-3922756)

* 當使用者在AEM Forms Designer中以底部或右側對齊方式放置欄位註解時，標籤樹僅包含註解而沒有對應的值，導致不完整的協助工具標籤。 (LC-3922619)

* 從AEM Forms 6.5 Service Pack 6升級至AEM Forms Service Pack 20時，所產生PDF中的二維碼變得無法讀取。 QR碼的替代文字也未能通過協助工具測試，影響熒幕助讀程式的相容性。 (LC-3922551)

* 當使用者在AEM Forms Service Pack 18上的代理程式UI中轉譯信函時，由於FormService.render() API，內容無法正確顯示。 (LC-3922461)

#### Forms

* 在AEM Forms中，在根面板上啟用「允許標題為RTF文字」會導致巢狀面板上的「從記錄檔案排除標題」無法正確地隱藏根面板的標題。 這會在產生的記錄檔案中進行。 (FORMS-19696)

* 在AEM 6.5上的JSON結構描述中，系統會忽略透過`sling:resourceType`指派的自訂`aem:afProperties`。呈現期間會忽略自訂資源型別。 (FORMS-19691)

* 當使用者提交具有使用URI預填附件的調適型表單時，由於缺少二進位資料，表單提交會失敗並出現NullPointerException。 (FORMS-19371) (FORMS-19486)

* 當使用者在PDF 6.5 Forms的「Forms和檔案」區段下傳AEM時，時間軸功能停止運作。 (FORMS-19407)(FORMS-19234)

* 當使用者使用AEM Forms中的現成(OOTB)檔案附件元件上傳檔案時，會識別安全漏洞。 此問題可能會導致未經授權的實體攔截提交流程。 (FORMS-19271)

* 當使用者在AEM Forms中設定現成的最適化表單以自動產生記錄檔案(DoR)時，Acrobat Reader檔案屬性中的「標題」欄位不顯示擷取的DoR標題。 依預設，表單標題不會出現在檔案名稱的位置。 (FORMS-19263)

* 當使用者在代理程式UI中開啟互動式通訊時，預先填入的資料無法完全清除；移除後，它會自動以相同的資料重新填入。 (FORMS-19151)

* 當使用者在代理UI中預覽日期欄位時，日期意外變化。 此問題發生的原因是VM的UTC設定與系統對日期的詮釋之間存在時區差異。 (FORMS-19115)

* 使用者提交表單時，檔案附件可能會重複，導致同一檔案多次上傳。 (FORMS-19045)(FORMS-19051)

* 在AEM 6.5 Document Security中，將協調員新增至原則集會在生產環境和較低環境中失敗。 (FORMS-18603、FORMS-18212、FORMS-19697)

* 當使用者在案頭模式中按一下AEM Forms Service Pack 22中具有空白欄位的「datepicker-calendar-icon」時，由於未定義的_$focusedDate變數而發生錯誤，並中斷相關的自訂指令碼。 (FORMS-18483)(FORMS-18268)

* 在AEM Forms Service Pack 19 (6.5.19.0)上，當客戶預覽信函時，「字數金額」欄位無法正確顯示或更新數字值，導致內容不對齊並遺失空格。 (FORMS-18437、FORMS-17330、FORMS-18209、FORMS-18557、CTG-4150848、FORMS-19614、LC-3922004)

* 當客戶在RHEL上預覽在AEM Forms 6.5 SP19中儲存的字母時，內容未妥善對齊、缺少空格，且出現非預期字元，如「x」。 (FORMS-18422)(FORMS-17641)

* 當使用者在AEM Forms中的標籤之間導覽時，在第一個標籤上選取元件會變得無回應。 (FORMS-18345)

* 在AEM Forms 6.5.21.0中，當使用者使用WebToPDF選項將HTML檔案轉換為PDF時，輸出PDF缺少標題區段，包括中繼資料和標題標籤。 (FORMS-18223、FORMS-17835、FORMS-19642、FORMS-18224)

* 在AEM JEE Process Manager SDK中，當使用者叫用retryAction(long actionOid)方法時，系統會錯誤地重試tb_action_instance表格中的第一個動作。 即使提供特定動作ID或ID為空值，也會發生此工作流程，導致非預期的行為。 (FORMS-18187)

* 更新至SP22後，使用者遇到問題，即儲存的草稿和提交功能失敗，未顯示任何錯誤訊息。 (FORMS-18069)

* 在AEM 6.5.21.0中，從XSD式基礎元件轉換至核心元件，會使無法在JSON結構描述中實作跨檔案參照，進而影響最適化Forms移轉。 (FORMS-18065)

* 當使用者在代理UI中預覽信函時，由於IC時間轉換問題，日期欄位顯示不正確的值。 這些差異是由於VM環境與系統對時間的詮釋（UTC與當地時間）之間的時區差異所造成。 (FORMS-17988) (FORMS-17248)

* 當使用者在AEM Forms中使用通知IC範本預覽信函時，PDF的產生時間差異顯著，從1.5秒到超過10秒，即使在同一部伺服器上也是如此。 這種不一致會影響關鍵業務工作流程。 (FORMS-17951)

* 當使用者使用「資料來源」選項將調適型表單中的手寫簽名物件繫結到XDP時，無法儲存變更。 原因是持續外觀比例驗證錯誤，即使使用有效值亦然。 (FORMS-17587)

* 當使用者使用具有許多隱藏欄位的特定XDP作為檔案片段時，AEM會建立CRX節點並將`cm:optional`屬性設定為false，這會造成互動式通訊(IC)提交失敗。 (FORMS-17538)

* 在AEM Forms 6.5.19.0上，當客戶預覽信函時，若已定義潛在客戶與片段的數位限制，數值方塊欄位將無法正確處理負值。 此問題是因為使用parseFloat而發生，這會將減號視為數字的一部分。 (FORMS-17451)

* 在AEM Forms 6.5上，預覽信函時，注意到Adobe.json檔案中使用「*」萬用字元，令人擔心其用途和可能的修改。 (FORMS-17317)

* 當使用者在`Apply for a Fixed Rate Saver joint account`上使用熒幕助讀程式時，標題錯誤地宣告為`clickable`，導致協助工具問題。 (FORMS-17038)

* 內嵌表單時，產生的iframe會遺失title屬性，導致協助工具相容問題。 (FORMS-17010)

* 使用Forms Manager UI下載表單一律包含關聯的相依性，例如主題和片段。 (FORMS-15811)

* 當使用者存取行動裝置上的表單(iOS和Android™)時，第一個頁面上的「下一個」和「上一個」按鈕會停用。 不過，熒幕助讀程式不會將其識別為停用。 (FORMS-15773)

* 當使用者儲存已啟用片段和延遲載入的大型表單時，將無法擷取草稿，並中斷工作流程。 (FORMS-19890， FORMS-19808)

#### FORMS JEE

* 當使用者在AEM Forms中重新設定資料庫時，連線會因硬式編碼引數而失敗。 (FORMS-19568， FORMS-17621)

* 當使用者使用partial turnkey方法設定AEM 6.5與MySQL 8.4時，LiveCycle Configuration Manager (LCM)無法辨識所需的MySQL聯結器驅動程式。 這會導致資料庫連線測試和設定失敗。 (FORMS-19442)

* 當使用者在JEE環境中的JRE 11上執行具有JDBC 12.8.1的LCM時，設定會因不相容問題而失敗。 (FORMS-19276)

* 當使用者在AEM內部部署中開啟任務時，系統會執行Workspace開始動作設定檔，而不是AssignedUserProfile。 (FORMS-19065)

* 當使用者在AEM JEE流程管理員中使用retryAction(long actionOid)方法時，會發生非預期的行為。 (FORMS-18357)(FORMS-18187)

* 在AEM Forms 6.5.21.0上，PDFG轉換因下列錯誤而失敗： (FORMS-16851)(FORMS-14613)

#### Forms驗證碼 {#forms-captcha-6523}

* 將提交錯誤代碼更新為400，改善調適型Forms中的reCAPTCHA警報。 此外，精細化記錄警報以區分逾時、過期和機器人偵測失敗，提高疑難排解精確度和系統可觀察性。 (FORMS-19240)
* 在AEM Forms中使用reCAPTCHA整合時，已關閉`ResourceResolver`中未關閉的`ReCaptchaConfigurationServiceImpl`執行個體，以防止潛在的資源洩漏並改善系統穩定性。 (FORMS-19242)
* 改善AEM Forms的驗證碼組態處理方式，確保當`/conf/global`資料夾中有多個專案時，每個表單都有正確的組態繫結。 避免在未明確選取組態容器時，意外使用不正確的驗證碼設定。 (FORMS-19239)

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
* 使用封裝管理員[的](/help/sites-administering/package-manager.md#package-share)HTTP API。 使用`cmd=install&recursive=true`安裝巢狀套件。

>[!NOTE]
>
>Experience Manager 6.5.23.0不支援Bootstrap安裝。<!-- UPDATE FOR EACH NEW RELEASE -->

**驗證安裝**

若要瞭解經過認證可搭配此版本使用的平台，請參閱[技術需求](/help/sites-deploying/technical-requirements.md)。

1. 產品資訊頁(`/system/console/productinfo`)會在`Adobe Experience Manager (6.5.23.0)`已安裝產品[!UICONTROL 下顯示更新的版本字串]。<!-- UPDATE FOR EACH NEW RELEASE -->

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
>UberJar和其他相關成品可在Maven中央存放庫上使用，而不是Adobe公共Maven存放庫(`repo.adobe.com`)。 主要UberJar檔案已重新命名為`uber-jar-<version>.jar`。 因此，`classifier`標籤沒有`apis`，其值為`dependency`。



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
`cache`和`diff-cache`的新資料夾會自動建立，而您在`mvstore`中不會再遇到與`error.log`相關的例外狀況。

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

* 如果您將[!DNL Experience Manager]執行個體從6.5.0 - 6.5.4升級至Java™ 11上的最新Service Pack，您會在`RRD4JReporter`檔案中看到`error.log`例外狀況。 若要停止例外狀況，請重新啟動[!DNL Experience Manager]的執行個體。<!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

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

內容片段 — 預覽失敗，因為大型片段樹受到DoS保護。 請參閱有關預設GraphQL查詢執行器組態選項[的](https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-23945)KB文章(SITES-17934)

### AEM Forms的已知問題 {#known-issues-aem-forms-6523}

>[!NOTE]
>
> 對於沒有可用的Hotfix的問題，請勿升級至Service Pack 6.5.23.0，因為這樣可能會導致未預期的錯誤。 只有在發行必要的Hotfix之後，才能升級至Service Pack 6.5.23.0。

#### 可用的Hotfix問題 {#aem-forms-issues-with-hotfixes}

下列問題有可供下載和安裝的Hotfix。 您可以[下載並安裝Hotfix](/help/release-notes/aem-forms-hotfix.md)以解決下列問題：

* **FORMS-20203**：當使用者將Struts架構從2.5.x版升級為6.x版時，AEM Forms中的原則UI無法顯示所有設定，例如新增浮水印的選項。

* **FORMS-20360**：升級至AEM Forms Service Pack 6.5.23.0後，ImageToPDF轉換服務會失敗，並出現錯誤：
  ```17:15:44,468 ERROR [com.adobe.pdfg.GeneratePDFImpl] (default task-49) ALC-PDG-001-000-ALC-PDG-011-028-Error occurred while converting the input image file to PDF. com/adobe/internal/pdftoolkit/core/encryption/EncryptionImp```

* **FORMS-20478**：嘗試將型別7/8 TIFF檔案轉換成PDF時，轉換程式會失敗，錯誤為「ALC-PDG-001-000-Image2Pdf轉換失敗，原因為：com/sun/image/codec/jpeg/JPEGCodec」和「ALC-PDG-016-003-PDF後處理期間發生未知/未預期的錯誤」。 系統會嘗試使用TM ImageIO TIFF解碼器重試，但最終無法完成工作。

* **FORMS-14521**：如果使用者嘗試預覽含有已儲存XML資料的草稿信件，某些特定信件的草稿信件會卡在`Loading`狀態。

* AEM Forms現在包含表單元件的Struts版本從2.5.33升級至6.x。 這可提供先前未包含在SP23中的Struts變更。 已透過[Hotfix](/help/release-notes/aem-forms-hotfix.md)新增支援，您可以下載並安裝該支援，以新增對最新版Struts的支援。

#### 其他已知問題 {#aem-forms-other-known-issues}

* 安裝AEM Forms JEE Service Pack 21 (6.5.21.0)後，如果在`(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)`資料夾(FORMS-14926)下找到Geode jar `<AEM_Forms_Installation>/lib/caching/lib`的重複專案，請執行以下步驟以解決問題：

   1. 停止儲位（如果它們正在執行）。
   2. 停止AEM伺服器。
   3. 移至`<AEM_Forms_Installation>/lib/caching/lib`。
   4. 移除除`geode-*-1.15.1.2.jar`以外的所有Geode修補程式檔案。 確認只有具有`version 1.15.1.2`的Geode jar存在。
   5. 在管理員模式中開啟命令提示字元。
   6. 使用`geode-*-1.15.1.2.jar`檔案安裝Geode修補程式。

* 當使用者從AEM 6.5 Forms Service Pack 18或19升級為Service Pack 20或21時，他們遇到JSP編譯錯誤。 此錯誤會阻止他們開啟或建立最適化表單。 它也會導致其他AEM介面發生問題。 這些介麵包含頁面編輯器、AEM Forms UI、工作流程編輯器和系統概覽UI。 (FORMS-15256)

  如果您遇到這類問題，請執行以下步驟來解決問題：
   1. 導覽至CRXDE中的目錄`/libs/fd/aemforms/install/`。
   2. 刪除名稱為`com.adobe.granite.ui.commons-5.10.26.jar`的組合。
   3. 重新啟動AEM伺服器。

* 在互動式通訊代理程式UI的列印預覽中，所有欄位值都會不一致地顯示貨幣符號（例如美元符號$）。 對於最多999的值會顯示它，但對於1000或以上的值則遺失。 (FORMS-16557)
* 互動式通訊中巢狀配置片段XDP的任何修改都不會反映在IC編輯器中。 (FORMS-16575)
* 在互動式通訊代理程式UI的列印預覽中，部分計算值無法正確顯示。 (FORMS-16603)
* 在「列印預覽」中檢視信函時，內容會變更。 也就是說，某些空格會消失，而某些字母會以`x`取代。 (FORMS-15681)
* **FORMS-15428**：使用Forms附加元件更新至AEM Forms Service Pack 20 (6.5.20.0)後，依賴舊版Adobe Analytics Cloud Service （使用認證型驗證）的設定停止運作。 此問題導致Analytics規則無法正確執行。

* 當使用者設定WebLogic 14c執行個體時，在JBoss®上執行的JEE上的AEM Forms Service Pack 21 (6.5.21.0)中的PDFG服務會失敗，因為類別載入器衝突涉及SLF4J程式庫。 錯誤顯示如下(CQDOC-22178)：

  ```java
  Caused by: java.lang.LinkageError: loader constraint violation: when resolving method "org.slf4j.impl.StaticLoggerBinder.getLoggerFactory()Lorg/slf4j/ILoggerFactory;"
  the class loader org.ungoverned.moduleloader.ModuleClassLoader @404a2f79 (instance of org.ungoverned.moduleloader.ModuleClassLoader, child of 'deployment.adobe-livecycle-jboss.ear'
  @7e313f80 org.jboss.modules.ModuleClassLoader) of the current class, org/slf4j/LoggerFactory, and the class loader 'org.slf4j.impl@1.1.0.Final-redhat-00001' @506ab52
  (instance of org.jboss.modules.ModuleClassLoader, child of 'app' jdk.internal.loader.ClassLoaders$AppClassLoader) for the method's defining class, org/slf4j/impl/StaticLoggerBinder,
  have different Class objects for the type org/slf4j/ILoggerFactory used in the signature.
  ```

* Forms-21378：啟用伺服器端驗證(SSV)時，表單提交可能會失敗。 如果您遇到此問題，請聯絡Adobe支援以尋求協助。



## 包含的OSGi套件組合和內容套件{#osgi-bundles-and-content-packages-included}

下列文字檔案列出此[!DNL Experience Manager] 6.5 Service Pack發行版本中包含的OSGi套件組合和內容套件：

* [Experience Manager中包含的OSGi套件組合清單6.5.23.0](/help/release-notes/assets/65230-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager中包含的內容套件清單6.5.23.0](/help/release-notes/assets/65230-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 受限制的網站{#restricted-sites}

這些網站僅供客戶使用。 如果您是客戶且需要存取權，請聯絡您的Adobe客戶經理。

* [產品下載網址為licensing.adobe.com](https://licensing.adobe.com/)
* [連絡Adobe客戶支援](https://experienceleague.adobe.com/zh-hant/docs/customer-one/using/home)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 產品頁面](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5檔案](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65)
>* [訂閱Adobe優先產品更新](https://www.adobe.com/tw/subscription/priority-product-update.html)
