---
title: 適用性表單運算式
seo-title: Adaptive Form Expressions
description: 使用最適化表單運算式來新增自動驗證、計算，以及開啟或關閉區段的可見性。
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

# 適用性表單運算式{#adaptive-form-expressions}

最適化表單提供最佳化且簡化的表單填寫體驗，讓使用者擁有動態指令碼功能。 它可讓您撰寫運算式來新增各種行為，例如動態顯示/隱藏欄位和面板。 它也可讓您新增計算欄位、讓欄位變成唯讀、新增驗證邏輯等。 動態行為是以使用者輸入或預填的資料為基礎。

JavaScript是最適化表單的運算式語言。 所有運算式都是有效的JavaScript運算式，且會使用最適化表單指令碼模型API。 這些運算式會傳回特定類型的值。 如需適用性表單類別、事件、物件和公用API的完整清單，請參閱 [適用於最適化表單的JavaScript程式庫API參考](https://helpx.adobe.com/experience-manager/6-5/forms/javascript-api/index.html).

## 撰寫運算式的最佳實務 {#best-practices-for-writing-expressions}

* 撰寫運算式時，若要存取欄位和面板，您可以使用欄位或面板的名稱。 若要存取欄位的值，請使用值屬性。 例如, `field1.value`
* 對表單中的欄位和面板使用唯一的名稱。 它有助於避免寫入運算式時與所使用欄位名稱產生任何可能衝突。
* 在編寫多行表達式時，使用分號來終止語句。

## 涉及重複面板的運算式最佳作法 {#best-practices-for-expressions-involving-repeating-panel}

重複面板是使用指令碼API或預先填入資料，以動態方式新增或移除面板的例項。 如需使用重複面板的詳細資訊，請參閱 [建立可重複區段的表單](/help/forms/using/creating-forms-repeatable-sections.md).

* 若要建立重複面板，請在面板對話方塊中開啟設定，並將「計數上限」欄位的值設為大於1。
* 面板重複設定的最小計數值可以是一或多個，但不能超過最大計數值。
* 當運算式引用重複面板的欄位時，運算式中的欄位名稱會解析為最接近的重複元素。
* 適用性表單提供一些特殊功能，可簡化可重複面板的計算，例如總計、計數、最小值、最大值、篩選等。 如需完整的函式清單，請參閱 [適用於最適化表單的JavaScript程式庫API參考](https://helpx.adobe.com/aem-forms/6/javascript-api/af.html)
* 用於操控重複面板實例的API包括：

   * 若要新增面板例項： `panel1.instanceManager.addInstance()`
   * 要獲取面板重複索引： `panel1.instanceIndex`
   * 若要取得面板的instanceManager: `_panel1 or panel1.instanceManager`
   * 若要移除面板的例項： `_panel1.removeInstance(panel1.instanceIndex)`

## 運算式類型 {#expression-types}

在適用性表單中，您可以撰寫運算式來新增動態顯示/隱藏欄位和面板等行為。 您也可以撰寫運算式來新增計算欄位、讓欄位成為唯讀、驗證邏輯等。 適用性表單支援下列運算式：

* **[存取運算式](#access-expression-enablement-expression)**:啟用/停用欄位。
* **[計算運算式](#calculate-expression)**:自動計算欄位值。
* **[按一下運算式](#click-expression)**:處理按鈕的點按事件上的動作。
* **[初始化指令碼](#initialization-script):** 在初始化欄位時執行動作。
* **[選項表達式](#options-expression)**:以動態填入下拉式清單。
* **[摘要運算式](#summary)**:動態計算折疊式功能表的標題。
* **[驗證運算式](#validate-expression)**:來驗證欄位。
* **[值提交指令碼](#value-commit-script):** 更改欄位值後表單的元件。
* **[可見性運算式](#visibility-expression)**:控制欄位和面板的可見性。
* **[步驟完成表達式](#step-completion-expression)**:來防止使用者進入精靈的下一步。

### 存取運算式（啟用運算式） {#access-expression-enablement-expression}

您可以使用存取運算式來啟用或停用欄位。 如果表達式使用欄位的值，則每當欄位的值更改時，都會檢索表達式。

**套用至**:欄位

**傳回類型**:運算式會傳回布林值，代表欄位已啟用或停用。 **true** 代表欄位已啟用，且 **false** 代表欄位已停用。

**範例**:僅在 **欄位1** 設為 **X**，存取運算式為： `field1.value == "X"`

### 計算表達式 {#calculate-expression}

計算表達式用於使用表達式自動計算欄位的值。 通常，此類表達式會使用其他欄位的值屬性。 例如, `field2.value + field3.value`. 每當 `field2`或 `field3`變更時，會擷取運算式，並重新計算值。

**套用至**:欄位

**傳回類型**:運算式會傳回與顯示運算式結果的欄位（例如小數）相容的值。

**範例**:顯示以下欄位之和的計算表達式： **欄位1** 為：
`field2.value + field3.value`

### 按一下運算式 {#click-expression}

點按運算式會處理按鈕的點按事件所執行的動作。 GuideBridge提供API，可立即執行各種功能，例如提交、驗證與點按運算式搭配使用。 如需API的完整清單，請參閱 [GuideBridge API](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html).

**套用至**:按鈕欄位

**傳回類型**:點按運算式不會傳回任何值。 如果任何運算式傳回值，則會忽略值。

**範例**:要填入文本框 **textbox1** 關於具有值的按鈕的點按動作 **AEM Forms**，按鈕的點按運算式為 `textbox1.value="AEM Forms"`

### 初始化指令碼 {#initialization-script}

初始化適用性表單時，會觸發初始化指令碼。 根據情況，初始化指令碼的行為如下：

* 在未預填資料的情況下轉譯最適化表單時，初始化表單後會執行初始化指令碼。
* 以資料預填呈現適用性表單時，指令碼會在預填操作完成後執行。
* 觸發伺服器端重新驗證適用性表單時，會執行初始化指令碼。

**適用於：** 欄位和面板

**傳回類型：** 初始化指令碼表達式不返回任何值。 如果任何運算式傳回值，則會忽略值。

**範例：** 在資料預填案例中，將預設值填入欄位 `'Adaptive Forms'` 將其值保存為null時，初始化指令碼表達式為：
`if(this.value==null) this.value='Adaptive Forms';`

### 選項表達式 {#options-expression}

選項運算式可用來動態填入下拉式清單欄位的選項。

**套用至**:下拉式清單欄位

**傳回類型**:options運算式會傳回字串值的陣列。 每個值都可以是簡單字串，例如 **男性**，或索引鍵=值配對格式，例如 **1=男性**

**範例**:要根據其他欄位的值填入欄位的值，請提供簡單的選項表達式。 例如，若要填入欄位， **孩子數**，根據 **婚姻狀況** 在另一個欄位中表示，運算式為：

**`marital_status.value == "married" ? ["1=One", "2=two"] : ["0=Zero"]`.**

只要 **firey_status** 欄位變更，則會擷取運算式。 您也可以從REST服務填入下拉式清單。 如需詳細資訊，請參閱 [動態填入下拉式清單](../../forms/using/dynamically-populate-dropdowns.md).

### 摘要運算式 {#summary}

「摘要」表達式動態計算折疊式面板的子面板的標題。 您可以在規則中指定「摘要」運算式，該運算式使用表單欄位或自訂邏輯來評估標題。 表單初始化時執行表達式。 如果要預填表單，則在預填資料後或在表達式中使用的從屬欄位的值更改時執行表達式。

「摘要」運算式通常用於重複折疊式面板配置面板的子項，以為每個子項面板提供有意義的標題。

**適用於：** 面板是其版面配置設定為折疊式面板的直接子項。

**傳回類型：** 運算式會傳回字串，成為折疊式功能表的標題。

**範例：** &quot;帳號：&quot; + textbox1.value

### 驗證運算式 {#validate-expression}

驗證表達式用於使用給定表達式驗證欄位。 這類運算式通常會使用規則運算式與欄位值搭配，以驗證欄位。 會擷取運算式，並根據欄位值的任何變更重新計算欄位的驗證狀態。

**套用至**:欄位

**傳回類型**:運算式會傳回布林值，代表欄位的驗證狀態。 值 **false** 代表欄位無效，且 **true** 表示欄位有效。
**範例**:對於代表UK後置代碼的欄位，驗證運算式為：

(**this.value** &amp; `this.value.match(/^(GIR 0AA|[A-Z]{1,2}\d[A-Z0-9]? ?[0-9][A-Z]{2}\s*)$/i) == null) ? false : true`

在上述範例中，如果非空白值不符合模式，運算式會傳回 **false** 以指出欄位無效。

>[!NOTE]
>
>如果您為非強制或強制欄位編寫驗證運算式，則無論欄位的可見性狀態如何，都會評估運算式。 要停止對隱藏欄位的驗證，請將「初始化」或「值提交指令碼」中的validationsDisabled屬性設定為true。 例如, `this.validationsDisabled=true`

### 值認可指令碼 {#value-commit-script}

值提交指令碼在以下情況下觸發：

* 使用者會從UI變更欄位的值。
* 欄位的值會因其他欄位的變更而以程式設計方式變更。

**適用於：** 欄位

**傳回類型：** 值提交指令碼表達式不返回任何值。 如果任何運算式傳回值，則會忽略值。

**範例：** 要在提交時將欄位中輸入字母的大小寫轉換為大寫，值提交表達式為：
`this.value=this.value.toUpperCase()`

>[!NOTE]
>
>以寫程式方式更改欄位的值時，可以禁用「值提交指令碼」的執行。 若要這麼做，請前往https://&#39;[伺服器]:[埠]「/system/console/configMgr和更改 **適用於相容性的Forms版本** to **AEM Forms 6.1**. 之後，只有當使用者從UI變更欄位值時，才會執行「值提交指令碼」。

### 可見性運算式 {#visibility-expression}

「可見性」表達式用於控制欄位/面板的可見性。 可見性運算式通常使用欄位的值屬性，且每當該值變更時都會擷取。

**套用至**:欄位和面板

**傳回類型**:運算式會傳回布林值，代表欄位/面板是否可見。 **false** 代表欄位或面板不可見，而true代表欄位或面板可見。

**範例**:對於只有在 **欄位1** 設為 **男性**，可見性運算式為： `field1.value == "Male"`

### 步驟完成表達式 {#step-completion-expression}

步驟完成表達式用於阻止用戶進入嚮導佈局的下一步。 當面板具有精靈版面時，會使用這些運算式（多步驟表單一次顯示一個步驟）。 只有當目前區段中的所有必要值皆已填入且有效時，使用者才可移至下一個步驟、面板或子區段。

**套用至**:項目配置設為精靈的面板。

**傳回類型**:運算式會傳回布林值，代表目前的面板有效與否。 **True** 表示目前的面板有效，且使用者可導覽至下一個面板。

**範例**:在導覽至下一個面板前，會先以各種面板組織的表單驗證目前的面板。 在這種情況下，會使用步驟完成運算式。 這些運算式通常會使用GuideBridge驗證API。 步驟完成表達式的示例如下：
`window.guideBridge.validate([],this.panel.navigationContext.currentItem.somExpression)`

## 適用性表單中的驗證 {#validations-in-adaptive-form}

有多種方法可將欄位驗證新增至最適化表單。 如果欄位上新增驗證檢查， **True** 表示在欄位中輸入的值有效。 **False** 表示值無效。 如果您在欄位中和欄位外標籤，則不會產生錯誤訊息。

在欄位上新增驗證的方法如下：

### 必要 {#required}

若要將元件設為必填項目，請在 **編輯** 元件的對話框，可以選取選項 **標題和文字>必要**. 您也可以新增適當的 **必填訊息** （選用）。.

### 驗證模式 {#validation-patterns}

一個欄位有多個可用的現成驗證模式。 若要選取驗證模式，請在 **編輯** 元件對話方塊中，找出 **模式** 區段，然後選取 **模式**. 您可以在 **圖樣** 框。 會傳回驗證狀態 **True** 只有在填入的資料符合驗證模式時，否則 **False** 的URL。 若要撰寫您自己的自訂驗證模式，請參閱 [HTML5表單的子句支援](/help/forms/using/picture-clause-support.md).

### 驗證運算式 {#validation-expressions}

也可以使用不同欄位上的運算式來計算欄位的驗證。 這些運算式都寫在 **驗證指令碼** 欄位 **指令碼** 標籤 **編輯** 對話框。 欄位的驗證狀態取決於運算式傳回的值。 有關如何編寫此類表達式的資訊，請參見 [驗證運算式](../../forms/using/adaptive-form-expressions.md#p-validate-expression-p).

## 其他資訊 {#additional-information}

### 使用欄位顯示格式 {#using-field-display-format}

「顯示格式」可用來以不同格式顯示資料。 例如，您可以使用顯示格式來顯示帶有連字型大小、ZIP代碼格式或日期選擇器的電話號碼。 可從 **模式** 元件的「編輯」對話框的「編輯」部分。 您可以撰寫類似上述驗證模式的自訂顯示模式。

### GuideBridge - API和事件 {#guidebridge-apis-and-events}

GuideBridge是API的集合，可用來與瀏覽器記憶體模型中的最適化表單互動。 如需指南橋接API的詳細簡介、類別方法、公開的事件，請參閱 [適用於最適化表單的JavaScript程式庫API參考](https://helpx.adobe.com/aem-forms/6/javascript-api/).

>[!NOTE]
>
>建議不要在運算式中使用GuideBridge事件監聽器。

#### GuideBridge在各種運算式中的使用 {#guidebridge-usage-in-various-expressions}

* 若要重設表單欄位，您可以觸發 `guideBridge.reset()` 按一下按鈕運算式的API。 同樣地，也有提交API可以以點按運算式的形式呼叫 `guideBridge.submit()`**.**

* 您可以使用 `setFocus()` 可跨不同欄位或面板設定焦點的API（面板焦點會自動設為第一個欄位）。 `setFocus()`提供多種導覽選項，例如跨面板導覽、先前/下次周遊、將焦點設定在特定欄位等。 例如，若要移至下一個面板，您可以使用： `guideBridge.setFocus(this.panel.somExpression, 'nextItem').`

* 若要驗證最適化表單或其特定面板，請使用 `guideBridge.validate(errorList, somExpression).`

#### 在運算式外使用GuideBridge  {#using-guidebridge-outside-expressions-nbsp}

您也可以在運算式外部使用GuideBridge API。 例如，您可以使用GuideBridge API來設定托管最適化表單的頁面HTML與表單模型之間的通訊。 此外，您還可以設定來自托管表單之Iframe父項的值。

若要針對上述範例使用GuideBridge API，請擷取GuideBridge的例項。 要捕獲實例，請聽 `bridgeInitializeStart`事件 `window`物件：

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
>在AEM中，最好將程式碼寫入clientLib中，並將其納入您的頁面（頁面的header.jsp或footer.jsp）中

若要在表單初始化後使用GuideBridge( `bridgeInitializeComplete` 事件已發送)，請使用獲取GuideBridge實例 `window.guideBridge`. 您可以使用 `guideBride.isConnected` API。

#### GuideBridge事件 {#guidebridge-events}

GuideBridge也針對托管頁面上的外部指令碼提供特定事件。 外部指令碼可監聽這些事件並執行各種操作。 例如，每當表單中的使用者名稱變更時，頁面標題中顯示的名稱也會變更。 如需此類事件的詳細資訊，請參閱 [適用於最適化表單的JavaScript程式庫API參考](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html).

使用以下代碼註冊處理程式：

```javascript
guideBridge.on("elementValueChanged", function (event, data)  {

      // execute some logic when value of a field is changed

});
```

### 為欄位建立自訂模式 {#creating-custom-patterns-for-a-field}

如上所述，最適化表單可讓作者提供驗證或顯示格式的模式。 除了使用現成可用的模式外，您還可以為最適化表單元件定義可重複使用的自訂模式。 例如，您可以定義文字欄位或數值欄位。 定義後，您可以在所有表單中對指定類型的元件使用這些模式。 例如，您可以為文字欄位建立自訂模式，並在其最適化表單的文字欄位中使用。 您可以存取元件編輯對話方塊中的模式區段，以選取自訂模式。 如需模式定義或格式的詳細資訊，請參閱 [HTML5表單的子句支援](/help/forms/using/picture-clause-support.md).

執行下列步驟為特定欄位類型建立自訂模式，並對相同類型的其他欄位重複使用：

1. 導覽至製作執行個體上的CRXDE Lite。
1. 建立資料夾以維護自訂模式。 在/apps目錄下，建立sling:folder類型的節點。 例如，建立名稱為的節點 `customPatterns`. 在此節點下，建立其他類型的節點 `nt:unstructed` 然後給它命名 `textboxpatterns`. 此節點包含您要新增的各種自訂模式。
1. 開啟已建立節點的「屬性」頁簽。 例如，開啟 `textboxpatterns`. 新增 `guideComponentType` 屬性設定為 *fd/af/components/formatter/guideTextBox*.

1. 此屬性的值會根據您要定義模式的欄位而有所不同。 若為數值欄位，則 `guideComponentType` 屬性為 *fd/af/components/formatter/guideNumericBox*. 「日期挑選器」欄位的值為 *fd/af/components/formatter/guideDatepicker*.&quot;
1. 您可以為 `textboxpatterns` 節點。 新增具有名稱的屬性(例如 `pattern1`)，並將其值設為您要新增的模式。 例如，新增屬性 `pattern1` 值Fax=text{99-999-9999999}。 此模式適用於您在適用性Forms中使用的所有文字方塊。

   ![為CrxDe中的欄位建立自訂模式](assets/creating-custom-patterns.png)

   建立自訂模式
