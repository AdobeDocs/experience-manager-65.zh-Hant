---
title: 建立SCF沙盒
seo-title: Create An SCF Sandbox
description: 本教程主要針對對使用SCF元件感AEM興趣的新開發人員。  它通過建立SCF沙盒站點
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

# 建立SCF沙盒  {#create-an-scf-sandbox}


截至AEM6.1社區，快速建立沙箱的最簡單方法是建立社區站點。 請參閱 [AEM Communities入門](getting-started.md)。

開發人員的另一個有用工具是 [社區元件指南](components-guide.md)它允許探索社區元件和功能並快速建立原型。

建立網站的練習對於瞭解網站的結構非常有用，該網AEM站可能包括社區功能，同時還提供了一些簡單的頁面，可供您探討如何與 [社會構成框架](scf.md)。

本教程主要針對對使用SCF元件感AEM興趣的新開發人員。 它將引導建立一個SCF沙盒站點，類似於 [如何建立功能齊全的Internet網站](../../help/sites-developing/website.md) 重點介紹網站結構，如導航、徽標、搜索、工具欄和列出子頁面。

在作者實例上進行開發，而在發佈實例上對站點進行實驗是最好的。

本教程中的步驟包括：

* [設定網站結構](setup-website.md)
* [初始沙盒應用程式](initial-app.md)
* [初始沙盒內容](initial-content.md)
* [開發沙盒應用程式](develop-app.md)
* [添加客戶端](add-clientlibs.md)
* [開發沙盒內容](develop-content.md)

>[!CAUTION]
>
>本教程不會使用使用 [社區站點控制台](sites-console.md)。 例如，本教程不介紹如何設定登錄、自註冊、 [社交登錄](social-login.md)、消息、配置檔案等。
>
>如果首選簡單的社區站點，請遵循 [建立示例頁](create-sample-page.md) 教程。

## 必備條件 {#prerequisites}

本教程假定您安裝了AEM一個作AEM者和一個發佈實例， [最新版本](deploy-communities.md#latest-releases) 社區。

以下是一些對新平台開發人員有用的AEM連結：

* [入門](../../help/sites-deploying/deploy.md#getting-started):用於部署實AEM例。

   * [基礎](../../help/sites-developing/the-basics.md):網站和功能的開發者。
   * [作者的第一步](../../help/sites-authoring/first-steps.md):頁面內容。

## 使用CRXDE Lite開發環境 {#using-crxde-lite-development-environment}

開發AEM商將大部分時間花在 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) 開發環境。 CRXDE Lite提供對CRX儲存庫的較少限制的訪問。 經典UI工具和支援觸摸的UI控制台提供了對CRX儲存庫特定部分的更結構化的訪問。

使用管理權限登錄後，有多種方法可訪問CRXDE Lite:

1. 從全局導航中，選擇導航 **[!UICONTROL 工具>CRXDE Lite]**。

   ![crxde-lite](assets/tools-crxde.png)

2. 從 [經典UI歡迎頁](http://localhost:4502/welcome.html)，向下滾動，按一下 **[!UICONTROL CRXDE Lite]** 的下界。

   ![經典ui-crxde](assets/classic-ui-crxde.png)

3. 直接瀏覽到 `CRXDE Lite`: `<server>:<port>/crx/de`

   例如，在本地作者實例上： [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

要使用CRXDE Lite，必須使用開發人員或管理員權限登錄。 對於預設的localhost實例，可以使用

* `username: admin`
* `password: admin`


**注意** 此登錄將超時，您需要使用CRXDe Lite工具欄右端的下拉菜單定期重新登錄。

如果未登錄，您將無法導航JCR儲存庫或執行任何編輯/保存操作。

***有疑問時，重新登錄！***

![重新登錄](assets/relogin.png)
