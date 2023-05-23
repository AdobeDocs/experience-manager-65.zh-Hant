---
title: Oracle Process Reporting中的預定義報表
seo-title: Pre-defined reports in Process Reporting
description: 查詢AEM FormsJEE進程資料以建立有關長期運行進程、進程持續時間和工作流卷的報告
seo-description: Query for AEM Forms on JEE process data to create reports on long running processes, Process duration, and Workflow volume
uuid: 704a8886-90ea-4793-a3fc-f998f878c928
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d93375e-ec37-4445-96ea-d315676787b4
docset: aem65
exl-id: 34e55676-6332-4616-aecc-bcc8cc1e8a29
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 0%

---

# Oracle Process Reporting中的預定義報表 {#pre-defined-reports-in-process-reporting}

## 預定義的在製品報告 {#pre-defined-reports-in-process-reporting-1}

AEM Forms流程報告附帶以下 *開箱即用* 報告：

* **[長時間運行的進程](#long-running-processes)**:一份關於AEM Forms所有需要超過指定時間才能完成的進程的報告
* **[進程持續時間圖表](#process-duration-report)**:按期限分列的AEM Forms進程報告
* **[工作流卷](#workflow-volume-report)**:按日期列出的指定進程的運行實例和已完成實例的報告

## 長時間運行的進程 {#long-running-processes}

「 Long Running Processes 」報告顯示已花費超過指定時間完成的AEM Forms進程。

### 執行長時間運行的進程報告 {#to-execute-a-long-running-process-report}

1. 要查看Process Reporting中預定義的報表清單，請在 **流程報告** 樹視圖，按一下 **報告** 的下界。
1. 按一下 **長時間運行的進程** 報告節點。

   ![long_running_node](assets/long_running_node.png)

   選擇報告時， **報表參數** 面板顯示在樹視圖的右側。

   ![長運行進程報表參數](assets/report_parameters_panel.png)

   參數:

   * **持續時間** (*強制*):指定持續時間和時間單位。 顯示運行時間超過指定持續時間的所有AEM Forms進程。
   * **開始時間** (*可選*):選擇日期。 篩選報表以顯示在指定日期後啟動的流程實例。
   * **開始時間** (*可選*):選擇日期。 篩選報表以顯示在指定日期之前啟動的流程實例。

1. 按一下 **開始** 的子菜單。

   報表顯示在 **報告** 位於 **流程報告** 的子菜單。

   ![long_running_processes](assets/long_running_processes.png)

   使用右上角的選項 **報告** 的子菜單。

   * **刷新**:使用儲存中的最新資料刷新報表
   * **更改圖例顏色**:選擇並更改報表圖例的顏色
   * **導出為CSV**:將資料從報表導出並下載到逗號分隔的檔案

## 「Process Duration」報告  {#process-duration-report}

「Process Duration」報告按每個實例已運行的天數顯示Forms進程的實例數。

### 執行「Process Duration」報告 {#to-execute-a-process-duration-report}

1. 要查看Oracle Process Reporting中的預定義報表，請在 **流程報告** 樹視圖，按一下 **報告** 的下界。
1. 按一下 **進程持續時間** 報告節點。

   ![process_duration_node](assets/process_duration_node.png)

   選擇報告時， **報表參數** 面板顯示在樹視圖的右側。

   ![長運行進程報表參數](assets/process_duration_params.png)

   參數:

   * **選擇流程** (*強制*):選擇一個AEM Forms進程。

1. 按一下 **開始** 的子菜單。

   報表顯示在 **報告** 對話框。

   ![process_duration_report](assets/process_duration_report.png)

   使用右上角的選項 **報告** 的子菜單。

   * **刷新**:使用儲存中的最新資料刷新報表
   * **更改圖例顏色**:選擇並更改報表圖例的顏色
   * **導出為CSV**:將資料從報表導出並下載到逗號分隔的檔案

## 工作流卷報告 {#workflow-volume-report}

「工作流卷」報告按日曆日顯示AEM Forms進程當前正在運行和已完成的實例數。

### 執行工作流卷報告 {#to-execute-a-workflow-volume-report}

1. 要查看Oracle Process Reporting中的預定義報表，請在 **流程報告** 樹視圖，按一下 **報告** 的下界。
1. 按一下 **工作流卷** 報告節點。

   ![工作流_卷_節點](assets/workflow_volume_node.png)

   選擇報告時， **報表參數** 面板顯示在樹視圖的右側。

   ![長運行進程報表參數](assets/workflow_volume_params.png)

   參數:

   * **選擇流程** (*強制*):選擇一個AEM Forms進程。

   * **開始時間** (*可選*):選擇日期。 篩選報表以顯示在指定日期後啟動的流程實例。

   * **開始時間** (*可選*):選擇日期。 篩選報表以顯示在指定日期之前啟動的流程實例。

1. 按一下 **開始** 的子菜單。

   報表顯示在 **報告** 位於 **流程報告** 的子菜單。

   ![工作流_卷_報告](assets/workflow_volume_report.png)

   使用右上角的選項 **報告** 的子菜單。

   * **刷新**:使用儲存中的最新資料刷新報表
   * **更改圖例顏色**:選擇並更改報表圖例的顏色
   * **導出為CSV**:將資料從報表導出並下載到逗號分隔的檔案
