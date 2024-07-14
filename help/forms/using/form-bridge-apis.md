---
title: 適用於HTML5表單的Form Bridge API
description: 外部應用程式會使用FormBridge API連線至XFA行動表單。 API會在父視窗上排程FormBridgeInitialized事件。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: developer-reference
exl-id: b598ef47-49ff-4806-8cc7-4394aa068eaa
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 0%

---

# 適用於HTML5表單的Form Bridge API {#form-bridge-apis-for-html-forms}

您可以使用Form Bridge API開啟XFA型HTML5表單與您的應用程式之間的通訊通道。 表單Bridge API提供&#x200B;**連線** API來建立連線。

**connect** API接受處理常式做為引數。 在XFA型HTML5表單與表單Bridge之間成功建立連線後，就會叫用控制代碼。

您可以使用以下範常式式碼來建立連線。

```javascript
// Example showing how to connect to FormBridge
window.addEventListener("FormBridgeInitialized",
                                function(event) {
                                    var fb = event.detail.formBridge;
                                    fb.connect(function() {
                                           //use form bridge functions
                         })
                            })
```

>[!NOTE]
>
>在加入formRuntime.jsp檔案之前，請確定您已建立連線。

## 可透過Bridge API使用  {#available-form-bridge-api-nbsp}

**getBridgeVersion()**

傳回指令碼程式庫的版本號碼

* **輸入**：無
* **輸出**：指令碼程式庫的版本號碼
* **錯誤**：無

**isConnected()**&#x200B;檢查表單狀態是否已初始化

* **輸入**：無
* 如果XFA表單狀態已初始化，**輸出**： **True**

* **錯誤**：無

**connect(handler， context)**&#x200B;連線至FormBridge，並在連線完成且表單狀態初始化後執行函式

* **輸入**：

   * **處理常式**：在連線表單Bridge之後要執行的函式
   * **context**： *處理常式*&#x200B;函式內容（這個）設定的物件。

* **輸出**：無
* **錯誤**：無

**getDataXML(options)**&#x200B;傳回XML格式的目前表單資料

* **輸入：**

   * **選項：**&#x200B;包含下列屬性的JavaScript物件：

      * **錯誤**：錯誤處理常式函式
      * **success**：成功處理常式函式。 此函式傳遞的物件包含&#x200B;*資料*&#x200B;屬性中的XML。
      * **context**： *success*&#x200B;函式內容（這個）設定的物件
      * **validationChecker**：用於呼叫以檢查從伺服器收到的驗證錯誤的函式。 驗證函式傳遞錯誤字串的陣列。
      * **formState**：必須傳回資料XML之XFA表單的JSON狀態。 如果未指定，它會傳回目前轉譯之表單的資料XML。

* **輸出：**&#x200B;無
* **錯誤：**&#x200B;無

**registerConfig(configName， config)**&#x200B;向FormBridge註冊使用者/入口網站的特定設定。 這些設定會覆寫預設設定。 支援的設定會在設定區段中指定。

* **輸入：**

   * **configName：**&#x200B;要覆寫的組態名稱

      * **widgetConfig：**&#x200B;允許使用者以自訂widget覆寫表單中的預設widget。 設定會覆寫，如下所示：

        *formBridge.registerConfig(&quot;widgetConfig&quot;：{/&amp;amp；ast；configuration&amp;amp；ast；/})*

      * **pagingConfig：**&#x200B;允許使用者覆寫僅呈現第一頁的預設行為。 設定會覆寫，如下所示：

        *window.formBridge.registerConfig(&quot;pagingConfig&quot;：{pagingDisabled： &lt;true | false>， shrinkPageDisabled： &lt;true | false> })。*

      * **LoggingConfig：**&#x200B;允許使用者覆寫記錄層級、停用類別的記錄，或者是否要顯示記錄主控台或傳送至伺服器。 設定可以覆寫，如下所示：

     ```javascript
     formBridge.registerConfig{
       "LoggerConfig" : {
     {
     "on":`<true *| *false>`,
     "category":`<array of categories>`,
     "level":`<level of categories>`, "
     type":`<"console"/"server"/"both">`
     }
       }
     ```

      * **SubmitServiceProxyConfig：**&#x200B;允許使用者註冊提交和記錄器Proxy服務。

        ```javascript
        window.formBridge.registerConfig("submitServiceProxyConfig",
        {
        "submitServiceProxy" : "`<submitServiceProxy>`",
        "logServiceProxy": "`<logServiceProxy>`",
        "submitUrl" : "`<submitUrl>`"
        });
        ```

   * **設定：**&#x200B;設定的值

* **輸出：**&#x200B;物件包含&#x200B;*資料*&#x200B;屬性中組態的原始值。

* **錯誤：**&#x200B;無

**hideFields(fieldArray)**&#x200B;隱藏fieldArray中提供Som運算式的欄位。 將指定欄位的presence屬性設定為隱藏

* **輸入：**

   * **fieldArray：**&#x200B;要隱藏之欄位的Som運算式陣列

