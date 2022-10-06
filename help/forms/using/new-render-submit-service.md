---
title: 新的呈現和提交服務
seo-title: New render and submit service
description: 在Workbench中定義轉譯及提交服務，以根據XDP表單所存取的裝置，將其轉譯為HTML或PDF。
seo-description: Define render and submit services in Workbench to render XDP form as HTML or PDF depending on the device it is accessed from.
uuid: 7f8348a1-753c-4dab-87d5-4a4a301198dd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6a32d240-c6a6-4937-a31f-7a5ec3c60b1f
docset: aem65
exl-id: 46de0101-9607-4429-84c3-7c1f34d2da27
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 0%

---

# 新的呈現和提交服務{#new-render-and-submit-service}

## 簡介 {#introduction}

在Workbench中，當您定義 `AssignTask` 操作，指定特定表單(XDP或PDF表單)。 另外，通過操作配置檔案指定一組呈現和提交服務。

XDP可呈現為PDF表單或HTML表單。 新功能包括：

* 呈現並提交XDP表單作為HTML
* 在桌上型電腦上以PDF形式呈現並提交XDP表單，並在行動裝置(例如iPad)上以HTML形式呈現

### 新HTMLForms服務 {#new-html-forms-service}

新的HTMLForms服務運用Forms的新功能，支援將XDP表單轉譯為HTML。 新的HTMLForms服務會公開下列方法：

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

如需行動表單設定檔的詳細資訊，請參閱 [建立自訂設定檔](/help/forms/using/custom-profile.md).

## 新的HTML表單轉譯與提交程式 {#new-html-form-render-amp-submit-processes}

對於每個「AssignTask」操作，指定使用表單呈現和提交流程。 這些進程由TaskManager調用 `renderForm`和 `submitForm`允許自訂處理的API。 新HTML表單的以下進程的語義：

### 轉譯新HTML表單 {#render-a-new-html-form}

呈現HTML的新過程與每個呈現過程一樣，具有以下I/O參數 — 

輸入 - `taskContext`

輸出 - `runtimeMap`

輸出 - `outFormDoc`

此方法模擬 `renderHTMLForm` NewHTMLFormsService的API。 它稱為 `generateFormURL` API以取得表單HTML轉譯的URL。 接著會以下列索引鍵或值填入runtimeMap:

新html表單= true

newHTMLFormURL =呼叫後傳回的URL `generateFormURL` API。

### 提交新的HTML表 {#submit-a-new-html-form}

提交新HTML表單的過程適用於以下I/O參數 — 

輸入 - `taskContext`

輸出 - `runtimeMap`

輸出 - `outputDocument`

程式會設定 `outputDocument`到 `inputDocument`從 `taskContext`.

## 預設呈現或提交流程和操作配置檔案 {#default-render-or-submit-processes-and-action-profiles}

預設的呈現和提交服務可讓支援在案頭上呈現PDF，並在行動裝置(iPad)上HTML。

### 預設渲染表單 {#default-render-form}

此程式可順暢地在多個平台上轉譯XDP表單。 程式會從中擷取使用者代理 `taskContext`，並使用資料來呼叫程式，以呈現HTML或PDF。

![default-render-form](assets/default-render-form.png)

### 預設提交表單 {#default-submit-form}

此過程可在多個平台上無縫提交XDP表單。 它會從中擷取使用者代理 `taskContext`並使用資料來呼叫程式以提交HTML或PDF。

![default-submit-form](assets/default-submit-form.png)

## 將行動表單的轉譯從PDF切換為HTML {#switch-the-rendering-of-mobile-forms-from-pdf-to-html}

瀏覽器正逐步停止支援以NPAPI為基礎的外掛程式，包括Adobe Acrobat和Adobe Acrobat Reader的外掛程式。 您可以使用下列步驟，將行動表單的轉譯從PDF變更為HTML:

1. 以有效使用者身分登入Workbench。
1. 選擇 **檔案** > **獲取應用程式**.

   將顯示「獲取應用程式」對話框。

1. 選取您要變更行動表單轉譯的應用程式，然後按一下 **確定**.
1. 開啟要更改其呈現的過程。
1. 開啟目標起始點/任務，導覽至「簡報與資料」區段，然後按一下 **管理動作設定檔**.

   將顯示管理操作配置檔案對話框。
1. 將預設呈現配置檔案配置從PDF更改為HTML，然後按一下 **確定**.
1. 簽入過程。
1. 重複這些步驟以更改其他進程的渲染。
1. 部署與您更改的流程相關的應用程式。

### 預設動作設定檔 {#default-action-profile}

預設的「動作設定檔」將XDP表單轉譯為PDF。 此行為現在已變更為使用「預設呈現表單」和「預設提交表單」流程。

有關動作設定檔的一些常見問題如下：

![gen_question_b_20](assets/gen_question_b_20.png) **哪些呈現/提交程式將可立即使用？**

* 轉譯指南（不建議使用參考線）
* 轉譯表單指南
* 呈現PDF表單
* 呈現HTML表單
* 呈現新HTML表單（新）
* 預設呈現表單（新）

此外，還有同等的提交流程。

![gen_question_b_20](assets/gen_question_b_20.png) **哪些動作設定檔將可立即使用？**

針對XDP Forms:

* 預設（使用新的「預設呈現/提交」流程呈現/提交）

![gen_question_b_20](assets/gen_question_b_20.png) **流程設計人員需要執行哪些操作才能使表單以HTML形式呈現在設備上，以及以PDF形式呈現在案頭上？**

沒有。 系統會自動選取預設的「動作描述檔」，並自動處理轉譯模式。

![gen_question_b_20](assets/gen_question_b_20.png) **要使表單以HTML形式呈現在案頭上，需要執行哪些操作？**

使用者必須為預設設定檔選取「HTML」選項按鈕。

![gen_question_b_20](assets/gen_question_b_20.png) **變更預設動作設定檔行為是否會受到升級影響？**

可以，因為先前與預設動作設定檔相關聯的呈現和提交服務不同，因此這些會視為現有表單的自訂。 按一下 **還原預設值**，則會改為設定預設的呈現和提交服務。

如果您已修改現有的「呈現」或「提交PDF表單」服務或已建立自訂服務（例如custom1），且現在想要對HTML轉譯使用相同的功能。 您需要複製新的呈現或提交服務（如custom2），並將類似的自訂套用至這些服務。 現在，修改XDP的動作設定檔，以開始使用custom2服務，而非自訂1，以便呈現或提交。

流程設計人員需要執行哪些操作才能使表單以HTML形式呈現在設備上，以及以PDF形式呈現在案頭上？
流程設計人員需要執行哪些操作才能使表單以HTML形式呈現在設備上，以及以PDF形式呈現在案頭上？
