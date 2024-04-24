---
title: 初始設定
description: 瞭解如何初始設定Adobe Experience Manager社群。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
exl-id: 6bda0f09-7ae5-4540-b035-9dd249ac3186
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 1%

---

# 初始設定 {#initial-setup}

## 啟動作者和發佈執行個體 {#start-author-and-publish-instances}

為了開發和示範之目的，必須執行一個製作和一個發佈例項。

若要這麼做，請遵循基本Adobe Experience Manager (AEM) [快速入門](../../help/sites-deploying/deploy.md#getting-started) 指示，會產生下列結果：

* 創作環境於 [localhost：4502](http://localhost:4502/)
* 發佈環境於 [localhost：4503](http://localhost:4503/)

若為AEM Communities，

* 「作者」環境適用於：

   * 網站、範本和元件的開發。
   * 管理和設定工作。

* 發佈環境適用於：

   * 發佈及仲裁內容的社群體驗。
   * 建立社群群組、成員和成員群組。

>[!NOTE]
>
>若不熟悉AEM，請檢視相關的檔案： [基本處理](../../help/sites-authoring/basic-handling.md) 和 [製作頁面的快速指南](../../help/sites-authoring/qg-page-authoring.md).

## 安裝最新的Communities版本 {#install-latest-communities-release}

本教學課程會建立 [參與社群網站](overview.md#engagement-community) 且是以AEM Communities 6.2 Feature Pack 1.10版為基礎。

若要確保已安裝最新的Feature Pack，請造訪：

* [最新版本](deploy-communities.md#latest-releases)

## 設定 Analytics {#configure-analytics}

時間 [已為社群網站設定Adobe Analytics](analytics.md)，提供社群活動相關資訊，可改善社群成員的體驗，並為網站管理員提供意見回饋。

可選擇與Adobe Analytics整合。

## 設定通知電子郵件 {#configure-email-for-notifications}

通知功能，預設適用於所有使用建立的網站 `Communities Sites` console，提供通知的電子郵件通道。

若要正確設定網站的電子郵件，就必須這麼做。

另請參閱 [設定電子郵件](email.md).

## 啟用通道服務 {#enable-the-tunnel-service}

在Author環境中建立社群網站時，通道服務可讓您將角色指派給Publish環境中註冊的受信任社群成員。 通道服務也允許從存取社群成員 [成員和群組主控台](members.md) 在作者環境中。

慣例適用於在發佈環境中建立的成員和成員群組： *非* 將在作者環境中重新建立。 如需詳細資訊，請參閱 [管理使用者和使用者群組](users.md).

如需啟用通道服務的簡單指示，請參閱 **作者** 例項，請參閱 [通道服務](deploy-communities.md#tunnel-service-on-author).

## 社群管理員角色 {#community-administrator-role}

「社群管理員」群組的成員可以建立社群網站、管理網站、管理成員（他們可以禁止社群中的成員）以及稽核內容。

### 建立使用者 {#create-user}

建立使用者於 *作者*，誰被指派了社群管理員的角色：

* 在作者執行個體上

   * 例如， [http://localhost:4502/](http://localhost:4503/)

* 使用管理員許可權登入

   * 例如，使用者名稱&#39;admin&#39; /密碼&#39;admin&#39;

* 從主控台，導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 作業]** > **[!UICONTROL 安全性]** > **[!UICONTROL 使用者]**.
* 從 **編輯** 功能表，選取 **[!UICONTROL 新增使用者]**

* 在 `Create New User` 對話方塊輸入：

   * **[!UICONTROL ID]**：天狼星
   * **[!UICONTROL 電子郵件地址]**： sirius.nilson@mailinator.com
   * **[!UICONTROL 密碼]**：密碼
   * **[!UICONTROL 確認密碼(&amp;A)；]**：密碼
   * **[!UICONTROL 名字]**：天狼星
   * **[!UICONTROL 姓氏]**： Nilson

### 指派Sirius至社群管理員群組 {#assign-sirius-to-community-administrators-group}

向下捲動至 `Add User to Groups`：

* 輸入&#39;C&#39;進行搜尋

   * 選取 `Community Administrators`
   * 選取 `Community Enablement Managers`

* 選取「**[!UICONTROL 儲存]**」。

![create-user](assets/create-user.png)

## 啟用社交登入 {#enable-social-login}

在可以使用Facebook和Twitter的社交登入示範版本之前，您必須

1. 安裝修正套件或 [最新feature pack](deploy-communities.md#latestfeaturepack) (2017年3月Facebook API變更除外)。
1. [啟用OAuth提供者](social-login.md#adobe-granite-oauth-authentication-handler) 在發佈環境中。

對於生產伺服器，必須建立提供社交登入所需的雲端服務。

另請參閱 [使用Facebook和Twitter進行社交登入](social-login.md).

## 建立教學課程標籤 {#create-tutorial-tags}

建立標籤，以便您能將tags用於engage教學課程，使用 `Tutorial`.

使用 [標籤主控台](../../help/sites-administering/tags.md#tagging-console) 若要建立下列標籤：

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![tutorial-tags](assets/tutorial-tags.png)

然後依照指示進行：

1. [設定標籤許可權](../../help/sites-administering/tags.md#setting-tag-permissions).
1. [發佈標籤](../../help/sites-administering/tags.md#publishing-tags).

為AEM Communities快速入門Tutorials建立的標籤範例套件

[取得檔案](assets/tutorial_tags-v63.zip)

## UGC公用存放區的MongoDB {#mongodb-for-ugc-common-store}

建議設定（但選用） [MSRP](msrp.md) (MongoDB)作為 [公用存放區](working-with-srp.md) 以體驗從發佈和/或作者環境中仲裁所有UGC的彈性。

如需指示，請造訪 [如何設定MongoDB以進行示範](demo-mongo.md).

依預設，安裝作者和發佈AEM執行個體時，使用者產生的內容(UGC)會儲存在 [JCR Tar儲存](../../help/sites-deploying/platform.md) ，存取方式： [JSRP](jsrp.md). JSRP不是通用存放區，這表示UGC只會顯示在輸入它的執行個體上。 通常UGC會輸入在發佈執行個體上，且不會顯示在製作環境中，導致所有協調工作需要使用發佈執行個體。
