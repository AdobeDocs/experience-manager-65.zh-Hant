---
title: 配置JEE上AEM Forms的安全管理設定
seo-title: Configuring Secure Administration Settings for AEM Forms on JEE
description: 了解如何管理使用者帳戶和服務，雖然這些是私人開發環境中的必要項目，但在JEE上的AEM Forms生產環境中並非必要項目。
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

# 配置JEE上AEM Forms的安全管理設定 {#configuring-secure-administration-settings-for-aem-forms-on-jee}

了解如何管理使用者帳戶和服務，雖然這些是私人開發環境中的必要項目，但在JEE上的AEM Forms生產環境中並非必要項目。

一般而言，開發人員不會使用生產環境來建立和測試其應用程式。 因此，您必須管理使用者帳戶和服務，雖然這些是私人開發環境中的必要項目，但在生產環境中並非必要項目。

本文透過AEM Forms on JEE提供的管理選項，說明減少整體攻擊面的方法。

## 禁用對服務的非必需遠程訪問 {#disabling-non-essential-remote-access-to-services}

在安裝和配置JEE上的AEM Forms後，許多服務都可用於通過SOAP和Enterprise JavaBeans™(EJB)進行遠程調用。在本例中，遠程術語是指任何對應用程式伺服器的SOAP、EJB或Action Message Format(AMF)埠具有網路訪問權限的調用方。

雖然JEE服務上的AEM Forms需要為授權呼叫者傳遞有效憑證，但您應僅允許遠程訪問您需要遠程訪問的服務。 要實現有限的可訪問性，您應將遠程可訪問的服務集減少到功能正常的系統所能達到的最低程度，然後啟用遠程調用所需的其他服務。

AEM Forms on JEE服務一律需要至少SOAP存取權。 這些服務通常為Workbench使用所需，但也包括由Workspace網頁應用程式呼叫的服務。

使用管理控制台中的「應用程式和服務」網頁完成此過程：

1. 在Web瀏覽器中輸入以下URL以登入Administration Console:

   ```java
            https://[host name]:'port'/adminui
   ```

1. 按一下 **「服務」>「應用程式和服務」>「首選項」**.
1. 設定「首選項」以在同一頁上查看最多200個服務和端點。
1. 按一下 **服務** > **應用程式和服務** > **端點管理**.
1. 選擇 **EJB** 從 **提供者** 清單，然後按一下 **篩選**.
1. 要禁用所有EJB端點，請選中清單中每個端點旁邊的複選框，然後按一下 **停用**.
1. 按一下 **下一個** 對所有EJB端點重複上一步。 在禁用終結點之前，請確保在「提供程式」列中列出了EJB。
1. 選擇 **SOAP** 從 **提供者** 清單，然後按一下 **篩選**.
1. 要刪除SOAP端點，請選中清單中每個端點旁邊的複選框，然後按一下 **移除**. 請勿移除下列端點：

   * AuthenticationManagerService
   * DirectoryManager服務
   * JobManager
   * event_management_service
   * event_configuration_service
   * ProcessManager
   * TemplateManager
   * RepositoryService
   * TaskManagerService
   * 任務隊列管理器
   * TaskManagerQueryService
   * WorkspaceSingleSignOn
   * ApplicationManager

1. 按一下 **下一個** 並對不在上述清單中的SOAP端點重複上一步。 移除端點之前，請確定SOAP列在「提供者」欄中。

## 禁用對服務的非必需匿名訪問 {#disabling-non-essential-anonymous-access-to-services}

某些表單伺服器服務允許對某些操作進行未驗證（匿名）的調用。 這意味著，可以作為任何已驗證用戶或完全沒有已驗證用戶調用由服務公開的一個或多個操作。

1. 在網頁瀏覽器中輸入下列URL，登入管理主控台：

   ```java
            https://[host name]:'port'/adminui
   ```

1. 按一下 **服務>應用程式和服務>服務管理**.
1. 按一下要禁用的服務的名稱（例如AuthenticationManagerService）。
1. 按一下 **「安全」頁簽**，取消選取 **允許匿名訪問**，然後按一下 **儲存**.
1. 完成下列服務的步驟3和4:

   * AuthenticationManagerService
   * EJB
   * 電子郵件
   * JobManager
   * WatchedFolder
   * UsermanagerUtilService
   * 遠端
   * RepositoryProviderService
   * EMCDocumentumRepositoryProvider
   * IBMFilenetRepositoryProvider
   * FormAugmenter
   * TaskManagerService
   * TaskManagerConnector
   * TaskManagerQueryService
   * 任務隊列管理器
   * TaskEndpointManager
   * UserService
   * WorkspaceSearchTemplateService
   * WorkspacePropertyService
   * OutputService
   * FormsService

   如果要為遠程調用公開這些服務中的任何服務，您也應考慮禁用這些服務的匿名訪問。 否則，任何具有此服務的網路訪問權的呼叫者都可能調用該服務，而不傳遞有效的憑據。

   對於任何不需要的服務，應禁用匿名訪問。 許多內部服務都要求啟用匿名身份驗證，因為這些身份驗證需要由系統中可能的任何用戶調用，而無需預先授權。

## 更改預設全局超時 {#changing-the-default-global-time-out}

一般使用者可透過Workbench、AEM Forms Web應用程式或叫用AEM Forms伺服器服務的自訂應用程式，驗證AEM Forms。 一個全域逾時設定用來指定這些使用者在被迫重新驗證前，可與AEM Forms互動（使用SAML型斷言）的時間長度。 預設設定為2小時。 在生產環境中，時間量必須縮短至可接受的最小分鐘數。

### 將重新驗證時間限制最小化 {#minimize-reauthentication-time-limit}

1. 在網頁瀏覽器中輸入下列URL，登入管理主控台：

   ```java
            https://[host name]:'port'/adminui
   ```

1. 按一下 **設定>使用者管理>設定>匯入和匯出設定檔**.
1. 按一下 **匯出** 若要使用現有的AEM Forms設定產生config.xml檔案。
1. 在編輯器中開啟XML檔案，並找到下列項目：

   `<entry key="assertionValidityInMinutes" value="120"/>`

1. 將值變更為大於5的任何數字（以分鐘為單位），然後儲存檔案。
1. 在管理控制台中，導覽至匯入和匯出組態檔頁面。
1. 輸入修改的config.xml檔案的路徑，或按一下「瀏覽」導航到該檔案。
1. 按一下 **匯入** 上傳修改的config.xml檔案，然後按一下 **確定**.
