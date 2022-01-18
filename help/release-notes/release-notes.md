---
title: 的發行說明 [!DNL Adobe Experience Manager] 6.5
description: '[!DNL Adobe Experience Manager] 6.5說明，概述發行資訊、新增功能、安裝方式，以及詳細的變更清單。'
exl-id: 0288aa12-8d9d-4cec-9a91-7a4194dd280a
source-git-commit: 1cfa01544ad8bf0adafd55e696a6844a8edf1007
workflow-type: tm+mt
source-wordcount: '3894'
ht-degree: 2%

---

# [!DNL Adobe Experience Manager] 6.5 Latest Service Pack Release Notes {#aem-service-pack-release-notes}

## 發行資訊 {#release-information}

| 產品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.11.0 |
| 類型 | Service Pack發行 |
| 日期 | 2021 年 11 月 25 日 |
| 下載URL | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.11.zip) |

## 包含的項目 [!DNL Adobe Experience Manager] 6.5.11.0 {#what-is-included-in-aem}

[!DNL Adobe Experience Manager] 6.5.11.0包含自2019年4月發行6.5版以來所發行的新功能、客戶要求的重要增強功能，以及效能、穩定性和安全性等改善項目。 Service Pack安裝在 [!DNL Adobe Experience Manager] 6.5。

中推出的主要功能和增強功能 [!DNL Adobe Experience Manager] 6.5.11.0為：

* 新增多欄位支援多行文字資料類型。

* 增強功能，讓使用者了解目前在背景執行的非同步作業，以防止他們在相同路徑上觸發多個非同步作業。

* 您可以使用 [SEO索引包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/sites-seo-index-content-1.0.0.zip). 它支援網站地圖、替代URL、機器人中繼標籤，以及 [!DNL Core Components].

* 使用者體驗增強功能會顯示資料夾中存在的資產數量。 若是資料夾中超過1000個資產， [!DNL Assets] 顯示1000+。

   ![資料夾中的資產數](/help/assets/assets/browse-folder-number-of-assets.png)

* Adobe資產連結的業務設定檔支援。

* 您現在可以使用 [!DNL Dynamic Media] 來設定一般設定，而非必須完成 [!DNL Dynamic Media Classic] 案頭應用程式。 請參閱 [配置Dynamic Media一般設定](/help/assets/dm-general-settings.md).

   ![DM一般設定](/help/assets/assets-dm/dm-general-settings.png)

* 您現在可以使用 [!DNL Dynamic Media] 來設定發佈設定，而不需要完成 [!DNL Dynamic Media Classic] 案頭應用程式。 請參閱 [設定Dynamic Media發佈設定](/help/assets/dm-publish-settings.md).

   ![DM發佈設定](/help/assets/assets-dm/dm-publish-setup.png)

* 內建存放庫(Apache Jackrabbit Oak)更新至1.22.9。

以下是中提供的修正清單 [!DNL Experience Manager] 6.5.11.0版。

### [!DNL Sites] {#sites-65110}

若要使用內容片段搭配GraphQL存取無周邊內容傳送，並使用增強的內容片段模型和編輯器功能，請安裝 [索引定義套件](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.0.0.zip)，並重新索引下列非同步AEM索引定義：

* /oak:index/assetPrefixNodename

* /oak:index/fragments

* /oak:index/graphqlConfig


已在 [!DNL Sites]:

* 建立內容片段時，無法看到建立內容片段的範本(SITES-3365)。

* 規則運算式和 [!UICONTROL 不重複] 欄位選項在中無法運作 [!UICONTROL appsUrl] 內容片段編輯器中的模型(SITES-1823)。

* 設定新增於 `/apps/system` 節點，而不是 `/libs` 安裝舊版Service Pack時(SITES-3203)。

* 使用內容片段的功能在安裝舊版Service Pack時無法正常運作(SITES-3151)。

* 排序在中無法運作 [!UICONTROL 內容片段模型] 主控台(SITES-2722)。

