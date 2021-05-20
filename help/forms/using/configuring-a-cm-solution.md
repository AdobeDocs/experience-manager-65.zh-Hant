---
title: 設定通信管理解決方案
seo-title: 設定通信管理解決方案
description: 設定通信管理解決方案
uuid: 76b25004-fe47-44d7-9bed-7c0fd963306b
topic-tags: correspondence-management
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 186ca75c-638b-4057-826e-cd5d56aa0397
feature: 通信管理
exl-id: f7f5eb0d-a283-45ea-84d3-d6375d2bb95b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 2%

---

# 配置通信管理解決方案{#configuring-a-correspondence-management-solution}

## 定義VersionRestoreManagerImpl {#defining-author-instance-url-for-versionrestoremanagerimpl}的作者實例URL

使用下列步驟來定義製作執行個體版本還原的製作執行個體URL:

1. 前往&#x200B;*https://:&lt;PublishHost>:&lt;PublishPort>/lc/system/console/configMgr*。 使用OSGi Management Console使用者憑證登入。 預設憑證為管理員/管理員。
1. 找到並按一下&#x200B;**[!UICONTROL com.adobe.livecycle.content.activate.impl.VersionRestoreManagerImpl.name]**&#x200B;設定旁的&#x200B;**[!UICONTROL 編輯]**&#x200B;圖示。
1. 在&#x200B;**[!UICONTROL VersionRestoreManager作者URL]**&#x200B;欄位中，指定VersionRestoreManager的作者實例的URL。

   **URL字串**:

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >如果負載平衡器前面有多個製作執行個體（已叢集），請在&#x200B;**[!UICONTROL VersionRestoreManager製作URL]**&#x200B;欄位中指定負載平衡器的URL。

1. 按一下「**[!UICONTROL 儲存]**」。

## 定義ActivationManagerImpl（公共實例激活管理器）的發佈實例URL {#defining-the-publish-instance-url-for-activationmanagerimpl-public-instance-activation-manager}

請依照下列步驟，定義公用執行個體啟動管理器的發佈執行個體URL:

1. 前往&#x200B;*https://:&lt;authorHost>:&lt;authorPort>/lc/system/console/configMgr*。 使用OSGi Management Console使用者憑證登入。 預設憑證為管理員/管理員。
1. 找到並按一下&#x200B;**[!UICONTROL com.adobe.livecycle.content.activate.impl.ActivationManagerImpl.name]**&#x200B;設定旁的&#x200B;**[!UICONTROL 編輯]**&#x200B;圖示。
1. 在&#x200B;**[!UICONTROL ActivationManager Publish URL]**&#x200B;欄位中，指定用於存取Publish實例ActivationManager的URL。 您可以提供下列URL。

   * **負載平衡器URL（建議）**:提供負載平衡器URL，如果在發佈伺服器陣列（多個非叢集發佈執行個體）前面有Web伺服器作為負載平衡器。
   * **發佈執行個體URL**:提供任何發佈執行個體URL，如果您有單一發佈執行個體，或發佈伺服器陣列前端的Web伺服器因任何限制而無法從製作環境存取。如果指定的發佈例項停止運作，作者端會有一個要處理的備援機制。
   * **URL字串**:

      `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.activationManager`

1. 按一下「**[!UICONTROL 儲存]**」。

有關配置通信管理的詳細資訊，請參閱[通信管理配置屬性](https://helpx.adobe.com/aem-forms/6-2/cm-configuration-properties.html)。
