---
title: 「Microsoft SQL Server資料庫：微調組態」
description: 瞭解如何微調Microsoft SQL Server資料庫的設定。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS, SG_AEMFORMS
exl-id: 9c570827-86e2-47d5-b8ae-66c0767bff2e
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# Microsoft SQL Server資料庫：微調組態 {#microsoft-sql-server-database-fine-tuning-the-configuration}

使用Microsoft SQL Server時，您應該變更預設組態設定。 在OracleEnterprise Manager中以滑鼠右鍵按一下本機伺服器，以存取特性對話方塊。

## 記憶體設定 {#memory-settings}

將最小記憶體配置變更為儘可能大的數字。 如果資料庫是在另一部電腦上執行，請使用所有記憶體。 預設設定不會積極地分配記憶體，這會阻礙幾乎任何資料庫的效能。 您應在生產機器上最積極地配置記憶體。

## 處理器設定 {#processor-settings}

修改處理器設定，最重要的是選取[Boost SQL Server Priority On Windows]核取方塊，讓伺服器使用儘可能多的週期。 「使用NT光纖」設定不太重要，但您也可以選取它。

## 資料庫設定 {#database-settings}

變更資料庫設定。 最重要的設定是「復原間隔」，它指定當機後等待復原的最長時間。 預設設定為一分鐘。 使用較大的值（從5分鐘到15分鐘）可改善效能，因為可讓伺服器有更多的時間將資料庫記錄檔的變更寫入資料庫檔案。

>[!NOTE]
>
>此設定不會影響交易行為，因為它只會變更啟動時必須執行的記錄檔重新執行長度。

將記錄檔和資料檔案的「已配置空間」大小設定為比初始資料庫大很多。 考慮資料庫在一年中的成長量。 理想情況下，記錄檔和資料檔會以連續範圍配置，以免資料最後分散到整個磁碟上。
