---
title: 在HTML5表單中建立自訂外觀
description: 您可以將自訂Widget插入Mobile Forms。 您可以擴充現有的jQuery Widget或開發您自己的自訂Widget。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms
exl-id: 76bd1e2d-9e65-452c-8cef-123d28886a62
source-git-commit: 524475c8f9dbd02bae30ecd558a376505fbe0aed
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# 在HTML5表單中建立自訂外觀{#create-custom-appearances-in-html-forms}

您可以將自訂Widget插入Mobile Forms。 您可以擴充現有的jQuery Widget，或使用外觀架構開發您自己的自訂Widget。 XFA引擎使用各種Widget，請參閱 [最適化和HTML5表單的外觀架構](/help/forms/using/introduction-widgets.md) 以取得詳細資訊。

![預設和自訂Widget的範例](assets/custom-widgets.jpg)

預設和自訂Widget的範例

## 整合自訂Widget與HTML5表單 {#integrating-custom-widgets-with-html-forms}

### 建立設定檔  {#create-a-profile-nbsp}

您可以建立設定檔或選擇現有設定檔以新增自訂Widget。 如需建立設定檔的詳細資訊，請參閱 [建立自訂設定檔](/help/forms/using/custom-profile.md).

### 建立 Widget {#create-a-widget}

HTML5表單提供Widget架構的實作，您可以擴充此實作來建立新的Widget。 實作是jQuery Widget *abstractWidget* 可以延伸以撰寫新的Widget。 只有延伸/覆寫下列提及的函式，才能讓新的Widget正常運作。

<table>
 <tbody>
  <tr>
   <td>函式/類別</td>
   <td>說明</td>
  </tr>
  <tr>
   <td>轉譯</td>
   <td>轉譯器函式會傳回Widget預設HTML元素的jQuery物件。 預設HTML元素應為可聚焦型別。 例如， &lt;a&gt;， &lt;input&gt;、和 &lt;li&gt;. 傳回的元素會用作$userControl。 如果$userControl指定上述條件約束，則AbstractWidget類別的函式會如預期般運作，否則某些常見的API （焦點、點按）需要變更。 </td>
  </tr>
  <tr>
   <td>getEventMap</td>
   <td>傳回對應以將HTML事件轉換為XFA事件。 <br /> {<br /> 模糊：XFA_EXIT_EVENT，<br /> }<br /> 此範例顯示模糊是一個HTML事件，而XFA_EXIT_EVENT則對應於XFA事件。 </td>
  </tr>
  <tr>
   <td>getOptionsMap</td>
   <td>傳回提供變更選項時執行之動作詳細資訊的地圖。 索引鍵是提供給Widget的選項，值是偵測到選項變更時所呼叫的函式。 Widget為所有常用選項（value和displayValue除外）提供處理常式</td>
  </tr>
  <tr>
   <td>getcommitvalue</td>
   <td>每當Widget的值儲存在XFAModel中時（例如，在textField的退出事件時），Widget架構就會載入函式。 實作應傳回儲存在Widget中的值。 處理常式會提供選項的新值。</td>
  </tr>
  <tr>
   <td>showValue</td>
   <td>依預設，在輸入事件的XFA中，會顯示欄位的rawValue。 呼叫此函式是為了向使用者顯示rawValue。 </td>
  </tr>
  <tr>
   <td>Showdisplayvalue</td>
   <td>依預設，在退出事件的XFA中，會顯示欄位的formattedValue 。 呼叫此函式是為了向使用者顯示formattedValue。 </td>
  </tr>
 </tbody>
</table>

若要建立您自己的Widget，請在上述建立的設定檔中，加入JavaScript檔案的參照，其中包含覆寫函式和新新增的函式。 例如， *sliderNumericFieldWidget* 是數值欄位的Widget。 若要在標題區段的設定檔中使用Widget，請包含下列行：

```javascript
window.formBridge.registerConfig("widgetConfig" , widgetConfigObject);
```

### 使用XFA Scripting Engine註冊自訂Widget  {#register-custom-widget-with-xfa-scripting-engine-nbsp}

當自訂Widget程式碼準備就緒時，請使用以向指令碼引擎註冊Widget `registerConfig`API for [Form Bridge](/help/forms/using/form-bridge-apis.md). 它以widgetConfigObject作為輸入。

```javascript
window.formBridge.registerConfig("widgetConfig",
        {
        ".<field-identifier>":"<name-of-the-widget>"
        }
    );
```

#### widgetConfigObject {#widgetconfigobject}

Widget設定是以JSON物件（索引鍵值配對的集合）形式提供，其中索引鍵可識別欄位，值代表要與這些欄位搭配使用的Widget。 範例設定看起來像這樣：

```
*{*

*"identifier1" : "customwidgetname",
"identifier2" : "customwidgetname2",
..
}*
```

其中，「identifier」是jQuery CSS選取器，代表特定欄位、特定型別的一組欄位或所有欄位。 以下列出不同情況下識別碼的值：

| 識別碼型別 | 識別碼 | 說明 |
|---|---|---|
| 具有名稱fieldname的特定欄位 | 識別碼：&quot;div.fieldname&quot; | 所有名為「fieldname」的欄位都會使用Widget轉譯。 |
| &#39;type&#39;型別的所有欄位（其中type為NumericField、DateField等）： | 識別碼： &quot;div.type&quot; | 對於Timefield和DateTimeField，型別是textfield，因為這些欄位不受支援。 |
| 所有欄位 | 識別碼： &quot;div.field&quot; |  |
