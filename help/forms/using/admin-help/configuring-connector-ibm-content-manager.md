---
title: 為IBM Content manager配置連接器
seo-title: 為IBM Content manager配置連接器
description: 設定Connector for IBM Content Manager，以啟用AEM表單與IBM Content Manager之間的通訊。
seo-description: 設定Connector for IBM Content Manager，以啟用AEM表單與IBM Content Manager之間的通訊。
uuid: 3d55169d-93e3-4d4e-b18b-2a3394e1de3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3094b178-3b1a-46b3-8fbd-c20388afa3a7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 為IBM Content manager配置連接器{#configuring-connector-for-ibm-content-manager}

IBM Content manager的Connector可讓AEM表單與IBM Content Manager進行通訊。 如需其他背景資訊，請參閱服務參考中的「ECM連接器」 [(Connectors for ECM)](https://www.adobe.com/go/learn_aemforms_services_63)。

## 配置IBM Content manager連接 {#configure-the-ibm-content-manager-connection}

1. 在管理控制台中，按一下「服務> Connector for IBM Content Manager」。
1. 在「資料儲存名稱」框中，輸入要連接到的IBM Content manager資料儲存的名稱。 如果資料庫是本地的，請輸入資料庫的名稱。 如果資料庫是遠程的，請輸入其別名。
1. 在「用戶名」框中，輸入將連接到IBM Content manager資料儲存庫的用戶的用戶ID。
1. 在「密碼」方塊中，輸入使用者的密碼。
1. （可選）在「別名連接字串」框中，輸入其他連接參數。 在大多數情況下，此方塊應為空。 如需詳細資訊，請參閱IBM檔案。
1. 按一下「儲存」。

## 服務設定驗證 {#validation-of-service-settings}

如果輸入了不正確的dataStore別名、用戶名或密碼，您將獲得以下結果，具體取決於IBM Content Manager服務的Content Repository Connector當前是否正在運行：

* 如果服務停止，則保存服務配置資訊時，不會顯示錯誤。 但是，下次啟動服務時，將拋出一個例外，服務將不啟動。
* 如果服務已啟動，則在保存服務配置資訊時，服務會嘗試立即驗證憑據資訊。 在這種情況下，會發生錯誤，且不會儲存設定資訊。

