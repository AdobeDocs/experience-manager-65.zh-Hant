---
title: 配置通信管理解決方案
seo-title: Configuring a Correspondence Management solution
description: 配置通信管理解決方案
uuid: 76b25004-fe47-44d7-9bed-7c0fd963306b
topic-tags: correspondence-management
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 186ca75c-638b-4057-826e-cd5d56aa0397
feature: Correspondence Management
exl-id: f7f5eb0d-a283-45ea-84d3-d6375d2bb95b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 1%

---

# 配置通信管理解決方案 {#configuring-a-correspondence-management-solution}

## 定義VersionRestoreManagerImpl的作者實例URL {#defining-author-instance-url-for-versionrestoremanagerimpl}

使用以下步驟為作者實例版本還原定義作者實例URL:

1. 轉到 *https://:&lt;publishhost>:&lt;publishport>/lc/system/console/configMgr*。 使用OSGi Management Console用戶憑據登錄。 預設憑據是admin/admin。
1. 查找並按一下 **[!UICONTROL 編輯]** 表徵圖 **[!UICONTROL com.adobe.livecycle.content.activate.impl.VersionRestoreManagerImpl.name]** 的子菜單。
1. 在 **[!UICONTROL VersionRestoreManager作者URL]** 欄位中，指定VersionRestoreManager的Author實例的URL。

   **URL字串**:

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >如果負載平衡器前面有多個作者實例（群集），請在 **[!UICONTROL VersionRestoreManager作者URL]** 的子菜單。

1. 按一下「**[!UICONTROL 儲存]**」。

## 定義ActivationManagerImpl（公共實例激活管理器）的發佈實例URL {#defining-the-publish-instance-url-for-activationmanagerimpl-public-instance-activation-manager}

按照以下步驟定義公共實例激活管理器的發佈實例URL:

1. 轉到 *https://:&lt;authorhost>:&lt;authorport>/lc/system/console/configMgr*。 使用OSGi Management Console用戶憑據登錄。 預設憑據是admin/admin。
1. 查找並按一下 **[!UICONTROL 編輯]** 表徵圖 **[!UICONTROL com.adobe.livecycle.content.activate.impl.ActivationManagerImpl.name]** 的子菜單。
1. 在 **[!UICONTROL ActivationManager發佈URL]** 欄位中，指定用於訪問發佈實例ActivationManager的URL。 可以提供以下URL。

   * **負載平衡器URL（推薦）**:提供負載平衡器URL，如果在發佈場（多個非群集發佈實例）前有一個Web伺服器充當負載平衡器。
   * **發佈實例URL**:提供任何發佈實例URL。如果您有單個發佈實例，或者由於任何限制，無法從作者環境訪問位於發佈場前面的Web伺服器。 如果指定的發佈實例關閉，則在作者端有一個要處理的回退機制。
   * **URL字串**:

      `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.activationManager`

1. 按一下「**[!UICONTROL 儲存]**」。

有關配置Tergement Management的詳細資訊，請參見 [通信管理配置屬性](https://helpx.adobe.com/aem-forms/6-2/cm-configuration-properties.html)。
