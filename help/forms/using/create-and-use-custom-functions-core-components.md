---
title: 在最適化表單中建立及新增自訂函式
description: AEM Forms支援自訂函式，可讓使用者在規則編輯器中建立並使用自己的函式。
keywords: 新增自訂函式、使用自訂函式、建立自訂函式，以及在規則編輯器中使用自訂函式。
content-type: reference
feature: Adaptive Forms, Core Components
role: Admin, User, Developer
exl-id: 00073e3a-f1b5-4c42-9fea-4a14b8a22c81
source-git-commit: 7f1283898cbeebdedb7bdea6f0a8d9db567617ee
workflow-type: tm+mt
source-wordcount: '3385'
ht-degree: 2%

---

# 最適化Forms核心元件中的自訂函式

本文介紹如何使用最新最適化表單核心元件建立自訂函式，這些元件具有最新功能，例如：

* 自訂函式的快取功能
* 自訂函式的全域範圍物件和欄位物件支援
* 支援現代JavaScript功能，例如左鍵和箭頭功能（ES10支援）

請確保在您的AEM Forms核心元件環境中設定[最新表單版本](https://github.com/adobe/aem-core-forms-components/tree/release/650)，以使用自訂函式中的最新功能。</span>


| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | 本文 |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/create-and-use-custom-functions) |

## 簡介

AEM Forms 6.5包含JavaScript函式，可讓您使用規則編輯器定義複雜的商業規則。 雖然AEM Forms提供多種現成可用的自訂函式，但許多使用案例需要定義您自己的自訂函式，才能用於多個表單。 這些自訂函式可讓您根據特定需求操控和處理輸入的資料，藉此增強表單的功能。 此外，它們允許根據預先定義的條件動態變更表單行為。

### 使用自訂函式 {#uses-of-custom-function}

在最適化Forms核心元件中使用自訂函式的優點包括：


* **管理資料**：自訂函式可管理及處理輸入到表單欄位中的資料。
* **資料處理**：自訂函式可協助處理輸入到表單欄位中的資料。
* **資料驗證**：自訂函式可讓您對表單輸入執行自訂檢查，並提供指定的錯誤訊息。
* **動態行為**：自訂函式可讓您根據特定條件控制表單的動態行為。 例如，您可以顯示/隱藏欄位、修改欄位值或動態調整表單邏輯。
* **整合**：您可以使用自訂函式與外部API或服務整合。 它有助於從外部來源擷取資料、傳送資料至外部Rest端點，或根據外部事件執行自訂動作。

自訂函式基本上是新增至JavaScript檔案中的使用者端程式庫。 建立自訂函式後，規則編輯器中即會顯示該函式，供使用者在最適化表單中選取。 自訂函式由規則編輯器中的JavaScript註解識別。

### 支援自訂功能的JavaScript註解 {#js-annotations}

**JavaScript註解提供JavaScript程式碼的中繼資料**。 它包含以特定符號開頭的註解，例如，`/**`和`@`。 註解提供關於程式碼中函式、變數和其他元素的重要資訊。 最適化表單支援下列自訂函式的JavaScript註解：

#### 名稱

**Name**&#x200B;用於識別最適化表單的規則編輯器中的自訂函式。 下列語法可用來命名自訂函式：

* `@name [functionName] <Function Name>`
* `@function [functionName] <Function Name>`
* `@func [functionName] <Function Name>`

>[!NOTE]
>`[functionName]`是函式的名稱。 不允許空格。
>`<Function Name>` 是Adaptive Forms規則編輯器中函式的顯示名稱。
>如果函式名稱與函式本身的名稱相同，您可以在語法中省略`[functionName]`。

#### 參數

**引數**&#x200B;是自訂函式使用的引數清單。 函式可支援多個引數。 下列語法可用來定義自訂函式中的引數：

