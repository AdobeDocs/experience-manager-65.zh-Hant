---
title: EMC Documentum&reg；使用者的聯結器備份策略
description: 瞭解如何為EMC Documentum&reg；使用者建立聯結器備份策略。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: b759b936-5907-4311-a5cc-60f321476368
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%
---
# EMC Documentum®使用者的Connector備份策略 {#backup-strategy-for-connector-for-emc-documentum-users}

如果您已安裝Connector for EMC Documentum® ，則除了本章的說明以外，您的備份與復原策略還必須包括備份（或復原）安裝ECM系統的電腦。 （請參閱ECM Documentum®檔案）。

使用ECM存放庫並執行下列工作，備份AEM表單環境：

* 依照本檔案所述的指示，備份AEM表單。
* 依照[備份EMC Documentum® Content Server](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#back-up-the-emc-documentum-content-server)中的指示來備份您的ECM Documentum®系統。

使用ECM存放庫並執行下列工作來還原AEM表單環境：

* 依照[還原EMC Documentum® Content Server](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#restore-the-emc-documentum-content-server)中的指示，還原您個別的ECM系統。
* 依照本檔案所述指示還原AEM表單。
