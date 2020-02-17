---
title: 配置通信管理解決方案
seo-title: 配置通信管理解決方案
description: 'null'
seo-description: 'null'
uuid: 76b25004-fe47-44d7-9bed-7c0fd963306b
topic-tags: correspondence-management
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 186ca75c-638b-4057-826e-cd5d56aa0397
translation-type: tm+mt
source-git-commit: 5120bbdefea528ad6d07a9c99df565555b6a8444

---


# 配置通信管理解決方案 {#configuring-a-correspondence-management-solution}

## 定義VersionRestoreManagerImpl的作者實例URL {#defining-author-instance-url-for-versionrestoremanagerimpl}

使用下列步驟為作者實例版本還原定義作者實例URL:

1. 前往 *https://:&lt;PublishHost>:&lt;PublishPort>/lc/system/console/configMgr*。 使用OSGi Management Console使用者憑證登入。 預設認證為admin/admin。
1. 尋找並按一 **[!UICONTROL 下]** com.adobe.livecycle.content.activate.impl.VersionRestoreManagerImpl.name設定旁的「編輯」圖示 **** 。
1. 在「 **[!UICONTROL VersionRestoreManager作者URL]** 」欄位中，指定VersionRestoreManager的作者實例的URL。

   **URL字串**:

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >如果負載平衡器前面有多個作者實例（叢集），請在 **[!UICONTROL VersionRestoreManager作者URL欄位中指定負載平衡器的URL]** 。

1. 按一下&#x200B;**[!UICONTROL 「儲存」]**。

## 定義ActivationManager的發佈例項URL實施（公開例項啟動管理員） {#defining-the-publish-instance-url-for-activationmanagerimpl-public-instance-activation-manager}

請依照下列步驟，定義公開執行個體啟動管理員的發佈執行個體URL:

1. 請至 *https://:&lt;authorHost>:&lt;authorPort>/lc/system/console/configMgr*。 使用OSGi Management Console使用者憑證登入。 預設認證為admin/admin。
1. 尋找並按一 **[!UICONTROL 下]** com.adobe.livecycle.content.activate.impl.ActivationManagerImpl.name設定旁的「編輯」圖示 **** 。
1. 在「 **[!UICONTROL ActivationManager發佈URL」欄位中]** ，指定存取「發佈例項ActivationManager」的URL。 您可以提供下列URL。

   * **負載平衡器URL（建議）**:提供負載平衡器URL，如果您在發佈群（多個非叢集發佈例項）前面有網站伺服器充當負載平衡器。
   * **發佈例項URL**:提供任何發佈例項URL。如果您有單一發佈例項或位於發佈群組前方的網頁伺服器，由於任何限制，作者環境無法存取。 如果指定的發佈例項關閉，則作者端有要處理的備援機制。
   * **URL字串**:

      `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.activationManager`

1. 按一下&#x200B;**[!UICONTROL 「儲存」]**。

有關配置通信管理的詳細資訊，請參閱 [通信管理配置屬性](https://helpx.adobe.com/aem-forms/6-2/cm-configuration-properties.html)。
