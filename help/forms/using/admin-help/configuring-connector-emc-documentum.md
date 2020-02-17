---
title: 為EMC Documentum配置連接器
seo-title: 為EMC Documentum配置連接器
description: 瞭解如何配置Connector for EMC Documentum ，以便在AEM表單和EMC Documentum之間進行通信。
seo-description: 瞭解如何配置Connector for EMC Documentum ，以便在AEM表單和EMC Documentum之間進行通信。
uuid: fc96900a-ec8a-4efd-ad8e-25e9967e649b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e62370a7-9d9e-43a3-8014-8e53800c870d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 為EMC Documentum配置連接器 {#configuring-connector-for-emc-documentum}

EMC Documentum的Connector支援AEM表單與EMC Documentum之間的通信。 如需其他背景資訊，請參閱服務參考中的「ECM連接器」 [(Connectors for ECM)](https://www.adobe.com/go/learn_aemforms_services_63)。

為EMC Documentum設定Connector涉及配置伺服器連接和儲存庫憑據。

>[!NOTE]
>
>在舊版中，資產可以儲存在ECM儲存庫中。 在目前版本中，資產會儲存在AEM表單原生儲存庫中，且資料庫提供者服務已不受支援。 當您執行AEM表單升級時，會將資產從ECM儲存庫移轉至AEM表單儲存庫。 如需詳細資訊，請參閱您應用程式伺服器的AEM表單升級指南。

## 配置伺服器連接 {#configuring-the-server-connection}

本主題介紹了可在「配置設定」頁上執行的EMC Documentum Connector的任務。

>[!NOTE]
>
>如果您同時設定所有設定，只需按一下「儲存」一次。

### 配置伺服器 {#configure-the-server}

您需要配置連接代理伺服器資訊。 在連接到Documentum內容儲存庫並啟動Connector for EMC Documentum時，需要此資訊。

1. 在管理控制台中，按一下「服務」>「EMC Documentum的連接器」>「配置設定」。
1. 在「Documentum配置資訊」區域中，輸入連接代理的主機名或IP地址和埠號。 埠號必須是正整數（例如1489）。
1. 按一下「儲存」。

### 配置承擔者憑據 {#configure-principal-credentials}

配置承擔者憑據時，您提供的儲存庫名稱取決於登錄過程中是否提供了顯式儲存庫名稱。

如果輸入了錯誤的用戶名或密碼，您將獲得以下結果，具體取決於服務當前是否正在運行：

* 如果EMC Documentum Repository Provider服務和EMC Documentum Content Repository Connector服務都已停止，則在保存服務配置資訊時，不會顯示錯誤。 但是，下次啟動服務時，將拋出一個例外，服務將不啟動。
* 如果啟動了EMC Documentum儲存庫提供方服務或EMC Documentum Content Repository Connector服務，則在保存服務配置資訊時，該服務會嘗試立即驗證憑據資訊。 在這種情況下，會發生錯誤，且不會儲存設定資訊。

1. 在管理控制台中，按一下「服務」>「EMC Documentum的連接器」>「配置設定」。
1. 在「Documentum承擔者憑據資訊」區域中，鍵入具有超級管理員權限的用戶的用戶名和密碼。
1. 如果在登錄過程中未提供明確的儲存庫名稱，請輸入與憑據關聯的儲存庫名稱。
1. 按一下「儲存」。

### 更改儲存庫服務提供程式 {#change-the-repository-service-provider}

您可以配置要與Documentum一起使用的儲存庫服務提供方。 儲存庫服務調用被委派給您配置的提供程式。 可使用下列選項：

**** 當前儲存庫服務提供方名稱：當前儲存庫服務提供方的名稱

**** ECM Documentum儲存庫提供方：使Documentum儲存庫提供程式成為儲存庫的提供程式。 此選項已過時

**** 儲存庫提供方：使本機儲存庫提供程式成為儲存庫的提供程式

***注意&#x200B;**:要選擇所列的儲存庫服務提供方以外的儲存庫服務提供方，請在「應用程式和服務」>「服務管理」中配置RepositoryService。<!-- Fix broken link (See Managing Services) -->*

1. 在管理控制台中，按一下「服務」>「EMC Documentum的連接器」>「配置設定」。
1. 在儲存庫服務提供方資訊區中，選擇替代儲存庫服務提供方。
1. 按一下「儲存」。

## 配置儲存庫憑據 {#configuring-repository-credentials}

Documentum憑證資訊會用於AEM表單系統內容。 儲存庫憑據是Documentum中特定儲存庫的特定憑據。 您可以為任意數量的儲存庫提供憑據；但是，每個儲存庫只能指定一組憑據。

### 添加儲存庫憑據 {#add-a-repository-credential}

1. 在管理控制台中，按一下「服務」>「EMC Documentum的連接器」>「儲存庫憑據設定」。
1. 按一下「新增」。此時將顯示「Documentum系統憑據資訊」頁。
1. 輸入儲存庫的名稱。
1. 輸入用戶名和密碼。
1. 按一下「儲存」。

如果Content Repository Connector for EMC Documentum服務和／或Repository Service for EMC Documentum正在運行，則在將憑據資訊儲存到資料庫中之前，會根據指定的儲存庫對憑據資訊進行驗證。 如果憑據無效或存在，則會顯示錯誤消息。

### 刪除儲存庫憑據 {#remove-a-repository-credential}

1. 在管理控制台中，按一下「服務」>「EMC Documentum的連接器」>「配置設定」。
1. 選擇儲存庫旁邊的複選框以從中刪除憑據，然後按一下刪除。 所選儲存庫的憑據將從資料庫中刪除。

### 更改儲存庫憑據的用戶名和密碼 {#change-the-user-name-and-password-for-a-repository-credential}

1. 在管理控制台中，按一下「服務」>「EMC Documentum的連接器」>「配置設定」。
1. 按一下儲存庫的名稱可編輯憑據。
1. 更改儲存庫的用戶名或密碼，或同時更改兩者。 （儲存庫名稱為只讀。）
1. 按一下「儲存」。

如果Content Repository Connector for EMC Documentum服務和／或Repository Service for EMC Documentum正在運行，則在將憑據資訊儲存到資料庫中之前，會根據指定的儲存庫對憑據資訊進行驗證。 如果憑據無效或存在，則會顯示錯誤消息。

## 啟用Workspace任務隊列共用請求 {#enable-the-request-for-sharing-of-workspace-task-queues}

需要一些手動步驟，以確保Workspace中「請求共用任務隊列」功能與Connector for EMC Documentum一起正常運行。

1. 在部署AEM表單並安裝Workbench後，請登入Workbench並開啟「資源」檢視。 您將從此視圖中確定QueueSharing.swf檔案的位置。
1. 根據您的作業系統，將QueueSharing.swf檔案從「資源檢視」拖曳至Windows案頭或相同位置。
1. 在管理控制台中，按一下「服務」>「EMC Documentum的連接器」>「配置設定」。
1. 在「儲存庫服務提供方資訊」下，將配置的儲存庫提供方更改為EMC Documentum儲存庫提供方。
1. 啟動Workbench，將QueueSharing.swf檔案從最初將其複製到的位置（例如Windows案頭或其他位置）複製到EMC Documentum儲存庫內的現有目錄中。
1. 在「工作台流程」視圖中，開啟「隊列共用」流程。
1. 在「變數」檢視中，開啟&quot;theForm&quot;變數的屬性，並變更URI，以符合您在步驟5中置入QueueSharing.swf檔案的路徑。
1. 儲存程式。
1. 根據您組織的政策，將流程移轉至生產環境。

