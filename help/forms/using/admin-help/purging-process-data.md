---
title: 清除流程資料
seo-title: 清除流程資料
description: 在呼叫長期處理時產生的處理資料可能會過大，導致AEM表單效能降低，並使用不必要的磁碟空間。 瞭解如何清除流程資料。
seo-description: 在呼叫長期處理時產生的處理資料可能會過大，導致AEM表單效能降低，並使用不必要的磁碟空間。 瞭解如何清除流程資料。
uuid: 2f04452c-71c6-452c-88c2-7560d35e7dec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3157bb92-4b07-40f2-be4c-8f5807f9a380
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 清除流程資料 {#purging-process-data}

在呼叫長期處理時產生的處理資料可能會過大，導致AEM表單效能降低，並使用不必要的磁碟空間。 在不再需要記錄時清除流程資料是很好的做法。 AEM表格提供數種清除流程資料的方式：

* 您可以使用管理控制台執行與長期流程相關的過時記錄的一次性清除，或計畫定期自動清除。 (請參 [閱從作業管理器資料庫清除記錄](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database)。)
* 您可以使用AEM表單Java API和web service API，以程式設計方式清除與長期處理相關的處理資料。 (請參閱「使用AEM表單進行程式設計」 [中的「清除流程資料](https://www.adobe.com/go/learn_aemforms_programming_63)」)。
* 使用流程清除工具根據流程名稱和其他參數清除流程。 如需詳細資訊，請參閱程式清除工具讀我檔案， *[位於aem_forms根目錄]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt。

