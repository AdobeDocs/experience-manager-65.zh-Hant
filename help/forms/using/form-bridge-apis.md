---
title: HTML5表單的Form Bridge API
seo-title: HTML5表單的Form Bridge API
description: 外部應用程式使用FormBridge API連線至XFA行動表單。 API在父窗口上調度FormBridgeInitialized事件。
seo-description: 外部應用程式使用FormBridge API連線至XFA行動表單。 API在父窗口上調度FormBridgeInitialized事件。
uuid: 0db22649-522b-4857-9ffd-826c52381d15
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: developer-reference
discoiquuid: c05c9911-7c49-4342-89de-61b8b9953c83
translation-type: tm+mt
source-git-commit: 8f90dc4865126d52e04effc9197ef7145b1a167e

---


# HTML5表單的Form Bridge API {#form-bridge-apis-for-html-forms}

您可以使用Form Bridge API來開啟以XFA為基礎的HTML5表單與您的應用程式之間的通訊管道。 表單Bridge API提供 **連接** API以建立連線。

連 **接** API接受處理程式作為參數。 在以XFA為基礎的HTML5表單與Form bridge之間建立成功的連線後，就會呼叫控制代碼。

您可以使用下列范常式式碼來建立連線。

```
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
>請務必先建立連線，再加入formRuntime.jsp檔案。

## 可用的表單Bridge API {#available-form-bridge-api-nbsp}

**getBridgeVersion()**

返回指令碼庫的版本號

* **輸入**:無
* **輸出**:指令碼庫的版本號
* **錯誤**:無

**isConnected()** Checks if Form State has been initialized

* **輸入**:無
* **輸出**:如 **** 果XFA表單狀態已初始化，則為True

* **錯誤**:無

**connect(handler, context)** ，建立與FormBridge的連線，並在建立連線並初始化表單狀態後執行函式

* **輸入**:

   * **處理常式**:連接表單網橋後要執行的函式
   * **內容**:將處理程式函式的上下文(this)設 *置到* 的對象。

* **輸出**:無
* **錯誤**:無

**getDataXML（選項）** 以XML格式傳回目前的表單資料

* **輸入:**

   * **** 選項：JavaScript物件包含下列屬性：

      * **錯誤**:錯誤處理程式函式
      * **成功**:成功處理常式函式。 此函式會傳遞資料屬性中包含XML *的物* 件。
      * **內容**:成功函式的上下文（此）設 *定* 。
      * **validationChecker**:函式，用於調用以檢查從伺服器收到的驗證錯誤。 驗證函式會傳遞一組錯誤字串。
      * **formState**:必須傳回資料XML之XFA表單的JSON狀態。 如果未指定，則返回當前呈現表單的資料XML。

* **** 輸出：無
* **** 錯誤：無

**registerConfig(configName, config)** Registers user / portal specific configurations with FormBridge. 這些配置會覆蓋預設配置。 支援的配置在配置部分中指定。

* **輸入:**

   * **** configName:要覆寫的配置名稱

      * **** widgetConfig:允許使用者使用自訂介面工具集覆寫表單中的預設介面工具集。 配置被覆蓋如下：

         *formBridge.registerConfig(&quot;widgetConfig&quot;:{/&amp;ast;configuration&amp;ast;/})*

      * **** pagingConfig:允許用戶覆蓋僅呈現第一頁的預設行為。 配置被覆蓋如下：

         *window.formBridge.registerConfig(&quot;pagingConfig&quot;:{pagingDisabled:&lt;true| false>,shrinkPageDisabled:&lt;true| false> })。*

      * **** LoggingConfig:允許用戶覆蓋記錄級別、禁用類別的記錄，或是顯示日誌控制台還是發送到伺服器。 可以按如下方式覆蓋配置：

      ```JavaScript
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

      * **** SubmitServiceProxyConfig:允許用戶註冊提交和記錄程式代理服務。

         ```JavaScript
         window.formBridge.registerConfig("submitServiceProxyConfig",
         {
         "submitServiceProxy" : "`<submitServiceProxy>`",
         "logServiceProxy": "`<logServiceProxy>`",
         "submitUrl" : "`<submitUrl>`"
         });
         ```
   * **** config:配置值



