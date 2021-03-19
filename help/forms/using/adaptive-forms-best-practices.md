---
title: 使用最適化表單的最佳範例
seo-title: 使用最適化表單的最佳範例
description: 說明建立AEM Forms專案、開發最適化表單以及最佳化AEM Forms系統效能的最佳實務。
seo-description: 說明建立AEM Forms專案、開發最適化表單以及最佳化AEM Forms系統效能的最佳實務。
uuid: ed95fc64-56b3-4ea1-a5ba-2e96953fca56
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 43c431e4-5286-4f4e-b94f-5a7451c4a22c
feature: 適用性表單
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '4298'
ht-degree: 0%

---


# 使用最適化表單{#best-practices-for-working-with-adaptive-forms}的最佳實務

## 概覽 {#overview}

Adobe Experience Manager(AEM)表格可協助您將複雜的交易轉換為簡單、愉悅的數位體驗。 但是，它需要共同努力來實施、建立、執行和維護一個高效和富有成效的AEM Forms生態系統。

本檔案提供管理員、作者和開發人員在使用AEM Forms時可從中獲益的准則和建議，尤其是最適化表單元件。 它討論從設定表單開發專案到設定、自訂、製作和最佳化AEM Forms的最佳實務。 這些最佳做法共同有助於AEM Forms生態系統的整體業績。

此外，以下是一般最佳實務的建議讀AEM數：

* [最佳實務：部署和維護AEM](/help/sites-deploying/best-practices.md)
* [最佳實務：製作內容](/help/sites-authoring/best-practices.md)
* [最佳實務：管理AEM](/help/sites-administering/administer-best-practices.md)
* [最佳實務：開發解決方案](/help/sites-developing/best-practices.md)

## 設定和配置AEM Forms{#set-up-and-configure-aem-forms}

### 設定表單開發專案{#setting-up-forms-development-project}

簡化和標準化的專案結構可大幅降低開發和維護工作。 Apache Maven是建立專案時建議使用的開放原始碼AEM工具。

* 使用Apache Maven `aem-project-archetype`來建立和管理專案的結AEM構。 它會為您的專案建立建議的結構AEM和範本。 此外，它還提供建置自動化和變更控制系統，以協助管理專案。

   * 使用maven `archetype:generate`命令生成初始結構。
   * 使用maven `eclipse:eclipse`命令產生eclipse專案檔案，並將專案匯入eclipse。

如需詳細資訊，請參閱[如何使用Apache MavenAEM](/help/sites-developing/ht-projects-maven.md)建立專案。

* FileVault工具或VLT可幫助您將CRX或實例的內AEM容映射到檔案系統。 它提供了變更控制管理操作，如項目內容的登入和登AEM出。 請參閱[如何使用VLT工具](/help/sites-developing/ht-vlttool.md)。

* 如果您使用Eclipse整合的開發環境，則可以使用開發人員工具，將Eclipse IDE與例項AEM順暢整合，以建立AEM應用程AEM式。 如需詳細資訊，請參閱[AEM Eclipse的開發人員工具](/help/sites-developing/aem-eclipse.md)。

* 請勿在/libs資料夾中儲存任何內容或進行任何修改。 在/app資料夾中建立覆蓋，以延伸或覆寫預設功能。

* 當您建立封裝以移動內容時，請確定封裝篩選路徑正確，且只提及必要的路徑。

* 請勿在/libs資料夾中儲存任何內容或進行任何修改。 在/app資料夾中建立覆蓋，以延伸或覆寫預設功能。

* 為軟體包定義正確的相依性，以強制執行預先確定的安裝順序／順序。

* 請勿在/libs或/apps中建立任何可參考的節點。

### 規劃編寫環境{#planning-for-authoring-environment}

設定專案後，AEM請定義製作和自訂最適化表單範本和元件的策略。

