---
title: 流程報告簡介
seo-title: Introduction to Process Reporting
description: AEM Forms關於JEE流程報告的介紹和關鍵功能
seo-description: Introduction and key capabilities of AEM Forms on JEE Process Reporting
uuid: a7f2455b-1b09-41a7-817b-e2e7a1ff9936
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4e83ed7b-3f48-4bf6-be4c-89f79949c1df
docset: aem65
exl-id: 674d28dc-7353-49de-9e12-b1998e1509c7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# 流程報告簡介{#introduction-to-process-reporting}

![進程報告](assets/process-reporting.png)

Process Reporting是一種基於瀏覽器的工具，用於建立和查看有關AEM Forms進程和任務的報告。

「Process Reporting」提供一組現成報告，允許您篩選、查看有關長時間運行的進程、進程持續時間和工作流卷的資訊。

此外，Process Reporting還提供了一個介面，用於運行臨時查詢並將自定義報表視圖整合到Process Reporting用戶介面。

有關支援的瀏覽器的清單，請參見 [AEM Forms支援的平台](/help/forms/using/aem-forms-jee-supported-platforms.md)。

Process Reporting構建在以下模組上：

* 從AEM Forms資料庫讀取進程資料
* 將流程資料發佈到嵌入式Process Reporting儲存庫
* 提供基於瀏覽器的用戶介面以查看報告

## 關鍵功能 {#key-capabilities}

### Always-on報告 {#always-on-reporting}

![站點管理](assets/site-management.png)

查看長時間運行的進程清單、進程持續時間圖表，並使用篩選器運行自定義查詢。

Process Reporting還提供了以CSV格式導出報表和查詢資料的選項。

### 臨時報告 {#adhoc-reports}

![打印和彩色](assets/print-&-colour.png)

使用篩選器可獲取資料的特定視圖。

您可以按ID、持續時間、開始和結束日期、進程啟動器等搜索進程或任務。

您可以組合多個篩選器以建立特定報告。

然後，您可以保存要在以後的日期或時間運行的報告篩選器。

### 進程/任務歷史記錄 {#process-task-history}

![檔案管理](assets/file-management.png)

AEM Forms伺服器並行運行多個進程。 這些進程繼續從一個狀態轉換到另一個狀態。 通過定期將Forms資料發佈到Process Reporting儲存庫，Process Reporting將保留有關在AEM Forms運行的進程的轉換資訊。

### 存取控制 {#access-control-br}

![無標題](assets/untitled.png)

「進程報告」提供對用戶介面的基於權限的訪問。

這意味著只有具有報告權限的用戶才能訪問Process Reporting用戶介面。
