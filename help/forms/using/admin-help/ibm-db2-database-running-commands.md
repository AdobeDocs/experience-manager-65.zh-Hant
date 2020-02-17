---
title: '"IBM DB2資料庫：運行用於定期維護的命令"'
seo-title: '"IBM DB2資料庫：運行用於定期維護的命令"'
description: 本檔案列出IBM DB2命令，建議您定期維護AEM表單資料庫。
seo-description: 本檔案列出IBM DB2命令，建議您定期維護AEM表單資料庫。
uuid: 235d59df-b9b9-4770-8b7d-00713701c3c2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a62b68b4-7735-49b1-8938-f0d9e4c4a051
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# IBM DB2資料庫：運行用於定期維護的命令 {#ibm-db-database-running-commands-for-regular-maintenance}

建議使用下列IBM DB2命令，以定期維護AEM表單資料庫。 有關DB2資料庫的維護和效能優化的詳細資訊，請參見 *IBM DB2 Administration Guide*。

* **** runstats:此命令更新描述資料庫表的物理特性及其相關索引的統計資訊。 由AEM表單產生的動態SQL陳述式會自動使用這些更新的統計資料，但資料庫內建的靜態SQL陳述式也需要 `db2rbind` 執行命令。
* **** db2rbind:此命令重新綁定資料庫中的所有包。 運行該實用程式後，請使 `runstats` 用此命令重新驗證資料庫中的所有包。
* **** 重組表或索引：此命令檢查是否需要對某些表和索引進行重組。

   隨著資料庫的增長和更改，重新計算表統計資訊對於提高資料庫效能至關重要，應定期執行。 這些命令可以通過使用指令碼或使用cron作業手動運行。

>[!NOTE]
>
>在運行該命 `runstats` 令之前，資料庫必須包含資料，並且至少必須執行一個目錄同步。

對於小型資料庫（如10,000個用戶或2,500個組），調用命令就足以減少 `runstats` 同步定時。

對於較大的資料庫（如100,000個用戶或10,000個組），在運行命 `reorg` 令之前運行該 `runstats` 命令。

## 在您的AEM表單資料庫上使用runstats命令 {#use-the-runstats-command-on-your-aem-forms-database}

在下列AEM `runstats` 表單資料庫表格和索引上執行命令。

>[!NOTE]
>
>該 `runstats` 命令只需要在第一個資料庫同步期間運行。 不過，在該程式中必須執行兩次：在用戶和組的同步期間，在組成員的同步期間。 確保指令碼在每次運行時都完全執行。

如需正確的語法和用法，請參閱資料庫製造商的檔案。 下面， `<schema>` 用於表示與DB2用戶名關聯的模式。 如果您有簡單的預設DB2安裝，則此為資料庫架構名稱。

```as3
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

在下列AEM `reorg` 表單資料庫表格和索引上執行命令。 如需正確的語法和用法，請參閱資料庫製造商的檔案。

```as3
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

