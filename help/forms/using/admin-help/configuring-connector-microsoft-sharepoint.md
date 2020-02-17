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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 配置Microsoft SharePoint的連接器 {#configuring-connector-for-microsoft-sharepoint}

Connector for Microsoft SharePoint可讓AEM表單與Microsoft SharePoint通訊。 如需其他背景資訊，請參閱服務參考中的「ECM連接器」 [(Connectors for ECM)](https://www.adobe.com/go/learn_aemforms_services_63)。

1. 在管理控制台中，按一下「服務> Connector for Microsoft SharePoint」。
1. 為SharePoint伺服器指定下列設定：

   **** SharePoint伺服器主機名稱：SharePoint伺服器上Web應用程式的主機名稱埠號，格式為 `[hostname]:[port]`。

   **** 用戶名：用於連接到SharePoint伺服器的用戶帳戶。

   **** 密碼：用於連接到SharePoint伺服器的用戶帳戶的密碼

   **** 域名：SharePoint伺服器所在的網域。

1. 按一下「儲存」。

## Microsoft SharePoint設定服務 {#microsoft-sharepoint-configuration-service}

Microsoft SharePoint設定服務可 `(MSSharePointConfigService)` 讓您指定具有模擬權限的AEM表單使用者認證。 有關模擬權限的資訊，請參 [閱配置Microsoft sharePoint的連接器](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html)。 請依照下列步驟來指定下列設定 `MSSharePointConfigService`:

1. 在管理控制台中，按一下「服務>應用程式與服務>服務管理」。
1. 導覽服務清單，然後按一下 `MSSharePointConfigService`。
1. 在「配置」頁面上指定下列設定：

   * 具有冒用權限的用戶的用戶名
   * 上述使用者的密碼

1. 按一下「儲存」。

