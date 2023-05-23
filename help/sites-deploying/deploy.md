---
title: 部署和維護
seo-title: Deploying and Maintaining
description: 瞭解如何開始安AEM裝。
seo-description: Learn how to get started with the AEM installation.
uuid: 4429ac4d-abd7-47d8-b19d-773accb7cc7a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: e48cc0ed-688c-44c8-b6d6-5f3c8593a295
docset: aem65
exl-id: 3df0662a-0768-4b56-8b94-c517657b4bd9
source-git-commit: 9052ed3e89fdc67d94fc60bbff64d42255565767
workflow-type: tm+mt
source-wordcount: '1802'
ht-degree: 3%

---

# 部署和維護{#deploying-and-maintaining}

在此頁中，您將找到：

* [基本概念](#basic-concepts)

   * [什麼AEM?](#what-is-aem)
   * [典型部署](#typical-deployment-scenarios)

      * [內部部署](#on-premise)
      * [Managed Services使用雲管理器](#managed-services-using-cloud-manager)

* [快速入門](#getting-started)

   * [必備條件](#prerequisites)
   * [獲取軟體](#getting-the-software)
   * [預設本地安裝](#default-local-install)
   * [作者和發佈安裝](#author-and-publish-installs)
   * [未打包的安裝目錄](#unpacked-install-directory)
   * [啟動和停止](#starting-and-stopping)

熟悉這些基本知識後，您將在以下子頁中找到更高級和詳細資訊：

* [技術要求](/help/sites-deploying/technical-requirements.md)
* [建議的部署](/help/sites-deploying/recommended-deploys.md)
* [自定義獨立安裝](/help/sites-deploying/custom-standalone-install.md)
* [應用程式伺服器安裝](/help/sites-deploying/application-server-install.md)
* [疑難排解](/help/sites-deploying/troubleshooting.md)
* [命令行啟動和停止](/help/sites-deploying/command-line-start-and-stop.md)
* [設定](/help/sites-deploying/configuring.md)
* [升級AEM到6.5](/help/sites-deploying/upgrade.md)
* [電子商務](/help/commerce/cif-classic/deploying/ecommerce.md)
* [配置How-To文章](/help/sites-deploying/ht-deploy.md)
* [Web 主控台](/help/sites-deploying/web-console.md)
* [排除複製故障](/help/sites-deploying/troubleshoot-rep.md)
* [最佳做法](/help/sites-deploying/best-practices.md)
* [部署社區](/help/communities/deploy-communities.md)
* [平台簡AEM介](/help/sites-deploying/platform.md)
* [效能指南](/help/sites-deploying/performance-guidelines.md)
* [AEM Mobile入門](/help/mobile/getting-started-aem-mobile.md)
* [什麼是AEM Screens?](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html)

## 基本概念 {#basic-concepts}

### 什麼AEM? {#what-is-aem}

Adobe Experience Manager是一個基於Web的客戶端 — 伺服器系統，用於構建、管理和部署商業網站及相關服務。 它將許多基礎架構級和應用程式級功能合併到一個整合的軟體包中。

在基礎架構級AEM別提供以下內容：

* **Web應用程式伺服器**:可以AEM以獨立模式（包括整合的Jetty Web伺服器）或作為第三方應用程式伺服器中的Web應用程式進行部署。
* **Web應用程式框架**:採AEM用Sling Web應用程式框架，簡化了REST風格、面向內容的Web應用程式的編寫。
* **內容儲存庫**:包AEM括Java內容儲存庫(JCR)，這是一種專門為非結構化和半結構化資料而設計的分層資料庫。 儲存庫不僅儲存面向用戶的內容，還儲存應用程式使用的所有代碼、模板和內部資料。

在此基礎上，還AEM提供了許多應用程式級功能，用於管理：

* **網站**
* **移動應用**
* **數字出版物**
* **Forms**
* **數位資產**
* **社群**
* **線上商務**

最後，客戶可以使用這些基礎架構和應用程式級構建塊通過構建自己的應用程式來建立定製的解決方案。

服AEM務器 **基於Java** 並運行於大多數支援該平台的作業系統。 與的所有客戶端AEM交互都通過 **web瀏覽器**。

### 典型部署方案 {#typical-deployment-scenarios}

在AEM術語中，「實例」是伺服器上運AEM行的副本。 安AEM裝通常至少涉及兩個實例，通常在不同的電腦上運行：

* **作者**:用於AEM建立、上載和編輯內容以及管理網站的實例。 一旦內容準備好投入使用，就會將其複製到發佈實例。
* **發佈**:向公AEM眾提供已發佈內容的實例。

這些實例與已安裝的軟體相同。 它們僅按配置來區分。 此外，大多數安裝都使用調度程式：

* **調度程式**:靜態Web伺服器(Apache httpd、MicrosoftIIS等) 與調度器模AEM塊一起擴展。 它快取發佈執行個體產生的網頁以提升效能。

此設定有許多高級選項和詳細說明，但大多數部署的核心是作者、發佈和調度器的基本模式。 我們首先將關注一個相對簡單的設定。 下面將討論高級部署選項。

以下各節介紹了兩種方案：

* **內部部署**:在AEM您的公司環境中部署和管理。

* **Managed Services-Adobe Experience Manager雲經理**:由AEMAdobe Managed Services部署和管理。

### 內部部署 {#on-premise}

您可以在AEM企業環境中的伺服器上安裝。 典型安裝實例包括：開發、測試和發佈環境。 請參閱 [入門](/help/sites-deploying/deploy.md#getting%20started) 部分，瞭解有關如何使軟體AEM本地安裝的基本詳細資訊。

要瞭解有關典型內部部署的詳細資訊，請參閱 [建議的部署](/help/sites-deploying/recommended-deploys.md)。

### Managed Services使用雲管理器 {#managed-services-using-cloud-manager}

AEMManaged Services是數字型驗管理的完整解決方案。 它提供了雲中體驗交付解決方案的優勢，同時保留了內部部署的所有控制、安全和定制優勢。 AEMManaged Services通過在雲上部署以及依靠Adobe提供的最佳實踐和支援使客戶能夠更快地啟動。 企業和業務用戶可以在最短的時間內與客戶接洽，擴大市場份額，並專注於建立創新的營銷活動，同時減輕IT負擔。

通過AEMManaged Services客戶可以實現以下好處：

**加快上市時間：** 借助Adobe Managed Services的靈活雲基礎架構，組織可以快速規劃、啟動和優化成功的數字型驗。 Adobe管理雲架構，無需額外的資金、硬體或軟體，並幫助Adobe的客戶解決方案工程師AEM、架構、配置、定制以連接到後端應用和上線最佳實踐。

**更高的效能：** 通過四個服務可用性選項（99.5% 、 99.9% 、 99.95%和99.99%）為您的業務提供可靠的數字型驗。 此外，它還允許自動備份和多模式災難恢復模式，以幫助確保可靠性和應急管理。

**優化的IT成本：** 前瞻性的指導和專業知識可幫助組織保持最新版本AEM。 Adobe白金維護和支援自動包括在AMS Enterprise/Basic的新部署中，提供技術專業知識和操作經驗，以幫助組織維護其關鍵應用程式。 免費的基本分析或目標功能為分析和個性化需求有限的中端市場組織提供了附加價值。

**最高安全性：** 通過在受限訪問設施、防火牆系統後或虛擬專用雲內托管客戶應用程式，確保企業級物理、網路和資料安全。 它包括單租戶虛擬機，具有強健的資料儲存加密、抗病毒和資料隔離。

**雲管理器**:Cloud Manager是Adobe Experience ManagerManaged Services產品的一部分，它是自助服務門戶，使組織能夠在雲中自我管理Adobe Experience Manager。 它包括最先進的連續整合和連續交付(CI/CD)管道，使IT團隊和實施合作夥伴能夠加快定制或更新的交付，而不影響效能或安全性。 Cloud Manager僅適用於Adobe托管服務客戶。

要瞭解有關雲管理器及其資源的詳細資訊，請參閱 [**《 Cloud Manager使用手冊》**](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html)。

## 快速入門 {#getting-started}

### 必備條件 {#prerequisites}

雖然生產實例通常在運行正式支援的作業系統的專用電腦上運行(請參見 [技術要求](/help/sites-deploying/technical-requirements.md)),Experience Manager伺服器將實際運行在支援 [**Java標準版8**](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)。

為了熟悉和在上開發，AEM通常使用本地電腦上安裝的實例運行AppleOS X或MicrosoftWindows或Linux的案頭版本。

在客戶端，可與所AEM有現代瀏覽器(**Microsoft邊**。 **Internet Explorer** 11, **鉻 **51+** **、**Firefox **47+, **薩法里** 8+)。 請參閱 [支援的客戶端平台](/help/sites-deploying/technical-requirements.md#supported-client-platforms) 的雙曲餘切值。

### 獲取軟體 {#getting-the-software}

具有有效維護和支援合同的客戶應已收到包含代碼的郵件通知，並能夠從AEM [**Adobe許可網站**](https://licensing.adobe.com/)。 業務合作夥伴可以請求下載訪問 [**spphelp@adobe.com**](mailto:spphelp@adobe.com)。

軟體AEM包有兩種形式：

* **cq-quickstart-6.5.0.jar:** 獨立執行檔 *罐* 檔案包含啟動和運行所需的一切。

* **cq-quickstart-6.5.0.war:** A *戰爭* 用於部署在第三方應用程式伺服器中的檔案。

在以下部分中，我們將介紹 **獨立安裝**。 有關在應用伺服器AEM中安裝的詳細資訊，請參見 [應用程式伺服器安裝](/help/sites-deploying/application-server-install.md)。

### 預設本地安裝 {#default-local-install}

1. 在本地電腦上建立安裝目錄。 例如：

   UNIX安裝位置： **/opt/aem**

   Windows安裝位置： **`C:\Program Files\aem`**

   同樣，通常在案頭上的資料夾中安裝示例實例。 無論如何，我們通常將此位置稱為：

   `<aem-install>`

   *請注意，檔案目錄的路徑必須只包含US ASCII字元。*

1. 放置 **罐** 和 **許可證** 此目錄中的檔案：

   ```shell
   <aem-install>/
       cq-quickstart-6.5.0.jar
       license.properties
   ```

   如果您不提供 `license.properties` 檔案AEM，將瀏覽器重定向到 **歡迎** 螢幕，您可以在其中輸入許可證密鑰。 如果您尚未獲得許可證密鑰，則需要從Adobe請求有效的許可證密鑰。

1. 要在GUI環境中啟動實例，只需按兩下 **`cq-quickstart-6.5.0.jar`** 的子菜單。

   另外，可以從命AEM令行啟動：

   ```shell
       java -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

將AEM花費幾分鐘來解壓縮jar檔案，安裝自己，然後啟動。 上述過程導致：

* 一個 **AEM作者** 實例
* 運行 **本地主機**
* 埠 **4502**

要訪問實例，請將瀏覽器指向：

**`https://localhost:4502`**

將自動配置作者實例中的結果以連接到 **發佈實例** 上 **`localhost:4503`**。

### 作者和發佈安裝 {#author-and-publish-installs}

預設安裝( **作者** 實例 **`localhost:4502`**)可以通過更名來更改 `jar` 檔案，然後首次啟動它。 命名模式為：

**`cq-<instance-type>-p<port-number>.jar`**

例如，將檔案更名為

**`cq-author-p4502.jar`**

啟動它將導致作者實例運行 **`localhost:4502`**。

同樣，更名和啟動檔案

**`cq-publish-p4503.jar`**

將導致發佈實例在上運行 **`localhost:4503`**。

例如，在

`<aem-install>/author`和

**`<aem-install>/publish`**

有關自定義安裝的詳細資訊，請參閱以下內容：

* [自定義獨立安裝](/help/sites-deploying/custom-standalone-install.md)
* [執行模式](/help/sites-deploying/configure-runmodes.md)

### 未打包的安裝目錄 {#unpacked-install-directory}

當快速啟動jar首次啟動時，它將在名為的新子目錄下將其解壓縮到同一目錄 `crx-quickstart`。 您最後應執行以下操作：

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

如果實例是從UI安裝的，則瀏覽器窗口將自動開啟，案頭應用程式窗口也將開啟，顯示實例的主機和埠以及開/關開關：

![啟動螢幕](assets/screen_shot_.png)

>[!NOTE]
>
>如果使用符號連結，請查看 [符號連結問題](https://helpx.adobe.com/experience-manager/kb/changing-symlink.html)。

### 啟動和停止 {#starting-and-stopping}

解AEM開自身並首次啟動後，按兩下安裝目錄中的jar檔案就會啟動實例，它不會重新安裝它。

要從GUI中停止實例，只需按一下 **開/關** 在案頭應用程式窗口上切換。

也可以從命令行AEM停止和啟動。 假設您已首次安裝實例， **命令行指令碼** 位於此處：

**`<aem-install>/crx-quickstart/bin/`**

此資料夾包含以下Unix bash shell指令碼：

* **`start`**:啟動實例
* `stop`:停止實例
* **`status`**:報告實例的狀態
* **`quickstart`**:用於配置開始資訊（如果需要）。

還有等價的 **`bat`** 檔案。 有關詳細資訊，請參閱：

* [命令行啟動和停止](/help/sites-deploying/command-line-start-and-stop.md)

啟AEM動並自動將網路瀏覽器重定向到相應的頁面，通常是登錄頁面；例如：

`https://localhost:4502/`

![登錄螢幕](assets/screen_shot_2019-04-08at83533am.png)

登錄後，您可以訪問AEM。 有關詳細資訊，請參閱以下內容：

* [編寫](/help/sites-authoring/home.md)
* [管理](/help/sites-administering/home.md)
* [開發](/help/sites-developing/home.md)
* [管理](/help/managing/best-practices.md)

## 高級部署 {#advanced-deployment}

上節應讓您充分瞭解安裝的基AEM本知識。 但是，安裝完整的生產系統AEM可能會比這複雜得多。 有關高級安裝的完全覆蓋範圍，請參閱以下子頁：

* [技術要求](/help/sites-deploying/technical-requirements.md)
* [建議的部署](/help/sites-deploying/recommended-deploys.md)
* [自定義獨立安裝](/help/sites-deploying/custom-standalone-install.md)
* [應用程式伺服器安裝](/help/sites-deploying/application-server-install.md)
* [疑難排解](/help/sites-deploying/troubleshooting.md)
* [命令行啟動和停止](/help/sites-deploying/command-line-start-and-stop.md)
* [設定](/help/sites-deploying/configuring.md)
* [升級AEM到6.5](/help/sites-deploying/upgrade.md)
* [電子商務](/help/commerce/cif-classic/deploying/ecommerce.md)
* [配置How-To文章](/help/sites-deploying/ht-deploy.md)
* [Web 主控台](/help/sites-deploying/web-console.md)
* [排除複製故障](/help/sites-deploying/troubleshoot-rep.md)
* [最佳做法](/help/sites-deploying/best-practices.md)
* [部署社區](/help/communities/deploy-communities.md)
* [平台簡AEM介](/help/sites-deploying/platform.md)
* [效能指南](/help/sites-deploying/performance-guidelines.md)
* [AEM Mobile入門](/help/mobile/getting-started-aem-mobile.md)
* [什麼是AEM Screens?](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html)
