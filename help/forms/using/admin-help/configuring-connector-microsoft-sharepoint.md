---
title: 配置MicrosoftSharePoint的連接器
seo-title: Configuring Connector for Microsoft SharePoint
description: 為MicrosoftSharePoint配置連接器，以啟用表單AEM與MicrosoftSharePoint之間的通信。
seo-description: Configure Connector for Microsoft SharePoint to enable communication between AEM forms and Microsoft SharePoint.
uuid: f1561b41-da20-4220-b13a-e78472a9449f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0ec881c9-8dcc-4847-9edf-24d9e6c4a7ea
exl-id: a8be58f1-1961-4bf5-aaad-feb4489fb389
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 1%

---

# 配置MicrosoftSharePoint的連接器 {#configuring-connector-for-microsoft-sharepoint}

MicrosoftSharePoint的連接器使表AEM格與MicrosoftSharePoint通信。 有關其他背景資訊，請參閱中的「ECM連接器」 [服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

1. 在管理控制台中，按一下「服務」>「MicrosoftSharePoint的連接器」。
1. 為您的SharePoint伺服器指定以下設定：

   **SharePoint伺服器主機名：** SharePoint伺服器上Web應用程式的主機名埠號，格式為 `[hostname]:'port'`。

   **用戶名：** 用於連接到SharePoint伺服器的用戶帳戶。

   **密碼：** 用於連接到SharePoint伺服器的用戶帳戶的密碼

   **域名：** SharePoint伺服器所在的域。

1. 按一下「儲存」。

## MicrosoftSharePoint配置服務 {#microsoft-sharepoint-configuration-service}

MicrosoftSharePoint配置服務 `(MSSharePointConfigService)` 用於為具有模擬權限AEM的表單用戶指定憑據。 有關模擬權限的資訊，請參見 [配置MicrosoftSharePoint的連接器](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html)。 按照以下步驟指定 `MSSharePointConfigService`:

1. 在管理控制台中，按一下「服務」>「應用程式和服務」>「服務管理」。
1. 導航服務清單，然後按一下 `MSSharePointConfigService`。
1. 在「配置」頁上指定以下設定：

   * 具有模擬權限的用戶的用戶名
   * 上述用戶的密碼

1. 按一下「儲存」。
