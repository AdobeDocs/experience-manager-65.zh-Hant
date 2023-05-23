---
title: "MicrosoftSQL Server資料庫：微調配置"
seo-title: "Microsoft SQL Server database: Fine-tuning the configuration"
description: 瞭解如何優化MicrosoftSQL Server資料庫的配置。
seo-description: Learn how you can fine tune the configuration of your Microsoft SQL Server database.
uuid: 2d618aab-3c67-4edb-a28f-a20904689e6f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS, SG_AEMFORMS
discoiquuid: 70559a94-42ea-411a-a32f-5f38bc17ff96
exl-id: 9c570827-86e2-47d5-b8ae-66c0767bff2e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# MicrosoftSQL Server資料庫：微調配置 {#microsoft-sql-server-database-fine-tuning-the-configuration}

使用MicrosoftSQL Server時應更改預設配置設定。 按一下右鍵OracleEnterprise Manager中的本地伺服器以訪問屬性對話框。

## 記憶體設定 {#memory-settings}

將最小記憶體分配更改為盡可能大的數字。 如果資料庫在單獨的電腦上運行，請使用所有記憶體。 預設設定不會大幅分配記憶體，這會妨礙幾乎任何資料庫的效能。 在生產機器上分配記憶體時，您應該最積極。

## 處理器設定 {#processor-settings}

修改處理器設定，最重要的是，選中Boost SQL Server Priority On Windows複選框，以便伺服器使用盡可能多的週期。 「使用NT光纖」(Use NT Fibres)設定不那麼重要，但您可能也想選擇它。

## 資料庫設定 {#database-settings}

更改資料庫設定。 最重要的設定是「恢復間隔」，它指定在崩潰後等待恢復的最長時間。 預設設定為1分鐘。 使用5到15分鐘的較大值可提高效能，因為它使伺服器有更多時間將更改從資料庫日誌寫入資料庫檔案。

>[!NOTE]
>
>此設定不會危害事務行為，因為它只更改啟動時必須完成的日誌檔案重放的長度。

將日誌和資料檔案的「已分配空間」大小設定為比初始資料庫大得多。 請考慮資料庫在一年內可以增長多少。 理想情況下，日誌和資料檔案以連續的方式分配，這樣資料就不會在整個磁碟上碎片化。