* **** 輸出：在data屬性中包含配置的原始 *值* 。

* **** 錯誤：無

**hideFields(fieldArray)** 隱藏其Som運算式在fieldArray中提供的欄位。 將指定欄位的存在屬性設定為不可見

* **輸入:**

   * **** fieldArray:要隱藏的欄位的Som表達式陣列

* **** 輸出：無
* **** 錯誤：無

**showFields(fieldArray)** 顯示其Som表達式在fieldArray中提供的欄位。 將提供欄位的存在屬性設定為可見

* **輸入:**

   * **** fieldArray:要顯示的欄位的Som運算式陣列

* **** 輸出：無
* **** 錯誤：無

**hideSubmitButtons()** 隱藏表單中的所有提交按鈕

* **輸入**:無
* **輸出**:無
* **錯誤**:如果表單狀態未初始化，則拋出異常

**getFormState()傳回表** 示「表單狀態」的JSON

* **** 輸入：無
* **** 輸出：包含JSON的物件，代表資料屬性中的目 *前表* 格狀態。

* **** 錯誤：無

**restoreFormState（選項）** 從選項物件中提供的JSON狀態還原表單狀態。 此狀態會套用，並在作業完成後呼叫成功或錯誤處理常式

* **輸入:**

   * **** 選項：JavaScript物件包含下列屬性：

      * **錯誤**:錯誤處理程式函式
      * **成功**:成功處理常式函式
      * **內容**:成功函式的上下文（此）設 *定* 。
      * **formState**:表單的JSON狀態。 表單會還原為JSON狀態。

* **** 輸出：無
* **** 錯誤：無

**setFocus(som)** Sets focus on the field specified in the Som expression

* **** 輸入：設定焦點的欄位的某些表達式
* **** 輸出：無
* **** 錯誤：在Som運算式不正確時引發例外

**setFieldValue(som, value)** 設定給定Som表達式的欄位值

* **輸入:**

   * **** som:包含欄位的Som表達式的陣列。 設定欄位值的som表達式。
   * **** 值：包含與somarray中提供的Som表達式相應值的 ****&#x200B;陣列。 如果值的資料類型與fieldType不同，則不會修改值。

* **** 輸出：無
* **** 錯誤：在Som運算式不正確的情況下拋出例外

**getFieldValue(som)** 返回給定Som表達式的欄位值

* **** 輸入：包含必須檢索其值的欄位的某些表達式的陣列
* **** 輸出：對象在data屬性中將結果包 **含為** Array。

* **** 錯誤：無

### getFieldValue()API範例 {#example-of-nbsp-getfieldvalue-api}

```JavaScript
var a =  formBridge.getFieldValue(“xfa.form.form1.Subform1.TextField”);
if(a.errors) {
    var err;
     while((err = a.getNextMessage()) != null)
               alert(a.message)
} else {
   alert(a.data[0])
}
```

**getFieldProperties(som, property)** 檢索Som表達式中指定欄位的給定屬性的值清單

* **輸入:**

   * **** som:包含欄位的Som表達式的陣列
   * **屬性**:需要值的屬性的名稱

* **** 輸出：在data屬性中將結果包含為Array *的對象*

* **** 錯誤：無

**setFieldProperties(som, property, values)** 為Som表達式中指定的所有欄位設定給定屬性的值

* **輸入:**

   * **** som:包含某些欄位表達式的陣列，其值必須設定
   * **屬性**:必須設定其值的屬性
   * **** 值：包含Som運算式中指定之欄位之指定屬性值的陣列

* **** 輸出：無
* **** 錯誤：無

## 表單Bridge API的範例使用 {#sample-usage-of-form-bridge-api}

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

**[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)**
