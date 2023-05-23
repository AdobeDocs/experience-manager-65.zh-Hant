---
title: 針對EMC Documentum用戶的Connector備份策略
seo-title: Backup strategy for Connector for EMC Documentum users
description: 檢查如何為EMC Documentum用戶建立Connector備份策略。
seo-description: Check how to create a backup strategy for Connector for EMC Documentum users.
uuid: 5d8a0476-5231-4e1d-96c4-ae3df68e09f0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e83b1a59-a730-4d22-9d58-1c9c38e5d534
exl-id: b759b936-5907-4311-a5cc-60f321476368
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# 針對EMC Documentum用戶的Connector備份策略 {#backup-strategy-for-connector-for-emc-documentum-users}

如果安裝了Connector for EMC Documentum ，則除本章中的說明外，備份和恢復策略還必須包括備份（或恢復）各個ECM系統所安裝的電腦。 （請參見ECM Documentum文檔）。

使用ECM存AEM儲庫並執行以下任務來備份您的表單環境：

* 按照本AEM文檔中所述的說明備份表單。
* 按照中的說明備份ECM Documentum系統 [備份EMC Documentum Content Server](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#back-up-the-emc-documentum-content-server)。

使用AEMECM儲存庫並執行以下任務來恢復表單環境：

* 按照中的說明恢復各自的ECM系統 [恢復EMC Documentum Content Server](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#restore-the-emc-documentum-content-server)。
* 按照AEM本文檔中介紹的說明恢復表單。
