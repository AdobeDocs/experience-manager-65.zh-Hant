---
title: 配置同步調度程式
seo-title: 配置同步調度程式
description: 瞭解如何移轉和同步資產、設定同步排程器，以及使用資料夾來排列資產。
seo-description: 瞭解如何移轉和同步資產、設定同步排程器，以及使用資料夾來排列資產。
uuid: b2c89feb-2947-418a-b343-4c01e453602b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 8c8b1998-eab4-4230-b24f-5e96883ba599
docset: aem65
translation-type: tm+mt
source-git-commit: 27695ee7880cfa23d504d723297c9a06729a424b

---


# 配置同步調度程式 {#configuring-the-synchronization-scheduler}

依預設，同步排程器會在每3分鐘後執行，以透過LiveCycle Workbench 11同步儲存庫中修改和更新的所有資產。 同步程式完成後，包含表單和資源的應用程式就會顯示在AEM Forms使用者介面中。

## 同步調度程式的更改間隔 {#change-interval-of-the-synchronization-scheduler}

執行以下步驟以更改同步調度程式的間隔：

1. 登入AEM Configuration Manager。 配置管理器的URL是 `https://[Server]:[Port]/lc/system/console/configMgr`

1. 找到並開啟 **FormsManagerConfiguration** bundle。

1. 為同步調度器頻率選 **項指定新值** 。

   頻率單位為分鐘。 例如，要將調度程式配置為每60分鐘運行一次，請指定60。

## 同步資產 {#synchronizing-assets}

您可以使用「從資 **料庫同步資產** 」選項手動同步資產。 執行下列步驟以手動同步資產：

1. 登入AEM Forms。 預設URL為 `https://[Server]:[Port]/lc/aem/forms/`。

   ![AEM Forms使用者介面](assets/aem_forms_ui.png)

   **** 圖： *AEM Forms使用者介面*

1. 按一 ![下工具列中的aem6forms_sync](assets/aem6forms_sync.png) 圖示。 如果您在最後設定的路徑上沒有任何資產，則對話方塊如下所示。 按一下 **開始** ，啟動同步。

   ![同步對話框](assets/migrate-and-syncronize.png)

   **** 圖：「同 *步」對話框*

## 同步錯誤疑難排解 {#troubleshooting-synchronization-error}

您可以在工作流程設計工具(LiveCycle Workbench)中建立新的應用程式。

如果新建立的應用程式和/content/dam/formsanddocuments資料夾的名稱相同，錯誤「*An asset with asse this asse this application already exist at root level.*」。

若要解決衝突，請重新命名應用程式，並手動同步資產。

![資產同步對話方塊中的衝突](assets/sync-conflict.png)

**** 圖：「資 *產同步中的衝突」對話框*
