---
title: '[!DNL Adobe Experience Manager] 6.5的發行說明'
description: 尋找 [!DNL Adobe Experience Manager] 6.5 的版本資訊、新增功能、安裝方法和詳細變更清單。
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
contentOwner: Rick Brough
role: User,Admin,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: ed762d86-a04b-452b-a08f-86359bb8ff27
    internal-label: Configuration and operations
subfeature_v2:
  - id: c21ccc2b-e0c8-4853-bf41-f12259ed93f8
    internal-label: Release information
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 383a6624329826101fc85861ee31d34ae7e59d71
workflow-type: tm+mt
source-wordcount: '7975'
ht-degree: 3%
---
# [!DNL Adobe Experience Manager] 6.5最新Service Pack發行說明 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!--
DO NOT DELETE THIS HIDDEN NOTE!      DO NOT DELETE THIS HIDDEN NOTE!
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, May 29, 2025. In addition, a list of Forms fixes and enhancements is added to this section.
-->

## 發行摘要 {#release-information}

| 產品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.26.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 類型 | Service Pack 發行 |
| 日期 | 2026年11月12日<!-- UPDATE FOR EACH NEW RELEASE --> |
| 下載 URL | [軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.26.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

<!-- REWRITE AI GENERATED SUMMARY OF NOTES BELOW FOR EACH NEW SERVICE PACK RELEASE -->

Experience Manager 6.5.26.0包含新功能、客戶要求的重要增強功能和錯誤修正。 此外，還包括自2019年4月起以6.5為基礎推出的協助工具、本地化、效能、穩定性及安全性改善專案。

Service Pack 26的關鍵重點包括：

* 安全性。 兩個關鍵修正關閉中繼資料編輯器中的伺服器端範本插入弱點，以及Coral UI servlet中的跨網站指令碼(XSS)違規。
* C2PA相容性。 Assets現在會偵測「更新資產」工作流程產生的C2PA憑證和簽署轉譯。 簽署會在每個執行個體本機執行，不支援專用或客戶擁有的簽署基礎結構。
* 協助工具。 超過25項修正可協助頁面編輯器和網站主控台符合WCAG對比、鍵盤和熒幕助讀程式的需求。
* 本地化。 有數十項修正可翻譯字串，並修正網站、Assets、安全性和營運中的版面問題。
* 可靠性。 修正了傳統UI中，發佈執行個體上的GraphQL鎖定爭用、MSM轉出、RTF編輯器工具列動作和頁面啟用問題。
* Analytics。 Launch整合會在Analytics 1.4生命週期結束前（2026年8月31日）使用Adobe Analytics 2.0 API。

>[!IMPORTANT]
>
>Adobe提供AEM 6.5 LTS的每季Service Pack，以及支援的Service Pack適用的累積安全性修正策略，以因應此區域更新的頻率。
>
> 對於使用傳統AEM 6.5的客戶，Service Pack 26可提供連續性，而支援和維護則會透過AEM 6.5 LTS工作流程繼續。 標準（2027年2月）和延伸（2028年2月）支援涵蓋Service Pack 26，其中僅接收安全性修正。
>
>Adobe提供的資源可協助您轉換至AEM 6.5 LTS或AEM as a Cloud Service，並使用最新的AI創新技術來提高生產力並最佳化新受眾。

<!-- UPDATE FOR EACH NEW RELEASE -->

## 修正Service Pack 26中的問題、增強功能和改善 {#fixed-issues}

<!-- 6.5.25.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->


### [!DNL Sites]{#sites-6526}

#### 協助工具 {#sites-accessibility-6526}

* 作者僅可使用鍵盤新增、移動及移除元件。 拖放互動需要指標，因此無法符合WCAG 2.1.1鍵盤標準。 編輯器現在提供「插入」元件快顯視窗、「剪下並貼上」和「刪除」等鍵盤可操作的同等功能。 (SITES-25359)

* 作者現在可以在文字元件內嵌選單中看到作用中的格式(「T」)按鈕。 在作者套用粗體或斜體格式後，按鈕圖示在深灰色背景中仍保持深色，並錯過WCAG 2.1 AA的最低對比率4.5:1。 更新的CSS會點亮圖示，回覆先前提供的Service Pack對比。 (SITES-51864)

* 現在，當您從「影像」下拉式清單中選擇「段落」後，「頁面編輯器」中的「Assets」標籤會在「選取元件」下拉式清單中顯示翻譯字串。 之前，由於本地化資源缺乏「其他」字串，因此顯示為英文。 更新的字典提供所有地區設定的翻譯。 (SITES-24525)




* 頁面編輯器中的ContextHub iframe現在有描述性標題屬性。 先前，`contexthub-ui-iframe`元素沒有標題，因此熒幕助讀程式的使用者在焦點移至它時無法識別它。 標題現在會顯示在每個編輯器頁面和檢視上，包括畫布、側邊欄和版面預覽。 (SITES-24650)
* Sites Console篩選邊欄中的篩選按鈕未在已儲存的搜尋和選取搜尋目錄欄位上方新增可見標籤。 稽核報告指出焦點離開按鈕、按下按鍵或按一下按鈕時，標籤隨即出現。 測試無法重現行為，因此不需要變更。 (SITES-24706)
* 「網站」主控台應用程式導覽中的連結現在會更清晰可見。 連結文字元合4.5:1的對比率，但細字型粗細和較小尺寸使連結難以看見。 較大的字型粗細與大小讓視力不佳的使用者更容易閱讀文字。 (SITES-24723)
* 熒幕助讀程式不再在「使用者偏好設定」強制回應視窗的工具提示內容前宣告「空白」。 先前資訊圖示使用`role="tooltip"`搭配`aria-labelledby`參考，因此NVDA會先讀取空白標籤。 圖示現在使用`role="button"`和`aria-label`的「資訊」，而變更會套用至共用此模式的Coral表單元件。 (SITES-24732)
* 「刪除」強制回應視窗中的「刪除」按鈕現在符合WCAG 1.4.3的4.5:1對比度要求。 先前，作者選取專案並按一下「動作工具列」中的「刪除」後，紅色背景的白色文字會提供3.9:1的比率。 較深的按鈕顏色讓視力不佳的作者看得懂標籤。 (SITES-24772)
* Sites主控台參照邊欄中的參照標題現在使用標題元素而非`div`。 以前，熒幕助讀程式無法將文字宣告為標題，因此使用者無法依標題導覽。 標題也會顯示在初始「參照」檢視的頂端。 (SITES-24967)
* Sites控制檯篩選邊欄中摺疊式功能表按鈕的焦點指標現在符合WCAG 1.4.11的3:1對比度要求。 之前，藍色指示燈在背景中顯示了2.3:1的比率，這使得鍵盤使用者很難找到「標籤」摺疊式功能表按鈕。 更新後的色彩可為鍵盤使用者提供清晰的焦點提示。 (SITES-24986)
* Sites主控台篩選器邊欄中選項按鈕的焦點指標現在符合WCAG 1.4.11的對比度要求3:1。 之前，淡藍色指示器在背景顯示的比例為1.7:1。 鍵盤使用者現在可以在「修改日期」設定追蹤器中追蹤其位置。 (SITES-24987)
* 在「頁面編輯器」側邊欄中，路徑和標籤欄位旁的「選取」按鈕不再使用核取方塊圖示。 之前，圖示建議進行切換，但啟動按鈕會開啟包含「樹狀目錄」的強制回應視窗。 「選取」按鈕現在會正確傳達其功能，同樣適用於「影像」和「預告」模式。 (SITES-25210)
* 熒幕助讀程式現在會略過頁面編輯器側邊欄中的資產縮圖影像。 之前，每個影像都附有複製可見資產名稱的替代文字，因此使用者會聽到相同的文字兩次。 空白`alt`屬性將影像標示為裝飾性，並將名稱保留在卡片標題中。 (SITES-25213)
* 熒幕助讀程式會將側邊欄「元件」清單識別為清單。 稽核將專案報告為不相關的元素，但測試確認標籤使用清單元素和清單專案。 不需要變更程式碼。 (SITES-25214)
* 「頁面編輯器」側邊欄中元件的資訊圖示會變大且更容易檢視。 先前，圖示使用的超小尺寸約12畫素，視力缺佳的使用者很難看清。 圖示現在使用中等大小。(SITES-25217)
* 註解強制回應中「色票」按鈕上的焦點指示器現在與按鈕有明顯區別。 以前，指示器與色票顏色相符。 這讓鍵盤使用者很難看到哪個按鈕具有焦點。 位移可讓指標在背景中擁有足夠的對比度，並保持其清晰可見。 (SITES-25253)
* 時間扭曲強制回應視窗中的「日期」欄位不再包含`aria-haspopup="dialog"`。 之前，熒幕助讀程式會宣佈欄位會開啟對話方塊，即使它沒有開啟。 移除屬性可為熒幕助讀程式使用者提供準確的資訊。 (SITES-25263)
* 「人口統計」工具列上的文字標籤（例如「建議」）現在已符合WCAG 1.4.3的4.5:1對比度要求。 以前，在預覽模式下，深灰色背景上的灰色文字會提供2.8:1的比率。 較暗或較淺的文字（視背景而定）可讓每個標籤都能看得懂。 (SITES-25307)
* 「人口統計」工具列上「Commerce」、「角色」和「裝置」按鈕的焦點指標現在已符合WCAG 1.4.11的3:1對比度要求。 之前，指標在工具列背景顯示的比例為1.9:1。 鍵盤使用者現在可以追蹤其位置。 (SITES-25308)
* 作者在「人口統計」工具列文字欄位中輸入的文字，現在已符合WCAG 1.4.3的對比要求4.5:1。 之前，灰色背景的白色文字在欄位中產生2.9:1的比率，例如在預覽模式中的設定檔下拉式清單`displayName`欄位。 更新後的顏色讓視力缺佳的作者可讀取輸入的值。 (SITES-25318)
* 現在當焦點達到Teaser、影像和轉盤對話方塊中的核取方塊時，熒幕閱讀器會閱讀說明工具提示。 以前，文字與核取方塊缺乏程式化關聯，因此使用者無法聽到指示。 `aria-describedby`屬性現在會將每個核取方塊連結至其說明。 (SITES-25364)
* 熒幕助讀程式現在會朗讀RTF編輯器中作用中的段落格式按鈕。 先前，從清單中選取選項時，輔助技術無法指出目前的選擇。 使用中的按鈕現在會帶入`aria-current="true"`，而使用中的超連結目標選項會帶入`aria-selected="true"`。 (SITES-25367)
* Sites主控台清單檢視的表格標題中的「排序」按鈕現在符合WCAG 1.4.11的3:1對比要求。 以前，淺灰色圖示相對於頁首背景顯示1.5:1的比率。 較深的圖示顏色會讓視力缺佳的作者看到這些按鈕。 (SITES-25372)
* 當焦點移至「篩選」欄位時，頁面編輯器側邊欄中的「Assets」索引標籤不再重新載入。 先前，將定位鍵插入空白欄位會觸發重新載入，而熒幕助讀程式每次都會宣佈載入訊息。 現在只有在變更篩選值並按Enter鍵後，標籤才會重新載入。 (SITES-25377)
* 在「註解」強制回應視窗中選取的色票圖示現在符合WCAG 1.4.11的3:1對比度要求。 先前，白色核取記號對黃色、橘色和綠色色票的比率低至1.58:1。 更新的圖示可為視力缺佳的作者提供明確的指標。 (SITES-25523)
* 頁面編輯器側面板中的「元件」清單不再使用鍵盤焦點。 鍵盤使用者在內容視窗中使用控制項來選取和移動元件，因此側面板清單會重複該功能。 元件篩選器下的註記會通知鍵盤使用者在何處尋找控制項。 (SITES-40752)


#### 管理員使用者介面{#sites-adminui-6526}


#### 傳統 UI{#sites-classicui-6526}

* 作者可以在傳統UI Sites主控台(`siteadmin.html`)中再次啟用頁面。 以前，「啟動頁面」按鈕會無限期地顯示「載入」旋轉圖示，而且永遠不會觸發復寫，因為失敗的追蹤指令碼暫停了點選處理常式。 點按處理常式現在會在沒有錯誤的情況下執行，並完成啟動。 (SITES-52165)
* 印尼文語言代碼現在會在語言副本屬性中顯示為ID。 先前，參考邊欄針對印尼語言根下的頁面顯示舊版程式碼IN 。 cq-wcm-core套件組合更新會修正值，使程式碼符合ISO標準。 (SITES-4491)

<!--
#### Component Console{#sites-component-console-6526}



#### [!DNL Content Fragments]{#sites-contentfragments-6526}



#### [!DNL Content Fragments] - Admin{#sites-admin-6526}
-->


#### [!DNL Content Fragments] — 片段編輯器{#sites-fragments-editor-6526}

* 「編輯內容片段」按鈕會立即出現，供內容片段編輯器中的每個多欄位參考使用。 以前，按鈕會一直隱藏，直到作者儲存父片段為止，而且在他們開啟路徑瀏覽器後沒有任何反應。 編輯器現在會在首次轉譯時建置動作清單，讓作者無需額外步驟即可開啟參照的片段。 (SITES-43733)

* 中文、日文和韓文字元在建立內容片段對話方塊預留位置中不再以斜體顯示。 先前，斜體樣式套用至&#x200B;**Assets** > **檔案**&#x200B;底下的CJK字元，造成文字難以閱讀。 更新的樣式會略過CJK語言的斜體。 (SITES-43548)
* Granite UI更新後，內容片段編輯器會正確驗證欄位。 最近的Granite UI變更導致回歸，因此編輯器使用者端程式庫不再符合新的驗證行為。 已調整的程式庫和測試可解決不符問題。 (SITES-46650)


#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-6526}

* 對內容片段的GraphQL查詢現在透過OpenAPI Assets識別對Dynamic Media的RemoteRef參考。 先前，當AEM 6.5網站使用AEM as a Cloud Service Assets時，查詢失敗並出現「持續的查詢驗證錯誤」，且未傳回任何資產資料。 回應現在包含存放庫ID和資產ID，因此使用者端可建立傳遞URL。 (SITES-48507)

* 發佈執行個體在GraphQL高流量期間仍會保持回應。 在`GraphQLServiceImpl`中鎖定爭用會延遲結構描述方法的要求處理執行緒，這會減緩要求並需要重新啟動。 改善的同步化可解決效能限制並維持網站和行動應用程式的可用性。 (SITES-48699)

* 重新載入頁面後，「GraphQL端點」頁面上的訊息仍維持本地化狀態。 先前，當您建立和刪除端點時，「找不到端點」訊息會以您的語言顯示，但在重新載入後會回覆成英文。 頁面現在會在每次造訪時載入翻譯字串。 (SITES-43586)


<!--
#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6526}
-->


#### [!DNL Content Fragments] — 模型與模型編輯器{#sites-models-model-editor-6526}

* 當設定名稱包含本地化字元（例如「espanol テスト」）時，內容片段模型的縮圖會顯示在&#x200B;**工具** > **一般** > **內容片段模型**&#x200B;中。 先前，上傳的縮圖未出現，因為字元導致路徑中發生錯誤。 更新的處理可正確編碼名稱。 (SITES-39242)

* 內容片段模型編輯器畫布上的欄位標簽字串現在會以使用者的語言顯示。 之前，作者將元件拖曳至畫布後，標籤仍保留英文，而且只有在他們儲存並重新開啟模型後，標籤才會翻譯。 標籤現在會立即翻譯，並符合「屬性」面板。 (SITES-45383)


<!--
#### [!DNL Content Fragments] - REST API{#sites-restapi-6526}

#### ContextHub{#sites-contexthub-6526}
-->


#### 核心後端{#sites-core-backend-6526}

* 透過開啟關閉時間排程的頁面啟用現在僅在需要時執行。 `OnOffTriggerProcessor`之前經常觸發復寫和快取失效，這強製作者手動重新發佈內容。 反向移植修正可免除不必要的處理，並還原可靠的排程發佈。 (SITES-48483)

* 檔案上傳適用於多欄位中新一代資產管理的遠端資產。 先前，當作者為多欄位內的欄位挑選遠端資產時，上傳會失敗。 核心元件更新會還原上傳流程，因此欄位會接受資產。 (SITES-44266)


#### 核心元件{#sites-core-components-6526}

* 遠端資產選擇器會保留每個多欄位專案的影像。 先前，在一個多欄位專案中選取影像時，將它套用到其他所有專案，而遠端資產參考並未儲存。 現在，每個專案都有自己的選取範圍，儲存對話方塊後，參照會持續存在。 (SITES-42376)

* 此發行版本包含Commerce、核心元件、基礎元件（舊版）、Launch和MSM即時副本的背景修正專案。 此修正解決安全性弱點、跨網站指令碼(XSS)違規、檔案上傳行為和即時副本行為。 反向連結將AEM 6.5和AEM 6.5 LTS與先前在AEM as a Cloud Service中提供的修正一致。 (SITES-43738)


<!--
#### Campaign integration{#sites-campaign-integration-6526}

#### ContentHub {#sites-contenthub-6526}

#### Crosswalk {#sites-crosswalk-6526}

#### Experience Fragments{#sites-experiencefragments-6526}

#### Foundation Components (Legacy){#sites-foundation-components-legacy-6526}
-->


#### Headless — 管理員 {#sites-headless-admin-6526}

增強功能： Headless管理員中的預覽檢視現在會將選取的變數路徑傳給預覽元件。 此變更可確保具有多個變異的內容片段預覽會從正確的變異載入內容。 `draftFragmentIds`陣列包含變數引數。 (SITES-42714)


#### 啟動{#sites-launches-6526}

* 提升啟動的時間軸專案現在會以使用者的語言顯示。 先前，在作者促銷啟動專案並在Sites中開啟網站時間軸後，「已建立的版本」和「促銷啟動專案之前」字串仍保留英文。 更新的資源提供所有地區設定的翻譯。 (SITES-13389)
* 「啟動」篩選器面板中的「選取啟動Source預留位置路徑」會顯示完整。 之前，由於文字不符合欄位，因此在法文、義大利文和葡萄牙文等當地語系化介面中截斷文字。 更新的版面配置會顯示完整的預留位置。 (SITES-42792)
* 「工具>網站>啟動」中的「上線日期」欄不再顯示德文、法文、西班牙文、義大利文、巴西葡萄牙文和繁體中文語言環境的AM或PM。 之前，欄使用不符合這些地區設定的12小時格式。 欄現在會顯示24小時格式。 (SITES-43178)


<!--
#### Link Checker{#sites-link-checker-6526}
-->


#### 本地化{#sites-localization-6526}

* 在&#x200B;**工具** > **作業**&#x200B;下之「健全狀況報告」頁面上的字串現在會以使用者的語言顯示。 先前，資源搜尋路徑、維護、復寫佇列、記錄錯誤、作用中套件組合和要求效能的訊息仍以英文顯示。 更新的i18n資源可提供翻譯，而遞補檔案則可保持字串可用。 (NPR-44279)

* 錯誤訊息「勾選「手動新增」選項時，會忽略「JSON路徑」的設定」現在會在&#x200B;**工具** > **Assets** > **中繼資料結構**&#x200B;主控台中以使用者的語言顯示。 之前，作者新增下拉式元素、選取透過JSON路徑新增，並切換為手動新增後，訊息仍維持英文。 更新的資源會提供翻譯。 (ASSETS-31575)
* **Assets** > **管理**&#x200B;標籤中的「提升」字串現在會以使用者的語言顯示。 之前，當您在選取「促銷」後將游標移至智慧標籤上時，字串仍維持為英文。 更新的資源會提供所有地區設定的翻譯。 (ASSETS-36070)
* 新增按鈕標籤不再與&#x200B;**資料夾屬性** > **資產貢獻**&#x200B;中的按鈕重疊。 之前，當您使用「Asset contribution」設定建立資料夾後，文字與德文、義大利文和巴西葡萄牙文介面的按鈕發生衝突。 更新的樣式為較長的翻譯標籤提供了足夠的空間。 (ASSETS-36746)
* Assets清單檢視中的欄標題現在會在日文介面中水準顯示。 之前，標題會垂直顯示在&#x200B;**Assets** > **檔案**&#x200B;下方的清單檢視中，以及內容片段編輯器的卡片檢視中。 更新的`cq-dam-content`套件修正文字方向。(ASSETS-43105)
* Assets欄檢視中的發佈狀態「已排程供稍後使用」現在會以使用者的語言顯示。 先前，在作者選取資產、選擇&#x200B;**管理出版物**、選取&#x200B;**稍後**&#x200B;選項、新增日期及發佈後，字串仍保留為英文。 更新的`cq-dam-content`套件提供所有地區設定的翻譯。 (ASSETS-43307)
* **智慧標籤組態**&#x200B;索引標籤中的字串現在會完整顯示法文和巴西葡萄牙文。 先前，當您在&#x200B;**工具** > **雲端服務** > **智慧標籤**&#x200B;下按一下&#x200B;**建立**&#x200B;後，文字會被切斷。 若要在不使用工具提示的情況下閱讀文字，請使用可提供充足空間的CSS更新。 (ASSETS-68045)
* Assets管理員搜尋邊欄中的「多重路徑值屬性述詞」字串現在會以使用者的語言顯示。 先前，當管理員在&#x200B;**工具** > **一般** > **搜尋**&#x200B;表單下編輯搜尋表單，並將述詞拖曳到表單上時，字串仍為英文。 更新的`cq-dam-content`套件提供翻譯。(CQ-4336103)
* 「專案」檢視中的Aria標籤現在以使用者的語言顯示。 先前，每個專案動態磚上的「動作」按鈕都沒有可存取的名稱，且「設定動態磚」動作使用硬式編碼英文標籤，而同層級標籤則是當地語系化。 更新的動態磚指令碼會為這兩個動作提供當地語系化的標籤。 (CQ-4352359)
* 名稱中包含中文、日文或韓文字元的智慧型系列現在可以正確儲存。 先前，當名稱包含CJK字元時，從&#x200B;**Assets** > **檔案** > **篩選器**&#x200B;儲存集合會失敗，並產生「儲存搜尋失敗 — 無效的請求，不允許重複的集合」。 重複檢查現在會比較收藏集標題，而非節點名稱，因此具有不同CJK標題的收藏集不再衝突。 (GRANITE-62592)
* **安全性** > **使用者** > **建立**&#x200B;中的國家/地區下拉式清單，現在會依使用者的語言以字母順序排序名稱。 過去，清單會以英文排序名稱，同時顯示當地語係化名稱，因此國家/地區在日文等當地語系化中會不按順序顯示。 更新的`com.adobe.granite.security.content`組合會以地區設定感知規則排序。 (GRANITE-67789)
* **工具** > **作業** > **維護**&#x200B;中AuditLog維護工作的免責宣告現在會以使用者的語言顯示。 先前，使用者按一下「每週維護」視窗中的免責宣告圖示後，有關稽核記錄清除與法規遵循要求的警告仍為英文。 更新的資源會提供所有地區設定的翻譯。 (NPR-44189)
* **安全性** > **許可權** > **稽核檢視**&#x200B;中的許可權名稱現在會以使用者的語言顯示。 以前，這些名稱會以英文顯示，因為缺少翻譯。 更新的`com.adobe.granite.platform.i18n`套件組合會提供這些套件。 (NPR-44477)
* **安全性** > **Adobe IMS設定**&#x200B;中的「檢查健康狀態」對話方塊現在會以使用者的語言顯示。 以前，對話方塊在本地化介面中顯示英文字串，因為缺少翻譯。 更新的`com.adobe.granite.platform.i18n`套件組合會提供這些套件。 (NPR-44479)
* 在&#x200B;**工具** > **作業** > **診斷**&#x200B;下之「使用者同步診斷」工具中的字串現在會以使用者的語言顯示。 之前，此工具會在當地語系化介面中顯示英文文字。 更新的`com.adobe.granite.platform.i18n`組合會提供翻譯。 (NPR-44481)
* 設定流程現在會以使用者的語言顯示好記的錯誤訊息。 以往，AEM設定頁面中的失敗會產生技術或未翻譯的文字。 更新的`com.adobe.granite.ui.content`套件組合會處理錯誤並提供本地化訊息。 (NPR-44840)
* 當您在&#x200B;**安全性** > **群組**&#x200B;中變更已刪除群組屬性時顯示的錯誤訊息，現在會以使用者的語言顯示。 以前，本地化介面的訊息仍以英文顯示。 更新的`com.adobe.granite.security.content`組合會提供翻譯。 (NPR-44841)
* 錯誤訊息「將變更儲存至群組時發生錯誤！」 現在會在&#x200B;**安全性** > **群組** > **編輯群組**&#x200B;主控台中以使用者的語言顯示。 以前，訊息會保留為英文以供本地化介面使用。 更新的`com.adobe.granite.security.content`組合會提供翻譯。 (NPR-44842)
* 中文、日文和韓文字元不再以斜體顯示在收件匣圖示錯誤訊息中。 以前，斜體樣式會扭曲字元，使文字更難以閱讀。 更新的`com.adobe.granite.ui.coralui3`組合會移除這些語言的樣式。 (NPR-44843)
* **作業** > **監視**&#x200B;中的數字現在會遵循使用者的地區設定格式。 以前，無論介面語言為何，頁面都會以固定格式顯示數字。 更新的`com.adobe.granite.monitoring.dashboard`組合套用正確的分隔符號和格式。 (NPR-44844)
* Explain Query索引標籤現在會顯示「Query Builder Debugger工具」。 使用者語言中的連結。 之前，由於字串未外部化，當地語系化的介面中遺漏連結文字。 更新的`com.adobe.granite.monitoring.dashboard`套件組合會將其還原。 (NPR-44845)
* Query Builder Debugger工具對話方塊中的文字，現在會以使用者的語言顯示在Explain Query索引標籤上。 之前，有幾個字串沒有外部化，所以會保留英文。 更新的`cq-platform-content`組合會提供翻譯。 (NPR-44846)
* 「一致性檢查結果」頁面中的文字現在會以使用者的語言顯示。 之前，有幾個字串未外部化，因此會以英文顯示。 更新的`com.adobe.granite.operations.ui.core`組合會提供翻譯。 (NPR-44847)
* 「監控圖表」現在會以使用者的語言顯示月和周標籤。 標籤以前是以英文硬式編碼，因此圖表會忽略介面地區設定。 更新的`com.adobe.granite.monitoring.dashboard`套件組合會將字串外部化，現在便會顯示翻譯。 (NPR-44848)
* **安全性** > **使用者** > **建立**&#x200B;中的國家/地區下拉式清單現在可正確排序專案。 以前，當地語系化的國家/地區名稱在某些語言中出現的順序錯誤。 更新的`com.adobe.granite.security.content`套件組合套用地區設定感知排序。 (NPR-44942)
* 按鈕元件對話方塊中的工具提示現在會以使用者的語言顯示。 先前，即使本地化服務中存在字串，按鈕文字、連結、圖示、HTML ID及`aria-label`欄位的資訊文字仍保留英文。 更新的字典提供所有支援地區設定的翻譯。 (SITES-7579)
* 內容片段清單元件的「屬性」區段中的工具提示現在會以使用者的語言顯示。 先前，內容片段模式、標籤、專案數量上限、父路徑、排序順序和排序依據欄位的資訊文字仍以英文顯示。 更新的字典提供所有支援地區設定的翻譯。 (SITES-14969)
* 範本編輯器中核心元件的說明連結現在導向本地化檔案頁面。 先前，在元件設定對話方塊中選取「說明」，會開啟英文頁面，無論介面語言為何。 更新後的URL現在會將使用者路由至其地區設定的頁面。 (SITES-15058)
* 內容片段對話方塊中的資訊工具提示現在會以使用者的語言顯示。 先前，「單一文字元素」和「多個元素」模式以及「內容片段」路徑的工具提示文字仍保留英文。 更新的字典提供所有地區設定的翻譯。 (SITES-17333)
* 範本編輯器元件原則編輯器中的錯誤訊息現在會以使用者的語言顯示。 先前，當作者編輯元件原則或建立新元件原則時，訊息「資源{}無法修改」和「無法建立節點於」仍為英文。 更新的資源提供所有支援地區設定的翻譯。 (SITES-17475)
* 現在，當您從「影像」下拉式清單中選擇「段落」後，「頁面編輯器」中的「Assets」標籤會在「選取元件」下拉式清單中顯示翻譯字串。 之前，由於本地化資源缺乏「其他」字串，因此顯示為英文。 更新的字典提供所有地區設定的翻譯。 (SITES-21481)
* 頁面編輯器設定元件對話方塊中的資訊工具提示不再顯示額外的分行符號。 以前，PDF Viewer和進度列等元件的工具提示會笨拙地包裝在數個區域設定中。 工具提示現在可以正確換行，且斷字功能可如預期運作。 (SITES-38567)
* 工具提示「要退出文字編輯器請按Esc鍵」現在會以使用者的語言顯示在「文字元件設定」對話方塊中。 之前，由於本地化資源缺乏字串，因此該字串會以英文顯示。 工具提示現在會在所有地區設定中翻譯。 (SITES-43186)
* 範本編輯器中的STRUCTURE標籤現在會以使用者的語言顯示。 之前，由於本地化資源中缺少字串，所以在作者開啟最適化表單範本時，標籤仍維持為英文。 標籤現在會在所有地區設定中翻譯。 (SITES-43599)


#### 多網站管理器 - 即時副本{#sites-msm-live-copies-6526}

* 升級後，「MSM轉出」對話方塊會再次載入即時副本清單。 之前，`AsyncOperationServlet.doGet`中的`NullPointerException`已停止旋轉圖示上的對話方塊，因此作者無法選取目標地區設定或開始轉出。 更新的`com.adobe.granite.jobs.async`套件組合會處理遺失的工作資料並完成要求。 (SITES-43116)
* 從Blueprint頁面上的可編輯工具列轉出可再次運作。 工具列動作因「無法讀取未定義的屬性（讀取&#39;doRollout&#39;）」而失敗，因為`MSM.Rollout`使用者端程式庫未載入。 更新頁面現在會載入程式庫，因此轉出工作會開始且變更會觸及即時副本。 (SITES-46052)

* 批次停用Blueprint頁面及其子頁面時，不再傳送重複的轉出事件。 當您在一個要求中停用父項及其子項時，復寫系統會發出五個事件（而非三個），而且每個子頁面都會轉出兩次。 轉出管理員中的重複資料刪除現在每頁會提交一個轉出，因此即時副本不會收到多餘套件。 (SITES-44988)


#### 頁面編輯器{#sites-pageeditor-6526}

* 捲動清單後，選取的樣式會在「頁面編輯器樣式選取」對話方塊中保持反白顯示。 過去，樣式會在您選擇時反白顯示，但當您按一下卷軸時，反白顯示會消失。 此回歸始於SP22之後，現在對話方塊會保持選取的狀態可見。 (SITES-30874)

* 當父元件和子元件定義不同的回應式中斷點時，作者可以在版面模式中編輯頁面。 getResponsiveCssClasses函式先前在省略cq:responsive/phone寬度的元件上因TypeError而失敗。 函式現在會回覆為可用值，並繼續呈現。 (SITES-46681)
* 自訂裁切比例現在會以混合內嵌編輯模式載入具有多個影像放置目標的元件。 先前，影像編輯器會為所有下拉目標初始化一個通用ipeConfig，因此編輯器只會顯示預設比例，並忽略每個目標的aspectRatios。 編輯器現在會讀取所選放置目標的設定，而裁切會套用至內嵌和全熒幕檢視。 (SITES-45771)
* 在RTF編輯器中按退格鍵不會為文字新增額外的內嵌樣式。 客戶回報移除粗體文字後的分行符號時，將style=&quot;font-size： 0.8125rem； background-color： transparent；&quot;新增至粗體標籤。 在最新的Service Pack上測試無法重現行為，因此不需要變更。 (SITES-15883)


<!--
#### Replication{#sites-replication-6526}
-->


#### RTF 編輯器{#sites-rte-6526}

* RTF編輯器工具列按鈕在回應式檢視和版面模式中運作。 以前，按一下按鈕時會反白顯示按鈕，但選取範圍保持不變，並且沒有開啟任何對話方塊。 更新的編輯器指令碼會套用格式，並在「編輯」模式下符合行為。 (SITES-44233)
* 作者可以在文字元件中加入貨幣和商標符號，而不會遺失它們。 「特殊字元」外掛程式會插入符號，但符號會在編輯器和發佈的輸出中顯示為空白。 更正後的處理會按照輸入的格式呈現每個符號。 (SITES-46532)
* RTF編輯器工具列中的「全熒幕」圖示會再次展開編輯器。 之前，按一下核心文字元件中的圖示不會執行任何動作，而編輯器會維持其內嵌大小。 現在，作者可在內嵌和對話方塊編輯中，針對長格式內容使用重點工作區。 (SITES-46396)


#### 網站管理員UI{#sites-admin-ui-6526}

將資產回覆成舊版現在會重新整理其卡片縮圖。 時間軸使用者端資料庫中的URL編碼變更造成路徑不符，因此卡片查詢失敗，且縮圖仍然過時。 比對編碼和原始路徑會還原重新整理。 (SITES-46590)

<!--
#### Universal editor {#sites-universal-editor-6526}
-->

#### 工作流程擴充功能 {#sites-workflow-extensions-6526}

檢視裝載現在會開啟Touch UI套件編輯器，以用於「管理發布」從多個頁面開始的工作流程。 之前，該動作會開啟已棄用的傳統UI封裝編輯器，即使作者是在觸控式UI中啟動工作流程亦然。 作者現在無需離開Touch UI即可檢查裝載。 (SITES-40928)


### [!DNL Assets] {#assets-6526}

* 增強功能：AEM Assets 6.5包含對創作AI內容的Convention for Content Provenance and Authenticity (C2PA)合規性的支援。 更新資產工作流程會偵測C2PA憑證、擷取中繼資料，並簽署工作流程重新產生的轉譯。 簽署會在每個AEM執行個體本機執行，因此客戶不需要專用的簽署基礎結構。 (ASSETS-75868)

* 檔案增強功能：新的公開檔案說明如何自訂資產處理管道，同時保持C2PA合規性。 說明檔案說明如何在轉譯步驟前放置偵測C2PA憑證步驟，以及如何在每個AEM執行個體本機執行簽署。 本檔案也說明專用或客戶擁有的簽署基礎結構的限制。 (ASSETS-76100)
* 現在當您將游標停留在AEM 6.5 SP26環境中的連結上時，殼層標頭中的說明下拉式清單會保持開啟狀態。 先前，下拉式清單會在指標進入清單時關閉，因此作者無法按一下「檔案」、「社群」或支援連結。 更新的`com.adobe.granite.ui.content`套件組合會延遲焦點檢查，因此功能表只會在焦點真正離開時關閉。 (ASSETS-65676)

<!--
#### [!DNL Dynamic Media]{#assets-dm-6526}
-->

### [!DNL Forms]{#forms-6526}

* 新功能：支援RTF中清單的協助工具標籤。 過去，只有當範本遵循特定結構時，協助工具標籤樹狀結構中才會出現清單標籤。 請求已關閉，成為提供該功能之相關票證的重複專案。 (LC-3923202)
* 增強： AEM Forms新增執行階段API，為每個要求選取舊版或預設的可延伸標籤語言(XML)資料匯出模式。 以前，只有`-Dcom.adobe.fd.forms.export.legacy` Java Virtual Machine (JVM)引數可控制模式，以及套用至伺服器上每個匯出的設定。 當請求未使用API時，JVM引數會繼續控制行為。 (FORMS-23114， FORMS-22983)
* 以不可見憑證簽章認證的可攜式檔案格式(PDF)檔案在Adobe Acrobat中的開啟速度不再緩慢。 先前僅套用至可見憑證簽章的修正現在也涵蓋不可見憑證簽章。 (FORMS-25171)
* 在Foundation元件式Adaptive Forms中，「檔案附件」元件現在會根據上傳時允許的檔案型別清單來檢查檔案。 以前，即使清單僅允許`application/pdf`、`image/jpeg`和`image/png`，像`.xsd`這樣的檔案也通過上傳步驟。 表單僅在送出時以一般不支援的檔案警示拒絕這些要求。 (FORMS-24295)

#### FORMS JEE {#forms-jee-6526}

* 增強： AEM Forms Document Security新增了Adobe Acrobat (PPKLite)的密碼金鑰（Web驗證或WebAuthn）支援。 (FORMS-21762)
* 增強功能： IBM Content Manager聯結器現在支援IBM Content Manager 8.7，因為IBM已終止支援8.5和8.6版。 (FORMS-6827)
* 在Windows上，將某些可攜式檔案格式(PDF)檔案轉換為影像（例如TIFF）時，ConvertPDF服務不再中止。 (FORMS-25796)
* 安全性宣告標籤語言(SAML)驗證現在會使用上傳的身分提供者(IdP)中繼資料的憑證來驗證宣告簽章。 當IdP憑證變更且中繼資料未更新時，驗證會失敗。 (FORMS-24679)
* 升級至AEM Forms Service Pack 6.5.24.0後，`server.log`和`error.log`不再填入`[XMLSecurity]`警告訊息，例如「Secure parser factory建立失敗，任何建立的XML剖析器都可能遭受XML型漏洞攻擊」。 訊息每秒出現幾次，即使在閒置的伺服器上也是如此，而且會快速消耗磁碟空間。 (FORMS-23717)
* JEE端的元件現在封裝Apache POI 5.4.0。 之前，某些套件組合仍包含Apache POI 3.17和3.9，這些套件在升級至AEM Forms Service Pack 6.5.24.0後會標籤安全性掃描。 (FORMS-23678)

#### Forms Designer {#forms-designer-6526}

* 增強功能： Forms Designer和輸出服務會在靜態互動和平面PDF檔案中，產生從標題層級1到標題層級6協助工具角色的巢狀可攜式檔案格式(PDF)書籤。 標題層級1會成為頂層書籤，不含作者先前在Adobe Acrobat中手動移除的空白或重複專案。 若要還原先前的書籤行為，請新增`<behaviorOverride>patch-LC-3922369:1</behaviorOverride>`至自訂XCI檔案。 (LC-3923490、LC-3922369)
* 增強功能：在靜態互動或平面可攜式檔案格式(PDF)檔案中選取書籤，現在會將相符的標題捲動至頁面頂端。 (LC-3923489、LC-3923289)
* 增強功能： Forms Designer可將書籤`extras`元素新增至使用「標題層級1」到「標題層級6」協助工具角色的文字物件。 之前，作者必須在XML Source中手動為每個標題新增`<extras name="bookmark">`，才能產生書籤。 (FORMS-24361)


### 基礎 {#foundation-6526}

* **安全性** > **使用者** > **建立**&#x200B;使用者對話方塊中的「國家/地區」字串現在會以使用者的語言顯示。 之前，本地化介面的標籤仍為英文。 更新的`com.adobe.granite.security.content`組合會提供翻譯。 (NPR-43882)
* 現在，當您將游標停留在AEM 6.5 SP26環境中的連結上時，殼層標頭中的說明下拉式清單會保持開啟。 先前，下拉式清單會在指標進入清單時關閉，因此作者無法按一下「檔案」、「社群」或支援連結。 更新的`com.adobe.granite.ui.content`套件組合會延遲焦點檢查，因此功能表只會在焦點真正離開時關閉。 (NPR-44686)
* 改善： `HtmlLibraryManagerImpl`查詢現在包含節點型別標籤，因此查詢一律使用預期的索引。 當服務找不到使用者端程式庫時，也會記錄「錯誤」，提醒管理員發生問題。 更新會顛覆Service Pack中的`com.adobe.granite.clientlibs`套件組合版本。 (NPR-44698)


<!--
#### Apache Felix {#foundation-apachefelix-6526}
-->


#### 驗證 {#foundation-authentication-6526}

現在，使用者編輯器中的「儲存並關閉」會傳回目前搜尋的搜尋結果。 先前，作者在Omnisearch中搜尋第二個使用者、編輯屬性並按一下「儲存並關閉」後，頁面會開啟第一個使用者的屬性。 更新的UserProperties.js指令碼會還原預期的導覽。 (NPR-44774)

<!--
#### Campaign{#foundation-campaign-6526}

#### Cloud Services{#foundation-cloudservices-6526}

#### Communities {#foundation-communities-6526}

#### Content distribution{#foundation-content-distribution-6526}

#### Adobe CRX {#foundation-crx-6526}
-->


#### Granite{#foundation-granite-6526}

* Assets Omnisearch篩選器中的「內容片段模式」預留位置現在已完整顯示。 先前，您前往Assets、按一下「篩選器」或「搜尋」圖示，然後展開「內容片段模式」欄位，系統就會截斷文字。 更新的樣式為預留位置提供了足夠的空間。 (GRANITE-54387)
* 現在，將指標移到殼層標頭的連結上時，殼層標頭中的說明下拉式清單會保持開啟。 先前，當指標進入檔案、社群和支援連結清單時，下拉式清單就會關閉，導致無法透過滑鼠連線到連結。 焦點處理常式現在會將其檢查延遲至下一個動畫影格，所以暫留不再計為焦點退出功能表。 (GRANITE-70978)

<!--
#### Jetty{#foundation-jetty-6526}
-->

#### Launch整合{#foundation-launch-integrations-6526}

改善： Adobe Analytics與Adobe Experience Manager Launch的整合使用Analytics 2.0 API。 Analytics 1.4 API的生命週期於2026年8月31日結束。 移轉可讓報表與Launch整合在當天之後繼續運作。 (CQ-4365074、CQ-4365080)

<!--
#### Localization{#foundation-localization-6526}

#### Oak {#foundation-oak-6526}
-->

#### Platform{#foundation-platform-6526}

* AEM登入頁面頁尾的「說明」連結現在會開啟一個工作頁面。 之前，該連結指向的marketing.adobe.com URL已不存在。 頁尾設定現在使用[Adobe Experience Manager檔案](https://experienceleague.adobe.com/en/docs/experience-manager) URL。 (NPR-44388)
* 增強功能：AEM傳送電子郵件時，客戶要求使用Microsoft Graph API做為SMTP的替代方案。 票證解析為重複，因為另一個票證已實作Graph API流程。 使用OAuth 2.0的SMTP仍適用於需要離開SMTP基本驗證的客戶。 (GRANITE-57478)

* 在&#x200B;**工具** > **一般** > **組態**&#x200B;瀏覽器中，[有效許可權]對話方塊中的字串現在會正確對齊。 先前，在您選取資料夾、按一下「屬性」並按一下「有效許可權」後，系統會顯示一個反白的字串。 更新版面配置規則以恢復對齊方式。 (CQ-4359166)


#### 專案 {#foundation-projects-6526}

「選取i18n字典」對話方塊中的「選取根目錄」字串現在會完整顯示。 之前，當您建立翻譯專案並新增i18n字典後，文字在數個當地語系化介面中被切斷。 更新的`cq-projects-translation-content`封裝為字串提供足夠的空間。 (CQ-4355405)

<!--
#### Security{#foundation-security-6526}

#### Sling{#foundation-sling-6526}

#### SPA editor {#foundation-spa-editor-6526}
-->


#### 翻譯{#foundation-translation-6526}

List元件的樣式選項現在會以使用者的語言顯示。 先前，在作者將List元件新增至體驗片段後，字串（例如「區塊」和「格線」）在樣式選單中仍維持英文。 更新後的資源提供翻譯功能，包括韓文、簡體中文和繁體中文介面。 (CQ-4349666)

<!--
#### User interface{#foundation-ui-6526}

#### WCM{#foundation-wcm-6526}
-->

#### 工作流程{#foundation-workflow-6526}

改善： Touch UI頁面編輯器現在會轉譯內容樹狀結構，並支援在Workflow封裝頁面上編輯Resource Definition元件。 先前，**管理出版物** > **稍後發佈**&#x200B;建立的`/etc/workflow/packages/`下的頁面在左側面板中未顯示內容樹狀結構，且作者無法編輯資源定義元件。 核准者現在會在觸控式UI中，檢查工作流程裝載中的頁面和資產，並符合Classic UI行為。 (GRANITE-65620)

## 安裝[!DNL Experience Manager] 6.5.26.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.26.0需要[!DNL Experience Manager] 6.5。 如需詳細指示，請參閱[升級檔案](/help/sites-deploying/upgrade.md)。<!-- UPDATE FOR EACH NEW RELEASE -->
* Service Pack下載專案可在Adobe [軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.26.0.zip)上取得。
* 在具有MongoDB和多個執行個體的部署上，使用封裝管理員在其中一個編寫執行個體上安裝[!DNL Experience Manager] 6.5.26.0。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe建議您不要刪除或解除安裝[!DNL Experience Manager] 6.5.26.0套件。 若要視需要回覆，請先建立`crx-repository`的備份，然後再安裝套件。<!-- UPDATE FOR EACH NEW RELEASE -->

<!-- FORMS For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->

### 在[!DNL Experience Manager] 6.5上安裝Service Pack{#install-service-pack}

1. 如果執行個體處於更新模式（從舊版更新執行個體時），請在安裝前重新啟動執行個體。 如果執行個體的目前運作時間很高，Adobe建議重新啟動。

1. 安裝之前，請為您的[!DNL Experience Manager]執行個體建立快照或全新備份。

1. 從[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.26.0.zip)下載Service Pack。<!-- UPDATE FOR EACH NEW RELEASE -->

1. 開啟封裝管理員，然後選取&#x200B;**[!UICONTROL 上傳封裝]**&#x200B;以上傳封裝。 如需詳細資訊，請參閱[封裝管理員](/help/sites-administering/package-manager.md)。

1. 選取封裝，然後選取&#x200B;**[!UICONTROL 安裝]**。

1. 若要更新S3聯結器，請在安裝Service Pack後停止執行個體，將現有聯結器取代為安裝資料夾中提供的新二進位檔案，然後重新啟動執行個體。 請參閱[Amazon S3資料存放區](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)。

>[!NOTE]
>
>安裝Service Pack期間，Package Manager UI上的對話方塊有時會關閉。 Adobe建議您先等候錯誤記錄檔停止更新，再存取部署。 在確認安裝成功之前，請等待與更新程式套件組合解除安裝相關的特定記錄。 此問題發生在[!DNL Safari]瀏覽器中，但有時也發生在任何瀏覽器中。

**自動安裝**

您可以使用兩種不同的方法來安裝[!DNL Experience Manager] 6.5.26.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* 伺服器上線時，請將封裝放入`../crx-quickstart/install`資料夾。 套件會自動安裝。
* 使用封裝管理員[&#128279;](/help/sites-administering/package-manager.md#package-share)的HTTP API。 使用`cmd=install&recursive=true`安裝巢狀套件。

>[!NOTE]
>
>Experience Manager 6.5.26.0不支援Bootstrap安裝。<!-- UPDATE FOR EACH NEW RELEASE -->

**驗證安裝**

如需經認證可搭配此版本使用的平台，請參閱[技術需求](/help/sites-deploying/technical-requirements.md)。

1. 產品資訊頁(`/system/console/productinfo`)會在[!UICONTROL 已安裝產品]下顯示更新的版本字串`Adobe Experience Manager (6.5.26.0)`。<!-- UPDATE FOR EACH NEW RELEASE -->

1. 在OSGi主控台中，所有OSGi套件組合均為&#x200B;**[!UICONTROL 作用中]**&#x200B;或&#x200B;**[!UICONTROL 片段]** （使用Web主控台： `/system/console/bundles`）。

1. OSGi套件`org.apache.jackrabbit.oak-core`是1.22.20或更新版本（使用Web主控台： `/system/console/bundles`）。<!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE. CHECK WITH SAMEER DHAWAN -->

### 安裝[!DNL Experience Manager] Forms的Service Pack{#install-aem-forms-add-on-package}

如需在Experience Manager Forms上安裝Service Pack的說明，請參閱[Experience Manager Forms Service Pack安裝說明](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)。

>[!NOTE]
>
>調適型表單功能 (適用於 [AEM 6.5 QuickStart](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/implementing/deploying/deploying/deploy)) 僅用於探索和評估目的。 若要供生產使用，必須獲得 AEM Forms 的有效許可；調適型表單的功能需要適當許可才可使用。

### 安裝適用於Experience Manager內容片段的GraphQL索引套件{#install-aem-graphql-index-add-on-package}

使用GraphQL的客戶必須安裝[Experience Manager內容片段搭配GraphQL索引套件1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip)。

這可讓您根據使用的功能新增所需的索引定義。

無法安裝此套件會導致GraphQL查詢變慢或失敗。

>[!NOTE]
>
>每個執行個體僅安裝此套件一次；不需要隨每個Service Pack重新安裝。

### UberJar{#uber-jar}

[!DNL Experience Manager] 6.5.26.0的UberJar可在[Maven中央存放庫](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.26/)中使用。<!-- CHECK FOR UPDATE EACH NEW RELEASE FROM MADHULIKA SINGH -->

若要在Maven專案中使用UberJar，請參閱[如何使用UberJar](/help/sites-developing/ht-projects-maven.md)，並在您的專案POM中包含下列相依性： <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.26</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar和其他相關成品可在Maven中央存放庫上使用，而不是Adobe公共Maven存放庫(`repo.adobe.com`)。 主要UberJar檔案已重新命名為`uber-jar-<version>.jar`。 沒有`dependency`標籤的`classifier`，其值為`apis`。



## 已棄用和已移除的功能{#removed-deprecated-features}

如需AEM 6.5已棄用或移除之所有功能的詳細清單，請參閱[已棄用和移除的功能](/help/release-notes/deprecated-removed-features.md)。

### AEM Assets REST API 中的內容片段支援 {#cf-support-assets-rest-api}

AEM 6.5 LTS SP2 為內容片段和模型管理提供現代化的 OpenAPI，因此 AEM Assets REST API 中較舊的內容片段支援端點現已棄用。

Adobe打算在產品生命週期結束前保留這些較舊的端點。 Adobe 未計劃針對已棄用的端點提供進一步的增強功能。

### SPA 編輯器 {#spa-editor}

[從AEM 6.5.25版開始的新專案已棄用SPA編輯器](/help/sites-developing/spa-overview.md)。 SPA Editor仍支援現有專案，但不應用於新專案。

目前，AEM 中用於管理 Headless 內容的首選編輯器為：

* [通用編輯器](/help/sites-developing/universal-editor/introduction.md)，用於視覺化編輯。
* [內容片段編輯器](/help/sites-developing/universal-editor/introduction.md)，用於表單型編輯。

## 已知問題{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

* 與Oak相關的&#x200B;**&#x200B;**
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
     系統會自動建立`cache`和`diff-cache`的新資料夾，而且您在`error.log`中不會再遇到與`mvstore`相關的例外狀況。

* 更新您的內容模型使用自訂API名稱的GraphQL查詢，以改用內容模型的預設名稱。

* GraphQL查詢使用`damAssetLucene`索引，而非`fragments`索引。 此動作會導致GraphQL查詢失敗或需要很長時間才能執行。

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

  執行這些步驟後，GraphQL查詢的執行速度會更快。

* 嘗試移動、刪除或發佈內容片段、網站或頁面時，在擷取內容片段參考時出現問題。 背景查詢失敗；功能無法運作。
若要確保作業正確，您必須將下列屬性新增至索引定義節點`/oak:index/damAssetLucene` （不需要重新索引）：

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* 如果您將[!DNL Experience Manager]執行個體從6.5.0 - 6.5.4升級至Java™ 11上的最新Service Pack，您會在`error.log`檔案中看到`RRD4JReporter`例外狀況。 若要停止例外狀況，請重新啟動[!DNL Experience Manager]的執行個體。<!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* 使用者可以在[!DNL Assets]中重新命名資料夾，並將巢狀資料夾發佈至[!DNL Brand Portal]。 但是，在重新發佈根資料夾之前，[!DNL Brand Portal]中的資料夾標題不會更新。

* 安裝[!DNL Experience Manager] 6.5.x.x期間出現下列錯誤和警告訊息：
  * 「當使用Adobe Target API （IMS驗證）在[!DNL Experience Manager]中設定Target Standard整合時，將體驗片段匯出至Target會導致建立錯誤的選件型別。 Target會建立多個型別為「HTML」/來源「Adobe Target Classic」的選件，而非「體驗片段」/來源「Adobe Experience Manager」型別。
  * `com.adobe.granite.maintenance.impl.TaskScheduler`：在`granite/operations/maintenance`找不到維護期間。
  * 使用彙總函式（例如SUM、MAX和MIN）時，Adaptive Form伺服器端驗證會失敗(CQ-4274424)。
  * `com.adobe.granite.maintenance.impl.TaskScheduler` ：在`granite/operations/maintenance`找不到維護期間。
  * 透過Shoppable Banner檢視器預覽資產時，Dynamic Media互動式影像中的熱點不可見。
  * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` ：等待登入變更完成解除登入逾時。

* 從AEM 6.5.15開始，`org.apache.servicemix.bundles.rhino`套件提供的Rhino JavaScript Engine有新的提升行為。 使用嚴格模式(`use strict;`)的指令碼必須宣告其正確的變數。 否則，它們不會執行，並最終擲回執行階段錯誤。

* 透過正式更新套件安裝標籤相關標準內容時，會將`/content/cq:tags`節點的languages屬性重設為預設值。 此動作適用於Service Pack、Security Service Pack、Extended Feature Pack、Cumulative Feature Pack、修補程式等。 因此，在安裝之前，必須將其新增到屬性。

### AEM Sites的已知問題 {#known-issues-aem-sites-6526}

* **適用於AEM Foundation的Hotfix已知問題**

  從舊版Service Pack升級至Experience Manager 6.5.26.0後，CRXDE Lite套件組合版本排序會導致Experience Manager無法選取預期的套件。 若要修正版本順序，請安裝Service Pack 26，然後從Software Distribution下載並安裝Hotfix [`CRXDE Lite hotfix GRANITE-76725`](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq660%2Fhotfixes%2Fgranite-76725%2Fcq-6.5.26-hotfix-GRANITE-76725-1.0.zip)。 此Hotfix為僅限版本的更新。 其中不包含程式碼或功能變更。 (GRANITE-76725)

* 內容片段 — 預覽失敗，因為大型片段樹受到DoS保護。 請參閱有關預設GraphQL查詢執行器組態選項[&#128279;](https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-23945)的KB文章(SITES-17934)

### AEM Forms的已知問題 {#known-issues-aem-forms-6526}

* 當包含使用`bindref`的&#x200B;**檔案附件**&#x200B;欄位的表單提交給具有&#x200B;**指派任務**&#x200B;步驟的AEM工作流程時，附件未顯示。 因此，當從「收件匣」開啟任務時，它們不會出現。 檔案會正確儲存至存放庫，但指派工作步驟UI無法顯示附件。 (FORMS-23722)

* 當數位簽署的PDF附加至AEM Forms JEE Workspace中的任務時，上傳維持卡在上傳狀態或發生「檔案無效」錯誤而失敗。 因此，無法將較大的已簽署PDF附件新增至工作。 此問題已在較新版本中修正。 如需Hotfix版本，請聯絡Adobe支援。 (FORMS-28517)

* 如修補程式135所報告，在IBM WebSphere上，透過AEM Forms Workbench中的「叫用Web服務」活動載入Web服務描述語言(WSDL)檔案，AEM Forms JEE 6.5.26.0 (Service Pack 26)可能會失敗。 相同的操作在JBoss上運作。 (FORMS-29972)

  **因應措施：**&#x200B;在裝載AEM Forms JEE的WebSphere應用程式伺服器上新增Java虛擬機器器(JVM)引數。 這是伺服器端設定，而非Workbench使用者端設定。

  1. 開啟裝載AEM Forms JEE之WebSphere應用程式伺服器的JVM設定。
  1. 將下列引數新增至伺服器JVM引數。 保留現有的引數。

     ```shell
     -Dcom.adobe.idp.dsc.webservice.loadSOAPClasses=true
     ```

  1. 儲存組態，然後重新啟動WebSphere應用程式伺服器，讓引數生效。
  1. 從AEM Forms Workbench重新連線，然後再次在叫用Web服務活動中載入WSDL。

#### 可用Hotfix的已知問題 {#aem-forms-issues-with-hotfixes}

下列問題有可供下載和安裝的Hotfix。 您可以[下載並安裝Hotfix](/help/release-notes/aem-forms-hotfix.md)以解決下列問題：

* 安裝AEM Forms JEE Service Pack 21 (6.5.21.0)後，如果在`<AEM_Forms_Installation>/lib/caching/lib`資料夾下找到Geode jar `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)`的重複專案，請執行以下步驟以解決問題(FORMS-14926)：

  1. 停止儲位（如果它們正在執行）。
  1. 停止AEM伺服器。
  1. 移至`<AEM_Forms_Installation>/lib/caching/lib`。
  1. 移除除`geode-*-1.15.1.2.jar`以外的所有Geode修補程式檔案。 確認只有具有`version 1.15.1.2`的Geode jar存在。
  1. 在管理模式中開啟命令提示字元。
  1. 使用`geode-*-1.15.1.2.jar`檔案安裝Geode修補程式。

## 包含的 OSGi 套件和內容套件{#osgi-bundles-and-content-packages-included}

下列zip檔案包含列出此[!DNL Experience Manager] 6.5 Service Pack發行版本中包含的OSGi套件組合和內容套件的文字檔案：

* [Experience Manager 6.5.26.0](/help/release-notes/assets/65260-bundles.zip)中包含的OSGi套件組合清單
<!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5.26.0](/help/release-notes/assets/65260-packages.zip)中包含的內容套件清單
<!-- UPDATE FOR EACH NEW RELEASE -->

## 受限制的網站{#restricted-sites}

這些網站僅供客戶使用。 若您是客戶並且需要存取權，請聯絡您的 Adobe 客戶經理。

* [在 licensing.adobe.com 下載產品](https://licensing.adobe.com/)
* [聯絡 Adobe 客戶支援](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-customer-support-experience#)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 產品頁面](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5檔案](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65)
>* [訂閱Adobe優先產品更新](https://www.adobe.com/tw/subscription/priority-product-update.html)




