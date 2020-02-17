---
title: 最適化表單運算式
seo-title: 最適化表單運算式
description: 使用最適化表單運算式來新增自動驗證、計算，並開啟或關閉區段的可見性。
seo-description: 使用最適化表單運算式來新增自動驗證、計算，並開啟或關閉區段的可見性。
uuid: c274dce5-8b87-472f-bff5-53b246fa6584
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 2fd2276e-cfe3-47ad-94c1-9c7af56b7a17
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# 最適化表單運算式{#adaptive-form-expressions}

最適化表單提供最佳化和簡化的表單填寫體驗，讓使用者能使用動態指令碼功能。 它可讓您編寫運算式，以新增各種行為，例如動態顯示／隱藏欄位和面板。 它也可讓您新增計算欄位、讓欄位變成唯讀、新增驗證邏輯等。 動態行為是以使用者輸入或預先填入的資料為基礎。

JavaScript是最適化表單的運算式語言。 所有運算式都是有效的JavaScript運算式，並使用最適化表單指令碼模型API。 這些運算式會傳回特定類型的值。 如需最適化表單類別、事件、物件和公用API的完整清單，請參閱適 [化表單的JavaScript程式庫API參考](https://helpx.adobe.com/aem-forms/6/javascript-api/index.html)。

## 編寫陳述式的最佳範例 {#best-practices-for-writing-expressions}

* 在編寫運算式時，若要存取欄位和面板，您可以使用欄位或面板的名稱。 若要存取欄位的值，請使用value屬性。 例如， `field1.value`
* 在表單中使用欄位和面板的唯一名稱。 它有助於避免與寫入運算式時使用的欄位名稱產生任何衝突。
* 在編寫多行表達式時，使用分號來終止語句。

## 包含重複面板之運算式的最佳範例 {#best-practices-for-expressions-involving-repeating-panel}

重複面板是使用指令碼API或預先填入資料動態新增或移除面板的例項。 如需使用重複面板的詳細資訊，請參 [閱建立具有重複區段的表單](/help/forms/using/creating-forms-repeatable-sections.md)。

* 若要建立重複面板，請在面板對話方塊中開啟設定，並將最大計數欄位的值設定為超過1。
* 面板重複設定的最小計數值可以是一或多個，但不能超過最大計數值。
* 當運算式引用重複面板的欄位時，運算式中的欄位名稱會解析為最接近的重複元素。
* 最適化表單提供一些特殊功能，可簡化可重複面板的計算，例如總計、計數、最小值、最大值、篩選器等。 如需完整的函式清單，請參閱適 [應性表單的JavaScript程式庫API參考](https://helpx.adobe.com/aem-forms/6/javascript-api/af.html)
* 用於控制重複面板實例的API包括：

   * 若要新增面板例項： `panel1.instanceManager.addInstance()`
   * 若要取得面板重複索引： `panel1.instanceIndex`
   * 若要取得面板的instanceManager: `_panel1 or panel1.instanceManager`
   * 要刪除面板實例： `_panel1.removeInstance(panel1.instanceIndex)`

## 運算式類型 {#expression-types}

在最適化表單中，您可以編寫運算式來新增動態顯示／隱藏欄位和面板等行為。 您也可以編寫運算式來新增計算欄位、讓欄位變成唯讀、驗證邏輯等。 最適化表單支援下列運算式：

* **[存取運算式](../../forms/using/adaptive-form-expressions.md#main-pars-header-4)**:啟用／停用欄位。
* **[計算表達式](../../forms/using/adaptive-form-expressions.md#p-calculate-expression-p)**:自動計算欄位的值。
* **[按一下運算式](../../forms/using/adaptive-form-expressions.md#p-click-expression-p)**:來處理按鈕的按一下事件上的操作。
* **[](../../forms/using/adaptive-form-expressions.md#p-initialization-script-p)初始化指令碼&#x200B;**:對欄位的初始化執行操作。
* **[選項運算式](../../forms/using/adaptive-form-expressions.md#p-options-expression-p)**:以動態填寫下拉式清單。
* **[摘要運算式](#summary)**:動態計算accordion的標題。
* **[驗證運算式](../../forms/using/adaptive-form-expressions.md#p-validate-expression-p)**:來驗證欄位。
* **[](../../forms/using/adaptive-form-expressions.md#p-value-commit-script-p)值提交指令碼&#x200B;**:變更欄位值後的表單元件。
* **[可見度運算式](../../forms/using/adaptive-form-expressions.md#p-visibility-expression-p)**:以控制欄位和面板的可見度。
* **[步驟完成運算式](../../forms/using/adaptive-form-expressions.md#p-step-completion-expression-p)**:以防止使用者進入精靈的下一步。

### 存取運算式（啟用運算式） {#access-expression-enablement-expression}

您可以使用存取運算式來啟用或停用欄位。 如果表達式使用欄位的值，則每當欄位的值更改時，都會檢索表達式。

**適用於**:欄位

**退貨類型**:運算式會傳回布林值，代表欄位是啟用還是停用。 **true** 代表欄位已啟用， **false** 代表欄位已停用。

**範例**:若要僅在欄位1的值設 **置為****X**&#x200B;時啟用欄位，訪問表達式為： `field1.value == "X"`

### 計算表達式 {#calculate-expression}

計算表達式用於使用表達式自動計算欄位的值。 通常，此表達式使用其他欄位的值屬性。 例如， `field2.value + field3.value`。 每當或的值 `field2`變 `field3`更時，都會檢索表達式並重新計算值。

**適用於**:欄位

**退貨類型**:運算式會傳回與顯示運算式結果的欄位相容的值（例如小數）。

**範例**:顯示欄位1中兩個欄位之和的計 **算表達式** 為：
`field2.value + field3.value`

### 按一下運算式 {#click-expression}

點按運算式可處理對按鈕點按事件所執行的動作。 GuideBridge現成可提供API來執行各種功能，例如提交、驗證與點按運算式一起使用。 如需API的完整清單，請參 [閱GuideBridge API](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html)。

**適用於**:按鈕欄位

**退貨類型**:點按運算式不會傳回任何值。 如果任何運算式傳回值，則會忽略該值。

**範例**:若要在按鈕的點 **按動作上填入文字方塊文字方塊1** ，請使用值 **AEM Forms**，按鈕的點按運算式為 `textbox1.value="AEM Forms"`

### 初始化指令碼 {#initialization-script}

初始化指令碼在初始化自適應表單時觸發。 初始化指令碼的行為方式取決於方案：

* 當在沒有資料預填的情況下呈現自適應表單時，初始化指令碼會在表單初始化後執行。
* 當以資料預填呈現最適化表格時，指令碼會在預填寫作業完成後執行。
* 當觸發自適應表單的伺服器側重驗證時，執行初始化指令碼。

**** 適用於：欄位和面板

**** 退貨類型：初始化指令碼表達式不返回任何值。 如果任何運算式傳回值，則會忽略該值。

**** 範例：在資料預先填入藍本中，若要在欄位的值儲存為 `'Adaptive Forms'` null時，將預設值填入欄位，初始化指令碼運算式為：
`if(this.value==null) this.value='Adaptive Forms';`

### 選項運算式 {#options-expression}

選項運算式可用來動態填入下拉式清單欄位的選項。

**適用於**:下拉式清單欄位

**退貨類型**:選項表達式返回字串值的陣列。 每個值都可以是簡單的字串，例如 **Male**，或是key=value對格式，例如 **1=Male**

**範例**:要根據另一個欄位的值填充欄位的值，請提供一個簡單的選項表達式。 例如，若要根據在另一欄位中 **表示的「婚姻狀態**」填入一個欄位Number of Kids **** ，其運算式為：

**`marital_status.value == "married" ? ["1=One", "2=two"] : ["0=Zero"]`.**

每當furnime_status欄 **位的值變更時** ，就會擷取運算式。 您也可以從REST服務填入下拉式清單。 如需詳細資訊，請參 [閱動態填入下拉式清單](../../forms/using/dynamically-populate-dropdowns.md)。

### 摘要運算式 {#summary}

「摘要」運算式會動態計算accordion版面面板的子面板標題。 您可以在規則中指定「摘要」運算式，該運算式會使用表單欄位或自訂邏輯來評估標題。 表單初始化時，表達式將執行。 如果要預填充表單，則表達式在預填充資料後或表達式中使用的從屬欄位的值更改後執行。

「摘要」運算式通常用於重複accordion版面面板的子系，以便為每個子系面板提供有意義的標題。

**** 適用於：面板是面板的直接子系，其版面配置為Accordion。

**** 退貨類型：運算式會傳回成為accordion標題的字串。

**** 範例：&quot;帳號：&quot;+ textbox1.value

### 驗證運算式 {#validate-expression}

validate運算式可用來使用指定運算式來驗證欄位。 通常，這些運算式會使用規則運算式與欄位值來驗證欄位。 將檢索表達式，並根據欄位值的任何變化重新計算欄位的驗證狀態。

**適用於**:欄位

**退貨類型**:運算式會傳回布林值，代表欄位的驗證狀態。 值 **false** 表示欄位無效， **true** 表示欄位有效。
**範例**:對於代表英國郵遞區號的欄位，驗證運算式為：

(**this.value** &amp;&amp; `this.value.match(/^(GIR 0AA|[A-Z]{1,2}\d[A-Z0-9]? ?[0-9][A-Z]{2}\s*)$/i) == null) ? false : true`

在上例中，如果非空值與模式不匹配，則表達式返回 **false** ，以指示欄位無效。

>[!NOTE]
>
>如果為非強制或強制欄位編寫驗證表達式，則無論欄位的可見性狀態如何，都會計算表達式。 要停止對隱藏欄位的驗證，請將「初始化」或「值提交指令碼」中的validationsDisabled屬性設定為true。 例如， `this.validationsDisabled=true`

### 值認可指令碼 {#value-commit-script}

Value Commit指令碼在以下情況下觸發：

* 使用者會從UI變更欄位的值。
* 欄位的值因其他欄位的更改而以程式方式更改。

**** 適用於：欄位

**** 退貨類型：值commit指令碼表達式不返回任何值。 如果任何運算式傳回值，則會忽略該值。

**** 範例：要在提交時將欄位中輸入的字母大小寫轉換為大寫，值commit表達式為：
`this.value=this.value.toUpperCase()`

>[!NOTE]
>
>當欄位的值以寫程式方式更改時，可以禁用「值提交指令碼」的執行。 若要這麼做，請前往https://[server]:[port/system/console/configMgr並將]Adaptive Forms for Compatibility **變更為****** AEM Forms 6.1。 此後，僅當用戶更改UI中欄位的值時，才執行「值提交指令碼」。

### 可見性運算式 {#visibility-expression}

「可見性」運算式可用來控制欄位／面板的可見性。 通常，可見性運算式會使用欄位的值屬性，當該值變更時就會擷取。

**適用於**:欄位和面板

**退貨類型**:運算式會傳回布林值，表示欄位／面板是否可見。 **false** 代表欄位或面板不可見，true代表欄位或面板可見。

**範例**:對於僅當field1的值設為 **Male** 時才會變為可見的面板 ****，可見性表達式為： `field1.value == "Male"`

### 步驟完成運算式 {#step-completion-expression}

步驟完成運算式可用來防止使用者進入精靈版面的下一步。 當面板具有精靈版面時，會使用這些運算式（一次顯示一個步驟的多步驟表單）。 只有當目前區段中的所有必要值都已填入且有效時，使用者才可移至下一個步驟、面板或子區段。

**適用於**:將項目版面設為精靈的面板。

**退貨類型**:運算式會傳回布林值，表示目前面板有效與否。 **True** 表示目前面板有效，使用者可導覽至下一個面板。

**範例**:在以各種面板組織的表單中，在導覽至下一個面板之前，會先驗證目前的面板。 在這種情況下，會使用步驟完成運算式。 通常，這些運算式會使用GuideBridge驗證API。 步驟完成運算式的範例為：
`window.guideBridge.validate([],this.panel.navigationContext.currentItem.somExpression)`

## 最適化表單中的驗證 {#validations-in-adaptive-form}

有多種方法可新增欄位驗證至最適化表單。 如果在欄位上新增驗證檢查， **True** 表示在欄位中輸入的值有效。 **False** 表示值無效。 如果您在欄位中或欄位外切換，則不會產生錯誤訊息。

在欄位上添加驗證的方法有：

### 必要 {#required}

要使元件成為必備元件，可在元件的「編 **輯** 」對話框中選擇選項「標題」和「文本」>「必 **要」**。 您也可以新增適當 **的必要訊息** （選用）。.

### 驗證模式 {#validation-patterns}

欄位有多個可用的現成可用驗證模式。 要選擇驗證模式，請在元件的「編 **輯** 」(Edit **)對話框中，找到「模式」(** Patterns **)部分並選**&#x200B;擇模式。 您可以在「模式」文字方塊中建立自 **訂驗證** 模式。 只有在填入的資 **料符合** 驗證模式時，才會傳回驗證狀態 **True** ，否則會傳回False。 若要編寫您自己的自訂驗證模式，請參 [閱HTML5表單的Picture子句支援](/help/forms/using/picture-clause-support.md)。

### 驗證運算式 {#validation-expressions}

您也可以使用不同欄位上的運算式來計算欄位的驗證。 這些運算式會寫入 **在元件「編輯** 」對話方塊的「指令碼 **」索引標籤的「驗證****** 指令碼」欄位中。 欄位的驗證狀態取決於表達式返回的值。 有關如何編寫此類表達式的資訊，請參 [閱驗證表達式](../../forms/using/adaptive-form-expressions.md#p-validate-expression-p)。

## 其他資訊 {#additional-information}

### 使用欄位顯示格式 {#using-field-display-format}

「顯示格式」可用來顯示不同格式的資料。 例如，您可使用顯示格式來顯示含連字型大小、郵遞區號格式或日期選擇器的電話號碼。 這些顯示陣列可從元件的「編 **輯」(Edit** )對話框的「陣列」(Patterns)部分中選取。 您可以編寫類似上述驗證模式的自訂顯示模式。

### GuideBridge - API和事件 {#guidebridge-apis-and-events}

GuideBridge是API的集合，可用來與瀏覽器記憶體模型中的最適化表單互動。 如需指南Bridge API、類別方法、公開事件的詳細簡介，請參閱適 [應性表單的JavaScript程式庫API參考](https://helpx.adobe.com/aem-forms/6/javascript-api/)。

>[!NOTE]
>
>建議不要在運算式中使用GuideBridge事件監聽器。

#### GuideBridge在各種運算式中的使用 {#guidebridge-usage-in-various-expressions}

* 若要重設表單欄位，您可以在按鈕的 `guideBridge.reset()` 點按運算式上觸發API。 同樣地，也有可以呼叫為點按運算式的送出API `guideBridge.submit()`**。**

* 您可以使用 `setFocus()` API來設定各欄位或面板的焦點（面板焦點會自動設定為第一個欄位）。 `setFocus()`提供多種導覽選項，例如跨面板導覽、先前／後次瀏覽、將焦點設定在特定欄位等。 例如，若要移至下一個面板，您可使用： `guideBridge.setFocus(this.panel.somExpression, 'nextItem').`

* 若要驗證最適化表單或其特定面板，請使用 `guideBridge.validate(errorList, somExpression).`

#### 在運算式外使用GuideBridge {#using-guidebridge-outside-expressions-nbsp}

您也可以在運算式外使用GuideBridge API。 例如，您可以使用GuideBridge API來設定裝載最適化表單的頁面HTML與表單模型之間的通訊。 此外，您也可以設定來自代管表單之Iframe父代的值。

若要針對上述範例使用GuideBridge API，請擷取GuideBridge的例項。 要捕獲實例，請監聽 `bridgeInitializeStart`對象的事 `window`件：

```
window.addEventListener("bridgeInitializeStart", function(evnt) {

     // get hold of the guideBridge object

     var gb = evnt.detail.guideBridge;

     //wait for the completion of AF

     gb.connect(function (){

        //this function will be called after Adaptive Form is initialized

     })

})
```

>[!NOTE]
>
>在AEM中，將程式碼寫入clientLib並加入您的頁面（頁面的header.jsp或footer.jsp）是一個很好的作法

若要在初始化表單後使用GuideBridge(事 `bridgeInitializeComplete` 件已調度)，請使用獲取GuideBridge實例 `window.guideBridge`。 您可以使用 `guideBride.isConnected` API檢查GuideBridge初始化狀態。

#### GuideBridge事件 {#guidebridge-events}

GuideBridge也針對代管頁面上的外部指令碼提供特定事件。 外部指令碼可以監聽這些事件並執行各種操作。 例如，每當表單中的使用者名稱變更時，頁面標題中顯示的名稱也會變更。 如需此類事件的詳細資訊，請參閱適 [應性表單的JavaScript程式庫API參考](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html)。

使用以下代碼註冊處理程式：

```
guideBridge.on("elementValueChanged", function (event, data)  {

      // execute some logic when value of a field is changed

});
```

### 建立欄位的自訂圖樣 {#creating-custom-patterns-for-a-field}

如上所述，最適化表單可讓作者提供驗證或顯示格式的模式。 除了使用現成可用的模式外，您還可以為自適應表單元件定義可重複使用的自訂模式。 例如，您可以定義文字欄位或數值欄位。 定義後，可在所有表單中為指定類型的元件使用這些模式。 例如，您可以為文字欄位建立自訂模式，並在其最適化表單的文字欄位中使用。 通過訪問元件的編輯對話框中的陣列部分，可以選擇自定義陣列。 如需Pattern定義或格式的詳細資訊，請參 [閱HTML5表單的Picture子句支援](/help/forms/using/picture-clause-support.md)。

執行以下步驟，為特定欄位類型建立自定義模式，並將其重複用於相同類型的其他欄位：

1. 導覽至您編寫執行個體上的CRXDE Lite。
1. 建立資料夾以維護自訂圖樣。 在/apps目錄下，建立sling:folder類型的節點。 例如，建立名稱為的節點 `customPatterns`。 在此節點下，建立另一個類型的節 `nt:unstructed` 點並將其命名 `textboxpatterns`。 此節點包含您要新增的各種自訂模式。
1. 開啟已建立節點的「屬性」頁籤。 例如，開啟的「屬性」頁籤 `textboxpatterns`。 將屬性 `guideComponentType` 新增至此節點，並將其值設 *為fd/af/components/formatter/guideTextBox*。

1. 此屬性的值會根據要定義陣列的欄位而有所不同。 對於數值欄位，屬 `guideComponentType` 性的值 *為fd/af/components/formatter/guideNumericBox*。 「日期選擇器」欄位的值 *為fd/af/components/formatter/guideDatepicker*。&quot;
1. 通過為節點分配屬性，可以添加自定義模 `textboxpatterns` 式。 新增名稱的屬性(例如 `pattern1`)，並將其值設定至您要新增的模式。 例如，新增值為 `pattern1` Fax=text{99-999-999999}的屬性。 此模式適用於您在「最適化表單」中使用的所有文字方塊。

   ![在CrxDe中建立欄位的自訂圖樣](assets/creating-custom-patterns.png)

   建立自訂圖樣

