---
title: 建立SCF沙箱
description: 本教學課程主要針對不熟悉AEM且有意使用SCF元件的開發人員。 它會逐步建立SCF沙箱網站
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 89858814-6625-4a56-8359-cc1eca402816
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---

# 建立SCF沙箱  {#create-an-scf-sandbox}

自AEM 6.1社群起，快速建立沙箱的最簡單方式就是建立社群網站。 另請參閱 [AEM Communities快速入門](getting-started.md).

另一個對開發人員有用的工具是 [社群元件指南](components-guide.md)，可讓您探索及快速建立Communities元件和功能的原型。

建立網站的練習有助於瞭解AEM網站的結構，其中可能包含Communities功能，同時提供簡單頁面，讓您探索如何使用網站 [社交元件架構(SCF)](scf.md).

本教學課程主要針對不熟悉AEM且有意使用SCF元件的開發人員。 它會逐步建立SCF沙箱網站，類似於的教學課程 [如何建立完整功能的網際網路網站](../../help/sites-developing/website.md) 它會著重於網站上的結構，例如導覽、標誌、搜尋、工具列以及列出子頁面。

開發會在作者執行個體上進行，而試驗網站最適合在發佈執行個體上進行。

本教學課程中的步驟為：

* [設定網站結構](setup-website.md)
* [初始沙箱應用程式](initial-app.md)
* [初始沙箱內容](initial-content.md)
* [開發沙箱應用程式](develop-app.md)
* [新增Clientlibs](add-clientlibs.md)
* [開發沙箱內容](develop-content.md)

>[!CAUTION]
>
>本教學課程不會使用建立的功能來建立社群網站 [社群網站主控台](sites-console.md). 例如，本教學課程未說明如何設定登入、自我註冊、 [社交登入](social-login.md)、傳訊、設定檔等。
>
>如果偏好使用簡單的社群網站，請遵循 [建立範例頁面](create-sample-page.md) 教學課程。

## 先決條件 {#prerequisites}

本教學課程假設您已安裝一個AEM作者和一個AEM發佈執行個體，該執行個體具有 [最新版本](deploy-communities.md#latest-releases) 社群的。

以下是初次接觸AEM平台之開發人員的一些實用連結：

* [快速入門](../../help/sites-deploying/deploy.md#getting-started)：用於部署AEM執行個體。

   * [基本資訊](../../help/sites-developing/the-basics.md)：適用於網站與功能的開發人員。
   * [作者的首要步驟](../../help/sites-authoring/first-steps.md)：用於編寫頁面內容。

## 使用CRXDE Lite開發環境 {#using-crxde-lite-development-environment}

AEM開發人員的大部分時間都花在 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) 製作例項上的開發環境。 CRXDE Lite提供對CRX存放庫的較少限制存取。 傳統UI工具和觸控式UI主控台提供對CRX存放庫特定部分的更結構化存取。

以管理許可權登入後，有多種方式可存取CRXDE Lite：

1. 在全域導覽中選取導覽 **[!UICONTROL 「工具」>「CRXDE Lite」]**.

   ![crxde-lite](assets/tools-crxde.png)

2. 從 [傳統UI歡迎頁面](http://localhost:4502/welcome.html)，向下捲動並按一下 **[!UICONTROL CRXDE Lite]** 在右側面板中。

   ![classic-ui-crxde](assets/classic-ui-crxde.png)

3. 直接瀏覽到 `CRXDE Lite`： `<server>:<port>/crx/de`

   例如，在本機作者執行個體上： [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

若要使用CRXDE Lite，您必須使用開發人員或管理員許可權登入。 對於預設的localhost執行個體，您可以以下列方式登入：

* `username: admin`
* `password: admin`


登入逾時，您必須使用CRXDE Lite工具列右端的下拉式功能表，定期重新登入。

如果未登入，您將無法導覽JCR存放庫或執行任何編輯/儲存操作。

***如有疑問，請重新登入！***

![重新登入](assets/relogin.png)
