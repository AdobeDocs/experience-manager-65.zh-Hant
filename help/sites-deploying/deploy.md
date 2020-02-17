---
title: 部署和維護
seo-title: 部署和維護
description: 瞭解如何開始使用AEM安裝。
seo-description: 瞭解如何開始使用AEM安裝。
uuid: 4429ac4d-abd7-47d8-b19d-773accb7cc7a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: e48cc0ed-688c-44c8-b6d6-5f3c8593a295
docset: aem65
translation-type: tm+mt
source-git-commit: b827c8acb1db158060d209c819fc72ffbfeca65f

---


# 部署和維護{#deploying-and-maintaining}

在本頁中，您會找到：

* [基本概念](#basic-concepts)

   * [什麼是AEM?](#what-is-aem)
   * [典型部署](#typical-deployment-scenarios)

      * [內部部署](#on-premise)
      * [使用Cloud manager的受管理服務](#managed-services-using-cloud-manager)

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
* [升級至AEM 6.5](/help/sites-deploying/upgrade.md)
* [電子商務](/help/sites-deploying/ecommerce.md)
* [設定操作說明文章](/help/sites-deploying/ht-deploy.md)
* [Web 控制台](/help/sites-deploying/web-console.md)
* [複製故障排除](/help/sites-deploying/troubleshoot-rep.md)
* [最佳實務](/help/sites-deploying/best-practices.md)
* [部署社群](/help/communities/deploy-communities.md)
* [AEM平台簡介](/help/sites-deploying/platform.md)
* [效能准則](/help/sites-deploying/performance-guidelines.md)
* [AEM mobile快速入門](/help/mobile/getting-started-aem-mobile.md)
* [更新發行工具定義](/help/sites-deploying/update-release-vehicle-definitions.md)
* [什麼是AEM Screens?](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/aem-screens-introduction.html)

## 基本概念 {#basic-concepts}

### 什麼是AEM? {#what-is-aem}

Adobe Experience manager是一套基於Web的主從式系統，用於建立、管理和部署商業網站及相關服務。 它將許多基礎架構級別和應用程式級別的功能結合到單個整合軟體包中。

在基礎架構層級，AEM提供下列功能：

* **Web應用程式伺服器**:AEM可部署在獨立模式（其中包含整合的Jetty網頁伺服器），或部署為協力廠商應用程式伺服器內的網頁應用程式。
* **Web應用程式框架**:AEM整合了Sling Web Application Framework，可簡化REST風格、內容導向網頁應用程式的編寫。
* **內容儲存庫**:AEM包含Java內容儲存庫(JCR)，這是一種階層式資料庫，專為非結構化和半結構化資料而設計。 儲存庫不僅儲存面向用戶的內容，還儲存應用程式使用的所有代碼、模板和內部資料。

AEM也以此為基礎，提供許多應用程式層級的功能，以管理：

* **網站**
* **行動應用程式**
* **數位出版品**
* **表單**
* **數位資產**
* **社群**
* **線上商務**

最後，客戶可以使用這些基礎架構和應用程式層級的建立區塊來建立自訂的解決方案，方法是自行建立應用程式。

AEM伺服器是以 **Java為基礎** ，並可在支援該平台的大部分作業系統上執行。 所有與AEM的用戶端互動都是透過網頁瀏 **覽器完成**。

### 典型部署方案 {#typical-deployment-scenarios}

在AEM術語中，「例項」是伺服器上執行的AEM復本。 AEM安裝通常至少需要兩個例項，通常在不同的電腦上執行：

* **作者**:用於建立、上傳和編輯內容以及管理網站的AEM例項。 內容一旦準備好上線，就會複製到發佈實例。
* **發佈**:為公眾提供已發佈內容的AEM例項。

這些實例與已安裝的軟體相同。 它們僅按配置區分。 此外，大多數安裝都使用調度程式：

* **Dispatcher**:靜態Web伺服器（Apache httpd、Microsoft IIS等）已擴充至AEM Dispatcher模組。 它會快取由發佈例項產生的網頁，以改善效能。

該系統有許多高級選項和詳細說明，但作者、發佈和調度器的基本模式是大多數部署的核心。 首先，我們將關注一個相對簡單的機構。 下面將討論高級部署選項。

以下幾節將說明這兩種情況：

* **內部部署**:AEM已部署並管理在您的公司環境中。

* **受管理服務——適用於Adobe Experience Manager的Cloud Manager**:由Adobe Managed services部署和管理的AEM。

### On-premise {#on-premise}

您可以在公司環境的伺服器上安裝AEM。 典型安裝實例包括：開發、測試和發佈環境。 如需如何讓AEM軟 [](/help/sites-deploying/deploy.md#getting%20started) 體在本機安裝的基本詳細資訊，請參閱「快速入門」一節。

若要進一步瞭解典型的內部部署，請參閱建議 [的部署](/help/sites-deploying/recommended-deploys.md)。

### 使用Cloud manager的受管理服務 {#managed-services-using-cloud-manager}

AEM Managed services是數位體驗管理的完整解決方案。 它提供雲端體驗傳遞解決方案的優點，同時保留內部部署的所有控制、安全性和自訂優點。 AEM Managed services可讓客戶透過部署在雲端，以及依賴Adobe的最佳實務與支援，以更快速地啟動產品。 企業組織和商業使用者可以在最短的時間內吸引客戶，推動市場份額，並專注於創新的行銷宣傳，同時減輕IT人員的負擔。

有了AEM Managed Services，客戶就可以獲得下列好處：

**** 縮短上市時間：有了Adobe Managed services的靈活雲端基礎架構，企業組織可以快速規劃、啟動並最佳化成功的數位體驗。 Adobe管理雲端架構時不需額外的資金、硬體或軟體，Adobe的客戶成功工程師可協助您處理AEM架構、布建、自訂以連接至後端應用程式和上線最佳實務。

**** 更高的效能：提供可靠的數位體驗，包括4個服務可用性選項：99.5%、99.9%、99.95%和99.99%。 此外，它還允許自動備份和多模式災難恢復模型，以幫助確保可靠性和應急管理。

**** 優化的IT成本：主動引導和專業知識可協助組織掌握最新版AEM。 Adobe白金級維護與支援會自動納入AMS企業／基礎的新部署，提供技術專業知識和營運經驗，以協助組織維護其關鍵任務應用程式。 免費的基本Analytics或Target功能可為分析和個人化需求有限的中端市場組織提供額外價值。

**** 最高安全性：將客戶應用程式托管在受限存取的設施、防火牆系統後或虛擬專用雲端，以確保企業級的物理、網路和資料安全。 它包含單一租用戶虛擬機，具備強穩的資料儲存加密、抗病毒和資料隔離功能。

**Cloud Manager**:Cloud Manager是Adobe Experience Manager Managed services產品的一部分，是自助服務入口網站，可讓組織在雲端自行管理Adobe Experience Manager。 它包含最新的持續整合與持續傳送(CI/CD)管道，可讓IT團隊與實施合作夥伴加速傳送自訂或更新，而不影響效能或安全性。 Cloud manager僅適用於Adobe Managed service客戶。

若要進一步瞭解Cloud Manager及其資源，請參閱 [**Cloud Manager使用指南&#x200B;**](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)。

## 快速入門 {#getting-started}

### 必備條件 {#prerequisites}

雖然生產例項通常在執行正式支援作業系統的專用機器上執行(請參閱 [Technical Requirements](/help/sites-deploying/technical-requirements.md))，但Experience Manager伺服器實際上將可在支援 [**Java Standard Edition 8的任何系統上執行&#x200B;**](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)。

為了熟悉情況並在AEM上開發，您很常會使用安裝在執行Apple OS x或Microsoft windows或Linux案頭版本之本機電腦上的執行個體。

在用戶端上，AEM可與所有現代瀏覽器(**Microsoft Edge**、 **Internet Explorer** 11、**Chrome51+ ***、**Firefox *47+、****** SafariExplore 8+)搭配使用，並可在桌上型電腦和平板電腦作業系統上運作。 如需詳 [細資訊，請參閱支援的](/help/sites-deploying/technical-requirements.md#supported-client-platforms) 「用戶端平台」。

### 取得軟體 {#getting-the-software}

擁有有效維護與支援合約的客戶應該已收到含有程式碼的電子郵件通知，並可從 [**Adobe授權網站下載AEM **](https://licensing.adobe.com/)。 商業合作夥伴可要求從spphelp@adobe.com取得下載[**存取權**](mailto:spphelp@adobe.com)。

AEM軟體套件提供兩種格式：

* **** cq-quickstart-6.5.0.jar:獨立的可執 *行檔案* jar檔案，包含啟動和運行所需的一切。

* **** cq-quickstart-6.5.0.war:用於 *在協力廠商* （協力廠商）應用程式伺服器中部署的war檔案。

在下節中，我們將說明獨立 **安裝**。 如需在應用程式伺服器中安裝AEM的詳細資訊，請參閱「應用 [程式伺服器安裝」](/help/sites-deploying/application-server-install.md)。

### 預設本地安裝 {#default-local-install}

1. 在本機電腦上建立安裝目錄。 例如：

   UNIX安裝位置： **/opt/aem**

   Windows安裝位置： **`C:\Program Files\aem`**

   同樣地，在案頭上的資料夾中安裝範例例項也很常見。 無論如何，我們通常將此位置稱為：

   `<aem-install>`

   *請注意，檔案目錄的路徑必須只包含美國ASCII字元。*

1. 將 **jar** 和**license **files放入此目錄：

   ```shell
   <aem-install>/
       cq-quickstart-6.5.0.jar
       license.properties
   ```

   如果您未提供檔 `license.properties` 案，AEM會在啟動時將瀏覽器重新導向至「歡迎 **** 」畫面，您可以在其中輸入授權金鑰。 如果您尚未向Adobe索取有效的授權金鑰，則需向Adobe索取。

1. 要在GUI環境中啟動實例，只需按兩下該文 **`cq-quickstart-6.5.0.jar`** 件。

   或者，您可以從命令列啟動AEM。 對於32位Java VM，請輸入以下內容：

   ```shell
       java -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

   對於64位虛擬機，請輸入：

   ```shell
       java -XX:MaxPermSize=256m -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

AEM需要幾分鐘的時間才能解壓縮jar檔案、自行安裝並啟動。 上述程式會導致：

* an **AEM author** instance
* 在localhost上運 **行**
* 在埠 **4502上**

若要存取執行個體，請將您的瀏覽器指向：

**`https://localhost:4502`**

作者實例的結果將自動配置為連接到上的 **發佈實例****`localhost:4503`**。

### 作者和發佈安裝 {#author-and-publish-installs}

只需在首次啟 **動檔案前重新命名檔案，即可****`localhost:4502`**`jar` 變更預設安裝（作者例項）。 命名模式為：

**`cq-<instance-type>-p<port-number>.jar`**

例如，將檔案重新命名為

**`cq-author-p4502.jar`**

而啟動它將會產生一個作者執行個體 **`localhost:4502`**。

同樣地，重新命名和啟動檔案

**`cq-publish-p4503.jar`**

將導致在上運行發佈實例 **`localhost:4503`**。

例如，您可以在

`<aem-install>/author`與

**`<aem-install>/publish`**

如需自訂安裝的詳細資訊，請參閱下列：

* [自訂獨立安裝](/help/sites-deploying/custom-standalone-install.md)
* [執行模式](/help/sites-deploying/configure-runmodes.md)

### 解壓縮的安裝目錄 {#unpacked-install-directory}

首次啟動快速啟動jar時，它將將其解壓縮到名為的新子目錄下的同一目錄中 `crx-quickstart`。 您最後應使用下列功能：

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
>如果您使用symlinks，請查看symlink [的問題](https://helpx.adobe.com/experience-manager/kb/changing-symlink.html)。

### 啟動和停止 {#starting-and-stopping}

當AEM已解壓縮並首次啟動後，連按兩下安裝目錄中的jar檔案，只會啟動執行個體，但不會重新安裝它。

要從GUI中停止實例，只需按一下案頭應 **用程式窗口上的** 「開／關」開關。

您也可以從命令列停止和啟動AEM。 假設您已首次安裝實例，則命 **令行指令碼位於** :

**`<aem-install>/crx-quickstart/bin/`**

此資料夾包含以下Unix bash shell指令碼：

* **`start`**:啟動實例
* `stop`:停止實例
* **`status`**:報告實例的狀態
* **`quickstart`**:用於配置啟動資訊（如果需要）。

此外，Windows也有相 **`bat`** 當的檔案。 如需詳細資訊，請參閱：

* [命令行啟動和停止](/help/sites-deploying/command-line-start-and-stop.md)

AEM會啟動您的網頁瀏覽器並自動將其重新導向至適當的頁面，通常是登入頁面；例如：

`https://localhost:4502/`

![登入螢幕](assets/screen_shot_2019-04-08at83533am.png)

登入後，您就可以存取AEM。 如需詳細資訊，請視您的角色而定，請參閱下列：

* [製作](/help/sites-authoring/home.md)
* [管理](/help/sites-administering/home.md)
* [開發](/help/sites-developing/home.md)
* [管理](/help/managing/best-practices.md)

## 進階部署 {#advanced-deployment}

上節應能讓您充份瞭解AEM安裝的基本概念。 不過，安裝完整的AEM生產系統可能會比較複雜。 如需進階安裝的完整涵蓋範圍，請參閱下列子頁面：

* [技術需求](/help/sites-deploying/technical-requirements.md)
* [建議的部署](/help/sites-deploying/recommended-deploys.md)
* [自訂獨立安裝](/help/sites-deploying/custom-standalone-install.md)
* [應用程式伺服器安裝](/help/sites-deploying/application-server-install.md)
* [疑難排解](/help/sites-deploying/troubleshooting.md)
* [命令行啟動和停止](/help/sites-deploying/command-line-start-and-stop.md)
* [設定](/help/sites-deploying/configuring.md)
* [升級至AEM 6.5](/help/sites-deploying/upgrade.md)
* [電子商務](/help/sites-deploying/ecommerce.md)
* [設定操作說明文章](/help/sites-deploying/ht-deploy.md)
* [Web 控制台](/help/sites-deploying/web-console.md)
* [複製故障排除](/help/sites-deploying/troubleshoot-rep.md)
* [最佳實務](/help/sites-deploying/best-practices.md)
* [部署社群](/help/communities/deploy-communities.md)
* [AEM平台簡介](/help/sites-deploying/platform.md)
* [效能准則](/help/sites-deploying/performance-guidelines.md)
* [AEM mobile快速入門](/help/mobile/getting-started-aem-mobile.md)
* [更新發行工具定義](/help/sites-deploying/update-release-vehicle-definitions.md)
* [什麼是AEM Screens?](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/aem-screens-introduction.html)

