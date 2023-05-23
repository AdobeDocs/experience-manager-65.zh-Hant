---
title: 為EMC Documentum配置連接器
seo-title: Configuring Connector for EMC Documentum
description: 瞭解如何配置Connector for EMC Documentum ，以啟用表單與EMC Documentum之AEM間的通信。
seo-description: Learn how to configure the Connector for EMC Documentum to enable communication between AEM forms and EMC Documentum.
uuid: fc96900a-ec8a-4efd-ad8e-25e9967e649b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e62370a7-9d9e-43a3-8014-8e53800c870d
exl-id: a31a496f-87b9-43c0-a98c-5f6ca5d11690
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 0%

---

# 為EMC Documentum配置連接器 {#configuring-connector-for-emc-documentum}

EMC Documentum的Connector支援表單與EMC DocumentumAEM之間的通信。 有關其他背景資訊，請參閱中的「ECM連接器」 [服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

為EMC Documentum設定Connector涉及配置伺服器連接和儲存庫憑據。

>[!NOTE]
>
>在早期版本中，資產可以儲存在ECM儲存庫中。 在當前版本中，資產儲存在表AEM單本機儲存庫中，且儲存庫提供程式服務已棄用。 在執行對表單的升級時AEM，將資產從ECM儲存庫遷移到表單AEM儲存庫。 有關詳細資訊，請參AEM閱應用程式伺服器的Forms Upgrade指南。

## 配置伺服器連接 {#configuring-the-server-connection}

本主題介紹了在「配置設定」頁上可以執行的EMC Documentum Connector的任務。

>[!NOTE]
>
>如果同時配置所有設定，則只需按一下「保存」一次。

### 配置伺服器 {#configure-the-server}

您需要配置連接代理伺服器資訊。 此資訊是連接到Documentum內容儲存庫和啟動EMC Documentum Connector所必需的。

1. 在管理控制台中，按一下「服務」>「EMC Documentum的連接器」>「配置設定」。
1. 在「Documentum配置資訊」區域中，輸入連接代理的主機名或IP地址和埠號。 埠號必須為正整數（例如1489）。
1. 按一下「儲存」。

### 配置主體憑據 {#configure-principal-credentials}

配置主體憑據時，您提供的儲存庫名稱取決於登錄期間是否提供了顯式儲存庫名稱。

如果輸入的用戶名或密碼不正確，則根據服務當前是否正在運行，您將得到以下結果：

* 如果EMC Documentum Repository Provider服務和EMC Documentum Content Repository Connector服務都停止，則在保存服務配置資訊時，不會顯示任何錯誤。 但是，下次啟動服務時，將引發異常，服務將不啟動。
* 如果啟動了EMC Documentum儲存庫提供程式服務或EMC Documentum內容儲存庫連接器服務，則在您保存服務配置資訊時，該服務會嘗試立即驗證憑據資訊。 在這種情況下，會發生錯誤，並且不會保存配置資訊。

1. 在管理控制台中，按一下「服務」>「EMC Documentum的連接器」>「配置設定」。
1. 在「Documentum主體憑據資訊」區域中，鍵入具有超級管理員權限的用戶的用戶名和密碼。
1. 如果登錄期間未提供顯式儲存庫名稱，請輸入與憑據關聯的儲存庫名稱。
1. 按一下「儲存」。

### 更改儲存庫服務提供程式 {#change-the-repository-service-provider}

您可以配置要與Documentum一起使用的儲存庫服務提供程式。 儲存庫服務調用將委派給您配置的提供程式。 以下選項可用：

**當前儲存庫服務提供程式名稱：** 當前儲存庫服務提供程式的名稱

**ECM Documentum儲存庫提供程式：** 使Documentum儲存庫提供程式成為儲存庫的提供程式。 已棄用此選項

**儲存庫提供程式：** 使本機儲存庫提供程式成為儲存庫的提供程式

>[!NOTE]
>
>要選擇列出的儲存庫服務提供商以外的儲存庫服務提供商，請在「應用程式和服務」>「服務管理」中配置RepositoryService。 <!-- Fix broken link (See Managing Services) -->。

1. 在管理控制台中，按一下「服務」>「EMC Documentum的連接器」>「配置設定」。
1. 在「儲存庫服務提供程式資訊」區域中，選擇備用儲存庫服務提供程式。
1. 按一下「儲存」。

## 配置儲存庫憑據 {#configuring-repository-credentials}

Documentum憑據資訊用於表單AEM系統上下文。 儲存庫憑據特定於Documentum中的特定儲存庫。 您可以為任意數量的儲存庫提供憑據；但是，每個儲存庫只能指定一組憑據。

### 添加儲存庫憑據 {#add-a-repository-credential}

1. 在管理控制台中，按一下「服務」>「EMC Documentum的連接器」>「儲存庫憑據設定」。
1. 按一下「添加」。 此時將顯示「Documentum系統憑據資訊」頁。
1. 輸入儲存庫的名稱。
1. 輸入用戶名和密碼。
1. 按一下「儲存」。

如果Content Repository Connector for EMC Documentum服務和/或Repository Service for EMC Documentum正在運行，則在將憑據資訊儲存到資料庫中之前，會根據指定的儲存庫驗證憑據資訊。 如果憑據無效或存在，則顯示錯誤消息。

### 刪除儲存庫憑據 {#remove-a-repository-credential}

1. 在管理控制台中，按一下「服務」>「EMC Documentum的連接器」>「配置設定」。
1. 選中儲存庫旁邊的複選框以從中刪除憑據，然後按一下刪除。 從資料庫中刪除所選儲存庫的憑據。

### 更改儲存庫憑據的用戶名和密碼 {#change-the-user-name-and-password-for-a-repository-credential}

1. 在管理控制台中，按一下「服務」>「EMC Documentum的連接器」>「配置設定」。
1. 按一下儲存庫的名稱以編輯其憑據。
1. 更改儲存庫的用戶名或密碼，或同時更改兩者。 （儲存庫名稱為只讀。）
1. 按一下「儲存」。

如果Content Repository Connector for EMC Documentum服務和/或Repository Service for EMC Documentum正在運行，則在將憑據資訊儲存到資料庫中之前，會根據指定的儲存庫驗證憑據資訊。 如果憑據無效或存在，則顯示錯誤消息。

## 啟用共用Workspace任務隊列的請求 {#enable-the-request-for-sharing-of-workspace-task-queues}

需要執行一些手動步驟，以確保Workspace中「請求共用任務隊列」功能與Connector for EMC Documentum一起正常工作。

1. 部AEM署表單並安裝Workbench後，登錄到Workbench並開啟「資源」視圖。 您將從此視圖確定QueueSharing.swf檔案的位置。
1. 將QueueSharing.swf檔案從「資源視圖」拖到Windows案頭或等效位置，具體取決於您的作業系統。
1. 在管理控制台中，按一下「服務」>「EMC Documentum的連接器」>「配置設定」。
1. 在「儲存庫服務提供方資訊」下，將已配置的儲存庫提供方更改為EMC Documentum儲存庫提供方。
1. 啟動Workbench，然後將QueueSharing.swf檔案從最初將其複製到的位置（例如，Windows案頭或其他位置）複製到EMC Documentum儲存庫內的現有目錄中。
1. 在「工作台流程」視圖中，開啟「隊列共用」流程。
1. 在「變數」視圖中，開啟&quot;theForm&quot;變數的屬性，並更改URI以與步驟5中放置QueueSharing.swf檔案的路徑匹配。
1. 保存進程。
1. 根據您組織的策略將流程遷移到生產環境。
