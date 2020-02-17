---
title: 新的演算和提交服務
seo-title: 新的演算和提交服務
description: 在Workbench中定義演算和提交服務，以根據XDP表單的存取裝置，將XDP表單轉換為HTML或PDF。
seo-description: 在Workbench中定義演算和提交服務，以根據XDP表單的存取裝置，將XDP表單轉換為HTML或PDF。
uuid: 7f8348a1-753c-4dab-87d5-4a4a301198dd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6a32d240-c6a6-4937-a31f-7a5ec3c60b1f
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# 新的演算和提交服務{#new-render-and-submit-service}

## 簡介 {#introduction}

在Workbench中，當您定義工 `AssignTask` 序時，請指定特定表單（XDP或PDF表單）。 此外，也可透過動作設定檔指定一組Render和Submit服務。

XDP可轉譯為PDF表單或HTML表單。 新功能包括：

* 將XDP表單演算並送出為HTML
* 在桌上型電腦上以PDF格式演算XDP表單，在行動裝置上以HTML格式（例如iPad）提交XDP表單

### 新的HTML Forms服務 {#new-html-forms-service}

全新的HTML Forms服務運用Forms中的新功能，支援將XDP表單轉換為HTML。 新的HTML Forms服務公開下列方法：

```java
/*
 * Generates a URL (for the HTML Form) to be passed to client, given a TaskContext.
 * The output of this API is something like this - /lc/content/xfaforms/profiles/default.ws.html?ContentRoot=repository://Applications/MyApplication/MyFolder&template=MyForm.xdp
 * @param taskContext task context
 * @param profileName Forms servlet URL.
 * @return form URL string
 */
public String generateFormURL(TaskContext taskContext, String profileName);

/*
 * Render the XDP Form as HTML. Can be used directly for updating the runtimeMap in render.
 * It adds the following keys to the map -
 * hint:new html form = true
 * newHTMLFormURL = the URL returned after calling 'generateFormURL' API.
 * @param TaskContext taskContext
 * @param profileName Forms servlet URL.
 * @param runtimeMap runtime map<string,object> associated with form rendering.
 * return runtimeMap
 */
public Map<String, Object> renderHTMLForm (TaskContext taskContext, String profileName, Map<String,Object> runtimeMap);
```

有關Mobile Form設定檔的詳細資訊，請參閱「 [建立自訂設定檔」](/help/forms/using/custom-profile.md)。

## 新的HTML表單演算與提交程式 {#new-html-form-render-amp-submit-processes}

對於每個「AssignTask」操作，都可以指定表單的Render和Submit進程。 TaskManager和API會呼叫這些 `renderForm`進 `submitForm`程，以允許自訂處理。 新HTML表單的這些進程語義：

### 演算新的HTML表格 {#render-a-new-html-form}

與每個演算程式一樣，轉換HTML的新程式有下列I/O參數-

輸入 - `taskContext`

輸出 - `runtimeMap`

輸出 - `outFormDoc`

此方法模擬NewHTMLFormsService `renderHTMLForm` 的API的精確行為。 它會呼叫 `generateFormURL` API，以取得表單的HTML轉譯URL。 然後，它會以下列索引鍵或值填入runtimeMap:

new html form = true

newHTMLFormURL =呼叫API後傳回的 `generateFormURL` URL。

### 提交新的HTML表單 {#submit-a-new-html-form}

提交新HTML表格的程式可與下列I/O參數搭配使用-

輸入 - `taskContext`

輸出 - `runtimeMap`

輸出 - `outputDocument`

進程將設定 `outputDocument`為從中 `inputDocument`檢索的 `taskContext`。

## 預設演算或提交程式，以及動作設定檔 {#default-render-or-submit-processes-and-action-profiles}

預設的「轉譯與送出」服務可讓支援在桌上型電腦上轉譯PDF，並在行動裝置(iPad)上轉譯HTML。

### 預設演算表單 {#default-render-form}

此程式可順暢地在多個平台上轉換XDP表單。 此程式會從中擷取使用 `taskContext`者代理，並使用資料來呼叫程式，以轉譯HTML或PDF。

![default-render-form](assets/default-render-form.png)

### 預設提交表單 {#default-submit-form}

此程式可順暢地在多個平台上提交XDP表格。 它會從中擷取使用 `taskContext`者代理，並使用資料來呼叫提交HTML或PDF的程式。

![default-submit-form](assets/default-submit-form.png)

## 將行動表單的轉換從PDF轉換為HTML {#switch-the-rendering-of-mobile-forms-from-pdf-to-html}

瀏覽器逐漸撤回對NPAPI增效模組的支援，包括Adobe Acrobat和Adobe Acrobat Reader的增效模組。 您可以使用下列步驟，將行動表單的轉換從PDF變更為HTML:

1. 以有效使用者身分登入Workbench。
1. 選擇「 **檔案** >取 **得應用程式**」。

   將顯示「獲取應用程式」對話框。

1. 選取您要變更行動表單轉換的應用程式，然後按一下「確 **定」**。
1. 開啟要更改渲染的過程。
1. 開啟定位的起點／工作，導覽至「簡報與資料」區段，然後按一下「管 **理動作設定檔**」。

   此時將顯示「管理操作配置檔案」對話框。
1. 將預設演算描述檔組態從PDF變更為HTML，然後按一下「 **確定**」。
1. 簽入流程。
1. 重複這些步驟以更改其他進程的渲染。
1. 部署與您已變更的程式相關的應用程式。

### 預設動作設定檔 {#default-action-profile}

預設的「動作描述檔」會將XDP表單轉換為PDF。 現在，此行為已變更為使用「預設演算表單」和「預設提交表單」程式。

有關動作設定檔的常見問題如下：

![gen_question_b_20](assets/gen_question_b_20.png) **What Render / Submit processes will be available out of the box?**

* 演算指南（不建議使用參考線）
* 演算表單指南
* 轉換PDF表單
* 演算HTML表單
* 演算新HTML表格（新）
* 預設演算表單（新）

此外，還有相當的「提交」程式。

![gen_question_b_20](assets/gen_question_b_20.png) 現 **成可用的動作設定檔？**

對於XDP表單：

* 預設（使用新的「預設演算／提交」程式來演算／提交）

![gen_question_b_20](assets/gen_question_b_20.png)**流程設計人員需要執行什麼工作，才能讓表單以HTML格式在裝置上轉譯，以PDF格式在案頭上轉譯？**

沒什麼。 預設的「動作描述檔」會自動選取，並自動處理演算模式。

![gen_question_b_20](assets/gen_question_b_20.png) **Facel To Pay To Be Rendered in HTML on a desktop?**

用戶必須為預設配置檔案選擇HTML單選按鈕。

![gen_question_b_20](assets/gen_question_b_20.png) 變更預 **設動作設定檔行為時，是否會有任何升級影響？**

是的，因為先前與預設動作描述檔相關聯的演算和提交服務不同，所以這些服務會視為現有表格的自訂。 按一下「 **還原預設值**」後，會改為設定預設演算和送出服務。

如果您已修改現有的Render或Submit PDF Form服務或已建立自訂服務（例如custom1），現在想要對HTML轉譯使用相同的功能。 您需要複製新的演算或提交服務（如custom2），並套用類似的自訂設定。 現在，請修改XDP的動作設定檔，以開始使用custom2服務，而非custom1來呈現或送出。

流程設計人員需要做什麼，才能讓表單在裝置上以HTML格式呈現，在案頭上以PDF格式呈現？
流程設計人員需要做什麼，才能讓表單在裝置上以HTML格式呈現，在案頭上以PDF格式呈現？  [聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
