---
title: 使用最適化表單的最佳實務
seo-title: Best practices for working with adaptive forms
description: 說明設定AEM Forms專案、開發最適化表單及最佳化AEM Forms系統效能的最佳實務。
seo-description: Explains best practices for setting up an AEM Forms project, developing adaptive forms, and optimizing the performance for AEM Forms system.
uuid: ed95fc64-56b3-4ea1-a5ba-2e96953fca56
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 43c431e4-5286-4f4e-b94f-5a7451c4a22c
feature: Adaptive Forms
exl-id: 5c75ce70-983e-4431-a13f-2c4c219e8dde
source-git-commit: f05ddd2fb72258b7de5d361eb87f5e68e7ddd7ff
workflow-type: tm+mt
source-wordcount: '4529'
ht-degree: 0%

---

# 使用最適化表單的最佳實務 {#best-practices-for-working-with-adaptive-forms}

## 概觀 {#overview}

Adobe Experience Manager(AEM)表單可協助您將複雜的交易轉換為簡單、令人愉悅的數位體驗。 但是，它需要協調努力，以實施、構建、執行和維護高效和高效的AEM Forms生態系統。

本檔案提供的准則和建議，可供使用AEM Forms時（尤其是最適化表單元件），表單管理員、作者和開發人員受益。 本文探討從設定表單開發專案到設定、自訂、製作和最佳化AEM Forms等最佳實務。 這些最佳實務共同促進AEM Forms生態系統的整體效能。

此外，以下是一般AEM最佳實務的建議讀數：

* [最佳實務：部署和維護AEM](/help/sites-deploying/best-practices.md)
* [最佳實務：製作內容](/help/sites-authoring/best-practices.md)
* [最佳實務：管理AEM](/help/sites-administering/administer-best-practices.md)
* [最佳實務：開發解決方案](/help/sites-developing/best-practices.md)

## 設定和配置AEM Forms {#set-up-and-configure-aem-forms}

### 設定表單開發專案 {#setting-up-forms-development-project}

簡化和標準化的項目結構可以顯著減少開發和維護工作。 建置AEM專案時，建議使用Apache Maven這項開放原始碼工具。

* 使用Apache Maven `aem-project-archetype` 來建立和管理AEM專案的結構。 它會為您的AEM專案建立建議的結構和範本。 此外，它還提供構建自動化和更改控制系統，以幫助管理項目。

   * 使用maven `archetype:generate` 命令生成初始結構。
   * 使用maven `eclipse:eclipse` 命令，以產生eclipse專案檔案並將專案匯入eclipse中。

如需詳細資訊，請參閱 [如何使用Apache Maven建立AEM專案](/help/sites-developing/ht-projects-maven.md).

* FileVault工具或VLT可幫助您將CRX或AEM實例的內容映射到檔案系統。 它提供變更控制管理操作，如簽入和簽出AEM項目內容。 請參閱 [如何使用VLT工具](/help/sites-developing/ht-vlttool.md).

* 如果您使用Eclipse整合的開發環境，則可以使用AEM開發人員工具，將Eclipse IDE與AEM執行個體緊密整合，以建立AEM應用程式。 如需詳細資訊，請參閱 [AEM for Eclipse開發人員工具](/help/sites-developing/aem-eclipse.md).

* 請勿在/libs資料夾中儲存任何內容或進行任何修改。 在/app資料夾中建立覆蓋，以擴充或覆寫預設功能。

* 建立套件以移動內容時，請確定套件篩選路徑正確，且只提及必要的路徑。

* 請勿在/libs資料夾中儲存任何內容或進行任何修改。 在/app資料夾中建立覆蓋，以擴充或覆寫預設功能。

* 為軟體包定義正確的依賴項，以強制預先確定的安裝順序/順序。

* 請勿在/libs或/apps中建立任何可參考的節點。

### 製作環境規劃 {#planning-for-authoring-environment}

