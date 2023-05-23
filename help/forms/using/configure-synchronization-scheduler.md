---
title: 配置同步調度程式
seo-title: Configuring the synchronization scheduler
description: 瞭解如何遷移和同步資產、配置同步計畫程式以及使用資料夾來安排資產。
seo-description: Learn how to migrate and sync assets, configure sync scheduler, and use folders to arrange assets.
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
source-wordcount: '286'
ht-degree: 0%

---

# 配置同步調度程式 {#configuring-the-synchronization-scheduler}

預設情況下，同步計畫程式每3分鐘運行一次，以通過LiveCycleWorkbench 11同步儲存庫中修改和更新的所有資產。 一旦同步過程完成，包含表單和資源的應用程式在AEM Forms用戶介面中就可見。

## 更改同步調度程式的間隔 {#change-interval-of-the-synchronization-scheduler}

執行以下步驟以更改同步調度程式的間隔：

1. 登錄到AEMConfiguration Manager。 Configuration Manager的URL為 `https://'[server]:[port]'/lc/system/console/configMgr`

1. 查找並開啟 **FormsManager配置** 捆綁。

1. 為 **同步調度程式頻率** 的雙曲餘切值。

   頻率單位為分鐘。 例如，要將調度程式配置為每60分鐘運行一次，請指定60。

## 同步資產 {#synchronizing-assets}

您可以使用 **同步儲存庫中的資產** 選項來手動同步資產。 執行以下步驟以手動同步資產：

1. 登錄AEM Forms。 預設URL為 `https://'[server]:[port]'/lc/aem/forms/`。

   ![AEM Forms用戶介面](assets/aem_forms_ui.png)

   **圖：** *AEM Forms用戶介面*

1. 按一下 ![aem6forms_sync](assets/aem6forms_sync.png) 的子菜單。 如果您在上次配置的路徑上沒有任何資產，則對話框如下所示。 按一下 **開始** 啟動同步。

   ![「同步」對話框](assets/migrate-and-syncronize.png)

   **圖：** *「同步」對話框*

## 排除同步錯誤 {#troubleshooting-synchronization-error}

您可以在工作流設計器(LiveCycle工作台)中建立新應用程式。

如果新建立的應用程式和/content/dam/formsanddocuments上的資料夾具有相同的名稱，則出現錯誤&quot;*根級別已存在與此應用程式同名的資產。*&#x200B;已記錄。

要解決衝突，請更名應用程式並手動同步資產。

![資產同步對話框中的衝突](assets/sync-conflict.png)

**圖：** *資產同步對話框中的衝突*
