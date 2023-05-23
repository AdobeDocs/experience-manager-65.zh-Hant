---
title: 登錄AEM Forms工作流
seo-title: Logging in AEM Forms workflows
description: 使用日誌調試AEM Forms工作流問題。
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

# 登錄AEM Forms工作流{#logging-in-aem-forms-workflows}

Forms工作流步驟提供詳細日誌以方便調試與工作流相關的問題。 啟用AEM Forms工作流的調試日誌記錄以查看日誌。

預設情況下，所有日誌資訊都可在 **錯誤.log** 檔案 */crx-repository/logs/* 的子菜單。

表單工作流的調試日誌包括：

* 每個工作流步驟的條目。 例如：\
   `[DEBUG] "Executing Invoke DDX Process step"`

* 退出每個工作流步驟。 例如：\
   `[DEBUG] "Successfully finished Invoke DDX Process step"`

* 服務調用消息。 例如：\
   `[DEBUG] Invoking Adobe Sign Service for creating agreement`

* 服務退出消息。 例如：\
   `[DEBUG] Agreement created successfully with agreement id <agreement id>`

* 從元資料映射中讀取的變數。 例如：\
   `[DEBUG] Successfully retrieved variable <variable name> from workflow meta data map`

* 寫入JCR儲存庫的變數。 例如：

   ```verilog
      [DEBUG] Successfully written variable <variable name> into meta data node at <JCR path where meta data is being written>
   ```

* 具有完整堆棧跟蹤的異常消息。 例如：\
   `[DEBUG] Exception in Adobe Sign Service <complete stack trace>`

* 動態步驟元資料參數。 例如：

   ```verilog
   [DEBUG] Document of Record to be generated for adaptive form <path of adaptive form>
    [DEBUG] Locale to be used for Document of Record is <locale>
   ```

以下示例說明了「簽名文檔」步驟的日誌：

```verilog
[DEBUG] Executing sign document step.
[DEBUG] Using adobe sign configuration: <path of adobe sign configuration>
[DEBUG] Invoking Adobe Sign Service for creating agreement
[DEBUG] Agreement created successfully with agreement id <agreement id>
[DEBUG] Exception in Adobe Sign Service <complete stack trace>
[ERROR] Exception in Adobe Sign Service
[DEBUG] Successfully finished sign document step
```

使用日誌評估：

* 您使用的是正確的adobe標籤配置。
* Adobe Sign服務在成功建立協定後退出。
* 「Sign Document（簽名文檔）」步驟將退出，並顯示成功消息。

如果存在異常，則可以查看完整的堆棧跟蹤以評估錯誤的原因。

## 啟用AEM Forms工作流的調試日誌記錄 {#enable-debug-logging-for-aem-forms-workflows}

執行以下步驟以啟用AEM Forms工作流的調試日誌記錄：

1. 轉至AEMWeb控制台配置管理器：

   https://&#39;[伺服器]:[埠]「/system/console/configMgr

1. 選擇 **[!UICONTROL 吊帶]** > **[!UICONTROL 日誌支援]**。
1. 點擊 **[!UICONTROL 添加新記錄器。]**
1. 選擇 **[!UICONTROL 調試]** 的 **[!UICONTROL 日誌級別]**。
1. 指定日誌檔案的位置。 日誌檔案的預設位置是： *日誌\error_log*
1. 將包的名稱指定為 **com.adobe.granite.workflow.core** 的 **[!UICONTROL 記錄器]** 的雙曲餘切值。

   執行這些步驟可儲存 **com.adobe.granite.workflow.core** 檔案。 點擊 **[!UICONTROL +]** 並將以下包名添加到清單中：

   * com.adobe.fd.workflow
   * com.adobe.fd.workspace