* GraphiQL未載入模型（結構），且端點JSON出現錯誤(SITES-2428)。

* 已新增至的分項清單欄位類型 [!UICONTROL 內容片段模型] 中未顯示 [!UICONTROL 內容片段模型編輯器] (SITES-2391)。

* Tags data type does not support certain data types (SITES-2390).

* [!UICONTROL Content Fragment Rest API] is exporting outdated tag values (SITES-2386).

* 階層連結中的箭頭在內容片段編輯器中未正確對齊(SITES-2341)。

* 大型資料集的內容片段參考搜尋速度緩慢(SITES-2147)。

* [!UICONTROL CopyUrl] 在 [!UICONTROL 內容片段編輯器] (SITES-2007)。

* 當內容片段與相關模型一起發佈且模型引入制動變更時(SITES-1988)，不會顯示警告。

* 針對編輯內容片段模型的不同使用案例(SITES-1980)，編輯內容片段模型的URL不同。

* 使用內嵌，以相同標題建立兩個內容片段時 [!UICONTROL 新內容片段] 動作，精靈會傳回相同的片段路徑(SITES-1978)。

* 自動完成在中無法運作 [!UICONTROL 內容片段模型] 搜尋面向(SITES-1976)。

* 如果內容片段包含巨大的巢狀片段階層，則 [!UICONTROL 內容片段編輯器] 載入側面板時變得無回應(SITES-1974)。

* 片段選擇器路徑中的全域搜尋無法運作(SITES-1973)。

* 移動內容片段時，參考正在更新(SITES-1897)。

* 卡片檢視和欄檢視中缺少建立頁面的選項(NPR-37549)。

* 在Launch頁面上重新排序元件時，提升Launch並不會保留元件的重新排序(NPR-37539)。

* 選取清單中所有項目的選項在轉出頁面上沒有作用(NPR-37443)。

* 排程啟動多個頁面會為開啟新的JCR工作階段 `wcm-workflow-service` 使用者(NPR-37417)。

* Sites主控台中資料夾的移動作業失敗，並出現「無法擷取所選項目的啟動資訊」錯誤訊息(NPR-37340)。

* When generating a thumbnail for blueprint and rolling out to live copies, the inheritance for tabs after thumbnail in live copies is broken (NPR-37190).

* The filter predicate to display Live Copy does not display all the live copies (NPR-37126).

* 在作者上呼叫復寫事件處理常式時，復寫事件不會傳回所有標示為刪除的上層和下層頁面清單(NPR-37123)。

* When saving a multi-valued property using Bulk Editor, then the comma-separated string is stored as the first element of the array (NPR-37089).

* 在行動版面中無法調整元件版面大小(NPR-37086)。

* 新增轉出設定後，儲存頁面屬性時，即時副本層級未正確建立新節點(NPR-37084)。

* 使用者無法為新主版頁面建立Live Copy或使用頁面屬性轉出(SITES-3442)。

* 標籤顯示標籤名稱而非標題和關閉選項並未完全移除標籤，因為當屬性層級取消繼承時，標籤屬性無法正常運作(NPR-36831)。

* 取消選取所有項目的選項無法運作，且標題與表格中顯示即時副本清單的頁面的第一列重疊(NPR-37070)。

* 在工作流程中使用的自訂對話方塊中，嘗試驗證對話方塊時，Experience Manager會在瀏覽器主控台中發生錯誤而失敗(GRANITE-35049)。

下列協助工具增強功能適用於 [!DNL Adobe Experience Manager Sites]:

* 螢幕助讀程式現在會宣佈 [!UICONTROL 網站參考] 和 [!UICONTROL 語言副本] 選項(SITES-1791)。

* 瀏覽器模式的焦點順序現在會依序移動至使用者介面上的各種選項(SITES-1791)。

* 螢幕助讀程式現在會提供旁白，說明所選樹狀項目是否處於選取狀態，並向使用者宣告已顯示動作區域(SITES-2109)。

