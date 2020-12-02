---
title: 初始設定
seo-title: 初始設定
description: 設定社區
seo-description: 設定社區
uuid: c53d280c-c5ae-47cf-8038-f0dea68e15ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 0d462ad1-5619-4bb6-9609-bc8987c40a0c
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 1%

---


# 初始設定{#initial-setup}

## 啟動作者和發佈例項{#start-author-and-publish-instances}

為了開發和展示，必須執行一個作者和一個發佈執行個體。

若要這麼做，請依照基本的AEM [快速入門](../../help/sites-deploying/deploy.md#getting-started)指示進行，這將導致：

* [localhost:4502](http://localhost:4502/)上的作者環境
* [localhost:4503](http://localhost:4503/)上的發佈環境

對於AEM Communities,

* 作者環境適用於：

   * 開發網站、範本和元件。
   * 管理和配置任務。

* 發佈環境適用於：

   * 張貼和協調內容的社群體驗。
   * 建立社區組、成員和成員組。

>[!NOTE]
>
>如果不熟悉AEM，請檢視[基本處理](../../help/sites-authoring/basic-handling.md)和[製作頁面快速指南的說明檔案](../../help/sites-authoring/qg-page-authoring.md)。

## 安裝最新的社區版本{#install-latest-communities-release}

本教學課程會建立[參與社群網站](overview.md#engagement-community)，並以AEM Communities 6.2功能套件1.10版為基礎。

若要確保已安裝最新的功能套件，請造訪：

* [最新版本](deploy-communities.md#latest-releases)

如需建立[啟用社群網站](overview.md#enablement-community)的教學課程，請造訪[AEM社群快速入門以進行啟用](getting-started-enablement.md)。

## 設定 Analytics {#configure-analytics}

為社群網站[設定](analytics.md) Adobe Analytics時，會提供社群活動的相關資訊，以增強社群成員的體驗，並為網站的管理員提供意見回應。

與Adobe Analytics整合是選用的。

## 設定電子郵件通知{#configure-email-for-notifications}

通知功能預設適用於使用`Communities Sites`主控台建立的所有網站，提供電子郵件通道以接收通知。

必須為網站正確設定電子郵件。

請參閱[設定電子郵件](email.md)。

## 啟用隧道服務{#enable-the-tunnel-service}

在作者環境中建立社區站點時，隧道服務可以將角色分配給在發佈環境中註冊的受信任社區成員。 隧道服務還允許從作者環境中的[成員和組控制台](members.md)訪問社區成員。

該約定適用於在發佈環境中建立到&#x200B;*not*&#x200B;的成員和成員組在作者環境中重新建立。 如需詳細資訊，請參閱[管理使用者和使用者群組](users.md)。

有關在&#x200B;**author**&#x200B;實例上啟用隧道服務的簡單說明，請參見[隧道服務](deploy-communities.md#tunnel-service-on-author)。

## 社區管理員角色{#community-administrator-role}

「社群管理員」群組成員可以建立社群網站、管理網站、管理成員（他們可以禁止社群成員）以及協調內容。

### 建立使用者 {#create-user}

在&#x200B;*author*&#x200B;上建立一個用戶，該用戶被分配為社區管理員的角色：

* 關於作者實例

   * 例如，[http://localhost:4502/](http://localhost:4503/)

* 以管理員權限登入

   * 例如，使用者名稱&#39;admin&#39; /密碼&#39;admin&#39;

* 從主控制台導航至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 安全]** > **[!UICONTROL 用戶]**。
* 從&#x200B;**編輯**&#x200B;菜單中，選擇&#x200B;**[!UICONTROL 添加用戶]**

* 在`Create New User`對話框中，輸入：

   * **[!UICONTROL ID]**:天狼星
   * **[!UICONTROL 電子郵件地址]**:sirius.nilson@mailinator.com
   * **[!UICONTROL 密碼]**:密碼
   * **[!UICONTROL 確認密碼(&amp;A)]**:密碼
   * **[!UICONTROL 名字]**:天狼星
   * **[!UICONTROL 姓氏]**:尼爾森

### 將Sirius分配給社區管理員組{#assign-sirius-to-community-administrators-group}

向下捲動至`Add User to Groups`:

* 輸入&#39;C&#39;以進行搜尋

   * 選取 `Community Administrators`
   * 選取 `Community Enablement Managers`

* 選擇&#x200B;**[!UICONTROL 保存]**。

![create-user](assets/create-user.png)

## 啟用社交登入{#enable-social-login}

在使用Facebook和Twitter的社交登入展示版本之前，必須

1. 安裝修正套件或[最新功能套件](deploy-communities.md#latestfeaturepack)（針對2017年3月Facebook API變更）。
1. [在發佈環境](social-login.md#adobe-granite-oauth-authentication-handler) 中啟用OAuth提供者。

對於生產伺服器，必須建立提供社交登入所需的雲端服務。

請參閱[使用Facebook和Twitter進行社交登入](social-login.md)。

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

1. [設定標籤權限](../../help/sites-administering/tags.md#setting-tag-permissions)。
1. [發佈標籤](../../help/sites-administering/tags.md#publishing-tags)。

為AEM Communities快速入門教學課程所建立的標籤範例套件

[取得檔案](assets/tutorial_tags-v63.zip)

## UGC通用儲存的MongoDB {#mongodb-for-ugc-common-store}

建議您將[MSRP](msrp.md)(MongoDB)設為[公用商店](working-with-srp.md)，以體驗從發佈和／或作者環境協調所有UGC的彈性。

有關說明，請訪問[如何設定演示的MongoDB](demo-mongo.md)。

依預設，安裝作者和發佈AEM例項會導致使用者產生的內容(UGC)儲存在使用[JSRP](jsrp.md)存取的[JCR Tar storage](../../help/sites-deploying/platform.md)中。 JSRP不是通用商店，這表示UGC只會在輸入該商店的例項上顯示。 通常，UGC是在發佈例項上輸入，在作者環境中不會顯示，導致所有需要使用發佈例項的協調工作。