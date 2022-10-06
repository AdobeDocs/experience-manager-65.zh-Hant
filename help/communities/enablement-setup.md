---
title: 啟用的初始設定
seo-title: Initial Setup
description: 啟用的初始設定
seo-description: Initial Setup for Enablement
uuid: 873ec41d-c088-41d9-a535-de5300661de6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: f2ac3d66-cc79-498f-83fb-dd96feb88de2
exl-id: ed494922-3e15-4778-84c1-35c8846ce980
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 1%

---

# 啟用的初始設定  {#initial-setup-for-enablement}

## 啟動製作和發佈例項 {#start-author-and-publish-instances}

為了開發和展示用途，必須執行一個製作和一個發佈例項。

遵循基本AEM [快速入門](../../help/sites-deploying/deploy.md#getting-started) 會導致

* 製作環境 [localhost:4502](http://localhost:4502/)
* 發佈環境於 [localhost:4503](http://localhost:4503/)

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
>如果不熟悉AEM，請在 [基本處理](../../help/sites-authoring/basic-handling.md) 和 [製作頁面的快速指南](../../help/sites-authoring/qg-page-authoring.md).

## 安裝最新的Communities版本 {#install-latest-communities-release}

本教學課程會建立 [啟用社群網站](overview.md#enablement-community). 若要確認已安裝最新的Feature Pack，請造訪：

* [最新發行](deploy-communities.md#latest-releases)

若為建立 [參與社群網站](overview.md#engagement-community)，造訪 [開始使用AEM Communities](getting-started.md).

## 配置啟用功能 {#configure-enablement-features}

若要遵循本教學課程，請務必正確安裝及 [設定啟用](enablement.md)，需要第三方產品，例如MySQL和FFmpeg。

## 設定 Analytics {#configure-analytics}

當 [Adobe Analytics已針對社群網站進行設定](analytics.md)，可在 [報告](reports.md) 在指派給社群成員（學習者）的啟用資源和學習路徑上產生。

## 設定通知的電子郵件 {#configure-email-for-notifications}

通知功能，預設適用於使用 `Communities Sites` console提供電子郵件通道以接收通知。

必須為網站正確設定電子郵件。

請參閱 [設定電子郵件](email.md).

## 啟用通道服務 {#enable-the-tunnel-service}

在製作環境中建立社群網站時，通道服務可讓您建立和管理在發佈環境中註冊的使用者和使用者群組（成員）、將角色指派給受信任的社群成員，以及將內容指派給使用者。

如需詳細資訊，請參閱 [管理使用者和使用者群組](users.md).

有關啟用隧道服務的簡單說明，請參見 [通道服務](deploy-communities.md#tunnel-service-on-author).

## 建立教學課程標籤 {#create-tutorial-tags}

使用的標籤命名空間，建立要用於參與和啟用教學課程的標籤 `Tutorial`.

使用 [標籤主控台](../../help/sites-administering/tags.md#tagging-console) 若要建立下列標籤：

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

## 建立啟用成員和組 {#create-enablement-members-and-groups}

對於啟用社群網站，網站訪客應無法 [自行註冊或使用社交登入](sites-console.md#user-management).

反之，使用 [隧道服務](#enable-the-tunnel-service) 已啟用， [成員控制台](members.md) 用於在發佈環境中註冊新成員。

在本教學課程中，會在發佈環境中建立三個成員。 兩個成員將成為指派給學習路徑的使用者群組的成員，而第三個成員將成為啟用資源連絡人。

第四個使用者是在製作環境中建立，並指派給Communities管理員和Communities啟用管理員的角色。

>[!NOTE]
>
>在建立 *啟用教學課程* 社群網站。
>
>如果之後已建立，則可將其新增為 *啟用教學課程成員群組* 在建立成員時。
>
>相反，稍後會 [分配給成員組](enablement-create-site.md#assignuserstocommunityenablemembersgroup).

### 萊利·泰勒 — 註冊人 {#riley-taylor-enrollee}

[建立成員](members.md#create-new-member) 他們將被加入一組學習者 — 社群滑雪課組。

* **ID**:萊利
* **電子郵件**:riley.taylor@mailinator.com
* **密碼**:密碼
* **確認密碼**:密碼
* **名字**:萊利
* **姓氏**:泰勒

### Sidney Croft — 註冊人 {#sidney-croft-enrollee}

[建立第二個成員](members.md#create-new-member) 將被添加到社區滑雪班組。

* **ID**:西德尼
* **電子郵件**:sidney.croft@mailinator.com
* **密碼**:密碼
* **確認密碼**:密碼
* **名字**:西德尼
* **姓氏**:克羅夫特

### 奎恩·哈珀 — 培訓資源聯繫人和主持人 {#quinn-harper-enablement-resource-contact-and-moderator}

[建立成員](members.md#create-new-member) 在建立站點後，將添加到社區站點的成員組的成員。 此成員資格將允許將成員分配為啟用 [資源聯繫人](resources.md#settings) 為網站建立啟用資源時。

* **ID**:奎恩
* **電子郵件**:quinn.harper@mailinator.com
* **密碼**:密碼
* **確認密碼**:密碼
* **名字**:奎恩
* **姓氏**:哈珀

### 添加用戶組 — 社區滑雪課 {#add-a-user-group-community-ski-class}

[新增群組](members.md#create-new-group) 命名為社區滑雪班。

* **ID**:社區 — 滑雪級
* **名稱**:社區滑雪班
* **說明**:用於分配啟用資源的示例組
* **添加成員到組** &#39;add&#39;:

   * 萊利
   * 西德尼

* 選擇 **[!UICONTROL 儲存]**

### 社區滑雪類屬性 {#community-ski-class-properties}

![ski-class-properties](assets/ski-class-properties.png)

>[!NOTE]
>
>在建立社區站點期間，可將現有成員和組添加到社區站點的成員組。

## 社區管理員角色 {#community-administrator-role}

社區管理員組的成員可以建立社區站點、管理站點、管理成員（他們可以禁止社區中的成員），以及審核內容。

### 建立使用者 {#create-user}

在 *作者*，此角色被分配給社區管理員：

* 在製作例項上

   * 例如， [http://localhost:4502/](http://localhost:4503/)

* 以管理員權限登入

   * 例如，使用者名稱&#39;admin&#39; /密碼&#39;admin&#39;

* 從主控台導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 安全性]** > **[!UICONTROL 使用者]**.
* 從 **[!UICONTROL 編輯]** 菜單，選擇 **[!UICONTROL 添加用戶]**.

* 在 `Create New User` 對話框輸入：

   * **ID&amp;Ast;**:天狼星
   * **電子郵件地址**:sirius.nilson@mailinator.com
   * **密碼(&amp;A);**:密碼
   * **確認密碼(&amp;A);**:密碼
   * **名字**:西里烏
   * **姓氏(&amp;A);**:尼爾森

### 將Sirius分配給社區管理員組 {#assign-sirius-to-community-administrators-group}

向下捲動至 `Add User to Groups`:

* 輸入&#39;C&#39;以搜索

   * 選取 `Community Administrators`
   * 選取 `Community Enablement Managers`

* 選擇 **[!UICONTROL 儲存]**

![管理員 — 角色](assets/admin-role.png)
