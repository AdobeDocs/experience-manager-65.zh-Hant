---
title: 設定同步排程器
description: 瞭解如何移轉及同步資產、設定同步排程器，以及使用資料夾來排列資產。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin,User
exl-id: 34db1f76-ee40-4612-85da-22041e7560fb
solution: Experience Manager, Experience Manager Forms
feature: Workbench,Adaptive Forms
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 36ac8e9c-5c7a-56d8-af5e-39399fd7b101
    internal-label: Workbench
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%
---
# 設定同步排程器 {#configuring-the-synchronization-scheduler}

根據預設，同步排程器每3分鐘會執行一次，以同步處理在存放庫中透過LiveCycle Workbench 11修改及更新的所有資產。 同步程式完成後，AEM Forms使用者介面中會顯示包含表單和資源的應用程式。

## 變更同步化排程器的間隔 {#change-interval-of-the-synchronization-scheduler}

執行以下步驟來變更同步化排程器的間隔：

1. 登入AEM組態管理員。 組態管理員的URL是`https://'[server]:[port]'/lc/system/console/configMgr`

1. 找到並開啟&#x200B;**FormsManagerConfiguration**&#x200B;套件。

1. 指定&#x200B;**同步化排程器頻率**&#x200B;選項的新值。

   頻率的單位是分鐘。 例如，若要設定排程器每60分鐘執行，請指定60。

## 同步資產 {#synchronizing-assets}

您可以使用&#x200B;**從存放庫同步Assets**&#x200B;選項，以手動同步資產。 執行以下步驟以手動同步資產：

1. 登入AEM Forms。 預設URL為`https://'[server]:[port]'/lc/aem/forms/`。

   ![AEM Forms使用者介面](assets/aem_forms_ui.png)

   **圖：** *AEM Forms使用者介面*

1. 按一下工具列中的![aem6forms_sync](assets/aem6forms_sync.png)圖示。 如果在最後設定的路徑沒有任何資產，則會顯示如下所示的對話方塊。 按一下&#x200B;**開始**&#x200B;以啟動同步處理。

   ![同步處理對話方塊](assets/migrate-and-syncronize.png)

   **圖：** *同步化對話方塊*

## 疑難排解同步處理錯誤 {#troubleshooting-synchronization-error}

您可以在工作流程設計工具(LiveCycle Workbench)中建立新的應用程式。

如果新建立的應用程式和位於/content/dam/formsanddocuments的資料夾具有相同的名稱，則會發生錯誤「*根層級已存在與此應用程式同名的資產。*」 已記錄。

若要解決衝突，請重新命名應用程式，然後手動同步資產。

![資產同步處理對話方塊中的衝突](assets/sync-conflict.png)

**圖：** *資產同步化對話方塊中的衝突*
