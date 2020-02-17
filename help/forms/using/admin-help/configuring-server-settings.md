---
title: 配置伺服器設定
seo-title: 配置伺服器設定
description: 「伺服器設定」頁提供對電子郵件、任務通知和管理員通知設定的訪問。
seo-description: 「伺服器設定」頁提供對電子郵件、任務通知和管理員通知設定的訪問。
uuid: 73b51ac0-56e5-4748-bb33-e3986c69eb2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e047a95e-0acb-438a-8d27-f005c0adc508
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 配置伺服器設定 {#configuring-server-settings}

「伺服器設定」頁面可讓您存取表單工作流程的各種設定：

* **啟用傳出電子郵件** 、電子郵件伺服器設定，以及用於這些訊息的電子郵件伺服器設定。 (請參 [閱設定電子郵件設定](configuring-server-settings.md#configuring-email-settings)。)
* **任務通知設定** ，用於啟用、禁用或修改在電子郵件通知中發送給最終用戶和組的與其任務相關的消息。 (請參 [閱設定使用者和群組的通知](configuring-server-settings.md#configuring-notifications-for-users-and-groups)。)
* **管理員通知設定** ，可啟用、停用或修改管理工作的電子郵件通知中傳送的訊息。 (請參 [閱設定管理員通知](configuring-server-settings.md#configuring-notifications-for-administrators)。)

## 設定電子郵件設定 {#configuring-email-settings}

您可以為表單伺服器指定電子郵件帳戶，透過該帳戶將電子郵件訊息傳送給AEM表單使用者和管理員。 這些電子郵件訊息可用來通知和提醒使用者必須完成的工作、通知使用者已到達期限的工作，以及通知管理員發生任何程式錯誤。

若要啟用AEM表單和使用者之間傳送電子郵件訊息，請在「電子郵件設定」頁面上設定傳出的電子郵件設定。 傳出電子郵件必須使用SMTP伺服器。

若要讓AEM表單接收和處理使用者傳入的電子郵件訊息，請為「完成工作」服務建立電子郵件端點。 (請參 [閱為「完成任務」服務建立電子郵件端點](/help/forms/using/admin-help/configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service))。

如果您的流程是設計並實作而不需要透過電子郵件，您就不需要在「電子郵件設定」頁面上設定任何選項。

### 設定傳出電子郵件設定 {#configure-outgoing-email-settings}

1. 在管理主控台中，按一下「服務>表單工作流程>伺服器設定>電子郵件設定」。
1. 選擇「啟用傳出消息」。
1. 在「SMTP伺服器」框中，鍵入電子郵件伺服器名或IP地址。 來自表單工作流程的所有通知電子郵件訊息都會從此電子郵件伺服器傳送。
1. 在「用戶名」和「密碼」框中，鍵入在SMTP伺服器需要驗證時要使用的登錄名和密碼。 如果允許匿名登入，請將其留空。
1. 在「電子郵件地址」方塊中，輸入要作為表單工作流程傳送之電子郵件回傳地址的電子郵件地址。

   >[!NOTE]
   >
   >如果您使用Microsoft Exchange Server且電子郵件地址是無效的電子郵件地址，則Microsoft exchange伺服器無法向分發清單發送電子郵件。 要解決此問題，請為Microsoft exchange服務 **器上的每個分發清單分別選擇「啟用外部通信** 」選項。

1. 按一下「儲存」。

>[!NOTE]
>
>如果輸入了不正確的資訊，可以按一下「取消」返回先前顯示的頁面。

### 設定電子郵件範本以使用AEM Forms Workspace {#configuring-email-templates-to-use-html-workspace}

>[!NOTE]
>
>AEM表單版本已停用Flex Workspace。

依預設，AEM表單傳送的電子郵件包含（JEE上的AEM表單已過時）Flex工作區的連結。 您可以設定AEM表格，以傳送含有AEM表格工作區連結的電子郵件。 若要進一步瞭解AEM Forms Workspace的優點，而非（JEE上的AEM Forms已過時）Flex Workspace，請參閱 [本](/help/forms/using/features-html-workspace-available-flex.md) 文。

1. 在管理控制台中，按一下「首頁>服務>表單工作流程>伺服器設定>工作通知」。
1. 開啟任務分配模板。
1. 將任務通知中的模板設定為： `https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@`

   ```as3
   https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@
   ```

## 設定使用者和群組的通知 {#configuring-notifications-for-users-and-groups}

在「任務通知」頁面上，您可以設定表單工作流程用來產生傳送給使用者和群組的電子郵件通知的範本。 您可以使用表單工作流程變數來自訂通知並設定通知的格式。

您可以為使用者和群組設定下列類型的通知：

* 提醒
* 任務分配
* 期限

若要產生群組的電子郵件通知，請在「使用者管理」中指定群組的電子郵件地址。 <!--Fix broken link See Setting up and organizing users -->當表單工作流程傳送電子郵件通知給群組時，群組內指定電子郵件地址的每位成員都會收到電子郵件通知。 當群組成員收到電子郵件通知並想要申請該任務時，該成員必須按一下電子郵件通知中的報銷申請連結，此連結會在「工作區」中開啟任務詳細資訊頁面。 從那裡，成員可以主張或主張並開啟工作項目。

>[!NOTE]
>
>AEM表單版本不建議使用Flex Workspace。

### 設定使用者或群組的提醒 {#configure-reminders-for-users-or-groups}

當完成任務的期限即將到來時，您可以傳送提醒通知給已指派的用戶或組。 用於確切確定何時發送提醒通知的規則由流程開發者確定。

1. 在管理控制台中，按一下「服務>表單工作流程>伺服器設定>工作通知」。
1. 在「通知類型」下，按一下「提醒（使用者）」或「群組——提醒（群組）」。
1. 選擇啟用提醒或啟用群組——提醒。
1. （僅限使用者通知）若要將表單的附件及其資料加入提醒電子郵件訊息，請選取「包含表單資料」。
1. 在「主旨」方塊中，輸入電子郵件訊息主旨行的文字。 此欄位會預先填入預設文字。 如需自訂此欄位的詳細資訊，請參 [閱自訂通知的內容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在「通知範本」方塊中，輸入電子郵件內文的文字。 此欄位會預先填入預設文字。 如需自訂此欄位的詳細資訊，請參 [閱自訂通知的內容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在「訊息格式」清單中，選取電子郵件訊息的傳送格式（HTML或文字）。 預設格式為HTML。
1. 在「電子郵件編碼」清單中，選取要用於電子郵件訊息的編碼格式。 預設值為UTF-8，大部分日本以外的使用者都會使用它。 日本的使用者可以選擇ISO2022-JP。
1. 按一下「儲存」。

### 為用戶或組配置任務分配通知 {#configure-task-assignment-notifications-for-users-or-groups}

您可以在指派任務時，將任務分配通知發送給用戶或組。

1. 在管理控制台中，按一下「服務>表單工作流程>伺服器設定>工作通知」。
1. 在「通知類型」下，按一下「用戶的任務分配」或「組——組的任務分配」。
1. 選擇「為用戶啟用任務分配」或「為組啟用組——為組分配任務」。
1. （僅限用戶通知）要將表單的附件及其資料包含在任務分配電子郵件消息中，請選擇「包括表單資料」。
1. 在「主旨」方塊中，輸入電子郵件訊息主旨行的文字。 此欄位會預先填入預設文字。 如需自訂此欄位的詳細資訊，請參 [閱自訂通知的內容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在「通知範本」方塊中，輸入電子郵件內文的文字。 此欄位會預先填入預設文字。 如需自訂此欄位的詳細資訊，請參 [閱自訂通知的內容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在「訊息格式」清單中，選取電子郵件訊息的傳送格式（HTML或文字）。 預設格式為HTML。
1. 在「電子郵件編碼」清單中，選取要用於電子郵件訊息的編碼格式。 預設值為UTF-8，大部分日本以外的使用者都會使用它。 日本的使用者可以選擇ISO2022-JP。
1. 按一下「儲存」。

### 設定使用者或群組的期限通知 {#configure-deadline-notifications-for-users-or-groups}

您可以在指定任務的期限過後，將期限通知發送給用戶和組。 期限通知通常是提供資訊的，因為用戶無法再對分配的任務執行操作。

1. 在管理控制台中，按一下「服務>表單工作流程>伺服器設定>工作通知」。
1. 在「通知類型」下，按一下「期限（使用者）」或「群組——期限（群組）」。
1. 選擇「啟用期限」或「啟用組——期限」。
1. 在「主旨」方塊中，輸入電子郵件訊息主旨行的文字。 此欄位會預先填入預設文字。 如需自訂此欄位的詳細資訊，請參 [閱自訂通知的內容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在「通知範本」方塊中，輸入電子郵件內文的文字。 此欄位會預先填入預設文字。 如需自訂此欄位的詳細資訊，請參 [閱自訂通知的內容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在「訊息格式」清單中，選取電子郵件訊息的傳送格式（HTML或文字）。 預設格式為HTML。
1. 在「電子郵件編碼」清單中，選取要用於電子郵件訊息的編碼格式。 預設值為UTF-8，大部分日本以外的使用者都會使用它。 日本的使用者可以選擇ISO2022-JP。
1. 按一下「儲存」。

### 隱藏所有電子郵件的DO NOT DELETE標籤 {#hide-the-do-not-delete-tag-for-all-emails}

您可以在以人為中心的流程中傳送的所有電子郵件中，將電子郵件設定為隱藏至「不刪除」追蹤標籤。 如需詳細資訊， [請參閱如何使用CSS隱藏&#39;DO-NOT-DELETE&#39;標籤](https://blogs.adobe.com/LiveCycleHelp/2013/09/how-to-hide-the-do-not-delete-tag-with-css.html)

## 為管理員配置通知 {#configuring-notifications-for-administrators}

您可以設定表單工作流程用來產生傳送給管理員的電子郵件通知的範本。

您可為管理員設定下列類型的通知：

* 停止分支
* 停止運行

### 配置停滯的分支通知 {#configure-stalled-branch-notifications}

如果分支停止（故意停止或因為錯誤而停止），您可以向管理員或其他用戶發送電子郵件通知，讓他們調查問題。

1. 在管理控制台中，按一下「服務>表單工作流程>伺服器設定>管理員通知」。
1. 在「通知類型」下，按一下「停止的分支」。
1. 選擇「啟用停止的分支」。
1. 在「電子郵件地址」方塊中，輸入分支停止時要通知的使用者地址。 使用user@domain.com格式，並以逗號分隔每個位址。 通常，此電子郵件地址是供管理員使用。
1. 在「主旨」方塊中，輸入電子郵件訊息主旨行的文字。 此欄位會預先填入預設文字。 如需自訂此欄位的詳細資訊，請參 [閱自訂通知的內容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在「通知範本」方塊中，輸入電子郵件內文的文字。 此欄位會預先填入預設文字。 如需自訂此欄位的詳細資訊，請參 [閱自訂通知的內容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在「訊息格式」清單中，選取電子郵件訊息的傳送格式（HTML或文字）。 預設格式為HTML。
1. 在「電子郵件編碼」清單中，選取要用於電子郵件訊息的編碼格式。 預設值為UTF-8，日本以外的大部分使用者都使用它。 日本的使用者可以選擇ISO2022-JP。
1. 按一下「儲存」。

### 配置停止的操作通知 {#configure-stalled-operation-notifications}

如果某個操作停止（故意停止或因為錯誤而停止），您可以向管理員或其他用戶發送電子郵件通知，讓他們調查問題。

1. 在管理控制台中，按一下「服務>表單工作流程>伺服器設定>管理員通知」。
1. 在「通知類型」下，按一下「停止操作」。
1. 選擇「啟用停止的操作」。
1. 在「電子郵件地址」方塊中，輸入作業停止時要通知的使用者地址。 使用user@domain.com格式，並以逗號分隔每個位址。 通常，此電子郵件地址是供管理員使用。
1. 在「主旨」方塊中，輸入電子郵件訊息主旨行的文字。 此欄位會預先填入預設文字。 如需自訂此欄位的詳細資訊，請參 [閱自訂通知的內容](configuring-server-settings.md#customizing-the-content-of-notifications)
1. 在「通知範本」方塊中，輸入電子郵件內文的文字。 此欄位會預先填入預設文字。 如需自訂此欄位的詳細資訊，請參 [閱自訂通知的內容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 按一下「儲存」。

## 自訂通知內容 {#customizing-the-content-of-notifications}

「任務通知」和「管理員通知」頁提供了幾種功能，使您能夠自定義通知消息：

* 豐富式文字編輯器
* 變數選擇器
* URL產生

### Rich text editor {#rich-text-editor}

「通知範本」區域是多樣化文字編輯器，可讓您產生電子郵件通知訊息的HTML。 它提供字型和段落格式選項，這些選項位於「通知範本」方塊下方。 選項包括字型類型、大小、樣式和顏色，以及段落對齊方式和項目符號。

### URL產生 {#url-generation}

僅適用於「任務通知」,「表單」工作流程包含兩個預先定義的URL設定，您可將其從「URL產生」清單拖曳至「通知範本」方塊，然後自訂：

* OpenTask可用於提醒和任務分配通知類型。 此URL提供工作區中工作的連結，讓使用者可從電子郵件通知快速存取工作。 將OpenTask URL拖到「通知模板」框時，URL的格式如下：

   `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

* ClaimTask可用於「組——提醒和組——任務分配」通知類型。 此URL提供Workspace中任務詳細資訊頁面的連結，用戶可以在該頁中聲明或聲明並開啟工作項目。 將ClaimTask URL拖動到「通知模板」框時，URL的格式如下：

   `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

>[!NOTE]
>
>AEM表單版本不建議使用Flex Workspace。

如果解決方案部署在叢集環境中，請以叢集 `@@notification-host@@` 位址取代。

`<`*PORT *是應用`>`程式伺服器的HTTP偵聽器的埠號。 支援的應用程式伺服器的預設HTTP偵聽器埠如下：

**** JBoss:郵遞區號8080

**** Oracle webLogic Server:郵編：7001

**** IBM webSphere:郵遞區號9080

要使這些URL正常運作，請 `<`*用適&#x200B;*合您環境的埠號替換PORT`>`。

***注意&#x200B;**:如果您使用Forms以外的自訂Web應用程式來讓使用者存取工作，則必須改用適合您自訂應用程式的URL格式。*

### 可變選擇器 {#variable-picker}

「變數選擇器」清單提供有用的變數，您可將這些變數拖放至「主旨」或「通知範本」方塊中。 將變數拖放至「主旨」或「通知範本」方塊時，變數會變更為實際的表單工作流程變數名稱，其兩側會有兩個@符號 `@@taskid@@`。

如需使用者和群組的提醒、工作指派和期限，您可以在「主旨」和「通知範本」方塊中使用下列變數：

**說明** ：說明屬性的內容，如Workbench中流程的用戶步驟（起始點、分配任務操作或分配多任務操作）中所定義。

**說明** 「任務說明」屬性的內容，如Workbench中流程的用戶步驟中所定義。

**notification-host** AEM forms應用程式伺服器的主機名稱。

**process-name** 流程的名稱。

**operation-name** 步驟的名稱。

**taskid** 當前任務的唯一標識符。

**動作** ：產生收件者可點按之有效路由的編號清單（例如「核准」、「拒絕」）。

此外，對於組提醒、組任務分配和組期限，您還可以使用：

**group-name** 指派工作項目的群組名稱。

**注意**:如 *果變數沒有值，則不會傳回任何內容。*

對於停止的分支，您可以在「主旨」和「通知範本」方塊中使用下列變數：

**branch-id** Branch標識符。

**process-id** 流程實例標識符。

**notification-host** AEM forms應用程式伺服器的主機名稱。

對於停止的操作，您可以在「主題」和「通知模板」框中使用以下變數：

**action-id** 操作標識符。

**branch-id** Branch標識符。

**process-id** 流程實例標識符。

**notification-host** AEM forms應用程式伺服器的主機名稱。

### 在「主旨」方塊中使用變數 {#using-a-variable-in-the-subject-box}

如果在「任務分配通知」的「主題」框中鍵入以下文本：

`Please complete task @@taskid@@`

如果用戶被分配任務376，則會收到包含以下主題的電子郵件消息：

`Please complete task 376`

### 在「通知範本」方塊中使用變數 {#using-variables-in-the-notification-template-box}

如果在「停止的分支」通知的「通知模板」框中鍵入以下文本：

`Branch @@branch-id@@ has stalled! You have received this notification from @@notification-host@@.`

如果分支編號為4868，而伺服器名稱為，則管理員會收到一封包含以下內容的電子郵件 `ServerXYZ`:

`Branch 4868 has stalled! You have received this notification from ServerXYZ.`

## 配置業務活動監視連接 {#configuring-business-activity-monitoring-connections}

Business Activity Monitoring（可選模組）提供一組操作儀表板，可即時查看您的操作和關鍵效能指標。

在「BAM配置設定」頁上，可以設定到運行BAM的伺服器的連接，以便跟蹤進程相關事件並將其發送到該伺服器。

1. 在管理控制台中，按一下「服務」>「表單」工作流>「伺服器設定」>「BAM配置設定」。
1. 在「BAM主機」框中，鍵入運行BAM的伺服器的名稱。 預設值為localhost。
1. 在「BAM埠」框中，鍵入用於連接到運行BAM的伺服器的埠。 JBoss的預設BAM埠為8080,WebLogic為7001,WebSphere為9080。
1. 在「伺服器主機」框中，鍵入主機表單伺服器的名稱或IP地址。 預設值為localhost。
1. 在「伺服器埠」框中，鍵入表單伺服器使用的埠號。
1. 在「用戶名」和「密碼」框中，鍵入相應的用戶ID和密碼以訪問BAM伺服器。 預設用戶名為CognosNowAdmin ，預設密碼為manager。
1. 按一下「儲存」。

