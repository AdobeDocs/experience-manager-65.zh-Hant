---
title: 為IBMFileNet配置連接器
seo-title: Configuring Connector for IBM FileNet
description: 瞭解如何配置IBMFileNet的連接器，以啟用表單與IBMAEM FileNet之間的通信。
seo-description: Learn how to configure the Connector for IBM FileNet to enable communication between AEM forms and IBM FileNet.
uuid: 29d4e221-97f7-4cfb-b7e4-75a8289d2604
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: be4994de-12f8-436e-926a-49a6783b006e
exl-id: f4045df5-a35b-41d7-910e-971017148597
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 0%

---

# 為IBMFileNet配置連接器 {#configuring-connector-for-ibm-filenet}

用於IBMFileNet的連接器AEM支援表單與IBMFileNet之間的通信。 有關其他背景資訊，請參閱中的「ECM連接器」 [服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>在早期版本中，資產可以儲存在ECM儲存庫中。 在此版本中，資產儲存在表AEM單本機儲存庫中，且儲存庫提供程式服務已棄用。 在執行對表單的升級時AEM，將資產從ECM儲存庫遷移到表單AEM儲存庫。 有關詳細資訊，請參AEM閱應用程式伺服器的Forms Upgrade指南。

## 配置到內容引擎的連接 {#configure-the-connection-to-the-content-engine}

IBMFileNet P8內容引擎提供軟體服務，用於管理FileNet內容儲存庫中的企業內容和客戶定義的業務對象。

1. 在管理控制台中，按一下「服務」>「IBMFileNet的連接器」。
1. 在「內容引擎URL」框中，輸入完整的連接URL。 例如：

   如果將FileNet Content Engine 4.x與CEWS傳輸一起使用，請輸入：

   `cemp:https://ContentEngineHostNameorIP:port/wsi/FNCEWS40DIME?jaasConfigurationName=FileNetP8WSI`

   如果將FileNet Content Engine 4.x與EJB傳輸一起使用（僅WebLogic支援），請輸入：

   `cemp:t3://ContentEngineHostNameorIP:port/FileNet/Engine?jaasConfigurationName=FileNetP8Engine`

1. 在憑據保護方案清單中，選擇以下保護級別之一：

   * **清除：** 以未保護模式通過網路發送憑據
   * **對稱：** 通過網路發送加密憑據

1. 在加密檔案位置框中，輸入加密檔案的路徑：

   * 如果選擇「清除」作為憑據保護方案，則將忽略此關鍵字及其值。
   * 如果選擇「對稱」作為憑據保護方案，則輸入的路徑將指向包含要使用的加密密鑰的forms伺服器上加密檔案的位置。

1. 在「預設對象儲存」框中，輸入表單所連接AEM的對象儲存連接器。
1. 在「用戶名」框中，輸入具有對您在上一步中指定的預設對象儲存的訪問權限的用戶的用戶名。
1. 在「密碼」框中，輸入用戶的密碼，然後按一下「保存」。

## 配置進程引擎設定 {#configure-the-process-engine-settings}

IBMFileNet連接器包含用於IBMFileNet服務的進程引擎連接器，該連接器用於與IBMFileNet進程引擎交互。 您可以配置此服務的設定。

1. 在管理控制台中，按一下「服務」>「IBMFileNet的連接器」。
1. 要啟用IBMFileNet服務的進程引擎連接器，請選擇使用進程引擎連接器服務。
1. 在「進程路由器/連接點」框中，輸入主機名或IP地址和埠號，然後輸入進程路由器的名稱。 例如：

   `rmi://ProcessEngineHostNameorIP:port/Name`

1. 在「用戶名」框中，輸入用於連接到流程引擎的用戶名。
1. 在「密碼」框中，輸入用於連接到進程引擎的密碼，然後按一下「保存」。

## 服務設定驗證 {#validation-of-service-settings}

如果在配置到內容引擎或進程引擎設定的連接時輸入了不正確的用戶名或密碼，則根據服務當前是否正在運行，您將得到以下結果：

* 如果IBMFileNet的儲存庫提供程式服務和IBMFileNet服務的內容儲存庫連接器都停止，則在保存服務配置資訊時，不會顯示任何錯誤。 但是，下次啟動服務時，將引發異常，服務將不啟動。
* 如果啟動了IBMFileNet的儲存庫提供程式服務或IBMFileNet服務的內容儲存庫連接器，則在您保存服務配置資訊時，該服務會嘗試立即驗證憑據資訊。 在這種情況下，會發生錯誤，並且不會保存配置資訊。

## 更改儲存庫服務提供程式 {#change-the-repository-service-provider}

可以配置要與FileNet一起使用的儲存庫服務提供程式。 儲存庫服務調用將委派給您配置的提供程式。

以下選項可用：

**當前儲存庫提供程式名稱：** 當前儲存庫服務提供程式的名稱

**IBMFileNet儲存庫提供程式：** 使FileNet儲存庫提供程式成為儲存庫的提供程式。 此選項已被棄用。

**儲存庫提供程式：** 使本機儲存庫提供程式成為儲存庫的提供程式

>[!NOTE]
>
>要選擇除列出的儲存庫服務提供商之外的儲存庫服務提供商，請在Applications and Services中配置RepositoryService。 <!-- Fix broken link(See Managing Services) -->

1. 在管理控制台中，按一下「服務」>「IBMFileNet的連接器」。
1. 在「儲存庫服務提供方資訊」區域，選擇備用儲存庫服務提供方，然後按一下「保存」。
