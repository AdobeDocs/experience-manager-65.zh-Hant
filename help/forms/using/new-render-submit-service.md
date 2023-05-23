---
title: 新建呈現和提交服務
seo-title: New render and submit service
description: 在Workbench中定義呈現和提交服務，以根據XDP表單所訪問的設備將其呈現為HTML或PDF。
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

# 新建呈現和提交服務{#new-render-and-submit-service}

## 簡介 {#introduction}

在工作台中，定義 `AssignTask` 操作，指定特定窗體(XDP或PDF窗體)。 另外，通過操作配置檔案指定一組呈現和提交服務。

XDP可以呈現為PDF形式或HTML形式。 新功能包括：

* 呈現並提交XDP表單作為HTML
* 呈現並提交XDP表單，作為案頭上的PDF，以及移動設備上的HTML(例如，iPad)

### 新HTMLForms社 {#new-html-forms-service}

新的HTMLForms服務利用Forms的新功能支援將XDP表格作為HTML。 新的HTMLForms服務公開了以下方法：

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

有關移動表單配置檔案的詳細資訊，請訪問 [建立自定義配置檔案](/help/forms/using/custom-profile.md)。

## 新建HTML窗體呈現和提交流程 {#new-html-form-render-amp-submit-processes}

對於每個「AssignTask」操作，使用表單指定一個呈現和提交進程。 這些進程由TaskManager調用 `renderForm`和 `submitForm`允許自定義處理的API。 新HTML表單的這些進程的語義：

### 呈現新HTML窗體 {#render-a-new-html-form}

要呈現HTML的新進程與每個呈現進程一樣，具有以下I/O參數 — 

輸入 - `taskContext`

輸出 - `runtimeMap`

輸出 - `outFormDoc`

此方法模擬 `renderHTMLForm` NewHTMLFormsService的API。 它稱之為 `generateFormURL` 用於獲取表單HTML格式副本的URL的API。 然後，它使用以下鍵或值填充runtimeMap:

新建html表單=true

newHTMLFormURL =調用後返回的URL `generateFormURL` API。

### 提交新HTML表 {#submit-a-new-html-form}

此提交新HTML表格的過程與以下I/O參數配合使用 — 

輸入 - `taskContext`

輸出 - `runtimeMap`

輸出 - `outputDocument`

該進程設定 `outputDocument`到 `inputDocument`從 `taskContext`。

## 預設呈現或提交進程和操作配置檔案 {#default-render-or-submit-processes-and-action-profiles}

預設的呈現和提交服務支援在案頭上呈現PDF，在移動設備(iPad)上呈現HTML。

### 預設渲染窗體 {#default-render-form}

此過程在多個平台上無縫呈現XDP表單。 進程從中檢索用戶代理 `taskContext`，並使用資料調用進程以呈現HTML或PDF。

![預設呈現形式](assets/default-render-form.png)

### 預設提交表單 {#default-submit-form}

此過程在多個平台上無縫提交XDP表單。 它從 `taskContext`並使用資料調用流程以提交HTML或PDF。

![預設提交表單](assets/default-submit-form.png)

## 將移動表單的呈現從PDF切換到HTML {#switch-the-rendering-of-mobile-forms-from-pdf-to-html}

瀏覽器正在逐步取消對基於NPAPI的插件的支援，包括對Adobe Acrobat和Adobe Acrobat Reader的插件。 您可以使用以下步驟將移動表單的呈現從PDF更改為HTML:

1. 以有效用戶身份登錄Workbench。
1. 選擇 **檔案** > **獲取應用程式**。

   將顯示「獲取應用程式」對話框。

1. 選擇要更改其移動表單呈現的應用程式，然後按一下 **確定**。
1. 開啟要更改其呈現的進程。
1. 開啟目標起始點/任務，導航到「演示和資料」部分，然後按一下 **管理操作配置檔案**。

   將顯示「管理操作配置檔案」對話框。
1. 將預設呈現配置檔案配置從PDF更改為HTML，然後按一下 **確定**。
1. 簽入流程。
1. 重複這些步驟以更改其他進程的渲染。
1. 部署與已更改的進程相關的應用程式。

### 預設操作配置檔案 {#default-action-profile}

預設的「操作配置檔案」將XDP表單呈現為PDF。 現在，此行為已更改為使用預設呈現表單和預設提交表單進程。

有關操作配置檔案的一些常見問題如下：

![gen_question_b_20](assets/gen_question_b_20.png) **哪些呈現/提交進程將在開箱後可用？**

* 呈現指南（不建議使用參考線）
* 渲染表單指南
* 呈現PDF窗體
* 呈現HTML窗體
* 呈現新HTML窗體（新）
* 預設渲染窗體（新）

並且，等效的「提交」流程。

![gen_question_b_20](assets/gen_question_b_20.png) **哪些操作配置檔案將開箱提供？**

對於XDPForms:

* 預設（使用新的「預設呈現/提交」進程呈現/提交）

![gen_question_b_20](assets/gen_question_b_20.png) **流程設計人員需要執行什麼操作才能使表單在設備上以HTML方式呈現，在案頭上以PDF方式呈現？**

沒什麼。 預設的「操作配置檔案」(Action Profile)會自動選擇，渲染模式也會自動處理。

![gen_question_b_20](assets/gen_question_b_20.png) **要使表單在案頭上以HTML形式呈現，需要執行哪些操作？**

用戶必須為預設配置檔案選擇HTML單選按鈕。

![gen_question_b_20](assets/gen_question_b_20.png) **是否對更改預設操作配置檔案行為產生任何升級影響？**

是的，因為與預設操作配置檔案關聯的上一個呈現和提交服務不同，所以這些服務被視為現有表單的自定義。 按一下 **恢復預設值**，則改為設定預設的render和submit服務。

如果您修改了現有的Render或SubmitPDF表單服務或建立了自定義服務（如custom1），並且現在希望將相同功能用於HTML格式副本。 您需要複製新的呈現或提交服務（如custom2），並對這些服務應用類似的自定義。 現在，修改XDP的操作配置檔案以開始使用custom2服務，而不是custom1來呈現或提交。

流程設計人員需要執行什麼操作才能使表單在設備上以HTML方式呈現，在案頭上以PDF方式呈現？
流程設計人員需要執行什麼操作才能使表單在設備上以HTML方式呈現，在案頭上以PDF方式呈現？
