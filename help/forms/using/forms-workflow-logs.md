---
title: 登入AEM Forms工作流程
description: 瞭解如何偵錯AEM Forms工作流程問題並啟用AEM Forms工作流程的偵錯記錄以檢視記錄。
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: 601c8d95-0d1a-4945-a522-e85d3e9fc4ae
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, Workflow
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 5%

---

# 登入AEM Forms工作流程{#logging-in-aem-forms-workflows}

Forms Workflow步驟提供詳細的記錄檔，以便您輕鬆偵錯工作流程相關問題。 啟用AEM Forms工作流程的偵錯記錄以檢視記錄。

依預設，所有記錄資訊都可在 **error.log** 檔案位於 */crx-repository/logs/* 目錄。

表單工作流程的偵錯記錄包括：

* 每個工作流程步驟的輸入。 例如：\
  `[DEBUG] "Executing Invoke DDX Process step"`

* 結束每個工作流程步驟。 例如：\
  `[DEBUG] "Successfully finished Invoke DDX Process step"`

* 服務呼叫訊息。 例如：\
  `[DEBUG] Invoking Adobe Sign Service for creating agreement`

* 服務結束訊息。 例如：\
  `[DEBUG] Agreement created successfully with agreement id <agreement id>`

* 從中繼資料對應讀取的變數。 例如：\
  `[DEBUG] Successfully retrieved variable <variable name> from workflow meta data map`

* 以JCR存放庫撰寫的變數。 例如：

  ```verilog
     [DEBUG] Successfully written variable <variable name> into meta data node at <JCR path where meta data is being written>
  ```

* 具有完整棧疊追蹤的例外狀況訊息。 例如：\
  `[DEBUG] Exception in Adobe Sign Service <complete stack trace>`

* 動態步驟中繼資料引數。 例如：

  ```verilog
  [DEBUG] Document of Record to be generated for adaptive form <path of adaptive form>
   [DEBUG] Locale to be used for Document of Record is <locale>
  ```

以下範例說明「簽署檔案」步驟的記錄：

```verilog
[DEBUG] Executing sign document step.
[DEBUG] Using adobe sign configuration: <path of adobe sign configuration>
[DEBUG] Invoking Adobe Sign Service for creating agreement
[DEBUG] Agreement created successfully with agreement id <agreement id>
[DEBUG] Exception in Adobe Sign Service <complete stack trace>
[ERROR] Exception in Adobe Sign Service
[DEBUG] Successfully finished sign document step
```

使用記錄來評估：

* 您使用正確的Adobe Sign設定。
* Adobe Sign服務會在成功建立合約後結束。
* 「簽署檔案」步驟結束，並顯示成功訊息。

如果發生例外狀況，您可以檢視完整的棧疊追蹤，以評估錯誤的原因。

## 啟用AEM Forms工作流程的偵錯記錄 {#enable-debug-logging-for-aem-forms-workflows}

請執行以下動作，以啟用AEM Forms工作流程的偵錯記錄：

1. 請前往AEM Web主控台組態管理員：

   https://&#39;[伺服器]：[連線埠]&#39;/system/console/configMgr

1. 選取 **[!UICONTROL Sling]** > **[!UICONTROL 記錄檔支援]**.
1. 選取 **[!UICONTROL 新增記錄器。]**
1. 選取 **[!UICONTROL 偵錯]** 作為 **[!UICONTROL 記錄層級]**.
1. 指定記錄檔的位置。 記錄檔的預設位置為： *logs\error.log*
1. 將封裝的名稱指定為 **com.adobe.granite.workflow.core** 在 **[!UICONTROL Logger]** 欄。

   執行這些步驟可讓儲存的偵錯記錄 **com.adobe.granite.workflow.core** 封裝。 選取 **[!UICONTROL +]** 並將下列封裝名稱新增至清單：

   * com.adobe.fd.workflow
   * com.adobe.fd.workspace
