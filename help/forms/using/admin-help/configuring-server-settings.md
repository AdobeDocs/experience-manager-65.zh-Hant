---
title: 配置伺服器設定
seo-title: Configuring Server Settings
description: 「伺服器設定」頁提供對電子郵件、任務通知和管理員通知設定的訪問。
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

「伺服器設定」頁提供了對表單工作流的各種設定的訪問權限：

* **電子郵件設定** 啟用傳出電子郵件以及用於這些郵件的電子郵件伺服器設定。 (請參閱 [配置電子郵件設定](configuring-server-settings.md#configuring-email-settings)。)
* **任務通知設定** 啟用、禁用或修改通過電子郵件通知發送給最終用戶和組的有關其任務的消息。 (請參閱 [為用戶和組配置通知](configuring-server-settings.md#configuring-notifications-for-users-and-groups)。)
* **管理員通知設定** 啟用、禁用或修改管理任務的電子郵件通知中發送的消息。 (請參閱 [為管理員配置通知](configuring-server-settings.md#configuring-notifications-for-administrators)。)

## 配置電子郵件設定 {#configuring-email-settings}

您可以為表單伺服器指定電子郵件帳戶，通過該帳戶向表單用戶和管AEM理員發送電子郵件。 這些電子郵件用於通知和提醒用戶必須完成的任務、通知用戶已到達最後期限的任務，以及將發生的任何進程錯誤通知管理員。

要啟用表單和用戶之間的電AEM子郵件發送，請在「電子郵件設定」頁上配置傳出電子郵件設定。 傳出電子郵件必須使用SMTP伺服器。

要使表單AEM能夠接收和處理來自用戶的傳入電子郵件，請為「完成任務」服務建立電子郵件終結點。 (請參閱 [為「完成任務」服務建立電子郵件終結點](/help/forms/using/admin-help/configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service))。

如果您的流程是在不需要電子郵件的情況下設計和實施的，則您不必在「電子郵件設定」頁面上配置任何選項。

### 配置傳出電子郵件設定 {#configure-outgoing-email-settings}

1. 在管理控制台中，按一下「服務」>「表單工作流」>「伺服器設定」>「電子郵件設定」。
1. 選擇啟用傳出消息。
1. 在「SMTP伺服器」框中，鍵入電子郵件伺服器名稱或IP地址。 來自表單工作流的所有通知電子郵件都從此電子郵件伺服器發送。
1. 在「用戶名」和「密碼」框中，鍵入SMTP伺服器需要身份驗證時要使用的登錄名和密碼。 如果允許匿名登錄，則將其留空。
1. 在「電子郵件地址」框中，鍵入要用作表單工作流發送的電子郵件的返回地址的電子郵件地址。

   >[!NOTE]
   >
   >如果您使用的是MicrosoftExchange Server，且電子郵件地址是無效的電子郵件地址，則MicrosoftExchange Server無法向通訊組清單發送電子郵件。 要解決此問題，請選擇 **啟用外部通信** 選項。

1. 按一下「儲存」。

>[!NOTE]
>
>如果輸入了錯誤的資訊，可按一下「取消」返回先前顯示的頁面。

### 配置電子郵件模板以使用AEM Forms工作區 {#configuring-email-templates-to-use-html-workspace}

>[!NOTE]
>
>不建議使用Flex工作AEM區來發佈表單。

預設情況下，表單發送的電AEM子郵件包含指向(JEE上的表AEM單已棄用)Flex工作區的連結。 您可以配AEM置表單，以發送帶有指向AEM Forms工作區連結的電子郵件。 要瞭解AEM Forms工作區的優勢(JEE上的表AEM單已棄用)Flex工作區，請參閱 [這個](/help/forms/using/features-html-workspace-available-flex.md) 文章。

1. 在管理控制台中，按一下「首頁」>「服務」>「表單工作流」>「伺服器設定」>「任務通知」。
1. 開啟任務分配模板。
1. 將任務通知中的模板設定為： `https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@`

   ```java
   https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@
   ```

## 為用戶和組配置通知 {#configuring-notifications-for-users-and-groups}

在「任務通知」頁上，可以配置表單工作流將用於生成發送到用戶和組的電子郵件通知的模板。 您可以使用表單工作流變數自定義和格式化通知。

為用戶和組配置以下類型的通知：

* 提醒
* 任務分配
* 截稿

要為組生成電子郵件通知，請在「用戶管理」中為該組指定電子郵件地址。 <!--Fix broken link See Setting up and organizing users -->當表單工作流向組發送電子郵件通知時，指定電子郵件地址的組內的每個成員都會收到電子郵件通知。 當組成員收到電子郵件通知並想聲明任務時，該成員必須按一下電子郵件通知中的聲明連結，該連結將在Workspace中開啟任務詳細資訊頁面。 從那裡，成員可以聲明或聲明並開啟工作項目。

>[!NOTE]
>
>不建議使用Flex工AEM作空間。

### 配置用戶或組的提醒 {#configure-reminders-for-users-or-groups}

在完成任務的截止時間即將到來時，您可以向已分配的用戶或組發送提醒通知。 用於準確確定何時發送提醒通知的規則由過程開發者確定。

1. 在管理控制台中，按一下「服務」>「Forms」工作流>「伺服器設定」>「任務通知」。
1. 在通知類型下，按一下提醒（對於用戶）或組 — 提醒（對於組）。
1. 選擇啟用提醒或啟用組 — 提醒。
1. （僅限用戶通知）要將表單及其資料的附件與提醒電子郵件一起包含，請選擇包括表單資料。
1. 在「主題」框中，鍵入電子郵件主題行的文本。 此欄位預填充了預設文本。 有關自定義此欄位的詳細資訊，請參閱 [自定義通知內容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在「通知模板」框中，鍵入電子郵件正文的文本。 此欄位預填充了預設文本。 有關自定義此欄位的詳細資訊，請參閱 [自定義通知內容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在「郵件格式」清單中，選擇電子郵件的發送格式(HTML或文本)。 預設格式為HTML。
1. 在「電子郵件編碼」清單中，選擇要用於電子郵件的編碼格式。 預設值為UTF-8，大多數日本以外的用戶將使用它。 日本用戶可以選擇ISO2022-JP。
1. 按一下「儲存」。

### 配置用戶或組的任務分配通知 {#configure-task-assignment-notifications-for-users-or-groups}

您可以在分配任務時將任務分配通知發送給用戶或組。

1. 在管理控制台中，按一下「服務」>「Forms」工作流>「伺服器設定」>「任務通知」。
1. 在通知類型下，按一下用戶的任務分配或組 — 組的任務分配。
1. 選擇「為用戶啟用任務分配」或「為組啟用組 — 任務分配」。
1. （僅限用戶通知）要將表單的附件及其資料包含在任務分配電子郵件消息中，請選擇包括表單資料。
1. 在「主題」框中，鍵入電子郵件主題行的文本。 此欄位預填充了預設文本。 有關自定義此欄位的詳細資訊，請參閱 [自定義通知內容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在「通知模板」框中，鍵入電子郵件正文的文本。 此欄位預填充了預設文本。 有關自定義此欄位的詳細資訊，請參閱 [自定義通知內容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在「郵件格式」清單中，選擇電子郵件的發送格式(HTML或文本)。 預設格式為HTML。
1. 在「電子郵件編碼」清單中，選擇要用於電子郵件的編碼格式。 預設值為UTF-8，大多數日本以外的用戶將使用它。 日本用戶可以選擇ISO2022-JP。
1. 按一下「儲存」。

### 配置用戶或組的截止通知 {#configure-deadline-notifications-for-users-or-groups}

當對分配的任務採取行動的截止時間已過時，您可以向用戶和組發送截止通知。 截止時間通知通常是資訊性的，因為用戶無法再對分配的任務執行操作。

1. 在管理控制台中，按一下「服務」>「Forms」工作流>「伺服器設定」>「任務通知」。
1. 在「通知類型」下，按一下「截止時間（對於用戶）」或「組 — 截止時間（對於組）」。
1. 選擇啟用截止時間或啟用組 — 截止時間。
1. 在「主題」框中，鍵入電子郵件主題行的文本。 此欄位預填充了預設文本。 有關自定義此欄位的詳細資訊，請參閱 [自定義通知內容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在「通知模板」框中，鍵入電子郵件正文的文本。 此欄位預填充了預設文本。 有關自定義此欄位的詳細資訊，請參閱 [自定義通知內容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在「郵件格式」清單中，選擇電子郵件的發送格式(HTML或文本)。 預設格式為HTML。
1. 在「電子郵件編碼」清單中，選擇要用於電子郵件的編碼格式。 預設值為UTF-8，大多數日本以外的用戶將使用它。 日本用戶可以選擇ISO2022-JP。
1. 按一下「儲存」。

### 隱藏所有電子郵件的DO NOTDELETE標籤 {#hide-the-do-not-delete-tag-for-all-emails}

您可以將電子郵件配置為隱藏到以人為中心流程發送的所有電子郵件中的「不DELETE」跟蹤標籤。

<!-- 
For details, see [How to hide the 'DO-NOT-DELETE' tag with CSS](https://blogs.adobe.com/LiveCycleHelp/2013/09/how-to-hide-the-do-not-delete-tag-with-css.html) 
-->

## 為管理員配置通知 {#configuring-notifications-for-administrators}

您可以配置表單工作流將用於生成發送到管理員的電子郵件通知的模板。

為管理員配置以下類型的通知：

* 停止的分支
* 停止運行

### 配置停止的分支通知 {#configure-stalled-branch-notifications}

如果分支停止（故意或由於錯誤而停止），您可以向管理員或其他用戶發送電子郵件通知，然後該用戶可以調查問題。

1. 在管理控制台中，按一下「服務」>「Forms」工作流>「伺服器設定」>「管理員通知」。
1. 在「通知類型」(Notification Type)下，按一下「停止的分支」(Stalted Branch)。
1. 選擇「啟用停止的分支」。
1. 在「電子郵件地址」框中，鍵入分支停止時要通知的用戶地址。 使用user@domain.com格式，用逗號分隔每個地址。 通常，此電子郵件地址是管理員的電子郵件地址。
1. 在「主題」框中，鍵入電子郵件主題行的文本。 此欄位預填充了預設文本。 有關自定義此欄位的詳細資訊，請參閱 [自定義通知內容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在「通知模板」框中，鍵入電子郵件正文的文本。 此欄位預填充了預設文本。 有關自定義此欄位的詳細資訊，請參閱 [自定義通知內容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在「郵件格式」清單中，選擇電子郵件的發送格式(HTML或文本)。 預設格式為HTML。
1. 在「電子郵件編碼」清單中，選擇要用於電子郵件的編碼格式。 預設值為UTF-8，大多數日本以外用戶都使用它。 日本用戶可以選擇ISO2022-JP。
1. 按一下「儲存」。

### 配置停止的操作通知 {#configure-stalled-operation-notifications}

如果操作停止（故意或由於錯誤而停止），您可以向管理員或其他用戶發送電子郵件通知，這些用戶可以調查問題。

1. 在管理控制台中，按一下「服務」>「Forms」工作流>「伺服器設定」>「管理員通知」。
1. 在「通知類型」(Notification Type)下，按一下「停止的操作」(Stalted Operation)。
1. 選擇啟用停止的操作。
1. 在「電子郵件地址」框中，鍵入操作停止時要通知的用戶地址。 使用user@domain.com格式，用逗號分隔每個地址。 通常，此電子郵件地址是管理員的電子郵件地址。
1. 在「主題」框中，鍵入電子郵件主題行的文本。 此欄位預填充了預設文本。 有關自定義此欄位的詳細資訊，請參閱 [自定義通知內容](configuring-server-settings.md#customizing-the-content-of-notifications)
1. 在「通知模板」框中，鍵入電子郵件正文的文本。 此欄位預填充了預設文本。 有關自定義此欄位的詳細資訊，請參閱 [自定義通知內容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 按一下「儲存」。

## 自定義通知內容 {#customizing-the-content-of-notifications}

「任務通知」和「管理員通知」頁提供了幾項功能，使您能夠自定義通知消息：

* 富文本編輯器
* 變數選取器
* URL生成

### 富格文本編輯器 {#rich-text-editor}

「通知模板」區域是富格文本編輯器，它使您能夠為電子郵件通知消息生成HTML。 它提供字型和段落格式選項，這些選項位於「通知模板」框下。 選項包括字型類型、大小、樣式和顏色，以及段落對齊和項目符號。

### URL生成 {#url-generation}

僅對於任務通知，Forms工作流包含兩個預定義的URL配置，您可以將它們從「URL生成」清單拖到「通知模板」框中，然後自定義：

* OpenTask可用於提醒和任務分配通知類型。 此URL提供了指向Workspace中任務的連結，允許用戶從電子郵件通知快速訪問該任務。 將OpenTask URL拖至「通知模板」框時，URL的格式如下：

   `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

* ClaimTask可用於組 — 提醒和組 — 任務分配通知類型。 此URL提供指向Workspace中任務詳細資訊頁面的連結，用戶可以在該頁面中聲明或聲明並開啟工作項目。 將ClaimTask URL拖到「通知模板」框時，URL的格式如下：

   `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

>[!NOTE]
>
>不建議使用Flex工AEM作空間。

如果您的解決方案部署在群集環境中，請替換 `@@notification-host@@` 群集地址。

`<`*埠* `>` 是應用程式伺服器的HTTP偵聽器的埠號。 支援的應用程式伺服器的預設HTTP偵聽器埠如下：

**JBoss:** 8080

**OracleWebLogic伺服器：** 7001

**IBM網球：** 9080

要使這些URL正確運行，請替換 `<`*埠* `>` 具有適合您環境的埠號。

>[!NOTE]
>
>如果您使用Forms以外的自定義Web應用程式來為用戶提供訪問任務的權限，則必須改用適用於自定義應用程式的URL格式。

### 可變選取器 {#variable-picker}

「變數選取器」(Variable Picker)清單提供了有用的變數，您可以將這些變數拖放到「主題」(Subject)或「通知模板」(Notification Template)框中。 在「主題」或「通知模板」框中放置變數時，它將更改為實際表單工作流變數名稱，其兩側有兩個@符號，例如， `@@taskid@@`。

對於用戶和組的提醒、任務分配和截止時間，您可以在「主題」和「通知模板」框中使用以下變數：

**描述** Workbench中流程的用戶步驟（起始點、分配任務工序或分配多個任務工序）中定義的「說明」屬性的內容。

**說明** 「任務說明」屬性的內容，如Workbench中流程的用戶步驟中所定義。

**通知主機** Forms應用程式服AEM務器的主機名。

**進程名** 進程的名稱。

**操作名稱** 步驟的名稱。

**小孩** 當前任務的唯一標識符。

**動作** 生成收件人可以按一下的有效路由（例如批准、拒絕）的編號清單。

此外，對於組提醒、組任務分配和組截止時間，您還可以使用：

**組名** 分配了工作項的組的名稱。

>[!NOTE]
>
>如果變數沒有值，則不返回任何內容。

對於已停止的分支，可在「主題」(Subject)和「通知模板」(Notification Template)框中使用以下變數：

**分支ID** 分支標識符。

**進程ID** 進程實例標識符。

**通知主機** Forms應用程式服AEM務器的主機名。

對於已停止的操作，可在「主題」(Subject)和「通知模板」(Notification Template)框中使用以下變數：

**操作ID** 操作標識符。

**分支ID** 分支標識符。

**進程ID** 進程實例標識符。

**通知主機** Forms應用程式服AEM務器的主機名。

### 在「主題」框中使用變數 {#using-a-variable-in-the-subject-box}

如果在「任務分配」通知的「主題」框中鍵入以下文本：

`Please complete task @@taskid@@`

如果用戶被分配了任務376，則該用戶接收具有以下主題的電子郵件：

`Please complete task 376`

### 在「通知模板」框中使用變數 {#using-variables-in-the-notification-template-box}

如果在「已停止的分支」通知的「通知模板」框中鍵入以下文本：

`Branch @@branch-id@@ has stalled! You have received this notification from @@notification-host@@.`

如果分支編號為4868且伺服器名稱為 `ServerXYZ`:

`Branch 4868 has stalled! You have received this notification from ServerXYZ.`

## 配置業務活動監視連接 {#configuring-business-activity-monitoring-connections}

業務活動監控是一個可選模組，它提供了一組操作控制板，可即時查看您的操作和關鍵效能指標。

在「BAM配置設定」頁上，您可以設定到運行BAM的伺服器的連接，以便跟蹤與進程相關的事件並將其發送到該伺服器。

1. 在管理控制台中，按一下「服務」>「Forms」工作流>「伺服器設定」>「BAM配置設定」。
1. 在「BAM主機」框中，鍵入運行BAM的伺服器的名稱。 預設值為localhost。
1. 在「BAM埠」框中，鍵入用於連接到運行BAM的伺服器的埠。 JBoss的預設BAM埠為8080,WebLogic為7001,WebSphere為9080。
1. 在「伺服器主機」框中，鍵入主機表單伺服器的名稱或IP地址。 預設值為localhost。
1. 在「伺服器埠」框中，鍵入表單伺服器使用的埠號。
1. 在「用戶名」和「密碼」框中，鍵入相應的用戶ID和密碼以訪問BAM伺服器。 預設用戶名為CognosNowAdmin，預設密碼為manager。
1. 按一下「儲存」。
