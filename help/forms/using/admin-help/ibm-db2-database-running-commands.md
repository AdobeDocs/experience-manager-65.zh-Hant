---
title: "IBMDB2資料庫：運行用於定期維護的命令"
seo-title: "IBM DB2 database: Running commands for regular maintenance"
description: 本文檔列出了建議定期維護表單資料庫的IBMDB2AEM命令。
seo-description: This document lists IBM DB2 commands that are recommended for regular maintenance of your AEM forms database.
uuid: 235d59df-b9b9-4770-8b7d-00713701c3c2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a62b68b4-7735-49b1-8938-f0d9e4c4a051
exl-id: 7a4281e7-1544-473a-a471-e9a4c2819a58
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# IBMDB2資料庫：運行用於定期維護的命令 {#ibm-db-database-running-commands-for-regular-maintenance}

建議使用以下IBMDB2命令定期維護AEM表單資料庫。 有關DB2資料庫的維護和效能調整的詳細資訊，請參見 *IBMDB2管理指南*。

* **運行狀態：** 此命令更新描述資料庫表的物理特徵及其關聯索引的統計資訊。 由表單生成的動態SQLAEM語句會自動使用這些更新的統計資訊，但在資料庫內構建的靜態SQL陳述式要求 `db2rbind` 命令也運行。
* **db2rbind:** 此命令重新綁定資料庫中的所有包。 運行 `runstats` 用於重新驗證資料庫中的所有包的實用程式。
* **重組表或索引：** 此命令檢查是否需要對某些表和索引進行重組。

   隨著資料庫的增長和更改，重新計算表統計資訊對於提高資料庫效能至關重要，應定期執行。 這些命令可以通過使用指令碼或使用cron作業手動運行。

>[!NOTE]
>
>在運行 `runstats` 命令，資料庫必須包含資料，並且至少必須執行一個目錄同步。

對於小型資料庫，如10 000個用戶或2 500個組，就足以調用 `runstats` 命令來減少同步計時。

對於較大的資料庫，如100,000個用戶或10,000個組，運行 `reorg` 命令 `runstats` 的子菜單。

## 在表單資料庫上使AEM用runstats命令 {#use-the-runstats-command-on-your-aem-forms-database}

運行 `runstats` 命令AEM。

>[!NOTE]
>
>的 `runstats` 命令只需在第一次資料庫同步期間運行。 但是，在此過程中必須運行兩次：在用戶和組的同步期間，然後在組成員的同步期間。 確保每次運行指令碼時指令碼都完全執行。

有關正確的語法和用法，請參閱資料庫製造商的文檔。 下面， `<schema>` 用於表示與DB2用戶名關聯的架構。 如果安裝了簡單的預設DB2，則這是資料庫架構名稱。

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

## 在表單資料庫上運AEM行reorg命令 {#run-the-reorg-command-on-your-aem-forms-database}

運行 `reorg` 命令AEM。 有關正確的語法和用法，請參閱資料庫製造商的文檔。

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
