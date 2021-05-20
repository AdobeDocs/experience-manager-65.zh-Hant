---
title: 新的呈現和提交服務
seo-title: 新的呈現和提交服務
description: 在Workbench中定義轉譯和提交服務，以根據從存取的裝置將XDP表單轉譯為HTML或PDF。
seo-description: 在Workbench中定義轉譯和提交服務，以根據從存取的裝置將XDP表單轉譯為HTML或PDF。
uuid: 7f8348a1-753c-4dab-87d5-4a4a301198dd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6a32d240-c6a6-4937-a31f-7a5ec3c60b1f
docset: aem65
exl-id: 46de0101-9607-4429-84c3-7c1f34d2da27
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 0%

---

# 新的呈現和提交服務{#new-render-and-submit-service}

## 簡介 {#introduction}

在Workbench中，當您定義`AssignTask`操作時，請指定特定表單（XDP或PDF表單）。 另外，通過操作配置檔案指定一組呈現和提交服務。

XDP可轉譯為PDF表單或HTML表單。 新功能包括：

* 將XDP表單轉譯為HTML並提交
* 在桌上型電腦上以PDF格式呈現並提交XDP表單，在行動裝置上以HTML格式呈現（例如iPad）

### 新的HTML Forms服務{#new-html-forms-service}

新的HTML Forms服務運用Forms的新功能，支援將XDP表單轉譯為HTML。 新的HTML Forms服務公開下列方法：

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

如需行動表單設定檔的詳細資訊，請參閱[建立自訂設定檔](/help/forms/using/custom-profile.md)。

## 新的HTML表單呈現和提交流程{#new-html-form-render-amp-submit-processes}

對於每個「AssignTask」操作，指定使用表單呈現和提交流程。 TaskManager `renderForm`和`submitForm`API調用這些進程以允許自定義處理。 新HTML表單的這些進程的語義：

### 呈現新的HTML表單{#render-a-new-html-form}

呈現HTML的新程式與每個呈現程式一樣，具有以下I/O參數 — 

輸入 - `taskContext`

輸出 - `runtimeMap`

輸出 - `outFormDoc`

此方法模擬NewHTMLFormsService的`renderHTMLForm` API的確切行為。 它會呼叫`generateFormURL` API，以取得表單的HTML轉譯URL。 接著會以下列索引鍵或值填入runtimeMap:

新html表單= true

newHTMLFormURL =呼叫`generateFormURL` API後傳回的URL。

### 提交新的HTML表單{#submit-a-new-html-form}

提交新HTML表單的程式可搭配下列I/O參數使用 — 

輸入 - `taskContext`

輸出 - `runtimeMap`

輸出 - `outputDocument`

該進程將`outputDocument`設定為從`taskContext`檢索的`inputDocument`。

## 預設呈現或提交進程，以及操作配置檔案{#default-render-or-submit-processes-and-action-profiles}

預設的「轉譯」和「提交」服務可支援在桌上型電腦上轉譯PDF，並在行動裝置(iPad)上轉譯HTML。

### 預設呈現表單{#default-render-form}

此程式可順暢地在多個平台上轉譯XDP表單。 進程從`taskContext`中檢索用戶代理，並使用資料調用進程以呈現HTML或PDF。

![default-render-form](assets/default-render-form.png)

### 預設提交表單{#default-submit-form}

此過程可在多個平台上無縫提交XDP表單。 它會從`taskContext`擷取使用者代理，並使用資料呼叫程式以提交HTML或PDF。

![default-submit-form](assets/default-submit-form.png)

## 將行動表單的轉譯從PDF切換為HTML {#switch-the-rendering-of-mobile-forms-from-pdf-to-html}

瀏覽器正逐步停止支援NPAPI型外掛程式，包括Adobe Acrobat和Adobe AcrobatReader的外掛程式。 您可以使用下列步驟，將行動表單的轉譯從PDF變更為HTML:

1. 以有效使用者身分登入Workbench。
1. 選擇&#x200B;**檔案** > **獲取應用程式**。

   將顯示「獲取應用程式」對話框。

1. 選擇要更改其移動表單呈現的應用程式，然後按一下&#x200B;**確定**。
1. 開啟要更改其呈現的過程。
1. 開啟目標起始點/任務，導覽至「Presentation &amp; Data」區段，然後按一下「**管理動作設定檔**」。

   將顯示管理操作配置檔案對話框。
1. 將預設的渲染配置檔案配置從PDF更改為HTML，然後按一下&#x200B;**OK**。
1. 簽入過程。
1. 重複這些步驟以更改其他進程的渲染。
1. 部署與您更改的流程相關的應用程式。

### 預設操作配置檔案{#default-action-profile}

預設的「動作描述檔」將XDP表單轉譯為PDF。 此行為現在已變更為使用「預設呈現表單」和「預設提交表單」流程。

有關動作設定檔的一些常見問題如下：

![gen_question_b_20](assets/gen_question_b_20.png) **什麼呈現/提交程式將可立即使用？**

* 轉譯指南（不建議使用參考線）
* 轉譯表單指南
* 轉譯PDF表單
* 呈現HTML表單
* 呈現新的HTML表單（新）
* 預設呈現表單（新）

此外，還有同等的提交流程。

![gen_question_b_20](assets/gen_question_b_20.png) **哪些動作設定檔將可立即使用？**

針對XDP Forms:

* 預設（使用新的「預設呈現/提交」流程呈現/提交）

![gen_question_b_20](assets/gen_question_b_20.png) **流程設計人員需要執行哪些操作，才能在裝置上以HTML和案頭上以PDF格式呈現表單？**

沒有。 系統會自動選取預設的「動作描述檔」，並自動處理轉譯模式。

![gen_question_b_20](assets/gen_question_b_20.png) **需要執行哪些操作才能在案頭的HTML中呈現表單？**

使用者必須為預設設定檔選取HTML選項按鈕。

![gen_question_b_20](assets/gen_question_b_20.png) **是否對更改預設操作配置檔案行為有任何升級影響？**

是，由於先前與預設動作設定檔相關聯的呈現和提交服務不同，因此這些會視為現有表單的自訂。 按一下「**還原預設值**」時，會改為設定預設的呈現和提交服務。

如果您已修改現有的Render或Submit PDF Form服務或已建立自訂服務（例如custom1），且現在想要對HTML轉譯使用相同的功能。 您需要複製新的呈現或提交服務（如custom2），並將類似的自訂套用至這些服務。 現在，修改XDP的動作設定檔，以開始使用custom2服務，而非自訂1，以便呈現或提交。

流程設計人員需要執行什麼操作才能使表單以HTML格式呈現在裝置上，以PDF格式呈現在案頭上？
流程設計人員需要執行什麼操作才能使表單以HTML格式呈現在裝置上，以PDF格式呈現在案頭上？
