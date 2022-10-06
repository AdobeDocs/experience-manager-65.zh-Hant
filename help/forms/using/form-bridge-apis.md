---
title: 適用於HTML5表單的表單橋接API
seo-title: Form Bridge APIs for HTML5 forms
description: 外部應用程式使用FormBridge API連線至XFA行動表單。 API在父窗口上分派FormBridgeInitialized事件。
seo-description: External applications use the FormBridge API to connect to the XFA Mobile Form. The API dispatches a FormBridgeInitialized event on the parent window.
uuid: 0db22649-522b-4857-9ffd-826c52381d15
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: developer-reference
discoiquuid: c05c9911-7c49-4342-89de-61b8b9953c83
exl-id: b598ef47-49ff-4806-8cc7-4394aa068eaa
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 0%

---

# 適用於HTML5表單的表單橋接API {#form-bridge-apis-for-html-forms}

您可以使用表單橋接器API，開啟XFA型HTML5表單與應用程式之間的通訊通道。 表單橋接器API提供 **connect** 建立連線的API。

此 **connect** API接受處理常式作為引數。 在基於XFA的HTML5表單和表單橋之間建立成功連接後，將調用句柄。

您可以使用下列范常式式碼來建立連線。

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
>請務必先建立連線，然後再加入formRuntime.jsp檔案。

## 可用表單橋接器API  {#available-form-bridge-api-nbsp}

**getBridgeVersion()**

返回指令碼庫的版本號

* **輸入**:無
* **輸出**:指令碼庫的版本號
* **錯誤**:無

**isConnected()** 檢查表單狀態是否已初始化

* **輸入**:無
* **輸出**: **True** 如果已初始化XFA表單狀態

* **錯誤**:無

**connect(handler, context)** 建立與FormBridge的連接，並在建立連接並初始化表單狀態後執行函式

* **輸入**:

   * **處理常式**:在表單橋接器連接後執行的函式
   * **內容**:上下文（此）所在的對象 *處理常式* 函式。

* **輸出**:無
* **錯誤**:無

**getDataXML(options)** 以XML格式返回當前表單資料

* **輸入:**

   * **選項：** JavaScript物件包含下列屬性：

      * **錯誤**:錯誤處理程式函式
      * **成功**:成功處理程式函式。 此函式會傳遞包含XML的物件，位於 *資料* 屬性。
      * **內容**:上下文（此）所在的對象 *成功* 函式已設定
      * **validationChecker**:用於調用以檢查從伺服器收到的驗證錯誤的函式。 驗證函式會傳遞錯誤字串的陣列。
      * **formState**:必須傳回資料XML的XFA表單的JSON狀態。 如果未指定，則返回當前呈現的表單的資料XML。

* **輸出：** 無
* **錯誤：** 無

**registerConfig(configName, config)** 使用FormBridge註冊用戶/門戶特定配置。 這些設定會覆寫預設設定。 支援的設定會在設定區段中指定。

* **輸入:**

   * **configName:** 要覆寫的配置名稱

      * **widgetConfig:** 允許用戶用自定義小部件覆蓋窗體中的預設小部件。 設定被覆寫如下：

         *formBridge.registerConfig(&quot;widgetConfig&quot;:{/&amp;ast;configuration&amp;ast;/})*

      * **pagingConfig:** 允許使用者僅覆寫第一頁呈現的預設行為。 設定被覆寫如下：

         *window.formBridge.registerConfig(&quot;pagingConfig&quot;:{pagingDisabled: &lt;true false=&quot;&quot;>, shrinkPageDisabled: &lt;true false=&quot;&quot;> })。*

      * **LoggingConfig:** 允許用戶覆蓋日誌記錄級別、禁用類別的日誌記錄，或者是顯示日誌控制台還是發送到伺服器。 可以按如下方式覆蓋配置：

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

      * **SubmitServiceProxyConfig:** 允許用戶註冊提交和記錄器代理服務。

         ```javascript
         window.formBridge.registerConfig("submitServiceProxyConfig",
         {
         "submitServiceProxy" : "`<submitServiceProxy>`",
         "logServiceProxy": "`<logServiceProxy>`",
         "submitUrl" : "`<submitUrl>`"
         });
         ```
   * **設定：** 設定的值



* **輸出：** 包含中配置的原始值的對象 *資料* 屬性。

* **錯誤：** 無

**hideFields(fieldArray)** 隱藏其Som表達式在fieldArray中提供的欄位。 將指定欄位的存在屬性設定為不可見

* **輸入:**

   * **fieldArray:** 要隱藏的欄位的某些運算式陣列

* **輸出：** 無
* **錯誤：** 無

**showFields(fieldArray)** 顯示其Som表達式在fieldArray中提供的欄位。 將提供欄位的presence屬性設定為可見

* **輸入:**

   * **fieldArray:** 要顯示的欄位的一些運算式陣列

* **輸出：** 無
* **錯誤：** 無

**hideSubmitButtons()** 隱藏窗體中的所有提交按鈕

* **輸入**:無
* **輸出**:無
* **錯誤**:未初始化表單狀態時擲回例外狀況

**getFormState()** 傳回代表表單狀態的JSON

* **輸入：** 無
* **輸出：** 包含JSON的物件，代表中目前的表單狀態 *資料* 屬性。

* **錯誤：** 無

**restoreFormState(options)** 從選項物件中提供的JSON狀態還原表單狀態。 會套用狀態，並在操作完成後呼叫成功或錯誤處理常式

* **輸入:**

   * **選項：** JavaScript物件包含下列屬性：

      * **錯誤**:錯誤處理程式函式
      * **成功**:成功處理程式函式
      * **內容**:上下文（此）所在的對象 *成功* 函式已設定
      * **formState**:表單的JSON狀態。 表單會還原為JSON狀態。

* **輸出：** 無
* **錯誤：** 無

**setFocus(som)** 將焦點置於Som表達式中指定的欄位上

* **輸入：** 要設定焦點的欄位的一些表達式
* **輸出：** 無
* **錯誤：** 擲回例外狀況，以防Som運算式不正確

**setFieldValue(som, value)** 設定給定Som表達式的欄位值

* **輸入:**

   * **som:** 包含欄位某些運算式的陣列。 設定欄位值的部分運算式。
   * **值：** 包含與 **som**&#x200B;陣列。 如果值的資料類型與fieldType不同，則不會修改該值。

* **輸出：** 無
* **錯誤：** 擲回例外狀況（若Som運算式不正確）

**getFieldValue(som)** 返回給定Som表達式的欄位值

* **輸入：** 陣列，包含必須擷取其值之欄位的某些運算式
* **輸出：** 包含結果的對象，如 **資料** 屬性。

* **錯誤：** 無

### getFieldValue()API範例 {#example-of-nbsp-getfieldvalue-api}

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

**getFieldProperties（som，屬性）** 檢索Som表達式中指定欄位的給定屬性的值清單

* **輸入:**

   * **som:** 包含欄位某些運算式的陣列
   * **屬性**:需要值的屬性的名稱

* **輸出：** 包含結果的對象，如 *資料* 屬性

* **錯誤：** 無

**setFieldProperties（som，屬性，值）** 為在Som表達式中指定的所有欄位設定給定屬性的值

* **輸入:**

   * **som:** 陣列，包含必須設定其值的欄位的某些運算式
   * **屬性**:必須設定其值的屬性
   * **值：** 陣列，包含Som運算式中指定欄位的指定屬性值

* **輸出：** 無
* **錯誤：** 無

## 表單橋接器API使用範例 {#sample-usage-of-form-bridge-api}

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
