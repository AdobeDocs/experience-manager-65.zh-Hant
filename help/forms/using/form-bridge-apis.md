---
title: 適用於HTML5表單的表單橋接器API
seo-title: 適用於HTML5表單的表單橋接器API
description: 外部應用程式使用FormBridge API連線至XFA行動表單。 API在父窗口上分派FormBridgeInitialized事件。
seo-description: 外部應用程式使用FormBridge API連線至XFA行動表單。 API在父窗口上分派FormBridgeInitialized事件。
uuid: 0db22649-522b-4857-9ffd-826c52381d15
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: developer-reference
discoiquuid: c05c9911-7c49-4342-89de-61b8b9953c83
exl-id: b598ef47-49ff-4806-8cc7-4394aa068eaa
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 0%

---

# HTML5表單的表單橋接API {#form-bridge-apis-for-html-forms}

您可以使用表單橋接器API，開啟XFA型HTML5表單與應用程式之間的通訊通道。 表單橋API提供&#x200B;**connect** API以建立連線。

**connect** API接受處理程式作為參數。 在以XFA為基礎的HTML5表單與表單橋接器之間建立成功連線後，會叫用控點。

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
* **輸出**: **** 若XFA表單狀態已初始化，則設為true

* **錯誤**:無

**connect(handler, context)** 建立與FormBridge的連線，並在建立連線並初始化表單狀態後執行函式

* **輸入**:

   * **處理常式**:在表單橋接器連接後執行的函式
   * **內容**:handlerfunction的上下文（此）設定到 ** 的對象。

* **輸出**:無
* **錯誤**:無

**getDataXML(options)** 以XML格式傳回目前的表單資料

* **輸入:**

   * **選項：** 包含下列屬性的JavaScript物件：

      * **錯誤**:錯誤處理程式函式
      * **成功**:成功處理程式函式。此函式傳遞的對象包含&#x200B;*data*&#x200B;屬性中的XML。
      * **內容**:成功函式的上下文（此）設定 ** 到的對象
      * **validationChecker**:用於調用以檢查從伺服器收到的驗證錯誤的函式。驗證函式會傳遞錯誤字串的陣列。
      * **formState**:必須傳回資料XML的XFA表單的JSON狀態。如果未指定，則返回當前呈現的表單的資料XML。

* **輸出：** 無
* **錯誤：** 無

**registerConfig(configName, config)** 使用FormBridge註冊使用者/入口專屬設定。這些設定會覆寫預設設定。 支援的設定會在設定區段中指定。

* **輸入:**

   * **configName:** 要覆寫的設定名稱

      * **widgetConfig:** 允許使用者使用自訂介面工具集覆寫表單中的預設介面工具集。設定被覆寫如下：

         *formBridge.registerConfig(&quot;widgetConfig&quot;:{/&amp;ast;configuration&amp;ast;/})*

      * **pagingConfig:** 允許使用者覆寫僅呈現第一頁的預設行為。設定被覆寫如下：

         *window.formBridge.registerConfig(&quot;pagingConfig&quot;:{pagingDisabled: &lt;true>, shrinkPageDisabled: &lt;true> })。*

      * **LoggingConfig:** 允許用戶覆蓋日誌記錄級別、禁用類別的日誌記錄，或是顯示日誌控制台還是發送到伺服器。可以按如下方式覆蓋配置：

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

      * **SubmitServiceProxyConfig:** 允許使用者註冊提交和記錄器代理服務。

         ```javascript
         window.formBridge.registerConfig("submitServiceProxyConfig",
         {
         "submitServiceProxy" : "`<submitServiceProxy>`",
         "logServiceProxy": "`<logServiceProxy>`",
         "submitUrl" : "`<submitUrl>`"
         });
         ```
   * **設定：** 設定的值



* **輸出：** 物件，包含dataproperty中設定的原始 ** 值。

* **錯誤：** 無

**hideFields(fieldArray)** 隱藏其Som表達式在fieldArray中提供的欄位。將指定欄位的存在屬性設定為不可見

* **輸入:**

   * **fieldArray:** 要隱藏欄位的某些運算式的陣列

* **輸出：** 無
* **錯誤：** 無

**showFields(fieldArray)** 顯示其Som表達式在fieldArray中提供的欄位。將提供欄位的presence屬性設定為可見

* **輸入:**

   * **fieldArray:** 要顯示欄位的一些運算式的陣列

* **輸出：** 無
* **錯誤：** 無

**hideSubmitButtons()** 隱藏表單中的所有提交按鈕

* **輸入**:無
* **輸出**:無
* **錯誤**:未初始化表單狀態時擲回例外狀況

**getFormState()** 傳回代表表單狀態的JSON

* **輸入：** 無
* **輸出：** 物件，其中包含JSON，代表dataproperty中目前的表 ** 單狀態。

* **錯誤：** 無

**restoreFormState(options)** 從options物件中提供的JSON狀態還原表單狀態。會套用狀態，並在操作完成後呼叫成功或錯誤處理常式

* **輸入:**

   * **選項：** 包含下列屬性的JavaScript物件：

      * **錯誤**:錯誤處理程式函式
      * **成功**:成功處理程式函式
      * **內容**:成功函式的上下文（此）設定 ** 到的對象
      * **formState**:表單的JSON狀態。表單會還原為JSON狀態。

* **輸出：** 無
* **錯誤：** 無

**setFocus(som)** 將焦點置於Som運算式中指定的欄位

* **輸入：** 要設定焦點之欄位的某些運算式
* **輸出：** 無
* **錯誤：** 擲回例外狀況，以防Som運算式不正確

**setFieldValue(som, value)** 設定給定Som表達式的欄位值

* **輸入:**

   * **som:** 包含欄位某些運算式的陣列。設定欄位值的部分運算式。
   * **value:** 包含與somarray中提供的Som運算式對應之值的 ****&#x200B;陣列。如果值的資料類型與fieldType不同，則不會修改該值。

* **輸出：** 無
* **錯誤：** 若Som運算式不正確，則擲回例外

**getFieldValue(som)** 傳回指定Som運算式的欄位值

* **輸入：** 陣列，包含必須擷取其值之欄位的某些運算式
* **輸出：** 在dataproperty中包含結果為Array的 **** 物件。

* **錯誤：** 無

### getFieldValue()API {#example-of-nbsp-getfieldvalue-api}示例

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

**getFieldProperties（som，屬性）** 檢索Som表達式中指定欄位的給定屬性的值清單

* **輸入:**

   * **som:** 包含欄位的Som運算式的陣列
   * **屬性**:需要值的屬性的名稱

* **輸出：** 在dataproperty中包含結果為Array的物 ** 件

* **錯誤：** 無

**setFieldProperties(som, property, values)** 為Som表達式中指定的所有欄位設定給定屬性的值

* **輸入:**

   * **som:** 陣列，包含必須設定其值的欄位的某些運算式
   * **屬性**:必須設定其值的屬性
   * **value:** 陣列，包含Som運算式中指定欄位的指定屬性值

* **輸出：** 無
* **錯誤：** 無

## 表單網橋API {#sample-usage-of-form-bridge-api}使用範例

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