設定AEM專案後，請定義製作策略和自訂最適化表單範本和元件。

* 最適化表單範本是專用的AEM頁面，可定義最適化表單的結構和頁首 — 頁尾資訊。 範本有預先設定的最適化表單版面、樣式和基本結構。 AEM Forms提供立即可用的範本和元件，供您編寫最適化表單。 不過，您可以根據需求建立自訂範本和元件。 建議您收集在最適化表單中所需其他範本和元件的需求。 如需詳細資訊，請參閱 [自訂最適化表單和元件](/help/forms/using/adaptive-forms-best-practices.md#customize-components).
* AEM Forms可讓您根據下清單單模型建立最適化表單。 表單模型用作表單與AEM系統之間資料交換的介面，並為最適化表單內外的資料流提供基於XML的結構。 此外，表單模型會以模式和XFA限制的形式對最適化表單施加規則和限制。

   * **無**:使用此選項建立的最適化表單不使用任何表單模型。 從這種表單生成的資料XML具有帶有欄位和相應值的扁平結構。
   * **XML或JSON結構**:XML和JSON結構代表組織內的後端系統產生或使用資料的結構。 您可以將結構與適用性表單建立關聯，並使用其元素將動態內容新增至適用性表單。 結構的元素可在內容瀏覽器的「資料模型物件」標籤中取得，以製作最適化表單。 您可以拖放結構元素以建立表單。
   * **XFA表單範本**:如果您對XFA型HTML5表單有投資，則此表單是理想的表單模型。 它提供將XFA型表單轉換為最適化表單的直接方式。 任何現有的XFA規則都會保留在相關聯的最適化表單中。 產生的最適化表單支援XFA結構，例如驗證、事件、屬性和模式。
   * **表單資料模型**:如果您想要整合資料庫、網站服務和AEM使用者設定檔等後端系統，以預填最適化表單，並將提交的表單資料寫回後端系統，這是偏好的表單模型。 表單資料模型編輯器可讓您在表單資料模型中定義和設定實體和服務，以供您建立最適化表單。 如需詳細資訊，請參閱 [AEM Forms資料整合](/help/forms/using/data-integration.md).

請務必謹慎選擇不僅符合您的要求，而且能延伸您對XFA和XSD資產的現有投資（如果有的話）的資料模型。 建議使用XSD模型來建立表單範本，因為產生的XML包含的資料與架構所定義的XPATH相同。 使用XSD模型作為表單資料模型的預設選項，也有助於將表單設計與後端系統分離，後端系統處理並取用資料，而且由於表單欄位的一對一對應，因此可改善表單的效能。 此外，欄位的BindRef可以在XML中使其資料值的XPATH成為。

如需詳細資訊，請參閱 [建立最適化表單](/help/forms/using/creating-adaptive-form.md).

* 最適化表單中有一些常見區段。 您可以識別它們，並定義策略以促進內容重複使用。 最適化表單可讓您建立獨立的片段，並在各表單間重複使用。 您也可以將最適化表單中的面板儲存為片段。 片段中的任何變更都會反映在所有相關聯的表單中。 它可協助您縮短製作時間，並確保各表單的一致性。 此外，片段的使用讓最適化表單變得精簡，進而改善製作體驗，尤其是大型表單。 如需詳細資訊，請參閱 [最適化表單片段](/help/forms/using/adaptive-form-fragments.md).

### 自訂最適化表單和元件 {#customize-components}

* AEM Forms提供現成可用的最適化表單範本，供您建立最適化表單。 您也可以建立自己的範本。 AEM提供靜態和可編輯的範本。

   * 靜態範本由開發人員定義和設定。
   * 可編輯的範本由作者使用範本編輯器建立。 範本編輯器可讓您定義範本中的基本結構和初始內容。 使用該模板的所有表單中都會反映結構層中的任何修改。 初始內容可以包括預先配置的主題、預填服務、提交操作等。 不過，可以使用表單編輯器修改表單的這些設定。 如需詳細資訊，請參閱 [最適化表單範本](/help/forms/using/template-editor.md).

* 若要設定特定欄位或面板例項的樣式，請使用 [內嵌樣式](/help/forms/using/inline-style-adaptive-forms.md). 或者，您可以在CSS檔案中定義類，並在元件的CSS類屬性中指定類名。
* 在元件中加入用戶端程式庫，以在使用該元件的適用性表單或片段間一致地套用樣式。 如需詳細資訊，請參閱 [建立最適化表單頁面元件](/help/forms/using/custom-adaptive-forms-templates.md).
* 在適用性表單容器屬性的CSS檔案路徑欄位中，指定指向用戶端資料庫的路徑，以套用在用戶端資料庫中定義的樣式以選取適用性表單。
* 若要建立樣式的用戶端資料庫，您可以在主題編輯器基底clientlib或表單容器屬性中設定自訂CSS檔案。
* 適用性表單提供面板配置，例如回應式、索引標籤式、折疊式和精靈，以控制表單元件在面板中的佈局方式。 您可以建立自訂面板配置，並讓表單作者使用。 如需詳細資訊，請參閱 [建立最適化表單的自訂版面元件](/help/forms/using/custom-layout-components-forms.md).
* 您也可以自訂特定的最適化表單元件，例如欄位和面板版面。

   * 使用 [覆蓋](/help/sites-developing/overlays.md) 修改元件副本的功能。 不建議修改預設元件。
   * 若要在/libs中自訂現成可用的最適化表單元件的版面， [建立自訂配置元件](/help/forms/using/custom-layout-components-forms.md) 除了 [預設配置](/help/forms/using/layout-capabilities-adaptive-forms.md).
   * 透過建立自訂小工具或外觀來引入自訂互動。 不建議修改預設元件。 如需詳細資訊，請參閱 [外觀框架](/help/forms/using/introduction-widgets.md).

* 請參閱 [處理個人識別資訊](/help/forms/using/adaptive-forms-best-practices.md#p-handling-personally-identifiable-information-p) 有關處理PII資料的建議。

### 建立表單範本

您可以使用 **配置瀏覽器**. 若要啟用表單範本，請參閱 [建立最適化表單範本](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/creating-your-first-adaptive-form/create-adaptive-form-template.html?lang=en).

您也可以從其他製作電腦上建立的適用性表單套件上傳表單範本。 表單範本可透過安裝 [aemforms-references-*套件](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en). 建議的一些最佳實務為：
* 此 **nosamplecontent** runmode僅建議作者使用，不建議發佈節點使用。
* 製作資產（例如最適化表單、主題、範本或雲端設定）的作業只會透過「作者」節點執行，而可在設定的「發佈」節點發佈。
如需詳細資訊，請參閱 [發佈和取消發佈表單和檔案](https://experienceleague.adobe.com/docs/experience-manager-65/forms/publish-process-aem-forms/publishing-unpublishing-forms.html?lang=en)
* 製作和發佈都需要Forms addon套件，才能支援檔案服務操作；因此，可視為相依性。
如果您只需要Forms相關範本、主題和DOR套件，則可從下載 [aemforms-references-*套件](https://experienceleague.adobe.com/docs/experience-manager-65/forms/publish-process-aem-forms/publishing-unpublishing-forms.html?lang=en).

如需詳細資訊，請參閱 [製作最適化表單簡介](/help/forms/using/introduction-forms-authoring.md).

## 製作最適化表單 {#author-adaptive-forms}

### 使用觸控最佳化UI進行製作 {#using-touch-optimized-ui-for-authoring}

* 在側欄中使用對象瀏覽器快速訪問表單層次結構中深層的欄位。 可以使用搜索框搜索窗體或對象樹中的對象，以從一個對象導航到另一個對象。
* 要在側欄的元件瀏覽器中查看和編輯元件的屬性，請選擇該元件並按一下 ![cmpr-1](assets/cmppr-1.png). 您也可以連按兩下元件，在屬性瀏覽器中檢視其屬性。
* 使用鍵盤快速鍵對表單執行快速動作。 請參閱 [AEM Forms鍵盤快速鍵](/help/forms/using/keyboard-shortcuts.md).

* 建議僅在最適化表單頁面中使用最適化表單元件。 元件依賴其父級階層。 因此，請勿在AEM頁面中使用。

另請參閱下列主題中的元件說明和最佳實務： [製作最適化表單簡介](/help/forms/using/introduction-forms-authoring.md).

### 在適用性表單中使用規則 {#using-rules-in-adaptive-forms}

AEM Forms提供 [規則編輯器](/help/forms/using/rule-editor.md) 可讓您建立規則，將動態行為新增至最適化表單元件。 使用這些規則，您可以評估條件並觸發元件上的動作，例如顯示或隱藏欄位、計算值、動態變更下拉式清單等。

規則編輯器提供用於編寫規則的可視化編輯器和代碼編輯器。 使用程式碼編輯器模式撰寫規則時，請考量下列事項：

* 對表單欄位和元件使用有意義的唯一名稱，以避免在編寫規則時產生任何可能的衝突。
* 使用 `this` 運算子，以在規則運算式中引用元件本身。 這可確保即使元件名稱變更，規則仍有效。 例如, `field1.valueCommit script: this.value > 10`.

* 參考其他表單元件時，請使用元件名稱。 使用 `value` 屬性，以擷取欄位或元件的值。 例如, `field1.value`.

* 依相對唯一階層來參照元件，以避免任何衝突。 例如, `parentName.fieldName`.

* 處理複雜或常用的規則時，請考慮將業務邏輯撰寫為個別用戶端程式庫中的函式，以便在最適化表單中指定和重複使用。 用戶端程式庫應為獨立的程式庫，且除jQuery和Underscore.js外，不應有任何外部相依性。 您也可以使用用戶端程式庫來強制執行 [伺服器端重新驗證](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form) 已提交的表單資料。
* 適用性表單提供一組API，可用來與最適化表單通訊及執行動作。 部分關鍵API如下。 如需詳細資訊，請參閱 [適用性Forms的JavaScript程式庫API參考](https://adobe.com/go/learn_aemforms_documentation_63).

   * `guideBridge.reset()`:重設表單。
   * `guideBridge.submit()`:提交表單。
   * `guideBridge.setFocus(somExp, focusOption, runCompletionExp)`:將焦點設定為欄位。
   * `guideBridge.validate(errorList, somExpression, focus)`:驗證表單。
   * `guideBridge.getDataXML(options)`:以XML形式獲取表單資料。
   * `guideBridge.resolveNode(somExpression)`:獲取表單對象。
   * `guideBridge.setProperty(somList, propertyName, valueList)`:設定表單對象的屬性。
   * 此外，您還可以使用下列欄位屬性：

      * `field.value` 來更改欄位的值。
      * `field.enabled` 啟用/停用欄位。
      * `field.visible` 更改欄位的可見性。

* 最適化表單作者可能需要編寫JavaScript程式碼，才能在表單中建立業務邏輯。 雖然JavaScript功能強大且有效，但可能會在安全性預期上有所妥協。 因此，您必須確保表單作者是值得信賴的人員，且在表單投入生產前，有需要檢閱和核准JavaScript程式碼的程式。 管理員可以根據使用者的角色或功能，限制對規則編輯器存取權限給使用者群組。 請參閱 [授予規則編輯器對選定用戶組的訪問權限](/help/forms/using/rule-editor-access-user-groups.md).
* 您可以在規則中使用運算式，讓最適化表單動態。 所有運算式都是有效的JavaScript運算式，且會使用最適化表單指令碼模型API。 這些運算式會傳回特定類型的值。 如需關於運算式和相關最佳實務的詳細資訊，請參閱 [適用性表單運算式](/help/forms/using/adaptive-form-expressions.md).

### 處理主題 {#working-with-themes}

主題適用性可讓您建立可重複使用的樣式，可套用至不同表單，以提供一致的外觀和樣式。 建議您使用主題來定義表單元件和面板的樣式。 有關主題的一些最佳做法如下：

* 使用資產資料庫來快速應用文字樣式、背景和影像。 在資產資料庫中新增樣式時，其他主題和表單編輯器的樣式模式中都可使用樣式。
* 使用頁面層級選取器套用全域設定，例如字型和頁面背景。
* 使用用戶端程式庫將現有或進階樣式匯入主題。
* 您可以在表單樣式層中覆寫特定欄位、面板或按鈕的樣式。
* 如果主題不符合樣式要求，則可以使用預定義的類，如guideFieldNode、guideFieldLabel、guideFieldWidget和guidePanelNode，以在各表單間應用公共樣式。

如需詳細資訊，請參閱 [主題](/help/forms/using/themes.md).

### 優化大型複雜表單的效能 {#optimizing-performance-of-large-and-complex-forms}

表單作者和使用者在製作模式或執行階段載入大型表單時，通常會遇到效能問題。 隨著表單中的物件（欄位和面板）數量增加，製作和執行階段體驗會開始降格。 這也防止了多位作者同時協作和製作表單。

請考慮下列最佳實務，以克服大型表單的效能問題：

* 建議您使用XSD表單資料模型建立最適化表單，即使可能的話，將XFA轉換為最適化表單亦然。
* 僅包含適用性表單中擷取使用者資訊的欄位和面板。 請考慮將靜態內容保持在最小，或使用URL在個別視窗中開啟靜態內容。
* 雖然每個表單都是專為特定用途而設計，但大部分表單中都有一些常見的區段。 例如，個人詳細資訊、地址、雇傭詳細資訊等。 建立 [適用性表單片段](/help/forms/using/adaptive-form-fragments.md) 用於常見的表單元素和區段，並跨表單使用。 您也可以將現有表單中的面板儲存為片段。 片段中的任何變更都會反映在所有相關聯的最適化表單中。 由於多位作者可同時處理組成表單的不同片段，因此可促進協作製作。

   * 與適用性表單類似，建議使用片段容器對話方塊在用戶端程式庫中定義所有片段專用樣式和自訂指令碼。 此外，請嘗試建立不依賴外部物件的自給自足片段。
   * 避免使用跨片段指令碼。 如果片段外部有您必須參照的任何物件，請嘗試將該物件設為上層表單的一部分。 如果物件仍必須位於另一個片段中，請在指令碼中依其名稱參考它。

* 使用「儲存並繼續並自動儲存」定期儲存最適化表單，讓使用者稍後重新造訪以完成表單。
* 設定片段以懶惰載入。 在執行階段，標示為懶散載入的片段只有在需要時才會轉譯。 可大幅縮短大型表單的載入時間。 可重複面板的片段也支援此功能。 如需詳細資訊，請參閱 [設定延遲載入](/help/forms/using/lazy-loading-adaptive-forms.md).

   * 請勿在回應式格線版面或第一個面板中，針對片段設定延遲載入。
   * 懶惰載入片段不支援檔案附件和條款與條件元件。
   * 如果在窗體的其它部分中使用該值，則將延遲載入面板中的值標籤為「全局使用值」(Use Value Globally)，以便在卸載容納面板時該值可用。
   * 請考慮針對應根據條件顯示或隱藏的片段撰寫可見性規則。
* 設定 **每個請求的呼叫數** 在 **Apache Sling主要Servlet** 數量相當大。 它可讓Forms伺服器允許其他呼叫。 設定會顯示預設值1500。 值（1500個呼叫）是用於其他Experience Manager元件，例如Sites和Assets。 適用性表單的預設值集為20000。 如果您遇到 `too many calls` 記錄檔中發生錯誤，或表單無法轉譯，請嘗試將值增加到大數以解決問題。 如果呼叫數超過20000，表示表單複雜，可能需要一些時間在瀏覽器中轉譯表單。 這只會在首次載入表單時、快取表單後，以及快取表單後，發生此情況對效能沒有重大影響。

### 預填最適化表單 {#prefilling-adaptive-forms}

您可以使用從後端擷取的資料預先填入最適化表單欄位，協助使用者快速填入表單，避免輸入錯誤。

* AEM Forms提供預填服務，可從預先定義的資料XML檔案讀取資料，並以預填XML檔案中的內容預填最適化表單的欄位。
* 預填資料XML必須與與最適化表單相關聯的表單模型的架構相容。
* 包括 `afBoundedData` 和 `afUnBoundedData` 預填XML中的區段，以在適用性表單中預填綁定和未綁定欄位。

* 針對以表單資料模型為基礎的最適化表單，AEM Forms提供現成可用的表單資料模型預填服務。 預填服務會查詢適用性表單中資料模型物件的資料來源，並在轉譯表單時預填欄位值。
* 您也可以使用檔案、crx、服務或http通訊協定來預填最適化表單。
* AEM Forms支援自訂預填服務，您可以將這些服務外掛為OSGi服務，以預填最適化表單。

如需詳細資訊，請參閱 [預填最適化表單欄位](/help/forms/using/prepopulate-adaptive-form-fields.md).

### 簽署和提交最適化表單 {#signing-and-submitting-adaptive-forms}

適用性表單需要提交動作，才能處理使用者指定的資料。 「提交」動作會決定您使用最適化表單提交之資料所執行的任務。

* 適用性表單中有數個可立即使用的提交動作。 如需詳細資訊，請參閱 [設定提交動作](/help/forms/using/configuring-submit-actions.md).
* 如果預設提交操作不符合您的使用案例，則可以編寫自定義提交操作。 如需詳細資訊，請參閱 [撰寫最適化表單的自訂提交動作](/help/forms/using/custom-submit-action-form.md).
* 納入伺服器端驗證，以防止提交無效的資料。

您可以在適用性表單中運用Adobe Sign的多重簽署體驗。 在適用性表單中設定Adobe Sign時，請考量下列事項。 如需詳細資訊，請參閱 [在最適化表單中使用Adobe Sign](/help/forms/using/working-with-adobe-sign.md).

* Adobe Sign啟用的適用性表單必須在所有簽署者簽署表單後才提交。 Forms會以「擱置中籤署」狀態顯示，直到所有簽署者簽署表單為止。
* 您可以設定表單內簽署體驗，或在提交時將簽署者重新導向至簽署頁面。
* 視需要設定循序或平行簽署體驗。

### 生成記錄文檔 {#generating-document-of-record}

記錄檔案(DoR)是可打印、簽名或歸檔的最適化表單的平面化PDF版本。

* 根據最適化表單所依據的表單資料模型，您可以依照下列方式設定DoR的範本：

   * **XFA表單範本**:使用關聯的XDP檔案作為DoR模板。
   * **XSD架構**:使用與適用性表單所使用相同XML架構的相關聯XFA範本。
   * **無**:使用自動生成的DoR。

* 從最適化表單編輯器的「記錄檔案」索引標籤，以右側設定頁首、頁尾、影像、顏色、字型等。
* 使用 `DoRService` 以寫程式方式生成DoR。
* 從DoR中排除隱藏欄位。
* 使用 `afAcceptLang` 請求參數，以查看其他地區設定中的DoR。

### 偵錯和測試最適化表單 {#debugging-and-testing-adaptive-forms}

[AEM Chrome外掛程式](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/) 是Google Chrome的瀏覽器擴充功能，提供調試最適化表單的工具。 表單作者和開發人員可使用這些工具：

* 找出表單呈現的瓶頸並優化效能
* 對表單中的關鍵字和bindRef錯誤進行調試
* 啟用和配置日誌
* 表單中的除錯規則和指令碼
* 探索及了解guideBridge API

如需詳細資訊，請參閱 [AEM Chrome外掛程式 — 適用性表單](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/adaptive-form/).

### 驗證AEM伺服器上的適用性表單 {#validating-adaptive-forms-on-aem-server}

需要伺服器端驗證，以防止任何嘗試略過客戶端上的驗證，以及資料提交和業務規則違規的任何可能危害。 伺服器端驗證會透過載入所需的用戶端程式庫，在伺服器上執行。

* 在用戶端程式庫中加入函式，以驗證適用性表單中的運算式，並在適用性表單容器對話方塊中指定用戶端程式庫。 如需詳細資訊，請參閱 [伺服器端重新驗證](/help/forms/using/configuring-submit-actions.md#p-server-side-revalidation-in-adaptive-form-p).
* 伺服器端驗證會驗證表單模型。 建議您建立個別的用戶端程式庫以進行驗證，但不要在相同的用戶端程式庫中與其他項目(例如HTML樣式和DOM操作)混合使用。

### 將最適化表單當地語系化 {#localizing-adaptive-forms}

AEM提供翻譯工作流程，供您將最適化表單當地化。 如需詳細資訊，請參閱 [使用AEM翻譯工作流程將最適化表單當地化](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md).

將最適化表單當地語系化時的一些最佳實務如下：

* 跨表單使用最適化表單片段以處理常見元素，並將片段當地化。 它可確保片段本地化一次，而且會在使用本地化片段的所有表單中反映。
* 任何修改（例如新增元件或以本地化形式套用指令碼）都不會自動本地化。 因此，您必須在將表單本地化之前完成表單的翻譯，以避免多個本地化週期。
* 使用 `afAcceptLang` 請求參數，以覆蓋瀏覽器地區並在指定地區中呈現表單。 例如，下列URL將強制以日文地區來呈現表單，而不考慮瀏覽器設定中指定的地區：

   `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

* AEM Forms目前支援以英文(en)、西班牙文(es)、法文(fr)、義大利文(it)、德文(de)、日文(ja)、葡萄牙文 — 巴西(pt-BR)、中文(zh-CN)、中文 — 台灣(zh-TW)和韓文(ko-KR)語言環境本地化最適化表單內容。 不過，您可以在執行階段新增對適用性表單新區域設定的支援。 如需詳細資訊，請參閱 [支援最適化表單本地化的新地區設定](/help/forms/using/supporting-new-language-localization.md).

## 準備生產用表單專案 {#prepare-forms-project-for-production}

### 添加表單處理伺服器 {#adding-forms-processing-server}

您可以設定位於安全區域防火牆後方的AEM Forms伺服器其他例項。 您可以將此例項用於：

* **批次處理**:批次重複或排程、負載沈重的作業。 例如，打印語句、生成對應，以及使用文檔服務(如PDF生成器、輸出和組合器)。
* **儲存PII資料**:將PII資料儲存至處理伺服器。 如果您已使用自訂儲存提供者來儲存PII資料，則不需要此功能。

### 將專案移至其他環境 {#moving-project-to-another-environment}

您經常需要將AEM專案從一個環境移至另一個環境。 移動時需記住的部分重要事項如下：

* 備份現有的客戶端庫、自定義代碼和配置。
* 在新環境中按指定順序手動部署產品包和修補程式。
* 手動部署專屬於專案的程式碼套件和套件組合，並在新AEM伺服器上以個別套件或套件組合的形式部署。
* (*AEM Forms on JEE*)在Forms Workflow伺服器上手動部署LCA和DSC。
* 使用 [匯出 — 匯入](/help/forms/using/import-export-forms-templates.md) 功能將資產移至新環境。 您也可以設定復寫代理並發佈資產。
* 升級後，請以新的API和功能取代所有已棄用的API和功能。

### 設定AEM {#configuring-aem}

設定AEM以改善整體效能的一些最佳實務如下：

* 從Felix Console為JavaScript和CSS啟用HTML用戶端程式庫壓縮。
* 快取位於 `/etc.clientlibs/fd` 和AEM dispatcher上的任何其他自訂用戶端程式庫，以提高已發佈表單的回應速度與安全性。 如需詳細資訊，請參閱 [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html).

* 不快取 `/content/forms/af/` 和 `/content/dam/formsanddocuments/*` 路徑。 如需設定最適化表單快取的詳細資訊，請參閱 [快取最適化表單](/help/forms/using/configure-adaptive-forms-cache.md).

* 透過Web伺服器壓縮模組啟用HTML。 如需詳細資訊，請參閱 [AEM Forms伺服器效能調整](/help/forms/using/performance-tuning-aem-forms.md).
* 針對大型表單增加每個請求設定的呼叫。 請參閱 [優化大型複雜表單的效能](/help/forms/using/adaptive-forms-best-practices.md#optimizing-performance-of-large-and-complex-forms).
* 建立 [錯誤處理程式顯示的自定義錯誤頁](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/customizing-errorhandler-pages.html).
* 安全的AEM Forms伺服器。

   * 使用 `nosamplecontent` 執行模式，以確保生產伺服器上未部署範例內容和範例使用者。 請參閱 [以生產就緒模式執行AEM](/help/sites-administering/production-ready.md).

* 將堆大小保持在8 GB以下。 如需其他設定，請參閱 [AEM Forms伺服器效能調整](/help/forms/using/performance-tuning-aem-forms.md).
* 使用服務用戶會話而不是管理會話來執行服務級別任務。 如需詳細資訊，請參閱 [服務驗證](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html).

>[!VIDEO](https://vimeo.com/)

### 為草稿和已提交的表單資料配置外部儲存 {#external-storage}

在生產環境中，建議不要將已提交的表單資料儲存在AEM存放庫中。 Forms Portal Store、Store內容和StorePDF的預設實作會將表單資料儲存在AEM存放庫中。 這些提交動作的用途僅止於示範。 此外，「儲存並繼續」和「自動儲存」功能預設會使用入口儲存。 因此，請考慮以下建議：

* **儲存草稿資料**:如果您使用適用性表單的草稿功能，應實作自訂服務提供介面(SPI)，將草稿資料儲存在資料庫之類的更安全儲存體中。 如需詳細資訊，請參閱 [將草稿和提交元件與資料庫整合的範例](/help/forms/using/integrate-draft-submission-database.md).

* **儲存提交資料**:如果您使用表單入口網站提交存放區，應實作自訂SPI，將提交資料儲存在資料庫中。 請參閱 [將草稿和提交元件與資料庫整合的範例](/help/forms/using/integrate-draft-submission-database.md) 以取得範例整合。

   您也可以撰寫自訂提交動作，將表單資料和附件儲存在安全的儲存空間中。 請參閱 [撰寫最適化表單的自訂提交動作](/help/forms/using/custom-submit-action-form.md) 以取得更多資訊。

* **草稿ID的長度**:將最適化表單儲存為草稿時，系統會產生草稿ID來唯一識別草稿。 草稿ID欄位長度的最小值為26個字元。 Adobe建議將草稿ID長度設為26個或更多字元。

### 處理個人識別資訊 {#handling-personally-identifiable-information}

組織面臨的主要挑戰之一，是如何處理個人識別(PII)資料。 以下是可協助您處理這些資料的最佳實務：

* 使用安全的外部儲存，如資料庫，儲存草稿和提交表單的資料。 請參閱 [為草稿和已提交的表單資料配置外部儲存](/help/forms/using/adaptive-forms-best-practices.md#external-storage).
* 啟用自動儲存前，請使用「條款與條件」表單元件取得使用者的明確同意。 在此情況下，僅當用戶同意「條款」和「條件」元件中的條件時，啟用自動保存。


