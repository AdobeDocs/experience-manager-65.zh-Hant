---
title: 流程報告中的預定義報告
seo-title: 流程報告中的預定義報告
description: 查詢JEE上的AEM Forms流程資料，以建立有關長期執行的流程、流程持續時間和工作流程卷的報表
seo-description: 查詢JEE上的AEM Forms流程資料，以建立有關長期執行的流程、流程持續時間和工作流程卷的報表
uuid: 704a8886-90ea-4793-a3fc-f998f878c928
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d93375e-ec37-4445-96ea-d315676787b4
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# 流程報告中的預定義報告 {#pre-defined-reports-in-process-reporting}

## 預先定義的在制報表 {#pre-defined-reports-in-process-reporting-1}

AEM Forms Process Reporting隨附下列現 *成可用的報表* :

* **[長時間運行的進程](#long-running-processes)**:所有AEM Forms進程的報表，這些流程需要超過指定的時間才能完成
* **[流程持續時間圖](#process-duration-report)**:依持續時間的指定AEM Forms流程報表
* **[工作流量](#workflow-volume-report)**:按日期列出指定流程的運行和完成實例的報告

## 長時間運行的進程 {#long-running-processes}

「長時間執行的流程」報表會顯示已花費超過指定時間完成的AEM Forms流程。

### 要執行長時間運行的進程報告 {#to-execute-a-long-running-process-report}

1. 要在「流程報告」中查看預定義報告的清單，請在「流程報告」樹狀 **視圖中** ，按一下「**報告」**節點。
1. 按一下「長 **運行進程** 」報告節點。

   ![long_running_node](assets/long_running_node.png)

   選擇報表時，樹狀 **視圖右側會顯示** 「報表參數」面板。

   ![長運行進程報告參數面板](assets/report_parameters_panel.png)

   參數:

   * **持續時間**(*必填*):指定持續時間和時間單位。 顯示已執行超過指定期間的所有AEM Forms進程。
   * **Started After** (*可選*):選擇日期。 篩選報表以顯示指定日期之後開始的流程例項。
   * **開始前** (*可選*):選擇日期。 篩選報表以顯示指定日期之前開始的流程例項。

1. 按一 **下開始** ，執行報表。

   報表顯示在「流程報表」視窗右側的「**報表*」 **面板中** 。

   ![long_running_processes](assets/long_running_processes.png)

   使用**報表**面板右上角的選項，對報表執行下列操作。

   * **刷新**:在儲存區中重新整理含有最新資料的報表
   * **變更圖例顏色**:選擇並變更報表圖例的顏色
   * **匯出至CSV**:將報表中的資料匯出並下載至逗號分隔的檔案

## 流程持續時間報告 {#process-duration-report}

「流程持續時間」報表會依據每個例項已執行的天數，顯示表單流程的例項數。

### 要執行「進程持續時間」報告，請執行以下操作： {#to-execute-a-process-duration-report}

1. 要在「流程報告」中查看預定義的報告，請在「流程報告」樹 **視圖中** ，按一下「**報告」**節點。
1. 按一下「進 **程持續時間** 」報告節點。

   ![process_duration_node](assets/process_duration_node.png)

   選擇報表時，樹狀 **視圖右側會顯示** 「報表參數」面板。

   ![長運行進程報告參數面板](assets/process_duration_params.png)

   參數:

   * **選擇流程**(必&#x200B;*備*):選取AEM Forms程式。

1. 按一下**前往**以執行報表。

   報表顯示在「流程報表」視窗右側的**報表**面板中。

   ![process_duration_report](assets/process_duration_report.png)

   使用**報表**面板右上角的選項，對報表執行下列操作。

   * **刷新**:在儲存區中重新整理含有最新資料的報表
   * **變更圖例顏色**:選擇並變更報表圖例的顏色
   * **匯出至CSV**:將報表中的資料匯出並下載至逗號分隔的檔案

## 「Workflow Volume」報告 {#workflow-volume-report}

「工作流量」報表會依日曆日顯示目前執行和完成的AEM Forms流程例項數。

### 要執行「工作流卷」報告 {#to-execute-a-workflow-volume-report}

1. 要在「流程報告」中查看預定義的報告，請在**流程報告**樹視圖中按一下**報表**節點。
1. 按一下「工 **作流卷** 」報告節點。

   ![workflow_volume_node](assets/workflow_volume_node.png)

   選擇報表時，樹狀 **視圖右側會顯示** 「報表參數」面板。

   ![長運行進程報告參數面板](assets/workflow_volume_params.png)

   參數:

   * **選擇流程**(必&#x200B;*備*):選取AEM Forms程式。

   * **Started After** (*可選*):選擇日期。 篩選報表以顯示指定日期之後開始的流程例項。

   * **開始前** (*可選*):選擇日期。 篩選報表以顯示指定日期之前開始的流程例項。

1. 按一下**前往**以執行報表。

   報表顯示在「流程報表」視窗右側的「**報表*」 **面板中** 。

   ![workflow_volume_report](assets/workflow_volume_report.png)

   使用**報表**面板右上角的選項，對報表執行下列操作。

   * **刷新**:在儲存區中重新整理含有最新資料的報表
   * **變更圖例顏色**:選擇並變更報表圖例的顏色
   * **匯出至CSV**:將報表中的資料匯出並下載至逗號分隔的檔案

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
