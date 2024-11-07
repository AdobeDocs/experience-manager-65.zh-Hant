---
title: ' [!DNL Adobe Experience Manager] 6.5的發行說明'
description: 尋找 [!DNL Adobe Experience Manager] 6.5的版本資訊、新增功能、安裝操作說明和詳細變更清單。
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: bb6e843bfad3feb194dd00588dbb4a2d3539743a
workflow-type: tm+mt
source-wordcount: '4658'
ht-degree: 1%

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
| 版本 | 6.5.22.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 類型 | Service Pack發行 |
| 日期 | 2024年11月21日星期四<!-- UPDATE FOR EACH NEW RELEASE --> |
| 下載 URL | [軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.21.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## [!DNL Experience Manager] 6.5.22.0包含的內容 {#what-is-included-in-aem-6522}

[!DNL Experience Manager] 6.5.22.0包含新功能、客戶要求的重要增強功能和錯誤修正。 此外，還包含自2019年4月6.5首次推出以來的效能、穩定性和安全性改善專案。 在[!DNL Experience Manager] 6.5上[安裝此Service Pack](#install)。

<!-- UPDATE FOR EACH NEW RELEASE -->

## 主要功能和增強功能

<!-- * _6.5.22.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

此版本中的部分主要功能和增強功能包括：


<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## 已修正Service Pack 22中的問題 {#fixed-issues}


### [!DNL Sites]{#sites-6522}


#### 親和力 {#sites-accessibility-6522}

* 附注色票選擇器按鈕缺少可存取的名稱。 也就是說，使用熒幕助讀程式，在輸入新的十六進位值後，按鈕沒有可理解的名稱可供選取。 (SITES-11992)主要
* 下列元素在左側邊欄功能表中看起來像是清單，但在熒幕助讀程式中並未標示為清單：

   * 網站
   * 即時副本
   * 啟動
   * 語言副本
   * 資料夾
   * CSV報表(SITES-2874)

* AEM Core Web Content Management需要RTF編輯器中超連結的協助工具標籤。 當文字元件中使用超連結時，錨點標籤應包含`aria-label`屬性，以確保熒幕朗讀程式可出於協助工具目的準確地閱讀及傳達連結文字。 (SITES-11511)
* 在AEM中，清單檢視的表格標題中的互動式元素沒有必要的「按鈕」角色。 因此，NVDA熒幕助讀程式不會針對下清單格標題宣告預期的按鈕角色：標題、名稱、已修改、已發佈、預覽、範本、操作、工作流程。 表格標頭中的每個互動式元素都應指派一個「按鈕」角色，以確保與NVDA等輔助技術的相容性。 (SITES-10962)


#### 管理員使用者介面{#sites-adminui-6522}

* 在AEM的某些情況下，版本預覽和比較功能在數個頁面中無法如預期運作。 具體來說：

   * **預覽問題：**&#x200B;嘗試預覽頁面版本時，一開始會出現錯誤。 重試後，預覽會產生空白頁面。
   * **版本比較問題：**「與目前版本比較」功能只會顯示目前版本，不會醒目顯示版本之間的任何差異。 (SITES-23988)主要

* 在複製並貼上動作期間使用`defaultPasteMode`設為`plaintext`時，RTF編輯器(RTE)欄位中出現未預期的`<br>`標籤。 此問題會對相同內容產生不同的標籤，導致相同的文字內容在客戶的翻譯記憶庫中翻譯兩次。 (SITES-23606)主要
* 在AEM 6.5.20.0中，**管理出版物**&#x200B;功能發生功能問題。 選取節點並排程以供未來發佈時，嘗試包含子節點時可能會顯示錯誤訊息「無法擷取所選專案的子資源」。 此問題阻止使用&#x200B;**包含子項**&#x200B;選項，導致預期的內容階層無法完整發佈。 (SITES-23000)主要
* 範本的「已發佈」時間戳記未在製作環境中更新，即使範本已成功復寫至發佈執行個體。 預期的行為是製作執行個體上的時間戳記反映最新的發佈，但此更新未按預期發生。 (SITES-21585)主要
* AEM作者環境中傳入連結的計數有所差異。 與傳統UI相比，左側邊欄顯示的連結較少。 此外，某些合法的傳入連結無法運作。 (SITES-24837)
* 在AEM的「時間軸」檢視中檢視頁面版本時，回報載入時間過長。 顯示版本最多需要19分鐘。 從AEM 6.4.8升級至6.5.18後，此問題持續發生，大幅干擾工作流程效率。 (SITES-22468 &amp; SITES-22467)

<!-- #### Classic UI{#sites-classicui-6522} 

* A -->


#### [!DNL Content Fragments]{#sites-contentfragments-6522}

* 在升級的AEM 6.5.17中，儲存內容片段導致下列錯誤： *錯誤：無法儲存內容片段。* (SITES-22993)嚴重
* 在AEM的發佈者上，`ContentFragmentModelOmniSearchHandler`中的未關閉資源解析程式發現問題。 (SITES-24903)


#### [!DNL Content Fragments] — 管理員{#sites-admin-6522}

* 按一下電子郵件通知中的連結，會將使用者導向預設的資產檢視器或編輯器。 如此一來，即使工作流程中的資產被確定為內容片段，內容片段編輯器仍會改用。 (SITES-24338)主要


#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-6522}

* 使用包含多行文字欄位專案的內容片段時，使用GraphQL進行查詢時產生的標籤無法保留HTML中指定的格式。 例如，清單後面缺少新行。 影響是最後一個段落成為清單的一部分。 (SITES-23233)


<!-- #### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6522}

* A


#### [!DNL Content Fragments] - REST API{#sites-restapi-6522}

* A -->

#### 核心後端{#sites-core-backend-6522}

* 在AEM編寫執行個體上報告了週期性`SegmentNotFoundException`錯誤。 重新啟動作者暫時解決此問題，但需要長期修正以防止再次發生。 (SITES-22573)
* 提出有關AEM Sites中時間表功能的問題，特別是處理註解上遺失`cq:lastModified`屬性的問題。 套用AEM 6.5.20後，無法確定現有內容是否需要針對遺失的屬性進行修正，或者時間軸是否已更新為在沒有時間軸的情況下正確運作。 (SITES-21861)


#### 核心元件{#sites-core-components-6522}

* 從AEM 6.5.18升級至6.5.21後，檢查元件即時使用的功能發現問題。 嘗試捲動即時使用頁面上的其他專案時，即使在UI中看到「載入更多專案」，表格仍無法載入更多結果。 (SITES-23919)
* 在包含兩個索引標籤的AEM元件對話方塊中，必填欄位驗證時報告了問題。 索引標籤1包含RTF編輯器(RTE)和文字欄位，而索引標籤2包含路徑欄位和文字欄位。 雖然所有欄位都標示為必填(`required=true`)，錯誤通知仍錯誤地保留在索引標籤1中，即使在填寫所有必填欄位之後也是如此。 相反地，標籤2中的錯誤如預期般清除。 (SITES-23243)
* 移轉至AEM 6.5.21後，HTML範本語言`data-sly-include`陳述式不再如預期運作，特別是無法支援`appendPath`和`prependPath`運算式。 因此，即使內含資源的輸出在移轉前可正常運作，仍無法正確轉譯。 此問題會導致依賴這些運算式進行路徑操作的資源呈現失敗。 (GRANITE-52970)


<!-- #### Campaign integration{#sites-campaign-integration-6522}

* A -->


#### 體驗片段{#sites-experiencefragments-6522}

* 在清單檢視中按一下&#x200B;**Title**&#x200B;欄標題時，體驗片段未依照預期的標題排序。 觀察到畫面快速閃爍，但未排序。 (SITES-23706)主要

* 在AEM 6.5.17中，使用現成可用的功能將頁面元件轉換為體驗片段時遇到問題。 轉換後，體驗片段在編輯期間顯示為空，儘管在使用的頁面上正確顯示。 該問題源自不正確的節點建立：元件節點放在根/容器節點之外，違反了範本的結構。 您必須手動將元件節點移至正確的根/容器節點，才能恢復片段的可編輯性。 (SITES-22974)主要

* 從AEM 6.5.11移轉至6.5.20後，體驗片段上的雲端設定無法正確儲存。 雖然設定似乎儲存在`crx/de`中，但在重新開啟設定主控台時不會顯示，這表示持續性問題。 (SITES-22287)主要


<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6522}

* A -->


#### 啟動{#sites-launches-6522}

* 在AEM生產中使用標籤篩選器新增體驗片段資產時，使用者可以選取它，但在選取&#x200B;**建立語言副本**&#x200B;後遇到錯誤。 預期的行為是從標籤篩選器中選取的體驗片段資產應該要新增到翻譯專案。 (SITES-24152)主要

#### 連結檢查程式{#sites-link-checker-6522}

* LinkCheckerTask無法驗證，因為HTTP使用者端在基本驗證之前嘗試NTLM，導致Proxy在多次嘗試失敗後封鎖使用者。 系統應該改用基本驗證來對Proxy進行驗證，以允許LinkCheckerTask服務正常運作。 (SITES-25034)主要


#### MSM — 即時副本{#sites-msm-live-copies-6522}

* 將SEO Robots標籤套用至主要副本並轉出至即時副本頁面時，值在`crx/de`中正確顯示。 但是，這些值沒有反映在即時副本頁面的頁面屬性下的使用者介面中。 (SITES-23475)主要
* 嘗試透過使用者介面提升Launch時，系統會顯示與Launch相關的錯誤。 「提升啟動」精靈保持空白，使提升流程無法完成。 (SITES-19718)
* 嘗試建立即時副本及執行轉出後，AEM中的體驗片段出現問題。 使用者嘗試從轉出畫面導覽回體驗片段管理畫面時，發生`NotFound`錯誤的問題。 (SITES-21933)


#### 頁面編輯器{#sites-pageeditor-6522}

* 「復原」按鈕除了將文字變更為最新版本外，還變更了元件的位置。 (SITES-17465)封鎖程式
* 貼上複製的容器元件後，該元件會以視覺化方式顯示兩次，導致頁面上出現三個例項。 然而，重新整理頁面後，重複專案消失，表示問題可能是暫時的視覺問題。 (SITES-21890)主要
* 使用鍵盤的Tab或Shift+Tab鍵導覽「元件」左窗格時，無法清楚看到多個文字元素，無論是視覺上還是定位鍵模式皆然。 此問題會影響協助工具，導致在鍵盤導覽期間難以識別這些元件或與其互動。 (SITES-2266)

#### 複製{#sites-replication-6522}

* 在AEM 6.5.18和6.5.19中，停用上層頁面時，系統會為每個子頁面產生多個停用請求。 此問題也會中斷大量取消發佈GraphQL端點。 (NPR-42075和NPR42010)嚴重


### [!DNL Assets]{#assets-6522}

* 使用「連線Assets」功能時，在AEM Assets中進行的更新不會反映在AEM Sites環境中。 (ASSETS-42344)主要<!-- Leave the "MAJOR" status priorities in place. -->
* (ASSETS-41158)主要
* 使用API上傳資產導致`unclosed resource resolver`錯誤訊息。 (ASSETS-41049)主要
* (ASSETS-40384)主要
* 在AEM 6.5.19版中，從搜尋面板結果中移除一個選項時，也會取消勾選所有其他可用的核取方塊。 (ASSETS-37335)主要
* 執行大量中繼資料匯出作業時，會在Excel輸出中顯示垃圾值。 (ASSETS-37260)主要
* 在AEM 6.5.19版中，當您上傳UTF-8格式的SVG檔案時，輸出會變得模糊。 (ASSETS-36616)主要
* 連線的Assets組態中缺少`Fetch original rendition for Dynamic Media Connected Assets`選項。 (ASSETS-41726)
* 即使您未定義必要欄位的值，也會儲存資產屬性。 (ASSETS-37914)

#### [!DNL Dynamic Media]{#assets-dm-6522}

* 當視訊上傳至Dynamic Media失敗時，生產問題會中斷移轉程式，並在使用者介面中顯示程式失敗錯誤。 (ASSETS-36038)


### [!DNL Forms]{#forms-65220}

在排程的[!DNL Experience Manager] Service Pack發行日期一週後，[!DNL Experience Manager] Forms中的修正會透過個別附加元件套件傳送。 在此案例中，AEM 6.5.22.0 Forms附加元件套件發行預計於2024年11月28日星期四推出。 此部分會在發行後新增Forms修正和增強功能的清單。


<!-- #### [!DNL Adaptive Forms] {#forms-6522}

* A


#### [!DNL Forms Designer] {#forms-designer-6522}

* A -->


### Foundation {#foundation-6522}

* 在AEM Assets主控台中，嘗試重新排序DITA檔案時發生問題。 路徑瀏覽器對話方塊頂端的階層連結錯誤地顯示節點名稱，而不是根父級的節點標題。 只有在階層連結中選取專案後，才會顯示正確的節點標題，表示暫時顯示錯誤。 (NPR-42106)主要


<!-- #### Apache Felix {#foundation-apachefelix-6522}


* A

#### Campaign{#foundation-campaign-6522}

* A


#### Cloud Services{#foundation-cloudservices-6522}

* A -->


#### Communities {#foundation-communities-6522}

* 從AEM 6.5.19升級至6.5.20後，發生呼叫`UgcSearch`後，`Connection evic`執行緒無法正確關閉的問題。 此問題會在生產環境中觀察到，並會導致這些執行緒隨著時間持續存在和累積，這可能會影響效能。 (NPR-42019)主要


<!-- #### Content distribution{#foundation-content-distribution-6522}

* A -->


#### CRX {#foundation-crx-6522}

* 依據CRX封裝管理員左側功能表中的&#x200B;**群組**&#x200B;的排序無法運作。 (GRANITE-53277)
* AEM中的「封裝管理員」預設會限制安裝較低封裝版本，但允許強制安裝較舊版本。 不過，使用強制安裝選項可能會干擾透過標準管道的未來安裝。 例如，如果已安裝1.21版並新增1.24版，則安裝會成功，並列出兩個版本。 不過，嘗試安裝1.22版而非1.24版會透過管道失敗，但如果強制安裝則會運作，並列出所有版本。 同樣地，如果版本1.24已存在，則會封鎖安裝1.23版，因為管道不允許降級。 (GRANITE-53263)


#### Granite{#foundation-granite-6522}

* 快照套件是使用CURL命令安裝在AEM中。 在安裝期間，JCR安裝程式會透過OSGI安裝程式掃描套件，以確保不需要其他OSGI套件組合或設定。 如果封裝版本包含「SNAPSHOT」，OSGI安裝程式會觸發VLT建立對應的快照封裝。 不過，由於每個AEM編寫執行個體都會執行自己的OSGI安裝程式，因此兩個執行個體可能會嘗試同時產生快照，導致存放庫內的工作階段衝突。 (NPR-42003)主要
* 使用AEM 6.5.21的`ScriptDependencyResolver`中存在鎖定競爭。 (GRANITE-53181)主要
* 將AEM升級至6.5.21後，在Sightly (HTL)語法（例如`data-sly-use`）中使用相對路徑時會發生問題。 (GRANITE-53080)主要


#### 整合{#foundation-integrations-6522}

* 新增Cloud Service使用者介面的法律歸因宣告。 (FORMS-16373)
* 為&#x200B;**fd-cloudservice**&#x200B;使用者新增讀取許可權，以存取hCaptcha和Turnstile設定，讓使用者擷取驗證碼轉譯和驗證所需的使用者端ID和使用者端密碼。 此外，已實施存取控制清單模型來管理對這些設定的存取。 (FORMS-16360)


#### 本地化{#foundation-localization-6522}

* 在![錘子圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Hammer_18_N.svg)工具> **安全性** > ![使用者圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_User_18_N.svg) **使用者**&#x200B;中，在「使用者管理」頁面上，表格的&#x200B;**狀態**&#x200B;欄中的資料垂直顯示。 (GRANITE-48304)


<!-- #### Oak {#foundation-oak-6522}

* A -->


#### Platform{#foundation-platform-6522}

* AEM 6.5.18中引入的企業資訊管理追蹤在計算產品採用分數時造成異常。 Adobe量度資料庫會覆寫Omega追蹤資料庫所提供的使用者資料，進而造成此問題。 因此，許多AEM Sites和AEM Assets客戶的採用分數從2024年2月起降至零。 (CQ-4358438)嚴重
* 在生產環境中，發現記憶體回收行程未正確處理標籤。 具體而言，當標籤移動或重新命名時，記憶體回收行程無法更新`cq:MovedTo`屬性，導致標籤從頁面中消失。 (CQ-4358293)主要
* AEM 6.5.19中的ContextHub問題導致區段在內容路徑新增到AEM執行個體時無法正確解析。 該問題尤其會影響頁面元件產生之JavaScript物件中的URL欄位，其中缺少必要的內容路徑前置詞。 此遺漏會使區段無法如預期運作。 (SITES-21852)
* 更新AEM Quickstart以使用程式庫`commons-collections-3.2.2-adobe-2`。 此更新可確保應用程式能夠繼續順利執行。 (NPR-42150)
* AEM 6.5中的SMTP OAuth2設定與AEM as a Cloud Service中使用的差異極大。 為了簡化設定並確保一致性，AEM 6.5中的設定必須符合AEM as a Cloud Service中使用的標準。 (GRANITE-53273)
* 當您按一下![指南針圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Compass_18_N.svg) > ![專案圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Project_18_N.svg)專案，然後將滑鼠指標停留在![導軌左側圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_RailLeft_18_N.svg) ![向下V形圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg)時，發現了一個問題，工具提示文字「僅內容」前出現一個抑音符號。 (CQ-4356633)

#### 安全性{#foundation-security-6522}

* AEM中的過時JSAFE密碼編譯程式庫（版本6.0.0）發生問題。 AEM 6.5.22中包含有JSAFE 6.2.5版的修補套件組合。 (NPR-42006)嚴重
* 在XSS檢查期間驗證允許的通訊協定時，處理常式會與「http」和「https」比較。 但是，URL物件的`protocol`屬性傳回這些帶有結尾冒號的值，例如`http:`和`https:`。 此不相符專案會導致驗證問題。 為確保正確剖析，協定檢查需要說明冒號或相應地調整比較邏輯。  (NPR-42119)
* 在IBM®WebSphere®Liberty Profile和Semeru Java 8.0上安裝AEM 6.5.21 (先前版本為AEM 6.5.19)後，無法開啟任何頁面。 錯誤記錄檔指出與需要不同套件組合的servlet版本相關的問題。 若要解決此問題，必須還原`org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`的相依性，因為它與問題有關。 (NPR-42116)
* 數個瀏覽器正在逐步停止支援&#x200B;**SameSite=None** Cookie （用於允許跨網站存取Cookie）。 作為替代方法，正在引入&#x200B;**已分割的Cookie**。 這些Cookie會依其使用環境來隔離儲存空間，藉由防止跨網站追蹤來增強隱私權和安全性，同時仍允許Cookie在特定分割內運作，例如內嵌的第三方內容。 (GRANITE-51953)


<!-- #### Sling{#foundation-sling-6522}

* A -->


#### 翻譯{#foundation-translation-6522}

* 新增對核心元件中預設翻譯規則近期變更的支援。 (NPR-42029)嚴重
* 在AEM Forms中匯出XLIFF檔案時發現問題。 使用&#x200B;**將選取專案匯出為XLIFF （僅限字串）**&#x200B;選項時，無法一致地維持元件順序。 但是，針對特定語言匯出XLIFF時，順序仍保持正確。 提供兩個檔案來示範問題： **DE-CH_Export.xliff** （順序正確）和&#x200B;**String_Export.xliff** （順序不正確）。 (NPR-42118)主要


#### 使用者介面{#foundation-ui-6522}

* `coralui-component-dialog`正在變更`cq-dialog-actions`的位置，可能會影響AEM對話方塊中動作按鈕的版面配置或行為。 (NPR-42294)阻斷因素
* AEM中的檢色器功能發生問題。 存取時，會顯示空白強制回應視窗，避免顏色選取。 在Stage環境中安裝AEM 6.5.20後，就開始發生此問題。 檢色器在&#x200B;*之前*&#x200B;正確運作以進行更新。 (NPR-42163)
* 在![錘子圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Hammer_18_N.svg) **工具** > **工作流程** > **模型** >選取任何模型> **啟動工作流程**&#x200B;中，**執行工作流程**&#x200B;對話方塊的[裝載]欄位中缺少[瀏覽]圖示。 (NPR-42162)


<!-- #### WCM{#foundation-wcm-6522}

* A


#### Workflow{#foundation-workflow-6522}

* A 


## Install [!DNL Experience Manager] 6.5.22.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.22.0需要[!DNL Experience Manager] 6.5。如需詳細指示，請參閱[升級檔案](/help/sites-deploying/upgrade.md)。<!-- UPDATE FOR EACH NEW RELEASE -->
* Service Pack下載專案可在Adobe[軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.21.0.zip)上取得。
* 在具有MongoDB和多個執行個體的部署上，使用封裝管理員在其中一個作者執行個體上安裝[!DNL Experience Manager] 6.5.22.0。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe不建議您移除或解除安裝[!DNL Experience Manager] 6.5.22.0套件。 因此，在安裝套件之前，您應該建立`crx-repository`的備份，以備您必須復原它時使用。<!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### 在[!DNL Experience Manager] 6.5上安裝Service Pack{#install-service-pack}

1. 如果執行個體處於更新模式（從舊版更新執行個體時），請在安裝前重新啟動執行個體。 如果執行個體的目前運作時間很高，Adobe建議重新啟動。

1. 安裝之前，請為您的[!DNL Experience Manager]執行個體建立快照或全新備份。

1. 從[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.21.0.zip)下載Service Sack。<!-- UPDATE FOR EACH NEW RELEASE -->

1. 開啟封裝管理員，然後選取&#x200B;**[!UICONTROL 上傳封裝]**&#x200B;以上傳封裝。 如需詳細資訊，請參閱[封裝管理員](/help/sites-administering/package-manager.md)。

1. 選取封裝，然後選取&#x200B;**[!UICONTROL 安裝]**。

1. 若要更新S3聯結器，請在安裝Service Pack後停止執行個體，將現有聯結器取代為安裝資料夾中提供的新二進位檔案，然後重新啟動執行個體。 請參閱[Amazon S3資料存放區](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)。

>[!NOTE]
>
>Service Pack安裝期間，Package Manager UI上的對話方塊有時會退出。 Adobe建議您先等待錯誤記錄穩定下來，再存取部署。 等待與更新程式套件組合解除安裝相關的特定記錄，再確認安裝成功。 此問題通常發生在[!DNL Safari]瀏覽器中，但可能間歇性地發生在任何瀏覽器中。

**自動安裝**

您可以使用兩種不同的方法來安裝[!DNL Experience Manager] 6.5.22.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* 伺服器上線時，請將封裝放入`../crx-quickstart/install`資料夾。 套件會自動安裝。
* 使用封裝管理員](/help/sites-administering/package-manager.md#package-share)的[HTTP API。 使用`cmd=install&recursive=true`安裝巢狀套件。

>[!NOTE]
>
>Experience Manager6.5.22.0不支援Bootstrap安裝。<!-- UPDATE FOR EACH NEW RELEASE -->

**驗證安裝**

若要瞭解經過認證可搭配此版本使用的平台，請參閱[技術需求](/help/sites-deploying/technical-requirements.md)。

1. 產品資訊頁(`/system/console/productinfo`)會在[!UICONTROL 已安裝產品]下顯示更新的版本字串`Adobe Experience Manager (6.5.22.0)`。<!-- UPDATE FOR EACH NEW RELEASE -->

1. 在OSGi主控台中，所有OSGi套件組合均為&#x200B;**[!UICONTROL 作用中]**&#x200B;或&#x200B;**[!UICONTROL 片段]** （使用Web主控台： `/system/console/bundles`）。

1. OSGi套件`org.apache.jackrabbit.oak-core`是1.22.20或更新版本（使用Web主控台： `/system/console/bundles`）。<!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE. CHECK WITH SAMEER DHAWAN -->

### 安裝[!DNL Experience Manager] Forms的Service Pack{#install-aem-forms-add-on-package}

如需在Experience Manager Forms上安裝Service Pack的說明，請參閱[Experience Manager Forms Service Pack安裝說明](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)。

>[!NOTE]
>
>調適型表單功能 (適用於 [AEM 6.5 QuickStart](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/implementing/deploying/deploying/deploy)) 僅用於探索和評估目的。若要供生產使用，必須獲得 AEM Forms 的有效許可；調適型表單的功能需要適當許可才可使用。

### 安裝Experience Manager內容片段的GraphQL索引套件{#install-aem-graphql-index-add-on-package}

使用GraphQL的客戶必須安裝[Experience Manager內容片段搭配GraphQL索引套件1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip)。

如此一來，您就可以根據使用者實際使用的功能，新增必要的索引定義。

無法安裝此套件可能會導致GraphQL查詢變慢或失敗。

>[!NOTE]
>
>每個執行個體僅安裝此套件一次；不需要隨每個Service Pack重新安裝。

### UberJar{#uber-jar}

[!DNL Experience Manager] 6.5.22.0的UberJar可在[Maven中央存放庫](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.21/)中使用。<!-- CHECK FOR UPDATE EACH NEW RELEASE -->

若要在Maven專案中使用UberJar，請參閱[如何使用UberJar](/help/sites-developing/ht-projects-maven.md)，並在您的專案POM中包含下列相依性： <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.22</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar和其他相關成品可在Maven中央存放庫上使用，而不是Adobe公共Maven存放庫(`repo.adobe.com`)。 主要UberJar檔案已重新命名為`uber-jar-<version>.jar`。 因此，`dependency`標籤沒有`classifier`，其值為`apis`。


## 過時和移除的功能{#removed-deprecated-features}

請參閱[已過時和已移除的功能](/help/release-notes/deprecated-removed-features.md/)。

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

   1. 從`crx-quickstart/repository/`中刪除以下兩個資料夾

      * `cache`
      * `diff-cache`

   1. 安裝Service Pack，或重新啟動Experience Manageras a Cloud Service。
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
   * 「當使用Adobe Target API （IMS驗證）在[!DNL Experience Manager]中設定Target Standard整合時，將體驗片段匯出至Target會導致建立錯誤的選件型別。 Target會建立多個具有「HTML」/來源「Adobe Target Classic」型別的選件，而不是「體驗片段」/來源「Adobe Experience Manager」。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在`granite/operations/maintenance`找不到維護期間。
   * 使用彙總函式(例如SUM、MAX和MIN)時，Adaptive Form伺服器端驗證會失敗(CQ-4274424)。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` ：在`granite/operations/maintenance`找不到維護期間。
   * 透過Shoppable Banner檢視器預覽資產時，不會顯示Dynamic Media互動影像中的熱點。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` ：等待登入變更完成解除登入逾時。

* 從AEM 6.5.15開始，```org.apache.servicemix.bundles.rhino```套件提供的Rhino JavaScript Engine有新的提升行為。 使用嚴格模式(```use strict;```)的指令碼必須宣告其正確的變數。 否則，它們不會執行，並最終擲回執行階段錯誤。

* 透過正式更新套件安裝標籤相關的現成可用內容會將`/content/cq:tags`節點的languages屬性重設為預設值。 此動作適用於Service Pack、Security Service Pack、Extended Feature Pack、Cumulative Feature Pack、修補程式等。 因此，在安裝之前，必須從屬性新增它。

### AEM Sites的已知問題 {#known-issues-aem-sites-6522}

* 內容片段 — 預覽因DoS保護大型片段樹狀結構而失敗。 請參閱有關預設GraphQL查詢執行器組態選項](https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-23945)的[KB文章(SITES-17934)


### AEM Forms的已知問題 {#known-issues-aem-forms-6522}


* 安裝AEM Forms JEE Service Pack 21 (6.5.21.0)後，如果在`<AEM_Forms_Installation>/lib/caching/lib`資料夾(FORMS-14926)下找到Geode jar `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)`的重複專案，請執行以下步驟以解決問題：

   1. 停止儲位（如果它們正在執行）。
   1. 停止AEM伺服器。
   1. 移至`<AEM_Forms_Installation>/lib/caching/lib`。
   1. 移除除`geode-*-1.15.1.2.jar`以外的所有Geode修補程式檔案。 確認只有具有`version 1.15.1.2`的Geode jar存在。
   1. 在管理員模式中開啟命令提示字元。
   1. 使用`geode-*-1.15.1.2.jar`檔案安裝Geode修補程式。

* 如果使用者嘗試預覽具有已儲存XML資料的草稿信件，它會在某些特定信件中陷入`Loading`狀態。 若要下載及安裝Hotfix，請參閱[Adobe Experience Manager Forms Hotfix](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)文章。 (FORMS-14521)

* 升級至AEM Forms Service Pack 6.5.21.0後，`PaperCapture`服務無法在PDF上執行OCR （光學字元辨識）作業。 此服務不會產生PDF或記錄檔形式的輸出。 若要下載及安裝Hotfix，請參閱[Adobe Experience Manager Forms Hotfix](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)文章。 (CQDOC-21680)

* 當使用者從AEM 6.5 Forms Service Pack 18或19升級為Service Pack 20或21時，他們遇到JSP編譯錯誤。 此錯誤會阻止他們開啟或建立最適化表單。 它也會導致其他AEM介面發生問題。 這些介麵包含頁面編輯器、AEM Forms UI、工作流程編輯器和系統概覽UI。 (FORMS-15256)

  如果您遇到這類問題，請執行以下步驟來解決問題：
   1. 導覽至CRXDE中的目錄`/libs/fd/aemforms/install/`。
   1. 刪除名稱為`com.adobe.granite.ui.commons-5.10.26.jar`的組合。
   1. 重新啟動AEM伺服器。

* 使用Forms附加元件更新至AEM Forms Service Pack 20 (6.5.20.0)後，依賴舊版Adobe Analytics Cloud Service （使用認證型驗證）的設定會停止運作。 此問題導致Analytics規則無法正確執行。 若要下載及安裝Hotfix，請參閱[Adobe Experience Manager Forms Hotfix](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)文章。 (FORMS-15428)

* 當使用者在JEE伺服器上更新至AEM Forms Service Pack 20 (6.5.20.0)，並使用輸出服務產生PDF時，PDF會出現協助工具問題。 若要下載及安裝Hotfix，請參閱[Adobe Experience Manager Forms Hotfix](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)文章。 (LC-3922112)
* 當使用者使用JEE上的輸出服務產生標籤PDF時，會顯示「不適當的結構警告」。 若要下載及安裝Hotfix，請參閱[Adobe Experience Manager Forms Hotfix](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)文章。 (LC-3922038)
* 在AEM Forms JEE上提交表單時，會從資料中移除重複的XML元素例項。 若要下載及安裝Hotfix，請參閱[Adobe Experience Manager Forms Hotfix](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)文章。 (LC-3922017)
* 當Linux®環境中的使用者在HTML中轉譯最適化表單（在JEE上）時，它將無法正確轉譯。 若要下載及安裝Hotfix，請參閱[Adobe Experience Manager Forms Hotfix](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)文章。 (LC-3921957)
* 當使用者使用AEM Forms JEE上的輸出服務將XTG檔案轉換為PostScript格式時，它會失敗並出現錯誤： `AEM_OUT_001_003: Unexpected Exception: PAExecute Failure: XFA_RENDER_FAILURE`。 若要下載及安裝Hotfix，請參閱[Adobe Experience Manager Forms Hotfix](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)文章。 (LC-3921720)
* 在JEE伺服器上升級至AEM Forms Service Pack 18 (6.5.18.0)後，當使用者提交表單時，將無法轉譯HTML5或PDF forms，並且XMLFM會當機。 若要下載及安裝Hotfix，請參閱[Adobe Experience Manager Forms Hotfix](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)文章。 (LC-3921718)
* 在互動式通訊代理程式UI的列印預覽中，所有欄位值都會不一致地顯示貨幣符號（例如美元符號$）。 對於最多999的值會顯示它，但對於1000或以上的值則遺失。 (FORMS-16557)
* 互動式通訊中巢狀配置片段XDP的任何修改都不會反映在IC編輯器中。 (FORMS-16575)
* 在互動式通訊代理程式UI的列印預覽中，部分計算值無法正確顯示。 (FORMS-16603)
* 在「列印預覽」中檢視信函時，內容會變更。 也就是說，部分空格會消失，而某些字母會取代為「x」(FORMS-15681)

## 包含的OSGi套件組合和內容套件{#osgi-bundles-and-content-packages-included}

下列文字檔案列出此[!DNL Experience Manager] 6.5 Service Pack發行版本中包含的OSGi套件組合和內容套件：

* [Experience Manager6.5.22.0](/help/release-notes/assets/65210-bundles.txt)中包含的OSGi套件組合清單<!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager6.5.22.0](/help/release-notes/assets/65210-packages.txt)中包含的內容套件清單<!-- UPDATE FOR EACH NEW RELEASE -->

## 受限制的網站{#restricted-sites}

這些網站僅供客戶使用。 如果您是客戶且需要存取權，請聯絡您的Adobe客戶經理。

* [產品下載網址為licensing.adobe.com](https://licensing.adobe.com/)
* [連絡Adobe客戶支援](https://experienceleague.adobe.com/en/docs/customer-one/using/home)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 產品頁面](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5檔案](https://experienceleague.adobe.com/en/docs/experience-manager-65)
>* [訂閱Adobe優先順序產品更新](https://www.adobe.com/tw/subscription/priority-product-update.html)
