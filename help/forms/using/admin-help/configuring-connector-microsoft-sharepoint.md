---
title: 配置Microsoft SharePoint的連接器
seo-title: 配置Microsoft SharePoint的連接器
description: 設定Connector for Microsoft SharePoint，以啟用AEM表單與Microsoft SharePoint之間的通訊。
seo-description: 設定Connector for Microsoft SharePoint，以啟用AEM表單與Microsoft SharePoint之間的通訊。
uuid: f1561b41-da20-4220-b13a-e78472a9449f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0ec881c9-8dcc-4847-9edf-24d9e6c4a7ea
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 1%

---


# 配置Microsoft SharePoint {#configuring-connector-for-microsoft-sharepoint}的連接器

Connector for Microsoft SharePoint可讓AEM表單與Microsoft SharePoint通訊。 有關其他背景資訊，請參閱[服務參考](https://www.adobe.com/go/learn_aemforms_services_63)中的「ECM連接器」。

1. 在管理控制台中，按一下「服務> Connector for Microsoft SharePoint」。
1. 為SharePoint伺服器指定下列設定：

   **SharePoint伺服器主機名：** SharePoint伺服器上網頁應用程式的主機名埠號，格式為 `[hostname]:'port'`。

   **使用者名** 稱：用來連線至SharePoint伺服器的使用者帳戶。

   **密碼：** 用於連接到SharePoint伺服器的用戶帳戶的密碼

   **網域名稱：** SharePoint伺服器所在的網域。

1. 按一下「儲存」。

## Microsoft SharePoint配置服務{#microsoft-sharepoint-configuration-service}

Microsoft SharePoint設定服務`(MSSharePointConfigService)`可讓您指定具有模擬權限的AEM表單使用者認證。 有關模擬權限的資訊，請參見[ Configuring Connector for Microsoft SharePoint](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html)。 請依照下列步驟來指定`MSSharePointConfigService`的設定：

1. 在管理控制台中，按一下「服務>應用程式與服務>服務管理」。
1. 導覽服務清單，然後按一下`MSSharePointConfigService`。
1. 在「配置」頁面上指定下列設定：

   * 具有冒用權限的用戶的用戶名
   * 上述使用者的密碼

1. 按一下「儲存」。

