---
title: 使用最適化表單的最佳範例
seo-title: 使用最適化表單的最佳範例
description: 說明設定AEM Forms專案、開發最適化表單以及最佳化AEM Forms系統效能的最佳實務。
seo-description: 說明設定AEM Forms專案、開發最適化表單以及最佳化AEM Forms系統效能的最佳實務。
uuid: ed95fc64-56b3-4ea1-a5ba-2e96953fca56
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 43c431e4-5286-4f4e-b94f-5a7451c4a22c
translation-type: tm+mt
source-git-commit: 6bd09bca68ea1fcec2dca7694dd3d39dc5153bfc

---


# 使用最適化表單的最佳範例 {#best-practices-for-working-with-adaptive-forms}

## 概覽 {#overview}

Adobe Experience Manager(AEM)表單可協助您將複雜的交易轉換為簡單、愉悅的數位體驗。 但是，它需要共同努力來建置、建立、執行和維護有效率且具生產力的AEM Forms生態系統。

本檔案提供管理員、作者和開發人員在使用AEM Forms時可從中獲益的准則和建議，尤其是最適化表單元件。 它討論從設定表單開發專案到設定、自訂、製作和最佳化AEM Forms的最佳實務。 這些最佳實務可共同協助AEM Forms生態系統的整體效能。

此外，以下是一般AEM最佳實務的建議讀取：

* [最佳實務：部署和維護AEM](/help/sites-deploying/best-practices.md)
* [最佳實務：製作內容](/help/sites-authoring/best-practices.md)
* [最佳實務：管理AEM](/help/sites-administering/administer-best-practices.md)
* [最佳實務：開發解決方案](/help/sites-developing/best-practices.md)

## 設定和設定AEM Forms {#set-up-and-configure-aem-forms}

### 設定表單開發專案 {#setting-up-forms-development-project}

簡化和標準化的專案結構可大幅降低開發和維護工作。 Apache Maven是建立AEM專案時建議使用的開放原始碼工具。

* 使用Apache Maven `aem-project-archetype` 建立並管理AEM專案的結構。 它會為您的AEM專案建立建議的結構和範本。 此外，它還提供建置自動化和變更控制系統，以協助管理專案。

   * 使用maven命 `archetype:generate` 令生成初始結構。
   * 使用maven `eclipse:eclipse` 命令產生eclipse專案檔案，並將專案匯入eclipse。

如需詳細資訊，請 [參閱「如何使用Apache Maven建立AEM專案」](/help/sites-developing/ht-projects-maven.md)。

* FileVault工具或VLT可協助您將CRX或AEM例項的內容對應至您的檔案系統。 它提供變更控制管理作業，例如登入和登出AEM專案內容。 請參 [閱如何使用VLT工具](/help/sites-developing/ht-vlttool.md)。

* 如果您使用Eclipse整合的開發環境，您可以使用AEM Developer工具，將Eclipse IDE與AEM例項完美整合，以建立AEM應用程式。 如需詳細資訊，請 [參閱Eclipse的AEM開發人員工具](/help/sites-developing/aem-eclipse.md)。

### 規劃製作環境 {#planning-for-authoring-environment}

在您設定AEM專案後，請定義編寫和自訂最適化表單範本和元件的策略。

