---
title: 初始設定
seo-title: 初始設定
description: 設定社群
seo-description: 設定社群
uuid: c53d280c-c5ae-47cf-8038-f0dea68e15ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 0d462ad1-5619-4bb6-9609-bc8987c40a0c
exl-id: 6bda0f09-7ae5-4540-b035-9dd249ac3186
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 2%

---

# 初始設定{#initial-setup}

## 啟動製作和發佈執行個體{#start-author-and-publish-instances}

為了開發和展示用途，必須執行一個製作和一個發佈例項。

要執行此操作，請遵循基本的AEM [快速入門](../../help/sites-deploying/deploy.md#getting-started)指示，這會導致：

* [localhost:4502](http://localhost:4502/)上的製作環境
* 在[localhost:4503](http://localhost:4503/)上發佈環境

對於AEM Communities,

* 製作環境適用於：

   * 開發網站、範本和元件。
   * 管理和配置任務。

* 發佈環境適用於：

   * 張貼和協調內容的社群體驗。
   * 建立社區組、成員和成員組。

>[!NOTE]
>
>若不熟悉AEM，請檢視[basic handling](../../help/sites-authoring/basic-handling.md)和[製作頁面快速指南](../../help/sites-authoring/qg-page-authoring.md)的相關檔案。

## 安裝最新的Communities版本{#install-latest-communities-release}

本教學課程會建立[參與社群網站](overview.md#engagement-community)，並以AEM Communities 6.2 Feature Pack 1.10版為基礎。

若要確認已安裝最新的Feature Pack，請造訪：

* [最新發行](deploy-communities.md#latest-releases)

如需建立[啟用社群網站](overview.md#enablement-community)的教學課程，請造訪[啟用AEM Communities快速入門](getting-started-enablement.md)。

## 設定 Analytics {#configure-analytics}

為社群網站](analytics.md)設定[Adobe Analytics時，可使用社群活動資訊來增強社群成員的體驗，並為網站管理員提供意見回饋。

與Adobe Analytics整合為選用。

## 配置通知的電子郵件{#configure-email-for-notifications}

預設情況下，使用`Communities Sites`控制台建立的所有網站都可使用通知功能，可提供通知的電子郵件通道。

必須為網站正確設定電子郵件。

請參閱[設定電子郵件](email.md)。

## 啟用通道服務{#enable-the-tunnel-service}

在製作環境中建立社群網站時，通道服務可將角色指派給在發佈環境中註冊的受信任社群成員。 通道服務也允許從製作環境中的[成員和群組控制台](members.md)存取社群成員。

此慣例適用於在發佈環境中建立至&#x200B;*not*&#x200B;的成員和成員群組，需在製作環境中重新建立。 如需詳細資訊，請參閱[管理使用者和使用者群組](users.md)。

有關在&#x200B;**author**&#x200B;實例上啟用隧道服務的簡單說明，請參閱[隧道服務](deploy-communities.md#tunnel-service-on-author)。

## 社區管理員角色{#community-administrator-role}

社區管理員組的成員可以建立社區站點、管理站點、管理成員（他們可以禁止社區中的成員），以及審核內容。

### 建立使用者 {#create-user}

在&#x200B;*author*&#x200B;上建立被分配了社區管理員角色的用戶：

* 在製作例項上

   * 例如， [http://localhost:4502/](http://localhost:4503/)

* 以管理員權限登入

   * 例如，使用者名稱&#39;admin&#39; /密碼&#39;admin&#39;

* 從主控台，導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 安全性]** > **[!UICONTROL 使用者]**。
* 從&#x200B;**Edit**&#x200B;菜單中，選擇&#x200B;**[!UICONTROL Add User]**

* 在`Create New User`對話方塊中，輸入：

   * **[!UICONTROL ID]**:天狼星
   * **[!UICONTROL 電子郵件地址]**:sirius.nilson@mailinator.com
   * **[!UICONTROL 密碼]**:密碼
   * **[!UICONTROL 確認密碼(&amp;A);]**:密碼
   * **[!UICONTROL 名字]**:西里烏
   * **[!UICONTROL 姓氏]**:尼爾森

### 將Sirius分配給社區管理員組{#assign-sirius-to-community-administrators-group}

向下捲動至`Add User to Groups`:

* 輸入&#39;C&#39;以搜索

   * 選取 `Community Administrators`
   * 選取 `Community Enablement Managers`

* 選擇&#x200B;**[!UICONTROL 保存]**。

![create-user](assets/create-user.png)

## 啟用社交登入{#enable-social-login}

在使用Facebook和Twitter的社交登入示範版本之前，您必須

1. 安裝Fix Pack或[最新Feature Pack](deploy-communities.md#latestfeaturepack)(針對2017年3月Facebook API變更)。
1. [在發佈環](social-login.md#adobe-granite-oauth-authentication-handler) 境中啟用OAuth提供者。

對於生產伺服器，必須建立提供社交登入所需的雲端服務。

請參閱[使用Facebook和Twitter進行社交登入](social-login.md)。

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

1. [設定標籤權限](../../help/sites-administering/tags.md#setting-tag-permissions)。
1. [發佈標籤](../../help/sites-administering/tags.md#publishing-tags)。

為AEM Communities快速入門Tutorials建立的標籤範例套件

[取得檔案](assets/tutorial_tags-v63.zip)

## 用於UGC常見儲存的MongoDB {#mongodb-for-ugc-common-store}

建議您將[MSRP](msrp.md)(MongoDB)設為[公用商店](working-with-srp.md)，以體驗從發佈和/或製作環境協調所有UGC的彈性。

有關說明，請訪問[如何為Demo](demo-mongo.md)設定MongoDB。

依預設，安裝製作和發佈AEM例項會導致使用者產生的內容(UGC)儲存在[JCR Tar storage](../../help/sites-deploying/platform.md)中，而此儲存是使用[JSRP](jsrp.md)存取。 JSRP不是常見商店，這表示UGC只會顯示在輸入的執行個體上。 通常，UGC是在發佈例項上輸入，且不會顯示在製作環境中，導致所有協調工作都需要使用發佈例項。
