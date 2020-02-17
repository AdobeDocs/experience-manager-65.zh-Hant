---
title: 針對EMC Documentum用戶的Connector備份戰略
seo-title: 針對EMC Documentum用戶的Connector備份戰略
description: 檢查如何為EMC Documentum用戶建立Connector備份策略。
seo-description: 檢查如何為EMC Documentum用戶建立Connector備份策略。
uuid: 5d8a0476-5231-4e1d-96c4-ae3df68e09f0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e83b1a59-a730-4d22-9d58-1c9c38e5d534
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 針對EMC Documentum用戶的Connector備份戰略 {#backup-strategy-for-connector-for-emc-documentum-users}

如果您安裝了Connector for EMC Documentum，除本章中的說明外，您的備份和恢復策略還必須包括備份（或恢復）相應ECM系統所安裝的電腦。 （請參閱ECM Documentum文檔）。

使用ECM儲存庫並執行下列工作，以備份AEM表單環境：

* 依照本檔案所述的指示，備份AEM表格。
* 按照備份EMC Documentum Content Server中的說明， [備份您的ECM Documentum系統](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#back-up-the-emc-documentum-content-server)。

使用ECM儲存庫並執行下列工作，以還原AEM表單環境：

* 按照恢復EMC Documentum Content Server中的說明，恢 [復您各自的ECM系統](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#restore-the-emc-documentum-content-server)。
* 依照本檔案所述的指示，還原AEM表格。

