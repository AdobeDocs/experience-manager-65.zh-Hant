---
title: 清除程式資料
description: 叫用長期處理程式時所產生的處理程式資料可能會變得太大，導致AEM表單效能降低及不必要的磁碟空間浪費。 瞭解如何永久刪除處理資料。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0da59dbe-f050-4ee5-b74c-4380b3543b97
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# 清除程式資料 {#purging-process-data}

叫用長期處理程式時所產生的處理程式資料可能會變得太大，導致AEM表單效能降低及不必要的磁碟空間浪費。 當不再需要記錄時，清除處理資料是很好的做法。 AEM forms提供數種清除流程資料的方法：

* 您可以使用管理主控台，執行一次性永久刪除與長期處理相關的過時記錄，或排程定期自動永久刪除。 (請參閱 [從「工作管理員」資料庫中清除記錄](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database).)
* 您可以使用AEM表單Java API和Web服務API，以程式設計方式清除與長期流程相關的流程資料。 （請參閱中的「永久刪除程式資料」） [使用AEM表單進行程式設計](https://www.adobe.com/go/learn_aemforms_programming_63).)
* 使用處理永久刪除工具，根據處理名稱和其他引數永久刪除處理。 如需詳細資訊，請參閱處理清除工具Readme檔案，位於 *[aem_forms根]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt.
