---
title: 新的轉譯與提交服務
description: 在Workbench中定義轉譯與提交服務，以根據從中存取XDP表單的裝置將XDP表單轉譯為HTML或PDF。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 46de0101-9607-4429-84c3-7c1f34d2da27
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms, Adaptive Forms
role: Admin, User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 0%

---

# 新的轉譯與提交服務{#new-render-and-submit-service}

## 簡介 {#introduction}

在Workbench中，當您定義 `AssignTask` 操作，指定特定表單(XDP或PDF表單)。 此外，透過動作設定檔指定一組轉譯和提交服務。

XDP可以呈現為PDF表單或HTML表單。 新功能包括：

* 將XDP表單轉譯為表單並提交為HTML
* 在案頭上將XDP表單轉譯為內部PDF並在行動裝置(例如iPad)上將其轉譯為HTML並提交

### 全新HTMLForms服務 {#new-html-forms-service}

新的HTML Forms服務使用Forms中的新功能來支援將XDP表單轉譯為HTML。 新的HTMLForms服務會公開下列方法：

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

有關行動表單設定檔的詳細資訊，請參閱 [建立自訂設定檔](/help/forms/using/custom-profile.md).

## 新HTML表單轉譯與提交程式 {#new-html-form-render-amp-submit-processes}

針對每個「AssignTask」作業，指定具有表單的「轉譯」和「提交」程式。 這些程式由TaskManager呼叫 `renderForm`和 `submitForm`允許自訂處理的API。 新HTML表單的這些流程的語意：

### 轉譯新的HTML表單 {#render-a-new-html-form}

呈現HTML的新程式（如同每個呈現程式）具有下列I/O引數 — 

輸入 —  `taskContext`

輸出 —  `runtimeMap`

輸出 —  `outFormDoc`

此方法會模擬以下專案的確切行為： `renderHTMLForm` NewHTMLFormsService的API。 它會呼叫 `generateFormURL` 用於取得表單HTML轉譯之URL的API。 然後它會使用下列索引鍵或值填入runtimeMap：

新html表單= true

newHTMLFormURL =呼叫後傳回的URL `generateFormURL` API。

### 提交新的HTML表單 {#submit-a-new-html-form}

提交新HTML表單的這個程式與下列I/O引數搭配使用 — 

輸入 —  `taskContext`

輸出 —  `runtimeMap`

輸出 —  `outputDocument`

程式會設定 `outputDocument`至 `inputDocument`擷取自 `taskContext`.

## 預設呈現或提交程式，以及動作設定檔 {#default-render-or-submit-processes-and-action-profiles}

預設的轉譯和提交服務可支援在案頭上轉譯PDF，以及在行動裝置上HTML(iPad)。

### 預設演算表單 {#default-render-form}

此過程可順暢地在多種平台上呈現XDP表單。 此程式會從擷取使用者代理程式 `taskContext`，並使用資料呼叫程式來轉譯HTML或PDF。

![default-render-form](assets/default-render-form.png)

### 預設提交表單 {#default-submit-form}

此程式可順暢地在多個平台上提交XDP表單。 它會從以下位置擷取使用者代理 `taskContext`並使用資料呼叫流程以提交HTML或PDF。

![default-submit-form](assets/default-submit-form.png)

## 將行動表單的呈現從PDF切換為HTML {#switch-the-rendering-of-mobile-forms-from-pdf-to-html}

瀏覽器逐漸停止支援以NPAPI為基礎的外掛程式，包括Adobe Acrobat和Adobe Acrobat Reader的外掛程式。 您可以使用下列步驟，將行動表單的呈現方式從PDF變更為HTML：

1. 以有效使用者的身分登入Workbench。
1. 選取 **檔案** > **取得應用程式**.

   「取得應用程式」對話方塊就會顯示。

1. 選取您要變更行動表單轉譯的應用程式，然後按一下 **確定**.
1. 開啟您要變更其演算的程式。
1. 開啟目標起點/工作，導覽至「簡報與資料」區段，然後按一下 **管理動作設定檔**.

   管理動作設定檔對話方塊就會顯示。
1. 將預設演算設定檔設定從PDF變更為HTML，然後按一下 **確定**.
1. 在程式中籤入。
1. 重複這些步驟以變更其他處理程式的演算。
1. 部署與已變更的處理程式相關的應用程式。

### 預設動作設定檔 {#default-action-profile}

預設動作設定檔將XDP表單轉譯為PDF。 此行為現在已變更為使用預設轉譯表單和預設提交表單程式。

有關動作設定檔的一些常見問題如下：

![gen_question_b_20](assets/gen_question_b_20.png) **哪些轉譯/提交程式將可立即使用？**

* 轉譯指南（指南已過時）
* 轉譯表單指南
* 呈現PDF表單
* 呈現HTML表單
* 轉譯新HTML表單（新）
* 預設演算表單（新）

以及等同的提交程式。

![gen_question_b_20](assets/gen_question_b_20.png) **開箱即用的動作設定檔有哪些？**

對於XDP Forms：

* 預設（使用新的「預設轉譯/提交」流程轉譯/提交）

![gen_question_b_20](assets/gen_question_b_20.png) **流程設計人員需要採取哪些動作，才能讓表單在裝置上以HTML呈現，並在案頭上以PDF呈現？**

沒有內容。 系統會自動選擇預設的「動作設定檔」，並自動管理演算模式。

![gen_question_b_20](assets/gen_question_b_20.png) **若要在案頭上以HTML呈現表單，需要執行哪些動作？**

使用者必須選取預設設定檔的HTML選項按鈕。

![gen_question_b_20](assets/gen_question_b_20.png) **變更預設動作設定檔行為是否會受到升級影響？**

可以，因為與預設動作設定檔關聯的先前轉譯與提交服務不同，所以會將其視為現有表單的自訂。 按一下 **還原預設值**，則會改為設定預設的轉譯器和提交服務。

如果您修改了現有的轉譯器或提交PDF表單服務，或建立了自訂服務（例如custom1），現在想要對HTML轉譯使用相同的功能。 您需要複製新的轉譯器或提交服務（例如custom2），並將類似的自訂套用至這些服務。 現在，修改您XDP的動作設定檔，以開始使用自訂2服務，而不是自訂1的呈現或提交。

流程設計人員需要採取哪些動作，才能讓表單在裝置上以HTML呈現，並在案頭上以PDF呈現？
流程設計人員需要採取哪些動作，才能讓表單在裝置上以HTML呈現，並在案頭上以PDF呈現？