* 螢幕助讀程式現在會在選取篩選或搜尋頁面時顯示載入指標(SITES-1790)。

* 螢幕助讀程式現在會提供旁白，說明 [!UICONTROL 篩選] 選項不會在左側邊欄中傳回任何搜尋結果(SITES-1599)。

* 在瀏覽模式中導覽時，螢幕助讀程式會在按下鍵時提供內容頁面的角色和頁面的選取狀態旁白(SITES-1579)。

* 螢幕助讀程式現在會在 [!UICONTROL 附註新增] 選項(SITES-1573)。

* 表單欄位現在除了預留位置外還有視覺標籤，因此在輸入欄位值時，螢幕助讀程式的使用者可獲得適當的引導(SITES-1258)。

### [!DNL Assets] {#assets-65110}

下列協助工具增強功能適用於 [!DNL Assets]:

* 在 [!DNL Assets] 存放庫，當使用 `Tab` 若要將焦點移至開啟焦點快速動作的第一個項目，螢幕助讀程式會朗讀焦點項目的名稱。
* 在 [!DNL Dynamic Media] [!UICONTROL 檢視器預設集編輯器]，如果陰影顏色和邊框顏色不存在，則使用禁用的屬性禁用輸入。 鍵盤使用者無法聚焦輸入，而螢幕助讀程式不會將控制項的狀態宣佈為已停用。
* 在 [!DNL Dynamic Media]，在介面中建立新的視訊編碼設定檔時， [!UICONTROL 智慧型裁切比例] 選項會標示為協助工具，讓螢幕助讀程式能正確宣告。

* 您現在可以存取 [!DNL Experience Manager Assets] 使用鍵盤。

已在 [!DNL Assets]:

* 貢獻者群組的使用者導覽至DAM資產存放庫時，此為例外 `POST` 會針對建立集合而觸發請求。 此 `POST` 請求失敗並反映記錄中的錯誤(NPR-37171)。

* 建立具有巢狀資料夾結構的Blueprint的Live Copy時，來源資料夾的修改屬性不會在Live Copy資料夾中更新(NPR-37449)。

* 選取多個資產並修改中繼資料欄位值時，儲存資產不會保留值。 此外，未套用中繼資料變更(NPR-37341)。

* 選取多個資產並修改屬性時，自訂屬性（下拉式清單）值會以預設值覆寫(NPR-36437)。

* 手冊、傳單和PDF範本產生錯誤的InDesign轉譯(NPR-36433)。

* 儲存 [!DNL Adobe Target] 活動 [!DNL Experience Manager] 定位模式在 [!DNL Adobe Analytics] 參考報表量度(NPR-37167)。

* 使用混合大小寫網域名稱的電子郵件使用者簽出資產時，資產不會顯示在使用者的已簽出資產中， [!DNL Asset Link] (CQ-4329266)。

<!-- Add 
* [!DNL Adobe Asset Link] is not able to access the digital assets even when the [!DNL Creative Cloud] and [!DNL Experience Management] entitlements are provided by two different organizations. -->

* 新增視訊與上傳至頁面時產生的自訂中繼資料，會顯示關於未知命名空間的錯誤，即使已註冊命名空間亦然(CQ-4331471)。

* 在 [!DNL Assets]，如果 [!DNL Launcher] 已停用，則手動觸發時中繼資料回寫無法運作(CQ-4329082)。

### [!DNL Dynamic Media] {#dynamic-media-65110}

下列錯誤修正適用於 [!DNL Dynamic Media]:

* 資產未在 [!DNL Dynamic Media] 在中還原資產版本時 [!DNL Experience Manager] (NPR-37421)。

* 發佈PDF檔案時未發佈ECatalog(CQ-4329886)。

* 開啟已發佈的頁面時，若元件使用現成的預設集(CQ-4329205)，則3D資產不會載入。

* 大型存放庫的PDF資產處理問題(CQ-4328711)。

* PDF處理錯誤不會傳播至 [!DNL Experience Manager] 在 [!DNL Scene7] (CQ-4331145)。

