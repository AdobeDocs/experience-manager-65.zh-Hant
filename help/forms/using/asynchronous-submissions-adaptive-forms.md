---
title: 非同步提交最適化表單
description: 瞭解如何設定最適化表單的非同步提交。
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms
exl-id: bd0589e2-b15a-4f0e-869c-2da4760b1ff4
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 11%

---

# 非同步提交最適化表單{#asynchronous-submission-of-adaptive-forms}

<span class="preview">Adobe 建議使用新式且可擴充的資料擷取[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，用來[建立新的最適化表單](/help/forms/using/create-an-adaptive-form-core-components.md)或[將最適化表單新增到 AEM Sites 頁面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文會介紹使用基礎元件編寫最適化表單的舊方法。</span>

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/asynchronous-submissions-adaptive-forms.html) |
| AEM 6.5 | 本文章 |

傳統上，網路表單會設定為同步提交。 在同步提交中，當使用者提交表單時，系統會將他們重新導向至確認頁面、感謝頁面，或者如果提交失敗，則導向至錯誤頁面。 不過，單頁應用程式等現代網頁體驗越來越受歡迎，這是因為網頁會維持靜態，而使用者端與伺服器之間的互動會在背景進行。 您現在可以設定非同步提交，以最適化表單提供此體驗。

在非同步提交中，當使用者提交表單時，表單開發人員會插入單獨的體驗，例如重新導向到其他表單或網站的單獨區段。 作者也可以外掛個別的服務，例如傳送資料至不同的資料存放區，或新增自訂分析引擎。 如果有非同步提交，則最適化表單的行為就像單頁應用程式，因為提交表單的資料在伺服器上驗證時，表單不會重新載入或其URL不會變更。

請閱讀下文，瞭解最適化表單非同步提交的詳細資訊。

## 設定非同步提交 {#configure}

若要設定最適化表單的非同步提交：

1. 在調適型表單製作模式中，選取「表單容器」物件，然後選取「 」 ![cmppr1](assets/cmppr1.png) 以開啟其屬性。
1. 在 **[!UICONTROL 提交]** 屬性區段，啟用 **[!UICONTROL 使用非同步提交]**.
1. 在 **[!UICONTROL 提交時]** 區段，選取下列其中一個選項以在成功提交表單時執行。

   * **[!UICONTROL 重新導向至URL]**：在提交表單時重新導向至指定的URL或頁面。 您可以指定URL或瀏覽以選擇 **[!UICONTROL 重新導向URL/路徑]** 欄位。
   * **[!UICONTROL 顯示訊息]**：在提交表單時顯示訊息。 您可以在[顯示訊息]選項下方的文字欄位中寫入訊息。 文字欄位支援RTF格式。

1. 選取 ![check-button1](assets/check-button1.png) 以儲存屬性。

## 非同步提交的運作方式 {#how-asynchronous-submission-works}

AEM Forms 為表單提交提供現成可用的成功和錯誤處理常式。處理常式是根據伺服器回應執行的用戶端函數。提交表單時，資料會傳送至伺服器進行驗證，伺服器會傳回回應給使用者端，其中包含提交成功或錯誤事件的相關資訊。 此資訊會以引數形式傳遞至相關處理常式，以執行函式。

此外，表單作者和開發人員可在表單層級撰寫規則以覆寫預設處理常式。 如需詳細資訊，請參閱 [使用規則覆寫預設處理常式](#custom).

讓我們先檢閱伺服器回應，以瞭解成功和錯誤事件。

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

如果表單提交成功，則伺服器回應包括：

* 表單資料格式型別： XML或JSON
* XML或JSON格式的表單資料
* 選取此選項以重新導向至頁面，或依據表單的設定顯示訊息
* 頁面URL或訊息內容（如表單中所設定）

成功處理常式會讀取伺服器回應，並據以重新導向至設定的頁面URL或顯示訊息。

### 提交錯誤事件的伺服器回應 {#server-response-for-submission-error-event}

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

如果表單提交中發生錯誤，伺服器回應會包括：

* 錯誤的原因，驗證碼或伺服器端驗證失敗
* 錯誤物件清單，包括驗證失敗的欄位的SOM運算式和對應的錯誤訊息

錯誤處理常式會讀取伺服器回應，並在表單上顯示錯誤訊息。

## 使用規則覆寫預設處理常式 {#custom}

表單開發人員和作者可以在表單層級的程式碼編輯器中撰寫規則來覆寫預設處理常式。 成功和錯誤事件的伺服器回應會公開於表單層級，開發人員可使用進行存取 `$event.data` 在規則中。

執行以下步驟來在程式碼編輯器中撰寫規則，以處理成功和錯誤事件。

1. 在撰寫模式中開啟最適化表單，選取任何表單物件，然後選取 ![edit-rules1](assets/edit-rules1.png) 以開啟規則編輯器。
1. 選取 **[!UICONTROL 表單]** 在「表單物件」樹狀結構中，選取 **[!UICONTROL 建立]**.
1. 選取 **[!UICONTROL 代碼編輯器]** 從模式選取下拉式清單。
1. 在程式碼編輯器中，選取 **[!UICONTROL 編輯程式碼]**. 選取 **[!UICONTROL 編輯]** 在確認對話方塊上。
1. 選擇 **[!UICONTROL 提交成功]** 或 **[!UICONTROL 提交時發生錯誤]** 從 **[!UICONTROL 事件]** 下拉式清單。
1. 為選取的事件撰寫規則，然後選取 **[!UICONTROL 完成]** 以儲存規則。
