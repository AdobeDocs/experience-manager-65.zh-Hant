---
title: 為IBM FileNet配置連接器
seo-title: 為IBM FileNet配置連接器
description: 了解如何配置Connector for IBM FileNet以啟用AEM表單與IBM FileNet之間的通信。
seo-description: 了解如何配置Connector for IBM FileNet以啟用AEM表單與IBM FileNet之間的通信。
uuid: 29d4e221-97f7-4cfb-b7e4-75a8289d2604
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: be4994de-12f8-436e-926a-49a6783b006e
exl-id: f4045df5-a35b-41d7-910e-971017148597
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 0%

---

# 為IBM FileNet {#configuring-connector-for-ibm-filenet}配置連接器

IBM FileNet的連接器支援AEM表單與IBM FileNet之間的通信。 有關其他背景資訊，請參閱[服務參考](https://www.adobe.com/go/learn_aemforms_services_63)中的「ECM連接器」。

>[!NOTE]
>
>在舊版中，資產可儲存在ECM存放庫中。 在此版本中，資產儲存在AEM表單原生存放庫中，且存放庫提供者服務已遭取代。 執行AEM Forms升級時，會將資產從ECM存放庫移轉至AEM Forms存放庫。 如需詳細資訊，請參閱應用程式伺服器的AEM Forms升級指南。

## 配置與內容引擎的連接{#configure-the-connection-to-the-content-engine}

IBM FileNet P8 Content Engine提供了軟體服務，用於管理FileNet內容儲存庫中企業內容和客戶定義的業務對象。

1. 在管理控制台中，按一下「服務」>「IBM FileNet的連接器」。
1. 在「內容引擎URL」方塊中，輸入完整的連線URL。 例如：

   如果您正在將FileNet Content Engine 4.x與CEWS傳輸一起使用，請輸入：

   `cemp:https://ContentEngineHostNameorIP:port/wsi/FNCEWS40DIME?jaasConfigurationName=FileNetP8WSI`

   如果使用FileNet Content Engine 4.x和EJB傳輸（僅WebLogic支援），請輸入：

   `cemp:t3://ContentEngineHostNameorIP:port/FileNet/Engine?jaasConfigurationName=FileNetP8Engine`

1. 在憑據保護方案清單中，選擇以下保護級別之一：

   * **清除：** 以未受保護的模式在網路中發送憑據
   * **對稱：** 在網路中發送加密憑據

1. 在加密檔案位置框中，輸入加密檔案的路徑：

   * 如果選擇清除作為憑據保護方案，則會忽略此關鍵字及其值。
   * 如果選擇「對稱」作為憑據保護方案，則輸入的路徑指向表單伺服器上包含要使用的加密密鑰的加密檔案的位置。

1. 在「預設對象儲存」框中，輸入AEM表單預設連接到的對象儲存連接器。
1. 在「用戶名」框中，輸入對您在上一步驟中指定的預設對象儲存區具有訪問權限的用戶的用戶名。
1. 在「密碼」框中，輸入用戶的密碼，然後按一下「保存」。

## 配置進程引擎設定{#configure-the-process-engine-settings}

IBM FileNet的連接器包含用於與IBM FileNet Process Engine交互的Process Engine Connector for IBM FileNet服務。 您可以配置此服務的設定。

1. 在管理控制台中，按一下「服務」>「IBM FileNet的連接器」。
1. 要啟用Process Engine Connector for IBM FileNet服務，請選擇Use Process Engine Connector Service。
1. 在Process Router/Connection Point框中，輸入主機名或IP地址和埠號，後跟進程路由器的名稱。 例如：

   `rmi://ProcessEngineHostNameorIP:port/Name`

1. 在「用戶名」框中，輸入用於連接到流程引擎的用戶名。
1. 在「密碼」框中，輸入用於連接到進程引擎的密碼，然後按一下「保存」。

## 驗證服務設定{#validation-of-service-settings}

如果您在配置到內容引擎或進程引擎設定的連接時輸入了不正確的用戶名或密碼，則將根據服務當前是否正在運行而得到以下結果：

* 如果IBM FileNet的儲存庫提供程式服務和IBM FileNet的Content Repository Connector服務都停止，則保存服務配置資訊時，不會顯示錯誤。 但是，下次啟動服務時，將引發異常，且服務將不啟動。
* 如果啟動了IBM FileNet的儲存庫提供程式服務或IBM FileNet的Content Repository Connector服務，則在保存服務配置資訊時，服務將嘗試立即驗證憑據資訊。 在此情況下，會發生錯誤且不會儲存設定資訊。

## 更改儲存庫服務提供程式{#change-the-repository-service-provider}

可以配置要與FileNet一起使用的儲存庫服務提供程式。 存放庫服務呼叫會委派給您設定的提供者。

可使用下列選項：

**當前儲存庫提供程式名稱：** 當前儲存庫服務提供程式的名稱

**IBM FileNet儲存庫提供程式：** 使FileNet儲存庫提供程式成為儲存庫的提供程式。已棄用此選項。

**存放庫提供者：** 將原生存放庫提供者設為存放庫的提供者

>[!NOTE]
>
>要選擇所列的儲存庫服務提供程式以外的儲存庫服務提供程式，請在「應用程式和服務」中配置RepositoryService。<!-- Fix broken link(See Managing Services) -->

1. 在管理控制台中，按一下「服務」>「IBM FileNet的連接器」。
1. 在「儲存庫服務提供程式資訊」區域中，選擇替代的儲存庫服務提供程式，然後按一下「保存」。
