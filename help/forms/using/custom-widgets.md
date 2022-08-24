---
title: 在HTML5窗體中建立自定義外觀
seo-title: Create custom appearances in HTML5 forms
description: 您可以將自定義小部件插入移動Forms。 您可以擴展現有的jQuery小部件或開發自己的自定義小部件。
seo-description: You can plug in custom widgets to a Mobile Forms. You can extend existing jQuery Widgets or develop your own custom widgets.
uuid: a9013c3d-20c7-45c9-be24-8e9d4525eff8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 17a86543-30d3-4e16-a373-67b46d551da9
docset: aem65
feature: Mobile Forms
exl-id: 76bd1e2d-9e65-452c-8cef-123d28886a62
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---

# 在HTML5窗體中建立自定義外觀{#create-custom-appearances-in-html-forms}

您可以將自定義小部件插入移動Forms。 可以擴展現有的jQuery小部件，或使用外觀框架開發自己的自定義小部件。 XFA引擎使用各種小部件，請參見 [用於自適應和HTML5形式的外觀框架](/help/forms/using/introduction-widgets.md) 的上界。

![預設和自定義小部件的示例](assets/custom-widgets.jpg)

預設和自定義小部件的示例

## 將自定義小部件與HTML5窗體整合 {#integrating-custom-widgets-with-html-forms}

### 建立配置檔案  {#create-a-profile-nbsp}

您可以建立配置檔案或選擇現有配置檔案以添加自定義小部件。 有關建立配置檔案的詳細資訊，請參閱 [建立自定義配置檔案](/help/forms/using/custom-profile.md)。

### 建立小部件 {#create-a-widget}

HTML5表單提供了可擴展以建立新小部件的構件框架的實現。 實現是jQuery小部件 *抽象小部件* 可以擴展以編寫新小部件。 只有擴展/覆蓋上述功能，才能使新小部件正常工作。

<table>
 <tbody>
  <tr>
   <td>函式/類</td>
   <td>說明</td>
  </tr>
  <tr>
   <td>呈現</td>
   <td>呈現函式返回小部件的預設HTML元素的jQuery對象。 預設HTML元素應為可聚焦類型。 比如說， &lt;a&gt;。 &lt;input&gt;, &lt;li&gt;。 返回的元素用作$userControl。 如果$userControl指定了上述約束，則AbstractWidget類的函式將按預期工作，否則某些常見API（焦點，按一下）需要更改。 </td>
  </tr>
  <tr>
   <td>getEventMap</td>
   <td>返回將HTML事件轉換為XFA事件的映射。 <br /> { 0}<br /> 模糊：XFA_EXIT_EVENT,<br /> }<br /> 此示例說明模糊是HTML事件，XFA_EXIT_EVENT是相應的XFA事件。 </td>
  </tr>
  <tr>
   <td>getOptionsMap</td>
   <td>返回一個映射，該映射提供選項更改時要執行的操作的詳細資訊。 鍵是提供給小部件的選項，值是每當檢測到該選項的更改時調用的函式。 該構件為所有常用選項（value和displayValue除外）提供了處理程式</td>
  </tr>
  <tr>
   <td>getCommitValue</td>
   <td>只要將小部件的值保存在XFAModel中（例如，在textField的exit事件上）,Widget框架就會載入該函式。 實現應返回小部件中保存的值。 該處理程式提供了該選項的新值。</td>
  </tr>
  <tr>
   <td>showValue</td>
   <td>預設情況下，在輸入事件時的XFA中，將顯示該欄位的rawValue。 調用此函式向用戶顯示rawValue。 </td>
  </tr>
  <tr>
   <td>showDisplayValue</td>
   <td>預設情況下，在XFA on exit事件中，將顯示該欄位的formatedValue。 調用此函式向用戶顯示formattedValue。 </td>
  </tr>
 </tbody>
</table>

要建立您自己的小部件，請在上面建立的配置檔案中包括JavaScript檔案的引用，該檔案包含被覆蓋的函式和新添加的函式。 例如， *sliderNumericFieldWidget* 是數字欄位的小部件。 要在頁眉部分中使用配置檔案中的構件，請包括以下行：

```javascript
window.formBridge.registerConfig("widgetConfig" , widgetConfigObject);
```

### 使用XFA指令碼引擎註冊自定義小部件  {#register-custom-widget-with-xfa-scripting-engine-nbsp}

當自定義構件代碼準備就緒時，使用 `registerConfig`API [窗體橋](/help/forms/using/form-bridge-apis.md)。 它以widgetConfigObject為輸入。

```javascript
window.formBridge.registerConfig("widgetConfig",
        {
        ".<field-identifier>":"<name-of-the-widget>"
        }
    );
```

#### 小部件ConfigObject {#widgetconfigobject}

小部件配置是作為JSON對象（鍵值對的集合）提供的，其中鍵標識欄位，值表示要與這些欄位一起使用的小部件。 配置示例如下：

```
*{*

*"identifier1" : "customwidgetname",
"identifier2" : "customwidgetname2",
..
}*
```

其中，「identifier」是jQuery CSS選擇器，它表示特定欄位、特定類型的一組欄位或所有欄位。 下面列出了不同情況下標識符的值：

| 標識符的類型 | 識別碼 | 說明 |
|---|---|---|
| 具有名稱欄位名稱的特定欄位 | 標識符：&quot;div.fieldname&quot; | 使用小部件呈現名為「fieldname」的所有欄位。 |
| 類型為「type」的所有欄位（其中類型為NumericField、DateField等）。: | 標識符：&quot;div.type&quot; | 對於Timefield和DateTimeField，類型為textfield，因為不支援這些欄位。 |
| 所有欄位 | 標識符：&quot;div.field&quot; |  |
