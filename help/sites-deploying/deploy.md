---
title: 部署和維護
seo-title: Deploying and Maintaining
description: 了解如何開始安裝AEM。
seo-description: Learn how to get started with the AEM installation.
uuid: 4429ac4d-abd7-47d8-b19d-773accb7cc7a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: e48cc0ed-688c-44c8-b6d6-5f3c8593a295
docset: aem65
exl-id: 3df0662a-0768-4b56-8b94-c517657b4bd9
source-git-commit: bb8dbb9069c4575af62a4d0b21195cee75944fea
workflow-type: tm+mt
source-wordcount: '1808'
ht-degree: 3%

---

# 部署和維護{#deploying-and-maintaining}

在此頁面中，您會找到：

* [基本概念](#basic-concepts)

   * [什麼是AEM?](#what-is-aem)
   * [典型部署](#typical-deployment-scenarios)

      * [內部部署](#on-premise)
      * [Managed Services使用Cloud Manager](#managed-services-using-cloud-manager)

* [快速入門](#getting-started)

   * [必備條件](#prerequisites)
   * [獲取軟體](#getting-the-software)
   * [預設本地安裝](#default-local-install)
   * [製作和發佈安裝](#author-and-publish-installs)
   * [未打包的安裝目錄](#unpacked-install-directory)
   * [啟動和停止](#starting-and-stopping)

熟悉這些基本知識後，您便可在下列子頁面中找到更進階的詳細資訊：

* [技術需求](/help/sites-deploying/technical-requirements.md)
* [建議的部署](/help/sites-deploying/recommended-deploys.md)
* [自定義獨立安裝](/help/sites-deploying/custom-standalone-install.md)
* [應用程式伺服器安裝](/help/sites-deploying/application-server-install.md)
* [疑難排解](/help/sites-deploying/troubleshooting.md)
* [命令行開始和停止](/help/sites-deploying/command-line-start-and-stop.md)
* [設定](/help/sites-deploying/configuring.md)
* [升級至AEM 6.5](/help/sites-deploying/upgrade.md)
* [電子商務](/help/commerce/cif-classic/deploying/ecommerce.md)
* [設定作法文章](/help/sites-deploying/ht-deploy.md)
* [Web 主控台](/help/sites-deploying/web-console.md)
* [疑難排解復寫](/help/sites-deploying/troubleshoot-rep.md)
* [最佳作法](/help/sites-deploying/best-practices.md)
* [部署社群](/help/communities/deploy-communities.md)
* [AEM Platform簡介](/help/sites-deploying/platform.md)
* [效能准則](/help/sites-deploying/performance-guidelines.md)
* [開始使用AEM Mobile](/help/mobile/getting-started-aem-mobile.md)
* [什麼是AEM Screens?](https://docs.adobe.com/content/help/zh-Hant/experience-manager-screens/user-guide/aem-screens-introduction.html)

## 基本概念 {#basic-concepts}

### 什麼是AEM? {#what-is-aem}

Adobe Experience Manager是以web為基礎的用戶端 — 伺服器系統，用於建立、管理及部署商業網站及相關服務。 它將許多基礎架構級別和應用程式級別功能合併到單個整合的軟體包中。

在基礎架構級別AEM提供以下內容：

* **Web應用程式伺服器**:AEM可以部署在獨立模式（包括整合的Jetty Web伺服器）中，或作為第三方應用程式伺服器內的Web應用程式。
* **Web應用程式框架**:AEM整合了Sling Web應用程式架構，可簡化RESTful、內容導向的Web應用程式的編寫。
* **內容存放庫**:AEM包含Java Content Repository(JCR)，這是一種專為非結構化和半結構化資料而設計的分層資料庫。 儲存庫不僅儲存面向用戶的內容，還儲存應用程式使用的所有代碼、模板和內部資料。

在此基礎上，AEM還提供許多應用程式層級功能，用於管理：

* **網站**
* **行動應用程式**
* **數位出版物**
* **Forms**
* **數位資產**
* **社群**
* **線上商務**

最後，客戶可以使用這些基礎架構和應用程式級構建塊，通過構建自己的應用程式來建立自定義的解決方案。

AEM伺服器為 **Java型** 並在支援該平台的大部分作業系統上運行。 所有與AEM的用戶端互動都是透過 **網頁瀏覽器**.

### 典型部署方案 {#typical-deployment-scenarios}

在AEM術語中，「例項」是伺服器上執行的AEM復本。 AEM安裝通常至少涉及兩個執行個體，通常在不同的電腦上執行：

* **作者**:用於建立、上傳和編輯內容及管理網站的AEM例項。 內容準備好上線後，就會複製到發佈執行個體。
* **發佈**:提供發佈內容給大眾的AEM例項。

這些實例與安裝的軟體相同。 它們僅由配置區別。 此外，大部分安裝都使用Dispatcher:

* **Dispatcher**:靜態Web伺服器(Apache httpd、Microsoft IIS等) 與AEM dispatcher模組搭配增強。 它會快取由發佈例項產生的網頁，以提升效能。

此設定有許多進階選項和說明，但製作、發佈和調度程式的基本模式是大部分部署的核心。 首先，我們將專注於一個相對簡單的機構。 下面將討論高級部署選項。

以下幾節將說明兩種情況：

* **內部部署**:AEM在您的公司環境中部署和管理。

* **Managed Services — 適用於Adobe Experience Manager的Cloud Manager**:由Adobe Managed Services部署和管理的AEM

### 內部部署 {#on-premise}

您可以在公司環境中的伺服器上安裝AEM。 典型安裝實例包括：開發、測試和發佈環境。 請參閱 [快速入門](/help/sites-deploying/deploy.md#getting%20started) 一節，以取得如何將AEM軟體安裝在本機的基本詳細資訊。

若要進一步了解典型的內部部署，請參閱 [建議的部署](/help/sites-deploying/recommended-deploys.md).

### Managed Services使用Cloud Manager {#managed-services-using-cloud-manager}

AEM Managed Services是數位體驗管理的完整解決方案。 它在雲端中提供體驗傳送解決方案的優點，同時保留內部部署的所有控制、安全性和自訂優點。 AEM Managed Services可讓客戶透過在雲端上部署，以及透過Adobe的最佳實務和支援來加快啟動速度。 組織和業務用戶可以在最短的時間內與客戶接洽，推動市場份額，並專注於創新營銷活動，同時減輕IT的負擔。

透過AEM Managed Services，客戶可實現下列優點：

**加速上市時間：** 透過Adobe Managed Services的彈性雲端基礎架構，組織可以快速規劃、啟動並最佳化成功的數位體驗。 Adobe無需額外的資金、硬體或軟體即可管理雲架構，Adobe的客戶成功工程師可提供AEM架構、布建、自訂以連接後端應用程式和上線最佳實踐方面的幫助。

**更高的效能：** 為您的企業提供可靠的數字型驗，提供4種服務可用性選項：99.5%、99.9%、99.95%和99.99%。 此外，它還允許自動備份和多模式災難恢復模型，以幫助確保可靠性和應急管理。

**優化的IT成本：** 主動式指引和專業知識可協助組織隨時掌握最新版AEM。 Adobe白金級維護和支援自動包括在AMS企業/基本的新部署中，提供技術專業知識和操作經驗，以幫助組織維護其關鍵應用程式。 免費的基本Analytics或Target功能提供額外的價值，尤其是對於對分析和個人化需求有限的中端市場組織。

**最高安全性：** 通過在受限訪問設施、防火牆系統後或虛擬專用雲中托管客戶應用程式，確保企業級的物理、網路和資料安全。 它包括單租戶虛擬機，具有強大的資料儲存加密、抗病毒和資料隔離。

**Cloud Manager**:Cloud Manager是Adobe Experience Manager Managed Services產品的一部分，是自助入口網站，可進一步讓組織在雲端中自行管理Adobe Experience Manager。 它包含最新的持續整合和持續傳送(CI/CD)管道，可讓IT團隊和實作合作夥伴加速自訂或更新的傳送，而不會影響效能或安全性。 Cloud Manager僅適用於Adobe托管服務客戶。

若要進一步了解Cloud Manager及其資源，請參閱 [**Cloud Manager使用手冊**](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html).

## 快速入門 {#getting-started}

### 必備條件 {#prerequisites}

雖然生產執行個體通常在執行正式支援作業系統的專用電腦上執行(請參閱 [技術需求](/help/sites-deploying/technical-requirements.md))，則Experience Manager伺服器實際上會在任何支援 [**Java標準版8**](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).

為了熟悉和在AEM上開發，常使用本機電腦上安裝的執行個體(執行Apple OS X或Microsoft Windows或Linux的案頭版本)。

在用戶端上，AEM可搭配所有現代瀏覽器(**Microsoft Edge**, **Internet Explorer** 11, **Chrome **51+** **, **Firefox **47+, **Safari** 8+)。 請參閱 [支援的客戶端平台](/help/sites-deploying/technical-requirements.md#supported-client-platforms) 以取得詳細資訊。

### 獲取軟體 {#getting-the-software}

擁有有效維護與支援合約的客戶應已收到包含程式碼的郵件通知，並可從 [**Adobe授權網站**](https://licensing.adobe.com/). 業務合作夥伴可向 [**spphelp@adobe.com**](mailto:spphelp@adobe.com).

AEM軟體套件提供兩種格式：

* **cq-quickstart-6.5.0.jar:** 獨立執行檔 *jar* 包含啟動和運行所需的一切的檔案。

* **cq-quickstart-6.5.0.war:** A *戰爭* 檔案，用於在第三方應用程式伺服器中部署。

在以下章節中，我們將說明 **獨立安裝**. 如需在應用程式伺服器中安裝AEM的詳細資訊，請參閱 [應用程式伺服器安裝](/help/sites-deploying/application-server-install.md).

### 預設本地安裝 {#default-local-install}

1. 在本地電腦上建立安裝目錄。 例如：

   UNIX安裝位置： **/opt/aem**

   Windows安裝位置： **`C:\Program Files\aem`**

   同樣地，通常將範例執行個體安裝在案頭上的資料夾中。 無論如何，我們通常將此位置稱為：

   `<aem-install>`

   *請注意，檔案目錄的路徑只能包含US ASCII字元。*

1. 放置 **jar** 和**許可證**檔案，此目錄：

   ```shell
   <aem-install>/
       cq-quickstart-6.5.0.jar
       license.properties
   ```

   若您未提供 `license.properties` 檔案，AEM會將您的瀏覽器重新導向至 **歡迎** 螢幕，您可以在其中輸入許可證密鑰。 如果您尚未取得有效的授權金鑰，則需要向Adobe索取有效的授權金鑰。

1. 要在GUI環境中啟動實例，只需按兩下 **`cq-quickstart-6.5.0.jar`** 檔案。

   或者，您也可以從命令列啟動AEM:

   ```shell
       java -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

AEM需要幾分鐘的時間來解壓縮jar檔案、安裝自己，然後啟動。 上述程式會產生：

* an **AEM作者** 執行個體
* 正在運行 **localhost**
* 埠 **4502**

若要存取執行個體，請將瀏覽器指向：

**`https://localhost:4502`**

製作例項中的結果會自動設定為連線至 **發佈例項** on **`localhost:4503`**.

### 製作和發佈安裝 {#author-and-publish-installs}

預設安裝( **作者** 執行個體 **`localhost:4502`**)只需重新命名即可變更 `jar` 檔案，然後再首次啟動。 命名模式為：

**`cq-<instance-type>-p<port-number>.jar`**

例如，將檔案重新命名為

**`cq-author-p4502.jar`**

若啟動，則會導致執行製作例項 **`localhost:4502`**.

同樣地，重新命名和啟動檔案

**`cq-publish-p4503.jar`**

會導致發佈執行個體在上執行 **`localhost:4503`**.

例如，您可以在中安裝這兩個例項

`<aem-install>/author`和

**`<aem-install>/publish`**

如需自訂安裝的詳細資訊，請參閱下列內容：

* [自定義獨立安裝](/help/sites-deploying/custom-standalone-install.md)
* [執行模式](/help/sites-deploying/configure-runmodes.md)

### 未打包的安裝目錄 {#unpacked-install-directory}

當快速啟動jar首次啟動時，它將將自己解壓縮到名為的新子目錄下的同一目錄 `crx-quickstart`. 您最後會得到下列結果：

```xml
<aem-install>/
    license.properties
    cq-quickstart-6.5.0.jar
    crx-quickstart/
        app/
        bin/
        conf/
        launchpad/
        logs/
        metrics/
        monitoring/
        opt/
        repository/
        threaddumps/
        eula-de_DE.html
        eula-en_US.html
        eula-fr_FR.html
        eula-ja_JP.html
        readme.txt
```

如果從UI安裝了實例，則會自動開啟一個瀏覽器窗口，並開啟一個案頭應用程式窗口，顯示實例的主機和埠以及開/關開關：

![啟動螢幕](assets/screen_shot_.png)

>[!NOTE]
>
>如果您使用symlink，請查看 [symlink問題](https://helpx.adobe.com/experience-manager/kb/changing-symlink.html).

### 啟動和停止 {#starting-and-stopping}

當AEM解壓自身並首次啟動後，按兩下安裝目錄中的jar檔案即會啟動執行個體，但不會重新安裝。

要從GUI中停止實例，只需按一下 **開啟/關閉** 在案頭應用程式窗口上切換。

您也可以從命令列停止和啟動AEM。 假設您已首次安裝執行個體，則 **命令行指令碼** 位於此處：

**`<aem-install>/crx-quickstart/bin/`**

此資料夾包含以下Unix bash shell指令碼：

* **`start`**:啟動實例
* `stop`:停止執行個體
* **`status`**:報告執行個體的狀態
* **`quickstart`**:如有需要，可用來設定開始資訊。

也有同等的 **`bat`** 檔案。 如需詳細資訊，請參閱：

* [命令行開始和停止](/help/sites-deploying/command-line-start-and-stop.md)

AEM會啟動網頁瀏覽器，並自動將其重新導向至適當的頁面，通常是登入頁面；例如：

`https://localhost:4502/`

![登入畫面](assets/screen_shot_2019-04-08at83533am.png)

登入後，您即可存取AEM。 如需詳細資訊，請參閱下列內容（視您的角色而定）:

* [製作](/help/sites-authoring/home.md)
* [管理](/help/sites-administering/home.md)
* [開發](/help/sites-developing/home.md)
* [管理](/help/managing/best-practices.md)

## 進階部署 {#advanced-deployment}

上節應能讓您充分了解AEM安裝的基本概念。 不過，安裝完整的AEM生產系統可能會涉及相當複雜的程式。 有關高級安裝的完整資訊，請參見以下子頁：

* [技術需求](/help/sites-deploying/technical-requirements.md)
* [建議的部署](/help/sites-deploying/recommended-deploys.md)
* [自定義獨立安裝](/help/sites-deploying/custom-standalone-install.md)
* [應用程式伺服器安裝](/help/sites-deploying/application-server-install.md)
* [疑難排解](/help/sites-deploying/troubleshooting.md)
* [命令行開始和停止](/help/sites-deploying/command-line-start-and-stop.md)
* [設定](/help/sites-deploying/configuring.md)
* [升級至AEM 6.5](/help/sites-deploying/upgrade.md)
* [電子商務](/help/commerce/cif-classic/deploying/ecommerce.md)
* [設定作法文章](/help/sites-deploying/ht-deploy.md)
* [Web 主控台](/help/sites-deploying/web-console.md)
* [疑難排解復寫](/help/sites-deploying/troubleshoot-rep.md)
* [最佳作法](/help/sites-deploying/best-practices.md)
* [部署社群](/help/communities/deploy-communities.md)
* [AEM Platform簡介](/help/sites-deploying/platform.md)
* [效能准則](/help/sites-deploying/performance-guidelines.md)
* [開始使用AEM Mobile](/help/mobile/getting-started-aem-mobile.md)
* [什麼是AEM Screens?](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/aem-screens-introduction.html)
