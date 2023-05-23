---
title: 使用SAPCommerce Cloud部署電子商務
description: 瞭解如何使用SAPCommerce Cloud部署電子商務。
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
exl-id: ecbd0097-c407-4581-bab2-4729a71df4a3
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 2%

---

# SAPCommerce Cloud{#sap-commerce-cloud}

>[!NOTE]
>
>此頁包含到Hybris網站的連結。 對於某些頁面，您需要一個帳戶才能登錄。

## 使用SAPCommerce Cloud部署電子商務 {#deploying-ecommerce-with-sap-commerce-cloud}

>[!NOTE]
>
>以下過程使用以下演示目錄來說明部署：
>
>`Geometrixx Outdoors Site English (US)`

部署 [必要的電子商務包](#packages-needed-for-ecommerce-with-hybris) 將提供電子商務框架的全部功能，並參考實現電子商務功能，同時提供一個hybris實現（包括一個示範目錄）

這可在英語（美國）分支( `/content/geometrixx-outdoors/en_US`):

* [產品資訊](#productinformationwithcolorvariants) （適用時帶有顏色變型）

* [購物車內容概述](#shoppingcartcontentoverview)
* [客戶註冊](#customersignup) 和 [客戶登錄](#customersignin)

* [訪問Hybris管理控制台](#accesstothehybrismanagementconsole)

### 技術要求 — Hybris Server {#technical-requirements-hybris-server}

電子商務整合框架的分支擴展已更新，以支援Hybris 5（預設），同時保持與 [Hybris 4](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#developing-for-hybris)。

>[!NOTE]
>
>* 支援18.11及更高版本。
>* 您需要Java 7來運行 [hybris 5伺服器。](https://www.hybris.com/en/architecture-technology)
>* 木屑附加物， [電信加速器](https://www.hybris.com/en/products/telecommunication)，擴展不支援AEM。
>


### 利用Hybris進行電子商務所需的包 {#packages-needed-for-ecommerce-with-hybris}

要安裝電子商務功能，您需要：

* 您的Hybris伺服器
* AEM電子商務框架：

   * 這是標準安裝的一AEM部分

* AEMGeometrixx包：

   * `cq-geometrixx-all-pkg`

* AEMhybris內容包：

   * `cq-hybris-content-6.3.2`
   * Hybris特定API實現
   * `cq-geometrixx-hybris-content-6.3.2`
   * 說明hybris的使用的參考實現 `geometrixx-outdoors/en_US`)

### 安裝具有Hybris的電子商務 {#installation-of-ecommerce-with-hybris}

要安裝完整的配置(使用演示目錄、Geometrixx Outdoors)，基本步驟如下：

1. [安AEM裝](/help/sites-deploying/deploy.md)。
1. 安裝Geometrixx — 全部包

   1. ` [cq-geometrixx-all-pkg](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq60/product/cq-geometrixx-all-pkg)`

1. 使用 [軟體包管理器](/help/sites-administering/package-manager.md):

   1. ` [cq-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-hybris-content)`
   1. ` [cq-geometrixx-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-geometrixx-hybris-content)`

1. [下載並構建您的Hybris Server](#download-and-build-your-hybris-server)。
1. 在電子商務引擎中構建目錄：

   1. [設定Geometrixx戶外商店](#setup-the-geometrixx-outdoors-store)。

1. [作者](/help/sites-authoring/qg-page-authoring.md) 需要的任何補充頁AEM。

>[!CAUTION]
>
>使用hybris伺服器需要單獨的hybris許可證。

>[!NOTE]
>
>為開發人員 [API文檔](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) 也可供下載。

### 下載並構建您的Hybris Server {#download-and-build-your-hybris-server}

此過程中的步驟將下載並構建hybris伺服器。 它還將進行hybris和cq之間連接所需的初始配置。 然後，該擴展將可用於預設設定。

>[!CAUTION]
>
>不支援早於5.5.1的Hybris版本。

>[!NOTE]
>
>要完成此操作，您需要 [Groovy](https://groovy-lang.org/) 安裝在系統上。

1. 下載 **赫布里斯商務套房酒店** 從hybris下載網站發行。

   >[!CAUTION]
   >
   >你需要一個帳戶（來自hybris）才能訪問這個。

1. 將分發檔案解壓縮到所需位置(稱為 &lt;hybris-root-directory>)。
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
   >按 `Return` 的下界。

1. 將下列檔案下載到您提取的碎片分佈的根資料夾，

   ```
       <hybris-root-directory>
   ```


[取得檔案](/help/sites-deploying/assets/setup.groovy)

   >[!NOTE]
   >
   >對於hybris 5.6.0和更高版本，請使用以下setup.groovy。

   5.6.0和更高版本

[取得檔案](/help/sites-deploying/assets/setup-1.groovy)

1. 在命令行中，執行以下操作：

   * 更新hybris伺服器的配置（根據擴展要求）
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
   >取決於您的系統，其中幾個步驟可能需要幾分鐘才能完成。

1. 在瀏覽器中，導航到 **hybris管理控制台** 地址：

   [http://localhost:9002](http://localhost:9002)

1. 按一下 **初始化** 然後確認初始化操作（因為它將刪除現有資料）。

   進度將顯示在控制台上， `FINISHED` 表示完成。

   >[!NOTE]
   >
   >取決於您的系統，這可能需要幾分鐘才能完成。

### 設定Geometrixx Outdoors商店 {#setup-the-geometrixx-outdoors-store}

此過程將上載和配置演示儲存 — 線上Geometrixx。

1. 開始你的骨碎病例。 在命令行中，執行以下操作：

   ```shell
   cd <hybris-root-directory>/bin/platform
   sh hybrisserver.sh
   ```

1. 在瀏覽器中，導航到 **hybris管理控制台** 地址：

   [https://localhost:9002/backoffice](https://localhost:9002/backoffice)

   使用這些憑據：
   * 用戶名：管理員
   * 密碼：尼姆達

1. 從提要欄導航，展開 **系統** 和 **工具**。 然後選擇 **導入** 開啟 **嚮導：CSV導入** 的子菜單。
1. 在 **配置** 頁籤 **上載** 以下 **導入檔案**:

[取得檔案](/help/sites-deploying/assets/geometrixx-outdoors-export.csv)

1. 設定 **區域設定** 至：

   `en_US - English (United States)`

1. 開啟 **資源** 頁籤。
1. **上載** 以下 **介質壓縮**:

[取得檔案](/help/sites-deploying/assets/geometrixx-outdoors-images.zip)

1. 按一下 **開始** 導入指定的檔案。 的 **結果** 頁籤將顯示所有日誌條目。

1. 按一下 **完成** 來修改標籤元素的屬性。

1. 從提要欄中，選擇 **系統**，則 **工具**，則 **導入**。

1. **上載** 以下 **導入檔案**:

[取得檔案](/help/sites-deploying/assets/base-store.csv)

   對於hybris 5.7，請使用以下命令：

[取得檔案](/help/sites-deploying/assets/base-store-5_7.csv)

1. 設定 **區域設定** 至：

   `en_US - English (United States)`

1. 按一下 **開始** 導入指定的檔案。 的 **結果** 頁籤將顯示所有日誌條目。

1. 按一下 **完成** 來修改標籤元素的屬性。

1. 現在，您可以使用產品駕駛艙查看導入的目錄和產品：

   [http://localhost:9002/productcockpit](http://localhost:9002/productcockpit)
