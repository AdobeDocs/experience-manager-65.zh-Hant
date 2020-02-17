---
title: SAP Commerce Cloud
seo-title: SAP Commerce Cloud
description: 瞭解如何使用SAP Commerce cloud部署電子商務。
seo-description: 瞭解如何使用SAP Commerce cloud部署電子商務。
uuid: a16ae42b-9c33-4da8-a130-52b72a779ec7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
discoiquuid: 44dfa10f-497e-473f-95d4-8dccae7ebf8e
pagetitle: Deploying eCommerce with SAP Commerce Cloud
translation-type: tm+mt
source-git-commit: 328e13eb2ce034b0b1ec7e5e0fb184de9435d1bc

---


# SAP Commerce Cloud{#sap-commerce-cloud}

>[!NOTE]
>
>此頁面包含Hybris網站的連結。 若是某些頁面，您需要帳戶才能登入。

## 使用SAP Commerce cloud部署電子商務 {#deploying-ecommerce-with-sap-commerce-cloud}

>[!NOTE]
>
>以下過程使用以下演示目錄來說明部署：
>
>`Geometrixx Outdoors Site English (US)`

部署必 [要的電子商務套件](#packages-needed-for-ecommerce-with-hybris) ，將提供電子商務架構的完整功能，以及隨同Hybris實作（包括展示目錄）一起提供的電子商務功能的參考實作

Geometrixx Outdoors網站的英文（美國）分支( `/content/geometrixx-outdoors/en_US`)中提供此功能：

* [產品資訊](#productinformationwithcolorvariants) （適合時使用顏色變體）

* [購物車內容概觀](#shoppingcartcontentoverview)
* [客戶註冊](#customersignup)[和客戶登入](#customersignin)

* [存取Hybris管理主控台](#accesstothehybrismanagementconsole)

### 技術需求- Hybris Server {#technical-requirements-hybris-server}

eCommerce Integration Framework的hybris擴充功能已更新為支援Hybris 5（視預設值而定），並維持與 [Hybris 4的回溯相容性](/help/sites-developing/sap-commerce-cloud.md#developing-for-hybris)。

>[!NOTE]
>
>* 支援18.11及更新版本。
>* 您需要Java 7才能執行 [hybris 5伺服器。](https://www.hybris.com/en/architecture-technology)
>* AEM擴充功能不支援hybris附加元件 [Telco Accelerator](https://www.hybris.com/en/products/telecommunication)。
>



### 包含hybris的電子商務所需套件 {#packages-needed-for-ecommerce-with-hybris}

若要安裝電子商務功能，您需要：

* 您的hybris伺服器
* AEM eCommerce架構：

   * 這是標準AEM安裝的一部分

* AEM Geometrixx-all套件：

   * `cq-geometrixx-all-pkg`

* AEM Hybris內容套件：

   * `cq-hybris-content-6.3.2`
   * 混合特定API實作
   * `cq-geometrixx-hybris-content-6.3.2`
   * 說明hybris()之使用的參考實 `geometrixx-outdoors/en_US`作

### 使用Hybris安裝電子商務 {#installation-of-ecommerce-with-hybris}

若要安裝完整的組態（使用展示目錄，Geometrixx Outdoors），基本步驟為：

1. [安裝AEM](/help/sites-deploying/deploy.md)。
1. 安裝Geometrixx-all套件

   1. ` [cq-geometrixx-all-pkg](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq60/product/cq-geometrixx-all-pkg)`

1. 使用套件管理器安裝展示內 [容套件](/help/sites-administering/package-manager.md):

   1. ` [cq-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-hybris-content)`
   1. ` [cq-geometrixx-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-geometrixx-hybris-content)`

1. [下載並建立您的Hybris伺服器](#download-and-build-your-hybris-server)。
1. 在電子商務引擎中建構您的目錄：

   1. [設定Geometrixx Outdoor Store](#setup-the-geometrixx-outdoors-store)。

1. [在](/help/sites-authoring/qg-page-authoring.md) AEM中編寫您需要的任何補充頁面。

>[!CAUTION]
>
>使用hybris伺服器需要個別的hybris授權。

>[!NOTE]
>
>對於開發 [人員](/help/sites-developing/ecommerce.md#api-documentation) ，也提供下載API檔案。

### 下載並建立您的Hybris伺服器 {#download-and-build-your-hybris-server}

此過程中的步驟將下載並構建hybris伺服器。 它還將進行hybris和cq之間連接所需的初始配置。 然後，擴充功能將可搭配預設設定使用。

>[!CAUTION]
>
>不支援5.5.1以前的Hybris版本。

>[!NOTE]
>
>要完成此操作，您需要在 [系統上安裝Groovy](https://groovy-lang.org/) 。

1. 從hybris下 **載網站下載Hybris Commerce Suite** 散發。

   >[!CAUTION]
   >
   >您需要帳戶（來自Hybris）才能存取此帳戶。

1. 將散發檔案解壓縮至所需位置（稱為&lt;hybris-root-directory>）。
1. 在命令行中，執行以下操作：

   ```shell
   cd <hybris-root-directory>/bin/platform
   . ./setantenv.sh
   ant clean all
   cd ../..
   ```

   >[!NOTE]
   >
   >執行時：
   >
   >`ant clean all`
   >
   >需要 `Return` 時按。

1. 將下列檔案下載到您擷取的Hybris散發的根資料夾，

   ```
       <hybris-root-directory>
   ```


   [取得檔案](assets/setup.groovy)

   >[!NOTE]
   >
   >對於hybris 5.6.0和更新版本，請使用下列setup.groovy。

   5.6.0和更新版本

   [取得檔案](assets/setup-1.groovy)

1. 在命令行中，執行以下操作：

   * 更新hybris伺服器的設定（依擴充功能的要求）
   * 使用已修改的配置重建hybris伺服器
   * 啟動伺服器

   ```shell
   groovy setup.groovy
   cd bin/platform
   ant clean all
   sh hybrisserver.sh
   ```

   >[!NOTE]
   >
   >視您的系統而定，完成這些步驟可能需要幾分鐘的時間。

1. 在您的瀏覽器中，導覽至 **Hybris管理主控台** :

   [http://localhost:9002](http://localhost:9002)

1. 按一 **下「初始化** 」，然後確認初始化動作（因為它會刪除現有資料）。

   進度將顯示在控制台上，並指 `FINISHED` 示完成。

   >[!NOTE]
   >
   >視您的系統而定，完成此作業可能需要幾分鐘的時間。

### 設定Geometrixx Outdoors商店 {#setup-the-geometrixx-outdoors-store}

此程式將上傳並設定展示商店- Geometrixx Online。

1. 啟動您的Hybris實例。 在命令行中，執行以下操作：

   ```shell
   cd <hybris-root-directory>/bin/platform
   sh hybrisserver.sh
   ```

1. 在您的瀏覽器中，導覽至 **Hybris管理主控台** :

   [https://localhost:9002/backoffice](https://localhost:9002/backoffice)

   請使用下列認證：
   * 用戶名：管理員
   * 密碼：nimda

1. 從側欄導覽、解說 **系統** 和 **工具**。 然後選擇 **導入** ，開啟向 **導：「CSV匯入** 」視窗。
1. 在「設 **定** 」索引標籤 **中** ，上傳下列 **「匯**&#x200B;入」檔案：

   [取得檔案](assets/geometrixx-outdoors-export.csv)

1. 將「地區 **設定** 」設定為：

   `en_US - English (United States)`

1. 開啟「資 **源** 」標籤。
1. **上傳** 下列 **媒體郵遞區號**:

   [取得檔案](assets/geometrixx-outdoors-images.zip)

1. 按一下 **開始** ，導入指定的檔案。 「結 **果** 」頁籤將顯示所有日誌條目。

1. 按一下 **完成** ，關閉導入窗口。

1. 從側欄中，依次選 **擇System**、 **Tools****、** Import。

1. **上傳** 下列 **匯入檔案**:

   [取得檔案](assets/base-store.csv)

   對於hybris 5.7，請使用下列功能：

   [取得檔案](assets/base-store-5_7.csv)

1. 將「地區 **設定** 」設定為：

   `en_US - English (United States)`

1. 按一下 **開始** ，導入指定的檔案。 「結 **果** 」頁籤將顯示所有日誌條目。

1. 按一下 **完成** ，關閉導入窗口。

1. 您現在可以使用產品Cockpit來檢視匯入的型錄和產品：

   [http://localhost:9002/productcockpit](http://localhost:9002/productcockpit)