* **輸出：**&#x200B;無
* **錯誤：**&#x200B;無

**showFields(fieldArray)**&#x200B;顯示fieldArray中提供Som運算式的欄位。 將所提供欄位的presence屬性設定為可見

* **輸入：**

   * **fieldArray：**&#x200B;要顯示之欄位的Som運算式陣列

* **輸出：**&#x200B;無
* **錯誤：**&#x200B;無

**hideSubmitButtons()**&#x200B;隱藏表單中的所有提交按鈕

* **輸入**：無
* **輸出**：無
* **錯誤**：如果表單狀態未初始化，則會擲回例外狀況

**getFormState()**&#x200B;傳回代表表單狀態的JSON

* **輸入：**&#x200B;無
* **輸出：**&#x200B;物件，包含代表&#x200B;*data*&#x200B;屬性中目前表單狀態的JSON。

* **錯誤：**&#x200B;無

**restoreFormState(options)**&#x200B;從選項物件中提供的JSON狀態還原表單狀態。 狀態已套用，並在作業完成後呼叫成功或錯誤處理常式

* **輸入：**

   * **選項：**&#x200B;包含下列屬性的JavaScript物件：

      * **錯誤**：錯誤處理常式函式
      * **success**：成功處理常式函式
      * **context**： *success*&#x200B;函式內容（這個）設定的物件
      * **formState**：表單的JSON狀態。 表單會還原為JSON狀態。

* **輸出：**&#x200B;無
* **錯誤：**&#x200B;無

**setFocus (som)**&#x200B;將焦點設定在Som運算式中指定的欄位

* **輸入：**&#x200B;要設定焦點的欄位的Som運算式
* **輸出：**&#x200B;無
* **錯誤：**&#x200B;如果Som運算式不正確，則擲回例外狀況

**setFieldValue (som， value)**&#x200B;設定指定Som運算式的欄位值

* **輸入：**

   * **som：**&#x200B;包含欄位的Som運算式的陣列。 用來設定欄位值的som運算式。
   * **值：**&#x200B;陣列包含對應於&#x200B;**som**&#x200B;陣列中所提供的Som運算式的值。 如果值的資料型別與fieldType不同，則不會修改值。

* **輸出：**&#x200B;無
* **錯誤：**&#x200B;如果有不正確的Som運算式，則擲回例外狀況

**getFieldValue (som)**&#x200B;傳回指定Som運算式的欄位值

* **輸入：**&#x200B;陣列包含必須擷取其值的欄位的Som運算式
* **輸出：**&#x200B;物件，在&#x200B;**資料**&#x200B;屬性中包含結果為Array。

* **錯誤：**&#x200B;無

### getFieldValue() API範例 {#example-of-nbsp-getfieldvalue-api}

```JavaScript
var a =  formBridge.getFieldValue("xfa.form.form1.Subform1.TextField");
if(a.errors) {
    var err;
     while((err = a.getNextMessage()) != null)
               alert(a.message)
} else {
   alert(a.data[0])
}
```

**getFieldProperties(som， property)**&#x200B;擷取Som運算式中所指定欄位之指定屬性的值清單

* **輸入：**

   * **som：**&#x200B;包含欄位的Som運算式的陣列
   * **屬性**：需要其值的屬性名稱

* **輸出：**&#x200B;物件包含結果為&#x200B;*資料*&#x200B;屬性中的陣列

* **錯誤：**&#x200B;無

**setFieldProperties(som， property， values)**&#x200B;針對Som運算式中指定的所有欄位，設定指定屬性的值

* **輸入：**

   * **som：**&#x200B;陣列包含必須設定其值的欄位的Som運算式
   * **屬性**：必須設定其值的屬性
   * **值：**&#x200B;陣列包含Som運算式中所指定欄位之指定屬性的值

* **輸出：**&#x200B;無
* **錯誤：**&#x200B;無

## 表單Bridge API的範例用法 {#sample-usage-of-form-bridge-api}

```JavaScript
// Example 1: FormBridge.restoreFormState
  function loadFormState() {
    var suc = function(obj) {
             //success
            }
    var err = function(obj) {
           while(var t = obj.getNextMessage()) {
         $("#errorDiv").append("<div>"+t.message+"</div>");
           }
           }
        var _formState = // load form state from storage
    formBridge.restoreFormState({success:suc,error:err,formState:_formState}); // not passing a context means that this will be formBridge itself. Validation errors will be checked.
  }

//--------------------------------------------------------------------------------------------------

//Example 2: FormBridge.submitForm
  function SubmitForm() {
    var suc = function(obj) {
             var data = obj.data;
         // submit the data to a url;
            }
    var err = function(obj) {
           while(var t = obj.getNextMessage()) {
         $("#errorDiv").append("<div>"+t.message+"</div>");
           }
           }
    formBridge.submitForm({success:suc,error:err}); // not passing a context means that this will be formBridge itself. Validation errors will be checked.
  }
```
