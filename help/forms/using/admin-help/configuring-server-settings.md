---
title: 配置伺服器設定
seo-title: Configuring Server Settings
description: 「伺服器設定」頁面提供對電子郵件、任務通知和管理員通知設定的訪問。
seo-description: The Server Settings page provides access to email, task notification and administrator notification settings.
uuid: 73b51ac0-56e5-4748-bb33-e3986c69eb2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e047a95e-0acb-438a-8d27-f005c0adc508
exl-id: 362b7b91-c58b-4e47-a6ef-56a4b54a100c
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '2625'
ht-degree: 0%

---

# 配置伺服器設定 {#configuring-server-settings}

「伺服器設定」頁面可存取表單工作流程的各種設定：

* **電子郵件設定** 啟用傳出電子郵件訊息，以及用於這些訊息的電子郵件伺服器設定。 (請參閱 [配置電子郵件設定](configuring-server-settings.md#configuring-email-settings).)
* **任務通知設定** 啟用、停用或修改電子郵件通知中傳送給使用者和群組的有關其工作訊息。 (請參閱 [設定使用者和群組的通知](configuring-server-settings.md#configuring-notifications-for-users-and-groups).)
* **管理員通知設定** 啟用、停用或修改管理任務的電子郵件通知中傳送的訊息。 (請參閱 [為管理員配置通知](configuring-server-settings.md#configuring-notifications-for-administrators).)

## 配置電子郵件設定 {#configuring-email-settings}

您可以為表單伺服器指定電子郵件帳戶，透過該帳戶向AEM表單使用者和管理員傳送電子郵件訊息。 這些電子郵件消息用於通知和提醒用戶必須完成的任務，通知用戶已到達最後期限的任務，並通知管理員發生任何進程錯誤。

若要啟用AEM表單與使用者之間傳送電子郵件訊息，請在「電子郵件設定」頁面上設定傳出的電子郵件設定。 傳出電子郵件必須使用SMTP伺服器。

要使AEM表單能夠接收和處理來自用戶的傳入電子郵件，請為「完成任務」服務建立電子郵件端點。 (請參閱 [為完成任務服務建立電子郵件端點](/help/forms/using/admin-help/configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service))。

如果您的程式是設計並實作而不需要電子郵件，則您不需要在「電子郵件設定」頁面上配置任何選項。

### 配置傳出電子郵件設定 {#configure-outgoing-email-settings}

1. 在管理控制台中，按一下「服務>表單工作流程>伺服器設定>電子郵件設定」。
1. 選擇啟用傳出消息。
1. 在「SMTP伺服器」框中，鍵入電子郵件伺服器名稱或IP地址。 來自表單工作流程的所有通知電子郵件訊息都會從此電子郵件伺服器傳送。
1. 在「用戶名」和「密碼」框中，鍵入當SMTP伺服器需要身份驗證時要使用的登錄名和密碼。 如果允許匿名登入，請將它們保留空白。
1. 在「電子郵件地址」方塊中，輸入要作為表單工作流程所傳送之電子郵件訊息的傳回地址的電子郵件地址。

   >[!NOTE]
   >
   >如果您使用Microsoft Exchange Server，且電子郵件地址無效，則Microsoft Exchange Server無法向通訊組清單發送電子郵件。 若要解決問題，請選取 **啟用外部通信** 選項，分別用於Microsoft Exchange伺服器上的每個分送清單。

1. 按一下「儲存」。

>[!NOTE]
>
>如果您輸入的資訊不正確，可以按一下「取消」返回先前顯示的頁面。

### 設定電子郵件範本以使用AEM Forms Workspace {#configuring-email-templates-to-use-html-workspace}

>[!NOTE]
>
>AEM Forms版本已不再使用Flex Workspace。

依預設，AEM表單傳送的電子郵件會包含Flex Workspace的連結(JEE上的AEM表單已過時)。 您可以設定AEM表單以傳送含有AEM Forms Workspace連結的電子郵件。 如需深入了解AEM Forms Workspace優於(JEE上的AEM表單已淘汰)Flex Workspace的優點，請參閱 [此](/help/forms/using/features-html-workspace-available-flex.md) 文章。

1. 在管理控制台中，按一下「首頁」>「服務」>「表單工作流」>「伺服器設定」>「任務通知」。
1. 開啟任務分配模板。
1. 將任務通知中的模板設定為： `https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@`

   ```java
   https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@
   ```

## 設定使用者和群組的通知 {#configuring-notifications-for-users-and-groups}

在「任務通知」頁上，您可以配置表單工作流將用於生成發送到用戶和組的電子郵件通知的模板。 您可以使用表單工作流程變數來自訂通知及設定通知格式。

您可以為使用者和群組設定下列類型的通知：

* 提醒
* 任務分配
* 截止日期

若要產生群組的電子郵件通知，請在「使用者管理」中指定群組的電子郵件地址。 <!--Fix broken link See Setting up and organizing users -->當表單工作流程傳送電子郵件通知至群組時，群組內指定電子郵件地址的每個成員都會收到電子郵件通知。 當組的成員收到電子郵件通知並想申請任務時，該成員必須按一下電子郵件通知中的申請連結，該連結將開啟工作區中的任務詳細資訊頁面。 從那裡，成員可以申請或申請並開啟工作項。

>[!NOTE]
>
>AEM Forms版本已不再使用Flex Workspace。

### 配置用戶或組的提醒 {#configure-reminders-for-users-or-groups}

當完成任務的截止期限即將到來時，您可以向分配的用戶或組發送提醒通知。 用於準確確定何時發送提醒通知的規則由流程開發人員確定。

1. 在管理控制台中，按一下「服務」>「Forms工作流」>「伺服器設定」>「任務通知」。
1. 在「通知類型」下，按一下「提醒（用戶）」或「組 — 提醒（組）」。
1. 選擇啟用提醒或啟用組 — 提醒。
1. （僅限用戶通知）若要將表單的附件及其資料與提醒電子郵件消息一起包含，請選擇「包含表單資料」。
1. 在「主旨」方塊中，輸入電子郵件訊息主旨行的文字。 此欄位已預先填入預設文字。 如需自訂此欄位的詳細資訊，請參閱 [自訂通知內容](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 在「通知範本」方塊中，輸入電子郵件訊息內文的文字。 此欄位已預先填入預設文字。 如需自訂此欄位的詳細資訊，請參閱 [自訂通知內容](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 在「郵件格式」清單中，選擇電子郵件的發送格式，可以是HTML或文本。 預設格式為HTML。
1. 在「電子郵件編碼」清單中，選取用於電子郵件訊息的編碼格式。 預設為UTF-8，日本以外的大部分使用者都會使用。 日本的使用者可選擇ISO2022-JP。
1. 按一下「儲存」。

### 配置用戶或組的任務分配通知 {#configure-task-assignment-notifications-for-users-or-groups}

您可以在用戶或組被分配任務時向其發送任務分配通知。

1. 在管理控制台中，按一下「服務」>「Forms工作流」>「伺服器設定」>「任務通知」。
1. 在「通知類型」下，按一下「用戶的任務分配」或「組 — 組的任務分配」。
1. 選擇「為用戶啟用任務分配」或「為組啟用組 — 任務分配」。
1. （僅限用戶通知）要將表單的附件及其資料與任務分配電子郵件消息一起包含，請選擇「包括表單資料」。
1. 在「主旨」方塊中，輸入電子郵件訊息主旨行的文字。 此欄位已預先填入預設文字。 如需自訂此欄位的詳細資訊，請參閱 [自訂通知內容](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 在「通知範本」方塊中，輸入電子郵件訊息內文的文字。 此欄位已預先填入預設文字。 如需自訂此欄位的詳細資訊，請參閱 [自訂通知內容](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 在「郵件格式」清單中，選擇電子郵件的發送格式，可以是HTML或文本。 預設格式為HTML。
1. 在「電子郵件編碼」清單中，選取用於電子郵件訊息的編碼格式。 預設為UTF-8，日本以外的大部分使用者都會使用。 日本的使用者可選擇ISO2022-JP。
1. 按一下「儲存」。

### 設定使用者或群組的截止通知 {#configure-deadline-notifications-for-users-or-groups}

您可以在指定任務執行作業的截止日期過後，將截止日期通知發送給用戶和組。 期限通知通常是提供資訊的，因為用戶無法再對分配的任務執行操作。

1. 在管理控制台中，按一下「服務」>「Forms工作流」>「伺服器設定」>「任務通知」。
1. 在「通知類型」下，按一下「截止時間（對於用戶）」或「組 — 截止時間（對於組）」。
1. 選擇「啟用截止日期」或「啟用組 — 截止日期」。
1. 在「主旨」方塊中，輸入電子郵件訊息主旨行的文字。 此欄位已預先填入預設文字。 如需自訂此欄位的詳細資訊，請參閱 [自訂通知內容](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 在「通知範本」方塊中，輸入電子郵件訊息內文的文字。 此欄位已預先填入預設文字。 如需自訂此欄位的詳細資訊，請參閱 [自訂通知內容](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 在「郵件格式」清單中，選擇電子郵件的發送格式，可以是HTML或文本。 預設格式為HTML。
1. 在「電子郵件編碼」清單中，選取用於電子郵件訊息的編碼格式。 預設為UTF-8，日本以外的大部分使用者都會使用。 日本的使用者可選擇ISO2022-JP。
1. 按一下「儲存」。

### 隱藏所有電子郵件的DO NOTDELETE標籤 {#hide-the-do-not-delete-tag-for-all-emails}

您可以設定電子郵件，在以人為中心的程式傳送的所有電子郵件中，隱藏至「請勿」DELETE追蹤標籤。

<!-- 
For details, see [How to hide the 'DO-NOT-DELETE' tag with CSS](https://blogs.adobe.com/LiveCycleHelp/2013/09/how-to-hide-the-do-not-delete-tag-with-css.html) 
-->

## 為管理員配置通知 {#configuring-notifications-for-administrators}

您可以設定表單工作流程用來產生傳送給管理員的電子郵件通知的範本。

您可以為管理員配置以下類型的通知：

* 已停止的分支
* 停止的操作

### 設定逾時的分支通知 {#configure-stalled-branch-notifications}

如果分支停止（因故意或錯誤而停止繼續），您可以向管理員或其他用戶發送電子郵件通知，以便他們調查問題。

1. 在管理控制台中，按一下「服務>Forms工作流程>伺服器設定>管理員通知」。
1. 在「通知類型」下，按一下「停止的分支」。
1. 選擇啟用已停止的分支。
1. 在「電子郵件地址」框中，鍵入要在分支停止時通知的用戶地址。 使用user@domain.com格式，並以逗號分隔每個地址。 此電子郵件地址通常是供管理員使用。
1. 在「主旨」方塊中，輸入電子郵件訊息主旨行的文字。 此欄位已預先填入預設文字。 如需自訂此欄位的詳細資訊，請參閱 [自訂通知內容](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 在「通知範本」方塊中，輸入電子郵件訊息內文的文字。 此欄位已預先填入預設文字。 如需自訂此欄位的詳細資訊，請參閱 [自訂通知內容](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 在「郵件格式」清單中，選擇電子郵件的發送格式，可以是HTML或文本。 預設格式為HTML。
1. 在「電子郵件編碼」清單中，選取用於電子郵件訊息的編碼格式。 預設為UTF-8，日本以外的大部分使用者都使用。 日本的使用者可選擇ISO2022-JP。
1. 按一下「儲存」。

### 配置已中止的操作通知 {#configure-stalled-operation-notifications}

如果操作中止（因故意或錯誤而停止繼續），您可以向管理員或其他用戶發送電子郵件通知，以便他們調查問題。

1. 在管理控制台中，按一下「服務>Forms工作流程>伺服器設定>管理員通知」。
1. 在「通知類型」下，按一下「停止的操作」。
1. 選擇「啟用停止的操作」。
1. 在「電子郵件地址」框中，鍵入要在操作中止時通知的用戶地址。 使用user@domain.com格式，並以逗號分隔每個地址。 此電子郵件地址通常是供管理員使用。
1. 在「主旨」方塊中，輸入電子郵件訊息主旨行的文字。 此欄位已預先填入預設文字。 如需自訂此欄位的詳細資訊，請參閱 [自訂通知內容](configuring-server-settings.md#customizing-the-content-of-notifications)
1. 在「通知範本」方塊中，輸入電子郵件訊息內文的文字。 此欄位已預先填入預設文字。 如需自訂此欄位的詳細資訊，請參閱 [自訂通知內容](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 按一下「儲存」。

## 自訂通知內容 {#customizing-the-content-of-notifications}

「任務通知」和「管理員通知」頁提供了幾項功能，使您能夠自定義通知消息：

* RTF編輯器
* 變數選擇器
* URL產生

### RTF編輯器 {#rich-text-editor}

「通知範本」區域是RTF編輯器，可讓您為電子郵件通知訊息產生HTML。 它提供了字型和段落格式選項，可在「通知模板」框下找到。 選項包括字型類型、大小、樣式和顏色，以及段落對齊和項目符號。

### URL產生 {#url-generation}

僅限於「任務通知」，Forms工作流程包含兩個預先定義的URL設定，您可以從「URL產生」清單拖曳至「通知範本」方塊，然後自訂：

* OpenTask可用於提醒和任務分配通知類型。 此URL提供工作區中工作的連結，讓使用者可從電子郵件通知快速存取工作。 將OpenTask URL拖到「通知模板」框時，URL的格式如下：

   `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

* ClaimTask可用於組 — 提醒和組 — 任務分配通知類型。 此URL提供了指向工作區中任務詳細資訊頁面的連結，用戶可以在該頁面中聲明或聲明並開啟工作項。 將ClaimTask URL拖到「通知模板」框時，該URL的格式如下：

   `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

>[!NOTE]
>
>AEM Forms版本已不再使用Flex Workspace。

如果您的解決方案部署在群集環境中，請替換 `@@notification-host@@` 具有群集地址。

`<`*埠* `>` 是應用程式伺服器的HTTP偵聽器的埠號。 支援的應用程式伺服器的預設HTTP偵聽器埠如下：

**JBoss:** 8080

**OracleWebLogic伺服器：** 7001

**IBM WebSphere:** 9080

若要讓這些URL正常運作，請取代 `<`*埠* `>` 具有適合您環境的埠號。

>[!NOTE]
>
>如果您使用Forms以外的自訂Web應用程式來讓使用者存取工作，則必須改用適合自訂應用程式的URL格式。

### 變數選擇器 {#variable-picker}

「變數選擇器」清單提供了一些有用的變數，您可以將它們拖放到「主題」或「通知範本」方塊中。 將變數放置到「主旨」或「通知範本」方塊時，變數會變更為實際的表單工作流程變數名稱，其兩側各有兩個@符號，例如 `@@taskid@@`.

對於用戶和組的提醒、任務分配和截止日期，您可以在「主題」和「通知模板」框中使用以下變數：

**說明** 說明屬性的內容，如Workbench中流程的用戶步驟（起始點、分配任務工序或分配多個任務工序）中所定義。

**說明** 「任務說明」屬性的內容，如Workbench中流程的使用者步驟中所定義。

**notification-host** AEM Forms應用程式伺服器的主機名稱。

**process-name** 進程的名稱。

**operation-name** 步驟的名稱。

**taskid** 當前任務的唯一標識符。

**動作** 生成有效路由的編號清單（例如，批准、拒絕），收件人可以按一下。

此外，對於組提醒、組任務分配和組截止時間，您還可以使用：

**群組名稱** 已分配工作項的組的名稱。

>[!NOTE]
>
>如果變數沒有值，則不會傳回任何內容。

對於逾時的分支，您可以在「主旨」和「通知範本」方塊中使用下列變數：

**branch-id** 分支識別碼。

**process-id** 進程實例標識符。

**notification-host** AEM Forms應用程式伺服器的主機名稱。

對於已停止的操作，您可以在「主旨」和「通知範本」方塊中使用下列變數：

**action-id** 操作標識符。

**branch-id** 分支識別碼。

**process-id** 進程實例標識符。

**notification-host** AEM Forms應用程式伺服器的主機名稱。

### 在「主旨」方塊中使用變數 {#using-a-variable-in-the-subject-box}

如果在「任務分配通知」的「主題」框中鍵入以下文本：

`Please complete task @@taskid@@`

如果被分配任務376，則用戶收到具有以下主題的電子郵件消息：

`Please complete task 376`

### 在通知範本方塊中使用變數 {#using-variables-in-the-notification-template-box}

如果在「已中止的分支」通知的「通知範本」(Notification Template)框中鍵入以下文本：

`Branch @@branch-id@@ has stalled! You have received this notification from @@notification-host@@.`

如果分支號為4868且伺服器名稱為，則管理員會收到包含下列內容的電子郵件 `ServerXYZ`:

`Branch 4868 has stalled! You have received this notification from ServerXYZ.`

## 配置業務活動監視連接 {#configuring-business-activity-monitoring-connections}

業務活動監控是一個可選模組，提供一組操作儀表板，可即時查看您的操作和關鍵績效指標。

在「BAM配置設定」頁上，可以設定與運行BAM的伺服器的連接，以便跟蹤與進程相關的事件並將其傳輸到該伺服器。

1. 在管理控制台中，按一下「服務」>「Forms工作流」>「伺服器設定」>「BAM配置設定」。
1. 在「BAM主機」框中，鍵入運行BAM的伺服器的名稱。 預設為localhost。
1. 在「BAM埠」框中，鍵入用於連接到運行BAM的伺服器的埠。 JBoss的預設BAM埠為8080, WebLogic為7001, WebSphere為9080。
1. 在「伺服器主機」框中，鍵入主機表單伺服器的名稱或IP地址。 預設值為localhost。
1. 在「伺服器埠」框中，鍵入表單伺服器使用的埠號。
1. 在「用戶名」和「密碼」框中，鍵入相應的用戶ID和密碼以訪問BAM伺服器。 預設用戶名為CognosNowAdmin，預設密碼為manager。
1. 按一下「儲存」。