* 使用者看不到.MOV資產的預設中繼資料屬性(CQ-4332546)。

* 無法將.MXF視訊檔案上傳至 [!DNL Dynamic Media] 使用 [!DNL Experience Manager] (CQ-4329709)。

* 設定自訂公司根目錄時出現上傳問題(CQ-4332800)。

* 在 [!DNL Experience Manager] 包含自定義啟動器的設定 `ActivationModel` 隨著工作流程，Experience Manager會因上傳PDF檔案時發生記憶體問題而當機。 (CQ-4330512).

* 中的效能問題 `DamEventRecorder` (CQ-4334072)。

* 如果可購買的視訊超連結（連結URL）包含特殊字元，則目標URL會由檢視器編碼，並結果為錯誤的產品頁面(CQ-4331639)。

* 在視訊描述檔頁面中，如果使用者在頁面載入時立即選取視訊描述檔，工具列選項就會消失(CQ-4308521)。

* 由於JCR同時寫入，DM資產處理失敗(CQ-4333489)。

* 如果使用者的視訊設定檔根節點上已定義視訊設定檔根節點的自訂存取原則，則存取「視訊設定檔」頁面會失敗(CQ-4332941)。

* 在可縮放的影像中，使用快捷鍵(「+」、「 — 」或「Esc」鍵，將螢幕助讀程式的焦點補漏白(CQ-4290719)。

* 當使用者按一下表單模式快速鍵(「F」)時，螢幕助讀程式不會映射 [!UICONTROL 內嵌大小] 功能表按鈕 [!UICONTROL 取得內嵌] 代碼對話框(CQ-4290929)。

* When using keyboard navigation to open the email link popup window, the error suggestions displayed on the user interface for the &#39;To&#39; and &#39;From&#39; fields are not descriptive (CQ-4290930).

* When navigating to the email link dialog box, the screen reader does not narrate the label information for the newly added edit fields on using the down arrow and form mode shortcut key (&#39;F&#39;) (CQ-4290934).

* 導覽至電子郵件連結對話方塊時，螢幕助讀程式不會反映「收件人」和「發件人」必填欄位(CQ-4290935)的視覺星號(*)符號。

* 使用者無法使用快速鍵(&#39;D&#39;, &#39;R&#39;)(CQ-4312118)來識別地標和地區。

<!-- Anuj to check if this section is required or not. We have an enh. in CIF area that is mentioned. It is added above and not part of this bug fix section.
-->

### 商務 {#commerce-65110}

* 使用 [!UICONTROL 稍後發佈] 選項，則使用者介面不會將狀態反映為 [!UICONTROL 發佈掛起] (CQ-4334229)。

* 取消發佈資料夾並未完全取消發佈該資料夾的產品，產品會從發佈者中移除，但仍存在於製作執行個體中(CQ-4332731)。

### 平台 {#platform-65110}

* When a user clicks on the reorder icon for a multifield option, the scroll bar disappears from the user interface (CQ-4331100).

* 升級後，當使用者開啟工作區登入容器元件時，使用者介面上看不到對話方塊的標題(CQ-4316173)。

### Integrations {#integrations-65110}

* 儲存 [!DNL Adobe Target] 活動 [!DNL Experience Manager] 定位模式在 [!DNL Adobe Analytics] 參考報表量度(NPR-37167)。

### 專案 {#projects-65110}

* 從升級時 [!DNL Experience Manager] 6.5.8.0到6.5.9.0版，則安裝會覆寫上的屬性 `/content/dam/projects`. 它會將指派的中繼資料結構和資料夾屬性重設為預設值(NPR-37124)。

### 使用者介面 {#user-interface-65110}

* 表示模型的資料夾圖示不正確(NPR-37176)。

* 使用者使用路徑欄位瀏覽器執行搜尋或瀏覽時，畫面顯示錯誤的節點(NPR-37175)。

* 在發佈執行個體上，傳入的要求會遭到數分鐘的封鎖(NPR-37169)。

* 在自訂工作流程的對話方塊中新增多欄位屬性時，對話方塊無法繼續，使用者無法關閉對話方塊(NPR-37075)。

### 翻譯專案 {#translation-65110}

* 翻譯啟動的自動促銷失敗，但有例外(NPR-37528)。

* 翻譯體驗片段時沒有更新URL語言副本的參考(NPR-37522)。

* 在不符合語言根結構路徑的路徑中建立體驗片段時，將該頁面新增至翻譯專案會反映空白錯誤訊息(NPR-37425)。

* 修改包含體驗片段的頁面（英文）並傳送以進行翻譯時，已翻譯的體驗片段會被英文內容覆寫(NPR-37283)。

* 翻譯提供者篩選器無法正常運作(NPR-37186)。

* 針對範例網站內容，體驗片段和折疊式功能表元件沒有立即取得轉譯(NPR-37170)。

* 升級至 [!DNL Experience Manager] 6.5.9.0，將頁面新增至翻譯專案時顯示空白錯誤訊息(NPR-37105)。

* 在launch中新增頁面時，專案中不包含名稱類似的翻譯頁面(NPR-37082)。

* 使用轉譯器介面將表單字典匯出為.xliff檔案時，匯出檔案的欄位順序不正確(NPR-37048)。

* 從翻譯專案轉出上層頁面時，會刪除語言專屬的子頁面(NPR-36998)。

* 建立翻譯專案時，頁面的循環參考會觸發啟動而導致錯誤(CQ-4332982)。

* 翻譯的體驗片段和頁面中的體驗片段連結包含啟動參考(NPR-37649)。

### Sling {#sling-65110}

* 上傳新套件時，MapEntries對映中的記憶體別名已移除(NPR-37067)。

### 工作流程 {#workflow-65110}

* `Deactivate` 方法輸入 `InboxOmniSearchHandler` 顯示Null指標異常(NPR-37533)。

### [!DNL Communities] {#communities-65110}

* 使用者無法新增評論至頁面， `Post` 操作失敗，錯誤代碼為500(NPR-37156)。

* 部署應用程式時，由於SyncManager的長時間執行工作階段，發現區段未找到例外狀況(NPR-37351)。

* 使用者無法在論壇討論貼文上看到執行緒回覆(NPR-37083)。




<!--
Need to verify with Engineering, the status is currently showing as Resolved
-->


<!--
### [!DNL Brand Portal] {#brandportal-65110}

*

-->

### [!DNL Forms] {#forms-65110}


>[!NOTE]
>
>* [!DNL Experience Manager Forms] 會在預定的 [!DNL Experience Manager] Service Pack 發行日期一週後發行附加元件的套件。


**調適型表單**

* 協助工具 — 當您設定 `Wizard` 版面中，導覽按鈕沒有Aria標籤和角色(NPR-37613)。

* 適用性表單中的日期欄位無法如預期運作(NPR-37556)。

* 核取方塊和選項按鈕元件的標籤文字長度過長時，文字無法適當調整大小(NPR-37294)。

* 將樣式變更套用至AEM Forms容器元件的感謝訊息時，這些變更不會在來源適用性表單中複製(NPR-37284)。

* 與 `Switch` 元件(NPR-37268)。

* 使用鍵盤鍵導覽至 `Submit` 選項並按 `Enter` 索引鍵，您可以多次提交最適化表單(CQ-4333993)。

* 檔案附件元件的移除操作無法如預期運作(NPR-37376)。

* 當欄位的標籤在翻譯成各種語言的適用性表單中超過1000個字元時，字典無法擷取標籤的翻譯(CQ-4329290)。

**文件服務**

* An error displays while using the Assembler service (NPR-37606):

   ```TXT
     500 Internal Server Error
   ```

* 將文檔附件傳遞到組合器服務時，出現以下異常(NPR-37582):

   ```TXT
     com.adobe.livecycle.assembler.client.ProcessingException: ⁪: Failed to execute the DDX
   ```

* 將PDF檔案轉換為PDF-A/1BPDF檔案後，資料中缺少右括弧(NPR-37608)。

**HTML5 Forms**

* 安裝AEM 6.5.10.0時，XDP表單的HTML預覽無法運作(NPR-37503、CQ-4331926)。

* 將PDF forms移轉至以各種語言HTML5個表單時發生文字重疊問題(NPR-37173)。

**字母**

* 當您提交信函並在HTML檢視中重新開啟信函時，文字檔案片段的位置不會維持相同(NPR-37307)。

**表單工作流程**

* 若是內嵌容器工作流程，您會收到多封工作流程完成電子郵件，即使選取 `Notify on Complete of Container Workflow` 選項(NPR-37280)。

**Foundation JEE**

* 安裝AEM 6.5 Forms Service Pack 9後，CRX存放庫URL已無法使用(NPR-37592)。

**在AEM Forms 6.5.11.1中修正的問題**

>[!NOTE]
>
>如果您尚未升級至AEM 6.5.11.0 Forms，請直接安裝AEM Forms 6.5.11.1附加元件套件。 若您已安裝AEM 6.5.11.0 Forms,Adobe建議升級至AEM 6.5.11.1 Forms。

* 安裝Forms 6.5.11.0附加元件套件後，提交動作、傳送電子郵件和叫用AEM工作流程即停止運作。
* 安裝Microsoft 6.5.11.0附加套件後，CreatePDF操作停止將Forms Word檔案轉換為PDF檔案。
* (僅限 JEE) 針對 Apache Log4j2 回報的重大安全漏洞 (CVE-2021-44228 和 CVE-2021-45046)。
* （僅限JEE）6.5.11.0修補程式中的組合器DSC包含錯誤的代碼，如規格版本和實際版本。


如需安全性更新的詳細資訊，請參閱 [[!DNL Experience Manager] 安全性佈告欄頁面](https://helpx.adobe.com/security/products/experience-manager.html).

## 安裝6.5.11.0 {#install}

**設定需求和詳細資訊**

* Experience Manager6.5.11.0需要Experience Manager6.5。請參閱 [升級檔案](/help/sites-deploying/upgrade.md) 以取得詳細指示。
* Service Pack下載可在Adobe上取得 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* 在具有MongoDB和多個執行個體的部署上，使用套件管理器在其中一個製作執行個體上安裝Experience Manager6.5.11.0。

>[!NOTE]
>
>Adobe不建議移除或解除安裝 [!DNL Adobe Experience Manager] 6.5.11.0包。

### 安裝Service Pack {#install-service-pack}

在 [!DNL Adobe Experience Manager] 6.5執行個體，請依照下列步驟操作：

1. 如果執行個體處於更新模式（從舊版更新執行個體時），請先重新啟動執行個體再進行安裝。 Adobe建議，如果執行個體的目前正常運行時間很長，則重新啟動。

1. 安裝之前，請拍攝快照或對 [!DNL Experience Manager] 例項。

1. 從下載Service Pack [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.11.zip).

1. 開啟套件管理器，然後按一下&#x200B;**[!UICONTROL 「上傳套件」]**&#x200B;即可上傳套件。要了解更多資訊，請參閱 [封裝管理員](/help/sites-administering/package-manager.md).

1. 選取套件，然後按一下 **[!UICONTROL 安裝]**.

1. 若要更新S3連接器，請在安裝Service Pack後停止執行個體，以安裝資料夾中提供的新二進位檔案取代現有連接器，然後重新啟動執行個體。 請參閱 [Amazon S3 Data Store](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>安裝Service Pack時，有時會退出套件管理程式UI上的對話方塊。 Adobe建議您先等待錯誤記錄穩定，再存取部署。 請等待與卸載更新程式捆綁相關的特定日誌，然後確保安裝成功。 通常，此問題會發生在 [!DNL Safari] 瀏覽器，但可在任何瀏覽器上間歇性發生。

**自動安裝**

自動安裝有兩種方式 [!DNL Experience Manager] 6.5.11.0（工作實例）:

A.將包裹放入 `../crx-quickstart/install` 資料夾。 程式包會自動安裝。

B.使用 [來自套件管理器的HTTP API](/help/sites-administering/package-manager.md#package-share). 使用 `cmd=install&recursive=true` 以便安裝嵌套包。

>[!NOTE]
>
>Adobe Experience Manager 6.5.11.0不支援安裝Bootstrap。

**驗證安裝**

1. 產品資訊頁面(`/system/console/productinfo`)顯示更新的版本字串 `Adobe Experience Manager (6.5.11.0)` 在 [!UICONTROL 已安裝的產品].

1. 所有OSGi套件組合 **[!UICONTROL 活動]** 或 **[!UICONTROL 片段]** 在OSGi控制台中(使用Web控制台： `/system/console/bundles`)。

1. OSGi捆綁 `org.apache.jackrabbit.oak-core` 為1.22.3版或更新版本(使用Web控制台： `/system/console/bundles`)。

若要了解經認證可與此版本搭配使用的平台，請參閱 [技術要求](/help/sites-deploying/technical-requirements.md).

<!-- 

### Install Adobe Experience Manager Forms add-on package {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Skip if you are not using Experience Manager Forms. Fixes in Experience Manager Forms are delivered through a separate add-on package a week after the scheduled [!DNL Experience Manager] Service Pack release.

1. Ensure that you have installed the Adobe Experience Manager Service Pack.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](/help/forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

>[!NOTE]
>
>Experience Manager 6.5.10.0 includes a new version of [AEM Forms Compatibility Package](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#aem-65-forms-releases). If you are using an older version of AEM Forms Compatibility Package and updating to Experience Manager 6.5.10.0, install the latest version of the package post installation of Forms Add-On Package.

### Install Adobe Experience Manager Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Skip if you are not using AEM Forms on JEE. Fixes in Adobe Experience Manager Forms on JEE are delivered through a separate installer.

For information about installing the cumulative installer for Experience Manager Forms on JEE and post-deployment configuration, see the [release notes](jee-patch-installer-65.md).

>[!NOTE]
>
>After installing the cumulative installer for Experience Manager Forms on JEE, install the latest Forms add-on package, delete the Forms add-on package from the `crx-repository\install` folder, and restart the server.

-->

### UberJar {#uber-jar}

適用於Experience Manager6.5.11.0的UberJar可於 [Maven Central存放庫](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.11/).

若要在Maven專案中使用UberJar，請參閱 [如何使用UberJar](/help/sites-developing/ht-projects-maven.md) 並在您的專案POM中加入下列相依性：

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.11</version>
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
| 整合 | 此 **[!UICONTROL AEM雲端服務選擇加入]** 螢幕已過時，因為 [!DNL Experience Manager] 和 [!DNL Adobe Target] Experience Manager6.5已更新整合。整合支援Adobe Target Standard API。 此API使用透過Adobe IMS的驗證，以及 [!DNL Adobe I/O] 並支援AdobeLaunch在儀器方面日益發揮的作用 [!DNL Experience Manager] 分析和個人化的頁面，選擇加入精靈的功能與您無關。 | 設定系統連線、Adobe IMS驗證，以及 [!DNL Adobe I/O] 透過個別 [!DNL Experience Manager] 雲端服務。 |
| 連接器 | 適用於Microsoft® SharePoint 2010和Microsoft® SharePoint 2013的AdobeJCR連接器已於Experience Manager6.5中淘汰。 | N/A |

## 已知問題 {#known-issues}

* 安裝AEM 6.5 Service Pack 11並嘗試下載狀態ZIP檔案時，Experience Manager會下載損毀的檔案。 下載並安裝 [AEM Sites SEO索引套件](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/sites-seo-index-content-1.0.0.zip) 在AEM執行個體上，再下載ZIP檔案以解決問題。

* As [!DNL Microsoft Windows Server 2019] 不支援 [!DNL MySQL 5.7] 和 [!DNL JBoss EAP 7.1], [!DNL Microsoft Windows Server 2019] 不支援全包安裝 [!DNL AEM Forms 6.5.10.0].

* 如果您要升級 [!DNL Experience Manager] 執行個體(從6.5版到6.5.10.0版)，您可以檢視 `RRD4JReporter` 例外 `error.log` 檔案。 若要解決問題，請重新啟動執行個體。

* 如果您安裝 [!DNL Experience Manager] 6.5 Service Pack 10或上一個Service Pack [!DNL Experience Manager] 6.5，資產自訂工作流程模型的執行階段副本(在 `/var/workflow/models/dam`)。
若要擷取執行階段副本，Adobe建議使用HTTP API，將自訂工作流程模型的設計時間副本與其執行階段副本同步：
   `<designModelPath>/jcr:content.generate.json`。

* 使用者可以在 [!DNL Assets] 並將巢狀資料夾發佈至 [!DNL Brand Portal]. 不過，資料夾的標題不會在 [!DNL Brand Portal] 直到重新發佈根資料夾為止。

* 當使用者首次選取以最適化表單設定欄位時，「屬性瀏覽器」中不會顯示儲存設定的選項。 在相同編輯器中選取以設定最適化表單的其他一些欄位，即可解決問題。

* 安裝Experience Manager6.5.x.x期間可能會顯示下列錯誤和警告訊息：
   * 「使用Target Standard API（IMS驗證）在Experience Manager中設定Adobe Target整合時，將體驗片段匯出至Target會導致建立錯誤的選件類型。 Target會建立數個具有「HTML」/來源「Adobe Target Classic」類型的選件，而非「體驗片段」/來源「Adobe Experience Manager」。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`:在granite/operations/maintenance找不到維護窗口。
   * 使用SUM、MAX和MIN等匯總函式時(CQ-4274424)，適用性表單伺服器端驗證會失敗。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`  — 在granite/operations/maintenance處找不到維護窗口。
   * 透過Shopbable Banner檢視器預覽資產時，Dynamic Media互動式影像中的熱點不會顯示。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` :等待登錄更改完成解除登錄的超時。

* 嘗試移動/刪除/發佈內容片段或網站/頁面時，內容片段參考擷取時會發生問題，因為背景查詢會失敗；即功能無法運作。
為確保操作正確，您需要將以下屬性添加到索引定義節點 `/oak:index/damAssetLucene` （不需要重新索引）:

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

## 包含的OSGi套件組合和內容套件 {#osgi-bundles-and-content-packages-included}

以下文字檔案列出包含在 [!DNL Experience Manager] 6.5.11.0:

* [Experience Manager6.5.11.0中包含的OSGi套件組合清單](assets/65110_bundles.txt)

* [Experience Manager6.5.11.0中包含的內容套件清單](assets/65110_packages.txt)

## 受限網站 {#restricted-sites}

這些網站僅供客戶使用。 如果您是Adobe，且需要存取權，請聯絡您的客戶經理。

* [透過licensing.adobe.com下載產品](https://licensing.adobe.com/)
* 請參閱 [如何聯絡Adobe客戶支援](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

## 以下版本的重要發行 [!DNL Adobe Experience Manager] 6.5 SP10{#key-releases-since-last-sp}

2021年8月26日至2021年11月25日，Adobe除了Service Pack外，還發行了下列內容：

* [!DNL Adobe Experience Manager] as a Cloud Service [2021.9.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/2021/release-notes-2021-9-0.html) 和 [2021.10.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=zh-Hant).

* [[!DNL Experience Manager] 案頭應用程式2.1(2.1.3.4)](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html).

* [Experience Manager Screens:Feature Pack 202109](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/release-notes/release-notes-fp-202109.html)


>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 產品頁面](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5檔案](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hant)
>* [訂閱 Adobe 優先產品更新](https://www.adobe.com/tw/subscription/priority-product-update.html)

