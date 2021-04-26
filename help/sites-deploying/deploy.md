---
title: 部署和維護
seo-title: 部署和維護
description: 瞭解如何開始安裝AEM。
seo-description: 瞭解如何開始安裝AEM。
uuid: 4429ac4d-abd7-47d8-b19d-773accb7cc7a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: e48cc0ed-688c-44c8-b6d6-5f3c8593a295
docset: aem65
exl-id: 3df0662a-0768-4b56-8b94-c517657b4bd9
translation-type: tm+mt
source-git-commit: 1cef6f87fa66fd78d439c23e6ac907f9531b8fd6
workflow-type: tm+mt
source-wordcount: '1833'
ht-degree: 3%

---

# 部署和維護{#deploying-and-maintaining}

在本頁中，您會找到：

* [基本概念](#basic-concepts)

   * [什麼AEM?](#what-is-aem)
   * [典型部署](#typical-deployment-scenarios)

      * [內部部署](#on-premise)
      * [Managed Services使用Cloud Manager](#managed-services-using-cloud-manager)

* [快速入門](#getting-started)

   * [必備條件](#prerequisites)
   * [取得軟體](#getting-the-software)
   * [預設本地安裝](#default-local-install)
   * [作者和發佈安裝](#author-and-publish-installs)
   * [解壓縮的安裝目錄](#unpacked-install-directory)
   * [啟動和停止](#starting-and-stopping)

一旦您熟悉了這些基本知識，您將會在下列子頁面中找到更進階和詳細的資訊：

* [技術需求](/help/sites-deploying/technical-requirements.md)
* [建議的部署](/help/sites-deploying/recommended-deploys.md)
* [自訂獨立安裝](/help/sites-deploying/custom-standalone-install.md)
* [應用程式伺服器安裝](/help/sites-deploying/application-server-install.md)
* [疑難排解](/help/sites-deploying/troubleshooting.md)
* [命令行啟動和停止](/help/sites-deploying/command-line-start-and-stop.md)
* [設定](/help/sites-deploying/configuring.md)
* [升級AEM至6.5](/help/sites-deploying/upgrade.md)
* [電子商務](/help/commerce/cif-classic/deploying/ecommerce.md)
* [設定操作說明文章](/help/sites-deploying/ht-deploy.md)
* [Web 主控台](/help/sites-deploying/web-console.md)
* [複製故障排除](/help/sites-deploying/troubleshoot-rep.md)
* [最佳作法](/help/sites-deploying/best-practices.md)
* [部署社群](/help/communities/deploy-communities.md)
* [平台簡AEM介](/help/sites-deploying/platform.md)
* [效能准則](/help/sites-deploying/performance-guidelines.md)
* [開始使用AEM Mobile](/help/mobile/getting-started-aem-mobile.md)
* [什麼是AEM Screens?](https://docs.adobe.com/content/help/zh-Hant/experience-manager-screens/user-guide/aem-screens-introduction.html)

## 基本概念{#basic-concepts}

### 什麼AEM?{#what-is-aem}

Adobe Experience Manager是一套以Web為基礎的用戶端——伺服器系統，用於建立、管理及部署商業網站及相關服務。 它將許多基礎架構級別和應用程式級別的功能結合到單個整合軟體包中。

在基礎架構層AEM級提供：

* **Web應用程式伺服器**:可AEM以部署在獨立模式（它包含整合的Jetty Web伺服器）或作為第三方應用程式伺服器內的Web應用程式。
* **Web應用程式框架**:整AEM合了Sling Web Application Framework，可簡化REST風格、內容導向網頁應用程式的編寫。
* **內容儲存庫**:包AEM含Java內容儲存庫(JCR)，這是專門為非結構化和半結構化資料而設計的分層資料庫類型。儲存庫不僅儲存面向用戶的內容，還儲存應用程式使用的所有代碼、模板和內部資料。

在此基礎上，還AEM提供多種應用程式層級功能，以管理：

* **網站**
* **行動應用程式**
* **數位出版品**
* **表單**
* **數位資產**
* **社群**
* **線上商務**

最後，客戶可以使用這些基礎架構和應用程式層級的建立區塊來建立自訂的解決方案，方法是自行建立應用程式。

伺AEM服器是&#x200B;**Java-based**，並可在支援該平台的大部分作業系統上執行。 與的所AEM有客戶端交互都通過&#x200B;**Web瀏覽器**&#x200B;完成。

### 典型部署方案{#typical-deployment-scenarios}

在術AEM語中，「例項」是在伺服器上執AEM行的副本。 安AEM裝通常至少需要兩個實例，通常運行在不同的電腦上：

* **作者**:用於AEM建立、上傳和編輯內容以及管理網站的例項。內容一旦準備好上線，就會複製到發佈實例。
* **發佈**:為公AEM眾提供已發佈內容的例項。

這些實例與已安裝的軟體相同。 它們僅按配置區分。 此外，大多數安裝都使用調度程式：

* **Dispatcher**:靜態Web伺服器（Apache httpd、Microsoft IIS等）增強了調AEM度器模組。 它會快取由發佈例項產生的網頁，以改善效能。

該系統有許多高級選項和詳細說明，但作者、發佈和調度器的基本模式是大多數部署的核心。 首先，我們將關注一個相對簡單的機構。 下面將討論高級部署選項。

以下幾節將說明這兩種情況：

* **內部部署**:部署AEM並管理在您的公司環境中。

* **Managed Services-Adobe Experience Manager的雲管理員**:由AEMAdobe Managed Services部署和管理。

### 內部部署{#on-premise}

您可以在AEM公司環境中的伺服器上安裝。 典型安裝實例包括：開發、測試和發佈環境。 有關如何讓本機安裝本軟體的基本詳細資訊，請參閱[快速入門](/help/sites-deploying/deploy.md#getting%20started)AEM一節。

要進一步瞭解典型的內部部署，請參閱[建議部署](/help/sites-deploying/recommended-deploys.md)。

### Managed Services使用Cloud Manager {#managed-services-using-cloud-manager}

AEMManaged Services是數位體驗管理的完整解決方案。 它提供雲端體驗傳遞解決方案的優點，同時保留內部部署的所有控制、安全性和自訂優點。 AEMManaged Services公司可讓客戶在雲端部署，並依賴Adobe提供的最佳實務與支援，以更快的速度啟動產品。 企業組織和商業使用者可以在最短的時間內吸引客戶，推動市場份額，並專注於創新的行銷宣傳，同時減輕IT人員的負擔。

有了AEMManaged Services，客戶可以實現以下好處：

**縮短上市時間：有了Adobe Managed Services的** 靈活雲端基礎架構，企業組織可以快速規劃、啟動並最佳化成功的數位體驗。Adobe管理雲端架構，毋需額外的資金、硬體或軟體，Adobe的客戶成功工程師、架構協助、布建、自訂以連線至後端應用程式和上線最佳實務。

**更高的效能：** 提供可靠的數位體驗給您的企業，提供4種服務可用性選項：99.5%、99.9%、99.95%和99.99%。此外，它還允許自動備份和多模式災難恢復模型，以幫助確保可靠性和應急管理。

**優化的IT成本：主** 動指導和專業知識可幫助組織掌握最新版本的資訊AEM。Adobe白金級維護與支援會自動納入AMS企業／基本的新部署中，提供技術專業知識和操作經驗，以協助組織維護其關鍵任務應用程式。 免費的基本Analytics或Target功能可為分析和個人化需求有限的中端市場組織提供額外價值。

**最高安全性：** 將客戶應用程式托管在受限存取的設施、防火牆系統後或虛擬專用雲端，以確保企業級的物理、網路和資料安全。它包含單一租用戶虛擬機，具備強穩的資料儲存加密、抗病毒和資料隔離功能。

**Cloud Manager**:Cloud Manager是Adobe Experience ManagerManaged Services服務的一部分，是自助服務門戶，可讓組織在雲中自行管理Adobe Experience Manager。它包含最新的持續整合與持續傳送(CI/CD)管道，可讓IT團隊與實施合作夥伴加速傳送自訂或更新，而不影響效能或安全性。 Cloud Manager僅適用於Adobe托管服務客戶。

若要進一步瞭解Cloud Manager及其資源，請參閱&#x200B;[**Cloud Manager使用手冊**](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)。

## 快速入門 {#getting-started}

### 必備條件 {#prerequisites}

雖然生產實例通常運行在運行正式支援的作業系統的專用電腦上（請參閱[技術要求](/help/sites-deploying/technical-requirements.md)），但Experience Manager伺服器實際上將運行在支援&#x200B;[**Java標準版8**](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)的任何系統上。

為了熟悉情況並在開發時AEM，常會使用在執行Apple OS X或Microsoft Windows或Linux案頭版本的本機電腦上安裝的執行個體。

在用戶端上，AEM可在桌上型電腦和平板電腦上使用所有最新瀏覽器(**Microsoft Edge**、**Internet Explorer** 11、**Chrome **51+** **、*Firefox **47+、**Safari** 8+)系統。 如需詳細資訊，請參閱[支援的用戶端平台](/help/sites-deploying/technical-requirements.md#supported-client-platforms)。

### 獲取軟體{#getting-the-software}

擁有有效維護與支援合約的客戶應該已收到含有程式碼的郵件通知，AEM並可從&#x200B;[**Adobe授權網站**](https://licensing.adobe.com/)下載。 商業合作夥伴可要求從&#x200B;[**spphelp@adobe.com**](mailto:spphelp@adobe.com)&#x200B;下載存取權。

此軟AEM體套件提供兩種格式：

* **cq-quickstart-6.5.0.jar：獨立執行的** jarfile，包 ** 含啟動和運行所需的一切。

* **cq-quickstart-6.5.0.war：要部署** 在 ** 第三方應用程式伺服器上的warfile。

在以下章節中，我們將介紹&#x200B;**獨立安裝**。 有關在應用程AEM序伺服器中安裝的詳細資訊，請參閱[應用程式伺服器安裝](/help/sites-deploying/application-server-install.md)。

### 預設本地安裝{#default-local-install}

1. 在本機電腦上建立安裝目錄。 例如：

   UNIX安裝位置：**/opt/aem**

   Windows安裝位置：**`C:\Program Files\aem`**

   同樣地，在案頭上的資料夾中安裝範例例項也很常見。 無論如何，我們通常將此位置稱為：

   `<aem-install>`

   *請注意，檔案目錄的路徑必須只包含美國ASCII字元。*

1. 將&#x200B;**jar**&#x200B;和**license **files放在此目錄中：

   ```shell
   <aem-install>/
       cq-quickstart-6.5.0.jar
       license.properties
   ```

   如果您未提供`license.properties`檔案，AEM將在啟動時將瀏覽器重新導向至&#x200B;**歡迎**&#x200B;畫面，您可在此輸入授權金鑰。 如果您尚未取得授權金鑰，您必須向Adobe申請有效的授權金鑰。

1. 要在GUI環境中啟動實例，只需按兩下&#x200B;**`cq-quickstart-6.5.0.jar`**&#x200B;檔案。

   或者，您可從命AEM令行啟動。 對於32位Java VM，請輸入以下內容：

   ```shell
       java -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

   對於64位虛擬機，請輸入：

   ```shell
       java -XX:MaxPermSize=256m -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

要AEM花幾分鐘的時間來解壓縮jar檔案、安裝自己，然後啟動。 上述程式會導致：

* an **AEMauthor** instance
* 運行&#x200B;**localhost**
* 埠&#x200B;**4502**&#x200B;上

若要存取執行個體，請將您的瀏覽器指向：

**`https://localhost:4502`**

將自動配置作者實例的結果，以連接到&#x200B;**`localhost:4503`**&#x200B;上的&#x200B;**publish實例**。

### 作者和發佈安裝{#author-and-publish-installs}

在首次啟動`jar`檔案之前，只需重新命名檔案，即可變更預設安裝（**author**&#x200B;例項在&#x200B;**`localhost:4502`**&#x200B;上）。 命名模式為：

**`cq-<instance-type>-p<port-number>.jar`**

例如，將檔案重新命名為

**`cq-author-p4502.jar`**

而啟動它將導致在&#x200B;**`localhost:4502`**&#x200B;上執行作者例項。

同樣地，重新命名和啟動檔案

**`cq-publish-p4503.jar`**

將導致在&#x200B;**`localhost:4503`**&#x200B;上運行發佈實例。

例如，您可以在

`<aem-install>/author`與

**`<aem-install>/publish`**

如需自訂安裝的詳細資訊，請參閱下列：

* [自訂獨立安裝](/help/sites-deploying/custom-standalone-install.md)
* [執行模式](/help/sites-deploying/configure-runmodes.md)

### 解壓縮安裝目錄{#unpacked-install-directory}

首次啟動快速啟動jar時，它將將其解壓縮到名為`crx-quickstart`的新子目錄下的同一目錄中。 您最後應使用下列功能：

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

如果實例是從UI安裝的，則瀏覽器窗口將自動開啟，案頭應用程式窗口也將開啟，顯示實例的主機和埠以及開／關交換機：

![啟動螢幕](assets/screen_shot_.png)

>[!NOTE]
>
>如果您使用symlinks，請查看symlink](https://helpx.adobe.com/experience-manager/kb/changing-symlink.html)的[問題。

### 啟動和停止{#starting-and-stopping}

解AEM壓縮並首次啟動後，按兩下安裝目錄中的jar檔案只會啟動實例，它不會重新安裝它。

要從GUI中停止實例，只需按一下案頭應用程式窗口中的&#x200B;**開／關**&#x200B;開關即可。

您也可以從命令行AEM停止和啟動。 假設您已首次安裝實例，**命令行指令碼**&#x200B;位於以下位置：

**`<aem-install>/crx-quickstart/bin/`**

此資料夾包含以下Unix bash shell指令碼：

* **`start`**:啟動實例
* `stop`:停止實例
* **`status`**:報告實例的狀態
* **`quickstart`**:用於配置啟動資訊（如果需要）。

此外，還有適用於Windows的等效&#x200B;**`bat`**&#x200B;檔案。 如需詳細資訊，請參閱：

* [命令行啟動和停止](/help/sites-deploying/command-line-start-and-stop.md)

啟AEM動並自動將您的網頁瀏覽器重新導向至適當的頁面，通常是登入頁面；例如：

`https://localhost:4502/`

![登入螢幕](assets/screen_shot_2019-04-08at83533am.png)

登入後，您即可存取AEM。 如需詳細資訊，請視您的角色而定，請參閱下列：

* [製作](/help/sites-authoring/home.md)
* [管理](/help/sites-administering/home.md)
* [開發](/help/sites-developing/home.md)
* [管理](/help/managing/best-practices.md)

## 高級部署{#advanced-deployment}

上節應能讓您充份瞭解安裝的基AEM本概念。 但是，安裝完整的生產系統AEM可能會比較複雜。 如需進階安裝的完整涵蓋範圍，請參閱下列子頁面：

* [技術需求](/help/sites-deploying/technical-requirements.md)
* [建議的部署](/help/sites-deploying/recommended-deploys.md)
* [自訂獨立安裝](/help/sites-deploying/custom-standalone-install.md)
* [應用程式伺服器安裝](/help/sites-deploying/application-server-install.md)
* [疑難排解](/help/sites-deploying/troubleshooting.md)
* [命令行啟動和停止](/help/sites-deploying/command-line-start-and-stop.md)
* [設定](/help/sites-deploying/configuring.md)
* [升級AEM至6.5](/help/sites-deploying/upgrade.md)
* [電子商務](/help/commerce/cif-classic/deploying/ecommerce.md)
* [設定操作說明文章](/help/sites-deploying/ht-deploy.md)
* [Web 主控台](/help/sites-deploying/web-console.md)
* [複製故障排除](/help/sites-deploying/troubleshoot-rep.md)
* [最佳作法](/help/sites-deploying/best-practices.md)
* [部署社群](/help/communities/deploy-communities.md)
* [平台簡AEM介](/help/sites-deploying/platform.md)
* [效能准則](/help/sites-deploying/performance-guidelines.md)
* [開始使用AEM Mobile](/help/mobile/getting-started-aem-mobile.md)
* [什麼是AEM Screens?](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/aem-screens-introduction.html)
