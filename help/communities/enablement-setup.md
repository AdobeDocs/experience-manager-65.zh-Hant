---
title: 啟用的初始設定
seo-title: 初始設定
description: 啟用的初始設定
seo-description: 啟用的初始設定
uuid: 873ec41d-c088-41d9-a535-de5300661de6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: f2ac3d66-cc79-498f-83fb-dd96feb88de2
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 1%

---


# 啟用的初始設定{#initial-setup-for-enablement}

## 啟動作者和發佈例項{#start-author-and-publish-instances}

為了開發和展示，必須執行一個作者和一個發佈執行個體。

請依照基本的AEM [快速入門](../../help/sites-deploying/deploy.md#getting-started)指示進行，以產生

* [localhost:4502](http://localhost:4502/)上的作者環境
* [localhost:4503](http://localhost:4503/)上的發佈環境

對於AEM Communities,

* 作者環境適用於：

   * 開發網站、範本、元件、實施資源和學習途徑。
   * 將成員和成員群組指派給啟用資源和學習路徑。
   * 產生指派、檢視和貼文的報表。
   * 管理和配置任務。

* 發佈環境適用於：

   * 根據啟用管理員管理的主題進行學習／培訓。
   * 註解和評分啟用資源與學習路徑。
   * 與資源聯繫人聯繫。

>[!NOTE]
>
>如果不熟悉AEM，請檢視[基本處理](../../help/sites-authoring/basic-handling.md)和[製作頁面快速指南的說明檔案](../../help/sites-authoring/qg-page-authoring.md)。

## 安裝最新的社區版本{#install-latest-communities-release}

本教學課程會建立[啟用社群網站](overview.md#enablement-community)。 若要確保已安裝最新的功能套件，請造訪：

* [最新版本](deploy-communities.md#latest-releases)

如需建立[參與社群網站](overview.md#engagement-community)的教學課程，請造訪[ AEM Communities](getting-started.md)快速入門。

## 設定啟用功能{#configure-enablement-features}

要遵循本教學課程，必須正確安裝並[設定enablement](enablement.md)，這需要協力廠商產品，例如MySQL和FFmpeg。

## 設定 Analytics {#configure-analytics}

為社群網站[設定](analytics.md)的Adobe Analytics時，[報告](reports.md)會針對指派給社群成員（學員）的啟用資源和學習路徑產生更多資訊。

## 設定電子郵件通知{#configure-email-for-notifications}

通知功能預設適用於使用`Communities Sites`主控台建立的所有網站，提供電子郵件通道以接收通知。

必須為網站正確設定電子郵件。

請參閱[設定電子郵件](email.md)。

## 啟用隧道服務{#enable-the-tunnel-service}

在作者環境中建立社群網站時，通道服務可讓您建立和管理在發佈環境（成員）中註冊的使用者和使用者群組、將角色指派給受信任的社群成員，以及將內容指派給學員。

如需詳細資訊，請參閱[管理使用者和使用者群組](users.md)。

有關啟用隧道服務的簡單說明，請參見[隧道服務](deploy-communities.md#tunnel-service-on-author)。

## 建立教學課程標籤{#create-tutorial-tags}

使用`Tutorial`的標籤命名空間，建立用於吸引與啟用教學課程的標籤。

使用[標籤控制台](../../help/sites-administering/tags.md#tagging-console)建立以下標籤：

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![教學課程標籤](assets/tutorial-tags.png)

然後，請依照指示執行：

1. [設定標籤權限](../../help/sites-administering/tags.md#setting-tag-permissions)
1. [發佈標籤](../../help/sites-administering/tags.md#publishing-tags)

為AEM Communities快速入門教學課程所建立的標籤範例套件

[取得檔案](assets/communities_tutorialtags-10.zip)

## 建立啟用成員和組{#create-enablement-members-and-groups}

對於啟用社群網站，網站訪客不應能夠[自行註冊，也不應使用社交登入](sites-console.md#user-management)。

相反，在[tunnel服務](#enable-the-tunnel-service)啟用後，[成員控制台](members.md)用於在發佈環境中註冊新成員。

在本教學課程中，會在發佈環境中建立三個成員。 兩個成員將成為指派給學習路徑的使用者群組的成員，而第三個成員將成為啟用資源聯絡人。

第四個用戶是在作者環境中建立的，並分配了「社區管理員」和「社區支援管理員」的角色。

>[!NOTE]
>
>這些成員是在建立&#x200B;*啟用教程*&#x200B;社區站點之前建立的。
>
>如果在建立後建立了這些成員，則可在建立成員期間將其添加為&#x200B;*啟用教程成員組*&#x200B;的成員。
>
>但是，稍後將[分配給成員組](enablement-create-site.md#assignuserstocommunityenablemembersgroup)。

### Riley Taylor —— 註冊人{#riley-taylor-enrollee}

[建立會](members.md#create-new-member) 員，將其新增至學員群組——社群滑雪課程群組。

* **ID**:賴萊
* **電子郵件**:riley.taylor@mailinator.com
* **密碼**:密碼
* **確認密碼**:密碼
* **名字**:萊利
* **姓氏**:泰勒

### Sidney Croft —— 註冊人{#sidney-croft-enrollee}

[建立第二個](members.md#create-new-member) 會員，將其新增至社群滑雪課程群組。

* **ID**:西德尼
* **電子郵件**:sidney.croft@mailinator.com
* **密碼**:密碼
* **確認密碼**:密碼
* **名字**:西德尼
* **姓氏**:克羅夫特

### Quinn Harper —— 啟用資源聯絡與協調人{#quinn-harper-enablement-resource-contact-and-moderator}

[建立](members.md#create-new-member) 將在建立站點後添加到社區站點成員組的成員。此會籍可讓會員在為網站建立啟用資源時，被指派為啟用[資源連絡](resources.md#settings)。

* **ID**:奎恩
* **電子郵件**:quinn.harper@mailinator.com
* **密碼**:密碼
* **確認密碼**:密碼
* **名字**:奎恩
* **姓氏**:哈珀

### 新增使用者群組——社群滑雪類別{#add-a-user-group-community-ski-class}

[新增名為社](members.md#create-new-group) 群滑雪課的群組。

* **ID**:社區滑雪課
* **名稱**:社區滑雪課
* **說明**:指派啟用資源的範例群組
* **將成員添加到組** 「添加」:

   * 賴萊
   * 西德尼

* 選擇&#x200B;**[!UICONTROL 保存]**

### 社區滑雪類屬性{#community-ski-class-properties}

![ski-class-properties](assets/ski-class-properties.png)

>[!NOTE]
>
>在建立社區站點期間，現有成員和組可以添加到社區站點的成員組中。

## 社區管理員角色{#community-administrator-role}

「社群管理員」群組成員可以建立社群網站、管理網站、管理成員（他們可以禁止社群成員）以及協調內容。

### 建立使用者 {#create-user}

在&#x200B;*author*&#x200B;上建立一個用戶，該用戶被分配為社區管理員的角色：

* 關於作者實例

   * 例如，[http://localhost:4502/](http://localhost:4503/)

* 以管理員權限登入

   * 例如，使用者名稱&#39;admin&#39; /密碼&#39;admin&#39;

* 從主控制台導航至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 安全]** > **[!UICONTROL 用戶]**。
* 從&#x200B;**[!UICONTROL 編輯]**&#x200B;菜單中，選擇&#x200B;**[!UICONTROL 添加用戶]**。

* 在`Create New User`對話框中，輸入：

   * **ID&amp;ast;**:天狼星
   * **電子郵件地址**:sirius.nilson@mailinator.com
   * **密碼(&amp;A)**:密碼
   * **確認密碼(&amp;A)**:密碼
   * **名字**:天狼星
   * **姓氏(&amp;A)**:尼爾森

### 將Sirius分配給社區管理員組{#assign-sirius-to-community-administrators-group}

向下捲動至`Add User to Groups`:

* 輸入&#39;C&#39;以進行搜尋

   * 選取 `Community Administrators`
   * 選取 `Community Enablement Managers`

* 選擇&#x200B;**[!UICONTROL 保存]**

![admin-role](assets/admin-role.png)

