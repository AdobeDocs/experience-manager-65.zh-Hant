---
title: 程式報表中的預先定義報表
description: 查詢JEE上的AEM Forms程式資料，以建立長時間執行程式、程式持續時間和工作流程量的報告
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: 34e55676-6332-4616-aecc-bcc8cc1e8a29
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 0%

---

# 程式報表中的預先定義報表 {#pre-defined-reports-in-process-reporting}

## 程式中的預先定義報表 {#pre-defined-reports-in-process-reporting-1}

AEM Forms Process Reporting隨附下列&#x200B;*個現成可用的報告*：

* **[長時間執行的處理序](#long-running-processes)**：需要超過指定時間才能完成之所有AEM Forms處理序的報告
* **[處理序持續時間圖表](#process-duration-report)**：指定的AEM Forms處理序報告（依持續時間）
* **[工作流程磁碟區](#workflow-volume-report)**：指定處理序的執行中及完成的執行個體報告（依日期）

## 長時間執行的程式 {#long-running-processes}

「長時間執行的程式」報表會顯示花費超過指定時間完成的AEM Forms程式。

### 執行長時間執行處理作業報告 {#to-execute-a-long-running-process-report}

1. 若要檢視「程式報告」中的預先定義報告清單，請在&#x200B;**程式報告**&#x200B;樹狀檢視上，按一下&#x200B;**報告**&#x200B;節點。
1. 按一下&#x200B;**長時間執行處理序**&#x200B;報告節點。

   ![long_running_node](assets/long_running_node.png)

   當您選取報表時，**報表引數**&#x200B;面板會顯示在樹狀檢視的右側。

   ![長時間執行的處理序報告引數面板](assets/report_parameters_panel.png)

   引數：

   * **期間** （*必要*）：指定期間和時間單位。 顯示執行時間超過指定持續時間的所有AEM Forms程式。
   * **開始於**&#x200B;之後（*選擇性*）：選取日期。 篩選報告以顯示指定日期後開始的程式執行個體。
   * **開始於**&#x200B;之前（*選擇性*）：選取日期。 篩選報告以顯示於指定日期前開始的程式執行個體。

1. 按一下&#x200B;**執行**&#x200B;以執行報告。

   報告會顯示在&#x200B;**處理報告**&#x200B;視窗右側的&#x200B;**報告**&#x200B;面板中。

   ![long_running_processes](assets/long_running_processes.png)

   使用&#x200B;**報表**&#x200B;面板右上角的選項，在報表上執行下列操作。

   * **重新整理**：以存放裝置中的最新資料重新整理報告
   * **變更圖例色彩**：選取並變更報表圖例的色彩
   * **匯出至CSV**：將資料從報表匯出並下載至逗號分隔的檔案

## 處理期間報表  {#process-duration-report}

「處理持續時間」報表會依每個執行個體執行的天數顯示Forms處理的執行個體數量。

### 執行處理期間報告 {#to-execute-a-process-duration-report}

1. 若要檢視「程式報告」中的預先定義報告，請在&#x200B;**程式報告**&#x200B;樹狀檢視上，按一下&#x200B;**報告**&#x200B;節點。
1. 按一下&#x200B;**處理期間**&#x200B;報告節點。

   ![process_duration_node](assets/process_duration_node.png)

   當您選取報表時，**報表引數**&#x200B;面板會顯示在樹狀檢視的右側。

   ![長時間執行的處理序報告引數面板](assets/process_duration_params.png)

   引數：

   * **選取處理序** （*強制*）：選取AEM Forms處理序。

1. 按一下&#x200B;**執行**&#x200B;以執行報告。

   報告會顯示在「程式報告」視窗右側的&#x200B;**報告**&#x200B;面板中。

   ![process_duration_report](assets/process_duration_report.png)

   使用&#x200B;**報表**&#x200B;面板右上角的選項，在報表上執行下列操作。

   * **重新整理**：以存放裝置中的最新資料重新整理報告
   * **變更圖例色彩**：選取並變更報表圖例的色彩
   * **匯出至CSV**：將資料從報表匯出並下載至逗號分隔的檔案

## 工作流程數量報告 {#workflow-volume-report}

「工作流程數量」報表會依日曆日顯示目前執行中及已完成的AEM Forms處理序執行個體數目。

### 執行工作流程磁碟區報告 {#to-execute-a-workflow-volume-report}

1. 若要檢視「程式報告」中的預先定義報告，請在&#x200B;**程式報告**&#x200B;樹狀檢視上，按一下&#x200B;**報告**&#x200B;節點。
1. 按一下&#x200B;**工作流程磁碟區**&#x200B;報告節點。

   ![workflow_volume_node](assets/workflow_volume_node.png)

   當您選取報表時，**報表引數**&#x200B;面板會顯示在樹狀檢視的右側。

   ![長時間執行的處理序報告引數面板](assets/workflow_volume_params.png)

   引數：

   * **選取處理序** （*強制*）：選取AEM Forms處理序。

   * **開始於**&#x200B;之後（*選擇性*）：選取日期。 篩選報告以顯示指定日期後開始的程式執行個體。

   * **開始於**&#x200B;之前（*選擇性*）：選取日期。 篩選報告以顯示指定日期前開始的程式執行個體。

1. 按一下&#x200B;**執行**&#x200B;以執行報告。

   報告會顯示在&#x200B;**處理報告**&#x200B;視窗右側的&#x200B;**報告**&#x200B;面板中。

   ![workflow_volume_report](assets/workflow_volume_report.png)

   使用&#x200B;**報表**&#x200B;面板右上角的選項，在報表上執行下列操作。

   * **重新整理**：以存放裝置中的最新資料重新整理報告
   * **變更圖例色彩**：選取並變更報表圖例的色彩
   * **匯出至CSV**：將資料從報表匯出並下載至逗號分隔的檔案