* `@param {type} name <Parameter Description>`
* `@argument` `{type} name <Parameter Description>`
* `@arg` `{type}` `name <Parameter Description>`

  `{type}`代表引數型別。 允許的引數型別包括：

   * string：代表單一字串值。
   * 數字：代表單一數值。
   * 布林值：代表單一布林值（true或false）。
   * string[]：代表字串值的陣列。
   * number[]：代表數值陣列。
   * 布林值[]：代表布林值的陣列。
   * date：代表單一日期值。
   * date[]：代表日期值的陣列。
   * array：代表包含各種型別值的泛型陣列。
   * object：代表傳遞至自訂函式的表單物件，而非直接傳遞其值。
   * 範圍：代表全域物件，其中包含唯讀變數，例如表單例項、目標欄位例項，以及在自訂函式內執行表單修改的方法。 這會宣告為JavaScript註解中的最後一個引數，且調適型表單的規則編輯器無法看到它。 scope引數可存取表單或元件的物件，以觸發表單處理所需的規則或事件。 如需有關Globals物件及其使用方式的進一步資訊，[請按一下這裡](/help/forms/using/create-and-use-custom-functions-core-components.md#field-and-global-scope-objects-in-custom-functions-support-field-and-global-objects)

引數型別是&#x200B;**不區分大小寫**，而且引數名稱中不允許有空格。

`<Parameter Description>`包含有關引數用途的詳細資料。 它可以有多個字詞。

<!--

**Optional Parameters**
By default, all parameters are mandatory. You can define a parameter as optional by either adding `=` after the parameter type or enclosing the parameter name in `[]`. Parameters defined as optional in JavaScript annotations are displayed as optional in the rule editor.
To define a variable as an optional parameter, you can use the any of the following syntaxes:
  
* `@param {type=} Input1`

In the above line of code, `Input1` is an optional parameter without any default value. To declare optional parameter with default value:

`@param {string=<value>} input1`
        
`input1` as an optional parameter with the default value set to `value`. 

* `@param {type} [Input1]`

In the above line of code, `Input1` is an optional parameter without any default value. To declare optional parameter with default value:

`@param {array} [input1=<value>]`

    `input1` is an optional parameter of array type with the default value set to `value`. 
    Ensure that the parameter type is enclosed in curly brackets {} and the parameter name is enclosed in square brackets []. 

Consider the following code snippet, where input2 is defined as an optional parameter:

```javascript

        /**
         * optional parameter function
         * @name OptionalParameterFunction
         * @param {string} input1 
         * @param {string=} input2 
         * @return {string}
        */
        function OptionalParameterFunction(input1, input2) {
        let result = "Result: ";
        result += input1;
        if (input2 !== null) {
            result += " " + input2;
        }
        return result;
        }
```

The following illustration displays using the `OptionalParameterFunction` csutom function in the rule editor:

![Optional or required parameters ](/help/forms/using/assets/optional-default-params.png)

You can save the rule without specifying a value for required parameters, but the rule is not executed and displays a warning message as:

![incomplete rule warning](/help/forms/using/assets/incomplete-rule.png)

When user leaves the optional parameter empty, then the "Undefined" value is passed to the custom function for the optional parameter.

To learn more about how to define optional parameters in JSDocs, [click here](https://jsdoc.app/tags-param).

-->

#### 傳回型別

傳回型別會指定自訂函式在執行後傳回的值型別。 下列語法可用來定義自訂函式中的傳回型別：

* `@return {type}`
* `@returns {type}`
  `{type}`代表函式的傳回型別。 允許的傳回型別為：
* string：代表單一字串值。
* 數字：代表單一數值。
* 布林值：代表單一布林值（true或false）。
* string[]：代表字串值的陣列。
* number[]：代表數值陣列。
* 布林值[]：代表布林值的陣列。
* date：代表單一日期值。
* date[]：代表日期值的陣列。
* array：代表包含各種型別值的泛型陣列。
* object：代表表單物件，而非直接代表其值。

傳回型別不區分大小寫。

#### 私人

宣告為私用的自訂函式不會出現在最適化表單的規則編輯器中的自訂函式清單中。 自訂函式預設為公用。 宣告自訂函式為私用的語法為`@private`。

<!--
#### Member

  Syntax: `@memberof namespace`
  Attaches a namespace to the function.
-->

<!--

#### This

   Syntax: `@this currentComponent`

   Use @this to refer to the Adaptive Form component on which the rule is written. 
  
   The following example is based on the field value. In the following example, the rule hides a field in the form. The `this` portion of `this.value` refers to underlying Adaptive Form component, on which the rule is written.

   ```
      /**
      * @function myTestFunction
      * @this currentComponent
      * @param {scope} scope in which code inside function will be executed.
      */
      myTestFunction = function (scope) {
         if(this.value == "O"){
               scope.age.visible = true;
         } else {
            scope.age.visible = false;
         }
      }

   ```

    >[!NOTE]
    >
    >Comments before custom function are used for summary. Summary can extend to multiple lines until a tag is encountered. Limit the size to a single for a concise description in the rule builder.

-->

<!--

## Function declaration supported types {#function-declaration-supported-types}

**Function Statement**

```javascript
function area(len) {
    return len*len;
}
```

This function is included without `jsdoc` comments.

**Function Expression**

```javascript
var area;
//Some codes later
/** */
area = function(len) {
    return len*len;
};
```

**Function Expression and Statement**

```javascript
var b={};
/** */
b.area = function(len) {
    return len*len;
}
```

**Function Declaration as Variable**

```javascript
/** */
var x1,
    area = function(len) {
        return len*len;
    },
    x2 =5, x3 =true;
```

Limitation: custom function picks only the first function declaration from the variable list, if together. You can use function expression for every function declared.

**Function Declaration as Object**

```javascript
var c = {
    b : {
        /** */
        area : function(len) {
            return len*len;
        }
    }
};
```
-->

## 建立自訂函式時的准則 {#considerations}

若要在規則編輯器中列出自訂函式，您可以使用下列任一格式：

### 包含或不包含jsdoc註解的函式陳述式

您可以建立包含或不包含jsdoc註解的自訂函式。

```javascript
    function functionName(parameters) 
        {
            // code to be executed
        }
```

如果使用者未將任何JavaScript註解新增至自訂函式，則會依函式名稱在規則編輯器中列出。 不過，建議您加入JavaScript註解，以提升自訂函式的可讀性。


### 箭頭功能與強制JavaScript註解或註解

您可以使用箭頭函式語法來建立自訂函式：

```javascript
    /**
    * test function
    * @name testFunction 
    * @param {string} a parameter description
    * @param {string=} b parameter description
    * @return {string}
    */
    testFunction = (a, b) => {
    return a + b;
    };
    /** */
    testFunction1=(a) => (return a)
    /** */
    testFunction2 = a => a + 100;
    
```

如果使用者沒有將任何JavaScript註解新增到自訂函式，則自訂函式不會列在最適化表單的規則編輯器中。

### 含有強制JavaScript註解或註解的函式運算式

若要列出最適化表單的規則編輯器中的自訂函式，請以下列格式建立自訂函式：

```javascript
    /**
    * test function
    * @name testFunction 
    * @param {string} input1 parameter description
    * @param {string=} input2 parameter description
    * @return {string}
    */
    testFunction = function(input1,input2)
        {
            // code to be executed
        }
```

如果使用者沒有將任何JavaScript註解新增到自訂函式，則自訂函式不會列在最適化表單的規則編輯器中。

### 建立自訂函式的先決條件

開始將自訂函式新增至最適化Forms之前，請確保您的電腦上安裝了下列軟體：

* **純文字編輯器(IDE)**：雖然任何純文字編輯器都可以運作，但Microsoft Visual Studio Code之類的整合式開發環境(IDE)可提供進階功能，讓編輯更輕鬆。

* **Git：**&#x200B;管理程式碼變更需要此版本控制系統。 如果您尚未安裝，請從https://git-scm.com下載。


## 建立自訂函數 {#create-custom-function}

建立自訂函式的步驟如下：
1. [使用AEM Project Archetype建立使用者端程式庫，並新增自訂函式](#create-client-library-archetype)
或
   [透過CRXDE建立自訂函式](#create-add-custom-function)
1. [將使用者端程式庫新增至最適化表單](#add-client-library)
1. [在最適化表單中使用自訂函式](#use-custom-functions)


### 使用AEM專案原型建立使用者端程式庫{#create-client-library-archetype}

您可以使用AEM Project Archetype[&#128279;](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/developing/archetype/using#getting-started)，將使用者端程式庫新增至已建立的專案，以新增自訂函式。
如果您有現有的專案<!--and have already the project structure as shown in the image below,-->，您可以直接將[自訂函式](#create-add-custom-function)新增到您的本機專案。

<!--![custom fuction folder structure](assets/custom-library-folder-structure.png)-->

建立原型專案或使用現有專案後，請建立使用者端程式庫。 若要建立使用者端程式庫，請執行下列步驟：

**新增使用者端資料庫資料夾**

若要新增使用者端程式庫資料夾至您的[AEM專案目錄]，請遵循下列步驟：

1. 在編輯器中開啟[AEM專案目錄]。

   ![自訂函式資料夾結構](assets/custom-library-folder-structure.png)

1. 找到`ui.apps`。
1. 新增資料夾。 例如，新增名為`experience-league`的資料夾。
1. 導覽至`/experience-league/`資料夾並新增`ClientLibraryFolder`。 例如，建立名為`customclientlibs`的使用者端資料庫資料夾。

   位置為： `[AEM project directory]/ui.apps/src/main/content/jcr_root/apps/`

**新增檔案和資料夾至使用者端資料庫資料夾**

將下列專案新增至新增的使用者端程式庫資料夾：

* `.content.xml`檔案
* `js.txt`檔案
* `js`資料夾

`Location is: [AEMaaCS project directory]/ui.apps/src/main/content/jcr_root/apps/experience-league/customclientlibs/`

1. 在`.content.xml`中新增下列幾行程式碼：

   ```javascript
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="cq:ClientLibraryFolder"
   categories="[customfunctionscategory]"/>
   ```

   >[!NOTE]
   >
   > 您可以為`client library folder`和`categories`屬性選擇任何名稱。

1. 在`js.txt`中新增下列幾行程式碼：

   ```javascript
         #base=js
       function.js
   ```

1. 在`js`資料夾中，將JavaScript檔案新增為`function.js`，其中包含自訂函式：

   ```javascript
   /**
       * Calculates Age
       * @name calculateAge
       * @param {object} field
       * @return {string} 
   */
   
   function calculateAge(field) {
   var dob = new Date(field);
   var now = new Date();
   
   var age = now.getFullYear() - dob.getFullYear();
   var monthDiff = now.getMonth() - dob.getMonth();
   
   if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
   age--;
   }
   
   return age;
   }
   ```

1. 儲存檔案。

![自訂函式資料夾結構](assets/custom-function-added-files.png)

**在filter.xml中包含新資料夾**：

1. 導覽至[AEMaaCS專案目錄]中的`/ui.apps/src/main/content/META-INF/vault/filter.xml`檔案。

1. 開啟檔案，並在結尾新增下列行：

   `<filter root="/apps/experience-league" />`
1. 儲存檔案。

   ![自訂函式篩選器xml](assets/custom-function-filterxml.png)

1. 依照[如何建置區段](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype#how-to-build)中提供的步驟，將新建立的使用者端程式庫資料夾建置到您的AEM環境。

## 透過CRXDE建立及部署自訂函式{#create-add-custom-function}

如果您使用最新的AEM Forms和Forms附加元件，可以透過CRXDE建立自訂函式，以使用自訂函式的最新更新。 若要這麼做，請執行下列步驟：

<!--![custom fuction folder structure](assets/custom-library-folder-structure.png)-->


1. 登入`http://server:port/crx/de/index.jsp#`。
1. 在 `/apps` 檔案夾中建立一個檔案夾。例如，建立名為`experience-league`的資料夾。
1. 儲存您的變更。
1. 導覽至建立的資料夾，並建立型別為`cq:ClientLibraryFolder`的節點作為`clientlibs`。
1. 導覽至新建立的`clientlibs`資料夾並新增`allowProxy`和`categories`屬性：

   ![自訂程式庫節點屬性](/help/forms/using/assets/customlibrary-catproperties.png)

   >[!NOTE]
   >
   > 您可以提供任何名稱來取代`customfunctionsdemo`。

1. 儲存您的變更。

1. 在`clientlibs`資料夾下建立名為`js`的資料夾。
1. 在`js`資料夾下建立名為`functions.js`的JavaScript檔案。
1. 在`clientlibs`資料夾下建立名為`js.txt`的檔案。
1. 儲存您的變更。
已建立的檔案夾結構如下所示：

   ![已建立的用戶端資料庫檔案夾結構](/help/forms/using/assets/clientlibrary_folderstructure.png)
1. 連按兩下`functions.js`檔案以開啟編輯器。 此檔案包含自訂函式的程式碼。
將下列程式碼新增至JavaScript檔案，以根據出生日期計算年齡(YYYY-MM-DD)。

   ```javascript
       /**
            * Calculates Age
            * @name calculateAge 
            * @return {string} 
       */
   
       function calculateAge(dateOfBirthString) {
       var dob = new Date(dateOfBirthString);
       var now = new Date();
   
       var age = now.getFullYear() - dob.getFullYear();
       var monthDiff = now.getMonth() - dob.getMonth();
   
       if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
       age--;
       }
   
       return age;
       }
   ```

1. 儲存`function.js`。
1. 瀏覽至`js.txt`並新增下列程式碼：

   ```javascript
       #base=js
       functions.js
   ```

1. 儲存 `js.txt` 檔案。

您可以參考下列[自訂函式](/help/forms/using/assets/customfunction.zip)資料夾。 下載此資料夾並安裝在您的AEM執行個體上。

現在，您可以新增使用者端程式庫，以在最適化表單中使用自訂函式。

## 在最適化表單中新增使用者端程式庫{#add-client-library}

將使用者端程式庫部署到AEM Forms環境後，請在最適化表單中使用其功能。 若要在最適化表單中新增使用者端程式庫

1. 在編輯模式中開啟您的表單。 若要以編輯模式開啟表單，請選取表單並選取&#x200B;**[!UICONTROL 編輯]**。
1. 開啟內容瀏覽器，然後選取最適化表單的「**[!UICONTROL 指引容器]**」元件。
1. 按一下「參考線容器」屬性圖示。 此時會開啟「最適化表單容器」對話框。
1. 開啟&#x200B;**[!UICONTROL 基本]**&#x200B;標籤，並從下拉式清單中選取&#x200B;**[!UICONTROL 使用者端程式庫類別]**&#x200B;的名稱（在此案例中選取`customfunctionscategory`）。

   ![正在新增自訂函式使用者端程式庫](/help/forms/using//assets/custom-function-category-name-core-component.png)

1. 按一下&#x200B;**[!UICONTROL 「完成」]**。

現在，您可以建立規則，以在規則編輯器中使用自訂函式：

![正在新增自訂函式使用者端程式庫](/help/forms/using//assets/calculateage-customfunction.png)

現在，讓我們瞭解如何在AEM Forms 6.5[&#128279;](/help/forms/using/rule-editor-core-components.md#invoke-form-data-model-service-invoke)中使用規則編輯器的Invoke服務來設定和使用自訂函式

## 在最適化表單中使用自訂函式 {#use-custom-functions}

在最適化表單中，您可以在規則編輯器[&#128279;](/help/forms/using/rule-editor-core-components.md)中使用自訂函式。
讓我們將下列程式碼新增至JavaScript檔案（`Function.js`檔案），以根據出生日期(YYYY-MM-DD)計算年齡。 建立自訂函式為`calculateAge()`，它以出生日期作為輸入並傳回年齡：

```javascript
    /**
        * Calculates Age
        * @name calculateAge
        * @param {object} field
        * @return {string} 
    */

    function calculateAge(field) {
    var dob = new Date(field);
    var now = new Date();

    var age = now.getFullYear() - dob.getFullYear();
    var monthDiff = now.getMonth() - dob.getMonth();

    if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
    age--;
    }

    return age;
    }
```

在上述範例中，當使用者以(YYYY-MM-DD)格式輸入出生日期時，會叫用自訂函式`calculateAge`並傳回年齡。

![在規則編輯器中計算Age自訂函式](/help/forms/using/assets/custom-function-calculate-age.png)

讓我們預覽表單，以觀察如何透過規則編輯器實作自訂函式：

![在規則編輯器表單預覽中計算年齡自訂函式](/help/forms/using/assets/custom-function-age-calculate-form.png)

>[!NOTE]
>
> 您可以參考下列[自訂函式](/help/forms/using/assets/customfunctions.zip)資料夾。 使用[封裝管理員](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager)下載此資料夾，並將其安裝在您的AEM執行個體中。

### 支援自訂函式中的非同步函式 {#support-of-async-functions}

非同步自訂函式未出現在規則編輯器清單中。 不過，您也可以在使用同步函式運算式建立的自訂函式中叫用非同步函式。

![同步和非同步自訂函式](/help/forms/using/assets/workflow-for-sync-async-custom-fumction.png)

>[!NOTE]
>
> 在自訂函式中呼叫非同步函式的優點在於，非同步函式允許同時執行多個任務，而自訂函式中使用的每個函式的結果都是如此。

檢視以下程式碼，瞭解如何使用自訂函式叫用非同步函式：

```javascript
    
    async function asyncFunction() {
    const response = await fetch('https://petstore.swagger.io/v2/store/inventory');
    const data = await response.json();
    return data;
    }

    /**
    * callAsyncFunction
    * @name callAsyncFunction callAsyncFunction
    */
    function callAsyncFunction() {
    asyncFunction()
        .then(responseData => {
        console.log('Response data:', responseData);
        })
        .catch(error => {
         console.error('Error:', error);
    });
}
```

在上述範例中，asyncFunction函式是`asynchronous function`。 它透過向`https://petstore.swagger.io/v2/store/inventory`發出`GET`請求來執行非同步操作。 它會使用`await`等待回應、使用`response.json()`將回應本文剖析為JSON，然後傳回資料。 `callAsyncFunction`函式是同步自訂函式，會叫用`asyncFunction`函式並在主控台中顯示回應資料。 雖然`callAsyncFunction`函式是同步的，但它會呼叫非同步asyncFunction函式，並以`then`和`catch`陳述式處理其結果。

若要檢視其運作情況，讓我們新增按鈕，並為按鈕建立規則，此規則會在按鈕按一下時叫用非同步函式。

![為非同步函式建立規則](/help/forms/using/assets/rule-for-async-funct.png)

請參考下方主控台視窗的圖例，以示範當使用者按一下`Fetch`按鈕時，會叫用自訂函式`callAsyncFunction`，進而呼叫非同步函式`asyncFunction`。 Inspect主控台視窗中，檢視按下按鈕時的回應：

![主控台視窗](/help/forms/using/assets/async-custom-funct-console.png)

讓我們來探討自訂函式的功能。

## 自訂功能的各種功能

您可以使用自訂函式，將個人化功能新增至表單。 這些函式支援各種功能，例如使用特定欄位、使用全域欄位或快取。 此彈性可讓您根據組織的需求自訂表格。

### 自訂函式中的欄位和全域範圍物件 {#support-field-and-global-objects}

欄位物件是指表單中的個別元件或元素，例如文字欄位、核取方塊。 全域物件包含唯讀變數，例如表單例項、目標欄位例項，以及在自訂函式內進行表單修改的方法。

>[!NOTE]
>
> `param {scope} globals`必須是最後一個引數，且不會顯示在調適型表單的規則編輯器中。

<!-- Let us look at the following code snippet:

```JavaScript
   
    /**
    * updateDateTime
    * @name updateDateTime
    * @param {object} field
    * @param {scope} globals
    */
    function updateDateTime(field, globals) {
    // Accessing the Date object from the global scope
    var currentDate = new Date();
    // Formatting the date and time
    var formattedDateTime = currentDate.toLocaleString();
    // Updating the field value with the formatted date and time using setProperty.
    globals.functions.setProperty(field, {value: formattedDateTime});
    }
```

In the above code snippet, a custom function named `updateDateTime` takes parameters such as a field object and a global object. The field represents the textbox object where the formatted date and time value is displayed within the form. -->

讓我們瞭解自訂函式如何透過使用不同使用案例的`Contact Us`表單來使用欄位和全域物件。

![連絡我們表單](/help/forms/using/assets/contact-us-form.png)

#### **使用案例**：使用`SetProperty`規則顯示面板

在自訂函式中新增下列程式碼（如[create-custom-function](#create-custom-function)區段中所述），以將表單欄位設為`Required`。

```javascript
    
    /**
    * enablePanel
    * @name enablePanel
    * @param {object} field1
    * @param {object} field2
    * @param {scope} globals 
    */

    function enablePanel(field1,field2, globals)
    {
       if(globals.functions.validate(field1).length === 0)
       {
       globals.functions.setProperty(field2, {visible: true});
       }
    }
```

>[!NOTE]
>
> * 您可以使用位於`[form-path]/jcr:content/guideContainer.model.json`中的可用屬性來設定欄位屬性。
> * 使用Globals物件的`setProperty`方法修改表單時，其本質是非同步的，不會在執行自訂函式時反映出來。

在此範例中，在按一下按鈕時就會進行`personaldetails`面板的驗證。 如果在面板中未偵測到任何錯誤，則按一下按鈕時，另一個面板（`feedback`面板）會變成可見。

讓我們為`Next`按鈕建立規則，以驗證`personaldetails`面板，並讓使用者按一下`Next`按鈕時顯示`feedback`面板。

![設定屬性](/help/forms/using/assets/custom-function-set-property.png)

請參閱下圖以示範，按一下`Next`按鈕後，`personaldetails`面板在哪裡驗證。 如果`personaldetails`中的所有欄位都已驗證，`feedback`面板就會顯示出來。

![設定屬性表單預覽](/help/forms/using/assets/set-property-form-preview.png)

如果「`personaldetails`」面板的欄位中存在錯誤，則按一下「`Next`」按鈕後，這些錯誤將顯示在欄位層級，而「`feedback`」面板將保持隱藏狀態。

![設定屬性表單預覽](/help/forms/using/assets/set-property-panel.png)

#### **使用案例**：驗證欄位。

依照[create-custom-function](#create-custom-function)區段中的說明，在自訂函式中新增下列程式碼，以驗證欄位。

```javascript
    /**
    * validateField
    * @name validateField
    * @param {object} field
    * @param {scope} globals
    */
    function validateField(field,globals)
    {
    
        globals.functions.validate(field);
    
    }   
```

>[!NOTE]
>
> 如果未在`validate()`函式中傳遞引數，則會驗證表單。

在此範例中，自訂驗證模式套用至`contact`欄位。 使用者必須輸入以`10`開頭後接`8`位數的電話號碼。 如果使用者輸入的電話號碼不是以`10`開頭或包含多於`8`位數，則按一下按鈕時會出現驗證錯誤訊息：

![電子郵件地址驗證模式](/help/forms/using/assets/custom-function-validation-pattern.png)

現在，下一步是為`Next`按鈕建立規則，以驗證按鈕點選上的`contact`欄位。

![驗證模式](/help/forms/using/assets/custom-function-validate.png)

請參考下圖以示範，如果使用者輸入的電話號碼不是以`10`開頭，則欄位層級會顯示錯誤訊息：

![電子郵件地址驗證模式](/help/forms/using/assets/custom-function-validate-error-message.png)

如果使用者輸入有效的電話號碼且`personaldetails`面板中的所有欄位都經過驗證，`feedback`面板就會顯示在畫面上：

![電子郵件地址驗證模式](/help/forms/using/assets/validate-form-preview-form.png)

#### **使用案例**：重設面板

依照[create-custom-function](#create-custom-function)區段中的說明，在自訂函式中新增下列程式碼，以重設面板。

```javascript
    /**
    * resetField
    * @name  resetField
    * @param {string} input1
    * @param {object} field
    * @param {scope} globals 
    */
    function  resetField(field,globals)
    {
    
        globals.functions.reset(field);
    
    }
```

>[!NOTE]
>
> 如果未在`reset()`函式中傳遞引數，則會驗證表單。

在此範例中，按一下`Clear`按鈕時，`personaldetails`面板會重設。 下一步是為`Clear`按鈕建立規則，以在按鈕點選時重設面板。

![清除按鈕](/help/forms/using/assets/custom-function-reset-field.png)

請參閱下圖以顯示，如果使用者按一下`clear`按鈕，`personaldetails`面板會重設：

![重設表單](assets/custom-function-reset-form.png)

#### **使用案例**：在欄位層級顯示自訂訊息並將欄位標籤為無效

您可以使用`markFieldAsInvalid()`函式將欄位定義為無效，並在欄位層級設定自訂錯誤訊息。 `fieldIdentifier`值可以是`fieldId`、`field qualifiedName`或`field dataRef`。 名稱為`option`的物件值可以是`{useId: true}`、`{useQualifiedName: true}`或`{useDataRef: true}`。
用於將欄位標示為無效並設定自訂訊息的語法如下：

* `globals.functions.markFieldAsInvalid(field.$id,"[custom message]",{useId: true});`
* `globals.functions.markFieldAsInvalid(field.$qualifiedName, "[custom message]", {useQualifiedName: true});`
* `globals.functions.markFieldAsInvalid(field.$dataRef, "[custom message]", {useDataRef: true});`

在自訂函式中新增下列程式碼（如[create-custom-function](#create-custom-function)區段中所述），以在欄位層級啟用自訂訊息。

```javascript
    /**
    * customMessage
    * @name customMessage
    * @param {object} field
    * @param {scope} globals 
    */
    function customMessage(field, globals) {
    const minLength = 15;
    const comments = field.$value.trim();
    if (comments.length < minLength) {
        globals.functions.markFieldAsInvalid(field.$id, "Comments must be at least 15 characters long.", { useId: true });
    }
}
```

在此範例中，如果使用者在註解文字方塊中輸入少於15個字元，則欄位層級會顯示自訂訊息。

下一步是為`comments`欄位建立規則：

![將欄位標示為無效](/help/forms/using/assets/custom-function-invalid-field.png)

請參閱下列示範，說明在`comments`欄位中輸入負面意見會觸發在欄位層級顯示自訂訊息：

![將欄位標示為無效的預覽表單](/help/forms/using/assets/custom-function-invalidfield-form.png)

如果使用者在評論文字方塊中輸入超過15個字元，則欄位會通過驗證並提交表單：

![將欄位標示為有效的預覽表單](/help/forms/using/assets/custom-function-validfield-form.png)


#### **使用案例**：將變更的資料提交至伺服器

下列程式碼行：
`globals.functions.submitForm(globals.functions.exportData(), false);`用於在操作後提交表單資料。
* 第一個引數是要提交的資料。
* 第二個引數代表是否要在提交前驗證表單。 它是`optional`，預設為`true`。
* 第三個引數是提交的`contentType`，也是選擇性的，預設值為`multipart/form-data`。 其他值可以是`application/json`和`application/x-www-form-urlencoded`。

在自訂函式中新增下列程式碼（如[create-custom-function](#create-custom-function)區段中所述），以在伺服器上提交操作過的資料：

```javascript
    /**
    * submitData
    * @name submitData
    * @param {object} field
    * @param {scope} globals 
    */
    function submitData(globals)
    {
    
    var data = globals.functions.exportData();
    if(!data.comments) {
    data.comments = 'NA';
    }
    console.log('After update:{}',data);
    globals.functions.submitForm(data, false);
    }
```

在此範例中，如果使用者將`comments`文字方塊留空，則在提交表單時會將`NA`提交至伺服器。

現在為提交資料的`Submit`按鈕建立規則：

![提交資料](/help/forms/using/assets/custom-function-submit-data.png)

請參考下圖`console window`以示範，如果使用者將`comments`文字方塊留空，則會在伺服器上提交值為`NA`：

![在主控台視窗提交資料](/help/forms/using/assets/custom-function-submit-data-form.png)

您也可以檢查主控台視窗，以檢視提交給伺服器的資料：

在主控台視窗![Inspect資料](/help/forms/using/assets/custom-function-submit-data-console-data.png)

<!--

#### **Use Case**: Display form submission and failure messages for custom submit action 

Add the following line of code as explained in the [create-custom-function ](#create-custom-function) section, to customize the submission or failure message for form submissions and display the form submission messages in a modal box:

```javascript
/**
 * Handles the success response after a form submission.
 *
 * @param {scope} globals - This object contains a read-only form instance, target field instance, triggered event, and methods for performing form modifications within custom functions.
 * @returns {void}
 */
function customSubmitSuccessHandler(globals) {
    var event = globals.event;
    var submitSuccessResponse = event.payload.body;
    var form = globals.form;

    if (submitSuccessResponse) {
        if (submitSuccessResponse.redirectUrl) {
            window.location.href = encodeURI(submitSuccessResponse.redirectUrl);
        } else if (submitSuccessResponse.thankYouMessage) {
            showModal("success", submitSuccessResponse.thankYouMessage);
        }
    }
}

/**
 * Handles the error response after a form submission.
 *
 * @param {string} customSubmitErrorMessage - The custom error message.
 * @param {scope} globals - This object contains a read-only form instance, target field instance, triggered event, and methods for performing form modifications within custom functions.
 * @returns {void}
 */
function customSubmitErrorHandler(customSubmitErrorMessage, globals) {
    showModal("error", customSubmitErrorMessage);
}
function showModal(type, message) {
    // Remove any existing modals
    var existingModal = document.getElementById("modal");
    if (existingModal) {
        existingModal.remove();
    }

    // Create the modal dialog
    var modal = document.createElement("div");
    modal.setAttribute("id", "modal");
    modal.setAttribute("class", "modal");

    // Create the modal content
    var modalContent = document.createElement("div");
    modalContent.setAttribute("class", "modal-content");

    // Create the modal header
    var modalHeader = document.createElement("div");
    modalHeader.setAttribute("class", "modal-header");
    modalHeader.innerHTML = "<h2>" + (type === "success" ? "Thank You" : "Error") + "</h2>";

    // Create the modal body
    var modalBody = document.createElement("div");
    modalBody.setAttribute("class", "modal-body");
    modalBody.innerHTML = "<p class='" + type + "-message'>" + message + "</p>";

    // Create the modal footer
    var modalFooter = document.createElement("div");
    modalFooter.setAttribute("class", "modal-footer");

    // Create the close button
    var closeButton = document.createElement("button");
    closeButton.setAttribute("class", "close-button");
    closeButton.innerHTML = "Close";
    closeButton.onclick = function() {
        modal.remove();
    };

    // Append the elements to the modal content
    modalFooter.appendChild(closeButton);
    modalContent.appendChild(modalHeader);
    modalContent.appendChild(modalBody);
    modalContent.appendChild(modalFooter);

    // Append the modal content to the modal
    modal.appendChild(modalContent);

    // Append the modal to the document body
    document.body.appendChild(modal);
}
```

In this example, when the user uses the `customSubmitSuccessHandler` and `customSubmitErrorHandler` custom functions, the success and failure messages are displayed in a modal. The JavaScript function `showModal(type, message)` is used to dynamically create and display a modal dialog box on a screen.

Now, create a rule for successful form submission:

![Form submission success](/help/forms/using/assets/form-submission-success.png)

Refer to the illustration below to demonstrate that when the form is submitted successfully, the success message is displayed in a modal:

![Form submission success message](/help/forms/using/assets/form-submission-success-message.png )
 
Similarly, let us create a rule for failed form submissions:

![Form submission fail](/help/forms/using/assets/form-submission-fail.png)

Refer to the illustration below to demonstrate that when the form submission fails, the error message is displayed in a modal:

![Form submission fail message](/help/forms/using/assets/form-submission-fail-message.png )

To display form submission success and failure in a default manner, the `Default submit Form Success Handler` and `Default submit Form Error Handler` functions are available out of the box.

In case, the custom submit action fails to perform as expected in existing AEM projects or forms, refer to the [troubleshooting](#troubleshooting) section.

-->

## 自訂函式的快取支援

Adaptive Forms會在規則編輯器中擷取自訂函式清單時，實作自訂函式的快取，以增強回應時間。 在`error.log`檔案中會顯示訊息為`Fetched following custom functions list from cache`。

具有快取支援的![自訂函式](/help/forms/using/assets/custom-function-cache-error.png)

如果修改自訂函式，快取會失效，並加以剖析。

## 疑難排解 {#troubleshooting}

* 使用者需要確定[核心元件和規格版本已設定為最新版本](https://github.com/adobe/aem-core-forms-components/tree/release/650)。 不過，對於現有的AEM專案和表單，還有其他步驟需要遵循：

   * 對於AEM專案，使用者應使用`submitForm()`取代`submitForm('custom:submitSuccess', 'custom:submitError')`的所有執行個體並部署專案。

   * 針對現有表單，如果自訂提交處理常式無法正常運作，使用者需要使用規則編輯器在&#x200B;**提交**&#x200B;按鈕上開啟並儲存`submitForm`規則。 此動作將表單中`submitForm('custom:submitSuccess', 'custom:submitError')`的現有規則取代為`submitForm()`。


* 如果包含自訂函式程式碼的JavaScript檔案發生錯誤，則自訂函式不會列在最適化表單的規則編輯器中。 若要檢查自訂函式清單，您可以導覽至`error.log`檔案以找出錯誤。 發生錯誤時，自訂函式清單會顯示為空白：

  ![錯誤記錄檔](/help/forms/using/assets/custom-function-list-error-file.png)

  如果沒有錯誤，則會擷取自訂函式並出現在`error.log`檔案中。 在`error.log`檔案中顯示為`Fetched following custom functions list`的訊息：

  使用適當的自訂函式![錯誤記錄檔](/help/forms/using/assets/custom-function-list-fetched-in-error.png)

## 考量事項

* `parameter type`和`return type`不支援`None`。

* 自訂函式清單中不支援的函式包括：
   * 產生器函式
   * 非同步/等待函式
   * 方法定義
   * 類別方法
   * 預設引數
   * Rest引數
