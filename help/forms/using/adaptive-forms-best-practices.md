---
title: 使用最適化表單的最佳作法
description: 說明設定AEM Forms專案、開發最適化表單及最佳化AEM Forms系統效能的最佳實務。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
feature: Adaptive Forms,Foundation Components,Core Components
exl-id: 5c75ce70-983e-4431-a13f-2c4c219e8dde
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 6ec4eca0c0ad5ecfe18ffc766e6415a0f48506a9
workflow-type: tm+mt
source-wordcount: '5963'
ht-degree: 0%

---

# 使用最適化表單的最佳作法 {#best-practices-for-working-with-adaptive-forms}

<span class="preview"> Adobe建議使用現代且可擴充的資料擷取[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hant)  針對[建立新的最適化Forms](/help/forms/using/create-an-adaptive-form-core-components.md)  或[將最適化Forms新增至AEM Sites頁面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。 這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文會介紹使用基礎元件編寫最適化表單的舊方法。</span>

## 概觀 {#overview}

Adobe Experience Manager (AEM)表單可協助您將複雜的交易轉換為簡單、愉快的數位體驗。 然而，您需要共同努力來實施、建立、執行及維護有效率且富有成效的AEM Forms生態系統。

本檔案提供表單管理員、作者和開發人員在使用AEM Forms （尤其是調適型表單元件）時可受益的准則和建議。 此影片探討最佳實務，從設定表單開發專案，到設定、自訂、編寫和最佳化AEM Forms。 這些最佳實務會共同為AEM Forms生態系統的整體效能作出貢獻。

此外，以下是一般AEM最佳實務的建議閱讀：

* [最佳實務：部署和維護AEM](/help/sites-deploying/best-practices.md)
* [最佳實務：製作內容](/help/sites-authoring/best-practices.md)
* [最佳作法：管理AEM](/help/sites-administering/administer-best-practices.md)
* [最佳實務：開發解決方案](/help/sites-developing/best-practices.md)

## 設定和配置AEM Forms {#set-up-and-configure-aem-forms}

### 設定表單開發專案 {#setting-up-forms-development-project}

簡化和標準化的專案結構可大幅減少開發和維護工作。 Apache Maven是用於建置AEM專案的建議開放原始碼工具。

* 使用Apache Maven `aem-project-archetype`建立和管理AEM專案的結構。 它會為您的AEM專案建立建議的結構和範本。 此外，它還提供建置自動化和變更控制系統，以協助管理專案。

   * 使用maven `archetype:generate`命令產生初始結構。
   * 使用maven `eclipse:eclipse`命令產生eclipse專案檔案，並將專案匯入eclipse。

如需詳細資訊，請參閱[如何使用Apache Maven建置AEM專案](/help/sites-developing/ht-projects-maven.md)。

* FileVault工具或VLT可協助您將CRX或AEM執行個體的內容對應至您的檔案系統。 它提供變更控制管理作業，例如AEM專案內容的簽入和簽出。 請參閱[如何使用VLT工具](/help/sites-developing/ht-vlttool.md)。

* 如果您使用Eclipse整合式開發環境，您可以使用AEM開發人員工具將Eclipse IDE與AEM執行個體緊密整合，以建立AEM應用程式。 如需詳細資訊，請參閱[Eclipse的AEM開發人員工具](/help/sites-developing/aem-eclipse.md)。

* 請勿在/libs資料夾中儲存任何內容或進行任何修改。 在/app資料夾中建立覆蓋以擴充或覆寫預設功能。

* 當您建立封裝以移動內容時，請確保封裝篩選路徑正確，並且只提到必要的路徑。

* 請勿在/libs資料夾中儲存任何內容或進行任何修改。 在/app資料夾中建立覆蓋以擴充或覆寫預設功能。

* 定義套件的正確相依性，以強制預先決定的安裝順序/順序。

* 請勿在/libs或/apps中建立任何可參照的節點。

### 規劃製作環境 {#planning-for-authoring-environment}

設定AEM專案後，定義製作和自訂最適化表單範本和元件的策略。

* 調適型表單範本是專門的AEM頁面，可定義調適型表單的結構和頁首頁尾資訊。 範本有預先設定的最適化表單版面、樣式和基本結構。 AEM Forms提供現成可用的範本和元件，供您製作調適型表單。 不過，您可以根據需求建立自訂範本和元件。 建議您收集最適化表單中所需其他範本和元件的需求。 如需詳細資訊，請參閱[自訂最適化表單和元件](/help/forms/using/adaptive-forms-best-practices.md#customize-components)。
* 建議您使用表單管理員使用者介面而非使用CRX封裝管理員使用者介面上傳表單套件，因為透過CRX封裝管理員上傳套件有時可能會導致異常。
* AEM Forms可讓您根據下清單單模型建立最適化表單。 表單模型可作為表單與AEM系統之間資料交換的介面，並為最適化表單內外資料流提供XML型結構。 此外，表單模型會以結構描述和XFA限制的形式對調適型表單施加規則和限制。

   * **無**：使用此選項建立的最適化表單不使用任何表單模型。 從此類表單產生的資料 XML 具有包含欄位和對應值的單層結構。
   * **XML或JSON結構描述**： XML和JSON結構描述代表貴組織中後端系統產生或使用資料的結構。 您可以將結構描述關聯至最適化表單，並使用其元素將動態內容新增至最適化表單。 結構描述的元素可在內容瀏覽器的「資料模型物件」標籤中使用，以編寫調適型表單。 您可以拖放結構元素來建置表單。
   * **XFA表單範本**：如果您有投資以XFA為基礎的HTML5表單，這會是理想的表單模型。 它可讓您直接將XFA式表單轉換為最適化表單。 任何現有的XFA規則都會保留在關聯的調適型表單中。 產生的調適型表單支援XFA建構，例如驗證、事件、屬性和模式。
   * **表單資料模型**：如果您想要整合您的後端系統(例如資料庫、Web服務和AEM使用者設定檔)，以預先填寫最適化表單並將提交的表單資料寫入後端系統，這會是您偏好的表單模型。 表單資料模型編輯器可讓您在可用來建立調適型表單的表單資料模型中定義及設定實體和服務。 如需詳細資訊，請參閱[AEM Forms資料整合](/help/forms/using/data-integration.md)。

請務必謹慎選擇資料模型，不僅要符合您的需求，還要擴大您對XFA和XSD資產（如果有的話）的現有投資。 使用XSD模型建立表單範本，因為產生的XML包含結構描述所定義的每個XPATH的資料。 使用XSD模型作為表單資料模型的預設選擇也有幫助，因為它將表單設計從處理和使用資料的後端系統分離開來，並且由於表單欄位的一對一對應而改善了表單的效能。 此外，欄位的BindRef可以設為其資料值的XML格式XPATH。

如需詳細資訊，請參閱[建立最適化表單](/help/forms/using/creating-adaptive-form.md)。

* 最適化表單中會有一些通用區段。 您可以識別這些變數並定義策略以促進內容重複使用。 最適化表單可讓您建立獨立的片段，並在各個表單中重複使用。 您也可以將最適化表單中的面板儲存為片段。 片段中的任何變更會反映在所有關聯的表單中。 它有助於減少編寫時間，並確保各表單的一致性。 此外，使用片段使得最適化表單變得輕量化，進而改善編寫體驗，尤其是大型表單。 如需詳細資訊，請參閱[最適化表單片段](/help/forms/using/adaptive-form-fragments.md)。

### 自訂最適化表單和元件 {#customize-components}

* AEM Forms提供可用於建立最適化表單的現成最適化表單範本。 您也可以建立自己的範本。 AEM提供靜態和可編輯的範本。

   * 靜態範本由開發人員定義和設定。
   * 可編輯的範本是由作者使用範本編輯器建立的。 範本編輯器可讓您定義範本中的基本結構和初始內容。 結構圖層中的任何修改都會反映在使用該範本的所有表單中。 初始內容可能包括預先設定的主題、預填服務、提交動作等。 不過，您可以使用表單編輯器修改表單的這些設定。 如需詳細資訊，請參閱[最適化表單範本](/help/forms/using/template-editor.md)。

* 若要設定特定欄位或面板執行個體的樣式，請使用[內嵌樣式](/help/forms/using/inline-style-adaptive-forms.md)。 或者，您可以在CSS檔案中定義類別，並在元件的CSS Class屬性中指定類別名稱。
* 在元件中加入使用者端資料庫，以便一致地套用樣式至使用該元件的調適型表單或片段。 如需詳細資訊，請參閱[建立最適化表單頁面元件](/help/forms/using/custom-adaptive-forms-templates.md)。
* 透過在適用性表單容器屬性的CSS檔案路徑欄位中指定使用者端資料庫的路徑，套用使用者端資料庫中定義的樣式以選取適用性表單。
* 若要建立樣式的使用者端資料庫，您可以在主題編輯器基底clientlib或表單容器屬性中設定自訂CSS檔案。
* 調適型表單提供面板配置，例如回應式、索引標籤、摺疊式功能表和精靈，以控制表單元件在面板中的配置方式。 您可以建立自訂面板版面配置，並讓表單作者可以使用它們。 如需詳細資訊，請參閱[建立最適化表單的自訂配置元件](/help/forms/using/custom-layout-components-forms.md)。
* 您也可以自訂特定的最適化表單元件，例如欄位和面板版面配置。

   * 使用AEM的[覆蓋](/help/sites-developing/overlays.md)功能來修改元件的復本。 不建議修改預設元件。
   * 若要自訂/libs中現成可用的最適化表單元件的版面，除了[預設版面](/help/forms/using/layout-capabilities-adaptive-forms.md)之外，還要[建立自訂版面元件](/help/forms/using/custom-layout-components-forms.md)。
   * 透過建立自訂Widget或外觀來引入自訂互動。 不建議修改預設元件。 如需詳細資訊，請參閱[外觀架構](/help/forms/using/introduction-widgets.md)。

* 如需處理PII資料的建議，請參閱[處理個人識別資訊](/help/forms/using/adaptive-forms-best-practices.md#p-handling-personally-identifiable-information-p)。

### 建立表單範本

您可以使用&#x200B;**設定瀏覽器**&#x200B;中啟用的表單範本來建立最適化表單。 若要啟用表單範本，請參閱[建立最適化表單範本](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/creating-your-first-adaptive-form/create-adaptive-form-template.html?lang=zh-Hant)。

表單範本也可以從其他作者電腦上建立的最適化表單套件上傳。 透過安裝[aemforms-references-*封裝](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hant)，即可使用表單範本。 建議的一些最佳實務如下：

* 只建議為作者使用&#x200B;**nosamplecontent**&#x200B;執行模式，不建議為發佈節點使用。
* 製作資產（例如最適化表單、主題、範本或雲端設定）作業只會透過製作節點執行，其可在已設定的發佈節點發佈。
如需詳細資訊，請參閱[發佈與取消發佈表單與檔案](https://experienceleague.adobe.com/docs/experience-manager-65/forms/publish-process-aem-forms/publishing-unpublishing-forms.html?lang=zh-Hant)
* 製作和發佈需要Forms附加元件套件來支援檔案服務操作；因此，可將其視為相依性。
如果您只想要Forms相關的範例範本、主題和DOR封裝，則可以從[aemforms-references-*封裝](https://experienceleague.adobe.com/docs/experience-manager-65/forms/publish-process-aem-forms/publishing-unpublishing-forms.html?lang=zh-Hant)下載。

如需進一步資訊，請參閱[製作最適化表單簡介](/help/forms/using/introduction-forms-authoring.md)中的最佳實務。

## 撰寫調適型表單 {#author-adaptive-forms}

### 使用觸控最佳化的UI進行製作 {#using-touch-optimized-ui-for-authoring}

* 使用側邊欄中的物件瀏覽器，快速存取表單階層中下方的欄位。 您可以使用搜尋方塊來搜尋表單或物件樹中的物件，以便從一個物件瀏覽至另一個物件。
* 若要在側邊欄的元件瀏覽器中檢視和編輯元件的屬性，請選取該元件，然後按一下![cmppr-1](assets/cmppr-1.png)。 您也可以連按兩下元件，以在屬性瀏覽器中檢視其屬性。
* 使用鍵盤快速鍵對您的表單執行快速動作。 請參閱[AEM Forms鍵盤快速鍵](/help/forms/using/keyboard-shortcuts.md)。

* 建議僅將最適化表單元件用於最適化表單頁面。 元件與其父項階層具有相依性。 因此，請勿在AEM頁面中使用這些引數。

另請參閱[製作最適化表單簡介](/help/forms/using/introduction-forms-authoring.md)中的元件說明和最佳實務。

### 在最適化表單中使用規則 {#using-rules-in-adaptive-forms}

AEM Forms提供[規則編輯器](/help/forms/using/rule-editor.md)，可讓您建立規則以將動態行為新增至最適化表單元件。 使用這些規則，您可以評估條件並在元件上觸發動作，例如顯示或隱藏欄位、計算值、動態變更下拉式清單等。

規則編輯器提供用於編寫規則的視覺化編輯器和程式碼編輯器。 使用程式碼編輯器模式撰寫規則時，請考量下列事項：

* 針對表單欄位和元件使用有意義且唯一的名稱，以避免在撰寫規則時可能發生任何衝突。
* 對元件使用`this`運運算元，以在規則運算式中參照自身。 這可確保即使元件名稱變更，規則仍保持有效。 例如，`field1.valueCommit script: this.value > 10`。

* 參照其他表單元件時使用元件名稱。 使用`value`屬性來擷取欄位或元件的值。 例如，`field1.value`。

* 按相對唯一階層參照元件，以避免任何衝突。 例如，`parentName.fieldName`。

* 處理複雜或常用的規則時，請考慮將商業邏輯寫入個別的使用者端程式庫中，以便您指定並在適用性表單中重複使用。 使用者端程式庫應為獨立程式庫，且不應有任何外部相依性，jQuery和Underscore.js除外。 您也可以使用使用者端程式庫來強制執行[伺服器端重新驗證](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form)提交的表單資料。
* 調適型表單提供了一組API，您可以使用這些API與調適型表單通訊及執行動作。 部分重要API如下。 如需詳細資訊，請參閱最適化Forms的[JavaScript資料庫API參考](https://adobe.com/go/learn_aemforms_documentation_63)。

   * `guideBridge.reset()`：重設表單。
   * `guideBridge.submit()`：提交表單。
   * `guideBridge.setFocus(somExp, focusOption, runCompletionExp)`：將焦點設定為欄位。
   * `guideBridge.validate(errorList, somExpression, focus)`：驗證表單。
   * `guideBridge.getDataXML(options)`：以XML格式取得表單資料。
   * `guideBridge.resolveNode(somExpression)`：取得表單物件。
   * `guideBridge.setProperty(somList, propertyName, valueList)`：設定表單物件的屬性。
   * 此外，您可以使用以下欄位屬性：

      * `field.value`以變更欄位的值。
      * `field.enabled`以啟用/停用欄位。
      * `field.visible`以變更欄位的可見度。

* 最適化表單作者可能需要撰寫JavaScript程式碼，才能在表單中建置商業邏輯。 雖然JavaScript功能強大且有效，但可能會影響安全性預期。 因此，您必須確保表單作者是受信任的角色，而且在表單投入生產之前，有程式可檢閱和核准JavaScript程式碼。 管理員可以根據使用者群組的角色或功能，限制使用者群組對規則編輯器存取權的存取權。 請參閱[將規則編輯器存取權授與選取的使用者群組](/help/forms/using/rule-editor-access-user-groups.md)。
* 您可以在規則中使用運算式，讓調適型表單成為動態表單。 所有運算式都是有效的JavaScript運算式，並使用適用性表單指令碼模型API。 這些運算式會傳回某些型別的值。 如需運算式和相關最佳實務的詳細資訊，請參閱[最適化表單運算式](/help/forms/using/adaptive-form-expressions.md)。

* 使用規則編輯器建立規則時，Adobe建議使用JavaScript同步作業，而非非同步作業。 強烈建議不要使用非同步操作。 不過，如果您發現自己無法避免非同步操作，實施JavaScript關閉函式就十分重要。 如此一來，您便可針對任何可能的競爭條件有效進行保護，確保您的規則實作可提供最佳效能並維持整體的穩定性。

  例如，假設我們需要從外部API擷取資料，然後根據該資料套用一些規則。 我們使用關閉來處理非同步API呼叫，並確保在擷取資料後套用規則。 以下是範常式式碼：

  ```JavaScript
       function fetchDataFromAPI(apiEndpoint, callback) {
        // Simulate asynchronous API call with setTimeout
        setTimeout(() => {
          // Assuming the API call is successful, we receive some data
          const data = {
            someValue: 42,
          };
          // Invoke the callback with the fetched data
          callback(data);
        }, 2000); // Simulate a 2-second delay for the API call
      }
      // Rule implementation using Closure
      function ruleImplementation(apiEndpoint) {
        // Using a closure to handle the asynchronous API call and rule application
        // say you have set this value in street field inside address panel
        var streetField = address.street;
        fetchDataFromAPI(apiEndpoint, (data) => {
          streetField.value = data.someValue;
        });
      }
      // Example usage of the rule implementation
      const apiEndpoint = "https://example-api.com/data";
      ruleImplementation(apiEndpoint);
  ```

  在此範例中，`fetchDataFromAPI`使用`setTimeout`模擬非同步API呼叫。 擷取資料後，它會叫用提供的回呼函式，這是處理後續規則應用程式的關閉。 `ruleImplementation`函式包含規則邏輯。


### 使用主題 {#working-with-themes}

主題適用性可讓您建立可重複使用的樣式，這些樣式可套用至各個表單，以獲得一致的外觀和樣式。 使用主題來定義表單元件和面板的樣式。 主題相關的最佳實務如下：

* 使用資產庫快速應用文字樣式、背景和影像。 將樣式新增至資產庫時，該樣式便可用於其他主題及表單編輯器的樣式模式。
* 使用頁面層級選取器套用字型和頁面背景等全域設定。
* 使用使用者端資料庫將現有或進階樣式匯入您的主題。
* 您可以覆寫表單樣式圖層中特定欄位、面板或按鈕的樣式。
* 如果主題不符合您的樣式需求，您可以使用預先定義的類別（例如guideFieldNode、guideFieldLabel、guideFieldWidget和guidePanelNode）來套用表單上的通用樣式。

如需詳細資訊，請參閱[主題](/help/forms/using/themes.md)。

### 最佳化大型與複雜表單的效能 {#optimizing-performance-of-large-and-complex-forms}

表單作者和一般使用者在製作模式或執行階段載入大型表單時，通常面臨效能問題。 隨著表單中物件（欄位和面板）的數目增加，編寫和執行階段體驗開始降低。 它還可防止多位作者同時共同作業及撰寫表單。

請考慮下列最佳實務，以克服大型表單的效能問題：

* 建議使用XSD表單資料模型建立調適型表單，即便在可能的情況下將XFA轉換為調適型表單時也是如此。
* 僅包含最適化表單中從使用者擷取資訊的欄位和面板。 請考慮將靜態內容維持在最小值，或使用URL在個別視窗中開啟。
* 雖然每個表單都是為特定目的而設計，但在大多數表單中都有一些常見的區段。 例如，個人詳細資料、地址、僱用詳細資料等。 為通用表單元素和區段建立[最適化表單片段](/help/forms/using/adaptive-form-fragments.md)，並在各個表單中使用它們。 您也可以將現有表單中的面板儲存為片段。 片段中的任何變更會反映在所有關聯的調適型表單中。 它促進了合作創作，因為多位作者可以同時處理構成表單的不同片段。

   * 請考慮在表單製作期間為不可重複使用的區段建立表單片段。 隨著表單的大小和複雜度增加，將其細分為片段可大幅簡化編寫流程，並讓表單更易於維護。 此方法可讓您專注在較小且更容易管理的表單上，而非一次處理整個表單。
   * 與調適型表單類似，建議使用片段容器對話方塊，在使用者端資料庫中定義所有片段特定的樣式和自訂指令碼。 此外，請嘗試建立不依賴外部物件的自給自足片段。
   * 避免使用跨片段指令碼。 如果片段外有任何您必須參照的物件，請嘗試將該物件設為父表單的一部分。 如果物件仍必須位於另一個片段中，請在指令碼中依其名稱參照。

* 使用自動儲存並恢復以定期儲存最適化表單，並讓使用者稍後重新造訪以完成表單。
* 設定片段以緩慢載入。 在執行階段，只有在需要標籤為延遲載入的片段時，才會轉譯。 它大幅縮短大型表單的載入時間。 具有可重複面板的片段也支援此功能。 如需詳細資訊，請參閱[設定延遲載入](/help/forms/using/lazy-loading-adaptive-forms.md)。

   * 請勿在回應式格線配置或第一個面板中，設定片段上的延遲載入。
   * 延遲載入的片段不支援檔案附件和條款與條件元件。
   * 如果延遲載入面板中的某個值用於表單的其他部分，請將該值標示為「全域使用值」，以便在解除安裝包含面板時使用該值。
   * 請考慮為應根據條件顯示或隱藏的片段寫入可見性規則。
* 將&#x200B;**Apache Sling主要Servlet**&#x200B;中每個請求&#x200B;**的**&#x200B;呼叫數的值設定為相當大的數字。 這可讓Forms伺服器允許其他呼叫。 組態顯示預設值1500。 值1500呼叫適用於其他Experience Manager元件，例如Sites和Assets。 調適型表單的預設值集為20000。 如果您在記錄中遇到`too many calls`錯誤或表單無法轉譯，請嘗試將值增加到較大的數字來解決問題。 如果呼叫數超過20000，表示表單很複雜，可能需要一些時間才能在瀏覽器中呈現表單。 這僅發生在首次載入表單時，之後會快取表單，而且快取表單後，對效能沒有重大影響。

### DOM大小考量事項和瀏覽器效能

建立大型且複雜的調適型表單時，請務必考慮DOM大小對轉譯和效能的影響：

* **DOM大小影響**：雖然AEM Forms沒有DOM大小的硬性限制，但過量的DOM大小可能會顯著影響效能，尤其是處理延遲載入的片段時。 大型DOM結構需要更多記憶體和處理時間才能呈現和操作。

* **瀏覽器轉譯差異**：轉譯效能在不同的瀏覽器和裝置上可能會有很大的差異。 有些瀏覽器轉譯引擎處理動態DOM更新的方式不同，在樣式重新計算、重新排列和重新繪製方面有不同的方式。 這在動態載入的大型內容中特別明顯。 在某些瀏覽器中，每一次重大的DOM操作都可能觸發頁面的完整版面重新計算及重繪，而加劇大型或複雜表單的效能問題。

* **效能因素**：有幾個因素會影響延遲載入效能：
   * 片段的大小和複雜性
   * 套用至元素的CSS樣式
   * 動態更新觸發的重新整理次數
   * 裝置和瀏覽器功能

* **真實世界影響**：在觀察到的案例中，DOM大小約400 KB的表單在某些瀏覽器上經歷了最多15秒的重大演算延遲。 這些延遲不僅是因為片段大小，也因為在動態內容插入期間觸發了CSS處理和頁面重新整理。

**管理DOM大小的最佳實務：**

* 針對靜態內容，請考慮使用AEM內容片段，而非透過延遲載入來動態插入大型HTML區塊。 此方法可減少重新排程、重繪和JavaScript執行時間，進而改善整體頁面載入效能。

* 當片段必須是動態且延遲載入時，請將大型片段分割為更小、更易於管理的片段，並視需要僅載入所需區段。

* 在適當時實施漸進式揭露模式，僅在根據使用者輸入需要時揭露其他表單欄位。

* 跨多個瀏覽器和裝置測試您的表單，尤其是使用延遲載入片段時，以確保跨不同環境的一致效能。

* 監控及最佳化表單中使用的CSS，因為廣泛或結構不良的CSS可大幅增加轉譯時間，尤其是在動態內容更新期間。

如需不同瀏覽器轉譯引擎如何處理DOM更新、重新排列和重繪的更多技術細節，請考慮探索瀏覽器引擎檔案，例如不同瀏覽器廠商提供的檔案。

### 預先填寫最適化表單 {#prefilling-adaptive-forms}

您可使用從後端擷取的資料預先填寫最適化表單欄位，以協助使用者快速填寫表單並避免輸入錯誤。

* AEM Forms提供預填服務，用於從預先定義的資料XML檔案讀取資料，並使用預填XML檔案中的內容預填調適型表單的欄位。
* 預填資料XML必須符合與調適型表單關聯的表單模型結構描述。
* 在預填XML中包含`afBoundedData`和`afUnBoundedData`區段，以預填最適化表單中的繫結和未繫結欄位。

* 針對以表單資料模型為基礎的最適化表單，AEM Forms提供立即可用的表單資料模型預填服務。 預填服務會查詢最適化表單中資料模型物件的資料來源，並在呈現表單時預填欄位值。
* 您也可以使用檔案、crx、服務或http通訊協定預先填寫最適化表單。
* AEM Forms支援自訂預填服務，您可以OSGi服務形式插入這些服務，以預填調適型表單。

如需詳細資訊，請參閱[預填最適化表單欄位](/help/forms/using/prepopulate-adaptive-form-fields.md)。

### 簽署及提交最適化表單 {#signing-and-submitting-adaptive-forms}

調適型表單需要提交動作來處理使用者指定的資料。 提交動作會決定使用最適化表單提交之資料所執行的工作。

* 適用性表單中有數個現成可用的提交動作。 如需詳細資訊，請參閱[設定提交動作](/help/forms/using/configuring-submit-actions.md)。
* 如果預設提交動作不符合您的使用案例，您可以編寫自訂提交動作。 如需詳細資訊，請參閱[撰寫最適化表單的自訂提交動作](/help/forms/using/custom-submit-action-form.md)。
* 包含伺服器端驗證，以防止提交無效的資料。

您可以在調適型表單中使用Adobe Sign的多重簽署體驗。 設定最適化表單中的Adobe Sign時，請考量下列事項。 如需詳細資訊，請參閱[在最適化表單中使用Adobe Sign](/help/forms/using/working-with-adobe-sign.md)。

* 啟用Adobe Sign的最適化表單只會在所有簽署者簽署表單後提交。 Forms會一直顯示於等待簽署狀態，直到所有簽署者簽署表單為止。
* 您可以設定表格中的簽名體驗，或在提交時將簽署者重新導向至簽名頁面。
* 視需要設定循序或平行簽署體驗。

### 正在產生記錄檔案 {#generating-document-of-record}

記錄檔案(DoR)是一種最適化表單的平面化PDF版本，您可以列印、簽署或封存。

* 根據最適化表單所依據的表單資料模型，您可以為DoR設定範本，如下所示：

   * **XFA表單範本**：使用關聯的XDP檔案做為DoR範本。
   * **XSD結構描述**：使用與適用性表單使用相同XML結構描述的相關聯XFA範本。
   * **無**：使用自動產生的DoR。

* 從最適化表單編輯器的「記錄檔案」索引標籤設定頁首、頁尾、影像、顏色、字型等。
* 使用`DoRService`以程式設計方式產生記錄檔案。
* 從DoR排除隱藏欄位。
* 使用`afAcceptLang`要求引數檢視其他地區設定中的DoR。

### 偵錯和測試調適型表單 {#debugging-and-testing-adaptive-forms}

[AEM Chrome外掛程式](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/)是Google Chrome的瀏覽器擴充功能，提供除錯最適化表單的工具。 表單作者和開發人員可使用這些工具來：

* 找出瓶頸並最佳化表單轉譯效能
* 表單中的偵錯關鍵字和bindRef錯誤
* 啟用和設定記錄檔
* 表單中的除錯規則和指令碼
* 探索和瞭解guideBridge API

如需詳細資訊，請參閱[AEM Chrome外掛程式 — 最適化表單](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/adaptive-form/)。

### 在AEM伺服器上驗證調適型表單 {#validating-adaptive-forms-on-aem-server}

需要伺服器端驗證，以防止任何在使用者端上繞過驗證的嘗試，以及資料提交和業務規則違規的任何可能危害。 伺服器端驗證會透過載入所需的使用者端程式庫在伺服器上執行。

* 將函式包含在使用者端程式庫中，以驗證最適化表單中的運算式，並在最適化表單容器對話方塊中指定使用者端程式庫。 如需詳細資訊，請參閱[伺服器端重新驗證](/help/forms/using/configuring-submit-actions.md#p-server-side-revalidation-in-adaptive-form-p)。
* 伺服器端驗證會驗證表單模型。建議您建立個別的使用者端程式庫進行驗證，不要將其與相同使用者端程式庫中的HTML樣式和DOM操作等其他專案混合。

### 將調適型表單當地語系化 {#localizing-adaptive-forms}

AEM提供翻譯工作流程，您可用來將最適化表單當地語系化。 如需詳細資訊，請參閱[使用AEM翻譯工作流程將最適化表單當地語系化](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md)。

將調適型表單當地語系化的一些最佳實務如下：

* 針對各表單的共同元素使用最適化表單片段，並將片段本地化。 它可確保您將片段本地化一次，並反映在使用本地化片段的所有表單中。
* 任何修改，例如新增元件或以當地語系化表單套用指令碼，都不會自動當地語系化。 因此，您必須先完成表單，再進行當地語系化，以避免多個本地化週期。
* 使用`afAcceptLang`要求引數覆寫瀏覽器地區設定並以指定的地區設定轉譯表單。 例如，無論瀏覽器設定中指定的地區設定為何，下列URL都會強制以日文地區設定轉譯表單：

  `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

* AEM Forms目前支援英文(en)、西班牙文(es)、法文(fr)、義大利文(it)、德文(de)、日文(ja)、葡萄牙文 — 巴西(pt-BR)、中文(zh-CN)、中文 — 台灣(zh-TW)和韓文(ko-KR)本地化內容。 不過，您可在執行階段為最適化表單新增地區設定的支援。 如需詳細資訊，請參閱[支援最適化表單本地化的新地區設定](/help/forms/using/supporting-new-language-localization.md)。

## 準備表單專案以供生產 {#prepare-forms-project-for-production}

### 新增表單處理伺服器 {#adding-forms-processing-server}

您可以另外設定一個AEM Forms伺服器執行個體，常駐於安全區域的防火牆之後。 您可以將此執行個體用於：

* **批次處理**：重複產生或排程的作業，批次中有大量負載。 例如，列印陳述式、產生對應，以及使用PDF Generator、Output和Assembler等檔案服務。
* **儲存PII資料**：將PII資料儲存在處理伺服器上。 如果您已使用自訂儲存提供者來儲存PII資料，則不需要使用。

### 將專案移動到另一個環境 {#moving-project-to-another-environment}

您經常需要將AEM專案從一個環境移動到另一個環境。 移動時要記住的一些關鍵事項如下：

* 備份您現有的使用者端程式庫、自訂程式碼和設定。
* 在新環境中以指定的順序手動部署產品套件和修補程式。
* 手動部署專案特定的程式碼套件和套件組合，並作為單獨的套件或套件組合部署在新的AEM伺服器上。
* (*僅限JEE上的AEM Forms*)在Forms Workflow伺服器上手動部署LCA和DSC。
* 使用[匯出 — 匯入](/help/forms/using/import-export-forms-templates.md)功能將資產移至新環境。 您也可以設定復寫代理程式並發佈資產。
* 升級時，請以新的API和功能取代所有已棄用的API和功能。

### 設定AEM {#configuring-aem}

設定AEM以改善整體效能的一些最佳實務如下：

* 從Felix主控台啟用適用於JavaScript和CSS的HTML使用者端程式庫壓縮。
* 快取`/etc.clientlibs/fd`的所有使用者端資料庫，以及AEM Dispatcher上的任何其他自訂使用者端資料庫，以提高您發佈表單的回應速度與安全性。 如需詳細資訊，請參閱[Dispatcher](https://helpx.adobe.com/tw/experience-manager/dispatcher/using/dispatcher.html)。

* 不要快取`/content/forms/af/`和`/content/dam/formsanddocuments/*`路徑。 如需設定最適化表單快取的詳細資訊，請參閱[快取最適化表單](/help/forms/using/configure-adaptive-forms-cache.md)。

* 透過網頁伺服器壓縮模組啟用HTML。 如需詳細資訊，請參閱[AEM Forms伺服器的效能調整](/help/forms/using/performance-tuning-aem-forms.md)。
* 針對大型表單，增加每個請求設定的呼叫。 請參閱[最佳化大型與複雜表單的效能](/help/forms/using/adaptive-forms-best-practices.md#optimizing-performance-of-large-and-complex-forms)。
* 建立錯誤處理常式[&#128279;](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/customizing-errorhandler-pages.html?lang=zh-Hant)顯示的自訂錯誤頁面。
* 安全的AEM Forms伺服器。

   * 使用`nosamplecontent`執行模式，確保生產伺服器上未部署範例內容和範例使用者。 請參閱[在生產就緒模式下執行AEM](/help/sites-administering/production-ready.md)。

* 將棧積大小維持在最小8 GB。 如需其他設定，請參閱[AEM Forms伺服器的效能調整](/help/forms/using/performance-tuning-aem-forms.md)。
* 使用服務使用者工作階段而非管理工作階段來執行服務層級工作。 如需詳細資訊，請參閱[服務驗證](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html)。

>[!VIDEO](https://vimeo.com/)

### 為草稿和提交的表單資料設定外部儲存空間 {#external-storage}

在生產環境中，建議不要將提交的表單資料儲存在AEM存放庫中。 Forms入口網站商店、商店內容和商店PDF提交動作的預設實施，會將表單資料儲存在AEM存放庫中。 這些提交動作僅供示範之用。 此外，「儲存並繼續」和「自動儲存」功能預設會使用入口網站儲存空間。 因此，請考慮下列建議：

* **儲存草稿資料**：如果您使用最適化表單的草稿功能，您應該實作自訂服務提供介面(SPI)，以將草稿資料儲存在更安全的儲存空間，例如資料庫。 如需詳細資訊，請參閱[將草稿與提交元件與資料庫整合的範例](/help/forms/using/integrate-draft-submission-database.md)。

* **儲存提交資料**：如果您使用表單入口網站提交存放區，您應該實作自訂SPI，以將提交資料儲存在資料庫中。 如需範例整合，請參閱[整合草稿與提交元件與資料庫](/help/forms/using/integrate-draft-submission-database.md)的範例。

  您也可以撰寫自訂提交動作，將表單資料和附件儲存在安全的儲存空間中。 如需詳細資訊，請參閱[撰寫最適化表單的自訂提交動作](/help/forms/using/custom-submit-action-form.md)。

* **草稿ID的長度**：將最適化表單儲存為草稿時，會產生草稿ID以唯一識別草稿。 草稿ID欄位長度的最小值為26個字元。 Adobe建議將草稿ID長度設為26個或更多字元。

### 處理個人識別資訊 {#handling-personally-identifiable-information}

組織面臨的主要挑戰之一是如何處理個人識別(PII)資料。 以下為可協助您處理此類資料的一些最佳實務：

* 使用安全的外部儲存空間（如資料庫），儲存草稿和已提交表單的資料。 請參閱[為草稿和已提交的表單資料設定外部儲存空間](/help/forms/using/adaptive-forms-best-practices.md#external-storage)。
* 在啟用自動儲存之前，使用條款與條件表單元件取得使用者的明確同意。 在此情況下，只有當使用者同意條款與條件元件中的條件時，才會啟用自動儲存。

## 選擇最適化表單的規則編輯器、代碼編輯器或自訂使用者端程式庫 {#RuleEditor-CodeEditor-ClientLibs}

### 規則編輯器 {#rule-editor}

<!--The AEM Forms Rule Editor offers predefined functions for defining rules in adaptive forms without extensive programming. It facilitates the implementation of conditional logic, data validation, and integration with external sources. This visual interface is especially valuable for business users and form designers, enabling them to create dynamic and complex rules with ease, here we discusss few use cases where rule editor allows you to:-->

AEM Forms規則編輯器提供建立和管理規則的視覺介面，減少大量編碼的需求。 對於可能沒有進階程式設計技能，但需要在表單中定義及維護商業規則的商務使用者或表單設計人員而言，此功能特別實用。這裡我們將討論一些使用案例，規則編輯器可讓您：

* &#x200B;<!-- Allows you --> 為您的表單定義商業規則，而不需要大量的程式設計。
* &#x200B;<!-- Use the Rule Editor when you need --> 若要在表單中實作條件式邏輯。 這包括顯示或隱藏表單元素、根據特定條件變更欄位值，或動態變更表單的行為。
* &#x200B;<!--When you want --> 若要對表單提交強制執行資料驗證規則，可使用規則編輯器來定義驗證條件。
* &#x200B;<!-- When you need --> 若要將表單與外部資料來源(FDM)或服務整合，規則編輯器可協助定義在表單互動期間擷取、顯示或操控資料的規則。
* &#x200B;<!-- If you want -->若要建立回應使用者動作的動態與互動式表單，規則編輯器可讓您定義規則以即時控制表單元素的行為。

規則編輯器適用於AEM Forms Foundation元件和核心元件。

### 程式碼編輯器 {#code-editor}

程式碼編輯器是Adobe Experience Manager (AEM) Forms中的工具，可讓您為表單中更複雜和進階的功能撰寫自訂指令碼和程式碼，以下我們將討論幾個使用案例：

* 當您需要實作超出AEM Forms規則編輯器功能的自訂使用者端邏輯或行為時。 程式碼編輯器可讓您撰寫JavaScript程式碼，以處理複雜的互動、計算或驗證。
* 如果您的表單需要伺服器端處理或與外部系統整合，您可以使用程式碼編輯器來撰寫自訂伺服器端指令碼。 您可以在程式碼編輯器中存取guideBridge API，以在表單事件和物件上實作任何複雜的邏輯。
* 當您需要超過AEM Forms元件標準功能的高度自訂使用者介面時，程式碼編輯器可讓您實施自訂樣式、行為，或甚至建立自訂表單元件。
* 如果您的表單涉及非同步作業（例如非同步資料載入），您可以使用程式碼編輯器透過自訂的非同步JavaScript程式碼管理這些作業。

請務必注意，使用程式碼編輯器需要充分瞭解JavaScript和AEM Forms架構。 此外，在實作自訂程式碼時，請確保您遵循最佳實務、遵守安全性方針，並徹底測試您的程式碼以防止生產環境中的潛在問題。 您可以使用程式碼編輯器為FDM實施回呼。

程式碼編輯器僅適用於AEM Forms Foundation元件。 對於最適化表單核心元件，您可以使用自訂函式來建立您自己的表單規則，如下節所述。

### 自訂函式 {#custom-client-libs}

在各種情況下，在AEM Forms (Adobe Experience Manager Forms)中使用自訂使用者端資料庫有助於增強表單的功能、樣式或行為。 以下是一些可能適合使用自訂使用者端程式庫的情況：

* 如果您的表單需要實作獨特的設計或品牌，且超過AEM Forms提供的預設樣式選項的功能，您可以選擇建立自訂使用者端資料庫來控制外觀。
* 當您需要自訂使用者端邏輯時，多個表單或行為中的方法無法透過標準AEM Forms功能達到可重複使用性。 這可能包括動態表單互動、自訂驗證，或與協力廠商程式庫的整合。
* 透過最佳化及精簡使用者端資源來改善表單效能。 自訂使用者端程式庫可用來打包和壓縮JavaScript和CSS檔案，減少整體的頁面載入時間。
* 當您需要整合預設JavaScript設定中未包含的其他AEM Forms程式庫或架構時。 這可能是增強型日期選擇器、圖表或其他互動式元件等功能的必要專案。

在決定使用自訂使用者端程式庫之前，請務必考量維護負荷、與未來更新的潛在衝突，以及是否遵守最佳實務。 確保您的自訂內容都經過妥善記錄和測試，以避免在升級期間或與其他開發人員合作時發生問題。

>[!NOTE]
> 自訂函式適用於AEM Forms基礎元件和核心元件。

**自訂函式的優點：**

**自訂函式**&#x200B;比&#x200B;**程式碼編輯器**&#x200B;更具有顯著的優勢，因為它在內容與程式碼之間提供了清晰的區隔，可加強協同合作並簡化工作流程。 建議您使用自訂函式，以獲得下列優點：

* **順暢地使用版本控制項，例如Git：**
   * 從內容中隔離程式碼可大幅減少內容管理期間的Git衝突，並提升妥善組織的存放庫。
   * 自訂函式對於有多位貢獻者同時運作的專案而言非常有用。

* **技術優點：**
   * 自訂函式提供模組化和封裝。
   * 模組可以獨立開發、測試和維護。
   * 增強程式碼的可重複使用性和可維護性。

* **有效的開發程式：**
   * 模組化可讓開發人員專注於特定功能。
   * 降低整個程式碼基底的複雜性，以提升開發流程的效率，進而減輕開發人員的負擔。



