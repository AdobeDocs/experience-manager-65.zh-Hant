---
title: 初始設定
seo-title: Initial Setup
description: 設定社區
seo-description: Setting up Communities
uuid: c53d280c-c5ae-47cf-8038-f0dea68e15ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 0d462ad1-5619-4bb6-9609-bc8987c40a0c
exl-id: 6bda0f09-7ae5-4540-b035-9dd249ac3186
source-git-commit: 942db8fe3dad16be53dc6abe0e519d97a659e480
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 2%

---

# 初始設定 {#initial-setup}

## 啟動作者和發佈實例 {#start-author-and-publish-instances}

為了開發和演示，需要運行一個作者和一個發佈實例。

為此，請遵循基AEM本 [入門](../../help/sites-deploying/deploy.md#getting-started) 說明，將導致：

* 作者環境 [localhost:4502](http://localhost:4502/)
* 在上發佈環境 [localhost:4503](http://localhost:4503/)

對於AEM Communities,

* 作者環境用於：

   * 開發網站、模板和元件。
   * 管理和配置任務。

* 發佈環境用於：

   * 發佈和調節內容的社區體驗。
   * 建立社區組、成員和成員組。

>[!NOTE]
>
>如果不熟悉AEM，請查看 [基本處理](../../help/sites-authoring/basic-handling.md) 和 [創作頁面的快速指南](../../help/sites-authoring/qg-page-authoring.md)。

## 安裝最新社區版本 {#install-latest-communities-release}

本教程將建立 [項目社區站點](overview.md#engagement-community) 基於AEM Communities6.2功能包版本1.10。

要確保安裝了最新的功能包，請訪問：

* [最新版本](deploy-communities.md#latest-releases)

## 設定 Analytics {#configure-analytics}

當 [Adobe Analytics為社區站點配置](analytics.md)，提供有關社區活動的資訊，以增強社區成員的體驗，並向站點管理員提供反饋。

與Adobe Analytics的融合是可選的。

## 為通知配置電子郵件 {#configure-email-for-notifications}

通知功能，預設情況下可用於使用 `Communities Sites` 控制台，提供通知的電子郵件通道。

需要為站點正確配置電子郵件。

請參閱 [配置電子郵件](email.md)。

## 啟用隧道服務 {#enable-the-tunnel-service}

當在作者環境中建立社區站點時，隧道服務使得能夠將角色分配給在發佈環境中註冊的受信任社區成員。 隧道服務還允許從 [成員和組控制台](members.md) 在作者環境中。

公約適用於在發佈環境中建立的成員和成員組 *不* 在作者環境中重新建立。 有關詳細資訊，請參閱 [管理用戶和用戶組](users.md)。

有關在上啟用隧道服務的簡單說明 **作者** 實例，請參閱 [隧道服務](deploy-communities.md#tunnel-service-on-author)。

## 社區管理員角色 {#community-administrator-role}

「社區管理員」組的成員可以建立社區站點、管理站點、管理成員（他們可以禁止社區成員），以及中等內容。

### 建立使用者 {#create-user}

在上建立用戶 *作者*，分配了「社區管理員」角色的用戶：

* 論作者案

   * 比如說， [http://localhost:4502/](http://localhost:4503/)

* 使用管理員權限登錄

   * 例如，用戶名「admin」/密碼「admin」

* 從主控制台導航到 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 安全]** > **[!UICONTROL 用戶]**。
* 從 **編輯** 菜單，選擇 **[!UICONTROL 添加用戶]**

* 在 `Create New User` 對話框輸入：

   * **[!UICONTROL ID]**:天狼星
   * **[!UICONTROL 電子郵件地址]**:sirius.nilson@mailinator.com
   * **[!UICONTROL 密碼]**:密碼
   * **[!UICONTROL 確認密碼(&amp;A);]**:密碼
   * **[!UICONTROL 名字]**:天狼星
   * **[!UICONTROL 姓氏]**:尼爾森

### 將Sirius分配給社區管理員組 {#assign-sirius-to-community-administrators-group}

向下滾動到 `Add User to Groups`:

* 輸入「C」以搜索

   * 選取 `Community Administrators`
   * 選取 `Community Enablement Managers`

* 選取&#x200B;**[!UICONTROL 儲存]**。

![建立用戶](assets/create-user.png)

## 啟用社交登錄 {#enable-social-login}

在使用Facebook和Twitter社會登錄演示版之前，必須

1. 安裝修復程式包或 [最新功能包](deploy-communities.md#latestfeaturepack) (2017年3月FacebookAPI更改)。
1. [啟用OAuth提供程式](social-login.md#adobe-granite-oauth-authentication-handler) 的子菜單。

對於生產伺服器，需要建立提供社交登錄所需的雲服務。

請參閱 [與Facebook和Twitter社會登錄](social-login.md)。

## 建立教程標籤 {#create-tutorial-tags}

使用的標籤命名空間建立用於項目教程的標籤 `Tutorial`。

使用 [標籤控制台](../../help/sites-administering/tags.md#tagging-console) 建立以下標籤：

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![教程標籤](assets/tutorial-tags.png)

然後按照說明執行以下操作：

1. [設定標籤權限](../../help/sites-administering/tags.md#setting-tag-permissions)。
1. [發佈標籤](../../help/sites-administering/tags.md#publishing-tags)。

為AEM Communities入門Tutorials建立的標籤包示例

[取得檔案](assets/tutorial_tags-v63.zip)

## 用於UGC公用儲存的MongoDB {#mongodb-for-ugc-common-store}

建議設定（但可選） [MSRP](msrp.md) (MongoDB) [普通商店](working-with-srp.md) 體驗從發佈和/或作者環境調節所有UGC的靈活性。

有關說明，請訪問 [如何設定MongoDB以進行演示](demo-mongo.md)。

預設情況下，安裝作者和發佈實例AEM將導致將用戶生成的內容(UGC)儲存在 [JCR Tar儲存](../../help/sites-deploying/platform.md) 使用 [JSRP](jsrp.md)。 JSRP不是公用儲存，這意味著UGC僅在輸入它的實例上可見。 通常，UGC是在發佈實例上輸入的，在作者環境中不可見，從而導致需要使用發佈實例的所有審核任務。
