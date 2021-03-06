---
title: 清除流程資料
seo-title: 清除流程資料
description: 調用長壽命進程時生成的進程資料可能會變得太大，導致AEM表單效能降低，並且會使用不必要的磁碟空間。 了解如何清除流程資料。
seo-description: 調用長壽命進程時生成的進程資料可能會變得太大，導致AEM表單效能降低，並且會使用不必要的磁碟空間。 了解如何清除流程資料。
uuid: 2f04452c-71c6-452c-88c2-7560d35e7dec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3157bb92-4b07-40f2-be4c-8f5807f9a380
exl-id: 0da59dbe-f050-4ee5-b74c-4380b3543b97
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# 清除進程資料{#purging-process-data}

調用長壽命進程時生成的進程資料可能會變得太大，導致AEM表單效能降低，並且會使用不必要的磁碟空間。 當不再需要記錄時，最好清除流程資料。 AEM forms提供多種清除程式資料的方式：

* 您可以使用管理控制台執行與長期流程相關的過時記錄的一次性清除，或計畫定期自動清除。 （請參閱從作業管理器資料庫](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database)清除記錄。）[
* 您可以使用AEM Forms Java API和網站服務API，以程式設計方式清除與長期程式相關的程式資料。 (請參閱[使用AEM表單寫程式](https://www.adobe.com/go/learn_aemforms_programming_63)中的「清除流程資料」。)
* 使用流程清除工具根據流程名稱和其他參數清除流程。 如需詳細資訊，請參閱位於&#x200B;*[aem_forms根]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt的流程清除工具自述檔案。
