---
title: 非同步提交最適化表單
seo-title: 非同步提交最適化表單
description: 瞭解如何針對最適化表單設定非同步提交。
seo-description: 瞭解如何針對最適化表單設定非同步提交。
uuid: 6555ac63-4d99-4b39-a2d0-a7e61909106b
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 0a0d2109-ee1f-43f6-88e5-1108cd215da6
docset: aem65
translation-type: tm+mt
source-git-commit: 8bc99ed3817398ae358d439a5c1fcc90bbd24327

---


# 非同步提交最適化表單{#asynchronous-submission-of-adaptive-forms}

傳統上，Web表格會設定為同步提交。 在同步提交中，當使用者送出表格時，會將他們重新導向至確認頁面、感謝頁面，或在提交失敗時，會導向錯誤頁面。 不過，如單頁應用程式等現代化網頁體驗越來越受歡迎，而網頁會保持靜態，而主從式互動則會在背景進行。 您現在可以設定非同步提交，以提供此體驗的最適化表單。

在非同步提交中，當使用者提交表格時，開發人員會將表格插入個別的體驗，例如重新導向至網站的其他表格或個別區段。 作者還可以插件單獨的服務，如將資料發送到不同的資料儲存或添加自定義分析引擎。在非同步提交的情況下，自適應表單的行為類似於單頁應用程式，因為表單不會重新載入，或者在伺服器上驗證提交的表單資料時其URL不會更改。

閱讀相關資訊，以取得在最適化表單中非同步提交的詳細資訊。

## 設定非同步提交 {#configure}

要配置自適應表單的非同步提交，請執行以下操作：

1. 在最適化表單製作模式中，選取「表單容器」物件並點選 ![cmppr1](assets/cmppr1.png) ，以開啟其屬性。
1. 在「提交 **[!UICONTROL 屬性]** 」區段中，啟用「 **[!UICONTROL 使用非同步提交」]**。
1. 在「提 **[!UICONTROL 交時]** 」區段中，選取下列其中一個選項以在成功提交表單時執行。

   * **[!UICONTROL 重新導向至URL]**:重新導向至指定的URL或表單提交頁面。 您可以指定URL或瀏覽，以在「重新導向URL/路徑」欄位中 **[!UICONTROL 選擇頁面的路徑]** 。
   * **[!UICONTROL 顯示消息]**:顯示表單提交的訊息。 您可以在「顯示訊息」選項下方的文字欄位中寫入訊息。 文字欄位支援豐富式文字格式。

1. 點選 ![check-button1](assets/check-button1.png) ，以儲存屬性。

## 非同步提交的運作方式 {#how-asynchronous-submission-works}

AEM Forms為表單提交提供現成可用的成功與錯誤處理常式。 處理常式是根據伺服器回應執行的用戶端函式。 當提交表單時，資料會傳送至伺服器進行驗證，而伺服器會傳回回應給用戶端，其中包含提交成功或錯誤事件的相關資訊。 這些資訊會作為參數傳遞給相關處理常式，以執行函式。

此外，表單作者和開發人員可在表單層級編寫規則，以覆寫預設處理常式。 如需詳細資訊，請參 [閱使用規則覆寫預設處理常式](#custom)。

讓我們先檢視伺服器對成功和錯誤事件的回應。

### 提交成功事件的伺服器回應 {#server-response-for-submission-success-event}

提交成功事件的伺服器回應結構如下：

```
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
* 選取的選項可重新導向至頁面或顯示表單中設定的訊息
* 頁面URL或訊息內容（在表單中設定）

成功處理常式會讀取伺服器回應，並據以重新導向至已設定的頁面URL或顯示訊息。

### 提交錯誤事件的伺服器回應 {#server-response-for-submission-error-event}

伺服器對提交錯誤事件的響應結構如下：

```
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

在提交表單時發生錯誤時，伺服器回應包括：

* 錯誤的原因、失敗的CAPTCHA或伺服器端驗證
* 錯誤對象清單，其中包括驗證失敗的欄位的SOM表達式和相應的錯誤消息

錯誤處理程式讀取伺服器響應，並相應地在表單上顯示錯誤消息。

## 使用規則覆寫預設處理常式 {#custom}

表單開發人員和作者可以在表單層級的程式碼編輯器中編寫規則，以覆寫預設處理常式。 針對成功和錯誤事件的伺服器回應會在表單層級公開，開發人員可使用規則來 `$event.data` 存取。

執行下列步驟，在程式碼編輯器中編寫規則，以處理成功和錯誤事件。

1. 在編寫模式中開啟最適化表單、選取任何表單物件，並點選 ![edit-rules1](assets/edit-rules1.png) 以開啟規則編輯器。
1. 在「表 **[!UICONTROL 單對象]** 」樹中選擇「表單」並點選「 **[!UICONTROL 建立」]**。
1. 從模 **** 式選擇下拉式清單中選取「程式碼編輯器」。
1. 在程式碼編輯器中，點選「 **[!UICONTROL 編輯程式碼」]**。 在確認對 **[!UICONTROL 話方塊中]** ，點選「編輯」。
1. 從「 **[!UICONTROL 事件]** 」下拉 **[!UICONTROL 式清單中選擇「成功提交]** 」或「提交 **[!UICONTROL 時發生錯誤]** 」。
1. 為選取的事件編寫規則，並點選「 **[!UICONTROL 完成]** 」以儲存規則。

