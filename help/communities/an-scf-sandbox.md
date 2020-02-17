---
title: 建立SCF沙盒
seo-title: 建立SCF沙盒
description: 本教學課程主要針對對AEM不熟悉的開發人員，他們有興趣使用SCF元件。  它會逐步建立SCF沙盒網站
seo-description: 本教學課程主要針對對AEM不熟悉的開發人員，他們有興趣使用SCF元件。  它會逐步建立SCF沙盒網站
uuid: ee52e670-e1e6-4bcd-9548-c963142e6704
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e1b5c25d-cbdd-421c-b81a-feb6039610a3
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---



# 建立SCF沙盒 {#create-an-scf-sandbox}


自AEM 6.1 Communities起，快速建立沙盒最簡單的方式就是建立社群網站。 請參 [閱「AEM Communities快速入門」](getting-started.md)。

開發人員的另一個實用工具是「社 [群元件」指南](components-guide.md)，可探索社群元件和功能並快速建立原型。

建立網站的練習對於瞭解AEM網站的結構非常有用，其中可能包含「社群」功能，同時也提供簡單頁面，以探索如何使用 [social元件架構(SCF)](scf.md)。

本教學課程主要針對對AEM不熟悉的開發人員，他們有興趣使用SCF元件。 它會逐步建立SCF沙盒網站，類似於如何建立功能完備的網際網路網站( [How to Create a Fully Featured Internet Website](../../help/sites-developing/website.md) )的教學課程，其中著重於網站結構，例如導覽、標誌、搜尋、工具列和列出子頁面。

開發是在作者執行個體上進行，而在發佈執行個體上試驗網站是最佳的。

本教學課程的步驟為：

* [設定網站結構](setup-website.md)
* [初始沙盒應用程式](initial-app.md)
* [初始沙盒內容](initial-content.md)
* [開發沙盒應用程式](develop-app.md)
* [新增Clientlibs](add-clientlibs.md)
* [開發沙盒內容](develop-content.md)

>[!CAUTION]
>
>本教學課程不會使用使用「社群網站」主控台建立的功能來 [建立社群網站](sites-console.md)。 例如，本教學課程不說明如何設定登入、自行註冊、 [社交登入](social-login.md)、訊息、設定檔等。
>
>如果偏好使用簡單的社群網站，請依照「建 [立範例頁面」教學課程](create-sample-page.md) 。

## 必備條件 {#prerequisites}

本教學課程假設您已安裝一個AEM作者和一個AEM發佈例項，其中包含最 [新版](deploy-communities.md#latest-releases) 「社群」。

以下是AEM平台新進開發人員的一些實用連結：

* [快速入門](../../help/sites-deploying/deploy.md#getting-started) -適用於部署AEM例項

   * [The Basics](../../help/sites-developing/the-basics.md) —— 適用於網站和功能的開發人員
   * [作者的第一步](../../help/sites-authoring/first-steps.md) -製作頁面內容

## 使用CRXDE Lite開發環境 {#using-crxde-lite-development-environment}

AEM開發人員將大部分時間花在 [CRXDE Lite開發環境中](../../help/sites-developing/developing-with-crxde-lite.md) ，用於編寫實例。 CRXDE Lite提供對CRX資料庫的較少限制存取。 傳統的UI工具和觸控式UI控制台提供對CRX儲存庫特定部分的更結構化的存取。

使用管理權限登入後，有多種存取CRXDE Lite的方式：

1. 從全域導覽中，選取導 **[!UICONTROL 覽工具> CRXDE Lite]**。

   ![chlimage_1-350](assets/chlimage_1-350.png)

2. 從傳統 [的UI歡迎頁面](http://localhost:4502/welcome.html)，向下捲動並按一下右 **[!UICONTROL 側面板中的CRXDE]** Lite。

   ![chlimage_1-351](assets/chlimage_1-351.png)

3. 直接瀏覽至 `CRXDE Lite`: `<server>:<port>/crx/de`

   例如，在本機作者例項上： ` [http://localhost:4502/crx/de](http://localhost:4502/crx/de)`

若要使用CRXDE Lite，您必須使用開發人員或管理員權限登入。 對於預設的localhost實例，可以使用

* `username: admin`
* `password: admin`


**請注意** ，此登入將逾時，您將需要使用CRXDe Lite工具列右端的下拉式清單定期重新登入。

如果未登錄，您將無法導航JCR儲存庫或執行任何編輯／保存操作。

***如有疑問，請重新登入！***

![chlimage_1-352](assets/chlimage_1-352.png)
