---
title: 在JEE上為AEM Forms配置安全管理設定
seo-title: 在JEE上為AEM Forms配置安全管理設定
description: 瞭解如何管理用戶帳戶和服務，雖然這些帳戶和服務在私人開發環境中是必要的，但在AEM Forms的JEE生產環境中卻不是必要的。
seo-description: 瞭解如何管理用戶帳戶和服務，雖然這些帳戶和服務在私人開發環境中是必要的，但在AEM Forms的JEE生產環境中卻不是必要的。
uuid: 04e45d06-f57d-406c-8228-15f483199430
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: d211d8b0-e75f-49c3-808d-5d0e26ad3a6b
role: 管理員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 0%

---


# 在JEE {#configuring-secure-administration-settings-for-aem-forms-on-jee}上配置AEM Forms的安全管理設定

瞭解如何管理用戶帳戶和服務，雖然這些帳戶和服務在私人開發環境中是必要的，但在AEM Forms的JEE生產環境中卻不是必要的。

一般而言，開發人員不會使用生產環境來建立和測試其應用程式。 因此，您必須管理在私人開發環境中不需要的使用者帳戶和服務。

本文介紹了通過JEE上AEM Forms提供的管理選項來減少整體攻擊面的方法。

## 禁用對服務的非基本遠程訪問{#disabling-non-essential-remote-access-to-services}

在安裝並配置JEE上的AEM Forms後，許多服務都可用於通過SOAP和Enterprise JavaBeans™(EJB)進行遠程調用。在本例中，遠程術語是指對應用程式伺服器的SOAP、EJB或Action Message Format(AMF)埠具有網路訪問權的任何調用方。

雖然AEM Forms的JEE服務需要為授權呼叫者傳遞有效的認證，但您應只允許遠程訪問需要遠程訪問的服務。 要實現有限的可訪問性，您應將遠程可訪問服務集減少到功能正常的系統所能使用的最低程度，然後啟用遠程調用所需的其他服務。

AEM Forms的JEE服務始終至少需要SOAP訪問。 這些服務通常是Workbench使用的必要條件，但也包含由Workspace Web應用程式呼叫的服務。

使用Administration Console的「應用程式與服務」網頁完成此程式：

1. 在網頁瀏覽器中輸入下列URL以登入「管理控制台」:

   ```java
            https://[host name]:'port'/adminui
   ```

1. 按一下「**服務>應用程式與服務>偏好設定**」。
1. 設定「偏好設定」，在同一頁面上檢視最多200個服務和端點。
1. 按一下「**服務** > **應用程式和服務** > **端點管理**」。
1. 從&#x200B;**Provider**&#x200B;清單中選擇&#x200B;**EJB**，然後按一下&#x200B;**Filter**。
1. 要禁用所有EJB端點，請選中清單中每個端點旁的複選框，然後按一下&#x200B;**禁用**。
1. 按一下&#x200B;**Next** ，對所有EJB端點重複上一步。 在禁用端點之前，請確保EJB列在「提供程式」列中。
1. 從&#x200B;**Provider**&#x200B;清單中選擇&#x200B;**SOAP**，然後按一下&#x200B;**Filter**。
1. 要刪除SOAP端點，請選中清單中每個端點旁的複選框，然後按一下&#x200B;**刪除**。 請勿移除下列端點：

   * AuthenticationManagerService
   * DirectoryManagerService
   * JobManager
   * event_management_service
   * event_configuration_service
   * ProcessManager
   * TemplateManager
   * RepositoryService
   * TaskManagerService
   * TaskQueueManager
   * TaskManagerQueryService
   * 工作區單一登入
   * ApplicationManager

1. 按一下&#x200B;**Next**，對上面清單中未包含的SOAP端點重複上一步驟。 在移除端點之前，請確定SOAP已列在「提供者」欄中。

## 禁用對服務{#disabling-non-essential-anonymous-access-to-services}的非基本匿名訪問

某些表單伺服器服務允許某些作業的未驗證（匿名）呼叫。 這表示服務公開的一個或多個操作可以作為任何已驗證用戶或完全沒有已驗證用戶被調用。

1. 在網頁瀏覽器中輸入下列URL，以登入管理控制台：

   ```java
            https://[host name]:'port'/adminui
   ```

1. 按一下&#x200B;**服務>應用程式和服務>服務管理**。
1. 按一下要禁用的服務的名稱（例如，AuthenticationManagerService）。
1. 按一下&#x200B;**安全頁籤**，取消選擇&#x200B;**允許匿名訪問** ，然後按一下&#x200B;**保存**。
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
   * TaskQueueManager
   * TaskEndpointManager
   * UserService
   * WorkspaceSearchTemplateService
   * WorkspacePropertyService
   * OutputService
   * FormsService

   如果您要公開這些服務中的任何一項以進行遠程調用，您也應考慮禁用這些服務的匿名訪問。 否則，任何有權訪問此服務的呼叫者都可能在未通過有效憑證的情況下調用服務。

   對於任何不需要的服務，應禁用匿名訪問。 許多內部服務都需要啟用匿名驗證，因為這些驗證需要由系統中任何可能的使用者呼叫，而不需預先授權。

## 更改預設全局超時{#changing-the-default-global-time-out}

使用者可以透過Workbench、AEM Forms網路應用程式或叫用AEM Forms伺服器服務的自訂應用程式，向AEM Forms進行驗證。 一個全域逾時設定可用來指定此類使用者在被迫重新驗證之前，可與AEM Forms（使用SAML架構斷言）互動的時間。 預設設定為2小時。 在生產環境中，需要將時間縮減為可接受的最小分鐘數。

### 將重新驗證時間限制降至最低{#minimize-reauthentication-time-limit}

1. 在網頁瀏覽器中輸入下列URL，以登入管理控制台：

   ```java
            https://[host name]:'port'/adminui
   ```

1. 按一下「**設定>用戶管理>配置>導入和導出配置檔案**」。
1. 按一下「**匯出**」，以產生具有現有AEM Forms設定的config.xml檔案。
1. 在編輯器中開啟XML檔案並找到以下條目：

   `<entry key=”assertionValidityInMinutes” value=”120”/>`

1. 將值變更為大於5（以分鐘為單位）的任何數字，並儲存檔案。
1. 在管理控制台中，導覽至「匯入和匯出設定檔」頁面。
1. 輸入已修改config.xml檔案的路徑，或按一下瀏覽導航到該檔案。
1. 按一下「**匯入**」上傳已修改的config.xml檔案，然後按一下「確定」。****

