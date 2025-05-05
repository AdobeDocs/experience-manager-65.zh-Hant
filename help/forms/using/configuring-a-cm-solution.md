---
title: 設定通訊管理解決方案
description: 瞭解如何在AEM Forms環境中設定通訊管理解決方案。
topic-tags: correspondence-management
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
feature: Correspondence Management
exl-id: f7f5eb0d-a283-45ea-84d3-d6375d2bb95b
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 1%

---

# 設定通訊管理解決方案 {#configuring-a-correspondence-management-solution}

## 定義VersionRestoreManagerImpl的作者執行個體URL {#defining-author-instance-url-for-versionrestoremanagerimpl}

使用以下步驟，為編寫執行個體版本還原定義編寫執行個體URL：

1. 移至&#x200B;*https://：&lt;PublishHost>：&lt;PublishPort>/lc/system/console/configMgr*。 使用OSGi Management Console使用者認證登入。 預設認證為admin/admin。
1. 尋找並按一下&#x200B;**[!UICONTROL com.adobe.livecycle.content.activate.impl.VersionRestoreManagerImpl.name]**&#x200B;設定旁的&#x200B;**[!UICONTROL 編輯]**&#x200B;圖示。
1. 在&#x200B;**[!UICONTROL VersionRestoreManager作者URL]**&#x200B;欄位中，指定VersionRestoreManager的作者執行個體的URL。

   **URL字串**：

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >如果負載平衡器前有多個作者執行個體（叢集），請在&#x200B;**[!UICONTROL VersionRestoreManager作者URL]**&#x200B;欄位中指定負載平衡器的URL。

1. 按一下「**[!UICONTROL 儲存]**」。

## 定義ActivationManagerImpl （公用執行個體啟動管理員）的Publish執行個體URL {#defining-the-publish-instance-url-for-activationmanagerimpl-public-instance-activation-manager}

請依照下列步驟，為公用執行個體啟用管理員定義Publish執行個體URL：

1. 移至&#x200B;*https://：&lt;authorHost>：&lt;authorPort>/lc/system/console/configMgr*。 使用OSGi Management Console使用者認證登入。 預設認證為admin/admin。
1. 尋找並按一下&#x200B;**[!UICONTROL com.adobe.livecycle.content.activate.impl.ActivationManagerImpl.name]**&#x200B;設定旁的&#x200B;**[!UICONTROL 編輯]**&#x200B;圖示。
1. 在&#x200B;**[!UICONTROL ActivationManager Publish URL]**&#x200B;欄位中，指定用於存取Publish執行個體ActivationManager的URL。 您可以提供下列URL。

   * **負載平衡器URL （建議）**：提供負載平衡器URL，如果您在發佈伺服器陣列前有一個做為負載平衡器的網頁伺服器（多個非叢集發佈執行個體）。
   * **Publish執行個體URL**：提供任何發佈執行個體URL。如果您有單一發佈執行個體，或因任何限制而無法從製作環境存取發佈伺服器陣列前的Web伺服器。 如果指定的發佈執行個體停止運作，作者端會有一個要處理的遞補機制。
   * **URL字串**：

     `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.activationManager`

1. 按一下「**[!UICONTROL 儲存]**」。

如需有關設定通訊管理的詳細資訊，請參閱[通訊管理組態屬性](https://helpx.adobe.com/tw/aem-forms/6-2/cm-configuration-properties.html)。
