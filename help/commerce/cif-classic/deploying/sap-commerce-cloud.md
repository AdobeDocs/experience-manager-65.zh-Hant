---
title: SAPCommerce Cloud
seo-title: SAPCommerce Cloud
description: 了解如何使用SAPCommerce Cloud部署eCommerce。
seo-description: 了解如何使用SAPCommerce Cloud部署eCommerce。
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 2%

---

# SAPCommerce Cloud{#sap-commerce-cloud}

>[!NOTE]
>
>此頁面包含Hybris網站的連結。 對於某些頁面，您需要帳戶才能登入。

## 使用SAPCommerce Cloud部署eCommerce {#deploying-ecommerce-with-sap-commerce-cloud}

>[!NOTE]
>
>以下過程使用以下演示目錄來說明部署：
>
>`Geometrixx Outdoors Site English (US)`

部署[必要的電子商務套件](#packages-needed-for-ecommerce-with-hybris)將提供電子商務架構的完整功能，以及隨Hybris實施（包括示範目錄）提供的電子商務功能的參考實施

這可在Geometrixx Outdoors網站的英文（美國）分支(`/content/geometrixx-outdoors/en_US`)下找到：

* [產品資訊](#productinformationwithcolorvariants) （若適用，會包含顏色變體）

* [購物車內容概觀](#shoppingcartcontentoverview)
* [客戶登](#customersignup) 入 [和客戶登入](#customersignin)

* [存取Hybris管理主控台](#accesstothehybrismanagementconsole)

### 技術要求 — hybris伺服器{#technical-requirements-hybris-server}

已更新電子商務整合架構的Hybris擴充功能，以支援Hybris 5（預設為），同時維持與[Hybris 4](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#developing-for-hybris)的向後相容性。

>[!NOTE]
>
>* 支援18.11版及更新版本。
>* 您需要Java 7才能運行[hybris 5伺服器。](https://www.hybris.com/en/architecture-technology)
>* AEM擴充功能不支援hybris附加元件[Telco Accelerator](https://www.hybris.com/en/products/telecommunication)。

>



### 具有hybris {#packages-needed-for-ecommerce-with-hybris}的電子商務所需的包

若要安裝電子商務功能，您需要：

* 您的hybris伺服器
* AEM eCommerce架構：

   * 這是標準AEM安裝的一部分

* AEMGeometrixx全套件：

   * `cq-geometrixx-all-pkg`

* AEM hybris內容套件：

   * `cq-hybris-content-6.3.2`
   * 混合專用API實作
   * `cq-geometrixx-hybris-content-6.3.2`
   * 說明hybris使用的參考實施(`geometrixx-outdoors/en_US`)

### 使用hybris {#installation-of-ecommerce-with-hybris}安裝電子商務

若要安裝完整的設定(使用展示目錄、Geometrixx Outdoors)，基本步驟為：

1. [安裝AEM](/help/sites-deploying/deploy.md)。
1. 安裝Geometrixx — 全部包

   1. ` [cq-geometrixx-all-pkg](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq60/product/cq-geometrixx-all-pkg)`

1. 使用[套件管理器](/help/sites-administering/package-manager.md)安裝演示內容套件：

   1. ` [cq-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-hybris-content)`
   1. ` [cq-geometrixx-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-geometrixx-hybris-content)`

1. [下載並建置您的Hybris伺服器](#download-and-build-your-hybris-server)。
1. 在電子商務引擎中建立目錄：

   1. [設定Geometrixx戶外商店](#setup-the-geometrixx-outdoors-store)。

1. [](/help/sites-authoring/qg-page-authoring.md) 編寫您在AEM中需要的補充頁面。

>[!CAUTION]
>
>使用hybris伺服器需要個別的hybris授權。

>[!NOTE]
>
>開發人員[ API檔案](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation)也可供下載。

### 下載並構建您的Hybris伺服器{#download-and-build-your-hybris-server}

此程式中的步驟將下載並建置hybris伺服器。 它也會讓hybris和cq之間的連線需要初始設定。 接著，擴充功能便可搭配預設設定使用。

>[!CAUTION]
>
>不支援5.5.1之前的Hybris版本。

>[!NOTE]
>
>要完成此操作，您需要在系統上安裝[Groovy](https://groovy-lang.org/)。

1. 從hybris下載網站下載&#x200B;**hybris Commerce Suite**&#x200B;發佈。

   >[!CAUTION]
   >
   >您需要帳戶（來自hybris）才能存取此權限。

1. 將分送檔案解壓縮至所需位置（稱為&lt;hybris-root-directory>）。
1. 從命令列執行下列動作：

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

1. 將下列檔案下載至已擷取hybris散布的根資料夾，

   ```
       <hybris-root-directory>
   ```


[取得檔案](/help/sites-deploying/assets/setup.groovy)

   >[!NOTE]
   >
   >對於hybris 5.6.0和更新版本，請使用以下setup.groovy。

   5.6.0和更新版本

[取得檔案](/help/sites-deploying/assets/setup-1.groovy)

1. 從命令列，執行下列動作：

   * 更新hybris伺服器的設定（根據擴充功能的要求）
   * 使用修改的配置重建hybris伺服器
   * 啟動伺服器

   ```shell
   groovy setup.groovy
   cd bin/platform
   ant clean all
   sh hybrisserver.sh
   ```

   >[!NOTE]
   >
   >根據您的系統，這些步驟中的幾個可能需要幾分鐘才能完成。

1. 在您的瀏覽器中，導覽至&#x200B;**hybris管理主控台**，網址為：

   [http://localhost:9002](http://localhost:9002)

1. 按一下&#x200B;**初始化**，然後確認初始化操作（因為它將刪除現有資料）。

   進度將顯示在控制台上，其中`FINISHED`表示已完成。

   >[!NOTE]
   >
   >視您的系統而定，完成此作業可能需要幾分鐘的時間。

### 設定Geometrixx Outdoors儲存{#setup-the-geometrixx-outdoors-store}

此過程將上載並配置演示儲存 — 線上Geometrixx。

1. 啟動您的hybris例項。 從命令列執行下列動作：

   ```shell
   cd <hybris-root-directory>/bin/platform
   sh hybrisserver.sh
   ```

1. 在您的瀏覽器中，導覽至&#x200B;**hybris management console**，網址為：

   [https://localhost:9002/backoffice](https://localhost:9002/backoffice)

   使用以下憑據：
   * 用戶名：管理員
   * 密碼：nimda

1. 從側欄導航中，展開&#x200B;**System**&#x200B;和&#x200B;**Tools**。 然後選擇&#x200B;**Import**&#x200B;以開啟&#x200B;**嚮導：CSV匯入**&#x200B;視窗。
1. 在&#x200B;**Configuration**&#x200B;標籤中，**Upload**&#x200B;以下&#x200B;**Import file**:

[取得檔案](/help/sites-deploying/assets/geometrixx-outdoors-export.csv)

1. 將&#x200B;**地區設定**&#x200B;設定為：

   `en_US - English (United States)`

1. 開啟&#x200B;**Resources**&#x200B;標籤。
1. **** 上傳下 **列Media-Zip**:

[取得檔案](/help/sites-deploying/assets/geometrixx-outdoors-images.zip)

1. 按一下&#x200B;**Start**&#x200B;以導入指定的檔案。 **Result**&#x200B;標籤將顯示任何日誌條目。

1. 按一下&#x200B;**Done**&#x200B;以關閉匯入視窗。

1. 從側欄中，依次選擇&#x200B;**System**、**Tools**、**Import**。

1. **** 上傳下列匯 **入檔案**:

[取得檔案](/help/sites-deploying/assets/base-store.csv)

   對於hybris 5.7，請使用下列內容：

[取得檔案](/help/sites-deploying/assets/base-store-5_7.csv)

1. 將&#x200B;**地區設定**&#x200B;設定為：

   `en_US - English (United States)`

1. 按一下&#x200B;**Start**&#x200B;以導入指定的檔案。 **Result**&#x200B;標籤將顯示任何日誌條目。

1. 按一下&#x200B;**Done**&#x200B;以關閉匯入視窗。

1. 您現在可以使用產品座艙來檢視匯入的目錄和產品：

   [http://localhost:9002/productcockpit](http://localhost:9002/productcockpit)
