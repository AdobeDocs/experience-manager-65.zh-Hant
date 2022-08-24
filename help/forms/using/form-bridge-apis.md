---
title: 用於HTML5個表單的表單橋API
seo-title: Form Bridge APIs for HTML5 forms
description: 外部應用程式使用FormBridge API連接到XFA移動表單。 API在父窗口上調度FormBridgeInitialized事件。
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

# 用於HTML5個表單的表單橋API {#form-bridge-apis-for-html-forms}

您可以使用表單橋API在基於XFA的HTML5表單和應用程式之間開啟通信通道。 表單橋API提供 **連接** 建立連接的API。

的 **連接** API將處理程式作為參數接受。 在基於XFA的HTML5窗體和窗體橋之間建立成功連接後，將調用句柄。

可以使用以下示例代碼建立連接。

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
>確保在包括formRuntime.jsp檔案之前建立連接。

## 可用表單橋API  {#available-form-bridge-api-nbsp}

**getBridgeVersion()**

返回指令碼庫的版本號

* **輸入**:無
* **輸出**:指令碼庫的版本號
* **錯誤**:無

**isConnected()** 檢查表單狀態是否已初始化

* **輸入**:無
* **輸出**: **真** 是否已初始化XFA窗體狀態

* **錯誤**:無

**connect（handler，上下文）** 建立到FormBridge的連接，並在建立連接並初始化窗體狀態後執行該函式

* **輸入**:

   * **處理程式**:連接窗體橋後要執行的函式
   * **上下文**:對象的上下文（此） *處理程式* 的子菜單。

* **輸出**:無
* **錯誤**:無

**getDataXML（選項）** 以XML格式返回當前表單資料

* **輸入:**

   * **選項：** 包含以下屬性的JavaScript對象：

      * **錯誤**:錯誤處理程式函式
      * **成功**:成功處理程式函式。 此函式傳遞的對象包含XML *資料* 屬性。
      * **上下文**:對象的上下文（此） *成功* 函式
      * **驗證檢查器**:用於調用以檢查從伺服器接收的驗證錯誤的函式。 驗證函式傳遞了錯誤字串陣列。
      * **窗體狀態**:必須返回資料XML的XFA表單的JSON狀態。 如果未指定，則返回當前呈現表單的資料XML。

* **輸出：** 無
* **錯誤：** 無

**registerConfig(configName, config)** 使用FormBridge註冊用戶/門戶特定配置。 這些配置將覆蓋預設配置。 在config節中指定了支援的配置。

* **輸入:**

   * **configName:** 要覆蓋的配置的名稱

      * **widgetConfig（小部件配置）:** 允許用戶使用自定義小部件覆蓋窗體中的預設小部件。 配置被覆蓋如下：

         *formBridge.registerConfig(&quot;widgetConfig&quot;:{/&amp;ast;configuration&amp;ast;/})*

      * **pagingConfig（尋呼配置）:** 允許用戶覆蓋僅呈現第一頁的預設行為。 配置被覆蓋如下：

         *window.formBridge.registerConfig(&quot;pagingConfig&quot;:{pagingDisabled: &lt;true false=&quot;&quot;>,shrinkPageDisabled: &lt;true false=&quot;&quot;> })。*

      * **日誌配置：** 允許用戶覆蓋記錄級別、禁用類別記錄，或者是顯示日誌控制台還是發送到伺服器。 可以按如下方式覆蓋配置：

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

      * **SubmitServiceProxyConfig:** 允許用戶註冊提交和記錄代理服務。

         ```javascript
         window.formBridge.registerConfig("submitServiceProxyConfig",
         {
         "submitServiceProxy" : "`<submitServiceProxy>`",
         "logServiceProxy": "`<logServiceProxy>`",
         "submitUrl" : "`<submitUrl>`"
         });
         ```
   * **配置：** 配置的值



* **輸出：** 包含中配置的原始值的對象 *資料* 屬性。

* **錯誤：** 無

**hideFields(fieldArray)** 隱藏其Som表達式在fieldArray中提供的欄位。 將指定欄位的存在屬性設定為不可見

* **輸入:**

   * **欄位陣列：** 要隱藏的欄位的Som表達式陣列

* **輸出：** 無
* **錯誤：** 無

**showFields(fieldArray)** 顯示其Som表達式在fieldArray中提供的欄位。 將提供的欄位的存在屬性設定為可見

* **輸入:**

   * **欄位陣列：** 要顯示的欄位的Som表達式陣列

* **輸出：** 無
* **錯誤：** 無

**hideSubmitButtons()** 隱藏表單中的所有提交按鈕

* **輸入**:無
* **輸出**:無
* **錯誤**:如果窗體狀態未初始化，則引發異常

**getFormState()** 返回表示窗體狀態的JSON

* **輸入：** 無
* **輸出：** 包含JSON的對象，該JSON表示中的當前窗體狀態 *資料* 屬性。

* **錯誤：** 無

**restoreFormState（選項）** 從選項對象中提供的JSON狀態恢復表單狀態。 應用該狀態，並在操作完成後調用成功或錯誤處理程式

* **輸入:**

   * **選項：** 包含以下屬性的JavaScript對象：

      * **錯誤**:錯誤處理程式函式
      * **成功**:成功處理程式函式
      * **上下文**:對象的上下文（此） *成功* 函式
      * **窗體狀態**:窗體的JSON狀態。 表單已還原為JSON狀態。

* **輸出：** 無
* **錯誤：** 無

**setFocus(som)** 集中於在Som表達式中指定的欄位

* **輸入：** 要設定焦點的欄位的某些表達式
* **輸出：** 無
* **錯誤：** 如果Som表達式不正確，則引發異常

**setFieldValue（som，值）** 設定給定Som表達式的欄位值

* **輸入:**

   * **som:** 包含欄位的Som表達式的陣列。 設定欄位值的som表達式。
   * **值：** 包含與Som表達式相應的值的陣列 **宋**&#x200B;陣列。 如果值的資料類型與fieldType不同，則不修改值。

* **輸出：** 無
* **錯誤：** 如果Som表達式不正確，則引發異常

**getFieldValue(som)** 返回給定Som表達式的欄位值

* **輸入：** 包含需要檢索其值的欄位的Som表達式的陣列
* **輸出：** 包含結果為Array的對象 **資料** 屬性。

* **錯誤：** 無

### getFieldValue()API示例 {#example-of-nbsp-getfieldvalue-api}

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

   * **som:** 包含欄位的Som表達式的陣列
   * **屬性**:需要其值的屬性的名稱

* **輸出：** 包含結果為Array的對象 *資料* 屬性

* **錯誤：** 無

**setFieldProperties（som，屬性，值）** 為Som表達式中指定的所有欄位設定給定屬性的值

* **輸入:**

   * **som:** 包含必須設定其值的欄位的Som表達式的陣列
   * **屬性**:必須設定其值的屬性
   * **值：** 包含Som表達式中指定欄位的給定屬性值的陣列

* **輸出：** 無
* **錯誤：** 無

## 表單橋API的示例使用 {#sample-usage-of-form-bridge-api}

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
