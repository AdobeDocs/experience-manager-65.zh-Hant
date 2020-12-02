---
title: 登入AEM Forms工作流程
seo-title: 登入AEM Forms工作流程
description: 使用記錄檔來除錯AEM Forms工作流程問題。
seo-description: 使用記錄檔來除錯AEM Forms工作流程問題。
uuid: 869d0271-c7e3-4b6d-8e63-893dc6af8b8a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 14bb521a-42ea-4fe2-90fb-202e7ddf917a
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 5%

---


# 登入AEM Forms工作流程{#logging-in-aem-forms-workflows}

表單工作流程步驟可方便地提供詳細的記錄檔，以除錯與工作流程相關的問題。 啟用AEM Forms工作流程的除錯記錄功能，以檢視記錄檔。

預設情況下，**error.log**&#x200B;檔案中的&#x200B;*/crx-repository/logs/*&#x200B;目錄下的所有日誌資訊都可用。

表單工作流程的除錯記錄檔包括：

* 輸入每個工作流程步驟。 例如：\
   `[DEBUG] "Executing Invoke DDX Process step"`

* 退出每個工作流程步驟。 例如：\
   `[DEBUG] "Successfully finished Invoke DDX Process step"`

* 服務調用消息。 例如：\
   `[DEBUG] Invoking Adobe Sign Service for creating agreement`

* 服務退出消息。 例如：\
   `[DEBUG] Agreement created successfully with agreement id <agreement id>`

* 從中繼資料地圖讀取的變數。 例如：\
   `[DEBUG] Successfully retrieved variable <variable name> from workflow meta data map`

* 寫入JCR儲存庫的變數。 例如：

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

使用記錄來評估：

* 您使用的是正確的adobe sign設定。
* Adobe Sign Service在成功建立合約後退出。
* 「簽署檔案」步驟會退出並顯示成功訊息。

如果有例外，您可以檢視完整的堆疊追蹤，以評估錯誤的原因。

## 啟用AEM Forms工作流程的除錯記錄{#enable-debug-logging-for-aem-forms-workflows}

執行下列步驟，以啟用AEM Forms工作流程的除錯記錄：

1. 前往AEM網頁主控台組態管理器，網址為：

   https://&#39;[server]:[port]&#39;/system/console/configMgr

1. 選擇&#x200B;**[!UICONTROL Sling]** > **[!UICONTROL Log Support]**。
1. 點選&#x200B;**[!UICONTROL Add new Logger.]**
1. 選擇&#x200B;**[!UICONTROL Debug]**&#x200B;作為&#x200B;**[!UICONTROL 日誌級別]**。
1. 指定日誌檔案的位置。 日誌檔案的預設位置為：*logs\error.log*
1. 在&#x200B;**[!UICONTROL Logger]**&#x200B;欄中，將套件名稱指定為&#x200B;**com.adobe.granite.workflow.core**。

   執行這些步驟可以儲存&#x200B;**com.adobe.granite.workflow.core**&#x200B;軟體包的調試日誌。 點選&#x200B;**[!UICONTROL +]**&#x200B;並將下列套件名稱新增至清單：

   * com.adobe.fd.workflow
   * com.adobe.fd.workspace

