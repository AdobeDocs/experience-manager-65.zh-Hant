---
title: SAPCommerce Cloud
seo-title: SAPCommerce Cloud
description: 瞭解如何使用SAPCommerce Cloud部署電子商務。
seo-description: 瞭解如何使用SAPCommerce Cloud部署電子商務。
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
translation-type: tm+mt
source-git-commit: 1cef6f87fa66fd78d439c23e6ac907f9531b8fd6
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 2%

---

# SAPCommerce Cloud{#sap-commerce-cloud}

>[!NOTE]
>
>此頁面包含Hybris網站的連結。 若是某些頁面，您需要帳戶才能登入。

## 使用SAPCommerce Cloud部署電子商務{#deploying-ecommerce-with-sap-commerce-cloud}

>[!NOTE]
>
>以下過程使用以下演示目錄來說明部署：
>
>`Geometrixx Outdoors Site English (US)`

部署[必要的電子商務套件](#packages-needed-for-ecommerce-with-hybris)將提供電子商務架構的完整功能，以及隨同Hybris實作（包括展示目錄）提供的電子商務功能的參考實作

這可從Geometrixx Outdoors網站的英文（美國）分支(`/content/geometrixx-outdoors/en_US`)下取得：

* [產品資訊](#productinformationwithcolorvariants) （適當時包含顏色變體）

* [購物車內容概觀](#shoppingcartcontentoverview)
* [客戶登入](#customersignup) 和 [客戶登入](#customersignin)

* [存取Hybris管理主控台](#accesstothehybrismanagementconsole)

### 技術要求- Hybris Server {#technical-requirements-hybris-server}

eCommerce Integration Framework的hybris擴充功能已更新為支援Hybris 5（依預設），同時維持與[Hybris 4](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#developing-for-hybris)的回溯相容性。

>[!NOTE]
>
>* 支援18.11及更新版本。
>* 您需要Java 7才能運行[hybris 5伺服器。](https://www.hybris.com/en/architecture-technology)
>* 擴充功能不支援hybris附加元件[Telco Accelerator](https://www.hybris.com/en/products/telecommunication)AEM。

>



### 具有hybris {#packages-needed-for-ecommerce-with-hybris}的電子商務所需的包

若要安裝電子商務功能，您需要：

* 您的hybris伺服器
* AEM電子商務框架：

   * 這是標準安裝的一AEM部分

* AEMGeometrixx包：

   * `cq-geometrixx-all-pkg`

* AEMhybris內容套件：

   * `cq-hybris-content-6.3.2`
   * 混合特定API實作
   * `cq-geometrixx-hybris-content-6.3.2`
   * 說明hybris(`geometrixx-outdoors/en_US`)使用的參考實作

### 使用hybris {#installation-of-ecommerce-with-hybris}安裝電子商務

要安裝完全成熟的配置(使用演示目錄，Geometrixx Outdoors)，基本步驟為：

1. [安裝AEM。](/help/sites-deploying/deploy.md)
1. 安裝Geometrixx-全部軟體包

   1. ` [cq-geometrixx-all-pkg](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq60/product/cq-geometrixx-all-pkg)`

1. 使用[package manager](/help/sites-administering/package-manager.md)安裝演示內容包：

   1. ` [cq-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-hybris-content)`
   1. ` [cq-geometrixx-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-geometrixx-hybris-content)`

1. [下載並建立您的Hybris伺服器](#download-and-build-your-hybris-server)。
1. 在電子商務引擎中建構您的目錄：

   1. [設定Geometrixx室外商店](#setup-the-geometrixx-outdoors-store)。

1. [制](/help/sites-authoring/qg-page-authoring.md) 作您需要的補充頁AEM面。

>[!CAUTION]
>
>使用hybris伺服器需要個別的hybris授權。

>[!NOTE]
>
>對於開發人員[API檔案](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation)也提供下載。

### 下載並建立您的Hybris伺服器{#download-and-build-your-hybris-server}

此過程中的步驟將下載並構建hybris伺服器。 它還將進行hybris和cq之間連接所需的初始配置。 然後，擴充功能將可搭配預設設定使用。

>[!CAUTION]
>
>不支援5.5.1以前的Hybris版本。

>[!NOTE]
>
>要完成此操作，您需要在系統上安裝[Groovy](https://groovy-lang.org/)。

1. 從hybris下載網站下載&#x200B;**hybris Commerce Suite**&#x200B;散發。

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
   >如果需要，請按`Return`。

1. 將下列檔案下載到您擷取的Hybris散發的根資料夾，

   ```
       <hybris-root-directory>
   ```


   [取得檔案](/help/sites-deploying/assets/setup.groovy)

   >[!NOTE]
   >
   >對於hybris 5.6.0和更新版本，請使用下列setup.groovy。

   5.6.0和更新版本

   [取得檔案](/help/sites-deploying/assets/setup-1.groovy)

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

1. 在您的瀏覽器中，導覽至&#x200B;**hybris管理控制台**，網址為：

   [http://localhost:9002](http://localhost:9002)

1. 按一下&#x200B;**Initialize** ，然後確認初始化操作（因為它將刪除現有資料）。

   控制台上將顯示進度，`FINISHED`表示完成。

   >[!NOTE]
   >
   >視您的系統而定，完成此作業可能需要幾分鐘的時間。

### 設定Geometrixx Outdoors商店{#setup-the-geometrixx-outdoors-store}

此程式將上傳並配置演示商店——線上Geometrixx。

1. 啟動您的Hybris實例。 在命令行中，執行以下操作：

   ```shell
   cd <hybris-root-directory>/bin/platform
   sh hybrisserver.sh
   ```

1. 在您的瀏覽器中，導覽至&#x200B;**hybris管理控制台**，網址為：

   [https://localhost:9002/backoffice](https://localhost:9002/backoffice)

   請使用下列認證：
   * 用戶名：管理員
   * 密碼：nimda

1. 從側欄導覽中，說明&#x200B;**System**&#x200B;和&#x200B;**Tools**。 然後選擇&#x200B;**Import**&#x200B;以開啟&#x200B;**嚮導：CSV Import**&#x200B;視窗。
1. 在&#x200B;**Configuration**&#x200B;標籤中，**Upload**&#x200B;以下&#x200B;**Import file**:

   [取得檔案](/help/sites-deploying/assets/geometrixx-outdoors-export.csv)

1. 將&#x200B;**地區設定**&#x200B;設為：

   `en_US - English (United States)`

1. 開啟&#x200B;**資源**&#x200B;頁籤。
1. **上** 載下列 **媒體郵遞區號**:

   [取得檔案](/help/sites-deploying/assets/geometrixx-outdoors-images.zip)

1. 按一下&#x200B;**開始**&#x200B;以導入指定的檔案。 **Result**&#x200B;頁籤將顯示所有日誌條目。

1. 按一下&#x200B;**Done**&#x200B;關閉導入窗口。

1. 從側欄中，選擇&#x200B;**System**，然後選擇&#x200B;**Tools**，然後選擇&#x200B;**Import**。

1. **上** 載下列 **匯入檔案**:

   [取得檔案](/help/sites-deploying/assets/base-store.csv)

   對於hybris 5.7，請使用下列功能：

   [取得檔案](/help/sites-deploying/assets/base-store-5_7.csv)

1. 將&#x200B;**地區設定**&#x200B;設為：

   `en_US - English (United States)`

1. 按一下&#x200B;**開始**&#x200B;以導入指定的檔案。 **Result**&#x200B;頁籤將顯示所有日誌條目。

1. 按一下&#x200B;**Done**&#x200B;關閉導入窗口。

1. 您現在可以使用產品Cockpit來檢視匯入的型錄和產品：

   [http://localhost:9002/productcockpit](http://localhost:9002/productcockpit)
