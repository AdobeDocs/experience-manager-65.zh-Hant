---
title: 設定伺服器設定
description: 「伺服器設定」頁面提供電子郵件、工作通知和管理員通知設定的存取權。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 362b7b91-c58b-4e47-a6ef-56a4b54a100c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '2643'
ht-degree: 0%

---

# 設定伺服器設定 {#configuring-server-settings}

「伺服器設定」頁面可讓您存取表單工作流程的各種設定：

* **電子郵件設定**&#x200B;可啟用外寄電子郵件訊息，以及這些訊息所使用的電子郵件伺服器設定。 （請參閱[設定電子郵件設定](configuring-server-settings.md#configuring-email-settings)。）
* **工作通知設定**&#x200B;可啟用、停用或修改傳送給使用者與群組有關其工作的電子郵件通知訊息。 （請參閱[設定使用者和群組的通知](configuring-server-settings.md#configuring-notifications-for-users-and-groups)。）
* **管理員通知設定**，可啟用、停用或修改管理工作的電子郵件通知中所傳送的訊息。 （請參閱[設定管理員的通知](configuring-server-settings.md#configuring-notifications-for-administrators)。）

## 正在設定電子郵件設定 {#configuring-email-settings}

您可以為Forms伺服器指定電子郵件帳戶，透過該帳戶傳送電子郵件訊息給AEM表單使用者和管理員。 這些電子郵件訊息用於通知和提醒使用者他們必須完成的工作、通知使用者任務已達到截止日期，以及通知管理員發生的任何程式錯誤。

若要在AEM表單和使用者之間啟用電子郵件訊息的傳送，請在「電子郵件設定」頁面上設定寄出電子郵件設定。 寄出電子郵件必須使用SMTP伺服器。

若要讓AEM表單接收並處理來自使用者的傳入電子郵件訊息，請為「完成任務」服務建立電子郵件端點。 （請參閱[為完成工作服務建立電子郵件端點](/help/forms/using/admin-help/configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service)）。

如果您的流程在設計及實作時不需要電子郵件，則您不需要在「電子郵件設定」頁面上設定任何選項。

### 設定外寄電子郵件設定 {#configure-outgoing-email-settings}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

1. 在管理控制檯中，按一下「服務>表單工作流程>伺服器設定>電子郵件設定」。
1. 選取啟用外寄郵件。
1. 在「SMTP伺服器」方塊中，輸入電子郵件伺服器名稱或IP位址。 表單工作流程的所有通知電子郵件訊息都會從此電子郵件伺服器傳送。
1. 在「使用者名稱」和「密碼」方塊中，輸入SMTP伺服器需要驗證時所使用的登入名稱和密碼。 如果允許匿名登入，則保留空白。
1. 在「電子郵件地址」方塊中，輸入電子郵件地址，用作Forms Workflow所傳送電子郵件訊息的回傳地址。

   >[!NOTE]
   >
   >如果您使用Microsoft Exchange Server，而且電子郵件地址為無效的電子郵件地址，則Microsoft Exchange Server無法傳送電子郵件至通訊群組清單。 若要解決此問題，請為Microsoft Exchange伺服器上的每個通訊群組清單分別選取&#x200B;**啟用外部通訊**&#x200B;選項。

1. 按一下「儲存」。

>[!NOTE]
>
>如果您輸入了不正確的資訊，可以按一下「取消」返回先前顯示的頁面。

### 設定電子郵件範本以使用AEM Forms Workspace {#configuring-email-templates-to-use-html-workspace}

>[!NOTE]
>
>AEM Forms版本已棄用Flex Workspace。

根據預設，AEM表單傳送的電子郵件會包含指向(JEE不建議使用AEM表單) Flex Workspace的連結。 您可以設定AEM表單，以傳送包含AEM Forms Workspace連結的電子郵件。 若要進一步瞭解AEM Forms Workspace優於(JEE上的AEM Forms已棄用) Flex Workspace，請參閱[此](/help/forms/using/features-html-workspace-available-flex.md)文章。

1. 在管理控制檯中，按一下首頁>服務>表單工作流程>伺服器設定>任務通知。
1. 開啟任務指派範本。
1. 將任務通知中的範本設定為下列專案： `https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@`

   ```java
   https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@
   ```

## 設定使用者和群組的通知 {#configuring-notifications-for-users-and-groups}

在「任務通知」頁面上，您可以設定表單工作流程將用來產生傳送給使用者和群組的電子郵件通知的範本。 您可以使用表單工作流程變數來自訂通知及設定通知格式。

您可以為使用者和群組設定下列型別的通知：

* 提醒
* 任務指派
* 截止日期

若要產生群組的電子郵件通知，請在「使用者管理」中指定群組的電子郵件地址。 <!--Fix broken link See Setting up and organizing users -->當表單工作流程傳送電子郵件通知給群組時，群組中每個具有指定電子郵件地址的成員都會收到電子郵件通知。 當群組的成員收到電子郵件通知並想要宣告任務時，該成員必須按一下電子郵件通知中的宣告連結，這會在Workspace中開啟任務詳細資訊頁面。 從那裡，成員可以要求或要求並開啟工作專案。

>[!NOTE]
>
>AEM Forms版本已棄用Flex工作區。

### 設定使用者或群組的提醒 {#configure-reminders-for-users-or-groups}

臨近完成任務的截止日期時，您可以向指派的使用者或群組傳送提醒通知。 用於決定提醒通知確切何時傳送的規則由流程開發人員決定。

1. 在管理控制檯中，按一下「服務> Forms工作流程>伺服器設定>工作通知」。
1. 在「通知型別」下，按一下「提醒」（適用於使用者）或「群組 — 提醒」（適用於群組）。
1. 選取「啟用提醒」或「啟用群組 — 提醒」。
1. （僅限使用者通知）若要在提醒電子郵件訊息中包含表單及其資料的附件，請選取「包含表單資料」。
1. 在「主旨」方塊中，輸入電子郵件主旨行的文字。 此欄位已預先填入預設文字。 如需有關自訂此欄位的詳細資訊，請參閱[自訂通知內容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在「通知範本」方塊中，輸入電子郵件內文的文字。 此欄位已預先填入預設文字。 如需有關自訂此欄位的詳細資訊，請參閱[自訂通知內容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在「郵件格式」清單中，選取傳送電子郵件訊息的格式，即HTML或文字。 預設格式為HTML。
1. 在電子郵件編碼清單中，選取用於電子郵件訊息的編碼格式。 預設值為UTF-8，日本以外的大多數使用者都會使用它。 日本使用者可選擇ISO2022-JP。
1. 按一下「儲存」。

### 設定使用者或群組的任務指派通知 {#configure-task-assignment-notifications-for-users-or-groups}

您可以在使用者或群組被指派任務時，將任務指派通知傳送給他們。

1. 在管理控制檯中，按一下「服務> Forms工作流程>伺服器設定>工作通知」。
1. 在通知型別下，按一下使用者的任務指派或群組 — 群組的任務指派。
1. 選取「啟用使用者的任務指派」或「啟用群組 — 群組的任務指派」。
1. （僅限使用者通知）若要在任務指派電子郵件訊息中包含表單及其資料的附件，請選取「包含表單資料」。
1. 在「主旨」方塊中，輸入電子郵件主旨行的文字。 此欄位已預先填入預設文字。 如需有關自訂此欄位的詳細資訊，請參閱[自訂通知內容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在「通知範本」方塊中，輸入電子郵件內文的文字。 此欄位已預先填入預設文字。 如需有關自訂此欄位的詳細資訊，請參閱[自訂通知內容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在「郵件格式」清單中，選取傳送電子郵件訊息的格式，即HTML或文字。 預設格式為HTML。
1. 在電子郵件編碼清單中，選取用於電子郵件訊息的編碼格式。 預設值為UTF-8，日本以外的大多數使用者都會使用它。 日本使用者可選擇ISO2022-JP。
1. 按一下「儲存」。

### 設定使用者或群組的截止日期通知 {#configure-deadline-notifications-for-users-or-groups}

您可以在對指派的任務採取行動的截止日期已過時，向使用者和群組傳送截止日期通知。 期限通知通常是資訊性的，因為使用者無法再對指派的任務採取行動。

1. 在管理控制檯中，按一下「服務> Forms工作流程>伺服器設定>工作通知」。
1. 在「通知型別」(Notification Type)下，按一下「截止日期」(Deadline) （適用於使用者）或「群組 — 截止日期」(Group) （適用於群組）。
1. 選取「啟用期限」或「啟用群組 — 期限」。
1. 在「主旨」方塊中，輸入電子郵件主旨行的文字。 此欄位已預先填入預設文字。 如需有關自訂此欄位的詳細資訊，請參閱[自訂通知內容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在「通知範本」方塊中，輸入電子郵件內文的文字。 此欄位已預先填入預設文字。 如需有關自訂此欄位的詳細資訊，請參閱[自訂通知內容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在「郵件格式」清單中，選取傳送電子郵件訊息的格式，即HTML或文字。 預設格式為HTML。
1. 在電子郵件編碼清單中，選取用於電子郵件訊息的編碼格式。 預設值為UTF-8，日本以外的大多數使用者都會使用它。 日本使用者可選擇ISO2022-JP。
1. 按一下「儲存」。

### 隱藏所有電子郵件的「不DELETE」標籤 {#hide-the-do-not-delete-tag-for-all-emails}

您可以設定電子郵件，以隱藏在以人為中心的流程傳送的所有電子郵件中，不要DELETE追蹤標籤。

<!-- 
For details, see [How to hide the 'DO-NOT-DELETE' tag with CSS](https://blogs.adobe.com/LiveCycleHelp/2013/09/how-to-hide-the-do-not-delete-tag-with-css.html) 
-->

## 為管理員設定通知 {#configuring-notifications-for-administrators}

您可以設定表單工作流程將用來產生傳送給管理員之電子郵件通知的範本。

您可以為管理員設定下列型別的通知：

* 已停止的分支
* 已停止的作業

### 設定停止的分支通知 {#configure-stalled-branch-notifications}

如果分支中止（故意或因錯誤而停止執行），您可以傳送電子郵件通知給管理員或其他使用者，管理員或使用者隨後可以調查問題。

1. 在管理控制檯中，按一下「服務> Forms工作流程>伺服器設定>管理員通知」。
1. 在「通知型別」下，按一下「停止的分支」。
1. 選取啟用停止的分支。
1. 在「電子郵件地址」方塊中，輸入分支停止時要通知的使用者地址。 使用格式user@domain.com ，並以逗號分隔每個地址。 通常此電子郵件地址是管理員的。
1. 在「主旨」方塊中，輸入電子郵件主旨行的文字。 此欄位已預先填入預設文字。 如需有關自訂此欄位的詳細資訊，請參閱[自訂通知內容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在「通知範本」方塊中，輸入電子郵件內文的文字。 此欄位已預先填入預設文字。 如需有關自訂此欄位的詳細資訊，請參閱[自訂通知內容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在「郵件格式」清單中，選取傳送電子郵件訊息的格式，即HTML或文字。 預設格式為HTML。
1. 在電子郵件編碼清單中，選取用於電子郵件訊息的編碼格式。 預設值為UTF-8，日本以外的大多數使用者都使用它。 日本使用者可選擇ISO2022-JP。
1. 按一下「儲存」。

### 設定停止的操作通知 {#configure-stalled-operation-notifications}

如果作業中止（故意或因錯誤而停止執行），您可以傳送電子郵件通知給管理員或其他使用者，讓他們調查問題。

1. 在管理控制檯中，按一下「服務> Forms工作流程>伺服器設定>管理員通知」。
1. 在「通知型別」下，按一下「已停止的作業」。
1. 選取「啟用停止的作業」。
1. 在「電子郵件地址」方塊中，輸入作業停止時要通知的使用者地址。 使用格式user@domain.com ，並以逗號分隔每個地址。 通常此電子郵件地址是管理員的。
1. 在「主旨」方塊中，輸入電子郵件主旨行的文字。 此欄位已預先填入預設文字。 如需有關自訂此欄位的詳細資訊，請參閱[自訂通知內容](configuring-server-settings.md#customizing-the-content-of-notifications)
1. 在「通知範本」方塊中，輸入電子郵件內文的文字。 此欄位已預先填入預設文字。 如需有關自訂此欄位的詳細資訊，請參閱[自訂通知內容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 按一下「儲存」。

## 自訂通知內容 {#customizing-the-content-of-notifications}

「工作通知」與「管理員通知」頁面提供數個功能，可讓您自訂通知訊息：

* RTF編輯器
* 變數選取器
* URL產生

### RTF編輯器 {#rich-text-editor}

「通知範本」區域是RTF編輯器，可讓您產生電子郵件通知訊息的HTML。 它提供字型和段落格式選項，這些選項可在「通知範本」方塊下找到。 選項包括字型型別、大小、樣式和顏色，以及段落對齊和專案符號。

### URL產生 {#url-generation}

僅針對任務通知，Forms工作流程包含兩個預先定義的URL設定，您可以將其從URL產生清單拖曳至「通知範本」方塊，然後進行自訂：

* OpenTask可用於「提醒」和「任務指派」通知型別。 此URL提供Workspace中任務的連結，可讓使用者從電子郵件通知快速存取任務。 當您將OpenTask URL拖曳到「通知範本」方塊時，URL的格式如下：

  `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

* ClaimTask可用於「群組 — 提醒」和「群組 — 任務指派」通知型別。 此URL提供指向Workspace中任務詳細資訊頁面的連結，使用者可以在其中宣告或宣告並開啟工作專案。 當您將ClaimTask URL拖曳到「通知範本」方塊時，URL的格式如下：

  `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

>[!NOTE]
>
>AEM Forms版本已棄用Flex工作區。

如果您的解決方案部署在叢集環境中，請將`@@notification-host@@`取代為叢集位址。

`<`*PORT* `>`是應用程式伺服器之HTTP接聽程式的連線埠號碼。 支援的應用程式伺服器的預設HTTP監聽器連線埠如下：

**JBoss：** 8080

**OracleWebLogic伺服器：** 7001

**IBM WebSphere：** 9080

若要讓這些URL正常運作，請將&#x200B;`<`*連線埠* `>`取代為適合您環境的連線埠號碼。

>[!NOTE]
>
>如果您使用Forms以外的自訂Web應用程式為使用者提供工作的存取權，您必須改用適合您自訂應用程式的URL格式。

### 變數選取器 {#variable-picker}

「變數選取器」清單提供有用的變數，您可以將其拖放至「主旨」或「通知範本」方塊中。 將變數放入「主旨」或「通知範本」方塊時，變數會變更為實際表單工作流程變數名稱，其兩側會有兩個@符號，例如`@@taskid@@`。

對於使用者和群組的提醒、任務指派和截止日期，您可以在「主旨」和「通知範本」方塊中使用下列變數：

**說明**&#x200B;說明屬性的內容，如Workbench中處理序的使用者步驟（起點、指派工作作業或指派多重工作作業）中所定義。

**指示**&#x200B;工作指示屬性的內容，如Workbench中處理序的使用者步驟中所定義。

**notification-host** AEM forms應用程式伺服器的主機名稱。

**process-name**&#x200B;處理序的名稱。

**operation-name**&#x200B;步驟的名稱。

**taskid**&#x200B;目前工作的唯一識別碼。

**動作**&#x200B;產生收件者可點按的有效路由的編號清單（例如，核准、拒絕）。

此外，對於群組提醒、群組任務指派和群組截止日期，您也可以使用：

**group-name**&#x200B;指派工作專案的群組名稱。

>[!NOTE]
>
>如果變數沒有值，則不會傳回任何專案。

對於已停止的分支，您可以在「主旨」和「通知範本」方塊中使用下列變數：

**branch-id**&#x200B;分支識別碼。

**process-id**&#x200B;處理序執行個體識別碼。

**notification-host** AEM forms應用程式伺服器的主機名稱。

對於已停止的作業，您可以在「主旨」和「通知範本」方塊中使用下列變數：

**action-id**&#x200B;作業識別碼。

**branch-id**&#x200B;分支識別碼。

**process-id**&#x200B;處理序執行個體識別碼。

**notification-host** AEM forms應用程式伺服器的主機名稱。

### 在主旨方塊中使用變數 {#using-a-variable-in-the-subject-box}

如果您在「工作分派」通知的「主旨」方塊中輸入下列文字：

`Please complete task @@taskid@@`

如果使用者被指派任務376，則使用者會收到一封包含以下主旨的電子郵件訊息：

`Please complete task 376`

### 在通知範本方塊中使用變數 {#using-variables-in-the-notification-template-box}

如果您在「通知範本」方塊中針對「已停止的分支」通知鍵入下列文字：

`Branch @@branch-id@@ has stalled! You have received this notification from @@notification-host@@.`

如果分支編號為4868且伺服器名稱為`ServerXYZ`，則管理員會收到包含下列內容的電子郵件訊息：

`Branch 4868 has stalled! You have received this notification from ServerXYZ.`

## 設定商務活動監視連線 {#configuring-business-activity-monitoring-connections}

業務活動監控是選用的模組，提供一組營運儀表板，可即時顯示您的營運情況和關鍵績效指標。

在「BAM組態設定」頁面中，您可以設定與執行BAM之伺服器的連線，以便可以追蹤與程式相關的事件並將其傳輸至該伺服器。

1. 在管理控制檯中，按一下「服務> Forms工作流程>伺服器設定> BAM組態設定」。
1. 在「BAM主機」方塊中，輸入執行BAM的伺服器名稱。 預設值為localhost。
1. 在「BAM連線埠」方塊中，輸入用來連線至執行BAM之伺服器的連線埠。 JBoss的預設BAM連線埠是8080、WebLogic是7001、WebSphere是9080。
1. 在「伺服器主機」方塊中，輸入主機Forms伺服器的名稱或IP位址。 預設值為localhost。
1. 在「伺服器連線埠」方塊中，輸入Forms伺服器使用的連線埠號碼。
1. 在「使用者名稱」與「密碼」方塊中，輸入適當的使用者ID與密碼以存取「BAM伺服器」。 預設使用者名稱為CognosNowAdmin，預設密碼為manager。
1. 按一下「儲存」。
