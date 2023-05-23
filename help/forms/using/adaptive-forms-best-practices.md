---
title: 使用自適應表單的最佳做法
seo-title: Best practices for working with adaptive forms
description: 介紹為AEM Forms系統設定項目、開發適應性表單和優化效能的最佳做法。
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

# 使用自適應表單的最佳做法 {#best-practices-for-working-with-adaptive-forms}

## 概觀 {#overview}

Adobe Experience Manager(AEM)表格可幫助您將複雜事務轉換為簡單、令人愉快的數字型驗。 但是，它需要共同努力來實施、建設、執行和維持一個高效和富有成效的AEM Forms生態系統。

本文檔提供了管理員、作者和開發人員在與AEM Forms合作時可從中獲益的指南和建議，特別是自適應表單元件。 它討論了從設定表單開發項目到配置、自定義、創作和優化AEM Forms的最佳做法。 這些最佳做法共同促進了AEM Forms生態系統的總體業績。

此外，以下是建議閱讀的一般最佳AEM做法：

* [最佳做法：部署和維AEM護](/help/sites-deploying/best-practices.md)
* [最佳做法：創作內容](/help/sites-authoring/best-practices.md)
* [最佳做法：管AEM理](/help/sites-administering/administer-best-practices.md)
* [最佳做法：開發解決方案](/help/sites-developing/best-practices.md)

## 設定和配置AEM Forms {#set-up-and-configure-aem-forms}

### 設定窗體開發項目 {#setting-up-forms-development-project}

簡化和標準化的項目結構可以大大減少開發和維護工作。 Apache Maven是建立項目時推薦的開源AEM工具。

* 使用Apache Maven `aem-project-archetype` 建立和管理項目AEM結構。 它為項目建立推薦的結構和AEM模板。 此外，它還提供了構建自動化和更改控制系統，以幫助管理項目。

   * 使用maven `archetype:generate` 命令生成初始結構。
   * 使用maven `eclipse:eclipse` 命令，以生成eclipse項目檔案並將項目導入eclipse。

有關詳細資訊，請參見 [如何使用Apache AEM Maven生成項目](/help/sites-developing/ht-projects-maven.md)。

* FileVault工具或VLT可幫助您將CRX或實例的內容AEM映射到檔案系統。 它提供變更控制管理操作，如項目內容的簽入和AEM簽出。 請參閱 [如何使用VLT工具](/help/sites-developing/ht-vlttool.md)。

* 如果使用Eclipse整合開發環境，則可以使用開發AEM人員工具將Eclipse IDE與實例無縫集AEM成以建立應AEM用程式。 有關詳細資訊，請參閱 [用AEM於Eclipse的開發人員工具](/help/sites-developing/aem-eclipse.md)。

* 不要在/libs資料夾中儲存任何內容或進行任何修改。 在/app資料夾中建立覆蓋以擴展或覆蓋預設功能。

* 在建立包以移動內容時，請確保包篩選器路徑正確且只提到所需路徑。

* 不要在/libs資料夾中儲存任何內容或進行任何修改。 在/app資料夾中建立覆蓋以擴展或覆蓋預設功能。

* 為軟體包定義正確的依賴項，以強制執行預定的安裝順序/順序。

* 請勿在/libs或/apps中建立任何可引用的節點。

### 創作環境的規劃 {#planning-for-authoring-environment}

設定項目後，AEM定義用於創作和自定義自適應表單模板和元件的策略。

