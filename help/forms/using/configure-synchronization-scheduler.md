---
title: 配置同步調度程式
seo-title: 配置同步調度程式
description: 了解如何移轉和同步資產、設定同步排程器，以及使用資料夾來排列資產。
seo-description: 了解如何移轉和同步資產、設定同步排程器，以及使用資料夾來排列資產。
uuid: b2c89feb-2947-418a-b343-4c01e453602b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 8c8b1998-eab4-4230-b24f-5e96883ba599
docset: aem65
role: Admin
exl-id: 34db1f76-ee40-4612-85da-22041e7560fb
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# 配置同步調度程式 {#configuring-the-synchronization-scheduler}

依預設，同步排程器會每3分鐘執行一次，以透過LiveCycle工作台11同步儲存庫中修改和更新的所有資產。 同步程式完成後，包含表單和資源的應用程式就會顯示在AEM Forms使用者介面中。

## 更改同步調度程式的間隔 {#change-interval-of-the-synchronization-scheduler}

執行以下步驟更改同步調度程式的間隔：

1. 登入AEM Configuration Manager。 Configuration Manager的URL為`https://'[server]:[port]'/lc/system/console/configMgr`

1. 找到並開啟&#x200B;**FormsManagerConfiguration**&#x200B;套件組合。

1. 為&#x200B;**同步調度程式頻率**&#x200B;選項指定新值。

   頻率單位為分鐘。 例如，若要將排程器設定為每60分鐘執行一次，請指定60。

## 同步資產 {#synchronizing-assets}

您可以使用&#x200B;**從存放庫同步資產**&#x200B;選項，以手動同步資產。 執行下列步驟以手動同步資產：

1. 登入AEM Forms。 預設URL為`https://'[server]:[port]'/lc/aem/forms/`。

   ![AEM Forms使用者介面](assets/aem_forms_ui.png)

   **圖：** *AEM Forms使用者介面*

1. 按一下工具列中的![aem6forms_sync](assets/aem6forms_sync.png)圖示。 如果您在最後設定的路徑上沒有任何資產，則會顯示對話方塊，如下所示。 按一下&#x200B;**Start**&#x200B;以啟動同步。

   ![同步對話框](assets/migrate-and-syncronize.png)

   **圖：** *同步對話框*

## 排除同步錯誤 {#troubleshooting-synchronization-error}

您可以在工作流設計工具(LiveCycle工作台)中建立新應用程式。

如果新建立的應用程式和/content/dam/formsanddocuments上的資料夾具有相同的名稱，則根級別已存在「*與此應用程式同名的資產」錯誤。*「 」已記錄。

若要解決衝突，請重新命名應用程式，並手動同步資產。

![資產同步對話方塊中的衝突](assets/sync-conflict.png)

**圖：** *資產同步對話方塊中的衝突*