* 最適化表單範本是專用的AEM頁面，可定義最適化表單的結構和頁首——頁尾資訊。 範本具有預先設定的版面配置、樣式和最適化表單的基本結構。 AEM Forms提供現成可用的範本和元件，讓您用來製作最適化表單。 不過，您可以根據需求建立自訂範本和元件。 建議您收集在最適化表單中需要的其他範本和元件需求。 如需詳細資訊，請參 [閱自訂最適化表單和元件](/help/forms/using/adaptive-forms-best-practices.md#customize-components)。
* AEM Forms可讓您根據下清單單模型建立最適化表單。 表單模型充當表單與AEM系統之間資料交換的介面，並為最適化表單內外的資料流提供XML架構。 另外，表單模型以模式和XFA約束的形式對自適應表單施加規則和約束。

   * **無**:使用此選項建立的最適化表單不會使用任何表單模型。 從這種表單中生成的資料XML具有平坦的結構，具有欄位和相應的值。
   * **XML或JSON結構描述**:XML和JSON結構描述資料由組織中的後端系統產生或使用的結構。 您可以將架構與最適化表單建立關聯，並使用其元素將動態內容新增至最適化表單。 架構的元素可在內容瀏覽器的「資料模型物件」索引標籤中使用，以製作最適化表單。 您可以拖放架構元素來建立表單。
   * **XFA表單範本**:如果您投資於以XFA為基礎的HTML5表單，這是理想的表單模型。 它提供將XFA型表單轉換為最適化表單的直接方式。 任何現有的XFA規則都會保留在相關的最適化表單中。 產生的最適化表單支援XFA結構，例如驗證、事件、屬性和模式。
   * **表單資料模型**:如果您想要整合後端系統（例如資料庫、網站服務和AEM使用者設定檔），以預先填寫最適化表單，並將提交的表單資料寫回後端系統，則此為偏好的表單模型。 表單資料模型編輯器可讓您定義並設定表單資料模型中的實體和服務，以便用來建立最適化表單。 如需詳細資訊，請參 [閱「AEM Forms資料整合」](/help/forms/using/data-integration.md)。

請務必謹慎選擇不僅符合您需求的資料模型，而且延伸您對XFA和XSD資產的現有投資（如果有的話）。 建議使用XSD模型來建立表單範本，因為產生的XML會依照架構定義的XPATH包含資料。 使用XSD模型作為表單資料模型的預設選擇，也有助於將表單設計與處理和使用資料的後端系統解耦，而且由於表單欄位的一對一對應，因此可改善表單的效能。 此外，欄位的BindRef也可以使其資料值在XML中的XPATH。

如需詳細資訊，請參 [閱建立最適化表單](/help/forms/using/creating-adaptive-form.md)。

* 在最適化表單中，有一些常見的章節。 您可以識別它們，並定義策略以促進內容重複使用。 最適化表單可讓您建立獨立的片段，並跨表單重複使用這些片段。 您也可以將最適化格式的面板儲存為片段。 片段中的任何變更都會反映在所有相關的表單中。 它可協助您縮短製作時間，並確保各表單的一致性。 此外，片段的使用讓可調式表單變得精簡，進而改善製作體驗，尤其是大型表單。 如需詳細資訊，請參 [閱最適化表單片段](/help/forms/using/adaptive-form-fragments.md)。

### 自訂最適化表單和元件 {#customize-components}

* AEM Forms提供現成可用的最適化表單範本，供您用來建立最適化表單。 您也可以建立自己的範本。 AEM提供靜態和可編輯的範本。

   * 靜態範本由開發人員定義和設定。
   * 可編輯的範本由作者使用範本編輯器建立。 範本編輯器可讓您定義範本中的基本結構和初始內容。 結構層中的任何修改都會反映在使用該模板的所有表單中。 初始內容可包括預先配置的主題、預填充服務、提交動作等。 不過，這些設定可使用表單編輯器來修改表單。 如需詳細資訊，請參 [閱最適化表單範本](/help/forms/using/template-editor.md)。

* 如要設定特定欄位或面板例項的樣式，請使用 [內嵌樣式](/help/forms/using/inline-style-adaptive-forms.md)。 或者，您可以在CSS檔案中定義類別，並在元件的「CSS類別」屬性中指定類別名稱。
* 在元件中加入用戶端程式庫，以一致地套用使用該元件之最適化表單或片段的樣式。 如需詳細資訊，請參 [閱建立最適化表單頁面元件](/help/forms/using/custom-adaptive-forms-templates.md)。
* 在最適化表單容器屬性的CSS檔案路徑欄位中，指定用戶端資料庫的路徑，以套用用戶端資料庫中定義的樣式來選取最適化表單。
* 若要建立樣式的用戶端資料庫，您可以在「主題編輯器」基本的clientlib或「表單容器」屬性中設定自訂CSS檔案。
* 最適化表單提供面板版面配置，例如互動式、標籤式、收合式和精靈，以控制表單元件在面板中的排版方式。 您可以建立自訂面板版面，並讓表單作者使用。 如需詳細資訊，請參 [閱建立最適化表單的自訂版面元件](/help/forms/using/custom-layout-components-forms.md)。
* 您也可以自訂特定的最適化表單元件，例如欄位和面板版面。

   * 使用 [AEM的](/help/sites-developing/overlays.md) 「覆蓋」功能來修改元件的復本。 不建議修改預設元件。
   * 若要自訂/libs中現成可用的最適化表單元件的版面，除了預 [設版面外](/help/forms/using/custom-layout-components-forms.md) ，還可建立自 [訂版面元件](/help/forms/using/layout-capabilities-adaptive-forms.md)。
   * 建立自訂介面工具集或外觀，以引入自訂互動活動。 不建議修改預設元件。 如需詳細資訊，請參 [閱Appearance framework](/help/forms/using/introduction-widgets.md)。

* 如需 [有關處理PII資料的建議](/help/forms/using/adaptive-forms-best-practices.md#p-handling-personally-identifiable-information-p) ，請參閱處理個人識別資訊。

## 製作最適化表單 {#author-adaptive-forms}

### 使用觸控最佳化的UI製作 {#using-touch-optimized-ui-for-authoring}

* 使用側欄中的「物件」瀏覽器，快速存取表單階層中深層的欄位。 您可以使用搜索框在表單或對象樹中搜索對象，以便從一個對象導航到另一個對象。
* 若要在側欄的元件瀏覽器中檢視並編輯元件的屬性，請選取元件，然後按一 ![下cmppr-1](assets/cmppr-1.png)。 您也可以按兩下元件，在屬性瀏覽器中檢視其屬性。
* 使用鍵盤快速鍵，在表單上快速動作。 請參閱 [AEM Forms鍵盤快速鍵](/help/forms/using/keyboard-shortcuts.md)。

* 建議只在最適化表單頁面中使用最適化表單元件。 這些元件對其父級層次具有依賴性。 因此，請勿在AEM頁面中使用它們。

此外，請參閱製作最適化表單簡介 [中的元件說明和最佳實務](/help/forms/using/introduction-forms-authoring.md)。

### 在最適化表單中使用規則 {#using-rules-in-adaptive-forms}

AEM Forms提供規 [則編輯器](/help/forms/using/rule-editor.md) ，可讓您建立規則，將動態行為新增至最適化表單元件。 使用這些規則，您可以評估條件並觸發元件上的動作，例如顯示或隱藏欄位、計算值、動態變更下拉式清單等。

規則編輯器提供可視編輯器和代碼編輯器，用於編寫規則。 使用程式碼編輯器模式編寫規則時，請考慮下列事項：

* 在撰寫規則時，為表單欄位和元件使用有意義且唯一的名稱，以避免任何可能的衝突。
* 使用 `this` 元件的運算子，在規則運算式中引用元件本身。 它可確保即使元件名稱變更，規則仍然有效。 例如， `field1.valueCommit script: this.value > 10`。

* 參照其他表單元件時，請使用元件名稱。 使用 `value` 屬性來擷取欄位或元件的值。 例如， `field1.value`。

* 依相對唯一階層來參考元件，以避免任何衝突。 例如， `parentName.fieldName`。

* 在處理複雜或常用的規則時，請考慮將商業邏輯編寫為個別用戶端程式庫中的函式，以便您指定並跨調適性表單重複使用。 用戶端程式庫應是獨立的程式庫，除jQuery和Undershore.js外，不應有任何外部相依性。 您也可以使用用戶端程式庫來強制 [伺服器端重新驗證已提交的表](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form) 單資料。
* 最適化表單提供一組API，您可用來與最適化表單通訊，並對其執行動作。 部分關鍵API如下。 如需詳細資訊，請參 [閱適用於Adaptive Forms的JavaScript程式庫API參考](https://adobe.com/go/learn_aemforms_documentation_63)。

   * `guideBridge.reset()`:重設表單。
   * `guideBridge.submit()`:提交表格。
   * `guideBridge.setFocus(somExp, focusOption, runCompletionExp)`:將焦點設定為欄位。
   * `guideBridge.validate(errorList, somExpression, focus)`:驗證表單。
   * `guideBridge.getDataXML(options)`:以XML格式取得表單資料。
   * `guideBridge.resolveNode(somExpression)`:獲取表單對象。
   * `guideBridge.setProperty(somList, propertyName, valueList)`:設定表單對象的屬性。
   * 此外，您還可使用下列欄位屬性：

      * `field.value` 來更改欄位的值。
      * f `ield.enabled` 啟用／停用欄位。
      * `field.visible` 變更欄位的可見度。

* 最適化表單作者可能需要編寫JavaScript程式碼，才能建立表單中的商業邏輯。 雖然JavaScript功能強大而且有效，但可能會在安全性預期上造成損害。 因此，您必須確保表單作者是受信任的人物，而且在表單投入生產之前，有需要檢閱和核准JavaScript程式碼的程式。 管理員可以根據用戶組的角色或功能限制對規則編輯器的訪問權限。 請參 [閱授予規則編輯器對選定用戶組的訪問權限](/help/forms/using/rule-editor-access-user-groups.md)。
* 您可以在規則中使用運算式，讓最適化表單變為動態。 所有運算式都是有效的JavaScript運算式，並使用最適化表單指令碼模型API。 這些運算式會傳回特定類型的值。 如需其相關運算式和最佳實務的詳細資訊，請參 [閱最適化表單運算式](/help/forms/using/adaptive-form-expressions.md)。

### 使用主題 {#working-with-themes}

主題最適化可讓您建立可重複使用的樣式，可套用至各種表單，以提供一致的外觀和樣式。 建議使用「主題」來定義表單元件和面板的樣式。 主題的一些最佳做法如下：

* 使用資產庫，快速套用文字樣式、背景和影像。 在資產庫中新增樣式時，其他主題和表格編輯器的樣式模式都可使用。
* 使用頁面層級選擇器套用全域設定，例如字型和頁面背景。
* 使用用戶端程式庫，將現有或進階樣式匯入主題。
* 您可以在表單樣式圖層中覆寫特定欄位、面板或按鈕的樣式。
* 如果主題不符合樣式要求，您可以使用預先定義的類，如guideFieldNode、guideFieldLabel、guideFieldWidget和guidePanelNode，跨表單應用通用樣式。

如需詳細資訊，請參 [閱主題](/help/forms/using/themes.md)。

### 最佳化大型和複雜表單的效能 {#optimizing-performance-of-large-and-complex-forms}

表單製作者和使用者通常在以編寫模式或執行時期載入大型表單時，會遇到效能問題。 隨著表單中物件（欄位和面板）數目增加，製作與執行時期的體驗開始降低。 此外，它還可防止多位作者同時協作和製作表單。

請考慮下列最佳實務，以克服大型表單的效能問題：

* 建議使用XSD表單資料模型建立最適化表單，即使將XFA轉換為最適化表單（如果可能）亦然。
* 在可從使用者擷取資訊的最適化表單中，僅包含這些欄位和面板。 請考慮將靜態內容保持在最小，或使用URL在個別視窗中開啟。
* 雖然每個表格都是專為特定用途而設計，但大部分表格中都有一些常見的區段。 例如，個人詳細資料、地址、雇傭詳細資料等。 建立 [通用表單元素](/help/forms/using/adaptive-form-fragments.md) 和章節的最適化表單片段，並跨表單使用。 您也可以將現有表單中的面板儲存為片段。 片段中的任何變更都會反映在所有相關的最適化表單中。 它可促進協作製作，因為多位作者可同時處理組成表單的不同片段。

   * 與最適化表單類似，建議使用片段容器對話方塊在用戶端程式庫中定義所有片段特定樣式和自訂指令碼。 此外，請嘗試建立不依賴外部物件的自給自足片段。
   * 避免使用跨片段指令碼。 如果片段外有您必須參照的任何物件，請嘗試將該物件設為父表單的一部分。 如果對象仍必須駐留在另一個片段中，請在指令碼中按其名稱引用該對象。

* 使用「儲存並繼續」與自動儲存功能，定期儲存最適化表單，讓使用者稍後可重新造訪以完成表單。
* 設定片段以延遲載入。 在執行時期，標籤為緩慢載入的片段只會在需要時顯示。 它可大幅降低大型表單的載入時間。 可重複面板的片段也支援它。 如需詳細資訊，請參 [閱設定延遲載入](/help/forms/using/lazy-loading-adaptive-forms.md)。

   * 請勿在回應式格點版面或第一個面板中設定片段的延遲載入。
   * 懶惰載入的片段不支援檔案附件和條款與條件元件。
   * 如果該值用於表單的其他部分，以便在卸載包含面板時使用該值，則將延遲載入面板中的值標籤為「全局使用值」。
   * 考慮針對應根據條件顯示或隱藏的片段編寫可見性規則。

### 預先填寫最適化表單 {#prefilling-adaptive-forms}

您可以預先填入從後端擷取的資料，以協助使用者快速填入表格並避免輸入錯誤。

* AEM Forms提供預先填寫服務，可從預先定義的資料XML檔案讀取資料，並以預先填寫的XML檔案中的內容預先填寫最適化表單的欄位。
* 預填充資料XML必須與與自適應表單相關聯的表單模型的模式相容。
* 在預 `afBoundedData` 先填 `afUnBoundedData` 寫XML中加入區段，以在最適化表單中預先填寫系結和未系結的欄位。

* 針對以表單資料模型為基礎的最適化表單，AEM Forms提供現成可用的表單資料模型預填服務。 預填充服務在自適應表單中查詢資料模型對象的資料源，並在呈現表單時預填充欄位值。
* 您也可以使用檔案、crx、服務或http通訊協定，預先填寫最適化表單。
* AEM Forms支援自訂的預填服務，您可將這些服務外掛為OSGi服務，以預填最適化表單。

如需詳細資訊，請參閱「預 [先填寫最適化表單欄位」](/help/forms/using/prepopulate-adaptive-form-fields.md)。

### 簽署和送出最適化表單 {#signing-and-submitting-adaptive-forms}

最適化表單需要「提交」動作來處理使用者指定的資料。 「提交」操作決定使用自適應表單對提交的資料執行的任務。

* 在最適化表單中，有數種現成可用的提交動作。 如需詳細資訊，請 [參閱設定提交動作](/help/forms/using/configuring-submit-actions.md)。
* 如果預設提交操作不符合您的使用案例，您可以編寫自定義提交操作。 如需詳細資訊，請參 [閱撰寫最適化表單的自訂提交動作](/help/forms/using/custom-submit-action-form.md)。
* 包含伺服器端驗證，以防止提交無效的資料。

您可以在最適化表單中運用Adobe Sign的多重簽署體驗。 在最適化表單中設定Adobe Sign時，請考慮下列事項。 如需詳細資訊，請 [參閱「在最適化表單中使用Adobe Sign](/help/forms/using/working-with-adobe-sign.md)」。

* 啟用Adobe Sign的最適化表單必須在所有簽署者簽署表單後才能送出。 表單會以「待簽署」狀態顯示，直到所有簽署者簽署表單為止。
* 您可以設定表單內簽署體驗，或在提交時將簽署者重新導向至簽署頁面。
* 視需要設定循序或平行的簽署體驗。

### 產生記錄檔案 {#generating-document-of-record}

記錄檔案(DoR)是可列印、簽署或封存之最適化表單的平面化PDF版本。

* 根據自適應表單所基於的表單資料模型，可以按如下方式為DoR配置模板：

   * **XFA表單範本**:使用關聯的XDP檔案作為DoR模板。
   * **XSD架構**:使用與最適化表單使用相同XML架構的相關XFA範本。
   * **無**:使用自動產生的DoR。

* 直接從最適化表單編輯器的「記錄檔案」索引標籤，設定頁首、頁尾、影像、顏色、字型等。
* 使用 `DoRService` 以程式設計方式產生DoR。
* 從DoR排除隱藏欄位。
* 使用 `afAcceptLang` 請求參數在其他地區設定中檢視DoR。

### 除錯和測試最適化表單 {#debugging-and-testing-adaptive-forms}

[AEM Chrome增效模組是Google Chrome的瀏覽器擴充功能](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/) ，可提供除錯最適化表單的工具。 表單作者和開發人員可使用這些工具：

* 找出表單轉換的瓶頸並最佳化效能
* 在表單中除錯關鍵字和bindRef錯誤
* 啟用和配置日誌
* 表單中的除錯規則和指令碼
* 探索並瞭解guideBridge API

如需詳細資訊，請 [參閱「AEM Chrome增效模組——最適化表單](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/adaptive-form/)」。

Calvin SDK是Adaptive Forms開發人員用來測試Adaptive Forms的公用API。 Calvin SDK建立在 [Hobbes.js測試架構之上](https://docs.adobe.com/docs/en/aem/6-3/develop/ref/test-api/index.html)。 您可使用架構來測試下列項目：

* 最適化表單的轉譯體驗
* 最適化表單的預填體驗
* 提交最適化表單的體驗
* 運算式規則
* 驗證
* 延遲載入

如需詳細資訊，請參 [閱自動測試最適化表單](/help/forms/using/calvin.md)。

### 驗證AEM伺服器上的最適化表單 {#validating-adaptive-forms-on-aem-server}

需要進行伺服器端驗證，以防止任何嘗試略過用戶端驗證，以及資料提交和違反業務規則的可能危害。 伺服器端驗證是透過載入所需的用戶端程式庫來在伺服器上執行。

* 在用戶端程式庫中包含函式，以驗證最適化表單中的運算式，並在最適化表單容器對話方塊中指定用戶端程式庫。 如需詳細資訊，請參 [閱伺服器端重新驗證](/help/forms/using/configuring-submit-actions.md#p-server-side-revalidation-in-adaptive-form-p)。
* 伺服器端驗證會驗證表單模型。 建議您建立個別的用戶端程式庫以進行驗證，而不要將它與HTML樣式和DOM控制等其他項目混合在相同的用戶端程式庫中。

### 本地化最適化表單 {#localizing-adaptive-forms}

AEM提供翻譯工作流程，讓您用來本地化最適化表單。 如需詳細資訊，請參 [閱「使用AEM轉譯工作流程來當地語系化最適化表單](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md)」。

在本地化自適應表單時的一些最佳做法如下：

* 針對表單中的常用元素使用最適化表單片段，並本地化片段。 它可確保片段本地化一次，並反映所有使用本地化片段的形式。
* 新增元件或在本地化表單中套用指令碼等任何修改都不會自動本地化。 因此，在本地化表單之前，您必須先完成表單的定版作業，以避免出現多個本地化週期。
* 使用 `afAcceptLang` 請求參數來覆寫瀏覽器地區設定，並在指定的地區設定中轉譯表單。 例如，下列URL將強制以日文地區來轉換表單，而不考慮瀏覽器設定中指定的地區：

   `https://[server]:[port]/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

* AEM Forms目前支援以英文(en)、西班牙文(es)、法文(fr)、義大利文(it)、德文(de)、日文(ja)、葡萄牙文——巴西(pt-br)、中文-(zh-tn)、中文——台灣(zh-tw)和韓文(ko-kr)地區語言，將最適化表單內容本土化。 不過，您可以在執行時期新增對最適化表單新地區設定的支援。 如需詳細資訊，請參 [閱支援最適化表單本地化的新地區設定](/help/forms/using/supporting-new-language-localization.md)。

## 準備表單專案以供製作 {#prepare-forms-project-for-production}

### 添加表單處理伺服器 {#adding-forms-processing-server}

您可以設定位於安全區防火牆後方的額外AEM Forms伺服器例項。 您可將此例項用於：

* **批次處理**:以大量負載的批次重複或排程的作業。 例如，列印陳述式、產生對應，以及使用檔案服務（例如PDF產生器、輸出和匯編器）。
* **儲存PII資料**:將PII資料儲存至處理伺服器。 如果您已使用自訂儲存提供者來儲存PII資料，則不需要此選項。

### 將專案移至其他環境 {#moving-project-to-another-environment}

您通常需要將AEM專案從一個環境移至另一個環境。 移動時要記住的一些關鍵事項如下：

* 備份您現有的用戶端程式庫、自訂程式碼和設定。
* 在新環境中按照指定順序手動部署產品包和修補程式。
* 以手動方式部署專案專用的程式碼套件和套件組合，並將它們當成個別的套件或套件組合，放在新的AEM伺服器上。
* (僅&#x200B;*限JEE上的AEM Forms*)在Forms Workflow伺服器上手動部署LCA和DSC。
* 使用 [「匯出——匯入](/help/forms/using/import-export-forms-templates.md) 」功能將資產移至新環境。 您也可以配置複製代理並發佈資產。

### 設定AEM {#configuring-aem}

以下是設定AEM以改善整體效能的一些最佳實務：

* 從Felix Console為JavaScript和CSS啟用HTML用戶端程式庫壓縮。 請參 [閱範例所說明的Clientlibs](https://blogs.adobe.com/experiencedelivers/experience-management/clientlibs-explained-example/)。
* 快取位於的所有用戶端程式 `/etc.clientlibs/fd` 庫，以及AEM Dispatcher上任何其他自訂用戶端程式庫，以提高已發佈表單的回應速度與安全性。 如需詳細資訊，請參 [閱Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)。

* 請勿快取 `/content/forms/af/` 和 `/content/dam/formsanddocuments/*` 路徑。 如需設定最適化表單快取的詳細資訊，請參閱快 [取最適化表單](/help/forms/using/configure-adaptive-forms-cache.md)。

* 透過網頁伺服器壓縮模組啟用HTML。 如需詳細資訊，請參 [閱「AEM Forms伺服器的效能調整」](/help/forms/using/performance-tuning-aem-forms.md)。
* 增加大型表單的每個請求組態的呼叫。 請參 [閱最佳化大型和複雜表單的效能](/help/forms/using/adaptive-forms-best-practices.md#optimizing-performance-of-large-and-complex-forms)。
* 建立 [由錯誤處理常式顯示的自訂錯誤頁面](https://helpx.adobe.com/experience-manager/6-2/sites-developing/customizing-errorhandler-pages.html)。
* 保全AEM Forms伺服器。

   * 使用 `nosamplecontent` 執行模式以確保生產伺服器上沒有部署範例內容和範例使用者。 請參 [閱「在生產就緒模式中執行AEM](/help/sites-administering/production-ready.md)」。

* 將堆大小保持在至少8 GB。 如需其他設定，請參 [閱「AEM Forms伺服器的效能調整」](/help/forms/using/performance-tuning-aem-forms.md)。
* 使用服務用戶會話而不是管理會話來執行服務級別任務。 如需詳細資訊，請參閱「 [服務驗證」](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html)。

>[!VIDEO](https://vimeo.com/)

### 為草稿和提交的表單資料配置外部儲存 {#external-storage}

在生產環境中，建議不要將提交的表單資料儲存在AEM儲存庫中。 Forms Portal Store、Store Content和Store PDF提交動作的預設實作會將表單資料儲存在AEM儲存庫中。 這些提交動作僅用於演示目的。 此外，「儲存和繼續」和「自動儲存」功能預設會使用入口儲存空間。 因此，請考慮以下建議：

* **儲存草稿資料**:如果您使用最適化表單的「草稿」功能，則應實作自訂的「服務提供介面」(SPI)，將草稿資料儲存在更安全的儲存中，例如資料庫。 如需詳細資訊，請參 [閱將草稿和提交元件與資料庫整合的範例](/help/forms/using/integrate-draft-submission-database.md)。

* **儲存提交資料**:如果您使用表單入口提交儲存，則應實施自定義SPI以將提交資料儲存在資料庫中。 如需 [整合草稿和提交元件與資料庫的範例](/help/forms/using/integrate-draft-submission-database.md) ，請參閱範例。

   您也可以撰寫自訂的提交動作，將表單資料和附件儲存在安全儲存空間中。 如需詳 [細資訊，請參閱撰寫最適化表單的自訂提交動作](/help/forms/using/custom-submit-action-form.md) 。

### 處理個人識別資訊 {#handling-personally-identifiable-information}

組織面臨的主要挑戰之一，是如何處理個人識別(PII)資料。 一些將幫助您處理此類資料的最佳做法如下：

* 使用安全的外部儲存（如資料庫）來儲存草稿和提交表單中的資料。 請參 [閱為草稿和提交的表單資料配置外部儲存](/help/forms/using/adaptive-forms-best-practices.md#external-storage)。
* 使用「條款與條件」表單元件，在啟用自動儲存前取得使用者的明確同意。 在此情況下，請僅在使用者同意「條款」和「條件」元件中的條件時啟用自動儲存。

