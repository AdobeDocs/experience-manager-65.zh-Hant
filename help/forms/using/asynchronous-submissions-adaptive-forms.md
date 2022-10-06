---
title: 非同步提交最適化表單
seo-title: Asynchronous submission of adaptive forms
description: 了解如何為最適化表單設定非同步提交。
seo-description: Learn to configure asynchronous submission for adaptive forms.
uuid: 6555ac63-4d99-4b39-a2d0-a7e61909106b
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 0a0d2109-ee1f-43f6-88e5-1108cd215da6
docset: aem65
feature: Adaptive Forms
exl-id: bd0589e2-b15a-4f0e-869c-2da4760b1ff4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 0%

---

# 非同步提交最適化表單{#asynchronous-submission-of-adaptive-forms}

傳統上，網路表單的設定是同步提交。 在同步提交中，當用戶提交表單時，他們會被重定向到確認頁、感謝頁，或者如果提交失敗，則會被重定向到錯誤頁。 不過，單頁應用程式等現代化網頁體驗正日益普及，當用戶端與伺服器互動於背景時，網頁會維持靜態。 您現在可以設定非同步提交，透過最適化表單提供此體驗。

在非同步提交中，當使用者提交表單時，表單開發人員會插入不同的體驗，例如重新導向至網站的其他表單或個別區段。 作者也可以外掛個別服務，例如傳送資料至不同的資料存放區或新增自訂分析引擎。如果非同步提交，適用性表單會像單頁應用程式一樣運作，因為表單沒有重新載入，或提交的表單資料在伺服器上驗證時，其URL不會變更。

如需適用性表單中非同步提交的詳細資訊，請參閱。

## 設定非同步提交 {#configure}

設定最適化表單的非同步提交：

1. 在最適化表單製作模式中，選取「表單容器」物件並點選 ![cmppr1](assets/cmppr1.png) 來開啟其屬性。
1. 在 **[!UICONTROL 提交]** 屬性部分，啟用 **[!UICONTROL 使用非同步提交]**.
1. 在 **[!UICONTROL 提交時]** 部分，選擇以下選項之一，以在成功提交表單時執行。

   * **[!UICONTROL 重新導向至URL]**:重新導向至表單提交時指定的URL或頁面。 您可以指定URL或瀏覽，以選擇 **[!UICONTROL 重新導向URL/路徑]** 欄位。
   * **[!UICONTROL 顯示消息]**:在表單提交時顯示訊息。 您可以在「顯示訊息」選項下方的文字欄位中撰寫訊息。 文字欄位支援RTF格式。

1. 點選 ![check-button1](assets/check-button1.png) 以儲存屬性。

## 非同步提交如何運作 {#how-asynchronous-submission-works}

AEM Forms為表單提交提供現成可用的成功和錯誤處理常式。 處理常式是根據伺服器回應執行的用戶端函式。 提交表單時，將資料發送到伺服器進行驗證，伺服器會向客戶端返回一個響應，其中包含有關提交成功或錯誤事件的資訊。 資訊會以參數形式傳遞至相關處理常式，以執行函式。

此外，表單作者和開發人員可以在表單層級撰寫規則，以覆寫預設處理常式。 如需詳細資訊，請參閱 [使用規則覆蓋預設處理程式](#custom).

讓我們先檢閱伺服器對成功和錯誤事件的回應。

### 提交成功事件的伺服器回應 {#server-response-for-submission-success-event}

提交成功事件的伺服器回應結構如下：

```json
{
  contentType : "<xmlschema or jsonschema>",
  data : "<dataXML or dataJson>" ,
  thankYouOption : <page/message>,
  thankYouContent : "<thank you page url/thank you message>"
}
```

成功提交表單時的伺服器回應包括：

* 表單資料格式類型：XML或JSON
* XML或JSON格式的表單資料
* 已選取重新導向至頁面或顯示訊息的選項（如表單中所設定）
* 頁面URL或訊息內容，如表單中設定

成功處理常式會讀取伺服器回應，並因此重新導向至設定的頁面URL或顯示訊息。

### 提交錯誤事件的伺服器響應 {#server-response-for-submission-error-event}

提交錯誤事件的伺服器回應結構如下：

```json
{
   errorCausedBy : "<CAPTCHA_VALIDATION or SERVER_SIDE_VALIDATION>",

   errors : [
               { "somExpression" : "<SOM Expression>",
                 "errorMessage"  : "<Error Message>"
               },
               ...
             ]
 }
```

提交表單時發生錯誤時的伺服器回應包括：

* 錯誤原因、驗證碼失敗或伺服器端驗證
* 錯誤對象清單，包括驗證失敗的欄位的SOM表達式和相應的錯誤消息

錯誤處理程式讀取伺服器回應，並因此在表單上顯示錯誤訊息。

## 使用規則覆蓋預設處理程式 {#custom}

表單開發人員和作者可以在表單層級的程式碼編輯器中撰寫規則，以覆寫預設處理常式。 成功和錯誤事件的伺服器回應會在表單層級公開，開發人員可使用 `$event.data` 在規則中。

執行下列步驟以在程式碼編輯器中撰寫規則，以處理成功和錯誤事件。

1. 在製作模式中開啟最適化表單、選取任何表單物件，然後點選 ![edit-rules1](assets/edit-rules1.png) 來開啟規則編輯器。
1. 選擇 **[!UICONTROL 表單]** 在「表單對象」樹中，並點選 **[!UICONTROL 建立]**.
1. 選擇 **[!UICONTROL 代碼編輯器]** 從「模式選擇」下拉清單中。
1. 在程式碼編輯器中，點選 **[!UICONTROL 編輯代碼]**. 點選 **[!UICONTROL 編輯]** 在確認對話方塊上。
1. 選擇 **[!UICONTROL 成功提交]** 或 **[!UICONTROL 提交錯誤]** 從 **[!UICONTROL 事件]** 下拉式清單。
1. 為選取的事件撰寫規則，然後點選 **[!UICONTROL 完成]** 來儲存規則。
