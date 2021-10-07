---
title: 概念
description: 使用AEM的電子商務的一般概念。
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: 290b2af6-257f-42f2-b809-1248227a4795
source-git-commit: 2bae11eafb875f01602c39c0dba00a888e11391a
workflow-type: tm+mt
source-wordcount: '4524'
ht-degree: 1%

---

# 概念{#concepts}

整合框架提供以下機制和組成部分：

* 連線至電子商務引擎
* 將資料提取至AEM
* 顯示該資料並收集購物者的回應
* 返回事務詳細資訊
* 從兩個系統搜索資料

這表示：

* 購物者無需等待即可註冊和購物。
* 購物者會立即看到價格變化。
* 您可以視需要新增產品。

>[!NOTE]
>
>電子商務框架可與以下項目一起使用：
>
>* [Magento](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md)
>* [SAPCommerce Cloud](/help/commerce/cif-classic/administering/sap-commerce-cloud.md)
>* [SalesforceCommerce Cloud](https://github.com/adobe/commerce-salesforce)

>


>[!CAUTION]
>
>[eCommerce整合架構](https://www.adobe.com/solutions/web-experience-management/commerce.html)為AEM附加元件。
>
>您的銷售代表將能夠根據相應引擎提供完整詳細資訊。

>[!CAUTION]
>
>此架構提供您專案的基礎需求。
>
>要使框架適應您的規範，始終需要進行一定數量的開發工作。

>[!CAUTION]
>
>標準AEM安裝包含一般AEM(JCR)電子商務實作。
>
>這目前的用途為示範，或根據您的需求，做為自訂實作的基礎。

為了優化操作，AEM和電子商務引擎都專注於自己的專業領域。 資訊在兩者之間即時傳輸；例如：

* AEM可以：

   * 請求：

      * 來自電子商務引擎的產品資訊。
   * 提供：

      * 產品資訊、購物車和結帳的使用者檢視。
      * 購物車和結帳資訊至電子商務引擎。
      * 搜尋引擎最佳化(SEO)。
      * 社群功能。
      * 無結構的行銷互動。


* 電子商務引擎可以：

   * 提供：

      * 資料庫中的產品資訊。
      * 產品變體管理。
      * 訂單管理。
      * ERP（企業資源規劃）。
      * 在產品資訊中搜尋。
   * 程序:

      * 購物車。
      * 結帳。
      * 訂單履行。


>[!NOTE]
>
>確切詳細資訊取決於電子商務引擎和專案實作。

提供許多現成可用的AEM元件以使用整合層。 目前包括：

* 產品資訊
* 購物車
* 結帳
* 我的帳戶

也提供各種搜尋選項。

## 架構 {#architecture}

整合架構提供API、說明功能的一系列元件，以及提供連線方法範例的數個擴充功能：

![chlimage_1-4](/help/sites-administering/assets/chlimage_1-4.png)

此架構可讓您存取下列功能：

![chlimage_1-5](/help/sites-administering/assets/chlimage_1-5.png)

### 實作 {#implementations}

AEM eCommerce是使用eCommerce引擎實作：

* 電子商務整合架構已建置，可讓您輕鬆將電子商務引擎與AEM整合。 建立電子商務引擎的用途控制產品資料、購物車、結帳和訂單履行，而AEM則控制資料顯示和行銷促銷活動。


>[!NOTE]
>
>標準AEM安裝包含一般AEM(JCR)電子商務實作。
>
>這目前的用途為示範，或根據您的需求，做為自訂實作的基礎。
>
>在AEM中使用以JCR為基礎的一般開發實作的AEM eCommerce為：
>
>* 說明API使用方式的獨立AEM原生電子商務範例。 這可用來控制產品資料、購物車和結帳，並結合現有的資料顯示和行銷活動。 在這種情況下，產品資料庫儲存在AEM的原生存放庫(Adobe的[JCR](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/index.html)實作)。
>
>  標準AEM安裝包含[通用電子商務實作](/help/commerce/cif-classic/administering/generic.md)的基本知識。

### 商務提供者 {#commerce-providers}

將資料從商務引擎匯入AEM eCommerce網站時，會使用商務提供者來為匯入工具提供資料。 一個商務提供者可支援多個匯入工具。

商務提供者是自訂為下列任一項的AEM程式碼：

* 後端商務引擎介面
* 在JCR存放庫上實作商務系統

AEM目前提供兩個商務提供者範例：

* geometrixx.hybris
* geometrixx-generic(JCR)的另一個

雖然通常，項目需要開發自己的、定製的、特定於其PIM和產品資料架構的商務提供商。

>[!NOTE]
>
>geometrixx匯入工具使用CSV檔案；實作上方的註解中會說明接受的結構（允許自訂屬性）。

[ProductServicesManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/commerce/pim/api/ProductServicesManager.html)維護（通過[OSGi](/help/sites-deploying/configuring.md#osgi-configuration-settings)）[ProductImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/commerce/pim/api/ProductImporter.html)和[CatalogBlueprintImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/commerce/pim/api/CatalogBlueprintImporter.html)介面的實施清單。 這些欄位會列在匯入工具精靈的&#x200B;**匯入工具/商務提供者**&#x200B;下拉式欄位中（以`commerceProvider`屬性作為名稱）。

從下拉式清單中取得特定匯入工具/商務提供者時，必須在下列任一項中定義其所需的任何補充資料（視匯入工具類型而定）:

* `/apps/commerce/gui/content/catalogs/importblueprintswizard/importers`
* `/apps/commerce/gui/content/products/importproductswizard/importers`

適當`importers`資料夾下的資料夾必須符合匯入工具名稱；例如：

* `.../importproductswizard/importers/geometrixx/.content.xml`

源導入檔案的格式由導入程式定義。 或者，匯入工具可建立與商務引擎的連線（例如WebDAV或http）。

## 角色 {#roles}

整合系統可滿足下列角色，以維護資料：

* 產品資訊管理(PIM)維護以下內容的用戶：

   * 產品資訊。
   * 分類、分類、核准。
   * 與數位資產管理互動。
   * 定價 — 這通常來自ERP系統，在商務系統中沒有明確維護。

* 作者/行銷經理，負責維護：

   * 所有管道的行銷內容。
   * 促銷活動.
   * 憑單.
   * 促銷活動.

* 瀏覽者/購物者：

   * 檢視您的產品資訊。
   * 將項目放入購物車。
   * 查出他們的訂單。
   * 預期訂單履行。

實際位置取決於您的實作；例如，使用一般或電子商務引擎：

![chlimage_1-6](/help/sites-administering/assets/chlimage_1-6.png)

## 產品 {#products}

### 產品資料與行銷資料 {#product-data-versus-marketing-data}

#### 結構與行銷類別 {#structural-versus-marketing-categories}

如果可區分以下兩個類別，則可讓您以有意義的結構（`cq:Page`節點的樹狀結構）來清楚顯示URL，因此非常接近傳統的AEM內容管理):

* *結構*類別

   定義&#x200B;*什麼是產品*&#x200B;的類別樹；例如：

   `/products/mens/shoes/sneakers`

* ** 行銷類別

   a *產品可以屬於*&#x200B;的所有其他類別；例如：

   `/special-offers/christmas/shoes`)

### 產品資料 {#product-data}

要描述和管理您的產品，您將希望掌握有關它們的一系列資訊。

產品資料可以是：

* 直接在AEM中維護（一般）。
* 在eCommerce引擎中維護，並可在AEM中使用。

   視需要而定，其為[synchronized](#catalog-maintenance-data-synchronization)，或直接存取；例如，在每個頁面請求上，都會從電子商務引擎擷取高度波動和關鍵資料，例如產品價格，以確保這些資料始終是最新的。

無論是哪種情況，當產品資料輸入/匯入AEM時，都可從&#x200B;**Products**&#x200B;主控台看到。 在此，產品的卡片和清單檢視會顯示下列資訊：

* 影像
* SKU代碼
* 上次修改時間

![chlimage_1-7](/help/sites-administering/assets/chlimage_1-7.png)

### 產品的系列品種 {#product-variants}

對於適當的產品，也可以保留有關變型的資訊。 例如，對於可用不同顏色的服裝項目，會保留為變體：

![ecommerproductvariants](/help/sites-administering/assets/ecommerceproductvariants.png)

### 產品屬性 {#product-attributes}

每個產品所保留的個別屬性可能取決於所使用的電子商務引擎和您的AEM實施。 檢視產品頁面和/或編輯產品資訊時，這些功能（視情況而定）可供使用，並可包括：

* **影像**

   產品的影像。

* **標題**

   產品名稱。

* **說明**

   產品的文字說明。

* **標記**

   用於將相關產品分組的標籤。

* **預設資產類別**

   資產的預設類別。

* **ERP 資料**

   企業資源規劃(ERP)資訊。

   * **SKU**

      庫存單位(SKU)資訊。

   * **彩色**
   * **大小**
   * **價格**

      產品的單價。

* **摘要**

   產品功能的摘要。

* **功能**

   產品功能的更完整細節。

### 產品資產 {#product-assets}

可針對個別產品保留精選的資產。 通常包括影像和影片。

## 目錄 {#catalogs}

目錄會將產品資料分組在一起，以方便管理並讓購物者呈現。 目錄通常是根據語言、地理區域、品牌、季數、嗜好、體育等屬性來建構。

### 目錄結構 {#catalog-structure}

#### 多語言目錄 {#catalogs-in-multiple-languages}

AEM支援多種語言的產品內容。 要求資料時，整合架構會從目前的樹狀結構中擷取語言（例如，`/content/geometrixx-outdoors/en_US`底下頁面的`en_US`）。

對於多語言商店，您可以分別匯入每個語言樹的目錄（或透過[MSM](/help/sites-administering/msm.md)複製目錄）。

#### 多品牌目錄 {#catalogs-for-multiple-brands}

與語言一樣，大型跨國公司可能需要滿足多個品牌的需求。

#### 依標籤的目錄 {#catalogs-by-tags}

標籤也可用來將產品群組在目錄中。 這些可用於更動態的目錄，例如季節性優惠方案。

### 目錄設定（初始匯入） {#catalog-setup-initial-import}

視您的實作而定，您可以將基礎目錄所需的產品資料從以下來源匯入AEM:

* CSV檔案（用於一般實施）
* 電子商務引擎

### 目錄維護（資料同步） {#catalog-maintenance-data-synchronization}

產品資料的進一步變更將不可避免：

* 對於一般實作，這些可透過[product editor](/help/commerce/cif-classic/administering/generic.md#editing-product-information)來管理
* 使用[eCommerce引擎時，必須同步更改](#data-synchronization-with-an-ecommerce-engine-ongoing)

#### 與電子商務引擎進行資料同步（持續） {#data-synchronization-with-an-ecommerce-engine-ongoing}

初次匯入後，產品資料的變更是不可避免的。

使用電子商務引擎時，產品資料會保留在該處，且需要可在AEM中使用。 更新時，需要同步此產品資料。

這取決於資料類型：

* 將[週期同步與變更](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#product-synchronization-and-publishing)的資料饋送一起使用。

   除此之外，您還可以為快速更新選擇特定更新。

* 從商務引擎中針對每個頁面請求擷取高度波動的資料（例如價格資訊），以確保其隨時為最新。

### 目錄 — 效能和擴展 {#catalogs-performance-and-scaling}

從電子商務引擎(PIM)導入具有大量產品（通常超過100,000個）的大型目錄會由於節點數過多而影響系統。 如果產品具有相關資產（例如產品影像），也可能會拖慢製作執行個體的速度。 這是因為這些資產的後置處理耗用CPU和記憶體。

您可以選擇各種策略來解決這些問題：

* [分段](#bucketing)  — 適應大量節點
* [將資產後處理卸載至專用執行個體](#offload-asset-post-processing-to-a-dedicated-instance)
* [僅匯入產品資料](#only-import-product-data)
* [導入節流和批保存](#import-throttling-and-batch-saves)
* [效能測試](#performance-testing)
* [效能 — 其他](#performance-miscellaneous)

#### 分段 {#bucketing}

如果JCR節點有許多直接子節點（例如1000個以上），則需要儲存貯體（虛設資料夾），以確保效能不受影響。 這些會在匯入時根據演算法產生。

這些貯體會採用虛設資料夾的形式，這些資料夾會導入目錄結構中，但可進行設定，使其在公用URL中不明顯。

#### 將資產後處理卸載至專用執行個體 {#offload-asset-post-processing-to-a-dedicated-instance}

此情境包含設定兩個製作例項：

1. 主作者例項

   從PIM匯入產品資料，資產路徑的後置處理將停用。

1. 專用DAM製作例項

   從PIM匯入和後續處理產品資產，然後將這些資產複製回主製作例項以供使用。

![架構圖](/help/sites-administering/assets/chlimage_1-8.png)

#### 僅匯入產品資料 {#only-import-product-data}

若產品不含要匯入的資產（影像），您可以匯入產品資料，而不受資產後期處理的影響。

![架構圖](/help/sites-administering/assets/chlimage_1-9.png)

#### 效能測試 {#performance-testing}

AEM eCommerce實作必須考慮效能測試：

* 製作環境：

   背景（例如，匯入）活動可與一般使用者活動（例如頁面編輯）同時發生，即使前端效能（一般而言）被賦予較高的優先順序，線上作者看到的效能不佳，可能會導致無法封鎖上線決策的困擾。

* 發佈環境：

   復寫是確保內容快速、可靠地發佈的關鍵過程。 作者對要發佈的內容進行分組的方式可能會影響此狀況。

* 前端：

   前端和快取無效的混合可能會導致效能意外。 測試有助於避免這些問題。

請注意，此效能測試需要您對目標的了解和分析：

* 內容卷

   * 資產
   * 本地化的I18內置產品和SKU

* 使用者活動：

   * 大量版
   * 大量發佈
   * 密集搜索請求

* 背景程式

   * 匯入
   * 同步更新（例如定價）

* 維護要求（備份、Tar PM優化、資料儲存垃圾收集等）

#### 效能 — 其他 {#performance-miscellaneous}

對於所有實施，請謹記下列幾點：

* 由於產品、庫存單位和類別可能很多，因此請嘗試使用最少的節點來建立內容模型。

   您擁有的節點越多，內容就越有彈性（例如parsys）。 但是，一切都是取捨，在操控（例如）30K產品時（預設情況下），您是否需要個人的靈活性？

* 請盡量避免重複（請參閱本地化），或在您重複時，想想您的重複會導致多少節點。
* 請盡量標籤您的內容，以便準備查詢最佳化。

   例如：

   `/content/products/france/fr/shoe/reebok/pump/46 SKU`

   每個內容層級（例如國家、語言、類別、品牌、產品）應有一個標籤。 搜尋

   `//element(*,my:Sku)[@country=’france’ and @language=’fr’`

   和

   `@category=’shoe’ and @brand=’reebok’ and @product=’pump’]`

   比搜索要快得多

   `/jcr:root/content/france/fr/shoe/reebok/pump/element(*,my:Sku)`

* 在您的技術堆棧中，規劃非常分工的內容訪問模型和服務。 這是一般的最佳實務，但更重要的是，在最佳化階段，您可以為經常讀取的資料（且您不想用來填入套件快取）新增應用程式快取。

   例如，屬性管理通常是快取的理想候選項，因為它與透過產品匯入更新的資料有關。
* 請考慮使用[代理頁面](#proxy-pages)。

### 目錄區段頁面 {#catalog-section-pages}

目錄區段可提供您下列項目：

* 類別簡介（影像和/或文字）;這也可用於橫幅和茶匙，以宣傳特別優惠方案
* 連結至該類別中的個別產品
* 連結至其他類別

![ecommerce_categoryrunning](/help/sites-administering/assets/ecommerce_categoryrunning.png)

### 產品頁面 {#product-pages}

產品頁面提供有關個別產品的完整資訊。 也會反映的動態更新；例如，在電子商務引擎上註冊的價格變更。

產品頁面是使用&#x200B;**Product**&#x200B;元件的AEM頁面；例如，在&#x200B;**商務產品**&#x200B;範本中：

![ecommerce_nairobirunnersgreen](/help/sites-administering/assets/ecommerce_nairobirunnersgreen.png)

產品元件提供：

* 一般產品資訊；包括文字和影像。
* 定價；這通常會在每次顯示/重新整理頁面時，從電子商務引擎中擷取。
* 產品變型資訊；例如顏色和大小。

此資訊可讓購物者在購物籃中新增項目時選取下列項目：

* 顏色和大小變體
* 數量

#### 產品登錄頁面 {#product-landing-pages}

這些是主要提供靜態資訊的AEM頁面；例如簡介和概述，其中包含基礎產品頁面的連結。

### 產品元件 {#product-component}

可將&#x200B;**Product**&#x200B;元件新增至任何具有提供所需中繼資料的上層頁面（即`cartPage`和`cartObject`的路徑）的頁面。 在演示站點中，Geometrixx Outdoors由`UserInfo.jsp`提供。

也可以根據您的個別需求自訂&#x200B;**Product**&#x200B;元件。

### 代理頁 {#proxy-pages}

代理頁用於簡化儲存庫的結構並優化大型目錄的儲存。

建立目錄會使用每個產品的10個節點，因為它為每個產品提供可在AEM內更新和自訂的個別元件。 如果您的目錄包含數百或甚至數千種產品，則會造成這麼大數量的節點問題。 若要避免任何問題，您可以使用Proxy頁面建立目錄。

代理頁使用不包含任何實際產品內容的雙節點結構（`cq:Page`和`jcr:content`）。 內容會在請求時參考產品資料和範本頁面而產生。

然而，這是一種取捨。 您將無法在AEM中自訂產品資訊，因此將會使用標準範本（為您的網站定義）。

>[!NOTE]
>
>如果您匯入沒有代理頁面的大型目錄，則不會遇到任何問題。
>
>您可以隨時從一種方法轉換為另一種方法。 您也可以轉換目錄的子區段。

## 促銷活動和憑單 {#promotions-and-vouchers}

### 憑單 {#vouchers}

憑單是一種經過嘗試和測試的方法，可提供折扣，以吸引購物者進行購買和/或獎勵客戶的忠誠度。

* 憑單供應：

   * 憑單代碼（由購物者輸入購物車）。
   * 憑單標籤（在購物者將其輸入購物車後顯示）。
   * 促銷路徑（定義憑證套用的動作）。

* 外部商務引擎也可以提供憑單。

在AEM中：

* 憑單是使用網站控制台建立/編輯的頁面型元件。
* **憑證**&#x200B;元件提供：

   * 憑證管理的轉譯者；這顯示當前購物車中的任何憑單。
   * 用於管理（添加/刪除）憑證的編輯對話框（表單）。
   * 向購物車添加/從購物車中刪除憑單所需的操作。

* 憑單沒有自己的開啟和關閉日期/時間，而是使用其父促銷活動的憑證。

>[!NOTE]
>
>AEM使用&#x200B;**憑單**&#x200B;一詞，這與&#x200B;**抵用券**&#x200B;一詞同義。

### 促銷活動 {#promotions}

促銷活動與憑單可讓您了解以下情形：

* 公司為員工提供定制價格，這是一份手工編製的用戶清單。
* 長期客戶可獲得所有訂單的折扣。
* 在明確的時間段內提供的售價。
* 當客戶的上一訂單超過特定金額時，客戶會收到憑單。
* 購買&#x200B;*product-X*&#x200B;的客戶在&#x200B;*product-Y*（配對產品）上可獲得折扣。

促銷活動通常不是由產品資訊經理維護，而是由行銷經理維護：

* 促銷活動是使用網站主控台建立/編輯的頁面型元件。 &quot;
* 促銷活動提供：

   * 優先順序
   * 升級處理程式路徑

* 您可以將促銷活動連結至促銷活動，以定義其開啟/關閉日期/時間。
* 您可以將促銷活動連結至體驗，以定義其區段。
* 未與體驗連結的促銷活動不會自行引發，但仍可由憑單引發。
* 升級元件包含：

   * 促銷管理的推薦者和對話
   * 用於呈現和編輯升級處理程式專用的配置參數的子元件

在AEM中，促銷活動也整合至[促銷活動管理](/help/sites-authoring/personalization.md):

* a [campaign](/help/sites-authoring/personalization.md)指定開/關時間
* [](/help/sites-authoring/personalization.md) ** 行銷活動中的體驗可用來根據對應的受眾區段，將資產（預告頁面、促銷活動等）分組

促銷活動可在體驗中進行，或直接在促銷活動中進行：

* 如果促銷活動是在體驗中持有，則會自動套用至對象區段。

   例如，在geometrixx-outdoors範例網站中，促銷活動：

   `/content/campaigns/geometrixx-outdoors/big-spender/ordervalueover100/free-shipping`

   在體驗中，因此會在區段(`ordervalueover100`)解析時自動觸發。

* 如果促銷活動未出現在體驗中（僅顯示在促銷活動中），則無法自動套用至對象。 但是，如果購物者在購物車中輸入憑單，且該憑單參考促銷，則仍可引發此憑證。

   例如，促銷活動：

   `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

   不在體驗之外，因此不會自動觸發(即：根據區段)。 但是，它被可在文章促銷活動內數個體驗中找到的憑單引用。 將這些憑單代碼輸入購物車會引發促銷活動。

>[!NOTE]
>
>[hybris促](https://www.hybris.com/modules/promotion) 銷活動 [和hybris ](https://www.hybris.com/en/modules/voucher) voucherscover影響購物車且與定價相關的一切。促銷活動專用的行銷內容（例如橫幅等）不屬於Hybris促銷活動。

## 個性化 {#personalization}

### 客戶註冊和帳戶 {#customer-registration-and-accounts}

當購物者註冊時，帳戶詳細資訊需要在AEM和電子商務引擎之間同步。 敏感資料會獨立保留，但設定檔會共用：

![chlimage_1-10](/help/sites-administering/assets/chlimage_1-10.png)

確切機制取決於情況：

1. 這兩個系統中都存在用戶帳戶：

   1. 無需任何動作。

1. 使用者帳戶僅存在於AEM中：

   1. 系統會在電子商務引擎中建立使用者，其帳戶ID與隨機密碼會儲存在AEM中。
   1. 隨機密碼是必要的，因為AEM會嘗試在第一次呼叫時登入電子商務引擎（例如，當請求產品頁面且參考了價格的電子商務引擎時）。 由於這會在AEM登入後發生，因此密碼無法使用。

1. 使用者帳戶僅存在於電子商務引擎中：

   1. 帳戶將在AEM中建立，並使用相同的帳戶ID和密碼。

使用電子商務引擎時，AEM只會儲存帳戶ID和密碼（選擇性地是使用者群組）。 所有其他資訊都儲存在電子商務引擎中。

>[!NOTE]
>
>使用電子商務引擎時，您需要確保為登入AEM例項的使用者建立的帳戶會複製（例如透過工作流程）至與該引擎通訊的任何其他AEM例項。
>
>否則，這些其他AEM例項也會嘗試為引擎中的相同使用者建立帳戶。 這些動作會因來自引擎的`DuplicateUidException`而失敗。

### 客戶註冊 {#customer-sign-up}

購物者必須註冊才能存取購物車。 這需要註冊（建立帳戶），才能建立客戶專屬帳戶。

![chlimage_1-11](/help/sites-administering/assets/chlimage_1-11.png)

>[!NOTE]
>
>也支援匿名購物車和結帳。

### 客戶登入 {#customer-sign-in}

註冊後，購物者可以使用其帳戶登入，以便追蹤其動作並完成其訂單。

![chlimage_1-12](/help/sites-administering/assets/chlimage_1-12.png)

### 單一登入 {#single-sign-on}

提供單一登入(SSO)，讓作者在AEM和電子商務系統中皆已知，不需重複登入。

### myAccount {#myaccount}

來自電子商務引擎的交易資料與關於購物者的個人資訊結合。 AEM將部分資料用作設定檔資料。 AEM中的表單動作會將資訊寫回電子商務引擎。

有一個頁面可讓您輕鬆管理您的帳戶資訊。 您可以按一下geometrixx頁面頂端的&#x200B;**My Account**，或導覽至`/content/geometrixx-outdoors/en/user/account.html`來存取它。

![chlimage_1-13](/help/sites-administering/assets/chlimage_1-13.png)

### 通訊錄 {#address-book}

您的網站需要儲存一系列地址；包括傳送、帳單和替代地址。 您可以根據預設地址格式使用表單來實作，也可以使用AEM提供的通訊簿元件。

此通訊簿元件允許您：

* 編輯帳簿中的地址
* 從帳簿中為發運地址選擇地址
* 從帳簿中選擇地址以進行開單地址

您可以選擇預設地址。

可通過按一下&#x200B;**通訊簿**&#x200B;或導航到`/content/geometrixx-outdoors/en/user/account/address-book.html`，從&#x200B;**我的帳戶**&#x200B;頁訪問通訊簿元件。

![chlimage_1-14](/help/sites-administering/assets/chlimage_1-14.png)

可以按一下「**添加新地址……」**&#x200B;在通訊簿中添加新地址。 它會開啟一個表單，您可以填寫該表單，然後按一下「**新增地址**」。

>[!NOTE]
>
>您可以在通訊簿中輸入多個地址。

結帳購物車時會使用通訊簿：

![chlimage_1-15](/help/sites-administering/assets/chlimage_1-15.png)

地址會保存在`user_home/profile/addresses`以下。
例如，若為Alison Parker，則位於/home/users/geometrixx/aparker@geometrixx.info/profile/addresses下

您可以選擇想要哪個位址作為預設，此資訊會保存在購物者的設定檔中，而非包含該位址。 設定檔屬性`address.default`是使用選定值地址的路徑設定的。

### 客戶特定定價 {#customer-specific-pricing}

電子商務引擎使用上下文（主要是購物者資訊）來確定其所持的價格，然後將正確的資訊提供回AEM。

## 購物車與訂購 {#shopping-cart-and-orders}

當購物者瀏覽產品頁面並選取項目以將其放入購物車中時。 當他們繼續結帳時，可以下訂單。

### 匿名購物者 {#anonymous-shoppers}

匿名客戶可以：

* 檢視產品
* 將產品新增至購物車
* 執行結帳以下單

>[!NOTE]
>
>結帳前可能需要執行個體地址資訊的設定或客戶註冊，視情況而定。

### 註冊購物者 {#registered-shoppers}

註冊客戶可以：

* 登入其帳戶
* 檢視產品
* 將產品新增至購物車
* 執行結帳以下單
* 檢視及追蹤先前的訂單

### 購物車內容概述 {#shopping-cart-content-overview}

購物車提供：

* 所選項的概觀
* 連結至所選項目的產品頁面
* 能夠：

   * 更新個別項目的數量/數量
   * 移除個別項目

![ecommerce_shoppingcart](/help/sites-administering/assets/ecommerce_shoppingcart.png)

購物車會根據所使用的引擎而儲存：

* AEM通用將購物車儲存在cookie中。
* 某些電子商務引擎可在工作階段中儲存購物車。

無論是哪種情況，項目都會在登入/登出期間（但僅在相同的電腦/瀏覽器上）保留在購物車中（且可以還原）。 例如：

* 以`anonymous`的形式瀏覽並將產品新增至購物車
* 登入為`Allison Parker` — 購物車空白
* 將產品新增至購物車
* 登出 — 購物車會顯示`anonymous`的產品

* 以`Allison Parker`重新登入 — 其產品已還原

>[!NOTE]
>
>匿名購物車只能在同一台電腦/瀏覽器上還原。

>[!NOTE]
>
>不建議使用`admin`帳戶測試還原購物車內容，因為這可能與電子商務引擎的`admin`帳戶（例如hybris）衝突。

>[!NOTE]
>
>可以將hybris配置為在定義的時間段後刪除掛起的購物車。

結帳前，價格變更會在發生時反映（在兩個系統中）。

### 訂單資訊 {#order-information}

根據您在電子商務引擎或AEM中保存的訂單相關實作資訊，此資訊由AEM呈現。

會儲存各種資訊，其中包括：

* **訂單 ID**

   訂單的參考編號。

* **已下單**

   下訂單的日期。

* **狀態**

   訂單狀態；例如，已發運。

* **貨幣**

   訂單的貨幣。

* **內容項目**

   已排序的項目清單。

* **小計**

   訂購物料的總成本。

* **稅金**

   訂單上應繳的稅金。

* **送貨**

   運費。

* **總計**

   訂單的總值；訂購的物品、稅金和分批。

* **帳單地址**

   應發送發票的地址。

* **付款 Token**

   付款方式。

* **付款狀態**

   付款的狀態。

* **送貨地址**

   貨物應運到的地址。

* **送貨方法**

   運輸方法；例如陸地、海洋或空氣。

* **追蹤編號**

   航運公司使用的任何跟蹤編號。

* **追蹤連結**

   用於在發運時追蹤訂單的連結。

>[!NOTE]
>
>建立順序精靈中使用的欄位取決於為該位置定義的觸控最佳化架構。 在一般範例中，這可從以下網址找到：
>`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`

在AEM內保留訂單時，Order Console會針對每筆訂單顯示下列內容：

* 購物車中的項目數
* 訂單的總值
* 下訂單時
* 狀態

![chlimage_1-16](/help/sites-administering/assets/chlimage_1-16.png)

### 訂單追蹤 {#order-tracking}

下訂單後，購物者通常會返回：

* 檢查訂單狀態
* 從訂單中刪除產品
* 將產品新增至訂單

在收到訂單傳送後，購物者可能也想要檢視一段時間內的訂單記錄。

訂單履行和追蹤通常由電子商務引擎管理。 AEM可使用訂單歷史記錄元件顯示資訊，該元件顯示所有相關詳細資訊，包括所應用的憑單和促銷。 例如：

![chlimage_1-17](/help/sites-administering/assets/chlimage_1-17.png)

## 結帳 {#checkout}

結帳是使用標準AEM表單實作。 這可讓行銷經理使用行銷內容自訂體驗。

然後，電子商務會使用AEM表單的輸入來管理結帳程式。

### 支付安全性 {#payment-security}

支付詳細資訊（包括信用卡資訊）通常由電子商務引擎管理。 AEM將此類交易資訊轉發到引擎（從引擎轉發到支付處理服務）。

支付卡行業(PCI)合規性可實現。

### 訂單確認 {#confirmation-of-order}

順序已在螢幕上確認，並可使用[順序追蹤](#order-tracking)來追蹤。

## 搜尋 {#search-features}

![chlimage_1-18](/help/sites-administering/assets/chlimage_1-18.png)

由於AEM使用產品的標準頁面，因此您可以使用標準搜尋元件來建立搜尋頁面。

若需要更徹底的實作，您可以：

* 使用您需要的功能擴充預設搜尋元件。
* 在`CommerceService`中實作搜尋方法，然後在搜尋頁面上使用電子商務搜尋元件。

使用電子商務引擎時，電子商務搜尋API可在電子商務引擎解決方案中完全實作，因此您可以使用現成可用的電子商務搜尋元件。 多面搜索允許您搜索JCR和/或引擎：
