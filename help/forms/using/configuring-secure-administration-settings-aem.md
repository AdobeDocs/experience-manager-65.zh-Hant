---
title: 在JEE上為AEM Forms配置安全管理設定
seo-title: Configuring Secure Administration Settings for AEM Forms on JEE
description: 瞭解如何管理用戶帳戶和服務，儘管在私有開發環境中是必需的，但在AEM FormsJEE的生產環境中卻不是必需的。
seo-description: Learn how to administer user accounts and services that, although required in a private development environment, are not required in a production environment of AEM Forms on JEE.
uuid: 04e45d06-f57d-406c-8228-15f483199430
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: d211d8b0-e75f-49c3-808d-5d0e26ad3a6b
role: Admin
exl-id: 40bc01b4-a59e-4420-81d6-2887857bddce
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 0%

---

# 在JEE上為AEM Forms配置安全管理設定 {#configuring-secure-administration-settings-for-aem-forms-on-jee}

瞭解如何管理用戶帳戶和服務，儘管在私有開發環境中是必需的，但在AEM FormsJEE的生產環境中卻不是必需的。

通常，開發人員不會使用生產環境來構建和test其應用程式。 因此，您必須管理用戶帳戶和服務，儘管這些帳戶和服務在專用開發環境中是必需的，但在生產環境中卻不是必需的。

本文介紹了通過AEM Forms在JEE上提供的管理選項來減少整體攻擊面的方法。

## 禁用對服務的非基本遠程訪問 {#disabling-non-essential-remote-access-to-services}

在JEE上安裝和配置AEM Forms後，許多服務都可用於通過SOAP和Enterprise JavaBeans™(EJB)進行遠程調用。在本例中，術語「遠程」是指對應用程式伺服器的SOAP、EJB或操作消息格式(AMF)埠具有網路訪問權限的任何調用方。

儘管AEM FormsJEE服務需要為授權呼叫者傳遞有效憑據，但您應僅允許遠程訪問需要遠程訪問的服務。 要實現有限的可訪問性，您應將遠程訪問服務集減少到運行系統所能使用的最小值，然後啟用對您需要的其他服務的遠程調用。

AEM Forms的JEE服務始終至少需要SOAP訪問。 這些服務通常是Workbench使用的必需服務，但也包括由Workspace Web應用程式調用的服務。

使用Administration Console中的Applications and Services網頁完成此過程：

1. 通過在Web瀏覽器中鍵入以下URL登錄到Administration Console:

   ```java
            https://[host name]:'port'/adminui
   ```

1. 按一下 **服務>應用程式和服務>首選項**。
1. 設定「首選項」以在同一頁上查看最多200個服務和端點。
1. 按一下 **服務** > **應用程式和服務** > **終結點管理**。
1. 選擇 **EJB** 從 **提供程式** 清單，然後按一下 **篩選**。
1. 要禁用所有EJB端點，請選中清單中每個端點旁邊的複選框，然後按一下 **禁用**。
1. 按一下 **下一個** 對所有EJB端點重複上一步。 在禁用終結點之前，請確保在「提供程式」列中列出EJB。
1. 選擇 **SOAP** 從 **提供程式** 清單，然後按一下 **篩選**。
1. 要刪除SOAP端點，請選中清單中每個端點旁邊的複選框，然後按一下 **刪除**。 不要刪除以下端點：

   * AuthenticationManager服務
   * DirectoryManager服務
   * 作業管理器
   * 事件_管理_服務
   * 事件_configuration_service
   * 進程管理器
   * 模板管理器
   * 儲存庫服務
   * TaskManager服務
   * 任務隊列管理器
   * TaskManager查詢服務
   * 工作區單點登錄
   * 應用程式管理器

1. 按一下 **下一個** 並對上面清單中未包含的SOAP端點重複上一步。 在刪除端點之前，請確保在「提供程式」列中列出SOAP。

## 禁用對服務的非必需匿名訪問 {#disabling-non-essential-anonymous-access-to-services}

某些表單伺服器服務允許對某些操作執行未經驗證（匿名）的調用。 這意味著，由服務公開的一個或多個操作可以作為任何經過驗證的用戶或根本不作為經過驗證的用戶調用。

1. 通過在Web瀏覽器中鍵入以下URL登錄到管理控制台：

   ```java
            https://[host name]:'port'/adminui
   ```

1. 按一下 **服務>應用程式和服務>服務管理**。
1. 按一下要禁用的服務的名稱（例如，AuthenticationManagerService）。
1. 按一下 **「安全」頁籤**&#x200B;取消選擇 **允許匿名訪問**，然後按一下 **保存**。
1. 完成以下服務的步驟3和4:

   * AuthenticationManager服務
   * EJB
   * 電子郵件
   * 作業管理器
   * 監視資料夾
   * 用戶管理器UtilService
   * 遠程處理
   * 儲存庫提供程式服務
   * EMCDocumentumRepositoryProvider
   * IBMFilenetRepositoryProvider
   * 形式加號
   * TaskManager服務
   * 任務管理器連接器
   * TaskManager查詢服務
   * 任務隊列管理器
   * 任務終結點管理器
   * 用戶服務
   * WorkspaceSearchTemplateService
   * WorkspacePropertyService
   * 輸出服務
   * 表單服務

   如果要公開這些服務中的任何一個以進行遠程調用，您還應考慮禁用這些服務的匿名訪問。 否則，任何有權訪問此服務的呼叫者都可以調用該服務，而不傳遞有效的憑據。

   對於任何不需要的服務，應禁用匿名訪問。 許多內部服務需要啟用匿名身份驗證，因為可能需要由系統中的潛在任何用戶調用這些身份驗證，而無需預先授權。

## 更改預設全局超時 {#changing-the-default-global-time-out}

最終用戶可以通過Workbench、AEM FormsWeb應用程式或調用AEM Forms伺服器服務的自定義應用程式驗證到AEM Forms。 一個全局超時設定用於指定這些用戶在被強制重新驗證之前可以與AEM Forms（使用基於SAML的斷言）交互多長時間。 預設設定為2小時。 在生產環境中，需要將時間量減少到可接受的最小分鐘數。

### 最小化重新驗證時間限制 {#minimize-reauthentication-time-limit}

1. 通過在Web瀏覽器中鍵入以下URL登錄到管理控制台：

   ```java
            https://[host name]:'port'/adminui
   ```

1. 按一下 **設定>用戶管理>配置>導入和導出配置檔案**。
1. 按一下 **導出** 生成具有現有AEM Forms設定的config.xml檔案。
1. 在編輯器中開啟XML檔案並找到以下條目：

   `<entry key="assertionValidityInMinutes" value="120"/>`

1. 將值更改為大於5（分鐘）的任意數字並保存檔案。
1. 在管理控制台中，導航到「導入和導出配置檔案」頁。
1. 輸入修改的config.xml檔案的路徑，或按一下「瀏覽」導航到該檔案。
1. 按一下 **導入** 上載修改的config.xml檔案，然後按一下 **確定**。
