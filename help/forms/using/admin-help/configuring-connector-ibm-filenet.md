---
title: 配置IBM FileNet的連接器
seo-title: 配置IBM FileNet的連接器
description: 瞭解如何設定Connector for IBM FileNet，以啟用AEM表單與IBM FileNet之間的通訊。
seo-description: 瞭解如何設定Connector for IBM FileNet，以啟用AEM表單與IBM FileNet之間的通訊。
uuid: 29d4e221-97f7-4cfb-b7e4-75a8289d2604
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: be4994de-12f8-436e-926a-49a6783b006e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 配置IBM FileNet的連接器 {#configuring-connector-for-ibm-filenet}

IBM FileNet的Connector可讓AEM表單與IBM FileNet通訊。 如需其他背景資訊，請參閱服務參考中的「ECM連接器」 [(Connectors for ECM)](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>在舊版中，資產可以儲存在ECM儲存庫中。 在此版本中，資產會儲存在AEM表單原生儲存庫中，且資料庫提供者服務已過時。 當您執行AEM表單升級時，會將資產從ECM儲存庫移轉至AEM表單儲存庫。 如需詳細資訊，請參閱您應用程式伺服器的AEM表單升級指南。

## 設定與內容引擎的連線 {#configure-the-connection-to-the-content-engine}

IBM FileNet P8 Content Engine提供軟體服務，用於管理FileNet內容儲存庫中的企業內容和客戶定義的業務對象。

1. 在管理控制台中，按一下「服務」>「IBM FileNet的連接器」。
1. 在「內容引擎URL」方塊中，輸入完整的連線URL。 例如：

   如果您正在將FileNet Content Engine 4.x與CEWS傳輸搭配使用，請輸入：

   `cemp:https://ContentEngineHostNameorIP:port/wsi/FNCEWS40DIME?jaasConfigurationName=FileNetP8WSI`

   如果您正在將FileNet Content Engine 4.x與EJB傳輸一起使用（僅WebLogic支援），請輸入：

   `cemp:t3://ContentEngineHostNameorIP:port/FileNet/Engine?jaasConfigurationName=FileNetP8Engine`

1. 在「憑據保護方案」清單中，選擇以下保護級別之一：

   * **** 清除：以未受保護模式在網路中發送憑據
   * **** 對稱：通過網路發送加密憑據

1. 在「加密檔案位置」框中，輸入加密檔案的路徑：

   * 如果選擇「清除」作為憑據保護方案，則會忽略此關鍵字及其值。
   * 如果選擇「對稱」作為憑據保護方案，則輸入的路徑指向要使用的加密密鑰的表單伺服器上加密檔案的位置。

1. 在「預設物件存放區」方塊中，輸入AEM表單依預設連接的物件存放區連接器。
1. 在「用戶名」框中，輸入對您在上一步中指定的預設對象儲存庫具有訪問權限的用戶的用戶名。
1. 在「密碼」框中，輸入用戶的密碼，然後按一下「保存」。

## 配置流程引擎設定 {#configure-the-process-engine-settings}

IBM FileNet的連接器包含用於與IBM FileNet Process engine交互的IBM FileNet Connector服務。 您可以設定此服務的設定。

1. 在管理控制台中，按一下「服務」>「IBM FileNet的連接器」。
1. 要啟用IBM FileNet服務的Process Engine Connector，請選擇Use Process Engine Connector Service。
1. 在「進程路由器／連接點」框中，輸入主機名或IP地址和埠號，後跟進程路由器的名稱。 例如：

   `rmi://ProcessEngineHostNameorIP:port/Name`

1. 在「用戶名」框中，輸入用於連接到流程引擎的用戶名。
1. 在「密碼」框中，輸入用於連接到流程引擎的密碼，然後按一下「保存」。

## 服務設定驗證 {#validation-of-service-settings}

如果您在設定與內容引擎或程式引擎設定的連線時輸入錯誤的使用者名稱或密碼，則會根據服務目前是否在執行，取得下列結果：

* 如果IBM FileNet的Repository Provider服務和IBM FileNet的Content Repository Connector服務都已停止，則在保存服務配置資訊時，不會顯示錯誤。 但是，下次啟動服務時，將拋出一個例外，服務將不啟動。
* 如果啟動了IBM FileNet的Repository Provider服務或IBM FileNet的Content Repository Connector服務，則在保存服務配置資訊時，服務將嘗試立即驗證憑據資訊。 在這種情況下，會發生錯誤，且不會儲存設定資訊。

## 更改儲存庫服務提供程式 {#change-the-repository-service-provider}

可以配置要與FileNet一起使用的儲存庫服務提供方。 儲存庫服務調用被委派給您配置的提供程式。

可使用下列選項：

**** 當前儲存庫提供程式名稱：當前儲存庫服務提供方的名稱

**** IBM FileNet Repository Provider:使FileNet儲存庫提供程式成為儲存庫的提供程式。 此選項已過時。

**** 儲存庫提供方：使本機儲存庫提供程式成為儲存庫的提供程式

***注意&#x200B;**:要選擇所列的儲存庫服務提供方以外的儲存庫服務提供方，請在「應用程式和服務」中配置RepositoryService。<!-- Fix broken link(See Managing Services) -->*

1. 在管理控制台中，按一下「服務」>「IBM FileNet的連接器」。
1. 在儲存庫服務提供方資訊區中，選擇替代儲存庫服務提供方，然後按一下保存。

