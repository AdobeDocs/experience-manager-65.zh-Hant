---
title: 為Microsoft SharePoint配置連接器
seo-title: 為Microsoft SharePoint配置連接器
description: 配置Microsoft SharePoint的連接器，以啟用AEM表單與Microsoft SharePoint之間的通信。
seo-description: 配置Microsoft SharePoint的連接器，以啟用AEM表單與Microsoft SharePoint之間的通信。
uuid: f1561b41-da20-4220-b13a-e78472a9449f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0ec881c9-8dcc-4847-9edf-24d9e6c4a7ea
exl-id: a8be58f1-1961-4bf5-aaad-feb4489fb389
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 1%

---

# 為Microsoft SharePoint {#configuring-connector-for-microsoft-sharepoint}配置連接器

Microsoft SharePoint的連接器可啟用AEM表單與Microsoft SharePoint之間的通訊。 有關其他背景資訊，請參閱[服務參考](https://www.adobe.com/go/learn_aemforms_services_63)中的「ECM連接器」。

1. 在管理控制台中，按一下「服務」>「Connector for Microsoft SharePoint」。
1. 為SharePoint伺服器指定以下設定：

   **SharePoint伺服器主機名：** SharePoint伺服器上Web應用程式的主機名埠號，格式為 `[hostname]:'port'`。

   **用戶名：** 用於連接到SharePoint伺服器的用戶帳戶。

   **密碼：** 用於連接到SharePoint伺服器的用戶帳戶的密碼

   **域名：**  SharePoint伺服器所在的域。

1. 按一下「儲存」。

## Microsoft SharePoint配置服務{#microsoft-sharepoint-configuration-service}

Microsoft SharePoint配置服務`(MSSharePointConfigService)`允許您指定具有模擬權限的AEM Forms用戶的憑據。 有關模擬權限的資訊，請參閱[為Microsoft SharePoint配置連接器](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html)。 請依照下列步驟指定`MSSharePointConfigService`的設定：

1. 在管理控制台中，按一下「服務」>「應用程式和服務」>「服務管理」。
1. 導航服務清單，然後按一下`MSSharePointConfigService`。
1. 在「設定」頁面上指定下列設定：

   * 具有模擬權限的用戶的用戶名
   * 上述用戶的密碼

1. 按一下「儲存」。