* 最適化表單範本是一AEM個專用頁面，定義最適化表單的結構和頁首——頁尾資訊。 範本具有預先設定的版面配置、樣式和最適化表單的基本結構。 AEM Forms提供現成可用的範本和元件，供您用來製作最適化表單。 不過，您可以根據需求建立自訂範本和元件。 建議您收集在最適化表單中需要的其他範本和元件需求。 如需詳細資訊，請參閱[自訂最適化表單和元件](/help/forms/using/adaptive-forms-best-practices.md#customize-components)。
* AEM Forms可讓您根據下清單單模型建立最適化表單。 表單模型用作表單與系統之間資料交換的介面AEM，並為自適應表單內外的資料流提供基於XML的結構。 另外，表單模型以模式和XFA約束的形式對自適應表單施加規則和約束。

   * **無**:使用此選項建立的最適化表單不會使用任何表單模型。從這種表單中生成的資料XML具有平坦的結構，具有欄位和相應的值。
   * **XML或JSON結構描述**:XML和JSON結構描述資料由組織中的後端系統產生或使用的結構。您可以將架構與最適化表單建立關聯，並使用其元素將動態內容新增至最適化表單。 架構的元素可在內容瀏覽器的「資料模型物件」索引標籤中使用，以製作最適化表單。 您可以拖放架構元素來建立表單。
   * **XFA表單範本**:如果您投資於以XFA為基礎的HTML5表單，這是理想的表單模型。它提供將XFA型表單轉換為最適化表單的直接方式。 任何現有的XFA規則都會保留在相關的最適化表單中。 產生的最適化表單支援XFA結構，例如驗證、事件、屬性和模式。
   * **表單資料模型**:如果您想要整合後端系統（例如資料庫、web services和使用者設定檔），以預先填寫最適化表單，並將提交的表單資料寫回後端系統，則此為偏好的表單模型。表單資料模型編輯器可讓您定義並設定表單資料模型中的實體和服務，以便用來建立最適化表單。 如需詳細資訊，請參閱[AEM Forms資料整合](/help/forms/using/data-integration.md)。

請務必謹慎選擇不僅符合您需求的資料模型，而且延伸您對XFA和XSD資產的現有投資（如果有的話）。 建議使用XSD模型來建立表單範本，因為產生的XML會依照架構定義的XPATH包含資料。 使用XSD模型作為表單資料模型的預設選擇，也有助於將表單設計與處理和使用資料的後端系統解耦，而且由於表單欄位的一對一對應，因此可改善表單的效能。 此外，欄位的BindRef也可以使其資料值在XML中的XPATH。

如需詳細資訊，請參閱[建立最適化表單](/help/forms/using/creating-adaptive-form.md)。

* 在最適化表單中，有一些常見的章節。 您可以識別它們，並定義策略以促進內容重複使用。 最適化表單可讓您建立獨立的片段，並跨表單重複使用這些片段。 您也可以將最適化格式的面板儲存為片段。 片段中的任何變更都會反映在所有相關的表單中。 它可協助您縮短製作時間，並確保各表單的一致性。 此外，片段的使用讓可調式表單變得精簡，進而改善製作體驗，尤其是大型表單。 如需詳細資訊，請參閱[最適化表單片段](/help/forms/using/adaptive-form-fragments.md)。

### 自定義最適化表單和元件{#customize-components}

* AEM Forms提供現成可用的可調式表單範本，讓您用來建立可調式表單。 您也可以建立自己的範本。 提供靜AEM態和可編輯的範本。

   * 靜態範本由開發人員定義和設定。
   * 可編輯的範本由作者使用範本編輯器建立。 範本編輯器可讓您定義範本中的基本結構和初始內容。 結構層中的任何修改都會反映在使用該模板的所有表單中。 初始內容可包括預先配置的主題、預填充服務、提交動作等。 不過，這些設定可使用表單編輯器來修改表單。 如需詳細資訊，請參閱[最適化表單範本](/help/forms/using/template-editor.md)。

* 要設定特定欄位或面板實例的樣式，請使用[內嵌樣式](/help/forms/using/inline-style-adaptive-forms.md)。 或者，您可以在CSS檔案中定義類別，並在元件的「CSS類別」屬性中指定類別名稱。
* 在元件中加入用戶端程式庫，以一致地套用使用該元件之最適化表單或片段的樣式。 如需詳細資訊，請參閱[建立最適化表單頁面元件](/help/forms/using/custom-adaptive-forms-templates.md)。
* 在最適化表單容器屬性的CSS檔案路徑欄位中，指定用戶端資料庫的路徑，以套用用戶端資料庫中定義的樣式來選取最適化表單。
* 若要建立樣式的用戶端資料庫，您可以在「主題編輯器」基本的clientlib或「表單容器」屬性中設定自訂CSS檔案。
* 最適化表單提供面板版面配置，例如互動式、標籤式、收合式和精靈，以控制表單元件在面板中的排版方式。 您可以建立自訂面板版面，並讓表單作者使用。 如需詳細資訊，請參閱[建立最適化表單的自訂版面元件](/help/forms/using/custom-layout-components-forms.md)。
* 您也可以自訂特定的最適化表單元件，例如欄位和面板版面。

   * 使用的[Overlay](/help/sites-developing/overlays.md)功能可修AEM改元件的副本。 不建議修改預設元件。
   * 若要自訂/libs中現成可用的最適化表單元件的版面，除了[預設版面](/help/forms/using/layout-capabilities-adaptive-forms.md)外，[還可建立自訂版面元件](/help/forms/using/custom-layout-components-forms.md)。
   * 建立自訂介面工具集或外觀，以引入自訂互動活動。 不建議修改預設元件。 如需詳細資訊，請參閱[外觀架構](/help/forms/using/introduction-widgets.md)。

* 有關處理PII資料的建議，請參閱[處理個人識別資訊](/help/forms/using/adaptive-forms-best-practices.md#p-handling-personally-identifiable-information-p)。

## 製作最適化表單{#author-adaptive-forms}

### 使用觸控最佳化UI製作{#using-touch-optimized-ui-for-authoring}

* 使用側欄中的「物件」瀏覽器，快速存取表單階層中深層的欄位。 您可以使用搜索框在表單或對象樹中搜索對象，以便從一個對象導航到另一個對象。
* 要在邊欄的元件瀏覽器中查看和編輯元件的屬性，請選擇該元件並按一下![cmppr-1](assets/cmppr-1.png)。 您也可以按兩下元件，在屬性瀏覽器中檢視其屬性。
* 使用鍵盤快速鍵，在表單上快速動作。 請參閱[AEM Forms鍵盤快速鍵](/help/forms/using/keyboard-shortcuts.md)。

* 建議只在最適化表單頁面中使用最適化表單元件。 這些元件對其父級層次具有依賴性。 因此，請勿在頁面中使AEM用。

此外，請參閱[製作最適化表單簡介](/help/forms/using/introduction-forms-authoring.md)中的元件說明和最佳實務。

### 在最適化表單{#using-rules-in-adaptive-forms}中使用規則

AEM Forms提供[規則編輯器](/help/forms/using/rule-editor.md)，可讓您建立規則，將動態行為新增至最適化表單元件。 使用這些規則，您可以評估條件並觸發元件上的動作，例如顯示或隱藏欄位、計算值、動態變更下拉式清單等。

規則編輯器提供可視編輯器和代碼編輯器，用於編寫規則。 使用程式碼編輯器模式編寫規則時，請考慮下列事項：

* 在撰寫規則時，為表單欄位和元件使用有意義且唯一的名稱，以避免任何可能的衝突。
* 使用`this`運算子，讓元件在規則運算式中參照自身。 它可確保即使元件名稱變更，規則仍然有效。 例如，`field1.valueCommit script: this.value > 10`。

* 參照其他表單元件時，請使用元件名稱。 使用`value`屬性來擷取欄位或元件的值。 例如，`field1.value`。

* 依相對唯一階層來參考元件，以避免任何衝突。 例如，`parentName.fieldName`。

* 在處理複雜或常用的規則時，請考慮將商業邏輯編寫為個別用戶端程式庫中的函式，以便您指定並跨調適性表單重複使用。 用戶端程式庫應是獨立的程式庫，除jQuery和Undershore.js外，不應有任何外部相依性。 您也可以使用用戶端程式庫，對已提交的表單資料強制[伺服器端重新驗證](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form)。
* 最適化表單提供一組API，您可用來與最適化表單通訊，並對其執行動作。 部分關鍵API如下。 如需詳細資訊，請參閱適用於Forms的[JavaScript程式庫API參考](https://adobe.com/go/learn_aemforms_documentation_63)。

   * `guideBridge.reset()`:重設表單。
   * `guideBridge.submit()`:提交表格。
   * `guideBridge.setFocus(somExp, focusOption, runCompletionExp)`:將焦點設定為欄位。
   * `guideBridge.validate(errorList, somExpression, focus)`:驗證表單。
   * `guideBridge.getDataXML(options)`:以XML格式取得表單資料。
   * `guideBridge.resolveNode(somExpression)`:獲取表單對象。
   * `guideBridge.setProperty(somList, propertyName, valueList)`:設定表單對象的屬性。
   * 此外，您還可使用下列欄位屬性：

      * `field.value` 來更改欄位的值。
      * f `ield.enabled`以啟用／停用欄位。
      * `field.visible` 變更欄位的可見度。

* 最適化表單作者可能需要編寫JavaScript程式碼，才能建立表單中的商業邏輯。 雖然JavaScript功能強大而且有效，但可能會在安全性預期上造成損害。 因此，您必須確保表單作者是受信任的人物，而且在表單投入生產之前，有需要檢閱和核准JavaScript程式碼的程式。 管理員可以根據用戶組的角色或功能限制對規則編輯器的訪問權限。 請參閱[授予規則編輯器對選定用戶組的訪問權限](/help/forms/using/rule-editor-access-user-groups.md)。
* 您可以在規則中使用運算式，讓最適化表單變為動態。 所有運算式都是有效的JavaScript運算式，並使用最適化表單指令碼模型API。 這些運算式會傳回特定類型的值。 如需有關運算式和最佳實務的詳細資訊，請參閱[最適化表單運算式](/help/forms/using/adaptive-form-expressions.md)。

### 使用主題{#working-with-themes}

主題最適化可讓您建立可重複使用的樣式，可套用至各種表單，以提供一致的外觀和樣式。 建議使用「主題」來定義表單元件和面板的樣式。 主題的一些最佳做法如下：

* 使用資產庫，快速套用文字樣式、背景和影像。 在資產庫中新增樣式時，其他主題和表格編輯器的樣式模式都可使用。
* 使用頁面層級選擇器套用全域設定，例如字型和頁面背景。
* 使用用戶端程式庫，將現有或進階樣式匯入主題。
* 您可以在表單樣式圖層中覆寫特定欄位、面板或按鈕的樣式。
* 如果主題不符合樣式要求，您可以使用預先定義的類，如guideFieldNode、guideFieldLabel、guideFieldWidget和guidePanelNode，跨表單應用通用樣式。

如需詳細資訊，請參閱[主題](/help/forms/using/themes.md)。

### 優化大型和複雜表單的效能{#optimizing-performance-of-large-and-complex-forms}

表單製作者和使用者通常在以編寫模式或執行時期載入大型表單時，會遇到效能問題。 隨著表單中物件（欄位和面板）數目增加，製作與執行時期的體驗開始降低。 此外，它還可防止多位作者同時協作和製作表單。

請考慮下列最佳實務，以克服大型表單的效能問題：

* 建議使用XSD表單資料模型建立最適化表單，即使將XFA轉換為最適化表單（如果可能）亦然。
* 在可從使用者擷取資訊的最適化表單中，僅包含這些欄位和面板。 請考慮將靜態內容保持在最小，或使用URL在個別視窗中開啟。
* 雖然每個表格都是專為特定用途而設計，但大部分表格中都有一些常見的區段。 例如，個人詳細資料、地址、雇傭詳細資料等。 建立[最適化表單片段](/help/forms/using/adaptive-form-fragments.md)以用於一般表單元素和區段，並跨表單使用。 您也可以將現有表單中的面板儲存為片段。 片段中的任何變更都會反映在所有相關的最適化表單中。 它可促進協作製作，因為多位作者可同時處理組成表單的不同片段。

   * 與最適化表單類似，建議使用片段容器對話方塊在用戶端程式庫中定義所有片段特定樣式和自訂指令碼。 此外，請嘗試建立不依賴外部物件的自給自足片段。
   * 避免使用跨片段指令碼。 如果片段外有您必須參照的任何物件，請嘗試將該物件設為父表單的一部分。 如果對象仍必須駐留在另一個片段中，請在指令碼中按其名稱引用該對象。

* 使用「儲存並繼續」與自動儲存功能，定期儲存最適化表單，讓使用者稍後可重新造訪以完成表單。
* 設定片段以延遲載入。 在執行時期，標籤為緩慢載入的片段只會在需要時顯示。 它可大幅降低大型表單的載入時間。 可重複面板的片段也支援它。 如需詳細資訊，請參閱[設定延遲載入](/help/forms/using/lazy-loading-adaptive-forms.md)。

   * 請勿在回應式格點版面或第一個面板中設定片段的延遲載入。
   * 懶惰載入的片段不支援檔案附件和條款與條件元件。
   * 如果該值用於表單的其他部分，以便在卸載包含面板時使用該值，則將延遲載入面板中的值標籤為「全局使用值」。
   * 考慮針對應根據條件顯示或隱藏的片段編寫可見性規則。

### 預先填寫最適化表單{#prefilling-adaptive-forms}

您可以預先填入從後端擷取的資料，以協助使用者快速填入表格並避免輸入錯誤。

* AEM Forms提供預填服務，以讀取預先定義之資料XML檔案中的資料，並以預填XML檔案中的內容預填最適化表單的欄位。
* 預填充資料XML必須與與自適應表單相關聯的表單模型的模式相容。
* 在預填充XML中包括`afBoundedData`和`afUnBoundedData`區段，以在自適應表單中預填充綁定和未綁定欄位。

* 對於基於表單資料模型的自適應表單，AEM Forms提供現成可用的表單資料模型預填充服務。 預填充服務在自適應表單中查詢資料模型對象的資料源，並在呈現表單時預填充欄位值。
* 您也可以使用檔案、crx、服務或http通訊協定，預先填寫最適化表單。
* AEM Forms支援自訂的預填服務，您可將其外掛為OSGi服務，以預填最適化表單。

如需詳細資訊，請參閱[預填最適化表單欄位](/help/forms/using/prepopulate-adaptive-form-fields.md)。

### 簽署和送出最適化表單{#signing-and-submitting-adaptive-forms}

最適化表單需要「提交」動作來處理使用者指定的資料。 「提交」操作決定使用自適應表單對提交的資料執行的任務。

* 在最適化表單中，有數種現成可用的提交動作。 如需詳細資訊，請參閱[設定提交動作](/help/forms/using/configuring-submit-actions.md)。
* 如果預設提交操作不符合您的使用案例，您可以編寫自定義提交操作。 如需詳細資訊，請參閱[針對最適化表單撰寫自訂提交動作](/help/forms/using/custom-submit-action-form.md)。
* 包含伺服器端驗證，以防止提交無效的資料。

您可以運用Adobe Sign的多重簽名體驗，以最適化表單呈現。 在最適化表單中配置Adobe Sign時，請考慮以下事項。 如需詳細資訊，請參閱[以最適化形式使用Adobe Sign](/help/forms/using/working-with-adobe-sign.md)。

* Adobe Sign啟用的調適性表格必須在所有簽署者簽署表格後才會送出。 Forms會以「待簽署」狀態顯示，直到所有簽署者簽署表單為止。
* 您可以設定表單內簽署體驗，或在提交時將簽署者重新導向至簽署頁面。
* 視需要設定循序或平行的簽署體驗。

### 生成記錄文檔{#generating-document-of-record}

記錄檔案(DoR)是可列印、簽署或封存之最適化表單的平面化PDF版本。

* 根據自適應表單所基於的表單資料模型，可以按如下方式為DoR配置模板：

   * **XFA表單範本**:使用關聯的XDP檔案作為DoR模板。
   * **XSD架構**:使用與最適化表單使用相同XML架構的相關XFA範本。
   * **無**:使用自動產生的DoR。

* 直接從最適化表單編輯器的「記錄檔案」索引標籤，設定頁首、頁尾、影像、顏色、字型等。
* 使用`DoRService`以程式設計方式產生DoR。
* 從DoR排除隱藏欄位。
* 使用`afAcceptLang`請求參數在其他地區設定中檢視DoR。

### 調試和測試最適化表單{#debugging-and-testing-adaptive-forms}

[Chrome Plug-](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/) inis是Google Chrome的瀏覽器擴充功能，提供調試最適化表單的工具。表單作者和開發人員可使用這些工具：

* 找出表單轉換的瓶頸並最佳化效能
* 在表單中除錯關鍵字和bindRef錯誤
* 啟用和配置日誌
* 表單中的除錯規則和指令碼
* 探索並瞭解guideBridge API

如需詳細資訊，請參閱AEM[ Chrome外掛程式——最適化表單](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/adaptive-form/)。

Calvin SDK是一個公用API，可供Adaptive Forms開發人員用來測試AdaptiveForms。 Calvin SDK建立在[Hobbes.js測試架構](https://docs.adobe.com/docs/en/aem/6-3/develop/ref/test-api/index.html)之上。 您可使用架構來測試下列項目：

* 最適化表單的轉譯體驗
* 最適化表單的預填體驗
* 提交最適化表單的體驗
* 運算式規則
* 驗證
* 延遲載入

如需詳細資訊，請參閱[自動測試最適化表單](/help/forms/using/calvin.md)。

### 驗證伺服器AEM{#validating-adaptive-forms-on-aem-server}上的自適應表單

需要進行伺服器端驗證，以防止任何嘗試略過用戶端驗證，以及資料提交和違反業務規則的可能危害。 伺服器端驗證是透過載入所需的用戶端程式庫來在伺服器上執行。

* 在用戶端程式庫中包含函式，以驗證最適化表單中的運算式，並在最適化表單容器對話方塊中指定用戶端程式庫。 如需詳細資訊，請參閱[伺服器端重新驗證](/help/forms/using/configuring-submit-actions.md#p-server-side-revalidation-in-adaptive-form-p)。
* 伺服器端驗證會驗證表單模型。 建議您建立個別的用戶端程式庫以進行驗證，而不要將它與HTML樣式和DOM控制等其他項目混合在相同的用戶端程式庫中。

### 本地化最適化表單{#localizing-adaptive-forms}

提AEM供翻譯工作流程，讓您用來本地化最適化表單。 有關資訊，請參見[使AEM用翻譯工作流程本地化最適化表單](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md)。

在本地化自適應表單時的一些最佳做法如下：

* 針對表單中的常用元素使用最適化表單片段，並本地化片段。 它可確保片段本地化一次，並反映所有使用本地化片段的形式。
* 新增元件或在本地化表單中套用指令碼等任何修改都不會自動本地化。 因此，在本地化表單之前，您必須先完成表單的定版作業，以避免出現多個本地化週期。
* 使用`afAcceptLang`請求參數來覆寫瀏覽器地區設定，並在指定的地區設定中轉譯表單。 例如，下列URL將強制以日文地區來轉換表單，而不考慮瀏覽器設定中指定的地區：

   `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

* AEM Forms目前支援以英文(en)、西班牙文(es)、法文(fr)、義大利文(it)、德文(de)、日文(ja)、葡萄牙文——巴西(pt-BR)、中文(zh-CN)、中文——台灣(zh-TW)和韓文(ko-KR)地區語言，將調適性表單內容本地化。 不過，您可以在執行時期新增對最適化表單新地區設定的支援。 如需詳細資訊，請參閱[支援最適化表單本地化的新地區設定](/help/forms/using/supporting-new-language-localization.md)。

## 準備製作表單專案{#prepare-forms-project-for-production}

### 添加表單處理伺服器{#adding-forms-processing-server}

您可以配置位於安全區防火牆後方的AEM Forms伺服器的附加實例。 您可將此例項用於：

* **批次處理**:以大量負載的批次重複或排程的作業。例如，列印陳述式、產生對應，以及使用檔案服務（例如PDF產生器、輸出和匯編器）。
* **儲存PII資料**:將PII資料儲存至處理伺服器。如果您已使用自訂儲存提供者來儲存PII資料，則不需要此選項。

### 將項目移至其他環境{#moving-project-to-another-environment}

您通常需要將專案從一AEM個環境移至另一個環境。 移動時要記住的一些關鍵事項如下：

* 備份您現有的用戶端程式庫、自訂程式碼和設定。
* 在新環境中按照指定順序手動部署產品包和修補程式。
* 手動部署專案專用的程式碼套件和組合，並將之作為個別的套件或組合部署在新伺服器AEM上。
* (*JEE上的AEM Forms僅*)在Forms Workflow伺服器上手動部署LCA和DSC。
* 使用[Export-Import](/help/forms/using/import-export-forms-templates.md)功能將資產移至新環境。 您也可以配置複製代理並發佈資產。
* 升級時，請以新的API和功能取代所有已過時的API和功能。

### 配AEM置{#configuring-aem}

配置以改進整AEM體效能的一些最佳實務如下：

* 從Felix Console為JavaScript和CSS啟用HTML用戶端程式庫壓縮。 請參閱[Clientlibs，其說明由example](https://blogs.adobe.com/experiencedelivers/experience-management/clientlibs-explained-example/)說明。
* 快取`/etc.clientlibs/fd`處的所有用戶端程式庫，以及Dispatcher上任何其他自訂用戶端程式庫，以AEM提高已發佈表單的回應速度與安全性。 有關詳細資訊，請參見[Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)。

* 不快取`/content/forms/af/`和`/content/dam/formsanddocuments/*`路徑。 有關配置自適應表單快取的詳細資訊，請參見[快取自適應表單](/help/forms/using/configure-adaptive-forms-cache.md)。

* 透過網頁伺服器壓縮模組啟用HTML。 有關詳細資訊，請參見[AEM Forms伺服器的效能調整。](/help/forms/using/performance-tuning-aem-forms.md)
* 增加大型表單的每個請求組態的呼叫。 請參閱[優化大型和複雜表單的效能](/help/forms/using/adaptive-forms-best-practices.md#optimizing-performance-of-large-and-complex-forms)。
* 建立[由錯誤處理程式](https://helpx.adobe.com/experience-manager/6-2/sites-developing/customizing-errorhandler-pages.html)顯示的自定義錯誤頁。
* 安全的AEM Forms伺服器。

   * 使用`nosamplecontent`執行模式，確保生產伺服器上沒有部署示例內容和示例用戶。 請參閱[在生AEM產就緒模式中運行](/help/sites-administering/production-ready.md)。

* 將堆大小保持在至少8 GB。 有關其他設定，請參見[AEM Forms伺服器的效能調整](/help/forms/using/performance-tuning-aem-forms.md)。
* 使用服務用戶會話而不是管理會話來執行服務級別任務。 如需詳細資訊，請參閱[服務驗證](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html)。

>[!VIDEO](https://vimeo.com/)

### 為草稿和提交的表單資料配置外部儲存{#external-storage}

在生產環境中，建議不要將提交的表單資料儲存在儲存庫AEM中。 Forms門戶商店、儲存內容和儲存PDF提交動作的預設實作，會將表單資料儲存在儲存AEM庫中。 這些提交動作僅用於演示目的。 此外，「儲存和繼續」和「自動儲存」功能預設會使用入口儲存空間。 因此，請考慮以下建議：

* **儲存草稿資料**:如果您使用最適化表單的「草稿」功能，則應實作自訂的「服務提供介面」(SPI)，將草稿資料儲存在更安全的儲存中，例如資料庫。如需詳細資訊，請參閱[將草稿和提交元件與資料庫整合的範例](/help/forms/using/integrate-draft-submission-database.md)。

* **儲存提交資料**:如果您使用表單入口提交儲存，則應實施自定義SPI以將提交資料儲存在資料庫中。如需整合範例，請參閱[將草稿和提交元件與資料庫](/help/forms/using/integrate-draft-submission-database.md)整合的範例。

   您也可以撰寫自訂的提交動作，將表單資料和附件儲存在安全儲存空間中。 如需詳細資訊，請參閱[撰寫最適化表單的自訂提交動作](/help/forms/using/custom-submit-action-form.md)。

* **草稿ID的長度**:將最適化表單另存為草稿時，會產生草稿ID以唯一識別草稿。草稿ID欄位長度的最小值為26個字元。 Adobe建議將草稿ID長度設為26個或更多字元。

### 處理個人識別資訊{#handling-personally-identifiable-information}

組織面臨的主要挑戰之一，是如何處理個人識別(PII)資料。 一些將幫助您處理此類資料的最佳做法如下：

* 使用安全的外部儲存（如資料庫）來儲存草稿和提交表單中的資料。 請參閱[為草稿和提交的表單資料配置外部儲存](/help/forms/using/adaptive-forms-best-practices.md#external-storage)。
* 使用「條款與條件」表單元件，在啟用自動儲存前取得使用者的明確同意。 在此情況下，請僅在使用者同意「條款」和「條件」元件中的條件時啟用自動儲存。

