---
title: 為EMC Documentum配置連接器
seo-title: Configuring Connector for EMC Documentum
description: 了解如何配置Connector for EMC Documentum以實現AEM表單與EMC Documentum之間的通信。
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
ht-degree: 1%

---

# 為EMC Documentum配置連接器 {#configuring-connector-for-emc-documentum}

EMC Documentum的Connector支援AEM表單與EMC Documentum之間的通信。 如需其他背景資訊，請參閱 [服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

為EMC Documentum設定Connector涉及配置伺服器連接和儲存庫憑據。

>[!NOTE]
>
>在舊版中，資產可儲存在ECM存放庫中。 在目前版本中，資產會儲存在AEM表單原生存放庫中，且存放庫提供者服務已遭取代。 執行AEM Forms升級時，會將資產從ECM存放庫移轉至AEM Forms存放庫。 如需詳細資訊，請參閱應用程式伺服器的AEM Forms升級指南。

## 配置伺服器連接 {#configuring-the-server-connection}

本主題介紹了可在「配置設定」頁上執行的EMC Documentum Connector的任務。

>[!NOTE]
>
>如果您同時配置所有設定，則只需按一下「儲存」一次。

### 配置伺服器 {#configure-the-server}

您需要配置連接代理伺服器資訊。 此資訊對於連接到Documentum內容儲存庫和啟動EMC Documentum的Connector是必需的。

1. 在管理控制台中，按一下「服務」>「EMC Documentum的連接器」>「配置設定」。
1. 在「Documentum配置資訊」區域中，輸入連接代理的主機名或IP地址和埠號。 埠號必須是正整數（例如1489）。
1. 按一下「儲存」。

### 配置主體憑據 {#configure-principal-credentials}

配置主憑據時，您提供的儲存庫名稱取決於登錄期間是否提供了顯式儲存庫名稱。

如果輸入的用戶名或密碼不正確，則根據服務當前是否正在運行，您將獲得以下結果：

* 如果EMC Documentum儲存庫提供程式服務和EMC Documentum Content Repository Connector服務都停止，則保存服務配置資訊時，不會顯示錯誤。 但是，下次啟動服務時，將引發異常，且服務將不啟動。
* 如果EMC Documentum儲存庫提供程式服務或EMC Documentum Content Repository Connector服務已啟動，則當您保存服務配置資訊時，該服務將嘗試立即驗證憑據資訊。 在此情況下，會發生錯誤且不會儲存設定資訊。

1. 在管理控制台中，按一下「服務」>「EMC Documentum的連接器」>「配置設定」。
1. 在「Documentum主體憑據資訊」區域中，鍵入具有超級管理員權限的用戶的用戶名和密碼。
1. 如果在登錄期間未提供明確的儲存庫名稱，請輸入與憑據關聯的儲存庫名稱。
1. 按一下「儲存」。

### 更改儲存庫服務提供程式 {#change-the-repository-service-provider}

您可以配置要與Documentum一起使用的儲存庫服務提供商。 存放庫服務呼叫會委派給您設定的提供者。 可使用下列選項：

**當前儲存庫服務提供程式名稱：** 當前儲存庫服務提供商的名稱

**ECM Documentum儲存庫提供程式：** 使Documentum儲存庫提供程式成為儲存庫的提供程式。 已棄用此選項

**儲存庫提供者：** 使本機儲存庫提供者成為儲存庫的提供者

>[!NOTE]
>
>要選擇所列儲存庫服務提供程式以外的儲存庫服務提供程式，請在「應用程式和服務」>「服務管理」中配置RepositoryService。 <!-- Fix broken link (See Managing Services) -->.

1. 在管理控制台中，按一下「服務」>「EMC Documentum的連接器」>「配置設定」。
1. 在「儲存庫服務提供程式資訊」區域中，選擇替代的儲存庫服務提供程式。
1. 按一下「儲存」。

## 配置儲存庫憑據 {#configuring-repository-credentials}

AEM表單系統上下文中使用Documentum憑據資訊。 儲存庫憑據是Documentum中特定儲存庫的特定憑據。 您可以為任意數量的儲存庫提供憑據；但是，每個儲存庫只能指定一組憑據。

### 添加儲存庫憑據 {#add-a-repository-credential}

1. 在管理控制台中，按一下「服務」>「EMC Documentum的連接器」>「儲存庫憑據設定」。
1. 按一下「新增」。此時將顯示「Documentum系統憑據資訊」頁。
1. 輸入儲存庫的名稱。
1. 輸入用戶名和密碼。
1. 按一下「儲存」。

如果Content Repository Connector for EMC Documentum服務和/或Repository Service for EMC Documentum正在運行，則在將憑據資訊儲存到資料庫之前，將根據指定的儲存庫驗證憑據資訊。 如果憑證無效或存在，則會顯示錯誤訊息。

### 刪除儲存庫憑據 {#remove-a-repository-credential}

1. 在管理控制台中，按一下「服務」>「EMC Documentum的連接器」>「配置設定」。
1. 選中儲存庫旁的複選框以從中刪除憑據，然後按一下刪除。 所選儲存庫的憑據將從資料庫中刪除。

### 更改儲存庫憑據的用戶名和密碼 {#change-the-user-name-and-password-for-a-repository-credential}

1. 在管理控制台中，按一下「服務」>「EMC Documentum的連接器」>「配置設定」。
1. 按一下儲存庫的名稱以編輯的憑據。
1. 更改儲存庫的用戶名或密碼，或更改兩者。 （存放庫名稱為唯讀。）
1. 按一下「儲存」。

如果Content Repository Connector for EMC Documentum服務和/或Repository Service for EMC Documentum正在運行，則在將憑據資訊儲存到資料庫之前，將根據指定的儲存庫驗證憑據資訊。 如果憑證無效或存在，則會顯示錯誤訊息。

## 啟用共用Workspace任務隊列的請求 {#enable-the-request-for-sharing-of-workspace-task-queues}

需要一些手動步驟，以確保Workspace中的「請求共用任務隊列」功能與EMC Documentum的Connector一起正常工作。

1. 部署AEM表單並安裝Workbench後，登入Workbench並開啟「資源」檢視。 通過此視圖，可確定QueueSharing.swf檔案的位置。
1. 根據您的作業系統，將QueueSharing.swf檔案從「資源視圖」拖動到Windows案頭或等效位置。
1. 在管理控制台中，按一下「服務」>「EMC Documentum的連接器」>「配置設定」。
1. 在「儲存庫服務提供程式資訊」下，將配置的儲存庫提供程式更改為「 EMC Documentum儲存庫提供程式」。
1. 啟動Workbench，將QueueSharing.swf檔案從您最初將其複製到的位置（例如，Windows案頭或其他位置）複製到EMC Documentum儲存庫內的現有目錄中。
1. 在「工作台流程」檢視中，開啟「佇列共用」流程。
1. 在「變數」視圖中，開啟&quot;theForm&quot;變數的屬性，並更改URI以匹配您在步驟5中放置QueueSharing.swf檔案的路徑。
1. 儲存程式。
1. 根據貴組織的原則，將程式移轉至生產環境。
