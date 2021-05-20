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
exl-id: ed494922-3e15-4778-84c1-35c8846ce980
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 1%

---

# 啟用的初始設定{#initial-setup-for-enablement}

## 啟動製作和發佈執行個體{#start-author-and-publish-instances}

為了開發和展示用途，必須執行一個製作和一個發佈例項。

請依照基本的AEM [快速入門](../../help/sites-deploying/deploy.md#getting-started)指示操作，這會導致

* [localhost:4502](http://localhost:4502/)上的製作環境
* 在[localhost:4503](http://localhost:4503/)上發佈環境

對於AEM Communities,

* 製作環境適用於：

   * 開發網站、範本、元件、啟用資源和學習路徑。
   * 為啟用資源和學習路徑分配成員和成員組。
   * 產生指派、檢視和貼文的報表。
   * 管理和配置任務。

* 發佈環境適用於：

   * 根據培訓管理員管理的主題進行學習/培訓。
   * 註解和評等啟用資源和學習路徑。
   * 與資源聯繫人聯繫。

>[!NOTE]
>
>若不熟悉AEM，請檢視[basic handling](../../help/sites-authoring/basic-handling.md)和[製作頁面快速指南](../../help/sites-authoring/qg-page-authoring.md)的相關檔案。

## 安裝最新的Communities版本{#install-latest-communities-release}

本教學課程會建立[啟用社群網站](overview.md#enablement-community)。 若要確認已安裝最新的Feature Pack，請造訪：

* [最新發行](deploy-communities.md#latest-releases)

如需建立[參與社群網站](overview.md#engagement-community)的教學課程，請造訪[AEM Communities快速入門](getting-started.md)。

## 配置啟用功能{#configure-enablement-features}

若要遵循本教學課程，必須正確安裝和[設定啟用](enablement.md)，這需要第三方產品，例如MySQL和FFmpeg。

## 設定 Analytics {#configure-analytics}

為社群網站](analytics.md)設定[Adobe Analytics時，[reports](reports.md)中會針對指派給社群成員（學習者）的啟用資源和學習路徑產生更多資訊，

## 配置通知的電子郵件{#configure-email-for-notifications}

預設情況下，使用`Communities Sites`控制台建立的所有網站都可使用通知功能，可提供通知的電子郵件通道。

必須為網站正確設定電子郵件。

請參閱[設定電子郵件](email.md)。

## 啟用通道服務{#enable-the-tunnel-service}

在製作環境中建立社群網站時，通道服務可讓您建立和管理在發佈環境中註冊的使用者和使用者群組（成員）、將角色指派給受信任的社群成員，以及將內容指派給使用者。

如需詳細資訊，請參閱[管理使用者和使用者群組](users.md)。

有關啟用隧道服務的簡單說明，請參閱[隧道服務](deploy-communities.md#tunnel-service-on-author)。

## 建立教學課程標籤{#create-tutorial-tags}

使用`Tutorial`的標籤命名空間，建立要用於參與和啟用教學課程的標籤。

使用[標籤控制台](../../help/sites-administering/tags.md#tagging-console)建立以下標籤：

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![教學課程 — 標籤](assets/tutorial-tags.png)

然後，請依照以下指示操作：

1. [設定標籤權限](../../help/sites-administering/tags.md#setting-tag-permissions)
1. [發佈標籤](../../help/sites-administering/tags.md#publishing-tags)

為AEM Communities快速入門Tutorials建立的標籤範例套件

[取得檔案](assets/communities_tutorialtags-10.zip)

## 建立啟用成員和組{#create-enablement-members-and-groups}

對於啟用社群網站，網站訪客不應能[自行註冊或使用社交登入](sites-console.md#user-management)。

反之，啟用[tunnel服務](#enable-the-tunnel-service)後，[成員控制台](members.md)將用於在發佈環境中註冊新成員。

在本教學課程中，會在發佈環境中建立三個成員。 兩個成員將成為指派給學習路徑的使用者群組的成員，而第三個成員將成為啟用資源連絡人。

第四個使用者是在製作環境中建立，並指派給Communities管理員和Communities啟用管理員的角色。

>[!NOTE]
>
>這些成員是在建立&#x200B;*啟用教程*&#x200B;社區站點之前建立的。
>
>如果在之後建立，則可在成員建立期間將它們添加為&#x200B;*啟用教程成員組*&#x200B;的成員。
>
>相反，稍後，它們將[分配給成員組](enablement-create-site.md#assignuserstocommunityenablemembersgroup)。

### 萊利·泰勒 — 登記者{#riley-taylor-enrollee}

[建立](members.md#create-new-member) 會加入一組學習者的成員 — 社群滑雪課組。

* **ID**:萊利
* **電子郵件**:riley.taylor@mailinator.com
* **密碼**:密碼
* **確認密碼**:密碼
* **名字**:萊利
* **姓氏**:泰勒

### Sidney Croft — 登記人{#sidney-croft-enrollee}

[建立將](members.md#create-new-member) 添加到社區滑雪班組的第二個成員。

* **ID**:西德尼
* **電子郵件**:sidney.croft@mailinator.com
* **密碼**:密碼
* **確認密碼**:密碼
* **名字**:西德尼
* **姓氏**:克羅夫特

### Quinn Harper — 培訓資源聯繫人和主持人{#quinn-harper-enablement-resource-contact-and-moderator}

[建立](members.md#create-new-member) 成員，在建立站點後，將其添加到社區站點的成員組中。為站點建立啟用資源時，此成員資格將允許將成員分配為啟用[資源聯繫人](resources.md#settings)。

* **ID**:奎恩
* **電子郵件**:quinn.harper@mailinator.com
* **密碼**:密碼
* **確認密碼**:密碼
* **名字**:奎恩
* **姓氏**:哈珀

### 添加用戶組 — 社區滑雪類{#add-a-user-group-community-ski-class}

[添加名為「社](members.md#create-new-group) 區滑雪課」的新組。

* **ID**:社區 — 滑雪級
* **名稱**:社區滑雪班
* **說明**:用於分配啟用資源的示例組
* **將成員添加到組** 「添加」：

   * 萊利
   * 西德尼

* 選擇&#x200B;**[!UICONTROL 保存]**

### 社區滑雪類屬性{#community-ski-class-properties}

![ski-class-properties](assets/ski-class-properties.png)

>[!NOTE]
>
>在建立社區站點期間，可將現有成員和組添加到社區站點的成員組。

## 社區管理員角色{#community-administrator-role}

社區管理員組的成員可以建立社區站點、管理站點、管理成員（他們可以禁止社區中的成員），以及審核內容。

### 建立使用者 {#create-user}

在&#x200B;*author*&#x200B;上建立被分配了社區管理員角色的用戶：

* 在製作例項上

   * 例如， [http://localhost:4502/](http://localhost:4503/)

* 以管理員權限登入

   * 例如，使用者名稱&#39;admin&#39; /密碼&#39;admin&#39;

* 從主控台，導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 安全性]** > **[!UICONTROL 使用者]**。
* 從&#x200B;**[!UICONTROL Edit]**&#x200B;菜單中，選擇&#x200B;**[!UICONTROL Add User]**。

* 在`Create New User`對話方塊中，輸入：

   * **ID&amp;A;**:天狼星
   * **電子郵件地址**:sirius.nilson@mailinator.com
   * **密碼(&amp;A);**:密碼
   * **確認密碼(&amp;A);**:密碼
   * **名字**:西里烏
   * **姓氏(&amp;A);**:尼爾森

### 將Sirius分配給社區管理員組{#assign-sirius-to-community-administrators-group}

向下捲動至`Add User to Groups`:

* 輸入&#39;C&#39;以搜索

   * 選取 `Community Administrators`
   * 選取 `Community Enablement Managers`

* 選擇&#x200B;**[!UICONTROL 保存]**

![管理員 — 角色](assets/admin-role.png)
