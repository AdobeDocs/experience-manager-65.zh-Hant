---
title: 在HTML5表單中建立自訂外觀
seo-title: 在HTML5表單中建立自訂外觀
description: 您可以將自訂Widget插入Mobile Forms。 您可以擴充現有的jQuery Widget，或開發您自己的自訂Widget。
seo-description: 您可以將自訂Widget插入Mobile Forms。 您可以擴充現有的jQuery Widget，或開發您自己的自訂Widget。
uuid: a9013c3d-20c7-45c9-be24-8e9d4525eff8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 17a86543-30d3-4e16-a373-67b46d551da9
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# 在HTML5表單中建立自訂外觀{#create-custom-appearances-in-html-forms}

您可以將自訂Widget插入Mobile Forms。 您可以擴充現有的jQuery Widget，或使用外觀架構開發您自己的自訂Widget。 XFA引擎使用各種Widget，如需詳細資 [訊，請參閱最適化和HTML5表單的](/help/forms/using/introduction-widgets.md) Appearance架構。

![預設和自訂介面工具集的範例](assets/custom-widgets.jpg)

預設和自訂介面工具集的範例

## 將自訂Widget與HTML5表單整合 {#integrating-custom-widgets-with-html-forms}

### 建立描述檔 {#create-a-profile-nbsp}

您可以建立描述檔或選擇現有的描述檔以新增自訂介面工具集。 如需建立描述檔的詳細資訊，請參 [閱建立自訂描述檔](/help/forms/using/custom-profile.md)。

### 建立介面工具集 {#create-a-widget}

HTML5表格提供Widget架構的實作，可加以擴充以建立新Widget。 實作是jQuery Widget abstractWidget ** ，可擴充以編寫新Widget。 新介面工具集只能透過擴充／覆寫下列功能，使其發揮功能。

<table>
 <tbody>
  <tr>
   <td>函式／類</td>
   <td>說明</td>
  </tr>
  <tr>
   <td>渲染</td>
   <td>render函式返回構件的預設HTML元素的jQuery對象。 預設的HTML元素應為可聚焦類型。 例如，&lt;a&gt;、&lt;input&gt;和&lt;li&gt;。 傳回的元素會用作$userControl。 如果$userControl指定上述限制，則AbstractWidget類的函式如預期般運作，否則某些常見API（焦點、按一下）需要變更。 </td>
  </tr>
  <tr>
   <td>getEventMap</td>
   <td>傳回將HTML事件轉換為XFA事件的地圖。 <br /> {<br /> blur:XFA_EXIT_EVENT,<br /><br /> }此示例顯示模糊是HTML事件，XFA_EXIT_EVENT是相應的XFA事件。 </td>
  </tr>
  <tr>
   <td>getOptionsMap</td>
   <td>傳回地圖，其中提供選項變更時要執行的動作的詳細資訊。 鍵是提供給介面工具集的選項，值是每當偵測到該選項的變更時所呼叫的函式。 介面工具集為所有常用選項（value和displayValue除外）提供處理常式</td>
  </tr>
  <tr>
   <td>getCommitValue</td>
   <td>每當Widget的值儲存在XFAModel中時（例如，在textField的exit事件上）,Widget架構就會載入函式。 實作應傳回儲存在介面工具集中的值。 處理常式會隨附選項的新值。</td>
  </tr>
  <tr>
   <td>showValue</td>
   <td>依預設，在XFA中，輸入事件時，會顯示欄位的rawValue。 此函式被呼叫，以向使用者顯示rawValue。 </td>
  </tr>
  <tr>
   <td>showDisplayValue</td>
   <td>依預設，在退出事件時的XFA中，會顯示欄位的formattedValue。 調用此函式可向用戶顯示formattedValue。 </td>
  </tr>
 </tbody>
</table>

若要建立您自己的介面工具集，請在上述建立的描述檔中，包含JavaScript檔案的參考，其中包含覆寫的函式和新增的函式。 例如，sliderNumericFieldWidget *是數值欄位的介面工具集* 。 若要在頁首區段中使用描述檔中的介面工具集，請加入下列行：

```
window.formBridge.registerConfig("widgetConfig" , widgetConfigObject);
```

### 使用XFA指令碼引擎註冊自訂Widget {#register-custom-widget-with-xfa-scripting-engine-nbsp}

當自訂介面工具集程式碼準備就緒時，請使用 `registerConfig`API for [Form Bridge，向指令碼引擎註冊介面工具集](/help/forms/using/form-bridge-apis.md)。 它以widgetConfigObject為輸入。

```
window.formBridge.registerConfig("widgetConfig",
        {
        ".<field-identifier>":"<name-of-the-widget>"
        }
    );
```

#### widgetConfigObject {#widgetconfigobject}

介面工具集設定是以JSON物件（索引鍵值配對的集合）提供，其中索引鍵識別欄位，而值代表要搭配這些欄位使用的介面工具集。 範例配置如下所示：

*{*

*&quot;identifier1&quot; :&quot;customwidgetname&quot;,&quot;identifier2&quot; :&quot;customwidgetname2&quot;,...}*

其中，「identifier」是jQuery CSS選擇器，代表特定欄位、特定類型的欄位集或所有欄位。 以下列出不同情況下識別碼的值：

| 識別碼類型 | 識別碼 | 說明 |
|---|---|---|
| 具有名稱欄位名的特定欄位 | 識別碼：&quot;div.fieldname&quot; | 所有名稱為「fieldname」的欄位都會使用介面工具集呈現。 |
| 所有類型為「type」的欄位（其中類型為NumericField、DateField等）。: | 識別碼：&quot;div.type&quot; | 對於Timefield和DateTimeField，類型為textfield，因為不支援這些欄位。 |
| 所有欄位 | 識別碼：&quot;div.field&quot; |  |

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