* 自適應表單模板是定AEM義自適應表單的結構和頁眉 — 頁腳資訊的專用頁。 模板具有預配置的佈局、樣式和自適應表單的基本結構。 AEM Forms提供現成的模板和元件，您可以使用這些模板和元件來製作自適應表單。 但是，您可以根據需要建立自定義模板和元件。 建議收集在自適應表單中需要的其他模板和元件的要求。 有關詳細資訊，請參閱 [自定義自適應表單和元件](/help/forms/using/adaptive-forms-best-practices.md#customize-components)。
* AEM Forms允許您基於以下表單模型建立自適應表單。 該表單模型充當表單和系統之間資料交換的介面AEM，並提供基於XML的結構，用於自適應表單內外的資料流。 另外，表單模型以模式和XFA約束的形式對自適應表單施加規則和約束。

   * **無**:使用此選項建立的自適應表單不使用任何表單模型。 從這些表單生成的資料XML具有帶欄位和相應值的扁平結構。
   * **XML或JSON架構**:XML和JSON架構表示組織中後端系統生成或使用資料的結構。 可以將模式與自適應表單相關聯，並使用其元素將動態內容添加到自適應表單。 模式的元素可在內容瀏覽器的「資料模型對象」頁籤中用於創作自適應表單。 可以拖放架構元素以構建表單。
   * **XFA表單模板**:如果您對基於XFA的HTML5表單有投資，則它是理想的表單模型。 它提供了將基於XFA的表單轉換為自適應表單的直接方法。 任何現有的XFA規則都保留在關聯的自適應表單中。 生成的自適應表單支援XFA構造，如驗證、事件、屬性和模式。
   * **窗體資料模型**:如果您希望整合後端系統（如資料庫、 Web服務和用戶配置檔案）AEM，以預填自適應表單並將提交的表單資料寫入後端系統，則它是首選的表單模型。 使用「表單資料模型」編輯器，可以定義和配置表單資料模型中的實體和服務，這些實體和服務可用於建立自適應表單。 有關詳細資訊，請參見 [AEM Forms資料整合](/help/forms/using/data-integration.md)。

必須仔細選擇不僅符合您要求而且擴展您對XFA和XSD資產的現有投資（如果有）的資料模型。 建議使用XSD模型建立表單模板，因為生成的XML包含由架構定義的XPATH中的資料。 使用XSD模型作為表單資料模型的預設選擇也很有幫助，因為它將表單設計與處理和使用資料的後端系統解耦，並且它由於表單域的一到一映射而提高了表單效能。 此外，欄位的BindRef可以使其資料值的XPATH成為XML。

有關詳細資訊，請參見 [建立自適應窗體](/help/forms/using/creating-adaptive-form.md)。

* 在自適應表單中有一些公共部分。 您可以識別它們並定義一種策略來促進內容重用。 自適應表單允許您建立獨立的片段並跨表單重新使用它們。 也可以將自適應格式的面板另存為片段。 片段中的任何更改都反映在所有關聯的表單中。 它幫助您減少創作時間並確保各表單的一致性。 此外，片段的使用使自適應形式變得輕巧，從而改善了創作體驗，特別是大型形式。 有關詳細資訊，請參見 [自適應形式片段](/help/forms/using/adaptive-form-fragments.md)。

### 自定義自適應表單和元件 {#customize-components}

* AEM Forms提供現成的自適應表單模板，您可以使用這些模板建立自適應表單。 您還可以建立自己的模板。 提AEM供靜態和可編輯模板。

   * 靜態模板由開發人員定義和配置。
   * 可編輯模板由作者使用模板編輯器建立。 模板編輯器允許您定義模板中的基本結構和初始內容。 結構層中的任何修改都反映在使用該模板的所有表單中。 初始內容可包括預配置的主題、預填充服務、提交操作等。 但是，可以使用表單編輯器修改表單的這些設定。 有關詳細資訊，請參見 [自適應表單模板](/help/forms/using/template-editor.md)。

* 要為特定欄位或面板實例定型，請使用 [內聯樣式](/help/forms/using/inline-style-adaptive-forms.md)。 或者，可以在CSS檔案中定義類，並在元件的CSS類屬性中指定類名。
* 將客戶端庫包括在元件中，以便在使用該元件的自適應表單或片段中一致應用樣式。 有關詳細資訊，請參見 [建立自適應表單頁元件](/help/forms/using/custom-adaptive-forms-templates.md)。
* 應用在客戶端庫中定義的樣式，以通過在自適應表單容器屬性的CSS檔案路徑欄位中指定到客戶端庫的路徑來選擇自適應表單。
* 要建立樣式的客戶端庫，可以在主題編輯器基客戶端庫或「表單容器」屬性中配置自定義CSS檔案。
* 自適應表單提供面板佈局，如響應、標籤式、手風琴和嚮導，以控制表單元件在面板中的佈局方式。 您可以建立自定義面板佈局，並使其可供表單作者使用。 有關詳細資訊，請參見 [為自適應表單建立自定義佈局元件](/help/forms/using/custom-layout-components-forms.md)。
* 還可以定制特定的自適應表單元件，如欄位和面板佈局。

   * 使用 [覆蓋](/help/sites-developing/overlays.md) 修改組AEM件副本的功能。 不建議修改預設元件。
   * 要在/lib中自定義出廠設定自適應表單元件的佈局， [建立自定義佈局元件](/help/forms/using/custom-layout-components-forms.md) 除了 [預設佈局](/help/forms/using/layout-capabilities-adaptive-forms.md)。
   * 通過建立自定義小部件或外觀來引入自定義交互活動。 不建議修改預設元件。 有關詳細資訊，請參見 [外觀框架](/help/forms/using/introduction-widgets.md)。

* 請參閱 [處理個人身份資訊](/help/forms/using/adaptive-forms-best-practices.md#p-handling-personally-identifiable-information-p) 有關處理PII資料的建議。

### 建立表單模板

可以使用中啟用的表單模板建立自適應表單 **配置瀏覽器**。 要啟用表單模板，請參閱 [建立自適應表單模板](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/creating-your-first-adaptive-form/create-adaptive-form-template.html?lang=en)。

還可以從在另一作者電腦上建立的Adaptive Form包上載表單模板。 通過安裝，表單模板可用 [Aemforms引用 — *包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hant)。 建議的一些最佳做法是：
* 的 **諾薩姆** 僅建議作者使用runmode，而不建議發佈節點使用runmode。
* 僅在「作者」節點上執行資產（如自適應表單、主題、模板或雲配置）的創作，這些節點可在配置的「發佈」節點上發佈。
有關詳細資訊，請參見 [發佈和取消發佈表單和文檔](https://experienceleague.adobe.com/docs/experience-manager-65/forms/publish-process-aem-forms/publishing-unpublishing-forms.html?lang=en)
* Formsaddon包是創作和發佈所需的，以支援文檔服務操作；因此，它可以被視為一種依賴。
如果您只想要與Forms相關的示例模板、主題和DOR包，則可以從 [Aemforms引用 — *包](https://experienceleague.adobe.com/docs/experience-manager-65/forms/publish-process-aem-forms/publishing-unpublishing-forms.html?lang=en)。

有關詳細資訊，請參閱 [創作自適應表單簡介](/help/forms/using/introduction-forms-authoring.md)。

## 作者自適應表單 {#author-adaptive-forms}

### 使用觸控優化的UI進行創作 {#using-touch-optimized-ui-for-authoring}

* 使用邊欄中的「對象」瀏覽器快速訪問表單層次結構中深層的欄位。 可以使用搜索框在表單或對象樹中搜索對象，以便從一個對象導航到另一個對象。
* 要查看和編輯邊欄中元件瀏覽器中元件的屬性，請選擇元件，然後按一下 ![CMPPR-1](assets/cmppr-1.png)。 也可以按兩下某個元件在屬性瀏覽器中查看其屬性。
* 使用鍵盤快捷鍵對表單執行快速操作。 請參閱 [AEM Forms鍵盤快捷鍵](/help/forms/using/keyboard-shortcuts.md)。

* 建議只在自適應表單頁中使用自適應表單元件。 這些元件與其父層次結構有依賴關係。 因此，不要在頁面中使AEM用它們。

另請參閱中的元件說明和最佳做法 [創作自適應表單簡介](/help/forms/using/introduction-forms-authoring.md)。

### 在自適應表單中使用規則 {#using-rules-in-adaptive-forms}

AEM Forms提供 [規則編輯器](/help/forms/using/rule-editor.md) 允許您建立規則，以將動態行為添加到自適應表單元件。 使用這些規則，您可以評估條件並觸發元件上的操作，如顯示或隱藏欄位、計算值、動態更改下拉清單等。

規則編輯器提供用於編寫規則的可視編輯器和代碼編輯器。 使用代碼編輯器模式編寫規則時，請考慮以下事項：

* 為表單域和元件使用有意義且唯一的名稱，以避免在編寫規則時出現任何可能的衝突。
* 使用 `this` 用於元件在規則表達式中引用自身的運算子。 它確保即使元件名稱發生更改，該規則仍然有效。 比如說， `field1.valueCommit script: this.value > 10`。

* 在引用其他窗體元件時使用元件名稱。 使用 `value` 屬性，以提取欄位或元件的值。 比如說， `field1.value`。

* 按相對唯一層次結構引用元件以避免任何衝突。 比如說， `parentName.fieldName`。

* 在處理複雜或常用規則時，請考慮將業務邏輯作為函式寫入單獨的客戶端庫中，您可以跨自適應表單指定和重用這些函式。 客戶端庫應是自包含庫，除jQuery和Underwork.js外，不應具有任何外部依賴項。 您還可以使用客戶端庫強制 [伺服器端重新驗證](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form) 的子菜單。
* 自適應表單提供了一組API，您可以使用這些API與自適應表單通信並對自適應表單執行操作。 一些關鍵API如下所示。 有關詳細資訊，請參見 [用於Adaptive Forms的JavaScript庫API參考](https://adobe.com/go/learn_aemforms_documentation_63)。

   * `guideBridge.reset()`:重置窗體。
   * `guideBridge.submit()`:提交表單。
   * `guideBridge.setFocus(somExp, focusOption, runCompletionExp)`:將焦點設定為欄位。
   * `guideBridge.validate(errorList, somExpression, focus)`:驗證窗體。
   * `guideBridge.getDataXML(options)`:以XML形式獲取表單資料。
   * `guideBridge.resolveNode(somExpression)`:獲取表單對象。
   * `guideBridge.setProperty(somList, propertyName, valueList)`:設定窗體對象的屬性。
   * 此外，您還可以使用以下欄位屬性：

      * `field.value` 的子菜單。
      * `field.enabled` 啟用/禁用欄位。
      * `field.visible` 的子菜單。

* 自適應表單作者可能需要編寫JavaScript代碼以在表單中構建業務邏輯。 儘管JavaScript功能強大且高效，但它很可能會在安全預期方面做出犧牲。 因此，必須確保表單作者是可信的角色，並且在表單投入生產之前，需要進行審閱和批准JavaScript代碼的過程。 管理員可以根據用戶組的角色或功能限制對規則編輯器的訪問。 請參閱 [授予規則編輯器對選定用戶組的訪問權限](/help/forms/using/rule-editor-access-user-groups.md)。
* 可以使用規則中的表達式使自適應表單動態。 所有表達式都是有效的JavaScript表達式，並使用自適應表單指令碼模型API。 這些表達式返回某些類型的值。 有關表達式和最佳實踐的詳細資訊，請參見 [自適應表單表達式](/help/forms/using/adaptive-form-expressions.md)。

### 處理主題 {#working-with-themes}

適應主題允許您建立可重複使用的樣式，這些樣式可應用於表單中，以便保持一致的外觀和樣式。 建議使用「主題」來定義表單元件和面板的樣式。 圍繞主題的一些最佳做法如下：

* 使用資產庫可快速應用文本樣式、背景和影像。 當在資產庫中添加樣式時，該樣式可用於其它主題，並且在表單編輯器的樣式模式下。
* 使用頁面級選擇器應用全局設定（如字型和頁面背景）。
* 使用客戶端庫將現有或高級樣式導入到主題中。
* 您可以覆蓋窗體樣式層中特定欄位、面板或按鈕的樣式。
* 如果主題不滿足您的樣式要求，則可以使用預定義的類（如guideFieldNode、guideFieldLabel、guideFieldWidget和guidePanelNode）跨表單應用公共樣式。

有關詳細資訊，請參見 [主題](/help/forms/using/themes.md)。

### 優化大型和複雜形式的效能 {#optimizing-performance-of-large-and-complex-forms}

在創作模式或運行時載入大型表單時，表單作者和最終用戶通常會面臨效能問題。 隨著形式中的對象（欄位和面板）數量增加，創作和運行時體驗開始降低。 它還防止了多個作者同時協作和編寫表單。

請考慮以下最佳實踐，以克服大型表單的效能問題：

* 建議使用XSD表單資料模型建立自適應表單，即使在將XFA轉換為自適應表單時也是如此。
* 僅包括那些以自適應形式捕獲用戶資訊的欄位和面板。 請考慮將靜態內容保持為最小，或使用URL在單獨的窗口中開啟它們。
* 雖然每個表單都是為特定目的而設計的，但大多數表單中有一些共同的段。 例如，個人詳細資訊、地址、雇傭詳細資訊等。 建立 [自適應形式片段](/help/forms/using/adaptive-form-fragments.md) 用於常用窗體元素和節，並跨窗體使用它們。 也可以將現有窗體中的面板另存為片段。 片段中的任何更改都反映在所有關聯的自適應形式中。 它促進協作創作，因為多個作者可以同時處理組成表單的不同片段。

   * 與自適應表單類似，建議使用片段容器對話框在客戶端庫中定義所有片段特定的樣式和自定義指令碼。 另外，嘗試建立不依賴於外部對象的自足片段。
   * 避免使用交叉片段指令碼。 如果片段外有您必須引用的對象，請嘗試將該對象設定為父表單的一部分。 如果對象仍必須駐留在另一個片段中，請在指令碼中按其名稱引用它。

* 使用「保存並恢復並自動保存」定期保存自適應表單，並允許用戶稍後重新訪問以完成表單。
* 配置片段以延遲載入。 在運行時，標籤為延遲載入的片段僅在需要時才會呈現。 它顯著減少了大型飛機的裝載時間。 它還支援在具有可重複面板的片段中。 有關詳細資訊，請參見 [配置延遲載入](/help/forms/using/lazy-loading-adaptive-forms.md)。

   * 不要在響應網格佈局或第一面板中配置片段的延遲載入。
   * 延遲載入的片段不支援檔案附件和條款和條件元件。
   * 如果該值在窗體的其它部分中使用，則將延遲載入面板中的值標籤為「全局使用值」(Use Value Global)，以便在卸載包含面板時使用該值。
   * 考慮根據條件為應顯示或隱藏的片段編寫可見性規則。
* 設定 **每個請求的呼叫數** 的 **Apache Sling主Servlet** 數量相當多。 它使Forms伺服器能夠允許額外呼叫。 配置顯示預設值1500。 值1500調用用於其他Experience Manager元件，如站點和資產。 自適應表單的預設值集為20000。 如果遇到 `too many calls` 日誌中出錯或表單無法呈現，請嘗試將值增加到大數以解決此問題。 如果調用數超過20000，則表單很複雜，在瀏覽器中呈現表單可能需要一些時間。 這只是第一次載入表單，在快取表單之後，並且快取表單後，對效能沒有顯著影響。

### 預填充自適應表單 {#prefilling-adaptive-forms}

您可以用從後端讀取的資料預填充自適應表單域，以幫助用戶快速填充表單並避免鍵入錯誤。

* AEM Forms提供預填充服務，從預定義的資料XML檔案中讀取資料，並用預填充XML檔案中的內容預填充自適應表單的欄位。
* 預填充資料XML必須與與自適應表單關聯的表單模型的模式相容。
* 包括 `afBoundedData` 和 `afUnBoundedData` 的子目錄中的子目錄。

* 對於基於表單資料模型的自適應表單，AEM Forms提供現成表單資料模型預填充服務。 預填充服務在呈現表單時查詢自適應表單中的資料模型對象的資料源並預填充欄位值。
* 您還可以使用檔案、 crx、服務或http協定預填充自適應表單。
* AEM Forms支援自定義預填表單服務，您可以將其作為OSGi服務插入，以預填自適應表單。

有關詳細資訊，請參見 [預填充自適應表單域](/help/forms/using/prepopulate-adaptive-form-fields.md)。

### 簽名和提交自適應表單 {#signing-and-submitting-adaptive-forms}

自適應表單要求提交操作以處理用戶指定的資料。 「提交」(Submit)操作確定使用自適應表單對提交的資料執行的任務。

* 在自適應表單中，有幾種現成的提交操作可用。 有關詳細資訊，請參閱 [配置提交操作](/help/forms/using/configuring-submit-actions.md)。
* 如果預設提交操作不符合您的使用案例，則可以編寫自定義提交操作。 有關詳細資訊，請參見 [為自適應表單編寫自定義提交操作](/help/forms/using/custom-submit-action-form.md)。
* 包括伺服器端驗證，以防止提交無效資料。

您可以以自適應形式利用Adobe Sign的多符號體驗。 在以自適應形式配置Adobe Sign時，請考慮以下事項。 有關詳細資訊，請參閱 [以自適應形式使用Adobe Sign](/help/forms/using/working-with-adobe-sign.md)。

* Adobe Sign啟用的自適應表單只有在所有簽名者簽名後才提交。 Forms在所有簽名者簽署表單之前，將處於「掛起簽名」狀態。
* 您可以配置表單簽名體驗或在提交時將簽名者重定向到簽名頁面。
* 根據需要配置順序簽名或並行簽名體驗。

### 生成記錄文檔 {#generating-document-of-record}

記錄文檔(DoR)是可打印、簽名或存檔的自適應表單的拼合PDF版本。

* 根據自適應表單所基於的表單資料模型，您可以按如下方式為DoR配置模板：

   * **XFA表單模板**:將關聯的XDP檔案用作DoR模板。
   * **XSD架構**:使用與自適應表單使用的XML模式相同的關聯XFA模板。
   * **無**:使用自動生成的DoR。

* 從自適應表單編輯器的「記錄文檔」頁籤右側配置頁眉、頁腳、影像、顏色、字型等。
* 使用 `DoRService` 以寫程式方式生成DoR。
* 從DoR中排除隱藏欄位。
* 使用 `afAcceptLang` 請求參數以查看其他區域設定中的DoR。

### 調試和測試自適應表單 {#debugging-and-testing-adaptive-forms}

[AEMChrome插件](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/) 是GoogleChrome的瀏覽器擴展，它提供調試自適應表單的工具。 表單作者和開發人員可以使用這些工具：

* 確定窗體渲染的瓶頸並優化效能
* 調試關鍵字和窗體中的bindRef錯誤
* 啟用和配置日誌
* 調試窗體中的規則和指令碼
* 瀏覽並瞭解guideBridge API

有關詳細資訊，請參見 [AEMChrome插件 — 自適應窗體](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/adaptive-form/)。

### 驗證伺服器上的自適AEM應表單 {#validating-adaptive-forms-on-aem-server}

需要進行伺服器端驗證，以防止任何繞過客戶端驗證的嘗試，以及資料提交和業務規則違規的任何可能危害。 通過載入所需的客戶端庫在伺服器上執行伺服器端驗證。

* 在客戶端庫中包含用於驗證自適應表單中表達式的函式，並在自適應表單容器對話框中指定客戶端庫。 有關詳細資訊，請參見 [伺服器端重新驗證](/help/forms/using/configuring-submit-actions.md#p-server-side-revalidation-in-adaptive-form-p)。
* 伺服器端驗證會驗證表單模型。 建議建立單獨的客戶端庫以進行驗證，但不要將其與HTML樣式和DOM操作等其他內容混合到同一客戶端庫中。

### 定位自適應表單 {#localizing-adaptive-forms}

提AEM供翻譯工作流，您可以使用這些工作流來本地化自適應表單。 有關資訊，請參見 [使用翻AEM譯工作流本地化自適應表單](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md)。

本地化自適應表單時的一些最佳做法如下：

* 對表單上的公共元素使用自適應表單片段並定位片段。 它確保您對片段進行一次本地化，並且它反映所有使用本地化片段的形式。
* 任何修改（如添加新元件或以本地化形式應用指令碼）都不會自動本地化。 因此，必須在對表單進行本地化之前完成表單的定版，以避免多個本地化週期。
* 使用 `afAcceptLang` 請求參數，以覆蓋瀏覽器區域設定並在指定區域設定中呈現表單。 例如，以下URL將強制以日語語言環境呈現表單，而不考慮在瀏覽器設定中指定的語言環境：

   `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

* AEM Forms目前支援以英語(en)、西班牙語(es)、法語(fr)、義大利語(it)、德語(de)、日語(ja)、葡萄牙語 — 巴西語(pt-BR)、中文(zh-CN)、中文 — 台灣語(zh-TW)和韓語(ko-KR)語言環境本地化自適應表單內容。 但是，可以在運行時為自適應表單添加對新語言環境的支援。 有關詳細資訊，請參見 [支援新語言環境以實現自適應表單本地化](/help/forms/using/supporting-new-language-localization.md)。

## 準備表單項目以供生產 {#prepare-forms-project-for-production}

### 添加表單處理伺服器 {#adding-forms-processing-server}

您可以配置位於安全區域防火牆後面的AEM Forms伺服器的其他實例。 您可以將此實例用於：

* **批處理**:以重負荷批次重複或計畫的作業。 例如，打印語句、生成對應，以及使用文檔服務(如PDF生成器、輸出和匯編器)。
* **儲存PII資料**:將PII資料保存到處理伺服器。 如果您已使用自定義儲存提供程式儲存PII資料，則不需要此選項。

### 將項目移至其他環境 {#moving-project-to-another-environment}

您通常需要將項AEM目從一個環境移動到另一個環境。 移動時要記住的一些關鍵事項如下：

* 備份現有客戶端庫、自定義代碼和配置。
* 在新環境中按指定順序手動部署產品包和修補程式。
* 手動部署特定於項目的代碼包和包，並將它們作為單獨的包或包部署在新服AEM務器上。
* (*AEM Forms僅JEE*)在Forms Workflow伺服器上手動部署LCA和DSC。
* 使用 [導出 — 導入](/help/forms/using/import-export-forms-templates.md) 功能將資產移動到新環境。 您還可以配置複製代理並發佈資產。
* 升級時，請用新的API和功能替換所有過時的API和功能。

### 配置AEM {#configuring-aem}

配置以改進AEM整體效能的一些最佳做法如下：

* 從Felix控制台為JavaScript和CSS啟用HTML客戶端庫壓縮。
* 快取位於的所有客戶端庫 `/etc.clientlibs/fd` 以及調度程式上的任何其他自AEM定義客戶端庫，以提高已發佈表單的響應能力和安全性。 有關詳細資訊，請參見 [調度程式](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)。

* 不快取 `/content/forms/af/` 和 `/content/dam/formsanddocuments/*` 路徑。 有關配置自適應表單快取的詳細資訊，請參見 [快取自適應表單](/help/forms/using/configure-adaptive-forms-cache.md)。

* 通過Web伺服器壓縮模組啟用HTML。 有關詳細資訊，請參見 [AEM Forms伺服器的效能調整](/help/forms/using/performance-tuning-aem-forms.md)。
* 增加大型表單的每個請求配置的調用數。 請參閱 [優化大型和複雜形式的效能](/help/forms/using/adaptive-forms-best-practices.md#optimizing-performance-of-large-and-complex-forms)。
* 建立 [錯誤處理程式顯示的自定義錯誤頁](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/customizing-errorhandler-pages.html)。
* 保護AEM Forms伺服器。

   * 使用 `nosamplecontent` 運行模式，以確保生產伺服器上沒有部署示例內容和示例用戶。 請參閱 [在生AEM產就緒模式下運行](/help/sites-administering/production-ready.md)。

* 將堆大小保持在最小8 GB。 有關其他設定，請參見 [AEM Forms伺服器的效能調整](/help/forms/using/performance-tuning-aem-forms.md)。
* 使用服務用戶會話而不是管理會話來執行服務級別任務。 有關詳細資訊，請參見 [服務驗證](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html)。

>[!VIDEO](https://vimeo.com/)

### 為草稿和提交的表單資料配置外部儲存 {#external-storage}

在生產環境中，建議不要將提交的表單資料儲存在儲存AEM庫中。 Forms門戶儲存、儲存內容和儲存PDF的預設實現操作將表單資料儲存在儲存AEM庫中。 這些提交操作僅用於演示目的。 另外，預設情況下，「保存和恢復」和「自動保存」功能使用入口儲存。 因此，考慮以下建議：

* **儲存草稿資料**:如果使用自適應表單的草稿功能，則應實現自定義服務提供介面(SPI)，以將草稿資料儲存在更安全的儲存中。 有關詳細資訊，請參見 [將草稿和提交元件與資料庫整合的示例](/help/forms/using/integrate-draft-submission-database.md)。

* **儲存提交資料**:如果使用表單門戶提交儲存，則應實現自定義SPI以將提交資料儲存在資料庫中。 請參閱 [將草稿和提交元件與資料庫整合的示例](/help/forms/using/integrate-draft-submission-database.md) 樣例整合。

   您還可以編寫一個自定義提交操作，將表單資料和附件儲存在安全儲存中。 請參閱 [為自適應表單編寫自定義提交操作](/help/forms/using/custom-submit-action-form.md) 的子菜單。

* **繪製ID的長度**:將自適應表單另存為繪製時，將生成一個繪製ID以唯一標識繪製。 草稿ID欄位長度的最小值為26個字元。 Adobe建議將草稿ID長度設定為26個或更多字元。

### 處理個人身份資訊 {#handling-personally-identifiable-information}

組織面臨的一個關鍵挑戰是如何處理個人身份識別(PII)資料。 一些有助於處理此類資料的最佳實踐如下：

* 使用安全的外部儲存（如資料庫）來儲存草稿和已提交表單中的資料。 請參閱 [為草稿和提交的表單資料配置外部儲存](/help/forms/using/adaptive-forms-best-practices.md#external-storage)。
* 使用「條款和條件」窗體元件在啟用自動保存之前獲得用戶的明確同意。 在這種情況下，僅當用戶同意條款和條件元件中的條件時，才啟用自動保存。


