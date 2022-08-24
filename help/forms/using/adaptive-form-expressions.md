---
title: 自適應表單表達式
seo-title: Adaptive Form Expressions
description: 使用自適應表單表達式添加自動驗證、計算和開啟或關閉節的可見性。
seo-description: Use adaptive forms expressions to add automatic validation, calculation, and turn visibility of a section on or off.
uuid: c274dce5-8b87-472f-bff5-53b246fa6584
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 2fd2276e-cfe3-47ad-94c1-9c7af56b7a17
docset: aem65
feature: Adaptive Forms
exl-id: 048bd9e8-ef34-40fb-9f46-73743d7b47c8
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '2746'
ht-degree: 0%

---

# 自適應表單表達式{#adaptive-form-expressions}

自適應表單為具有動態指令碼功能的最終用戶提供了優化和簡化的表單填充體驗。 它允許您編寫表達式以添加各種行為，如動態顯示/隱藏欄位和面板。 它還允許您添加計算欄位、使欄位為只讀、添加驗證邏輯等。 動態行為基於用戶輸入或預填充資料。

JavaScript是自適應表單的表達式語言。 所有表達式都是有效的JavaScript表達式，並使用自適應表單指令碼模型API。 這些表達式返回某些類型的值。 有關自適應表單類、事件、對象和公共API的完整清單，請參見 [用於自適應表單的JavaScript庫API參考](https://helpx.adobe.com/experience-manager/6-5/forms/javascript-api/index.html)。

## 編寫表達式的最佳做法 {#best-practices-for-writing-expressions}

* 在編寫表達式時，要訪問欄位和面板，可以使用欄位或面板的名稱。 要訪問欄位的值，請使用value屬性。 例如， `field1.value`
* 對表單中的欄位和面板使用唯一的名稱。 它有助於避免與編寫表達式時使用的欄位名稱發生任何可能的衝突。
* 編寫多行表達式時，使用分號來終止語句。

## 涉及重複面板的表達式的最佳做法 {#best-practices-for-expressions-involving-repeating-panel}

重複面板是使用指令碼API或預填充資料動態添加或刪除的面板的實例。 有關使用重複面板的詳細資訊，請參見 [建立可重複節的表單](/help/forms/using/creating-forms-repeatable-sections.md)。

* 要建立重複面板，請在面板對話框中開啟設定，並將最大計數欄位的值設定為大於1。
* 面板重複設定的最小計數值可以是一個或多個，但不能大於最大計數值。
* 當表達式引用重複面板的欄位時，表達式中的欄位名稱將解析為最接近的重複元素。
* 自適應形式提供了一些特殊函式來簡化可重複面板的計算，如求和、計數、最小、最大、濾波等。 有關函式的完整清單，請參見 [用於自適應表單的JavaScript庫API參考](https://helpx.adobe.com/aem-forms/6/javascript-api/af.html)
* 用於操作重複面板實例的API為：

   * 要添加面板實例： `panel1.instanceManager.addInstance()`
   * 要獲取面板重複索引，請執行以下操作： `panel1.instanceIndex`
   * 要獲取面板的instanceManager: `_panel1 or panel1.instanceManager`
   * 要刪除面板實例，請執行以下操作： `_panel1.removeInstance(panel1.instanceIndex)`

## 表達式類型 {#expression-types}

在自適應表單中，可以編寫表達式來添加動態顯示/隱藏欄位和面板等行為。 您還可以編寫表達式來添加計算欄位、使欄位為只讀、驗證邏輯等。 自適應表單支援以下表達式：

* **[訪問表達式](#access-expression-enablement-expression)**:啟用/禁用欄位。
* **[計算表達式](#calculate-expression)**:值。
* **[按一下表達式](#click-expression)**:處理按鈕的按一下事件時的操作。
* **[初始化指令碼](#initialization-script):** 對欄位的初始化執行操作。
* **[選項表達式](#options-expression)**:的子菜單。
* **[摘要表達式](#summary)**:以動態計算折疊面板的標題。
* **[驗證表達式](#validate-expression)**:來驗證欄位。
* **[值提交指令碼](#value-commit-script):** 的子菜單。
* **[可見性表達式](#visibility-expression)**:控制欄位和面板的可見性。
* **[步驟完成表達式](#step-completion-expression)**:來防止用戶進入嚮導的下一步。

### 訪問表達式（啟用表達式） {#access-expression-enablement-expression}

可以使用訪問表達式啟用或禁用欄位。 如果表達式使用欄位的值，則只要欄位的值更改，就會重新觸發表達式。

**應用於**:欄位

**返回類型**:表達式返回一個布爾值，表示欄位是啟用還是禁用。 **真** 表示欄位已啟用，並 **假** 表示欄位已禁用。

**示例**:僅在 **欄位1** 設定為 **X**，訪問表達式為： `field1.value == "X"`

### 計算表達式 {#calculate-expression}

計算表達式用於使用表達式自動計算欄位的值。 通常，此表達式使用其他欄位的值屬性。 比如說， `field2.value + field3.value`。 無論何時 `field2`或 `field3`更改，將重新調用表達式並重新計算值。

**應用於**:欄位

**返回類型**:表達式返回與顯示表達式結果的欄位（例如，小數）相容的值。

**示例**:顯示中兩個欄位和的計算表達式 **欄位1** 為：
`field2.value + field3.value`

### 按一下表達式 {#click-expression}

按一下表達式處理對按鈕的按一下事件所執行的操作。 現成， GuideBridge提供API來執行各種功能，如提交、驗證與按一下表達式一起使用。 有關API的完整清單，請參見 [GuideBridge API](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html)。

**應用於**:按鈕欄位

**返回類型**:按一下表達式不返回任何值。 如果任何表達式返回值，則忽略該值。

**示例**:填充文本框 **文本框1** 按鈕的按一下操作 **AEM Forms**，按一下按鈕的表達式為 `textbox1.value="AEM Forms"`

### 初始化指令碼 {#initialization-script}

初始化自適應表單時觸發初始化指令碼。 根據情形，初始化指令碼的行為方式如下：

* 當在沒有資料預填充的情況下呈現自適應表單時，初始化指令碼在表單初始化後運行。
* 當使用資料預填充呈現自適應表單時，指令碼在預填充操作完成後運行。
* 當觸發自適應表單的伺服器側重新驗證時，執行初始化指令碼。

**適用於：** 欄位和面板

**返回類型：** 初始化指令碼表達式不返回任何值。 如果任何表達式返回值，則忽略該值。

**示例：** 在資料預填充方案中，用預設值填充欄位 `'Adaptive Forms'` 當其值保存為null時，初始化指令碼表達式為：
`if(this.value==null) this.value='Adaptive Forms';`

### 選項表達式 {#options-expression}

選項表達式用於動態填充下拉清單欄位的選項。

**應用於**:下拉清單欄位

**返回類型**:選項表達式返回字串值的陣列。 每個值都可以是簡單的字串，如 **男性**&#x200B;或鍵=值對格式，如 **1=男**

**示例**:要根據另一個欄位的值填充欄位的值，請提供一個簡單的選項表達式。 例如，要填充欄位， **孩子數**，根據 **婚姻狀況** 在另一個欄位中表示，表達式為：

**`marital_status.value == "married" ? ["1=One", "2=two"] : ["0=Zero"]`.**

只要 **婚姻狀態** 欄位更改，表達式將被重新觸發。 您也可以從REST服務填充下拉清單。 有關詳細資訊，請參見 [動態填充下拉清單](../../forms/using/dynamically-populate-dropdowns.md)。

### 摘要表達式 {#summary}

「摘要」表達式動態計算折疊佈局面板的子面板的標題。 可以在規則中指定摘要表達式，該表達式使用表單域或自定義邏輯來計算標題。 表單初始化時執行表達式。 如果要預填表單，則表達式在預填資料或表達式中使用的從屬欄位值更改後執行。

「摘要」表達式通常用於重複折疊佈局面板的子級，以便為每個子級面板提供有意義的標題。

**適用於：** 面板是其佈局配置為折疊面板的直接子代。

**返回類型：** 表達式返回一個String，該String成為折疊面板的標題。

**示例：** &quot;帳號：&quot; + textbox1.value

### 驗證表達式 {#validate-expression}

validate表達式用於使用給定表達式驗證欄位。 通常，此類表達式使用規則運算式和欄位值來驗證欄位。 將重新觸發表達式，並根據欄位值的任何變化重新計算欄位的驗證狀態。

**應用於**:欄位

**返回類型**:表達式返回一個布爾值，表示欄位的驗證狀態。 值 **假** 表示欄位無效，並且 **真** 表示欄位有效。
**示例**:對於表示英國郵遞區號的欄位，驗證表達式為：

(**此值** &amp; `this.value.match(/^(GIR 0AA|[A-Z]{1,2}\d[A-Z0-9]? ?[0-9][A-Z]{2}\s*)$/i) == null) ? false : true`

在上例中，如果非空值與模式不匹配，則表達式將返回 **假** 以指示該欄位無效。

>[!NOTE]
>
>如果為非強制或強制欄位編寫驗證表達式，則不管該欄位的可見性狀態如何，都會計算該表達式。 要停止對隱藏欄位的驗證，請將初始化或值提交指令碼中的validationsDisabled屬性設定為true。 例如， `this.validationsDisabled=true`

### 值認可指令碼 {#value-commit-script}

值提交指令碼在以下情況下觸發：

* 用戶從UI更改欄位的值。
* 由於另一個欄位中的更改，欄位的值會以寫程式方式更改。

**適用於：** 欄位

**返回類型：** 值commit指令碼表達式不返回任何值。 如果任何表達式返回值，則忽略該值。

**示例：** 要在提交時將欄位中輸入的字母大小寫轉換為大寫，值提交表達式為：
`this.value=this.value.toUpperCase()`

>[!NOTE]
>
>當以寫程式方式更改欄位的值時，可以禁用值提交指令碼的執行。 為此，請訪問https://&#39;[伺服器]:[埠]「/system/console/configMgr和更改 **適應Forms版本以實現相容性** 至 **AEM Forms6.1**。 此後，僅當用戶更改UI中欄位的值時，才執行值提交指令碼。

### 可見性運算式 {#visibility-expression}

「可見性」表達式用於控制欄位/面板的可見性。 通常，可見性表達式使用欄位的值屬性，並且每當該值更改時都會重新觸發。

**應用於**:欄位和面板

**返回類型**:表達式返回一個布爾值，表示欄位/面板是否可見。 **假** 表示欄位或面板不可見，而true表示欄位或面板可見。

**示例**:對於僅在 **欄位1** 設定為 **男性**，可見性表達式為： `field1.value == "Male"`

### 步驟完成表達式 {#step-completion-expression}

步驟完成表達式用於防止用戶進入嚮導佈局的下一步。 當面板具有嚮導佈局（一個多步驟表單一次顯示一個步驟）時，會使用這些表達式。 僅當當前部分中的所有必需值都已填充且有效時，用戶才能移動到下一步、面板或子部分。

**應用於**:項佈局設定為嚮導的面板。

**返回類型**:表達式返回一個布爾值，表示當前面板是否有效。 **真** 表示當前面板有效，用戶可以導航到下一個面板。

**示例**:在按不同面板組織的表單中，在導航到下一個面板之前，驗證當前面板。 在這種情況下，使用步驟完成表達式。 通常，這些表達式使用GuideBridge驗證API。 步驟完成表達式的示例為：
`window.guideBridge.validate([],this.panel.navigationContext.currentItem.somExpression)`

## 自適應表單中的驗證 {#validations-in-adaptive-form}

有多種方法可將欄位驗證添加到自適應表單。 如果在欄位上添加了驗證檢查， **真** 表示在欄位中輸入的值有效。 **假** 表示該值無效。 如果在域中和域外執行制表操作，則不會生成錯誤消息。

在欄位上添加驗證的方法有：

### 必要 {#required}

要強制使用元件，請在 **編輯** 對話框，可以選擇選項 **標題和文本>必需**。 您還可以添加相應的 **必需消息** （可選）。。

### 驗證模式 {#validation-patterns}

有多個可用於欄位的出廠驗證模式。 要選擇驗證模式，請在 **編輯** 對話框，找到 **圖案** 選擇 **圖案**。 您可以在 **圖案** 的子菜單。 返回驗證狀態 **真** 僅當填充的資料符合驗證模式時，否則 **假** 的子菜單。 要編寫您自己的自定義驗證模式，請參閱 [對HTML5窗體的Picture子句支援](/help/forms/using/picture-clause-support.md)。

### 驗證表達式 {#validation-expressions}

也可以使用不同欄位上的表達式計算欄位的驗證。 這些表達式都寫在 **驗證指令碼** 的 **指令碼** 頁籤 **編輯** 對話框。 欄位的驗證狀態取決於表達式返回的值。 有關如何編寫此類表達式的資訊，請參見 [驗證表達式](../../forms/using/adaptive-form-expressions.md#p-validate-expression-p)。

## 其他資訊 {#additional-information}

### 使用欄位顯示格式 {#using-field-display-format}

「顯示格式」(Display Format)可用於以不同格式顯示資料。 例如，可以使用顯示格式顯示帶連字元、格式ZIP代碼或日期選取器的電話號碼。 可從 **圖案** 的子菜單。 可以編寫與上述驗證模式類似的自定義顯示模式。

### GuideBridge - API和事件 {#guidebridge-apis-and-events}

GuideBridge是API的集合，可用於與瀏覽器記憶體模型中的自適應表單交互。 有關Guide Bridge API、類方法、公開的事件的詳細介紹，請參見 [用於自適應表單的JavaScript庫API參考](https://helpx.adobe.com/aem-forms/6/javascript-api/)。

>[!NOTE]
>
>建議不要在表達式中使用GuideBridge事件偵聽器。

#### GuideBridge在各種表達式中的用法 {#guidebridge-usage-in-various-expressions}

* 要重置表單域，可以觸發 `guideBridge.reset()` 按一下按鈕表達式上的API。 同樣，也有可以作為按一下表達式調用的提交API `guideBridge.submit()`**。**

* 您可以使用 `setFocus()` 用於設定各個欄位或面板焦點的API（面板焦點自動設定為第一個欄位）。 `setFocus()`提供了多種導航選項，如跨面板導航、先前/下一次遍歷、將焦點設定為特定欄位等。 例如，要移動到下一個面板，可以使用： `guideBridge.setFocus(this.panel.somExpression, 'nextItem').`

* 要驗證自適應表單或其特定面板，請使用 `guideBridge.validate(errorList, somExpression).`

#### 在表達式外使用GuideBridge  {#using-guidebridge-outside-expressions-nbsp}

也可以在表達式外部使用GuideBridge API。 例如，可以使用GuideBridge API設定承載自適應表單的頁面HTML和表單模型之間的通信。 此外，還可以設定來自承載表單的Iframe父級的值。

要對上述示例使用GuideBridge API，請捕獲GuideBridge的實例。 要捕獲實例，請聽 `bridgeInitializeStart`事件 `window`對象：

```javascript
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
>在AEM中，最好在clientLib中編寫代碼並將其包含在頁面（頁面的header.jsp或footer.jsp）中

在初始化表單後使用GuideBridge( `bridgeInitializeComplete` 事件已調度)，使用 `window.guideBridge`。 可以使用 `guideBride.isConnected` API。

#### GuideBridge事件 {#guidebridge-events}

GuideBridge還為托管頁面上的外部指令碼提供某些事件。 外部指令碼可以偵聽這些事件並執行各種操作。 例如，每當表單中的用戶名更改時，頁面標題中顯示的名稱也會更改。 有關此類事件的詳細資訊，請參閱 [用於自適應表單的JavaScript庫API參考](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html)。

使用以下代碼註冊處理程式：

```javascript
guideBridge.on("elementValueChanged", function (event, data)  {

      // execute some logic when value of a field is changed

});
```

### 為欄位建立自定義模式 {#creating-custom-patterns-for-a-field}

如上所述，自適應表單允許作者提供驗證或顯示格式的模式。 除了使用現成模式外，還可以為自適應表單元件定義可重用的自定義模式。 例如，可以定義文本欄位或數字欄位。 定義完後，可以在所有窗體中為指定類型的元件使用這些模式。 例如，可以為文本欄位建立自定義模式，並在文本欄位的自適應窗體中使用它。 通過訪問元件編輯對話框中的陣列部分，可以選擇自定義陣列。 有關陣列定義或格式的詳細資訊，請參閱 [對HTML5窗體的Picture子句支援](/help/forms/using/picture-clause-support.md)。

執行以下步驟為特定欄位類型建立自定義模式，並將其重新用於相同類型的其他欄位：

1. 導航到創作實例上的CRXDE Lite。
1. 建立資料夾以維護自定義模式。 在/apps目錄下，建立sling:folder類型的節點。 例如，建立具有名稱的節點 `customPatterns`。 在此節點下，建立其他類型的節點 `nt:unstructed` 然後點名 `textboxpatterns`。 此節點包含要添加的各種自定義模式。
1. 開啟所建立節點的「屬性」頁籤。 例如，開啟的「屬性」頁籤 `textboxpatterns`。 添加 `guideComponentType` 屬性到此節點，將其值設定為 *fd/af/components/formatter/guide文本框*。

1. 此屬性的值會根據要為其定義陣列的欄位而有所不同。 對於數字欄位， `guideComponentType` 屬性 *fd/af/components/formatter/guideNumericBox*。 「日期選取器」(Datepicker)欄位的值為 *fd/af/components/formatter/guideDatepicker*。&quot;
1. 通過向 `textboxpatterns` 的下界。 添加具有名稱的屬性(例如 `pattern1`)，並將其值設定為要添加的模式。 例如，添加屬性 `pattern1` 值為Fax=text{99-999-999999}。 該模式可用於在自適應Forms中使用的所有文本框。

   ![為CrxDe中的欄位建立自定義模式](assets/creating-custom-patterns.png)

   建立自定義模式
