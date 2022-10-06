---
title: 建立SCF沙箱
seo-title: Create An SCF Sandbox
description: 本教學課程主要針對對使用SCF元件感興趣的AEM新手開發人員。  它會逐步說明如何建立SCF沙箱網站
seo-description: This tutorial is primarily for developers, new to AEM, who are interested in using SCF components.  It walks through the creation of An SCF Sandbox site
uuid: ee52e670-e1e6-4bcd-9548-c963142e6704
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e1b5c25d-cbdd-421c-b81a-feb6039610a3
exl-id: 89858814-6625-4a56-8359-cc1eca402816
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---

# 建立SCF沙箱  {#create-an-scf-sandbox}


與AEM 6.1社群相同，快速建立沙箱最簡單的方式是建立社群網站。 請參閱 [開始使用AEM Communities](getting-started.md).

開發人員的另一個實用工具是 [社群元件指南](components-guide.md)，可探索Communities元件和功能並快速建立原型。

建立網站的練習有助於了解AEM網站的結構（可能包含Communities功能），同時也提供可探索如何與搭配使用的簡單頁面 [社會構成框架](scf.md).

本教學課程主要針對對使用SCF元件感興趣的AEM新手開發人員。 它會逐步說明如何建立SCF沙箱網站，類似於的教學課程 [如何建立功能齊全的網際網路網站](../../help/sites-developing/website.md) 重點在網站結構，例如導覽、標誌、搜尋、工具列和列出子頁面。

開發會在製作例項上進行，而實驗網站最適合在發佈例項上。

本教學課程中的步驟為：

* [設定網站結構](setup-website.md)
* [初始沙箱應用程式](initial-app.md)
* [初始沙箱內容](initial-content.md)
* [開發沙箱應用程式](develop-app.md)
* [新增Clientlibs](add-clientlibs.md)
* [開發沙箱內容](develop-content.md)

>[!CAUTION]
>
>本教學課程不會使用使用 [Communities Sites主控台](sites-console.md). 例如，本教學課程不說明如何設定登入、自行註冊、 [社交登入](social-login.md)、傳訊、設定檔等。
>
>如果偏好使用簡單的社群網站，請遵循 [建立範例頁面](create-sample-page.md) 教學課程。

## 必備條件 {#prerequisites}

本教學課程假設您已安裝一個AEM作者和一個AEM發佈例項，其中包含 [最新版本](deploy-communities.md#latest-releases) 社區。

以下是剛接觸AEM平台的開發人員的實用連結：

* [快速入門](../../help/sites-deploying/deploy.md#getting-started):用於部署AEM例項。

   * [基本概念](../../help/sites-developing/the-basics.md):適用於網站和功能的開發人員。
   * [作者的第一步](../../help/sites-authoring/first-steps.md):，用於編寫頁面內容。

## 使用CRXDE Lite開發環境 {#using-crxde-lite-development-environment}

AEM開發人員將大部分時間花在 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) 製作例項上的開發環境。 CRXDE Lite提供對CRX存放庫的較少限制存取。 傳統UI工具和觸控式UI主控台可提供對CRX存放庫特定部分的更結構化存取。

以管理權限登入後，有多種存取CRXDE Lite的方式：

1. 從全局導航中，選擇導航 **[!UICONTROL 工具>CRXDE Lite]**.

   ![crxde-lite](assets/tools-crxde.png)

2. 從 [傳統UI歡迎頁面](http://localhost:4502/welcome.html)，向下捲動並按一下 **[!UICONTROL CRXDE Lite]** 中。

   ![classic-ui-crxde](assets/classic-ui-crxde.png)

3. 直接瀏覽至 `CRXDE Lite`: `<server>:<port>/crx/de`

   例如，在本機製作例項上： [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

若要使用CRXDE Lite，您必須使用開發人員或管理員權限登入。 對於預設的localhost實例，可以使用

* `username: admin`
* `password: admin`


**注意** 此登入會逾時，您將需要使用CRXDe Lite工具列右端的下拉式清單，定期重新登入。

如果未登入，您將無法導覽JCR存放庫或執行任何編輯/儲存作業。

***有疑問時，重新登錄！***

![重新登入](assets/relogin.png)
