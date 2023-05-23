---
title: 自定義表單事件跟蹤
seo-title: Customizing form event tracking
description: 如果用戶在欄位上花費的時間超過60秒，則觸發欄位訪問事件並將欄位的詳細資訊發送到Adobe SiteCatalyst。
seo-description: If a user spends more than 60 seconds on a field, a fieldvisit event is triggered and the details of the field are sent to Adobe SiteCatalyst.
uuid: 2f790085-2f1a-45be-9a69-6100c76dcae0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 60d67c6b-5994-42ef-b159-ed6edf5cf9d4
exl-id: d0280a15-5d0d-49cf-bce9-ad1c40530eae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 1%

---

# 自定義表單事件跟蹤 {#customizing-form-event-tracking}

現在，可以在啟用分析的自適應表單中跟蹤以下事件：

<table>
 <tbody>
  <tr>
   <th>Event</th>
   <th>可用變數</th>
  </tr>
  <tr>
   <td>呈現</td>
   <td>formName、formTitle、formInstance、source</td>
  </tr>
  <tr>
   <td>放棄</td>
   <td>formName、formTitle、formInstance、panelName、panelTitle</td>
  </tr>
  <tr>
   <td>保存</td>
   <td>formName、formTitle、formInstance、panelName、source</td>
  </tr>
  <tr>
   <td>提交</td>
   <td>formName、formTitle、formInstance、source</td>
  </tr>
  <tr>
   <td>錯誤</td>
   <td>formName、formTitle、fieldName、fieldTitle、panelTitle</td>
  </tr>
  <tr>
   <td>說明</td>
   <td>formName、formTitle、fieldName、fieldTitle、panelTitle</td>
  </tr>
  <tr>
   <td>欄位訪問</td>
   <td>formName、formTitle、fieldName、fieldTitle、panelTitle<br /> </td>
  </tr>
  <tr>
   <td>面板訪問</td>
   <td>formName、formTitle、panelName、panelTitle</td>
  </tr>
 </tbody>
</table>

## 自定義現場訪問事件超時 {#customizing-the-field-visit-event-timeout}

在預設窗AEM體設定中，如果用戶在欄位上花費的時間超過60秒，則 `fieldvisit` 觸發事件，並將欄位的詳細資訊發送到Adobe Analytics。 您可以在配置控制台(/system/console/configMgr)的AEM Forms分析配置下自定義欄位時間跟蹤基準AEM，以增加或減少超時限制。

## 自定義跟蹤事件 {#customizing-the-tracking-events}

可以修改 `trackEvent`函式可用 `/libs/afanalytics/js/custom.js` 檔案，以自定義事件跟蹤。 當正在跟蹤的事件以自適應形式出現時， `trackEvent`函式。 的 `trackEvent` 函式接受兩個參數： `eventName`和 `variableValueMap`。

可以計算 *事件名稱* 和 *變數值映射* 參數以更改事件的跟蹤行為。 例如，您可以選擇在發生一定數量的錯誤事件後將資訊發送到分析伺服器。 您也可以選擇執行以下任意自定義項：

* 可以在發送事件之前設定閾值時間。
* 您可以維護一個狀態來決定操作，例如， *欄位訪問* 基於上次事件的時間戳推送虛擬事件。
* 您可以使用 `pushEvent` 函式，用於將事件發送到分析伺服器 *。*

* 您可以選擇完全不將事件推送到分析伺服器。

### 範例 {#sample}

在以下示例中， *錯誤* 每個事件 *欄位名稱* 屬性已維護。 僅當再次發生錯誤時，事件才會發送到分析伺服器。

```javascript
case 'error':
        if(errorOccurred[variableValueMap.fieldName] == true) {
            pushEvent(eventName, variableValueMap)
        }
        errorOccurred[variableValueMap.fieldName] = true;
        break;
```

## 自定義PanelVisit事件 {#customizing-the-panelvisit-event}

在預設的AEM Forms設定中，每隔60秒就會檢查包含自適應表單的窗口是否處於活動狀態。 如果窗口處於活動狀態，則 `panelVisit`事件觸發到Adobe Analytics。 它有助於確定文檔或表單是否處於活動狀態，並計算在相應表單或文檔上花費的時間。

>[!NOTE]
>
>用於確定活動和計算所花費時間的事件名稱為&quot;panelVisit&quot;。 此事件與上表所列的小組訪問事件不同。

可以修改中提供的scheduleHeartBeatCheck函式 `/libs/afanalytics/js/custom.js` 檔案，以更改或停止以常規時間間隔發送到Adobe Analytics的事件。
