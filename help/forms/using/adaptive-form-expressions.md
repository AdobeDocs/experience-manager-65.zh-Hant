---
title: 最適化表單運算式
seo-title: 最適化表單運算式
description: Use adaptive forms expressions to add automatic validation, calculation, and turn visibility of a section on or off.
seo-description: Use adaptive forms expressions to add automatic validation, calculation, and turn visibility of a section on or off.
uuid: c274dce5-8b87-472f-bff5-53b246fa6584
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 2fd2276e-cfe3-47ad-94c1-9c7af56b7a17
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Adaptive Form Expressions{#adaptive-form-expressions}

最適化表單提供最佳化和簡化的表單填寫體驗，讓使用者能使用動態指令碼功能。 它可讓您編寫運算式，以新增各種行為，例如動態顯示／隱藏欄位和面板。 它也可讓您新增計算欄位、讓欄位變成唯讀、新增驗證邏輯等。 動態行為是以使用者輸入或預先填入的資料為基礎。

JavaScript是最適化表單的運算式語言。 所有運算式都是有效的JavaScript運算式，並使用最適化表單指令碼模型API。 這些運算式會傳回特定類型的值。 如需最適化表單類別、事件、物件和公用API的完整清單，請參閱適 [化表單的JavaScript程式庫API參考](https://helpx.adobe.com/aem-forms/6/javascript-api/index.html)。

## 編寫陳述式的最佳範例 {#best-practices-for-writing-expressions}

* While writing expressions, to access fields and panels, you can use name of field or panel. 若要存取欄位的值，請使用value屬性。 例如， `field1.value`
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
   * To get a panel repeat index: `panel1.instanceIndex`
   * To get the instanceManager of a panel: `_panel1 or panel1.instanceManager`
   * To remove an instance of a panel: `_panel1.removeInstance(panel1.instanceIndex)`

## Expression Types {#expression-types}

在最適化表單中，您可以編寫運算式來新增動態顯示／隱藏欄位和面板等行為。 您也可以編寫運算式來新增計算欄位、讓欄位變成唯讀、驗證邏輯等。 最適化表單支援下列運算式：

* **[Access expressions](../../forms/using/adaptive-form-expressions.md#main-pars-header-4)**: to enable/disable a field.
* **[Calculate expressions](../../forms/using/adaptive-form-expressions.md#p-calculate-expression-p)**: to auto-compute value of a field.
* **[Click expression](../../forms/using/adaptive-form-expressions.md#p-click-expression-p)**: to handle actions on click event of a button.
* **[初始化指令碼](../../forms/using/adaptive-form-expressions.md#p-initialization-script-p):**對欄位的初始化執行操作。
* **[選項運算式](../../forms/using/adaptive-form-expressions.md#p-options-expression-p)**:以動態填寫下拉式清單。
* **[摘要運算式](#summary)**:動態計算accordion的標題。
* **[驗證運算式](../../forms/using/adaptive-form-expressions.md#p-validate-expression-p)**:來驗證欄位。
* **[值提交指令碼](../../forms/using/adaptive-form-expressions.md#p-value-commit-script-p):**變更欄位值後的表單元件。
* **[可見度運算式](../../forms/using/adaptive-form-expressions.md#p-visibility-expression-p)**:以控制欄位和面板的可見度。
* **[步驟完成運算式](../../forms/using/adaptive-form-expressions.md#p-step-completion-expression-p)**:以防止使用者進入精靈的下一步。

### 存取運算式（啟用運算式） {#access-expression-enablement-expression}

您可以使用存取運算式來啟用或停用欄位。 如果表達式使用欄位的值，則每當欄位的值更改時，都會檢索表達式。

**適用於**:欄位

**退貨類型**:運算式會傳回布林值，代表欄位是啟用還是停用。 **true** 代表欄位已啟用， **false** 代表欄位已停用。

**範例**:若要僅在欄位1的值設 **置為****X**&#x200B;時啟用欄位，訪問表達式為： `field1.value == "X"`

### 計算表達式 {#calculate-expression}

計算表達式用於使用表達式自動計算欄位的值。 通常，此表達式使用其他欄位的值屬性。 For example, `field2.value + field3.value`. 每當或的值 `field2`變 `field3`更時，都會檢索表達式並重新計算值。

**適用於**:欄位

**退貨類型**:運算式會傳回與顯示運算式結果的欄位相容的值（例如小數）。

**範例**:顯示欄位1中兩個欄位之和的計 **算表達式** 為：
`field2.value + field3.value`

### 按一下運算式 {#click-expression}

點按運算式可處理對按鈕點按事件所執行的動作。 GuideBridge現成可提供API來執行各種功能，例如提交、驗證與點按運算式一起使用。 For complete list of the APIs, see [GuideBridge APIs](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html).

**Applies to**: Button fields

**退貨類型**:點按運算式不會傳回任何值。 如果任何運算式傳回值，則會忽略該值。

**Example**: To populate a text box **textbox1** on the click action of a button with value **AEM Forms**, the click expression of the button is `textbox1.value="AEM Forms"`

### 初始化指令碼 {#initialization-script}

The initialization script is triggered when an adaptive form is initialized. 初始化指令碼的行為方式取決於方案：

* When an adaptive form is rendered without a data prefill, the initialization script runs after the form is initialized.
* When an adaptive form is rendered with a data prefill, the script is run after the pre-fill operation completes.
* When server sided revalidation of an adaptive form is triggered, the initialization script is executed.

**適用於：** 欄位和面板

**退貨類型：** 初始化指令碼表達式不返回任何值。 如果任何運算式傳回值，則會忽略該值。

**範例：** 在資料預先填入藍本中，若要在欄位的值儲存為 `'Adaptive Forms'` null時，將預設值填入欄位，初始化指令碼運算式為：
`if(this.value==null) this.value='Adaptive Forms';`

### 選項運算式 {#options-expression}

選項運算式可用來動態填入下拉式清單欄位的選項。

**適用於**:下拉式清單欄位

**退貨類型**:選項表達式返回字串值的陣列。 每個值都可以是簡單的字串，例如 **Male**，或是key=value對格式，例如 **1=Male**

**範例**:要根據另一個欄位的值填充欄位的值，請提供一個簡單的選項表達式。 例如，若要根據在另一欄位中 **表示的「婚姻狀態**」填入一個欄位Number of Kids **** ，其運算式為：

**`marital_status.value == "married" ? ["1=One", "2=two"] : ["0=Zero"]`.**

每當furnime_status欄 **位的值變更時** ，就會擷取運算式。 您也可以從REST服務填入下拉式清單。 For detailed information, see [Dynamically populating dropdowns](../../forms/using/dynamically-populate-dropdowns.md).

### Summary Expression {#summary}

The Summary expression dynamically computes the title of a child panel of an accordion layout panel. You can specify the Summary expression in a rule, which uses a form field or a custom logic to evaluate the title. The expression executes when the form initializes. 如果要預填充表單，則表達式在預填充資料後或表達式中使用的從屬欄位的值更改後執行。

The Summary expression is typically used for repeating children of an accordion layout panel to provide meaningful title to each child panel.

**Applies to:** Panels that are direct children of a panel whose layout is configured as Accordion.

**退貨類型：** 運算式會傳回成為accordion標題的字串。

**範例：** &quot;帳號：&quot;+ textbox1.value

### Validate Expression {#validate-expression}

The validate expression is used to validate the fields using the given expression. 通常，這些運算式會使用規則運算式與欄位值來驗證欄位。 The expression is retriggered and validation status of the field is recomputed on any change in the value of a field.

**適用於**:欄位

**Return Type**: The expression returns a Boolean value, representing the validation status of the field. The value **false** represents that the field is invalid and **true** represents that the field is valid.
**範例**:對於代表英國郵遞區號的欄位，驗證運算式為：

(**this.value** &amp;&amp; `this.value.match(/^(GIR 0AA|[A-Z]{1,2}\d[A-Z0-9]? ?[0-9][A-Z]{2}\s*)$/i) == null) ? false : true`

In the above example, if the non-empty value does not match the pattern, the expression returns **false** to indicate that the field is not valid.

>[!NOTE]
>
>If you write a validation expression for a non- mandatory or mandatory field, the expression is evaluated irrespective of the visibility status of the field. To stop validation for the hidden fields, set the validationsDisabled property in the Initialization or Value Commit Script to true. 例如， `this.validationsDisabled=true`

### 值認可指令碼 {#value-commit-script}

The Value Commit script is triggered when:

* 使用者會從UI變更欄位的值。
* 欄位的值因其他欄位的更改而以程式方式更改。

**適用於：** 欄位

**Return Type:** The value commit script expression does not return any value. 如果任何運算式傳回值，則會忽略該值。

**Example:** To convert the case of alphabets entered in the field to uppercase on commit, the value commit expression is:
`this.value=this.value.toUpperCase()`

>[!NOTE]
>
>You can disable the execution of the Value Commit Script when the value of a field is changed programmatically. To do so, go to https://&#39;[server]:[port]&#39;/system/console/configMgr and change **Adaptive Forms Version for Compatibility** to **AEM Forms 6.1**. Thereafter, Value Commit Script is executed only when the user changes the value of the field from the UI.

### 可見性運算式 {#visibility-expression}

The Visibility expression is used to control the visibility of field/panel. 通常，可見性運算式會使用欄位的值屬性，當該值變更時就會擷取。

**適用於**:欄位和面板

**Return Type**: Expression returns a Boolean value, representing the field/panel is visible or not. **false** represents that the field or panel is not visible and true represents that the field or panel is visible.

**Example**: For a panel that becomes visible only if value of **field1** is set to **Male**, the visibility expression is: `field1.value == "Male"`

### Step Completion Expression {#step-completion-expression}

The step completion expression is used to prevent a user from going to the next step of a wizard layout. These expressions are used when panels have a wizard layout (a multi-step forms showing one step at a time). The user can move to the next step, panel, or subsection only if all the required values in the current section are filled and valid.

**Applies to**: Panels with layout of item set to wizard.

**退貨類型**:運算式會傳回布林值，表示目前面板有效與否。 **True** represents that the current panel is valid and the user can navigate to next panel.

**Example**: In a form organized in various panels, before navigating to the next panel the current panel is validated. 在這種情況下，會使用步驟完成運算式。 Generally, these expressions use the GuideBridge validate API. 步驟完成運算式的範例為：
`window.guideBridge.validate([],this.panel.navigationContext.currentItem.somExpression)`

## 最適化表單中的驗證 {#validations-in-adaptive-form}

There are multiple methods to add field validation to an adaptive form. If a validation check is added on a field, **True** represents that the value entered in the field is valid. **False** represents that the value is invalid. If you tab in and out of a field, the error message is not generated.

The methods to add validations on a field are:

### 必要 {#required}

To make a component mandatory, in the **Edit** dialog of the component, you can select option **Title and Text > Required**. You can also add the appropriate **required message** (optional) as well. .

### Validation Patterns {#validation-patterns}

There are multiple out of the box validation patterns available for a field. 要選擇驗證模式，請在元件的「編 **輯** 」(Edit **)對話框中，找到「模式」(** Patterns **)部分並選**&#x200B;擇模式。 您可以在「模式」文字方塊中建立自 **訂驗證** 模式。 只有在填入的資 **料符合** 驗證模式時，才會傳回驗證狀態 **True** ，否則會傳回False。 若要編寫您自己的自訂驗證模式，請參 [閱HTML5表單的Picture子句支援](/help/forms/using/picture-clause-support.md)。

### 驗證運算式 {#validation-expressions}

您也可以使用不同欄位上的運算式來計算欄位的驗證。 這些運算式會寫入 **在元件「編輯** 」對話方塊的「指令碼 **」索引標籤的「驗證指令****** 碼」欄位中。 欄位的驗證狀態取決於表達式返回的值。 有關如何編寫此類表達式的資訊，請參 [閱驗證表達式](../../forms/using/adaptive-form-expressions.md#p-validate-expression-p)。

## 其他資訊 {#additional-information}

### 使用欄位顯示格式 {#using-field-display-format}

「顯示格式」可用來顯示不同格式的資料。 例如，您可使用顯示格式來顯示含連字型大小、郵遞區號格式或日期選擇器的電話號碼。 這些顯示陣列可從元件的「編 **輯」(Edit** )對話框的「陣列」(Patterns)部分中選取。 您可以編寫類似上述驗證模式的自訂顯示模式。

### GuideBridge - API和事件 {#guidebridge-apis-and-events}

GuideBridge是API的集合，可用來與瀏覽器記憶體模型中的最適化表單互動。 如需指南Bridge API、類別方法、公開事件的詳細簡介，請參閱適 [應性表單的JavaScript程式庫API參考](https://helpx.adobe.com/aem-forms/6/javascript-api/)。

>[!NOTE]
>
>建議不要在運算式中使用GuideBridge事件偵聽器。

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

執行以下步驟為特定欄位類型建立自定義模式，並將其重複用於相同類型的其他欄位：

1. 導覽至您編寫執行個體上的CRXDE Lite。
1. 建立資料夾以維護自訂圖樣。 在/apps目錄下，建立sling:folder類型的節點。 例如，建立名稱為的節點 `customPatterns`。 在此節點下，建立另一個類型的節 `nt:unstructed` 點並將其命名 `textboxpatterns`。 此節點包含您要新增的各種自訂模式。
1. 開啟已建立節點的「屬性」頁籤。 例如，開啟的「屬性」頁籤 `textboxpatterns`。 Add the `guideComponentType` property to this node and set its value to *fd/af/components/formatter/guideTextBox*.

1. 此屬性的值會根據要定義陣列的欄位而有所不同。 對於數值欄位，屬 `guideComponentType` 性的值 *為fd/af/components/formatter/guideNumericBox*。 「日期選擇器」欄位的值 *為fd/af/components/formatter/guideDatepicker*。&quot;
1. You can add a custom pattern by assigning a property to the `textboxpatterns` node. Add a property with a name (for example `pattern1`), and set its value to the pattern you want to add. 例如，新增值為 `pattern1` Fax=text{99-999-999999}的屬性。 此模式適用於您在「最適化表單」中使用的所有文字方塊。

   ![在CrxDe中建立欄位的自訂圖樣](assets/creating-custom-patterns.png)

   建立自訂圖樣

