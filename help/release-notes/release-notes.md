---
title: 版本注意事項 [!DNL Adobe Experience Manager] 6.5
description: 尋找版本資訊、新增功能、安裝作法和詳細的變更清單 [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
source-git-commit: 26cea35dcbdbafe622f975bac7920ea5fd5fbd6c
workflow-type: tm+mt
source-wordcount: '4460'
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
| 版本 | 6.5.18.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 類型 | Service Pack發行 |
| 日期 | 2023年8月24日星期四 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 下載 URL | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.18.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## 包含的內容 [!DNL Experience Manager] 6.5.18.0 {#what-is-included-in-aem-6518}

[!DNL Experience Manager] 6.5.18.0包括自2019年4月6.5首次發行以來所推出的新功能、客戶要求的重要增強功能、錯誤修正，以及效能、穩定性和安全性改善專案。 [安裝此Service Pack](#install) 於 [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

此版本中的部分主要功能和增強功能包括：

**重要功能**

* 資產，Dynamic Media - [Dynamic Media中的影片支援多字幕與多音訊曲目](/help/assets/video.md#about-msma) — 您現在可以輕鬆地將多個字幕和多個音軌新增到主要視訊中。 此功能表示您的視訊可在全球對象中存取。 您可以透過多種語言，為全球觀眾自訂單一已發佈的主要影片，並遵守不同地理區域的協助工具准則。 作者也可以從使用者介面的單一標籤管理字幕和音軌。

* 資產 — 您現在可以從搜尋結果導覽至包含資產的檔案夾位置，因此可讓您執行各種資產管理工作。 (ASSETS-23182)

**重要增強功能**

* 內容片段中的Sites Polaris選取器已改善效能。 (SITES-14092)

* 啟用Sites頁面編輯器/影像元件使用者，以參照遠端資產Cloud Service中的資產。 (SITES-13448， SITES-13433)

* 為了在清單檢視中快速找到系統中可能有多個專案的專案，Adobe現在支援伺服器端排序。 專案節點會在使用者介面中呈現之前，根據使用者選取的欄在後端排序。 (NPR-41027)

* AEM 6.5.18.0支援MongoDB 5.0至6.0。

**汰除功能**

* AEM中的ActiveMQ已過時。 ActiveMQ用於兩個AEM Publish執行個體之間的通訊。 Adobe建議客戶現在使用負載平衡器。

**Forms**

* **[增強規則編輯器中使用自訂錯誤處理常式的錯誤處理功能](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/standard-validation-error-messages-adaptive-forms.html)：** 您現在可以叫用自訂函式（使用使用者端程式庫）來回應外部服務傳回的錯誤，並為一般使用者提供量身打造的回應。 或者，您可以針對服務傳回的錯誤採取特定動作。例如，您可以在後端叫用自訂工作流程來取得特定錯誤代碼，或通知客戶服務已停止服務

* **[增強的Adobe Sign工作流程步驟](https://experienceleague.adobe.com/docs/experience-manager-65/forms/workflows/aem-forms-workflow-step-reference.html#sign-document-step)：** AEM工作流程中的Adobe Sign工作流程步驟提供下列增強功能。

   * **Adobe Sign採用政府ID式驗證，具備更強的安全性：** Adobe Acrobat Sign的政府機關身分證件可讓使用者使用政府核發的ID （駕照、國民身分證、護照）進行身分驗證，提供額外的驗證層。 運用信任的身分識別檔案，這項增強功能為簽署程式增添了額外的信賴度，非常適合需要增強安全性、法規遵循及使用者驗證的案例。

   * **增強Adobe Sign檔案稽核軌跡的透明度：** 使用稽核軌跡功能，以針對Adobe Sign檔案的生命週期取得詳細深入分析。 使用「稽核軌跡」，您現在可以維護與檔案相關的所有動作與互動的完整記錄。 其中包括檢視、編輯或簽署檔案者的詳細資訊，以及每個事件的時間戳記。 此增強功能對於維護合規性、解決爭議及確保數位合約的完整性至關重要。


   * **擴充協定收件者的角色，而不只是簽署者：** Adobe Acrobat Sign可選擇擴充協定收件者的角色，而不只是簽署者，以便更符合其工作流程需求。 啟用後，協定中的每個收件者皆可個別設定其角色，預設值為「簽署者」。


* **[jee上的AEM Forms完整安裝程式](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/jee-installation/aem-forms-jee-supported-platforms.html)**：此Service Pack為JEE上的AEM Forms提供完整安裝程式，可支援多種新軟體組合，包括：
   * Microsoft Windows Server 2022
   * Microsoft Active Directory 2022
   * 在Windows Server 2022上OracleWebLogic 14C
   * redhat JBoss 7.4.10
   * MongoDB 4.4
   * MySQL JDBC聯結器8

如果您要執行全新的安裝或打算在JEE環境中使用AEM 6.5 Forms的最新軟體，Adobe建議在JEE完整安裝程式上使用AEM 6.5.18.0 Forms 。 若要探索新增和淘汰的軟體的完整清單，請參閱JEE上的AEM Forms或OSGi上的AEM Forms檔案。

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## 已修正Service Pack 18中的問題 {#fixed-issues}

### [!DNL Sites]{#sites-6518}

* 已使用大量編輯器透過下載 `tsv` 匯出、離線變更，然後上傳 `tsv` 返回Experience Manager。 即使頁面已更新，JCR屬性 `cq:lastModified` 未更新且位於時間軸中。 (SITES-14072)
* 建立體驗片段的即時副本或轉出時，體驗片段內的連結參考沒有更新。 (SITES-14759)
* 已將工作流程同步動作從父頁面新增至現成的Experience Manager標準轉出設定「轉出頁面和子頁面」，且非同步作業失敗並出現NullPointer例外狀況。 來源位置頁面(en-us)不存在於父項中，但存在於目標位置（即時副本） (en)中。 (SITES-12207)
* 您有&#39;en&#39;頁，其中包含 `jcr:description` 並傳送頁面以供翻譯。 此 `jcr:description` 正在翻譯中，屬性會顯示在launch下。 但是，提升啟動時， `jcr:description` 未在頁面中更新。 (SITES-13146)
* Blueprint轉出後，即時副本上的本地化內容會遺失。 (SITES-12602)

#### 管理員使用者介面{#sites-adminui-6518}

* 如果透過useradmin主控台移除使用者的刪除許可權，使用者將不再看到sites.html主控台中的「屬性」按鈕（選取頁面時）。 但是，如果使用者開啟頁面編輯器，則會出現此選項。 (SITES-14341)
* 當資料夾中有許多頁面（每個頁面都有許多版本）時，使用比較版本功能時，執行個體的負載會變高。 如果有多位使用者同時使用此功能，執行個體可能會停止運作。 (SITES-13026)

#### [!DNL Content Fragments]{#sites-contentfragments-6518}

* 發現下列專案中的例外狀況處理問題 `RemoteAssetClientImpl`. 當查詢中繼資料時發生IOException或RuntimeException時，目前的執行緒會嘗試關閉並重新建立共用的httpClient，這可能會導致執行緒中出現一連串的其他錯誤。 (SITES-14092)
* 當作者在內容片段中填寫RTF編輯器欄位，並在連結內插入影像時，當透過GraphQL API查詢內容片段時，出現錯誤訊息 `Exception while fetching data (/genericContentByPath) : null` 會傳回。 只有在連結內有影像時，才會發生此錯誤。 從連結中移除影像會使錯誤訊息消失。 (SITES-13988)
* GraphQL的Experience Manager6.5實作與主要版本不符，且缺少數個重要修正。 (SITES-13096)
* 存取中繼資料服務端點時需要強制的HTTP標頭。 (SITES-13068)

#### 核心元件{#sites-core-components-6518}

* 資產選擇器關閉並重新開啟時，不會擷取更新的資產清單。 如果新資產上傳到存放庫，在重新整理包含資產選擇器的頁面之前，它們不會顯示在資產選擇器中。 (SITES-14828)
* 整合在網站編輯器(CS)中的資產選擇器使用者介面在視窗縮小時沒有回應。 (SITES-14127)
* 資產選擇器整合的Adobe IMS (Identity Management系統)設定接受不正確的值。 (SITES-13962)
* 資產選取器若整合至網站影像元件，不應允許選取非影像資產。 (SITES-13879)
* 成功登入後，系統會將使用者重新導向至頁面編輯器。 使用者必須重新開啟資產選擇器，才能挑選遠端資產。 (SITES-13851)
* 遠端資產選取器一律會重新導向至Adobe IMS (Identity Management System) Stage環境。 (SITES-13448， SITES-13433)

<!-- #### [!DNL Experience Fragments]{#sites-experiencefragments-6518}

* A -->

#### 頁面編輯器{#sites-pageeditor-6518}

* 當作者開啟頁面屬性時，對話方塊的檢視不正確。 也就是說，會顯示額外的水準卷軸和額外邊界。 (SITES-14502)
* Experience Manager6.5 Service Pack 17中為錨點和內文標籤新增的樣式已導致CSS問題。 在Author中，錨點標籤未顯示底線。 (SITES-14261)

### [!DNL Assets]{#assets-6518}

* 熒幕助讀程式不會宣告 [!UICONTROL 開始裁切] 選項。 (NPR-40593)
* 在AEM 6.5.17.0執行個體上傳資產時，Experience Manager會顯示錯誤和警告訊息。 (ASSETS-26232)
* 當您從具有唯讀存取權的資料夾以完整存取權來關聯資料夾中的資產時，Experience Manager會顯示錯誤訊息，但還是會在兩個資產之間建立部分關係。 (ASSETS-25832)
* 連結的資產在AMS執行個體和Cloud Service執行個體之間無法運作。 (ASSETS-24930)
* 編輯中繼資料結構Forms時， [!UICONTROL 準時] 和 [!UICONTROL 關閉時間] 欄位未正確儲存。 (ASSETS-24871)
* 針對已訓練的標籤產生智慧標籤報表時，不會列出可信度分數較低的標籤。 (ASSETS-24109)
* 在「欄」檢視中編輯和註解影像時，Experience Manager會顯示空白熒幕。 (ASSETS-24108)
* 熒幕助讀程式在建立集合時，不會朗讀「新增使用者」欄位的目的。 (ASSETS-21736)
* 此 **集合** 標籤未在「集合」屬性頁面上本地化。 (ASSETS-21102)
* 當您新增規則或使用預設中繼資料結構表單編輯現有規則時，下拉式清單中的語言未當地語系化。 (ASSETS-21026)
* 在中繼資料結構中新增JSON路徑時，Experience Manager會顯示未本地化的錯誤訊息。 (ASSETS-21025)
* 左側導覽中的時間軸選項未顯示適當的對比率。 (ASSETS-17348)
* 日曆元素不使用必要的ARIA屬性。 (ASSETS-17282)
* 左側導覽文字未顯示適當的對比率。 (ASSETS-17268)
* 熒幕助讀程式使用者不會隱藏Lightbox影像。 (ASSETS-17263， ASSETS-17242)
* 作用中使用者介面的狀態未提供有關背景的合適對比率。 (ASSETS-17260)
* 為資產加上註解時，熒幕助讀程式無法辨識 [!UICONTROL 另存為版本] 或 [!UICONTROL 開始工作流程] 使用鍵盤方向鍵導覽按鈕時，使用這些按鈕。 (ASSETS-17253)
* 某些ARIA角色在Assets首頁上不包含適當的子角色。 (ASSETS-17248)
* 當您使用鍵盤導覽至影像型別資產的編輯選項時， [!UICONTROL 啟動地圖] 無法辨識選項，鍵盤焦點會移至「取消」按鈕。 (ASSETS-17238)

#### [!DNL Dynamic Media]{#assets-dm-6518}

* 當VTT無法下載時，視訊不會顯示。 它會顯示空白熒幕，而視訊筆畫壓感則會向前移動。 (ASSETS-21909)
* 使用鍵盤上的Tab鍵導覽時，焦點沒有移動到視訊下方的多個控制項。 因此，無法存取。 改善互動視訊的鍵盤導覽。 (ASSETS-25749)
* 修正Dynamic Media元件中顯示停用的檢視器預設集。 (ASSETS-22922)
* 已移除「一般設定安全性」標籤中的「影像伺服」。 (ASSETS-24618)
* 修正無法上傳至Dynamic Media和StringIndexOutOfBoundsException的資產。 (ASSETS-25787)
* 在「基本」索引標籤中為強制性「寬度」編輯欄位新增視覺星號。 (ASSETS-25741)
* 修正了浮水印Dynamic Media轉譯的下載問題。 (ASSETS-26173)
* 恢復非視訊資產名稱的127個字元限制。 (ASSETS-26074)

### [!DNL Forms]{#forms-6518}

<!-- Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the AEM 6.5.18.0 Forms add-on packages release is scheduled for Thursday, August 31, 2023. A list of Forms fixes and enhancements would be added to this section post the release. -->

* **文件服務**
   * 當使用者使用transformPDF服務時，它會因例外而失敗： `java.lang.ClassNotFoundException: default task-158Class name com.adobe.internal.afml.AFMLExceptionInvalidParameter from package com.adobe.internal.afml` (FORMS-9957)
   * 如果伺服器在PDF檔案產生期間關閉，則會擲回伺服器啟動後工作處理錯誤。 伺服器啟動期間需要新增引數 — Dcom.adobe.livecycle.dsc.deferServiceStart=true。 (FORMS-9836)
   * 如果使用者嘗試使用AssemblerService.Invoke方法合併PDF，則組合器無法執行工作。 (FORMS-9550)
   * 當您在OSGI和JEE環境中升級至AEM 6.5.15.0 Service Pack時，使用特定範本的組合器服務會停止運作。 (FORMS-9355、FORMS-9445、FORMS-9408)
   * Java記憶體回收無法清除AEM Forms OSGi伺服器上的舊程式碼棧積，因為XMLFormService的「全域逾時」未設定為適當的值。 (FORMS-9384、FORMS-9035)
   * 呈現最適化表單的PDF預覽時，錯誤記錄中會出現不想要的Java棧疊傾印。 (FORMS-8865)
   * 當使用者檢視檔案詳細資訊區段中檔案的檔案狀態時，其未正確顯示。 (FORMS-8946、FORMS-10424)
   * 當使用者升級至AEM Forms並使用sendToPrinter服務時，棧積利用率會持續增加。 (FORMS-10148)
   * 在JBoss 7.4 EAP伺服器上，電子郵件功能失敗的原因為 `java.io.IOException`. (FORMS-10138)
   * 當使用者使用transformPDF服務時，它會失敗並出現錯誤： `java.lang.ClassNotFoundException: default task-158Class name com.adobe.internal.afml.AFMLExceptionInvalidParameter from package com.adobe.internal.afml`(FORMS-9957)
   * 升級至AEM Service Pack 6.5.14.0後，使用特定範本時，組裝程式服務會發生問題。 (FORMS-9445、FORMS-9408)
  <!-- *  When a user configures the watched folder endpoint for PDF Generator, it fails to pick documents on JDK 11. (FORMS-10152) -->
* **調適型表單**
   * 當使用者嘗試在不修改欄位的情況下呼叫自訂函式時（例如設定另一個欄位的值），它會失敗。 (FORMS-9921)
   * 在最適化表單中使用規則編輯器的自訂錯誤函式時，會發生下列錯誤：
      * 當使用者嘗試使用時@param{boolean} 若使用函式，規則編輯器不允許布林值傳遞至函式。
      * 當使用者嘗試使用時@param{string} 若使用函式，規則編輯器無法傳遞選用值，且會對不完整的規則發出警告。 (FORMS-9816、FORMS-9815)
   * 表單 — 使用者群組無法在最適化表單中呼叫規則編輯器兩次。 (FORMS-9051)
   * 在視覺編輯器中，當使用者選取表單物件時，則會將整個欄位例項物件傳遞至自訂函式，而非僅傳遞欄位的值。 (FORMS-10015)
   * 當使用者建立核心元件型最適化表單並新增文字輸入元件時， `Is Empty` 和 `Is Not Empty` 無法在規則編輯器中運作。 (FORMS-10098)
   * 如果欄位在核心元件型最適化表單中被標籤為無效，它會在欄位上啟動變更事件。 (FORMS-10087)
   * 當使用者嘗試使用複雜的JSON結構描述建立最適化表單時，它會失敗。 錯誤發生於：
     `GET /content/forms/af/katezeroone/testaf1.html HTTP/1.1] com.adobe.aemds.guide.service.impl.JsonObjectCreatorImpl Could not emit JSON with context java.lang.ArrayIndexOutOfBoundsException:0`。(FORMS-9639)
   * 在調適型表單中，當使用者停用「我同意條款與條件」核取方塊時，只要使用者向下捲動，就會再次啟用。 (FORMS-9458)
   * 當使用者使用Google Chrome/Firefox在Android裝置上開啟最適化表單並在文字方塊中輸入允許的最大字元時，文字方塊中的值無法清除。 (FORMS-9354)
   * 當核取方塊的標籤包含&#39;，&#39;、&#39;/&#39;或&#39;.&#39;等特殊字元時，按一下文字/標籤不會選取個別核取方塊。 (FORMS-9313)
   * 當使用者嘗試驗證條款與條件元件時，它無法驗證元件是否不在焦點中，同時其他元件獲得驗證。 (FORMS-8725、FORMS-8913)
   * 如果最適化表單在升級至AEM 6.5.16.0 Service Pack後重新載入，檔案附件擷取會失敗。 (FORMS-8906)
   * 在基於XDP的調適型表單中，如果核取方塊元件包含指派給數值的文字標題，則文字標題會遭截斷，且不符合指派值。 (FORMS-8743)
   * 如果使用者嘗試為製作環境在內嵌於最適化表單中的片段實施延遲載入，為片段定義的規則/邏輯不會反映在表單中。 (FORMS-8554、FORMS-9182)
   * 當您嘗試在AEM 6.5.16.0 Service Pack中開啟任何Coral對話方塊時，它會產生 `error.log: cannot render resource` 例外。 (FORMS-8942)
   * 當使用者嘗試翻譯在最適化表單中包含單一選項的核取方塊時，它會失敗。 (FORMS-10181)
* **協助工具**
   * 在最適化表單中使用手寫簽名元件時，會發生下列錯誤：
      * 在「草寫簽名」元件之後，如果有更多元件，按下Tab鍵不會移到簽名對話方塊；而是移到下一個元件。 只有在遍歷所有元件後，它才會最終移至簽名對話方塊。
      * 當使用者使用筆刷或鍵盤登入簽名對話方塊時，按Enter鍵不會關閉對話方塊。
      * 無法使用鍵盤存取清除簽章確認對話方塊。
      * 熒幕助讀程式無法讀取在對話方塊中輸入的資訊。
      * 若不使用滑鼠則無法清除簽名。  (FORMS-9317)
   * 當使用者提交最適化表單時，熒幕助讀程式無法讀取必填欄位的錯誤訊息。 (FORMS-9316)
   * 當熒幕助讀程式讀取HTML表單時，以字距微調（間距）讀取文字時發生問題。 (FORMS-9258)
   * 在最適化表單中，連結至文字的參考/註腳不會使用熒幕助讀程式來呼叫。 (FORMS-8920)
   * 最新的設計工具無法正確辨識協助工具標籤。 (FORMS-10139)
* **互動式通訊**
   * 在通訊管理中，本地化無法運作。 (FORMS-8926)
   * 使用publishAll服務時，草稿字母無法開啟。 (FORMS-8589)
   * Experience Manager後，伺服器上已安裝Service Pack 16，所有互動式通訊字母嘗試編輯這些字母時都會開始計時。 如果他們提供任何範例裝載來預覽或檢視/編輯屬性頁面，就有效果。 但是，他們無法編輯字母。 (FORMS-9067)


<!-- ### [!DNL Commerce]{#commerce-6518}

* A -->

### Foundation{#foundation-6518}

#### 內容發佈{#foundation-content-distribution-6518}

* 不應封鎖資產刪除佇列，且記錄檔中不應發生錯誤。 (NPR-40570)

<!-- #### Integrations{#integrations-6518}

* A -->

<!-- #### Oak{#oak-6518}

* A -->

#### Platform{#foundation-platform-6518}

* 安裝vanillaExperience Manager、Service Pack 17後，您會看到 `stderr.log`. Vanilla安裝應該不會發生錯誤。 (CQ-4353637)
* 「標籤」(Tagging)畫面中的「建立」(Create)按鈕不遵守ACL （存取控制清單）。 (NPR-40973)
* 無法在Experience Manager上建立、存取（或兩者）ContextHub的快取節點。 (NPR-40515)

#### 複製{#foundation-replication-6518}

* 復寫排清會刪除請求路徑的所有子系。 (NPR-40569)

#### Sling{#foundation-sling-6518}

* 產生「連結共用報表」時，「連結」欄未包含正確的值。 (NPR-40798)
* 使用AEM 6.5.15.0時，AEM重新啟動後所有虛名URL、Sling別名和Sling對應都會中斷。 (NPR-40420)

#### 翻譯專案{#foundation-translation-6518}

* 翻譯 `rules.xml` 從翻譯設定使用者介面新增規則時，會以不良方式排序。 (NPR-40431)
* 支援在翻譯期間使用查詢引數的連結。 (NPR-40339)
* 更新其他內容根目錄後，字典使用者介面未為客戶載入。 (NPR-40650)
* 當其中一個資產是內容片段，包含具有ReferenceFragment或ContentFragment型別的多欄位時，建立語言副本時發生錯誤。 (NPR-40892)

#### 使用者介面{#foundation-ui-6518}

* 如 [設定瀏覽器檔案](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/configurations.html?lang=en#using-configuration-browser)， _名稱會成為存放庫中的節點名稱_. 不過，在設定瀏覽器中，設定標題會用於CRXDE Lite中的路徑，而設定名稱會遭忽略。 (NPR-40607)

<!-- #### WCM{#wcm-6518}

* A -->

#### 工作流程{#foundation-workflow-6518}

* 回覆資產版本會將資產狀態維持在處理模式。 (NPR-41029)
* 資產和專案使用者介面的排序問題。 有些會根據業務需求覆蓋資產和專案使用者介面上的自訂欄。 他們已使用現成可用的屬性實作排序 `sortable=true`. 不過，當「專案」或「資產」使用者介面下有許多專案時，他們發現排序不一致。 (NPR-41027)
* 記錄檔已填滿 `NullPointerException` 在 `EMailNotificationService`不會傳送工作流程應傳送的、和電子郵件。 (NPR-40898)
<!-- REMOVED BY ENGINEERING FROM TOTAL RELEASE CANDIDATE LIST  * The timeline is not providing references to the selected content. (NPR-40806) -->

## 安裝 [!DNL Experience Manager] 6.5.18.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.18.0需要 [!DNL Experience Manager] 6.5.請參閱 [升級檔案](/help/sites-deploying/upgrade.md) 以取得詳細指示。 <!-- UPDATE FOR EACH NEW RELEASE -->
* 您可在Adobe上取得Service Pack下載 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.18.0.zip).
* 在具有MongoDB和多個執行個體的部署上，安裝 [!DNL Experience Manager] 使用封裝管理程式的其中一個Author執行個體上的6.5.18.0 。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe不建議您移除或解除安裝 [!DNL Experience Manager] 6.5.18.0套件。 因此，在安裝套件之前，您應該建立 `crx-repository` 以防您必須將其回覆。 <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### 在上安裝Service Pack [!DNL Experience Manager] 6.5{#install-service-pack}

1. 如果執行個體處於更新模式（從舊版更新執行個體時），請在安裝前重新啟動執行個體。 如果執行個體的目前運作時間很高，Adobe建議重新啟動。

1. 安裝之前，請拍攝快照或進行全新備份 [!DNL Experience Manager] 執行個體。

1. 下載Service Pack，從 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.18.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. 開啟封裝管理員，然後選取 **[!UICONTROL 上傳套裝]** 以上傳套件。 若要瞭解更多，請參閱 [封裝管理員](/help/sites-administering/package-manager.md).

1. 選取封裝，然後選取 **[!UICONTROL 安裝]**.

1. 若要更新S3聯結器，請在安裝Service Pack後停止執行個體，將現有聯結器取代為安裝資料夾中提供的新二進位檔案，然後重新啟動執行個體。 另請參閱 [Amazon S3資料存放區](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>在安裝Service Pack期間，套件管理員UI上的對話方塊有時會退出。 Adobe建議您先等待錯誤記錄穩定下來，再存取部署。 等待與更新程式套件組合解除安裝相關的特定記錄，再確認安裝成功。 此問題通常發生在以下位置： [!DNL Safari] 瀏覽器，但可能間歇性地在任何瀏覽器上發生。

**自動安裝**

您可以使用兩種不同的方法來自動安裝 [!DNL Experience Manager] 6.5.18.0。<!-- UPDATE FOR EACH NEW RELEASE -->

* 將套件置於 `../crx-quickstart/install` 資料夾（當伺服器線上上可用時）。 套件會自動安裝。
* 使用 [來自封裝管理員的HTTP API](/help/sites-administering/package-manager.md#package-share). 使用 `cmd=install&recursive=true` 以便安裝巢狀套件。

>[!NOTE]
>
>Experience Manager6.5.18.0不支援Bootstrap安裝。 <!-- UPDATE FOR EACH NEW RELEASE -->

**驗證安裝**

若要瞭解經過認證可搭配此版本使用的平台，請參閱 [技術需求](/help/sites-deploying/technical-requirements.md).

1. 產品資訊頁(`/system/console/productinfo`)顯示更新的版本字串 `Adobe Experience Manager (6.5.18.0)` 在 [!UICONTROL 已安裝的產品]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. 所有OSGi套件組合都是 **[!UICONTROL 作用中]** 或 **[!UICONTROL 片段]** 在OSGi主控台中(使用Web主控台： `/system/console/bundles`)。

1. OSGi套件 `org.apache.jackrabbit.oak-core` 是1.22.16版或更新版本(使用Web主控台： `/system/console/bundles`)。 <!-- NPR-41010 for 6.5.18.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### 安裝Service Pack for [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

如需在Experience Manager Forms上安裝Service Pack的說明，請參閱 [Experience Manager Forms Service Pack安裝指示](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

### 安裝Experience Manager內容片段的GraphQL索引套件{#install-aem-graphql-index-add-on-package}

使用GraphQL的客戶必須安裝 [使用GraphQL索引套件1.1.1Experience Manager內容片段](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

如此一來，您就可以根據使用者實際使用的功能，新增必要的索引定義。

無法安裝此套件可能會導致GraphQL查詢變慢或失敗。

>[!NOTE]
>
>每個執行個體僅安裝此套件一次；不需要隨每個Service Pack重新安裝。

### UberJar{#uber-jar}

The UberJar for [!DNL Experience Manager] 6.5.18.0可在以下網址取得： [Maven中央存放庫](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.18/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

若要在Maven專案中使用UberJar，請參閱 [如何使用UberJar](/help/sites-developing/ht-projects-maven.md) 並在專案POM中加入下列相依性： <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.18</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar和其他相關成品可在Maven中央存放庫上使用，而不是Adobe公共Maven存放庫(`repo.adobe.com`)。 主要UberJar檔案已重新命名為 `uber-jar-<version>.jar`. 因此，不存在 `classifier`，使用 `apis` 作為值，針對 `dependency` 標籤之間。

## 過時的功能{#removed-deprecated-features}

以下是標示為過時的功能 [!DNL Experience Manager] 6.5.7.0。功能最初會標示為過時，之後會在未來版本中移除。 提供替代選項。

檢閱是否在部署中使用功能或功能。 此外，計畫變更實作以使用替代選項。

| 區域 | 功能 | 替代方案 |
|---|---|---|
| 整合 | 畫面 **[!UICONTROL Experience Manager Cloud Service選擇加入]** 已過時，因為 [!DNL Experience Manager] 和 [!DNL Adobe Target] 整合已更新於 [!DNL Experience Manager] 6.5.整合支援Adobe Target Standard API。 API透過Adobe IMS和以下方式使用驗證 [!DNL Adobe I/O Runtime]. 它可支援AdobeLaunch在樂器方面日益增加的作用 [!DNL Experience Manager] 頁面對於analytics和個人化，選擇加入精靈在功能上無關。 | 設定系統連線、Adobe IMS驗證和 [!DNL Adobe I/O Runtime] 透過個別 [!DNL Experience Manager] 雲端服務。 |
| 連接器 | Microsoft®SharePoint 2010和Microsoft® SharePoint 2013的JCR ConnectorAdobe已遭取代 [!DNL Experience Manager] 6.5. | N/A |

## 已知問題{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->
<!-- REMOVED AS PER CQDOC-20022, JANUARY 23, 2023 * If you install [!DNL Experience Manager] 6.5 Service Pack 10 or a previous service pack on [!DNL Experience Manager] 6.5, the runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) is deleted.
To retrieve your runtime copy, Adobe recommends to synchronize the design-time copy of the custom workflow model with its runtime copy using the HTTP API:
`<designModelPath>/jcr:content.generate.json`. -->

* 與來自Service Pack 13及更高版本的Oak相關，以下錯誤記錄已開始出現，這會影響持續性快取：

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

* 將可能已使用您內容模型的自訂API名稱的GraphQL查詢更新為改用內容模型的預設名稱。

* GraphQL查詢可能使用 `damAssetLucene` 索引而非 `fragments` 索引。 此動作可能會導致GraphQL查詢失敗或需要很長時間才能執行。

  若要修正問題， `damAssetLucene` 必須設定為包含下列兩個屬性：

   * `contentFragment`
   * `model`

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
   * 透過Shoppable Banner檢視器預覽資產時，Dynamic Media互動影像中的熱點不可見。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` ：等待登入變更完成解除登入逾時。

* 從AEM 6.5.15開始，Rhino JavaScript Engine由 ```org.apache.servicemix.bundles.rhino``` 捆綁有新的提升行為。 使用嚴格模式的指令碼(```use strict;```)必須正確宣告其變數，否則不會執行，而會擲回執行階段錯誤。

### AEM Forms的已知問題

#### 支援平台

* WebLogic JEE伺服器不支援高於1.8.0_281的JDK版本。 (FORMS-8498、CQDOC-20383)
* 作為 [!DNL Microsoft® Windows Server 2019] 不支援 [!DNL MySQL 5.7] 和 [!DNL JBoss® EAP 7.1]， [!DNL Microsoft® Windows Server 2019] 不支援全包安裝 [!DNL Experience Manager Forms 6.5.10.0]. (CQDOC-18312)
* JDK 11.0.20不支援在JEE安裝程式上安裝AEM Forms。 僅支援JDK 11.0.19或較舊版本以在JEE安裝程式上安裝AEM Forms。 (FORMS-10659)

#### 安裝

* 在JBoss® 7.1.4平台上，當使用者安裝Experience Manager6.5.16.0或更新版Service Pack時， `adobe-livecycle-jboss.ear` 部署失敗。 (CQ-4351522、CQDOC-20159)

#### 最適化表單

* 發佈調適型表單時，其所有相依性（包括原則）都會重新發佈，即使未進行任何修改亦然。 (FORMS-10454)
* 當使用者選擇在最適化表單中首次設定欄位時，儲存設定的選項未顯示在屬性瀏覽器中。 選擇在同一編輯器中設定最適化表單的其他欄位即可解決問題。
* 在最適化表單的指南容器中設定重新導向URL時，內嵌簽署會停止運作。 (FORMS-10493)

#### 互動式通訊

* 升級至AEM Service Pack 18後，無法編輯互動式通訊信件。 (FORMS-10578)

## 包含的OSGi套件組合和內容套件{#osgi-bundles-and-content-packages-included}

下列文字檔案列出中包含的OSGi套件組合和內容套件 [!DNL Experience Manager] 6.5.18.0： <!-- UPDATE FOR EACH NEW RELEASE -->

* [Experience Manager6.5.18.0中包含的OSGi套件組合清單](/help/release-notes/assets/65180_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager6.5.18.0中包含的內容套件清單](/help/release-notes/assets/65180_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 受限制的網站{#restricted-sites}

這些網站僅供客戶使用。 如果您是客戶且需要存取權，請聯絡您的Adobe客戶經理。

* [產品下載網址為licensing.adobe.com](https://licensing.adobe.com/)
* [聯絡Adobe客戶支援](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 產品頁面](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5檔案](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hant)
>* [訂閱 Adobe 優先產品更新](https://www.adobe.com/tw/subscription/priority-product-update.html)
