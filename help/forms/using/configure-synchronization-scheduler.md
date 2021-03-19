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
role: 管理員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---


# 配置同步調度程式{#configuring-the-synchronization-scheduler}

預設情況下，同步調度程式每3分鐘運行一次，以通過LiveCycle工作台11同步儲存庫中修改和更新的所有資產。 同步過程完成後，包含表單和資源的應用程式將在AEM Forms用戶介面中顯示。

## 更改同步調度程式{#change-interval-of-the-synchronization-scheduler}的間隔

執行以下步驟以更改同步調度程式的間隔：

1. 登入Configuration AEM Manager。 配置管理器的URL為`https://'[server]:[port]'/lc/system/console/configMgr`

1. 找到並開啟&#x200B;**FormsManagerConfiguration**&#x200B;捆綁包。

1. 為&#x200B;**同步調度器頻率**&#x200B;選項指定新值。

   頻率單位為分鐘。 例如，要將調度程式配置為每60分鐘運行一次，請指定60。

## 同步資產{#synchronizing-assets}

您可以使用&#x200B;**「從儲存庫同步資產」選項手動同步資產。**&#x200B;執行下列步驟以手動同步資產：

1. 登入AEM Forms。 預設URL為`https://'[server]:[port]'/lc/aem/forms/`。

   ![AEM Forms用戶介面](assets/aem_forms_ui.png)

   **圖：** *AEM Forms用戶介面*

1. 按一下工具列中的![aem6forms_sync](assets/aem6forms_sync.png)圖示。 如果您在最後設定的路徑上沒有任何資產，則對話方塊如下所示。 按一下&#x200B;**啟動**&#x200B;啟動同步。

   ![同步對話框](assets/migrate-and-syncronize.png)

   **圖：同** *步對話框*

## 同步錯誤疑難排解{#troubleshooting-synchronization-error}

您可以在工作流程設計人員(LiveCycle工作台)中建立新的應用程式。

如果新建立的應用程式和/content/dam/formsanddocuments的資料夾名稱相同，則根層級已存在錯誤&quot;*與此應用程式同名的資產。*」。

若要解決衝突，請重新命名應用程式，並手動同步資產。

![資產同步對話方塊中的衝突](assets/sync-conflict.png)

**圖：資產** *同步對話方塊中的衝突*
