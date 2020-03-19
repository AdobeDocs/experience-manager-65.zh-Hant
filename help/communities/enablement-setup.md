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
source-git-commit: d6c8bbb9aa763a2eb6660b6b6755aba75241e394

---


# 啟用的初始設定 {#initial-setup-for-enablement}

## 啟動作者和發佈例項 {#start-author-and-publish-instances}

為了開發和展示，必須執行一個作者和一個發佈執行個體。

請依照基本的AEM [快速入門](../../help/sites-deploying/deploy.md#getting-started) (Getting Started)指示進行，以產生

* localhost:4502上的 [作者環境](http://localhost:4502/)
* localhost:4503上 [的發佈環境](http://localhost:4503/)

對於AEM Communities,

* 作者環境適用於

   * 開發網站、範本、元件、實作資源和學習途徑
   * 將成員和成員組分配給啟用資源和學習路徑
   * 產生指派、檢視和貼文的報表
   * 管理和配置任務

* 發佈環境適用於

   * 根據由啟用管理員管理的主題進行學習／培訓
   * 註解與評分啟用資源與學習途徑
   * 與資源聯繫人聯繫

>[!NOTE]
>
>如果不熟悉AEM，請檢視基本處理 [相關檔案](../../help/sites-authoring/basic-handling.md) ，以 [及製作頁面的快速指南](../../help/sites-authoring/qg-page-authoring.md)。

## 安裝最新的Communities版本 {#install-latest-communities-release}

本教學課程會建立 [啟用社群網站](overview.md#enablement-community)。 若要確保已安裝最新的功能套件，請造訪：

* [最新版本](deploy-communities.md#latest-releases)

如需建立參與社群網 [站的教學課程](overview.md#engagement-community)，請 [造訪「AEM社群快速入門」](getting-started.md)。

## 設定啟用功能 {#configure-enablement-features}

要遵循本教學課程，必須正確安裝和 [設定啟用](enablement.md)，這需要協力廠商產品，例如MySQL和FFmpeg。

## 設定 Analytics {#configure-analytics}

為社 [群網站設定Adobe Analytics時](analytics.md)[](reports.md) ，會在針對指派給社群成員（學員）的啟用資源和學習路徑產生的報告中提供更多資訊。

## 設定電子郵件通知 {#configure-email-for-notifications}

通知功能預設適用於使用主控台建立的所有網站， `Communities Sites` 提供電子郵件通知管道。

必須為網站正確設定電子郵件。

請參閱 [設定電子郵件](email.md)。

## 啟用隧道服務 {#enable-the-tunnel-service}

在作者環境中建立社群網站時，通道服務可讓您建立和管理在發佈環境（成員）中註冊的使用者和使用者群組、將角色指派給受信任的社群成員，以及將內容指派給學員。

如需詳細資訊，請 [參閱管理使用者和使用者群組](users.md)。

有關啟用隧道服務的簡單說明，請參 [閱隧道服務](deploy-communities.md#tunnel-service-on-author)。

## 建立教學課程標籤 {#create-tutorial-tags}

使用的標籤命名空間，建立要用於參與與啟用教學課程的標籤 `Tutorial`。

使用「標 [記控制台](../../help/sites-administering/tags.md#tagging-console) 」來建立下列標籤：

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![chlimage_1-417](assets/chlimage_1-417.png)

然後依照指示，

1. [設定標籤權限](../../help/sites-administering/tags.md#setting-tag-permissions)
1. [發佈標籤](../../help/sites-administering/tags.md#publishing-tags)

為AEM Communities快速入門教學課程所建立的標籤範例套件

[取得檔案](assets/communities_tutorialtags-10.zip)

## 建立啟用成員和群組 {#create-enablement-members-and-groups}

對於啟用社群網站，網站訪客不應能夠自 [行註冊或使用社交登入](sites-console.md#user-management)。

相反，在啟用 [通道服務後](#enable-the-tunnel-service) ,「成 [](members.md) 員」控制台用於在發佈環境中註冊新成員。

在本教學課程中，會在發佈環境中建立三個成員。 兩個成員將成為指派給學習路徑的使用者群組的成員，而第三個成員將成為啟用資源聯絡人。

第四個用戶是在作者環境中建立的，並分配了「社區管理員」和「社區支援管理員」的角色。

>[!NOTE]
>
>這些成員是在建立啟用教學課程社群網站 *之前建立* 的。
>
>如果在建立後建立了這些成員，則可在建立成員期間將其添加 *為啟用教程成員* 組的成員。
>
>但是，稍後會將其指 [派給成員群組](enablement-create-site.md#assignuserstocommunityenablemembersgroup)。

### Riley Taylor —— 註冊人 {#riley-taylor-enrollee}

[建立將新增至](members.md#create-new-member) 「學員」群組（社群滑雪課程群組）的成員。

* **ID**:賴萊
* **電子郵件**:riley.taylor@mailinator.com
* **密碼**:密碼
* **確認密碼**:密碼
* **名字**:萊利
* **姓氏**:泰勒

### Sidney Croft —— 註冊人 {#sidney-croft-enrollee}

[建立將添加到](members.md#create-new-member) 「社區滑雪類」組的第二個成員。

* **ID**:西德尼
* **電子郵件**:sidney.croft@mailinator.com
* **密碼**:密碼
* **確認密碼**:密碼
* **名字**:西德尼
* **姓氏**:克羅夫特

### Quinn Harper —— 啟用資源聯絡與協調人 {#quinn-harper-enablement-resource-contact-and-moderator}

[建立成員](members.md#create-new-member) ，在建立該站點後，該成員將添加到社區站點的成員組。 此會籍可讓會員在為網站建立啟用資源時， [被指派為啟用資源連絡人](resources.md#settings) 。

* **ID**:奎恩
* **電子郵件**:quinn.harper@mailinator.com
* **密碼**:密碼
* **確認密碼**:密碼
* **名字**:奎恩
* **姓氏**:哈珀

### 新增使用者群組——社群滑雪課程 {#add-a-user-group-community-ski-class}

[新增名為](members.md#create-new-group) Community Ski Class的群組。

* **ID**:社區滑雪課
* **名稱**:社區滑雪課
* **說明**:指派啟用資源的範例群組
* **將成員添加到組** 「添加」:

   * 賴萊
   * 西德尼

* 選擇保 **[!UICONTROL 存]**

### 社區滑雪課屬性 {#community-ski-class-properties}

![chlimage_1-418](assets/chlimage_1-418.png)

>[!NOTE]
>
>在建立社區站點期間，現有成員和組可以添加到社區站點的成員組中。

## 社區管理員角色 {#community-administrator-role}

「社群管理員」群組成員可以建立社群網站、管理網站、管理成員（他們可以禁止社群成員）以及協調內容。

### 建立使用者 {#create-user}

在作者上創 *建*，該用戶被指派為社區管理員：

* 關於作者實例

   * 例如， [http://localhost:4502/](http://localhost:4503/)

* 以管理員權限登入

   * 例如，使用者名稱&#39;admin&#39; /密碼&#39;admin&#39;

* 從主控制台導覽至「工具」、「作 **[!UICONTROL 業>安全性>使用者」]**
* 從「編輯」 **[!UICONTROL 菜單中]** ，選擇「添 **[!UICONTROL 加用戶」]**

* 在對話方 `Create New User` 塊中輸入

   * **ID&amp;ast;**:天狼星
   * **電子郵件地址**:sirius.nilson@mailinator.com
   * **Password&amp;ast;**:密碼
   * **確認密碼&amp;ast;**:密碼
   * **名字**:天狼星
   * **姓氏&amp;ast;**:尼爾森

### 將Sirius指派給社區管理員群組 {#assign-sirius-to-community-administrators-group}

向下捲動至 `Add User to Groups`:

* 輸入&#39;C&#39;以進行搜尋

   * 選取 `Community Administrators`
   * 選取 `Community Enablement Managers`

* 選擇保 **[!UICONTROL 存]**

![chlimage_1-419](assets/chlimage_1-419.png)

