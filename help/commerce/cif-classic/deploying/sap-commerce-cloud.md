---
title: 使用SAPCommerce Cloud部署電子商務
description: 瞭解如何使用SAPCommerce Cloud部署Adobe Experience Manager eCommerce。
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
exl-id: ecbd0097-c407-4581-bab2-4729a71df4a3
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 1%

---

# SAPCOMMERCE CLOUD{#sap-commerce-cloud}

>[!NOTE]
>
>此頁面包含Hybris網站的連結。 對於某些頁面，您需要帳戶才能登入。

## 使用SAPCommerce Cloud部署eCommerce {#deploying-ecommerce-with-sap-commerce-cloud}

>[!NOTE]
>
>下列程式使用下列示範目錄來說明部署：
>
>`Geometrixx Outdoors Site English (US)`

部署[必要的電子商務套件](#packages-needed-for-ecommerce-with-hybris)可提供電子商務架構的完整功能，以及隨附於Hybris實作（包括示範目錄）之電子商務功能的參考實作

這可在Geometrixx Outdoors網站的英文（美國）分支( `/content/geometrixx-outdoors/en_US`)下取得：

* [產品資訊](#productinformationwithcolorvariants) （在適當時包含顏色變化）

* [購物車內容總覽](#shoppingcartcontentoverview)
* [客戶註冊](#customersignup)和[客戶登入](#customersignin)

* [Hybris管理主控台的存取權](#accesstothehybrismanagementconsole)

### 技術需求 — hybris Server {#technical-requirements-hybris-server}

已更新eCommerce Integration Framework的hybris延伸模組，以支援Hybris 5 （預設值），同時保持與[Hybris 4](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#developing-for-hybris)的回溯相容性。

>[!NOTE]
>
>* 支援18.11版及更新版本。
>* 您需要Java™ 7才能執行[hybris 5伺服器。](https://www.sap.com/products/crm.html)
>* AEM擴充功能不支援hybris附加元件[Telco加速器](https://www.sap.com/products/crm.html)。
>

### 具有hybris的電子商務所需的套件 {#packages-needed-for-ecommerce-with-hybris}

若要安裝電子商務功能，您需要：

* 您的hybris伺服器
* AEM電子商務架構：

   * 這是標準AEM安裝的一部分

* AEM全Geometrixx套件：

   * `cq-geometrixx-all-pkg`

* AEM hybris內容套件：

   * `cq-hybris-content-6.3.2`
   * hybris專屬的API實作
   * `cq-geometrixx-hybris-content-6.3.2`
   * 說明使用hybris ( `geometrixx-outdoors/en_US`)的參考實作

### 使用Hybris安裝電子商務 {#installation-of-ecommerce-with-hybris}

若要安裝完整的組態(使用示範目錄、Geometrixx Outdoors)，基本步驟如下：

1. [安裝AEM](/help/sites-deploying/deploy.md)。
1. 安裝全Geometrixx套件

   1. ` [cq-geometrixx-all-pkg](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq60/product/cq-geometrixx-all-pkg)`

1. 使用[封裝管理員](/help/sites-administering/package-manager.md)安裝示範內容封裝：

   1. ` [cq-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-hybris-content)`
   1. ` [cq-geometrixx-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-geometrixx-hybris-content)`

1. [下載並建置您的hybris伺服器](#download-and-build-your-hybris-server)。
1. 在電子商務引擎中建構您的目錄：

   1. [設定Geometrixx戶外商店](#setup-the-geometrixx-outdoors-store)。

1. [作者](/help/sites-authoring/qg-page-authoring.md)您在AEM中需要的任何補充頁面。

>[!CAUTION]
>
>使用hybris伺服器需要個別的hybris授權。

>[!NOTE]
>
>開發人員也可下載[API檔案](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation)。

### 下載並建置您的hybris伺服器 {#download-and-build-your-hybris-server}

此程式中的步驟會下載及建置hybris伺服器。 也會進行hybris與cq之間連線所需的初始設定。 擴充功能就會與預設設定搭配使用。

>[!CAUTION]
>
>不支援5.5.1之前的Hybris版本。

>[!NOTE]
>
>若要完成此作業，您的系統上必須安裝[Groovy](https://groovy-lang.org/)。

1. 從Hybris下載網站下載&#x200B;**Hybris Commerce Suite**&#x200B;發佈。

   >[!CAUTION]
   >
   >您需要帳戶（來自hybris）才能存取此專案。

1. 將散發檔案解壓縮至所需的位置（稱為&lt;hybris-root-directory>）。
1. 從命令列，執行下列動作：

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
   >必要時，按`Return`。

1. 將下列檔案下載到解壓縮的hybris散髮根資料夾，

   ```
       <hybris-root-directory>
   ```


[取得檔案](/help/sites-deploying/assets/setup.groovy)

   >[!NOTE]
   >
   >對於hybris 5.6.0和更新版本，請使用下列setup.groovy。

   5.6.0和更新版本

[取得檔案](/help/sites-deploying/assets/setup-1.groovy)

1. 從命令列，執行下列至：

   * 更新hybris伺服器的設定（根據擴充功能的要求）
   * 使用修改的組態重新建置hybris伺服器
   * 啟動伺服器

   ```shell
   groovy setup.groovy
   cd bin/platform
   ant clean all
   sh hybrisserver.sh
   ```

   >[!NOTE]
   >
   >視您的系統而定，其中數個步驟可能需要幾分鐘才能完成。

1. 在您的瀏覽器中，瀏覽至&#x200B;**hybris管理主控台**，網址為：

   [http://localhost:9002](http://localhost:9002)

1. 按一下&#x200B;**初始化**，然後確認初始化動作（因為它會刪除現有的資料）。

   進度會顯示在主控台上，`FINISHED`表示完成。

   >[!NOTE]
   >
   >視您的系統而定，這可能需要幾分鐘才能完成。

### 設定Geometrixx Outdoors存放區 {#setup-the-geometrixx-outdoors-store}

此程式會上傳並設定示範存放區 — 線上Geometrixx。

1. 啟動您的hybris執行個體。 從命令列，執行下列動作：

   ```shell
   cd <hybris-root-directory>/bin/platform
   sh hybrisserver.sh
   ```

1. 在您的瀏覽器中，瀏覽至&#x200B;**hybris管理主控台**，網址為：

   [https://localhost:9002/backoffice](https://localhost:9002/backoffice)

   使用這些認證：
   * 使用者名稱：admin
   * 密碼： nimda

1. 從側欄導覽中，展開&#x200B;**系統**&#x200B;和&#x200B;**工具**。 然後選取&#x200B;**匯入**&#x200B;以開啟&#x200B;**精靈：CSV匯入**&#x200B;視窗。
1. 在&#x200B;**組態**&#x200B;索引標籤中，**上傳**&#x200B;下列&#x200B;**匯入檔案**：

[取得檔案](/help/sites-deploying/assets/geometrixx-outdoors-export.csv)

1. 將&#x200B;**地區設定**&#x200B;設為：

   `en_US - English (United States)`

1. 開啟&#x200B;**資源**&#x200B;標籤。
1. **上傳**&#x200B;下列&#x200B;**Media-Zip**：

[取得檔案](/help/sites-deploying/assets/geometrixx-outdoors-images.zip)

1. 按一下&#x200B;**開始**&#x200B;匯入指定的檔案。 **結果**&#x200B;索引標籤會顯示任何記錄專案。

1. 按一下&#x200B;**完成**&#x200B;以關閉匯入視窗。

1. 從側邊欄選取&#x200B;**系統**、**工具**、**匯入**。

1. **上傳**&#x200B;下列&#x200B;**匯入檔案**：

[取得檔案](/help/sites-deploying/assets/base-store.csv)

   對於hybris 5.7，請使用下列專案：

[取得檔案](/help/sites-deploying/assets/base-store-5_7.csv)

1. 將&#x200B;**地區設定**&#x200B;設為：

   `en_US - English (United States)`

1. 按一下&#x200B;**開始**&#x200B;匯入指定的檔案。 **結果**&#x200B;索引標籤會顯示任何記錄專案。

1. 按一下&#x200B;**完成**&#x200B;以關閉匯入視窗。

1. 您現在可以使用產品駕駛艙來檢視匯入的目錄和產品：

   [http://localhost:9002/productcockpit](http://localhost:9002/productcockpit)
