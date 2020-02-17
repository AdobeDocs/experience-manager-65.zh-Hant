---
title: 在JEE上設定AEM Forms的安全管理設定
seo-title: 在JEE上設定AEM Forms的安全管理設定
description: 瞭解如何管理使用者帳戶和服務，這些帳戶和服務雖然在私人開發環境中是必要的，但在JEE上的AEM Forms生產環境中卻是不必要的。
seo-description: 瞭解如何管理使用者帳戶和服務，這些帳戶和服務雖然在私人開發環境中是必要的，但在JEE上的AEM Forms生產環境中卻是不必要的。
uuid: 04e45d06-f57d-406c-8228-15f483199430
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: d211d8b0-e75f-49c3-808d-5d0e26ad3a6b
translation-type: tm+mt
source-git-commit: b2fd6e0412ee0dacf7b68f4a0b219804dd4a6150

---


# 在JEE上設定AEM Forms的安全管理設定 {#configuring-secure-administration-settings-for-aem-forms-on-jee}

瞭解如何管理使用者帳戶和服務，這些帳戶和服務雖然在私人開發環境中是必要的，但在JEE上的AEM Forms生產環境中卻是不必要的。

一般而言，開發人員不會使用生產環境來建立和測試其應用程式。 因此，您必須管理在私人開發環境中不需要的使用者帳戶和服務。

本文說明透過AEM Forms on JEE提供的管理選項來降低整體攻擊面的方法。

## 禁用對服務的非基本遠程訪問 {#disabling-non-essential-remote-access-to-services}

在安裝和設定JEE上的AEM Forms後，許多服務都可供透過SOAP和Enterprise JavaBeans™(EJB)進行遠端呼叫。在本例中，遠端一詞是指可以網路存取應用程式伺服器的SOAP、EJB或Action Message Format(AMF)埠的呼叫者。

雖然JEE服務上的AEM Forms需要為授權呼叫者傳遞有效憑證，但您應僅允許遠端存取您需要遠端存取的服務。 要實現有限的可訪問性，您應將遠程可訪問服務集減少到功能正常的系統所能使用的最低程度，然後啟用遠程調用所需的其他服務。

JEE服務上的AEM Forms永遠至少需要SOAP存取權。 這些服務通常是Workbench使用的必要條件，但也包含由Workspace web應用程式呼叫的服務。

使用Administration console的「應用程式與服務」網頁完成此程式：

1. 在網頁瀏覽器中輸入下列URL以登入「管理控制台」:

   ```as3
            https://[host name]:[port]/adminui
   ```

1. 按一 **下「服務>應用程式與服務>偏好設定」**。
1. 設定「偏好設定」，在同一頁面上檢視最多200個服務和端點。
1. 按一 **下「服務** >應 **用程式與服務** >端點 **管理」**。
1. 從「提 **供者** 」清單中選取 **EJB** ，然後按一下「篩 **選器**」。
1. 要禁用所有EJB端點，請選中清單中每個端點旁的複選框，然後按一下「禁 **用」**。
1. 按一下「 **下一步** 」，對所有EJB端點重複上一步。 在禁用端點之前，請確保EJB列在「提供程式」列中。
1. 從「提 **供者** 」清單中選取 **SOAP** ，然後按一下「 **篩選器**」。
1. 要刪除SOAP端點，請選中清單中每個端點旁的複選框，然後按一下「刪 **除」**。 請勿移除下列端點：

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

1. 單 **擊「下一步** 」，對不在上述清單中的SOAP端點重複上一步。 在移除端點之前，請確定SOAP已列在「提供者」欄中。

## 停用非必要的匿名服務存取 {#disabling-non-essential-anonymous-access-to-services}

某些表單伺服器服務允許某些作業的未驗證（匿名）呼叫。 這表示服務公開的一個或多個操作可以作為任何已驗證用戶或完全沒有已驗證用戶被調用。

1. 在網頁瀏覽器中輸入下列URL，以登入管理控制台：

   ```as3
            https://[host name]:[port]/adminui
   ```

1. 按一 **下「服務>應用程式與服務>服務管理」**。
1. 按一下要禁用的服務的名稱（例如，AuthenticationManagerService）。
1. 按一下「安 **全性」標籤**，取消選 **取「允許匿名存取**」，然後按一 **下「儲存**」。
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

## 變更預設全域逾時 {#changing-the-default-global-time-out}

使用者可以透過Workbench、AEM Forms web應用程式或叫用AEM Forms伺服器服務的自訂應用程式，驗證AEM Forms。 全域逾時設定可用來指定這些使用者在被迫重新驗證之前，可與AEM Forms（使用SAML架構的斷言）互動的時間長度。 預設設定為2小時。 在生產環境中，需要將時間縮減為可接受的最小分鐘數。

### 將重新驗證時間限制降到最低 {#minimize-reauthentication-time-limit}

1. 在網頁瀏覽器中輸入下列URL，以登入管理控制台：

   ```as3
            https://[host name]:[port]/adminui
   ```

1. 按一 **下「設定>使用者管理>設定>匯入和匯出設定檔」**。
1. 按一 **下「匯出** 」，以使用現有的AEM Forms設定產生config.xml檔案。
1. 在編輯器中開啟XML檔案並找到以下條目：

   `<entry key=”assertionValidityInMinutes” value=”120”/>`

1. 將值變更為大於5（以分鐘為單位）的任何數字，並儲存檔案。
1. 在管理控制台中，導覽至「匯入和匯出設定檔」頁面。
1. 輸入已修改config.xml檔案的路徑，或按一下瀏覽導航到該檔案。
1. 按一 **下「匯入** 」以上傳已修改的config.xml檔案，然後按一下「 **確定」**。

