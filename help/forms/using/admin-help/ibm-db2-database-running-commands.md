---
title: 「IBM DB2資料庫：執行命令以進行定期維護」
description: 本檔案列出定期維護AEM表單資料庫所建議的IBM DB2命令。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7a4281e7-1544-473a-a471-e9a4c2819a58
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# IBM DB2資料庫：執行命令以進行定期維護 {#ibm-db-database-running-commands-for-regular-maintenance}

建議您使用下列IBM DB2命令，以定期維護AEM表單資料庫。 如需有關DB2資料庫之維護與效能調整的詳細資訊，請參閱 *IBM DB2 Administration指南*.

* **runstats：** 這個命令會更新描述資料庫表格實體特性的統計資料，以及相關的索引。 AEM表單產生的動態SQL敘述句會自動使用這些更新的統計資料，但建置在資料庫內的靜態SQL敘述句需要 `db2rbind` 命令也會執行。
* **db2rbind：** 這個命令會重新繫結資料庫中的所有套裝程式。 執行後，請使用此命令 `runstats` 用來重新驗證資料庫中所有套件的公用程式。
* **重組表格或索引：** 這個命令會檢查是否需要對某些表格和索引進行重新整理。

  隨著資料庫的成長與變更，重新計算表格統計資料對於改善資料庫效能至關重要，應定期進行。 這些命令可以使用指令碼手動執行，也可以使用cron作業手動執行。

>[!NOTE]
>
>在您執行 `runstats` 命令，資料庫必須包含資料，而且至少必須已執行一個目錄同步處理。

若是小型資料庫（例如10,000位使用者或2,500個群組），只要叫用 `runstats` 減少同步處理時間的命令。

對於大型資料庫（例如100,000位使用者或10,000個群組），請執行 `reorg` 命令執行之前 `runstats` 命令。

## 在您的AEM表單資料庫上使用runstats命令 {#use-the-runstats-command-on-your-aem-forms-database}

執行 `runstats` 命令於下列AEM forms資料庫表格和索引。

>[!NOTE]
>
>此 `runstats` 命令只需要在第一次資料庫同步處理期間執行。 但是，必須在該過程中執行兩次：一次是在同步化使用者和群組期間，另一次是在同步化群組成員期間。 請確定每次執行時指令碼都會完全執行。

如需正確語法和使用方式，請參閱資料庫製造商的檔案。 下， `<schema>` 用於表示與您的DB2使用者名稱相關聯的結構描述。 如果您有簡單的預設DB2安裝，這是資料庫架構名稱。

```sql
     TABLE <schema>.EDCPRINCIPALGROUPENTITY
 
     TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY
 
     TABLE <schema>.EDCPRINCIPALENTITY
 
     TABLE <schema>.EDCPRINCIPALUSERENTITY
 
     TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY
 
     TABLE <schema>.EDCPRINCIPALENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALUSERENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALGROUPENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY FOR INDEXES ALL
```

## 在您的AEM表單資料庫上執行reorg命令 {#run-the-reorg-command-on-your-aem-forms-database}

執行 `reorg` 命令於下列AEM forms資料庫表格和索引。 如需正確語法和使用方式，請參閱資料庫製造商的檔案。

```sql
     TABLE <schema>.EDCPRINCIPALGROUPENTITY
 
     TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY
 
     TABLE <schema>.EDCPRINCIPALENTITY
 
     TABLE <schema>.EDCPRINCIPALUSERENTITY
 
     TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALUSERENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALGROUPENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY
```
