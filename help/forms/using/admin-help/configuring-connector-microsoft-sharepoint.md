---
title: 設定Microsoft SharePoint的聯結器
description: 設定Microsoft SharePoint的聯結器，以啟用AEM表單與Microsoft SharePoint之間的通訊。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: a8be58f1-1961-4bf5-aaad-feb4489fb389
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 1%

---

# 設定Microsoft SharePoint的聯結器 {#configuring-connector-for-microsoft-sharepoint}

Microsoft SharePoint的聯結器可啟用AEM表單與Microsoft SharePoint之間的通訊。 如需其他背景資訊，請參閱下列「Connectors for ECM」： [服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

1. 在管理控制檯中，按一下「服務」 > 「Microsoft SharePoint的聯結器」 。
1. 為您的SharePoint伺服器指定下列設定：

   **SharePoint伺服器主機名稱：** SharePoint伺服器上Web應用程式的主機名稱連線埠號碼，格式為 `[hostname]:'port'`.

   **使用者名稱：** 用來連線至SharePoint伺服器的使用者帳戶。

   **密碼：** 用來連線至SharePoint伺服器的使用者帳戶密碼

   **網域名稱：** SharePoint伺服器所在的網域。

1. 按一下「儲存」。

## Microsoft SharePoint設定服務 {#microsoft-sharepoint-configuration-service}

Microsoft SharePoint設定服務 `(MSSharePointConfigService)` 可讓您為具有模擬許可權的AEM表單使用者指定認證。 如需模擬許可權的相關資訊，請參閱 [設定Microsoft SharePoint的聯結器](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html). 請依照下列步驟指定 `MSSharePointConfigService`：

1. 在Administration Console中，按一下「服務>應用程式和服務>服務管理」。
1. 瀏覽服務清單並按一下 `MSSharePointConfigService`.
1. 在「組態」頁面中指定下列設定：

   * 具有模擬許可權的使用者的使用者名稱
   * 上述使用者的密碼

1. 按一下「儲存」。
