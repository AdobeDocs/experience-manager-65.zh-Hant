---
title: 版本注意事項 [!DNL Adobe Experience Manager] 6.5
description: 尋找版本資訊、新增功能、安裝作法和詳細的變更清單 [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
exl-id: cac14ac1-9cda-46ae-8aa3-94674bb79157
source-git-commit: 8d06457241919095fd9802f69df426a1cc6851da
workflow-type: tm+mt
source-wordcount: '3675'
ht-degree: 4%

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
| 版本 | 6.5.19.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 類型 | Service Pack發行 |
| 日期 | 2023年11月30日星期四 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 下載 URL | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.19.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## 包含的內容 [!DNL Experience Manager] 6.5.19.0 {#what-is-included-in-aem-6519}

[!DNL Experience Manager] 6.5.19.0包括自2019年4月6.5首次發行以來所推出的新功能、客戶要求的重要增強功能、錯誤修正，以及效能、穩定性和安全性改善專案。 [安裝此Service Pack](#install) 於 [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

此版本中的部分主要功能和增強功能包括：

**重要功能**

* 資產，Dynamic Media - [Dynamic Media中的影片支援多字幕與多音訊曲目](/help/assets/video.md#about-msma) — 您現在可以輕鬆地將多個字幕和多個音軌新增到主要視訊中。 此功能表示全球對象都可以存取您的影片。您可以以多種語言向全球對象自訂單一已發佈的主要影片，並遵守不同地理區域的輔助功能指南。作者還可以從使用者介面中的單個標籤管理字幕和音訊。

* 資產 — 您現在可以從搜尋結果導覽至包含資產的檔案夾位置，以讓您執行各種資產管理任務。 (ASSETS-23182)

**重要增強功能**

* 內容片段中的Sites Polaris選取器已改善效能。 (SITES-14092)

* 啟用Sites頁面編輯器/影像元件使用者從遠端資產Cloud Service參照資產。 (SITES-13448， SITES-13433)

* 若要在清單檢視中快速找到系統中可能有多個專案的專案，Adobe現在支援伺服器端排序。 專案節點會在使用者介面中呈現之前，根據使用者選取的欄在後端排序。 (NPR-41027)

* AEM 6.5.19.0支援MongoDB 5.0至6.0。

**汰除功能**

* AEM中的ActiveMQ已過時。 ActiveMQ用於兩個AEM Publish執行個體之間的通訊。 Adobe建議客戶現在使用負載平衡器。

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## 已修正Service Pack 19中的問題 {#fixed-issues}

### [!DNL Sites]{#sites-6519}

#### 協助工具{#sites-accessibility-6519}

* 在AEM Sites頁面上，當您放大頁面200%時，連結會 **[!UICONTROL 語言副本]** 和 **[!UICONTROL CSV報表]** 在參照邊欄中消失。 (SITES-11011)

#### 管理員使用者介面{#sites-adminui-6519}

* AEM Screens頻道 **[!UICONTROL 預覽]** 功能無法運作或顯示在控制面板上。 (SITES-15730)
* 在頁面移動作業期間，如果使用者介面無法顯示參照，但指出會自動重新發佈參照，則會顯示參照 *非* 已重新發佈。 (SITES-16435)
* 在具有Service Pack 16或17的AEM 6.5中，當在已啟用「工作流程」欄的網站清單檢視中時，您無法根據該欄中的專案排序清單。 沒有排序。 (SITES-15385)
* 對於重新導向頁面範本，重新導向欄位已設定為必填。 不過，必要欄位的驗證不適用於以下兩種情況：建立頁面時沒有強制重新導向值；無法建立重新導向頁面。 使用鍵盤快速鍵導覽時驗證無法運作，且當欄位被標籤為無效時，驗證無法繼續。 (SITES-15903)
* 部分 **傳入連結** 未包括在「 」中顯示的計數 **引用** 面板。 例如，面板顯示 **傳入連結(6)** 但實際上有9個傳入連結。 (SITES-14816)

#### 傳統 UI{#sites-classicui-6519}

* 在SITES-15827中安裝Hotfix後，單字之間有空白的對話方塊標題會取代為 `" "`. 也正在移除分行符號。 (SITES-16089)
* 已編碼的對話方塊標題現在會導致標題的雙重編碼。 (SITES-15841)
* 將AEM伺服器從Service Pack 6.5.16更新至6.5.17會導致傳統UI對話方塊標題編碼兩次。 (SITES-15634)

#### [!DNL Content Fragments]{#sites-contentfragments-6519}

* 內容片段編輯器中會顯示內部伺服器錯誤訊息。 (SITES-13550)
* 更新 `org.json` 資料庫透過NPR-41291導致中的資料錯誤轉換 `DefaultDataTypeConverter` 的 `cfm-impl` 套件組合。 資料型別轉換必須更靈活。 (SITES-16473)
* 收到錯誤快顯訊息：「由於內容不相容，此內容片段版本無法與目前版本比較。」 內容片段應該可以比較，但事實並非如此。 (SITES-16317)
* 將資產選擇器JS URL從
  `https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js`
至
  `https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/assets-selectors.js` (SITES-16068)
* 為CFM-Polaris整合調整新的Polaris中繼資料API回應結構。 (SITES-15166)
* 應列出所有內容片段，其中參照了所選的內容片段。 內容片段參考面板中的資產參考會顯示0 （零）參考。 (SITES-15036)

#### 核心後端{#sites-core-backend-6519}

* 改進 `StyleImpl`. (SITES-15164)
* 改進WCM管道的版本/650分支，以便能夠對其模組執行整合測試。 (SITES-12938)

<!--#### Core Components{#sites-core-components-6519}

* A -->

#### Campaign整合{#sites-campaign-integration-6519}

* 在簽章元件上(`/apps/fpl/components/campaign/signature`)，連結Externalizer無法運作。 如果影像標籤上方的HTML註解已移除，則不會將網域附加至影像來源。 此問題僅存在於生產環境中的簽名元件中，而非中繼環境中。 (SITES-16120)

<!--#### Experience Fragments{#sites-experiencefragments-6519}

* A -->

#### 基礎元件（舊版）{#sites-foundation-components-legacy-6519}

* Adobe Experience Manager (AEM) Sites Search元件損壞了使用者介面。 (SITES-15087)

#### GraphQL 查詢編輯器{#sites-graphql-query-editor-6519}

* 當查詢數量較多時（例如，超過25個），GraphQL編輯器使用者介面無法讓您捲動瀏覽所有持續存在的查詢。 (SITES-16008)
* GraphQL編輯器沒有儲存持續查詢的發佈狀態。 取消發佈按鈕會出現在GraphQL編輯器中，但不顯示指示持久查詢已發佈的圖示。 重新整理頁面會顯示持續查詢甚至尚未發佈。 (SITES-15858)

#### 啟動{#sites-launches-6519}

* 存放庫中的變更未儲存，因為 `Oak0001` 正在編輯多個頁面或正在編寫內容時發生衝突。 在此類事件中執行重試是正常的，但不會發生這種情況。 (SITES-14840)

#### MSM — 即時副本{#sites-msm-live-copies-6519}

* MSM轉出按鈕在觸控式圖形使用者介面中無法運作。 (SITES-16991)
* 建立即時副本或轉出體驗片段時，體驗片段內的連結參考沒有更新。 (SITES-15460)

#### 頁面編輯器{#sites-pageeditor-6519}

* 在「Forms >主題」中，如果您在主題編輯器中開啟主題並進行一些變更並儲存，然後按一下「預覽」，則會顯示載入圖示，但未載入實際預覽。 (SITES-17164)
* 在資產型別篩選器上選取多個檔案檔案型別在頁面主控台上無法運作。 即使某個特定檔案型別的結果可用，也找不到任何結果。 因此，作者無法篩選多個檔案。 他們必須使用多種檔案型別，而且必須一次篩選一種。 (SITES-14047)
* 從AEM 6.5.17和AEM 6.5.18升級執行個體後，從頁面編輯器內（如果您選取） **[!UICONTROL 發佈頁面]**，系統會將您重新導向至不存在的URL。 系統會將使用者重新導向至發佈精靈。 (SITES-15856)
* 在作業系統剪貼簿的貼上過程中，AEM剪貼簿中有多餘的復本。 (SITES-15704)
* 在「資產」中，選取 **[!UICONTROL 檔案]**，然後在下方 **[!UICONTROL 篩選型別]**，選取 **[!UICONTROL Microsoft® Word]** 或 **[!UICONTROL Microsoft® Excel]** 即使兩種型別的檔案都存在，也不會顯示結果。 (SITES-14837)

### [!DNL Assets]{#assets-6519}

* 當您建立或儲存公用資料夾時，會在管理員控制面板中建立三個群組。 (ASSETS-26700)
* 無法區分將資產發佈到Experience Manager或Brand Portal。 (NPR-41320)
* 在搜尋面板中，當您選取核取方塊並取消選取其中任何一個核取方塊時，所有核取方塊都會取消勾選。 (ASSETS-26377)

#### [!DNL Dynamic Media]{#assets-dm-6519}

* 將資產上傳至AEM後， `update_asset` 工作流程已觸發。 工作流程永遠不會完成。 檢視工作流程例項，工作流程會完成至產品上傳步驟。 下一步是Scene7批次上傳。 使用者可透過Dynamic Media Classic應用程式檢視資產是否位於Scene7中。 (ASSETS-30443)
* 自訂Servlet （API端點）傳回錯誤的Dynamic Media (Scene7)檔案名稱。 刪除資產並取代為相同名稱的資產時，就會發生這種情況。 自訂servlet會傳回舊的Dynamic Media (Scene7)檔案名稱，而「jcr」API呼叫會傳回正確的檔案名稱。 (ASSETS-29476)
* 即使在資料夾層級關閉同步之後，記錄檔仍會顯示「Scene7 ReplicateOnModifyListener」的觸發程式。 此 `ReplicateOnModifyListener/Worker` 應該略過非Dynamic Media資料夾資產和內容片段的處理。 (ASSETS-26705)
* 如果焦點在高對比黑白模式下的下拉式元素（僅限內容、檢視、更多選項）中不可見，則弱視者會受到影響。 (ASSETS-25759)
* 如果頁面上文字的明度對比率小於4.5:1，則會影響弱視者。 (ASSETS-25756)
* 熒幕助讀程式在提交資料後，不會提供所顯示快顯訊息的旁白。 (ASSETS-25755)
* 使用地標/區域捷徑鍵導覽時，熒幕助讀程式無法辨識頁面中的地標(Dynamic Media；建立視訊編碼設定檔) `D/R`. (ASSETS-25752)
* 使用地標/區域捷徑鍵導覽時，熒幕助讀程式無法辨識頁面中的多個地標(Dynamic Media；建立互動式視訊) `D/R`. (ASSETS-25750)
* 熒幕助讀程式（NVDA/JAWS/朗讀程式）無法辨識中的地標 **編輯資產** 使用快速鍵導覽時所在的頁面 `D/R`. (ASSETS-25744)
* 使用者收到空白/錯誤的非同步作業訊息，但已成功發佈連線的資產。 (ASSETS-29342)

### [!DNL Forms]{#forms-6519}

中的修正 [!DNL Experience Manager] Forms會透過單獨的附加元件套件在排程一週後傳送 [!DNL Experience Manager] Service Pack發行日期。 在此案例中，AEM 6.5.19.0 Forms附加元件套件發行預計於2023年11月30日星期四推出。 此版本發行後，本節將新增Forms修正和增強功能的清單。

* 新增存取控制清單 `fd-cloudservice` 使用者能夠讀取或更新下的Microsoft®設定 `cloudconfigs/microsoftoffice`. (FORMS-11142)

<!--LEFT BULLET LIST HERE IN CASE OF REUSE BY FORMS IN THE FUTURE 
* **Document Services**
  * text
* **Adaptive Forms** 
  * text
* **Accessibility**
  * text
* **Interactive Communications**
  * text -->

<!--### Commerce{#commerce-6519}

* A -->

### Foundation{#foundation-6519}

* 在語言根層級建立語言復本時，不會調整頁面中的路徑。 若已建立語言副本（不是針對語言根，而是針對其下方的頁面），則路徑已正確變更。 (NPR-41364)
* 按鍵盤上的Esc鍵只能關閉「相對日期顯示」工具提示。 工具提示應在使用者選取使用者介面的任何部分時關閉。 (NPR-41394)
* 未當地語系化的字串 `Something went wrong while adding the private key.` 在中新增錯誤的私密金鑰檔案時 **編輯使用者** > **金鑰存放區**. (NPR-41366)
* AEM 6.5環境中的Microsoft®SharePoint和Microsoft® One Drive需要圖示。 (NPR-41354)
* 未當地語系化的「使用者ID/密碼不符」。 字串輸入 **安全性** > **使用者** > **建立** 對話方塊。 (NPR-41245)
* 彈出視窗程式碼和事件處理常式會載入兩次，這會破壞使用者建立的Coral3型使用者介面。 (NPR-41171)
* 在AEM Sites主控台中使用「全選」後，取消選取無法正常運作。 (NPR-41304)

<!--#### Content distribution{#foundation-content-distribution-6519}

* T -->

#### 整合{#integrations-6519}

* AEM電子郵件行銷活動中的SMS連結未正確寫入；它們包含HTML錨點元素。 (NPR-41211)
* 在帳戶設定畫面中使用的措辭不應使用新的認證型別。 (NPR-41210)
* 正在移動Analytics報表匯入排程器 `ManagedPollConfig` 到sling jobs。 將兩個不同的分析架構附加至不同網站的不同報表套裝時， `ManagedPollConfig` 僅輪詢其中一項。 (NPR-41209)
* 當此值重設為預設時，先前選取的時間範圍按鈕保持啟用狀態。 在AEM的內容深入分析控制面板中，預設時間範圍會設定為一週，並將內容深入分析顯示為每週資料。 現在，如果使用者選取其他時間範圍選項，例如小時、日、月和年，資料會根據選取的值而變更。 但是，如果重設值，預設情況下，可見的時間範圍為周，但仍會選取先前選取的時間範圍選項。 (NPR-41246)

#### Oak{#oak-6519}

* 反向連線公用程式，可在非同步索引延遲時限制寫入AEM的速率。 (NPR-40985)

#### Platform{#foundation-platform-6519}

* 含方括弧的QueryBuilder查詢被錯誤轉譯為xpath 。 (NPR-41298)

<!--#### Replication{#foundation-replication-6519}

* R -->

<!--#### Sling{#foundation-sling-6519}

* W -->

#### 翻譯專案{#foundation-translation-6519}

* 建立頁面「A」的語言副本時，應自動建立參考頁面、體驗片段、內容片段和資產的語言副本。 此外，在新路徑新建立的頁面「A」語言副本應該會將其參考更新為頁面、體驗片段、內容片段和資產的個別新建立語言副本。 (NPR-41076)

<!--#### User interface{#foundation-ui-6519}

* A -->

<!--#### WCM{#wcm-6519}

* A -->

#### 工作流程{#foundation-workflow-6519}

* 無法完成收件匣中的工作。 嘗試完成工作並選取動作時，下拉式選單中只會顯示「未定義」值。 這表示使用者無法套用AEM 6.5.18 Service Pack。 (NPR-41402和NPR-41473)
* 無法完成收件匣中的工作。 嘗試完成zip檔案、資產報告、移動（成功或失敗）或資產到期的工作時，下拉式清單中沒有值（僅限「未定義」）。 (NPR-41305)
* 當使用者選取 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** >執行個體，然後選取執行中的工作流程，再選取 **[!UICONTROL 檢視裝載]**，則會導致500錯誤頁面。 (NPR-41325)

## 安裝 [!DNL Experience Manager] 6.5.19.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.19.0需要 [!DNL Experience Manager] 6.5.請參閱 [升級檔案](/help/sites-deploying/upgrade.md) 以取得詳細指示。 <!-- UPDATE FOR EACH NEW RELEASE -->
* 您可在Adobe上取得Service Pack下載 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.19.0.zip).
* 在具有MongoDB和多個執行個體的部署上，安裝 [!DNL Experience Manager] 使用封裝管理程式的其中一個Author執行個體上的6.5.19.0 。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe不建議您移除或解除安裝 [!DNL Experience Manager] 6.5.19.0套件。 因此，在安裝套件之前，您應該建立 `crx-repository` 以防您必須將其回覆。 <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### 在上安裝Service Pack [!DNL Experience Manager] 6.5{#install-service-pack}

1. 如果執行個體處於更新模式（從舊版更新執行個體時），請在安裝前重新啟動執行個體。 如果執行個體的目前運作時間很高，Adobe建議重新啟動。

1. 安裝之前，請拍攝快照或進行全新備份 [!DNL Experience Manager] 執行個體。

1. 下載Service Pack，從 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.19.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. 開啟封裝管理員，然後選取 **[!UICONTROL 上傳套裝]** 以上傳套件。 若要瞭解更多，請參閱 [封裝管理員](/help/sites-administering/package-manager.md).

1. 選取封裝，然後選取 **[!UICONTROL 安裝]**.

1. 若要更新S3聯結器，請在安裝Service Pack後停止執行個體，將現有聯結器取代為安裝資料夾中提供的新二進位檔案，然後重新啟動執行個體。 另請參閱 [Amazon S3資料存放區](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>在安裝Service Pack期間，套件管理員UI上的對話方塊有時會退出。 Adobe建議您先等待錯誤記錄穩定下來，再存取部署。 等待與更新程式套件組合解除安裝相關的特定記錄，再確認安裝成功。 此問題通常發生在 [!DNL Safari] 瀏覽器，但可能間歇性地在任何瀏覽器上發生。

**自動安裝**

您可以使用兩種不同的方法來自動安裝 [!DNL Experience Manager] 6.5.19.0。<!-- UPDATE FOR EACH NEW RELEASE -->

* 將套件置於 `../crx-quickstart/install` 資料夾（當伺服器線上上可用時）。 套件會自動安裝。
* 使用 [來自封裝管理員的HTTP API](/help/sites-administering/package-manager.md#package-share). 使用 `cmd=install&recursive=true` 以便安裝巢狀套件。

>[!NOTE]
>
>Experience Manager6.5.19.0不支援Bootstrap安裝。 <!-- UPDATE FOR EACH NEW RELEASE -->

**驗證安裝**

若要瞭解經過認證可搭配此版本使用的平台，請參閱 [技術需求](/help/sites-deploying/technical-requirements.md).

1. 產品資訊頁(`/system/console/productinfo`)顯示更新的版本字串 `Adobe Experience Manager (6.5.19.0)` 在 [!UICONTROL 已安裝的產品]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. 所有OSGi套件組合都是 **[!UICONTROL 作用中]** 或 **[!UICONTROL 片段]** 在OSGi主控台中(使用Web主控台： `/system/console/bundles`)。

1. OSGi套件 `org.apache.jackrabbit.oak-core` 是1.22.17版或更新版本(使用Web主控台： `/system/console/bundles`)。 <!-- NPR-41292 for 6.5.19.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### 安裝Service Pack for [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

如需在Experience Manager Forms上安裝Service Pack的說明，請參閱 [Experience Manager Forms Service Pack安裝指示](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>調適型表單功能 (適用於 [AEM 6.5 QuickStart](https://experienceleague.corp.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html)) 僅用於探索和評估目的。若要供生產使用，必須獲得 AEM Forms 的有效許可；調適型表單的功能需要適當許可才可使用。

### 安裝Experience Manager內容片段的GraphQL索引套件{#install-aem-graphql-index-add-on-package}

使用GraphQL的客戶必須安裝 [使用GraphQL索引套件1.1.1Experience Manager內容片段](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

如此一來，您就可以根據使用者實際使用的功能，新增必要的索引定義。

無法安裝此套件可能會導致GraphQL查詢變慢或失敗。

>[!NOTE]
>
>每個執行個體僅安裝此套件一次；不需要隨每個Service Pack重新安裝。

### UberJar{#uber-jar}

The UberJar for [!DNL Experience Manager] 6.5.19.0可在以下網址取得： [Maven中央存放庫](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.19/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

若要在Maven專案中使用UberJar，請參閱 [如何使用UberJar](/help/sites-developing/ht-projects-maven.md) 並在專案POM中加入下列相依性： <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.19</version>
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

### AEM Forms的已知問題

#### 支援平台

* WebLogic JEE伺服器不支援高於1.8.0_281的JDK版本。 (FORMS-8498、CQDOC-20383)
* 作為 [!DNL Microsoft® Windows Server 2019] 不支援 [!DNL MySQL 5.7] 和 [!DNL JBoss® EAP 7.1]， [!DNL Microsoft® Windows Server 2019] 不支援全包安裝 [!DNL Experience Manager Forms 6.5.10.0]. (CQDOC-18312)
* JDK 11.0.20不支援在JEE安裝程式上安裝AEM Forms。 僅支援JDK 11.0.19或較舊版本以在JEE安裝程式上安裝AEM Forms。 (FORMS-10659)

#### 安裝

* 在JBoss® 7.1.4平台上，當使用者安裝Experience Manager6.5.16.0或更新版Service Pack時， `adobe-livecycle-jboss.ear` 部署失敗。 (CQ-4351522、CQDOC-20159)
* 升級至Windows Server 2022上的AEM Forms 6.5.18.0 JBoss® Turnkey完整安裝程式環境後，使用Java™ 11編譯輸出使用者端應用程式程式碼時，可能會發生下列編譯錯誤：

  ```
  error: error reading [AEM_Forms_Installation_dir]\sdk\client-libs\common\adobe-output-client.jar; java.net.URISyntaxException: 
  Illegal character in path at index 70: file:/[AEM_Forms_Installation_dir]/sdk/client-libs/common/${clover.jar.name} 1 error
  ```

  若要解決此問題，請執行以下步驟：
   1. 瀏覽至 `[AEM_Forms_Installation_dir]\sdk\client-libs\common\` 並解壓縮 `adobe-output-client.jar` 以擷取 `Manifest.mf` 檔案。
   1. 更新 `Manifest.mf` 移除專案以建立檔案 `${clover.jar.name}` 從class-path屬性。

      >[!NOTE]
      >
      > 您也可以使用就地編輯工具（例如7-zip）來更新 `Manifest.mf` 檔案。

   1. 儲存更新的 `Manifest.mf` 在 `adobe-output-client.jar` 封存。
   1. 儲存修改的專案 `adobe-output-client.jar` 檔案並重新執行安裝程式。 (CQDOC-20878)
* 安裝AEM Service Pack 6.5.19.0完整安裝程式後，使用JBoss® Turnkey的JEE上EAR部署會失敗。
若要解決問題，請找到 `<AEM_Forms_Installation_dir>\jboss\bin\standalone.bat` 檔案和更新 `Adobe_Adobe_JAVA_HOME` 至 `Adobe_JAVA_HOME` 執行configuration manager之前的所有事件。 (CQDOC-20803)

#### 安裝servlet片段(AEM Service Pack 6.5.14.0或更舊版本)

* 如果您要升級至AEM Service Pack 6.5.15.0或更新版本，而您的AEM執行個體在Tomcat 8.5.88上運作，則必須安裝servlet片段 *早於* 請繼續安裝Service Pack 6.5.15.0或更新版本。
* 您必須為所有應用程式伺服器(在JBoss® EAP 7.4.0上執行的除外)安裝servlet片段。

**安裝servlet片段：**

1. 下載servlet片段，從 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar).
1. 啟動應用程式伺服器。
1. 等待記錄檔穩定並檢查套件組合狀態。
1. 開啟Web控制檯套件組合。 預設URL為 `http://[Server]:[Port]/system/console/bundles`.
1. 選取 **[!UICONTROL 安裝]** 或 **[!UICONTROL 更新]**.
1. 選取下載的片段
   `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`
1. 選取 **[!UICONTROL 安裝]** 或 **[!UICONTROL 更新]**.
1. 等待應用程式伺服器穩定下來。
1. 停止應用程式伺服器。

#### 最適化表單

* 發佈調適型表單時，其所有相依性（包括原則）都會重新發佈，即使未進行任何修改亦然。 (FORMS-10454)
* 當使用者選擇在最適化表單中首次設定欄位時，儲存設定的選項未顯示在屬性瀏覽器中。 選擇在同一編輯器中設定最適化表單的其他欄位即可解決問題。
* 在最適化表單的指南容器中設定重新導向URL時，內嵌簽署會停止運作。 (FORMS-10493)若要解決此問題，請下載並安裝 [6.5.18.0的Hotfix](/help/release-notes/aem-forms-hotfix.md).
* 所有記錄檔案(DoR)範本都無法發佈。 僅發佈英文地區設定型DoR範本及其相關的Forms型DoR範本。 (FORMS-10535)若要解決此問題，請下載並安裝 [6.5.18.0的Hotfix](/help/release-notes/aem-forms-hotfix.md).


#### 互動式通訊

* 升級至AEM Service Pack 18後，無法在編輯模式中開啟具有大型內嵌影像的互動式通訊。 (FORMS-10578)若要解決此問題，請下載並安裝 [6.5.18.0的Hotfix](/help/release-notes/aem-forms-hotfix.md).

## 包含的OSGi套件組合和內容套件{#osgi-bundles-and-content-packages-included}

下列文字檔案列出中包含的OSGi套件組合和內容套件 [!DNL Experience Manager] 6.5.19.0： <!-- UPDATE FOR EACH NEW RELEASE -->

* [Experience Manager6.5.19.0中包含的OSGi套件組合清單](/help/release-notes/assets/65190_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager6.5.19.0中包含的內容套件清單](/help/release-notes/assets/65190_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 受限制的網站{#restricted-sites}

這些網站僅供客戶使用。 如果您是客戶且需要存取權，請聯絡您的Adobe客戶經理。

* [產品下載網址為licensing.adobe.com](https://licensing.adobe.com/)
* [聯絡Adobe客戶支援](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 產品頁面](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5檔案](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hant)
>* [訂閱 Adobe 優先產品更新](https://www.adobe.com/tw/subscription/priority-product-update.html)
