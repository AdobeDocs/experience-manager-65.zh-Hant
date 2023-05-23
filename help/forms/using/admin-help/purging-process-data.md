---
title: 清除流程資料
seo-title: Purging process data
description: 調用長壽命進程時生成的進程資料可能會變得過大，導致表AEM單效能降低，並且使用不必要的磁碟空間。 瞭解如何清除流程資料。
seo-description: Process data that is generated when a long-lived process is invoked can become too large, resulting in lower AEM forms performance and the use of unnecessary disk space. See how you can purge process data.
uuid: 2f04452c-71c6-452c-88c2-7560d35e7dec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3157bb92-4b07-40f2-be4c-8f5807f9a380
exl-id: 0da59dbe-f050-4ee5-b74c-4380b3543b97
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# 清除流程資料 {#purging-process-data}

調用長壽命進程時生成的進程資料可能會變得過大，導致表AEM單效能降低，並且使用不必要的磁碟空間。 最好在不再需要記錄時清除流程資料。 表AEM單提供了多種清除流程資料的方法：

* 您可以使用管理控制台執行與長期進程相關的過時記錄一次性清除，或計畫定期自動清除。 (請參閱 [從作業管理器資料庫中清除記錄](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database)。)
* 可以使用Java APIAEM和Web服務API表單以寫程式方式清除與長期進程相關的進程資料。 (請參閱中的「清除流程資料」 [用表格編AEM程](https://www.adobe.com/go/learn_aemforms_programming_63)。)
* 使用流程清除工具根據流程名稱和其它參數清除流程。 有關詳細資訊，請參閱「進程清除工具」自述檔案， *[aem_forms根]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt。
