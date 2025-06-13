---
title: 部署和維護
description: 瞭解如何開始安裝AEM。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
docset: aem65
exl-id: 3df0662a-0768-4b56-8b94-c517657b4bd9
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: f96b178ae84b4b930b59e36d4994970682c53dbd
workflow-type: tm+mt
source-wordcount: '1779'
ht-degree: 3%

---

# 部署和維護{#deploying-and-maintaining}

您可以在此頁面找到：

* [基本概念](#basic-concepts)

   * [什麼是AEM？](#what-is-aem)
   * [典型部署](#typical-deployment-scenarios)

      * [內部部署](#on-premise)
      * [使用Cloud Manager的Managed Services](#managed-services-using-cloud-manager)

* [快速入門](#getting-started)

   * [先決條件](#prerequisites)
   * [取得軟體](#getting-the-software)
   * [預設本機安裝](#default-local-install)
   * [製作和發佈安裝](#author-and-publish-installs)
   * [解壓縮的安裝目錄](#unpacked-install-directory)
   * [啟動和停止](#starting-and-stopping)

熟悉這些基本知識後，您就可以在下列子頁面中找到更進階和詳細的資訊：

* [技術需求](/help/sites-deploying/technical-requirements.md)
* [建議的部署](/help/sites-deploying/recommended-deploys.md)
* [自訂獨立安裝](/help/sites-deploying/custom-standalone-install.md)
* [應用程式伺服器安裝](/help/sites-deploying/application-server-install.md)
* [疑難排解](/help/sites-deploying/troubleshooting.md)
* [命令列啟動和停止](/help/sites-deploying/command-line-start-and-stop.md)
* [設定](/help/sites-deploying/configuring.md)
* [升級至AEM 6.5](/help/sites-deploying/upgrade.md)
* [電子商務](/help/commerce/cif-classic/deploying/ecommerce.md)
* [設定作法文章](/help/sites-deploying/ht-deploy.md)
* [Web 控制台](/help/sites-deploying/web-console.md)
* [疑難排解復寫](/help/sites-deploying/troubleshoot-rep.md)
* [最佳實務](/help/sites-deploying/best-practices.md)
* [部署社群](/help/communities/deploy-communities.md)
* [AEM平台簡介](/help/sites-deploying/platform.md)
* [效能准則](/help/sites-deploying/performance-guidelines.md)
* [AEM Mobile快速入門](/help/mobile/getting-started-aem-mobile.md)
* [什麼是AEM Screens？](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html)

## 基本概念 {#basic-concepts}

### 什麼是AEM？ {#what-is-aem}

Adobe Experience Manager是網頁式使用者端伺服器系統，用於建立、管理和部署商業網站及相關服務。 它將數個基礎架構層級和應用程式層級的功能合併為單一整合套件。

在基礎架構層級，AEM提供下列功能：

* **Web應用程式伺服器**： AEM可部署為獨立模式（包含整合式Jetty Web伺服器），或部署為協力廠商應用程式伺服器內的Web應用程式。
* **Web應用程式架構**： AEM整合了Sling Web應用程式架構，可簡化RESTful、內容導向的Web應用程式撰寫。
* **內容存放庫**： AEM包含Java™內容存放庫(JCR)，這是專為非結構化與半結構化資料設計的階層式資料庫型別。 存放庫不僅儲存面向使用者的內容，也儲存應用程式使用的所有程式碼、範本和內部資料。

在此基礎上再接再厲，AEM也提供數種應用程式層級功能，以管理下列專案：

* **網站**
* **行動應用程式**
* **數位出版物**
* **Forms與檔案**
* **數位Assets**
* **社群**
* **線上Commerce**

最後，客戶可以利用這些基礎結構和應用程式層級的建置組塊，透過建置自己的應用程式來建立自訂解決方案。

AEM伺服器是&#x200B;**Java型**，並在支援該平台的大多數作業系統上執行。 所有使用者端與AEM的互動都是透過&#x200B;**網頁瀏覽器**&#x200B;完成。

>[!NOTE]
>
>AEM 6.5 QuickStart提供的最適化Forms功能僅供探索和評估用途。 若要供生產使用，必須獲得 AEM Forms 的有效許可；調適型表單的功能需要適當許可才可使用。

### 典型部署案例 {#typical-deployment-scenarios}

在AEM術語中，「例項」是指在伺服器上執行的AEM副本。 AEM安裝通常至少涉及兩個執行個體，通常在不同電腦上執行：

* **作者**：用來建立、上傳和編輯內容以及管理網站的AEM執行個體。 一旦內容準備好上線，就會將其復寫到發佈執行個體。
* **發佈**：將發佈的內容提供給公用的AEM執行個體。

這些例項在安裝軟體方面是相同的。 它們僅能透過設定來區分。 此外，大部分安裝都使用Dispatcher：

* **Dispatcher**：靜態網頁伺服器(Apache httpd、Microsoft®IIS等)已透過AEM Dispatcher模組增強。 它快取發佈執行個體產生的網頁以提升效能。

此設定有許多進階選項和詳細說明，但製作者、發佈和Dispatcher的基本模式是大多數部署的核心。 讓我們從簡單的設定開始。 接著會討論進階部署選項。

以下各節將說明這兩種情況：

* **內部部署**： AEM已在您的公司環境中部署和管理。

* **Managed Services - Adobe Experience Manager適用的Cloud Manager**：Adobe Managed Services所部署和管理的AEM。

### 內部部署 {#on-premise}

您可以在公司環境的伺服器上安裝AEM。 典型的安裝例項包括：開發、測試和發佈環境。 請參閱[快速入門](/help/sites-deploying/deploy.md#getting%20started)，瞭解如何取得AEM軟體以在本機安裝。

若要進一步瞭解一般內部部署，請參閱[建議的部署](/help/sites-deploying/recommended-deploys.md)。

### 使用Cloud Manager的Managed Services {#managed-services-using-cloud-manager}

AEM Managed Services是數位體驗管理的完整解決方案。 它提供雲端體驗傳送解決方案的優點，同時保留內部部署的所有控制、安全性和自訂優點。 AEM Managed Services可讓客戶透過在雲端部署，並借鑑Adobe的最佳實務和支援，以更快的速度啟動。 組織和業務使用者可在最短的時間內與客戶互動、提高市場份額，並專注於建立創新的行銷活動，同時減輕IT負擔。

透過AEM Managed Services，客戶可獲得下列優點：

**加快上市時間：**&#x200B;透過Adobe Managed Services的彈性雲端基礎結構，組織可以快速規劃、啟動及最佳化成功的數位體驗。 Adobe可管理雲端架構，不需額外資金、硬體或軟體，而Adobe的客戶解決方案工程師可協助完成AEM架構、布建、連線後端應用程式的自訂功能，以及上線最佳作法。

**更高的效能：**&#x200B;提供99.5%、99.9%、99.95%和99.99%四種服務可用性選項，為您的企業提供可靠的數位體驗。 此外，它還可提供自動備份和多模式災難回覆模式，協助確保可靠性和應急管理。

**最佳化的IT成本：**&#x200B;主動式指引和專業知識可協助組織隨時掌握最新版AEM的最新資訊。 Adobe白金級維護和支援會自動包含在AMS Enterprise/Basic的新部署中，提供技術專業和營運經驗，以協助組織維護其關鍵任務應用程式。 免費基本Analytics或Target功能提供額外價值，特別適用於對分析和個人化需求有限的中端市場組織。

**最高安全性：**&#x200B;將客戶應用程式託管於受限制的存取設施、防火牆系統後面或虛擬私人雲端，確保企業級實體、網路和資料安全性。 它包含單一租使用者虛擬機器器，提供強大的資料儲存加密、防毒軟體和資料隔離功能。

**Cloud Manager**： Cloud Manager是Adobe Experience Manager Managed Services產品的一部分，也是一個自助服務入口網站，可進一步讓組織在雲端中自行管理Adobe Experience Manager。 其中包括最先進的持續整合和持續傳遞(CI/CD)管道，可讓IT團隊與實作合作夥伴加速自訂或更新的傳遞，而不會影響效能或安全性。 Cloud Manager僅適用於Adobe Managed Service客戶。

若要進一步瞭解Cloud Manger及其資源，請參閱&#x200B;[**Cloud Manager使用手冊**](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html)。

## 快速入門 {#getting-started}

### 先決條件 {#prerequisites}

雖然生產執行個體是在執行官方支援作業系統的專用電腦上執行（請參閱[技術需求](/help/sites-deploying/technical-requirements.md)），但Experience Manager伺服器實際上會在任何支援&#x200B;[**Java™ Standard Edition 8**](https://www.oracle.com/java/technologies/downloads/#java8)的系統上執行。

為了熟悉和開發AEM，通常會使用安裝在執行Apple OS X或Microsoft® Windows或Linux®案頭版本的本機電腦上的執行個體。

在使用者端上，AEM可在桌上型電腦及平板電腦作業系統上與所有現代瀏覽器(**Microsoft® Edge**、**Internet Explorer** 11、**Chrome &#x200B;** 51+**&#x200B;**、**Firefox &#x200B;** 47+、**Safari** 8+)搭配使用。 如需詳細資訊，請參閱[支援的使用者端平台](/help/sites-deploying/technical-requirements.md#supported-client-platforms)。

### 取得軟體 {#getting-the-software}

持有有效維護與支援合約的客戶應已收到內含程式碼的郵件通知，並可從&#x200B;[**Adobe授權網站**](https://licensing.adobe.com/)下載AEM。 業務夥伴可以向&#x200B;[**spphelp@adobe.com**](mailto:spphelp@adobe.com)&#x200B;要求下載存取權。

AEM軟體套件有兩種形式：

* **cq-quickstart-6.5.0.jar：**&#x200B;獨立的可執行檔&#x200B;*jar*&#x200B;檔案，包含您需要執行的所有專案。

* **cq-quickstart-6.5.0.war：**&#x200B;在協力廠商應用程式伺服器中部署的&#x200B;*war*&#x200B;檔案。

在以下章節中，我們將說明&#x200B;**獨立安裝**。 如需在應用程式伺服器中安裝AEM的詳細資訊，請參閱[應用程式伺服器安裝](/help/sites-deploying/application-server-install.md)。

### 預設本機安裝 {#default-local-install}

1. 在本機電腦上建立安裝目錄。 例如：

   UNIX®安裝位置： **/opt/aem**

   Windows安裝位置： **`C:\Program Files\aem`**

   同樣地，將範例執行個體直接安裝在案頭上的資料夾中也是很常見的做法。 無論如何，Adobe一般會將此位置稱為：

   `<aem-install>`

   *檔案目錄的路徑只能包含美國ASCII字元。*

1. 將&#x200B;**jar**&#x200B;和&#x200B;**license**&#x200B;檔案放置在此目錄中：

   ```shell
   <aem-install>/
       cq-quickstart-6.5.0.jar
       license.properties
   ```

   如果您未提供`license.properties`檔案，AEM會在啟動時將瀏覽器重新導向至&#x200B;**歡迎**&#x200B;畫面，您可以在其中輸入授權金鑰。 如果您還沒有授權金鑰，則需要向Adobe索取有效的授權金鑰。

1. 若要在GUI環境中啟動執行個體，請連按兩下&#x200B;**`cq-quickstart-6.5.0.jar`**&#x200B;檔案。

   或者，您可以從命令列啟動AEM：

   ```shell
       java -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

AEM需要幾分鐘來解壓縮jar檔案、自行安裝並啟動。 上述程式會產生：

* **AEM作者**&#x200B;執行個體
* 正在&#x200B;**localhost**&#x200B;上執行
* 在連線埠&#x200B;**4502**&#x200B;上

若要存取執行個體，請將瀏覽器指向：

**`https://localhost:4502`**

作者執行個體中的結果將會自動設定為連線到&#x200B;**`localhost:4503`**&#x200B;上的&#x200B;**發佈執行個體**。

### 製作和發佈安裝 {#author-and-publish-installs}

預設安裝（在&#x200B;**`localhost:4502`**&#x200B;上的&#x200B;**作者**&#x200B;執行個體）只需在第一次啟動`jar`檔案之前重新命名檔案即可變更。 命名模式為：

**`cq-<instance-type>-p<port-number>.jar`**

例如，將檔案重新命名為

**`cq-author-p4502.jar`**

啟動後，會在&#x200B;**`localhost:4502`**&#x200B;上執行製作執行個體。

同樣地，重新命名和啟動檔案

**`cq-publish-p4503.jar`**

導致發佈執行個體在&#x200B;**`localhost:4503`**&#x200B;上執行。

例如，您可將這兩個例項安裝在中

`<aem-install>/author`和

**`<aem-install>/publish`**

如需自訂安裝的詳細資訊，請參閱下列內容：

* [自訂獨立安裝](/help/sites-deploying/custom-standalone-install.md)
* [執行模式](/help/sites-deploying/configure-runmodes.md)

### 解壓縮的安裝目錄 {#unpacked-install-directory}

第一次啟動快速入門jar時，它會在名為`crx-quickstart`的新子目錄下將自身解壓縮到相同的目錄中。 您應該具備下列條件：

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

如果從UI安裝執行個體，瀏覽器視窗會自動開啟，案頭應用程式視窗也會開啟，顯示執行個體的主機和連線埠，以及開啟/關閉開關：

![啟動畫面](assets/screen_shot_.png)

### 啟動和停止 {#starting-and-stopping}

當AEM自行解壓縮並首次啟動後，在安裝目錄中連按兩下jar檔案即可啟動執行個體，但不會重新安裝。

若要從GUI停止執行個體，請按一下案頭應用程式視窗上的&#x200B;**開啟/關閉**&#x200B;開關。

您也可以從命令列停止和啟動AEM。 假設您已經第一次安裝執行個體，**命令列指令碼**&#x200B;就在這裡：

**`<aem-install>/crx-quickstart/bin/`**

此資料夾包含下列UNIX® bash shell指令碼：

* **`start`**：啟動執行個體
* `stop`：停止執行個體
* **`status`**：報告執行個體的狀態
* **`quickstart`**：用來設定啟動資訊（如有必要）。

也有等同於Windows的&#x200B;**`bat`**&#x200B;檔案。 如需詳細資訊，請參閱：

* [命令列啟動和停止](/help/sites-deploying/command-line-start-and-stop.md)

AEM會啟動，並自動將您的網頁瀏覽器重新導向至適當的頁面，通常是登入頁面；例如：

`https://localhost:4502/`

![登入畫面](assets/screen_shot_2019-04-08at83533am.png)

登入後，您就能存取AEM。 如需詳細資訊，請參閱下列內容（視您的角色而定）：

* [製作](/help/sites-authoring/first-steps.md)
* [管理](/help/sites-administering/home.md)
* [開發](/help/sites-developing/getting-started.md)
* [管理](/help/managing/best-practices.md)

## 進階部署 {#advanced-deployment}

上節應能讓您充分瞭解AEM安裝的基本概念。 不過，安裝AEM的完整生產系統可能會相當複雜。 如需進階安裝的完整涵蓋範圍，請參閱下列子頁面：

* [技術需求](/help/sites-deploying/technical-requirements.md)
* [建議的部署](/help/sites-deploying/recommended-deploys.md)
* [自訂獨立安裝](/help/sites-deploying/custom-standalone-install.md)
* [應用程式伺服器安裝](/help/sites-deploying/application-server-install.md)
* [疑難排解](/help/sites-deploying/troubleshooting.md)
* [命令列啟動和停止](/help/sites-deploying/command-line-start-and-stop.md)
* [設定](/help/sites-deploying/configuring.md)
* [升級至AEM 6.5](/help/sites-deploying/upgrade.md)
* [電子商務](/help/commerce/cif-classic/deploying/ecommerce.md)
* [設定作法文章](/help/sites-deploying/ht-deploy.md)
* [Web 控制台](/help/sites-deploying/web-console.md)
* [疑難排解復寫](/help/sites-deploying/troubleshoot-rep.md)
* [最佳實務](/help/sites-deploying/best-practices.md)
* [部署社群](/help/communities/deploy-communities.md)
* [AEM平台簡介](/help/sites-deploying/platform.md)
* [效能准則](/help/sites-deploying/performance-guidelines.md)
* [AEM Mobile快速入門](/help/mobile/getting-started-aem-mobile.md)
* [什麼是AEM Screens？](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html)
