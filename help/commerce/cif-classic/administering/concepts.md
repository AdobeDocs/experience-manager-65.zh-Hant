---
title: 概念
description: 透過Adobe Experience Manager瞭解電子商務的一般概念。
contentOwner: Guillaume Carlino
exl-id: 290b2af6-257f-42f2-b809-1248227a4795
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '4439'
ht-degree: 1%

---

# 概念{#concepts}

整合架構提供以下用途的機制和元件：

* 連線至電子商務引擎
* 將資料提取至Adobe Experience Manager (AEM)
* 顯示該資料並收集購物者的回應
* 傳回交易詳細資料
* 搜尋來自兩個系統的資料

這表示：

* 購物者無需等待即可註冊和購物。
* 購物者可立即看到價格變更。
* 您可以視需要新增產品。

>[!NOTE]
>
>電子商務架構可搭配下列專案使用：
>
>* [Adobe Commerce](/help/commerce/cif/integrating/magento.md)
>* [SAPCOMMERCE CLOUD](/help/commerce/cif-classic/administering/sap-commerce-cloud.md)
>* [SalesforceCommerce Cloud](https://github.com/adobe/commerce-salesforce)
>

>[!CAUTION]
>
>此 [電子商務整合框架](https://business.adobe.com/products/experience-manager/sites/ecommerce-integrations.html) 是AEM附加元件。
>
>您的銷售代表可以根據適當的引擎提供完整詳細資訊。

>[!CAUTION]
>
>此架構提供您專案的基礎需求。
>
>總是需要一定的開發工作來調整框架以符合您的規格。

>[!CAUTION]
>
>標準AEM安裝包含通用AEM (JCR)電子商務實作。
>
>其目的是為了示範，或作為根據您需求自訂實作的基本基礎。

為了最佳化營運，AEM和電子商務引擎都會專注於各自的專業領域。 資訊會在兩者之間即時傳輸；例如：

* AEM可以：

   * 要求：

      * 電子商務引擎的產品資訊。

   * 提供：

      * 使用者檢視產品資訊、購物車和結帳。
      * 購物車和結帳資訊至電子商務引擎。
      * 搜尋引擎最佳化(SEO)。
      * 社群功能。
      * 非結構化行銷互動。

* 電子商務引擎可以：

   * 提供：

      * 資料庫中的產品資訊。
      * 產品變體管理。
      * Order Management。
      * ERP （企業資源規劃）。
      * 搜尋產品資訊。

   * 程式：

      * 購物車。
      * 結帳。
      * 訂單履行。

>[!NOTE]
>
>確切的詳細資料取決於電子商務引擎和專案實作。

提供幾個現成的AEM元件，以供使用整合層。 目前，這些類別包括：

* 產品資訊
* 購物車
* 結帳
* 我的帳戶

您也可以使用各種搜尋選項。

## 架構 {#architecture}

整合框架提供API、一系列元件來說明功能，而數個擴充功能則提供連線方法的範例：

![chlimage_1-4](/help/sites-administering/assets/chlimage_1-4.png)

此框架可讓您存取以下功能：

![chlimage_1-5](/help/sites-administering/assets/chlimage_1-5.png)

### 實作 {#implementations}

AEM eCommerce是使用電子商務引擎實施：

* 電子商務整合架構的建置可讓您輕鬆地將電子商務引擎與AEM整合。 專門建立的電子商務引擎可控制產品資料、購物車、結帳和訂單履行，而AEM則可控制資料顯示和行銷活動。


>[!NOTE]
>
>標準AEM安裝包含通用AEM (JCR)電子商務實作。
>
>其目的是為了示範，或作為根據您需求自訂實作的基本基礎。
>
>在AEM中使用根據JCR的一般開發來實作的AEM電子商務是：
>
>* 獨立AEM原生電子商務範例，說明如何使用API。 這可用來透過現有的資料顯示和行銷活動，控制產品資料、購物車和結帳。 在這種情況下，產品資料庫會儲存在AEM原生儲存庫中(Adobe的 [JCR](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/index.html))。
>
>  標準AEM安裝包含 [通用電子商務實施](/help/commerce/cif-classic/administering/generic.md).

### Commerce提供者 {#commerce-providers}

將資料從商務引擎匯入您的AEM電子商務網站時，會使用商務提供者為匯入者提供資料。 一個商務提供者可以支援多個匯入工具。

商務提供者為自訂的AEM程式碼，其中之一為：

* 後端商務引擎的介面
* 在JCR存放庫上實作商業系統

AEM目前提供兩個範例商業提供者：

* 一個用於geometrixx-hybris
* 另一個適用於geometrixx-generic (JCR)

雖然專案通常需要開發自己的、自訂的、特定於其PIM和產品資料模式的商業提供者。

>[!NOTE]
>
>Geometrixx匯入工具使用CSV檔案；在其實作上方的註解中有接受的結構描述（允許自訂屬性）。

此 [產品服務管理員](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/commerce/pim/api/ProductServicesManager.html) 維護(透過 [osgi](/help/sites-deploying/configuring.md#osgi-configuration-settings))的實施清單 [ProductImporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/commerce/pim/api/ProductImporter.html) 和 [CatalogBlueprintImporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/commerce/pim/api/CatalogBlueprintImporter.html) 介面。 這些專案會列於 **匯入工具/Commerce提供者** 匯入工具精靈的下拉式欄位(使用 `commerceProvider` 屬性作為名稱)。

當下拉式清單中提供特定的匯入工具/商務提供者時，您必須在以下任一位置定義所需的任何補充資料（視匯入工具型別而定）：

* `/apps/commerce/gui/content/catalogs/importblueprintswizard/importers`
* `/apps/commerce/gui/content/products/importproductswizard/importers`

位於適當下方的資料夾 `importers` 資料夾必須符合匯入工具名稱；例如：

* `.../importproductswizard/importers/geometrixx/.content.xml`

來源匯入檔案的格式由匯入工具定義。 或者，匯入工具可能會建立與商務引擎的連線（例如WebDAV或http）。

## 角色 {#roles}

整合的系統會針對下列角色來維護資料：

* 維護下列專案的產品資訊管理(PIM)使用者：

   * 產品資訊。
   * 分類、分類、核准。
   * 與數位資產管理互動。
   * 定價 — 通常來自ERP系統，不會在商務系統中明確維護。

* 負責維護下列專案的作者/行銷經理：

   * 所有管道的行銷內容。
   * 促銷活動。
   * 憑單。
   * 行銷活動。

* 瀏覽網路者/購物者：

   * 檢視您的產品資訊。
   * 將專案放入購物車。
   * 檢查他們的訂單。
   * 期望訂單履行。

雖然實際位置取決於您的實作，例如通用或使用電子商務引擎：

![chlimage_1-6](/help/sites-administering/assets/chlimage_1-6.png)

## 產品 {#products}

### 產品資料與行銷資料的比較 {#product-data-versus-marketing-data}

#### 結構性與行銷類別 {#structural-versus-marketing-categories}

如果您可以區分以下兩個類別，這可以讓您以有意義的結構來清楚顯示URL (樹狀結構： `cq:Page` 節點)，因此與經典的AEM內容管理非常接近)：

* *結構*類別

  類別樹狀結構定義 *什麼是產品*；例如：

  `/products/mens/shoes/sneakers`

* *行銷* 類別

  所有其他類別 *產品可屬於*；例如：

  `/special-offers/christmas/shoes`)

### 產品資料 {#product-data}

為了描繪和管理您的產品，您將需要儲存一系列關於它們的資訊。

產品資料可以是：

* 直接在AEM中維護（一般）。
* 在電子商務引擎中維護，並在AEM中提供。

  視資料型別而定 [已同步](#catalog-maintenance-data-synchronization) 必要時，或直接存取；例如，產品價格等極不穩定和關鍵資料會從每個頁面請求的電子商務引擎中擷取，以確保其隨時保持最新。

無論是哪種情況，當產品資料已輸入/匯入AEM時，都可以從 **產品** 主控台。 在此處，產品的卡片和清單檢視會顯示如下資訊：

* 影像
* SKU代碼
* 上次修改時間

![chlimage_1-7](/help/sites-administering/assets/chlimage_1-7.png)

### 產品的系列品種 {#product-variants}

對於適當的產品，也可以儲存關於變體的資訊。 例如，對於服裝專案，可用的不同顏色會視為變體保留：

![ecommerceproductvariants](/help/sites-administering/assets/ecommerceproductvariants.png)

### 產品屬性 {#product-attributes}

各產品的個別屬性可能取決於所使用的電子商務引擎和您的AEM實作。 檢視產品頁面和/或編輯產品資訊時，這些選項都可（視情況而定）使用，可能包括：

* **影像**

  產品的影像。

* **標題**

  產品名稱。

* **說明**

  產品的文字說明。

* **標籤**

  用於將相關產品分組的標籤。

* **預設資產類別**

  資產的預設類別。

* **ERP資料**

  企業資源規劃(ERP)資訊。

   * **SKU**

     庫存單位(SKU)資訊。

   * **顏色**
   * **大小**
   * **價格**

     產品的單價。

* **摘要**

  產品功能的摘要。

* **功能**

  更完整的產品功能細節。

### 產品資產 {#product-assets}

您可以為個別產品保留一系列資產。 其中通常包括影像和影片。

## 目錄 {#catalogs}

目錄會將產品資料分組在一起，既方便管理，又能向購物者呈現。 目錄通常會根據語言、地理區域、品牌、季節、愛好、運動等屬性來建構。

### 目錄結構 {#catalog-structure}

#### 多國語言的目錄 {#catalogs-in-multiple-languages}

AEM支援多種語言的產品內容。 請求資料時，整合架構會從目前的樹狀結構中擷取語言(例如 `en_US` 對於下的頁面 `/content/geometrixx-outdoors/en_US`)。

若為多語言存放區，您可以個別匯入每個語言樹狀結構的目錄（或透過以下方式複製） [MSM](/help/sites-administering/msm.md))。

#### 多個品牌的目錄 {#catalogs-for-multiple-brands}

與語言一樣，大型跨國企業必須滿足多個品牌的需求。

#### 依標籤的目錄 {#catalogs-by-tags}

標籤也可用來將產品分組到目錄中。 這些可用於更具活力的目錄，例如季節性優惠方案。

### 目錄設定（初始匯入） {#catalog-setup-initial-import}

您可以將基礎目錄所需的產品資料從下列位置匯入AEM，具體取決於您的實作：

* CSV檔案（用於一般實作）
* 電子商務引擎

### 目錄維護（資料同步） {#catalog-maintenance-data-synchronization}

產品資料不可避免地會有進一步的變更：

* 對於一般實作，可透過以下方式管理 [產品編輯器](/help/commerce/cif-classic/administering/generic.md#editing-product-information)
* 使用 [電子商務引擎必須同步變更](#data-synchronization-with-an-ecommerce-engine-ongoing)

#### 與電子商務引擎進行資料同步（進行中） {#data-synchronization-with-an-ecommerce-engine-ongoing}

初次匯入後，您的產品資料不可避免地會變更。

使用電子商務引擎時，會在該處維護產品資料，且必須在AEM中提供。 進行更新時，必須同步處理此產品資料。

這可能取決於資料型別：

* A [定期同步會與變更的資料摘要一起使用](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#product-synchronization-and-publishing).

  除此之外，您還可以為快速更新選取特定更新。

* 高度不穩定的資料（例如價格資訊）會從每個頁面請求的商業引擎中擷取，以確保其隨時保持最新。

### 目錄 — 效能與規模調整 {#catalogs-performance-and-scaling}

從電子商務引擎(PIM)匯入具有大量產品（超過100,000）的大型目錄可能會因為節點數量過多而影響系統。 如果產品有關聯的資產（例如產品影像），也可能會減慢編寫執行個體的速度。 這是因為這些資產的後續處理需要大量的CPU和記憶體。

您可選擇使用多種策略來解決這些問題：

* [分段](#bucketing)  — 滿足大量節點的需求
* [將資產後處理解除安裝到專用執行個體](#offload-asset-post-processing-to-a-dedicated-instance)
* [僅匯入產品資料](#only-import-product-data)
* [匯入節流和批次儲存](#import-throttling-and-batch-saves)
* [效能測試](#performance-testing)
* [績效 — 其他](#performance-miscellaneous)

#### 分段 {#bucketing}

如果JCR節點有許多直接子節點（例如1000個以上），則需要貯體（虛擬資料夾）以確保效能不受影響。 匯入時會根據演演算法產生這些值。

這些貯體採用引入目錄結構的虛擬資料夾形式，但可以設定為在公共URL中不顯現。

#### 將資產後處理解除安裝到專用執行個體 {#offload-asset-post-processing-to-a-dedicated-instance}

此情境涉及設定兩個作者執行個體：

1. 主要作者執行個體

   從PIM匯入產品資料，PIM會停用資產路徑的後處理。

1. 專用DAM作者例項

   從PIM匯入產品資產並進行後續處理，然後將這些資產復寫回主要作者執行個體以供使用。

![架構圖](/help/sites-administering/assets/chlimage_1-8.png)

#### 僅匯入產品資料 {#only-import-product-data}

對於不含要匯入之資產（影像）的產品，您可以匯入產品資料，而不受資產後處理的影響。

![架構圖](/help/sites-administering/assets/chlimage_1-9.png)

#### 效能測試 {#performance-testing}

在AEM電子商務實作中必須考量效能測試：

* 作者環境：

  背景（例如，匯入）活動可與一般使用者活動（例如頁面編輯）同時發生，即使前端效能（一般而言）被賦予較高的優先順序，線上作者看到的效能不佳也會導致無法封鎖上線決定的挫折。

* 發佈環境：

  復寫是確保內容快速可靠地發佈的重要程式。 這可能受作者如何分組要發佈的內容所影響。

* 前端：

  前端和快取無效混合在一起，可能會導致效能驚人。 測試有助於避免這些問題。

請注意，此效能測試需要目標的知識和分析：

* 內容數量

   * Assets
   * 本地化的I18ned產品和SKU

* 使用者活動：

   * 大量版本
   * 大量發佈
   * 大量搜尋請求

* 背景處理程式

   * 匯入
   * 同步處理更新（例如，定價）

* 維護需求（備份、Tar PM最佳化、資料存放區垃圾收集等）

#### 績效 — 其他 {#performance-miscellaneous}

對於所有實作，請謹記以下幾點：

* 由於產品、庫存單位和類別可能會很多，請嘗試使用儘可能少的節點數來建立內容模型。

  節點越多，內容就越有彈性（例如parsys）。 不過，一切都是權衡取捨，您在操作（例如）30,000種產品時，是否需要個別的彈性（依預設）？

* 儘可能避免重複（請參閱本地化），或是在進行重複時，考慮重複會造成多少節點。
* 儘可能標籤您的內容，以準備查詢最佳化。

  例如：

  `/content/products/france/fr/shoe/reebok/pump/46 SKU`

  每個內容層級應有一個標籤（即國家、語言、類別、品牌、產品）。 正在搜尋

  `//element(*,my:Sku)[@country='france' and @language='fr'`

  和

  `@category='shoe' and @brand='reebok' and @product='pump']`

  會比搜尋快很多

  `/jcr:root/content/france/fr/shoe/reebok/pump/element(*,my:Sku)`

* 在您的技術棧疊中，計劃分解式內容存取模式與服務。 此為一般最佳實務，但此處更重要，因為您可以在最佳化階段為經常讀取的資料（且您不想使用填入套件快取的）新增應用程式快取。

  例如，屬性管理通常是快取的良好候選專案，因為它與透過產品匯入更新的資料有關。
* 考慮使用 [Proxy頁面](#proxy-pages).

### 目錄區段頁面 {#catalog-section-pages}

例如，目錄區段會提供您下列資訊：

* 類別的簡介（影像和/或文字）；這也可以用於橫幅和Teaser以促銷特殊優惠方案
* 該類別中個別產品的連結
* 其他類別的連結

![e-commerce_categoryrunning](/help/sites-administering/assets/ecommerce_categoryrunning.png)

### 產品頁面 {#product-pages}

產品頁面提供個別產品的完整資訊。 來自的動態更新也會反映出來；例如，在電子商務引擎上註冊的價格變更。

產品頁面為使用下列專案的AEM頁面： **產品** 元件；例如 **Commerce產品** 範本：

![e-commerce_nairobirunnersgreen](/help/sites-administering/assets/ecommerce_nairobirunnersgreen.png)

「產品」元件提供：

* 一般產品資訊；包括文字和影像。
* 定價；每次顯示/重新整理頁面時，都會從電子商務引擎擷取此值。
* 產品變體資訊；例如，顏色和大小。

此資訊可讓購物者在將專案新增至購物籃時選取下列專案：

* 顏色和大小變體
* 數量

#### 產品登陸頁面 {#product-landing-pages}

這些主要是提供靜態資訊的AEM頁面；例如，包含基礎產品頁面連結的簡介和概觀。

### 產品元件 {#product-component}

此 **產品** 元件可新增至具有提供所需中繼資料(亦即 `cartPage` 和 `cartObject`)。 在示範網站Geometrixx Outdoors中，這由以下專案提供 `UserInfo.jsp`.

此 **產品** 元件亦可根據您的個別需求進行自訂。

### Proxy頁面 {#proxy-pages}

Proxy頁面可用來簡化存放庫結構，以及將大型目錄的儲存空間最佳化。

建立目錄時，每個產品會使用十個節點，因為目錄會針對您可以在AEM中更新和自訂的每個產品提供個別元件。 如果您的目錄包含數百甚至數千種產品，那麼如此大量的節點可能會成為一個問題。 若要避免發生任何問題，您可以使用Proxy頁面建立您的目錄。

Proxy頁面使用雙節點結構( `cq:Page` 和 `jcr:content`)，不包含任何實際產品內容。 內容是在請求時透過參考產品資料和範本頁面產生的。

不過，還是需要權衡取捨。 您將無法在AEM內自訂您的產品資訊，將使用標準範本（為您的網站定義）。

>[!NOTE]
>
>如果您匯入沒有Proxy頁面的大型目錄，則不會遇到任何問題。
>
>您可以隨時從一種方法轉換為另一種方法。 您也可以轉換目錄的子區段。

## 促銷活動與憑單 {#promotions-and-vouchers}

### 憑單 {#vouchers}

憑單是經過測試和試用的方法，提供折扣來吸引購物者進行購買和/或獎勵客戶的忠誠度。

* 憑單供給：

   * 憑單代碼（由購物者輸入購物車中）。
   * 憑單標籤（購物者將其輸入購物車後顯示）。
   * 促銷活動路徑（定義憑單套用的動作）。

* 外部商務引擎也可以提供憑單。

在AEM中：

* 憑單是使用「網站」主控台建立/編輯的頁面型元件。
* 此 **憑單** 元件提供：

   * 憑單管理的轉譯器；這會顯示目前購物車中的任何憑單。
   * 用於管理（新增/移除）憑單的編輯對話方塊（表單）。
   * 在購物車中新增/移除憑單所需的動作。

* 憑單沒有自己的開啟和結束日期/時間，但會使用父行銷活動的日期/時間。

>[!NOTE]
>
>AEM使用術語 **憑單**，這是辭彙的同義字 **抵用券**.

### 促銷活動 {#promotions}

促銷活動與憑單一起可讓您瞭解以下情況：

* 公司為員工提供自訂價格，這是一份手工製作的使用者清單。
* 長期客戶會收到所有訂單的折扣。
* 在定義明確的時段內提供的銷售價格。
* 當客戶先前的訂單超過特定金額時，客戶會收到憑單。
* 購買產品的客戶 *product-X* 在此提供折扣： *product-Y* （配對產品）。

促銷活動並非由產品資訊管理員維護，而是由行銷管理員維護：

* 促銷活動是使用「網站」主控台建立/編輯的頁面型元件。 &quot;
* 促銷供應：

   * 優先順序
   * 推進處理常式路徑

* 您可以將促銷活動連結至促銷活動，以定義其開啟/關閉日期/時間。
* 您可以將促銷活動連結至體驗，以定義其區段。
* 未連線至體驗的促銷活動不會自行引發，但憑單仍可引發。
* 「推進」元件包含：

   * 推進管理的轉譯器和對話方塊
   * 用於呈現和編輯升級處理常式專屬之組態引數的子元件

在AEM中，促銷活動也會整合至 [Campaign Management](/help/sites-authoring/personalization.md)：

* a [行銷活動](/help/sites-authoring/personalization.md) 指定開啟/關閉時間
* [體驗](/help/sites-authoring/personalization.md) *範圍* 促銷活動用於根據資產（Teaser頁面、促銷活動等）對應的受眾區隔將其分組

促銷活動可在體驗中或直接在行銷活動中進行：

* 如果促銷活動在體驗中進行，則會自動套用至對象區段。

  例如，在geometrixx-outdoors範例網站中，促銷活動會：

  `/content/campaigns/geometrixx-outdoors/big-spender/ordervalueover100/free-shipping`

  位在體驗中，因此每當區段( `ordervalueover100`)解析。

* 如果促銷活動未出現在體驗中（僅在行銷活動中），則無法自動套用至對象。 但是，如果購物者將憑單輸入購物車中，且該憑單參考促銷活動，則仍可引發促銷活動。

  例如，促銷活動：

  `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

  在體驗之外，因此絕不會自動引發（即：根據分段）。 不過，可在文章行銷活動內的數個體驗中找到的憑單會參考它。 將這些憑單代碼輸入購物車會導致促銷啟動。

>[!NOTE]
>
>[hybris促銷活動](https://www.hybris.com/modules/promotion) 和 [hybris憑單](https://www.hybris.com/en/modules/voucher) 涵蓋所有影響購物車及與定價相關的專案。 促銷特定行銷內容（例如橫幅等）。 不是hybris促銷活動的一部分。

## 個人化 {#personalization}

### 客戶註冊與帳戶 {#customer-registration-and-accounts}

購物者註冊時，帳戶詳細資料必須在AEM和電子商務引擎之間同步。 敏感資料會獨立儲存，但設定檔會共用：

![chlimage_1-10](/help/sites-administering/assets/chlimage_1-10.png)

確切的機制可能取決於以下情況：

1. 使用者帳戶存在於兩個系統中：

   1. 不需要採取任何動作。

1. 使用者帳戶僅存在於AEM中：

   1. 使用者是在電子商務引擎中以相同的帳戶ID建立，密碼則隨機儲存在AEM中。
   1. 隨機密碼是必要的，因為AEM會嘗試在第一次呼叫時登入電子商務引擎（例如，當請求產品頁面且已參考電子商務引擎的價格時）。 由於這發生在AEM登入之後，因此密碼無法使用。

1. 使用者帳戶僅存在於電子商務引擎中：

   1. 此帳戶是在AEM中以相同的帳戶ID和密碼建立的。

使用電子商務引擎時，AEM只會儲存帳戶ID和密碼（可選擇使用使用者群組）。 所有其他資訊都會儲存在電子商務引擎中。

>[!NOTE]
>
>使用電子商務引擎時，您必須確保將為登入AEM執行個體之使用者建立的帳戶，會復寫（例如，透過工作流程）至與該引擎通訊的任何其他AEM執行個體。
>
>否則，這些其他AEM執行個體也會嘗試為引擎中的相同使用者建立帳戶。 這些動作會因 `DuplicateUidException` 來自引擎。

### 客戶註冊 {#customer-sign-up}

通常需要註冊才能讓購物者存取購物車。 這需要註冊（建立帳戶），才能建立客戶特定的帳戶。

![chlimage_1-11](/help/sites-administering/assets/chlimage_1-11.png)

>[!NOTE]
>
>也支援匿名購物車和結帳。

### 客戶登入 {#customer-sign-in}

註冊之後，購物者可以使用帳戶登入，以便可以追蹤他們的動作並完成他們的訂單。

![chlimage_1-12](/help/sites-administering/assets/chlimage_1-12.png)

### 單一登入 {#single-sign-on}

提供單一登入(SSO)，讓作者在AEM及電子商務系統中皆為人所知，不必登入兩次。

### 我的帳戶 {#myaccount}

來自電子商務引擎的交易資料會與購物者的個人資訊結合。 AEM會使用部分資料作為設定檔資料。 AEM中的表單動作會將資訊寫回電子商務引擎。

有一個頁面可讓您輕鬆管理帳戶資訊。 您可以按一下 **我的帳戶** ，或導覽至「 」頁面Geometrixx `/content/geometrixx-outdoors/en/user/account.html`.

![chlimage_1-13](/help/sites-administering/assets/chlimage_1-13.png)

### 通訊錄 {#address-book}

您的網站需要儲存一系列地址；包括傳遞、帳單和替代地址。 您可以使用以預設地址格式為基礎的表格來實作此作業，或者也可以使用AEM提供的「通訊錄」元件。

此通訊錄元件可讓您：

* 編輯報表簿中的地址
* 從出貨地址簿中選取一個地址
* 從帳本中選取帳單地址的地址

您可以選擇預設地址。

通訊錄元件可從 **我的帳戶** 按一下以建立頁面 **通訊錄** 或瀏覽至 `/content/geometrixx-outdoors/en/user/account/address-book.html`.

![chlimage_1-14](/help/sites-administering/assets/chlimage_1-14.png)

您可以按一下 **新增地址……** 在通訊錄中新增地址。 它會開啟一個您可以填寫的表單，然後按一下 **新增地址**.

>[!NOTE]
>
>您可以在通訊錄中輸入多個地址。

「結帳」購物車時會使用「通訊錄」：

![chlimage_1-15](/help/sites-administering/assets/chlimage_1-15.png)

位址持續顯示如下 `user_home/profile/addresses`.
例如，對於Alison Parker，其位於/home/users/geometrixx/aparker@geometrixx.info/profile/addresses下

您可以選擇預設的地址，此資訊會保留在購物者的設定檔中，而不是地址中。 設定檔屬性 `address.default` 以選取之值的位址的路徑設定。

### 客戶特定定價 {#customer-specific-pricing}

電子商務引擎會使用內容（主要是購物者資訊）來決定價格，然後向AEM提供正確的資訊。

## 購物車與訂購 {#shopping-cart-and-orders}

購物時，購物者會瀏覽產品頁面並選取專案，以將它們放入購物車中。 當他們繼續結帳時，可以下訂單。

### 匿名購物者 {#anonymous-shoppers}

匿名客戶可以：

* 檢視產品
* 將產品新增至購物車
* 執行結帳以下訂單

>[!NOTE]
>
>視您執行個體地址資訊或客戶註冊的設定而定，在結帳前可能需要進行註冊。

### 註冊購物者 {#registered-shoppers}

註冊客戶可以：

* 登入其帳戶
* 檢視產品
* 將產品新增至購物車
* 執行結帳以下訂單
* 檢視及追蹤先前的訂單

### 購物車內容概觀 {#shopping-cart-content-overview}

購物車提供：

* 所選專案的概觀
* 所選專案的產品頁面連結
* 具備以下功能：

   * 更新個別料號的數目/數量
   * 移除個別專案

![e-commerce_shoppingcart](/help/sites-administering/assets/ecommerce_shoppingcart.png)

購物車會根據使用的引擎儲存：

* AEM generic會將購物車儲存在Cookie中。
* 某些電子商務引擎可在工作階段中儲存購物車。

無論哪種情況，專案都會在登入/登出期間保留在購物車中（且可以還原） （但僅限在相同的電腦/瀏覽器上）。 例如：

* 瀏覽為 `anonymous` 並將產品新增至購物車
* 登入身份 `Allison Parker` - Allison的購物車是空的
* 新增產品至Allison的購物車
* 登出 — 購物車顯示產品 `anonymous`

* 再次登入身份 `Allison Parker` - Allison的產品已還原

>[!NOTE]
>
>匿名購物車只能在相同電腦/瀏覽器上還原。

>[!NOTE]
>
>不建議使用測試還原購物車內容 `admin` 帳戶，因為這可能與 `admin` 電子商務引擎的帳戶（例如，hybris）。

>[!NOTE]
>
>hybris可設定為在定義的時段後移除擱置中的購物車。

結帳前，價格變更會在發生時反映在（兩個系統）中。

### 訂單資訊 {#order-information}

根據您有關訂單的實作資訊包含在電子商務引擎或AEM中，此資訊會由AEM呈現。

會儲存各種資訊，其中可能包括：

* **訂單ID**

  訂單的參考編號。

* **已下單**

  下訂單的日期。

* **狀態**

  訂單的狀態；例如，「已出貨」。

* **貨幣**

  訂單的貨幣。

* **內容專案**

  排序的專案清單。

* **小計**

  訂購料號的總成本。

* **稅金**

  訂單上任何應付稅款的金額。

* **送貨**

  運費。

* **總計**

  訂單的總值；訂購的專案、稅金和送貨。

* **帳單地址**

  發票應傳送的地址。

* **付款Token**

  付款方式。

* **付款狀態**

  付款的狀態。

* **送貨地址**

  貨品應運往的地址。

* **送貨方法**

  運輸方法；例如，陸運、海運或空運。

* **追蹤編號**

  航運公司使用的任何追蹤編號。

* **追蹤連結**

  在出貨時用來追蹤訂單的連結。

>[!NOTE]
>
>建立訂單精靈中使用的欄位取決於為位置定義的觸控最佳化支架。 在一般範例中，這可在下列位置找到：
>`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`

在AEM中保留訂單時，「訂單」主控台會針對每個訂單顯示下列專案：

* 購物車中的專案數
* 訂單的總值
* 下訂單的時間
* 狀態

![chlimage_1-16](/help/sites-administering/assets/chlimage_1-16.png)

### 訂單追蹤 {#order-tracking}

下訂單後，購物者通常會回到：

* 檢查其訂單的狀態
* 從訂單移除產品
* 新增產品至訂單

收到訂單遞送後，購物者可能也會想要檢視一段期間內的訂單歷史記錄。

訂單履行與追蹤由電子商務引擎管理。 AEM可以使用「訂單歷史記錄」元件來顯示資訊，該元件會顯示所有相關細節，包括套用的憑單和促銷活動。 例如：

![chlimage_1-17](/help/sites-administering/assets/chlimage_1-17.png)

## 結帳 {#checkout}

簽出是使用標準AEM表單實作。 這可讓行銷經理使用行銷內容自訂體驗。

電子商務接著會使用AEM表單中的輸入來管理結帳程式。

### 付款安全性 {#payment-security}

付款詳細資料，包括信用卡資訊，通常由電子商務引擎管理。 AEM會將此類交易式資訊轉送至引擎（再從此處轉送至付款處理服務）。

可符合支付卡產業(PCI)規範。

### 訂單確認 {#confirmation-of-order}

訂單會在熒幕上確認，並可使用進行追蹤 [訂單追蹤](#order-tracking).

## 搜尋 {#search-features}

![chlimage_1-18](/help/sites-administering/assets/chlimage_1-18.png)

由於AEM對產品使用標準頁面，因此您可以使用標準搜尋元件來建立搜尋頁面。

如果您需要更徹底的實施，您可以：

* 以您需要的功能擴充預設搜尋元件。
* 在您的中實作搜尋方法 `CommerceService` 然後使用搜尋頁面上的電子商務搜尋元件。

使用電子商務引擎時，電子商務搜尋API可以在電子商務引擎解決方案中完全實作，因此您可以使用現成提供的電子商務搜尋元件。 多面向搜尋可讓您搜尋JCR和/或引擎：
