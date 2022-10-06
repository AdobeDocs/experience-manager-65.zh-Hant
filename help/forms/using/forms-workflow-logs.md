---
title: 登入AEM Forms工作流程
seo-title: Logging in AEM Forms workflows
description: 使用記錄檔對AEM Forms工作流程問題進行除錯。
seo-description: Use logs to debug AEM Forms workflow issues.
uuid: 869d0271-c7e3-4b6d-8e63-893dc6af8b8a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 14bb521a-42ea-4fe2-90fb-202e7ddf917a
docset: aem65
exl-id: 601c8d95-0d1a-4945-a522-e85d3e9fc4ae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 5%

---

# 登入AEM Forms工作流程{#logging-in-aem-forms-workflows}

Forms工作流程步驟可方便地提供詳細記錄，以偵錯工作流程相關問題。 啟用AEM Forms工作流程的除錯記錄以檢視記錄。

依預設，所有記錄資訊皆可在 **error.log** 檔案 */crx-repository/logs/* 目錄。

表單工作流程的除錯記錄包括：

* 輸入每個工作流步驟。 例如：\
   `[DEBUG] "Executing Invoke DDX Process step"`

* 退出每個工作流程步驟。 例如：\
   `[DEBUG] "Successfully finished Invoke DDX Process step"`

* 服務調用消息。 例如：\
   `[DEBUG] Invoking Adobe Sign Service for creating agreement`

* 服務退出消息。 例如：\
   `[DEBUG] Agreement created successfully with agreement id <agreement id>`

* 從中繼資料映射讀取的變數。 例如：\
   `[DEBUG] Successfully retrieved variable <variable name> from workflow meta data map`

* 寫入JCR存放庫的變數。 例如：

   ```verilog
      [DEBUG] Successfully written variable <variable name> into meta data node at <JCR path where meta data is being written>
   ```

* 具有完整堆棧跟蹤的異常消息。 例如：\
   `[DEBUG] Exception in Adobe Sign Service <complete stack trace>`

* 動態步驟中繼資料參數。 例如：

   ```verilog
   [DEBUG] Document of Record to be generated for adaptive form <path of adaptive form>
    [DEBUG] Locale to be used for Document of Record is <locale>
   ```

以下範例說明「簽署檔案」步驟的記錄檔：

```verilog
[DEBUG] Executing sign document step.
[DEBUG] Using adobe sign configuration: <path of adobe sign configuration>
[DEBUG] Invoking Adobe Sign Service for creating agreement
[DEBUG] Agreement created successfully with agreement id <agreement id>
[DEBUG] Exception in Adobe Sign Service <complete stack trace>
[ERROR] Exception in Adobe Sign Service
[DEBUG] Successfully finished sign document step
```

請使用記錄來評估：

* 您使用正確的adobe sign設定。
* Adobe Sign服務在成功建立合約後退出。
* 「簽署檔案」步驟會退出並顯示成功訊息。

如果有例外，您可以檢視完整的堆疊追蹤，以評估錯誤的原因。

## 為AEM Forms工作流程啟用除錯記錄 {#enable-debug-logging-for-aem-forms-workflows}

執行下列步驟以啟用AEM Forms工作流程的除錯記錄：

1. 前往AEM Web主控台組態管理器：

   https://&#39;[伺服器]:[埠]「/system/console/configMgr

1. 選擇 **[!UICONTROL Sling]** > **[!UICONTROL 記錄支援]**.
1. 點選 **[!UICONTROL 添加新記錄器。]**
1. 選擇 **[!UICONTROL 除錯]** 作為 **[!UICONTROL 記錄層級]**.
1. 指定記錄檔的位置。 記錄檔的預設位置為： *logs\error.log*
1. 將包的名稱指定為 **com.adobe.granite.workflow.core** 在 **[!UICONTROL 記錄器]** 欄。

   執行這些步驟可儲存 **com.adobe.granite.workflow.core** 包。 點選 **[!UICONTROL +]** 並將以下程式包名稱添加到清單中：

   * com.adobe.fd.workflow
   * com.adobe.fd.workspace
