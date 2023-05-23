---
title: 概念
description: 電子商務的一般概AEM念
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: 290b2af6-257f-42f2-b809-1248227a4795
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '4514'
ht-degree: 2%

---

# 概念{#concepts}

整合框架為以下方面提供了機制和元件：

* 連接到電子商務引擎
* 將資料拉入AEM
* 顯示資料並收集購物者的反應
* 返回事務處理詳細資訊
* 從兩個系統搜索資料

這表示：

* 購物者可以不等待地註冊和購物。
* 消費者將毫不遲疑地看到價格變化。
* 產品可根據需要添加。

>[!NOTE]
>
>電子商務框架可用於：
>
>* [Adobe Commerce](/help/commerce/cif/integrating/magento.md)
>* [SAPCommerce Cloud](/help/commerce/cif-classic/administering/sap-commerce-cloud.md)
>* [SalesforceCommerce Cloud](https://github.com/adobe/commerce-salesforce)
>


>[!CAUTION]
>
>的 [電子商務整合框架](https://www.adobe.com/solutions/web-experience-management/commerce.html) 是AEM載入項。
>
>您的銷售代表將能夠根據相應的引擎提供全部詳細資訊。

>[!CAUTION]
>
>該框架為您自己的項目提供了基礎要求。
>
>要使框架適應您的規格，總需要進行一定量的開發工作。

>[!CAUTION]
>
>標準安AEM裝包括通AEM用(JCR)電子商務實現。
>
>目前，這是為了演示目的，或根據您的要求作為自定義實施的基本基礎。

為了優化運營，AEM電子商務引擎都專注於自己的專業領域。 資訊在兩者之間即時傳輸；例如：

* AEM可以：

   * 請求：

      * 來自電子商務引擎的產品資訊。
   * 提供：

      * 產品資訊、購物車和結帳的用戶視圖。
      * 購物車和結帳資訊到電子商務引擎。
      * 搜索引擎優化(SEO)。
      * 社區功能。
      * 非結構化的營銷互動。


* 電子商務引擎可以：

   * 提供：

      * 資料庫中的產品資訊。
      * 產品變型管理。
      * 訂單管理。
      * ERP（企業資源計畫）。
      * 在產品資訊中搜索。
   * 程序:

      * 購物車。
      * 簽出。
      * 訂單履行。


>[!NOTE]
>
>具體細節將取決於電子商務引擎和項目實施情況。

提供了多個現成元件AEM以使用整合層。 目前，這些因素包括：

* 產品資訊
* 購物車
* 簽出
* 我的帳戶

酒店還提供各種搜索選項。

## 架構 {#architecture}

整合框架提供了API、一系列用於說明功能的元件和幾個用於提供連接方法示例的擴展：

![chlimage_1-4](/help/sites-administering/assets/chlimage_1-4.png)

該框架允許您訪問以下功能：

![chlimage_1-5](/help/sites-administering/assets/chlimage_1-5.png)

### 實施 {#implementations}

電AEM子商務採用電子商務引擎：

* 已構建電子商務整合框架，使您能夠輕鬆將電子商務引擎與整合AEM。 該目的構建的電子商務引擎控制產品資料、購物車、結帳和訂單履行，AEM同時控制資料顯示和市場營銷活動。


>[!NOTE]
>
>標準安AEM裝包括通AEM用(JCR)電子商務實現。
>
>目前，這是為了演示目的，或根據您的要求作為自定義實施的基本基礎。
>
>AEM基於JCR的通AEM用開發實現的電子商務為：
>
>* 一個獨立AEM的本機電子商務示例，用於說明API的使用。 這可用於控制產品資料、購物車和結帳，並結合現有的資料顯示和市場營銷活動。 在這種情況下，產品資料庫儲存在儲存庫的本AEM地位置(Adobe實施 [JCR](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/index.html))。
>
>  標準安AEM裝包含 [通用電子商務實現](/help/commerce/cif-classic/administering/generic.md)。

### 商業提供商 {#commerce-providers}

將資料從商務引擎導入電AEM子商務站點時，商務提供商用於向進口商提供資料。 一個商業提供商可以支援多個進口商。

商業提供商的代AEM碼是自定義為：

* 後端商務引擎的介面
* 在JCR儲存庫上實施商務系統

當前可提供以下兩個商業提供AEM商：

* 一個用於幾何碎片
* 用於geometrixx-generic(JCR)的另一個

儘管通常項目需要開發其PIM和產品資料架構專用的自定義商務提供程式。

>[!NOTE]
>
>幾何導入程式使用CSV檔案；在其實現上方的注釋中，對接受的架構（允許使用自定義屬性）有說明。

的 [產品服務管理器](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/commerce/pim/api/ProductServicesManager.html) 保持 [OSGi](/help/sites-deploying/configuring.md#osgi-configuration-settings))實現清單  [產品導入程式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/commerce/pim/api/ProductImporter.html) 和 [目錄藍圖導入程式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/commerce/pim/api/CatalogBlueprintImporter.html) 介面。 這些列在 **進口商/商務提供商** 導入程式嚮導的下拉欄位(使用 `commerceProvider` 屬性)。

當從下拉清單中提供特定的導入程式/商務提供程式時，必須在以下任一清單中定義它所需的任何補充資料（取決於導入程式類型）:

* `/apps/commerce/gui/content/catalogs/importblueprintswizard/importers`
* `/apps/commerce/gui/content/products/importproductswizard/importers`

相應資料夾下 `importers` 資料夾必須與導入程式名稱匹配；例如：

* `.../importproductswizard/importers/geometrixx/.content.xml`

源導入檔案的格式由導入程式定義。 或者，導入程式可以建立到商務引擎的連接（例如WebDAV或http）。

## 角色 {#roles}

整合系統滿足以下角色以維護資料：

* 產品資訊管理(PIM)維護者：

   * 產品資訊。
   * 分類、分類、批准。
   * 與數字資產管理交互。
   * 定價 — 這通常來自ERP系統，在商業系統中沒有明確維護。

* 作者/營銷經理，維護：

   * 所有渠道的營銷內容。
   * 促銷活動.
   * 憑單.
   * 行銷活動.

* 衝浪者/購物者：

   * 查看您的產品資訊。
   * 將物品放入購物車。
   * 檢查他們的命令。
   * 預計訂單履行。

儘管實際位置可能取決於您的實施；例如，泛型或具有電子商務引擎：

![chlimage_1-6](/help/sites-administering/assets/chlimage_1-6.png)

## 產品 {#products}

### 產品資料與營銷資料 {#product-data-versus-marketing-data}

#### 結構與市場營銷類別 {#structural-versus-marketing-categories}

如果可以區分以下兩個類別，則允許您使用有意義的結構（樹）來明確URL `cq:Page` 因此，非常接近經典的內AEM容管理):

* *結構*類別

   類別樹定義 *什麼是產品*;例如：

   `/products/mens/shoes/sneakers`

* *營銷* 類別

   所有其他類別a *產品可以屬於*;例如：

   `/special-offers/christmas/shoes`)

### 產品資料 {#product-data}

要描述和管理您的產品，您需要保存有關這些產品的一系列資訊。

產品資料可以是：

* 直接維AEM護（泛型）。
* 在電子商務引擎中維護，並在中提AEM供。

   根據資料類型 [同步](#catalog-maintenance-data-synchronization) 或直接訪問；例如，在每個頁面請求上從電子商務引擎檢索高度易變和關鍵的資料，以確保它們始終是最新的。

在兩種情況下，當產品資料已輸入/導入AEM到其中時，可從 **產品** 控制台。 在此，產品的卡和清單視圖顯示以下資訊：

* 影像
* SKU代碼
* 上次修改時間

![chlimage_1-7](/help/sites-administering/assets/chlimage_1-7.png)

### 產品的系列品種 {#product-variants}

對於適當的產品，還可以保存有關變型的資訊。 例如，對於可用顏色不同的服裝項目，將保留為變型：

![生態產品變異](/help/sites-administering/assets/ecommerceproductvariants.png)

### 產品屬性 {#product-attributes}

每個產品所保留的各個屬性可能取決於所使用的電子商務引擎和您AEM的實施。 在查看產品頁面和/或編輯產品資訊時，這些功能（視情況而定）可用，並可包括：

* **影像**

   產品的影像。

* **標題**

   產品名稱。

* **說明**

   產品的文本說明。

* **標記**

   用於對相關產品進行分組的標籤。

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

   產品功能的更全面細節。

### 產品資產 {#product-assets}

可為單個產品保留資產的選擇。 通常包括影像和視頻。

## 目錄 {#catalogs}

目錄將產品資料分組在一起，以方便管理和讓購物者展示。 目錄通常根據語言、地理區域、品牌、季節、愛好、體育等屬性進行結構化。

### 目錄結構 {#catalog-structure}

#### 多語言目錄 {#catalogs-in-multiple-languages}

支AEM持多種語言的產品內容。 當請求資料時，整合框架從當前樹中檢索語言(例如， `en_US` 頁 `/content/geometrixx-outdoors/en_US`)。

對於多語言儲存，可以單獨導入每個語言樹的目錄(或通過 [MSM](/help/sites-administering/msm.md))。

#### 多品牌目錄 {#catalogs-for-multiple-brands}

與語言一樣，大型跨國公司可能需要迎合多個品牌的需求。

#### 按標籤列出的目錄 {#catalogs-by-tags}

標籤也可用於將產品組合到目錄中。 這些目錄可用於更動態的目錄，如季節性優惠。

### 目錄設定（初始導入） {#catalog-setup-initial-import}

根據實施情況，您可以將基礎目錄所需的產品資料從以下產品導入AEM:

* a CSV檔案（用於一般實現）
* 電子商務引擎

### 目錄維護（資料同步） {#catalog-maintenance-data-synchronization}

產品資料的進一步更改將不可避免：

* 對於通用實現，可通過 [產品編輯器](/help/commerce/cif-classic/administering/generic.md#editing-product-information)
* 使用 [電子商務引擎必須同步更改](#data-synchronization-with-an-ecommerce-engine-ongoing)

#### 與電子商務引擎的資料同步（持續） {#data-synchronization-with-an-ecommerce-engine-ongoing}

初始導入後，對產品資料的更改將不可避免。

當使用電子商務引擎時，產品資料將在其中維護，並且需要在中AEM提供。 更新時需要同步此產品資料。

這取決於資料類型：

* A [週期同步與更改的資料饋送一起使用](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#product-synchronization-and-publishing)。

   除此之外，您還可以為快速更新選擇特定更新。

* 從商業引擎為每個頁面請求檢索高度易失的資料，如價格資訊，以確保它始終是最新的。

### 目錄 — 效能和擴展 {#catalogs-performance-and-scaling}

從電子商務引擎(PIM)中導入大量產品（通常超過100,000個）的大目錄，由於節點數量大，會影響系統。 如果產品具有關聯的資產（如產品影像），則還可以減慢創作實例的速度。 這是由於這些資產的後處理需要佔用大量CPU和記憶體。

您可以選擇多種策略來解決這些問題：

* [分段](#bucketing)  — 適應大量節點
* [將資產後處理卸載到專用實例](#offload-asset-post-processing-to-a-dedicated-instance)
* [僅導入產品資料](#only-import-product-data)
* [導入限制和批量保存](#import-throttling-and-batch-saves)
* [效能測試](#performance-testing)
* [效能 — 雜項](#performance-miscellaneous)

#### 分段 {#bucketing}

如果JCR節點有許多直接子節點（如1000個以上），則需要儲存段（幻像資料夾）以確保效能不受影響。 這些是在導入時根據算法生成的。

這些儲存段採用虛擬資料夾的形式，這些資料夾被引入到目錄結構中，但可以進行配置，以便它們在公共URL中不明顯。

#### 將資產後處理卸載到專用實例 {#offload-asset-post-processing-to-a-dedicated-instance}

此方案包括設定兩個作者實例：

1. 主作者實例

   從PIM導入產品資料，在PIM上禁用了資產路徑的後處理。

1. 專用DAM作者實例

   從PIM導入和後處理產品資產，然後將這些資產複製回主作者實例以供使用。

![體系結構圖](/help/sites-administering/assets/chlimage_1-8.png)

#### 僅導入產品資料 {#only-import-product-data}

對於產品不包含要導入的資產（影像）的情況，您可以導入產品資料而不受資產後處理的影響。

![體系結構圖](/help/sites-administering/assets/chlimage_1-9.png)

#### 效能測試 {#performance-testing}

在實施電子商務時，必須考AEM慮效能測試：

* 作者環境：

   背景（例如導入）活動可與正常用戶活動（例如頁面編輯）同時發生，即使前端效能（通常）被給予較高的優先順序，線上作者看到的不良效能也可能導致能夠阻止即時決定的沮喪。

* 發佈環境：

   複製是確保內容快速、可靠地發佈的關鍵過程。 這可能受作者對要發佈的內容進行分組的方式的影響。

* 前端：

   前端和快取失效的混合可能導致效能意外。 測試有助於避免這些問題。

請注意，此效能測試需要瞭解並分析您的目標：

* 內容卷

   * Assets
   * 本地化、I18ned產品和SKU

* 用戶活動：

   * 批量版
   * 批量發佈
   * 密集搜索請求

* 後台進程

   * 進口
   * 同步更新（例如定價）

* 維護要求（備份、Tar PM優化、資料儲存垃圾收集等）

#### 效能 — 雜項 {#performance-miscellaneous}

對於所有實施，可以牢記以下幾點：

* 作為產品，庫存單位和類別可以很多，嘗試使用盡可能少的節點來對內容進行建模。

   節點越多，內容就越靈活（例如parsys）。 但是，一切都是權衡，在操作（例如）30K產品時，您是否需要個人的靈活性（預設情況下）?

* 盡量避免重複（請參閱本地化），或者當您重複時，請考慮複製將導致多少節點。
* 嘗試盡可能多地標籤內容以準備查詢優化。

   例如：

   `/content/products/france/fr/shoe/reebok/pump/46 SKU`

   每個內容級別（即國家/地區、語言、類別、品牌、產品）應有一個標籤。 搜索

   `//element(*,my:Sku)[@country=’france’ and @language=’fr’`

   和

   `@category=’shoe’ and @brand=’reebok’ and @product=’pump’]`

   會比尋找更快

   `/jcr:root/content/france/fr/shoe/reebok/pump/element(*,my:Sku)`

* 在您的技術堆棧中，規劃非常分工的內容訪問模型和服務。 這是一般的最佳做法，但更為關鍵的是，在優化階段，您可以為經常讀取的資料添加應用程式快取（並且您不想用它填充捆綁包快取）。

   例如，屬性管理經常是快取的一個很好的候選項，因為它涉及通過產品導入更新的資料。
* 考慮使用 [代理頁](#proxy-pages)。

### 目錄節頁 {#catalog-section-pages}

目錄節提供了以下功能：

* 類別簡介（影像和/或文本）;這也可用於橫幅和茶具，以推廣特價優惠
* 連結到該類別中的單個產品
* 連結到其他類別

![eCommerce_category運行](/help/sites-administering/assets/ecommerce_categoryrunning.png)

### 產品頁面 {#product-pages}

產品頁面提供有關單個產品的全面資訊。 還反映了動態更新；例如，在電子商務引擎上註冊的價格更改。

產品頁AEM是使用 **產品** 元件；例如，在 **商業產品** 模板：

![電子商務_nairobirunnersgreen](/help/sites-administering/assets/ecommerce_nairobirunnersgreen.png)

產品元件提供：

* 一般產品資訊；包括文字和影像。
* 定價；通常每次顯示/刷新頁面時都從電子商務引擎檢索。
* 產品變型資訊；例如，顏色和大小。

此資訊允許購物者在將商品添加到購物籃時選擇以下內容：

* 顏色和大小變型
* 數量

#### 產品登錄頁 {#product-landing-pages}

這些頁面AEM主要提供靜態資訊；例如，介紹和概述，其中包含指向基礎產品頁的連結。

### 產品元件 {#product-component}

的 **產品** 可以將元件添加到任何具有父頁的頁面中，該父頁可提供所需的元資料(即到 `cartPage` 和 `cartObject`)。 在演示場所，Geometrixx Outdoors，這由 `UserInfo.jsp`。

的 **產品** 也可以根據您的個別要求定制元件。

### 代理頁 {#proxy-pages}

代理頁用於簡化儲存庫的結構並優化大目錄的儲存。

建立目錄將使用每個產品10個節點，因為它為您可以在中更新和自定義的每個產品提供了各個AEM元件。 如果您的目錄包含數百甚至數千種產品，則大量節點可能會成為問題。 要避免任何問題，可以使用代理頁建立目錄。

代理頁使用雙節點結構( `cq:Page` 和 `jcr:content`)，但不包含任何實際產品內容。 在請求時，通過引用產品資料和模板頁生成內容。

然而，這是一種取捨。 您將無法在中自定義產品資訊AEM，將使用標準模板（為您的站點定義）。

>[!NOTE]
>
>如果導入沒有代理頁的大型目錄，則不會遇到任何問題。
>
>可以隨時從一種方法轉換到另一種方法。 也可以轉換目錄的子部分。

## 促銷和憑單 {#promotions-and-vouchers}

### 憑單 {#vouchers}

憑單是一種經過試驗和檢驗的提供折扣的方法，可以吸引購物者購買和/或獎勵顧客的忠誠。

* 憑證供應：

   * 憑證代碼（由購物者輸入購物車）。
   * 憑證標籤（在購物者將其輸入購物車後顯示）。
   * 升級路徑（定義憑證應用的操作）。

* 外部商務引擎也可提供憑證。

在AEM:

* 憑單是使用網站控制台建立/編輯的基於頁面的元件。
* 的 **憑證** 元件提供：

   * 憑證管理的呈現者；這顯示購物車中當前的任何憑證。
   * 用於管理（添加/刪除）憑證的編輯對話框（表單）。
   * 在購物車中添加/刪除憑單所需的操作。

* 憑單沒有其自己的開/關日期/時間，但使用其父市場活動的日期/時間。

>[!NOTE]
>
>使AEM用術語 **憑證**，這和術語 **優惠券**。

### 促銷活動 {#promotions}

促銷和憑單使您能夠實現以下情形：

* 公司為員工提供定制價格，這是手工編製的用戶清單。
* 長期客戶可按所有訂單獲得折扣。
* 在明確定義的時間段內提供的售價。
* 當客戶的上一訂單超過特定金額時，客戶將收到憑單。
* 購買的客戶 *產品 — X* 優惠是 *產品 — Y* （對產品）。

促銷通常不是由產品資訊經理維護的，而是由營銷經理維護的：

* 升級是使用網站控制台建立/編輯的基於頁面的元件。 &quot;
* 促銷供應：

   * 優先順序
   * 升級處理程式路徑

* 您可以將促銷與市場活動連接，以定義其開/關日期/時間。
* 您可以將促銷與體驗相連，以定義其細分市場。
* 與體驗無關的促銷不會自行啟動，但仍然可以通過憑單啟動。
* 升級元件包含：

   * 提升管理的呈現者和對話
   * 用於呈現和編輯特定於升級處理程式的配置參數的子元件

在AEM促銷中， [Campaign Management](/help/sites-authoring/personalization.md):

* a [活動](/help/sites-authoring/personalization.md) 指定開/關時間
* [體驗](/help/sites-authoring/personalization.md) *內* 市場活動用於根據其對應的受眾段對資產（預告頁、促銷等）進行分組

促銷可以通過經驗進行，也可以直接在活動中進行：

* 如果促銷是以經驗進行的，則它可自動應用於受眾部分。

   例如，在geometrixx-outdoors示例站點中，升級：

   `/content/campaigns/geometrixx-outdoors/big-spender/ordervalueover100/free-shipping`

   是經驗，因此在段( `ordervalueover100`)解析。

* 如果促銷未在體驗中出現（僅在市場活動中），則它不能自動應用於受眾。 但是，如果購物者將憑單輸入購物車中，而該憑單是促銷的參考，則仍可以解雇。

   例如，促銷：

   `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

   不在體驗範圍內，因此從不自動觸發(即：基於分割)。 但是，在文章活動的若干經驗中可以找到的憑證也引用了這一點。 將這些憑證代碼輸入購物車將導致促銷觸發。

>[!NOTE]
>
>[割禮促銷](https://www.hybris.com/modules/promotion) 和 [碎物券](https://www.hybris.com/en/modules/voucher) 包括影響購物車和與定價相關的一切。 促銷特定的營銷內容（如橫幅等）不是慈善促銷的一部分。

## 個人化 {#personalization}

### 客戶註冊和帳戶 {#customer-registration-and-accounts}

當購物者註冊時，帳戶詳細資訊需要在電AEM子商務引擎之間同步。 敏感資料是獨立保存的，但配置檔案是共用的：

![chlimage_1-10](/help/sites-administering/assets/chlimage_1-10.png)

具體機制可以取決於以下情形：

1. 這兩個系統中都存在用戶帳戶：

   1. 不需要任何操作。

1. 用戶帳戶僅存在於AEM:

   1. 用戶將在電子商務引擎中建立，其帳戶ID和隨機密碼將儲存在AEM中。
   1. 隨機密碼是必需的，AEM因為第一次調用時嘗試登錄到電子商務引擎（例如，當請求產品頁並且引用電子商務引擎來獲取價格時）。 由於這種情況在登AEM錄後發生，因此密碼不可用。

1. 用戶帳戶僅存在於電子商務引擎中：

   1. 將使用相同的帳AEM戶ID和密碼建立帳戶。

使用電子商務引擎時，AEM僅儲存帳戶ID和密碼（可選地是用戶組）。 所有其他資訊都儲存在電子商務引擎中。

>[!NOTE]
>
>使用電子商務引擎時，您需要確保為登錄到實例的用戶建立的帳戶被複製AEM（例如通過工作流）到與該引擎通信的AEM任何其他實例。
>
>否則，這AEM些其他實例還將嘗試為引擎中的相同用戶建立帳戶。 這些操作將失敗， `DuplicateUidException` 從引擎上傳來的。

### 客戶註冊 {#customer-sign-up}

購物者通常需要註冊才能使用購物車。 這需要註冊（建立帳戶），以便建立特定於客戶的帳戶。

![chlimage_1-11](/help/sites-administering/assets/chlimage_1-11.png)

>[!NOTE]
>
>還支援匿名購物車和結帳。

### 客戶登錄 {#customer-sign-in}

註冊後，購物者可以使用其帳戶登錄，以便跟蹤其活動並完成其訂單。

![chlimage_1-12](/help/sites-administering/assets/chlimage_1-12.png)

### 單一登錄 {#single-sign-on}

提供單一登錄(SSO)，使得作者在電子商務系統和AEM電子商務系統中都是已知的，而不必兩次登錄。

### 我的帳戶 {#myaccount}

來自電子商務引擎的交易資料與關於購物者的個人資訊相結合。 將AEM其中一些資料用作配置檔案資料。 表單在將資訊AEM寫回電子商務引擎中的操作。

有一個頁面允許您輕鬆管理帳戶資訊。 您可以通過按一下 **我的帳戶** 在幾何頁面頂部，或導航到 `/content/geometrixx-outdoors/en/user/account.html`。

![chlimage_1-13](/help/sites-administering/assets/chlimage_1-13.png)

### 通訊錄 {#address-book}

您的站點需要儲存一系列地址；包括交貨、帳單和替代地址。 您可以使用基於預設地址格式的表單來實現此功能，也可以使用由提供的通訊簿元件AEM。

此通訊簿元件允許您：

* 編輯帳簿中的地址
* 從帳簿中選擇地址以發運地址
* 從帳簿中為開單地址選擇地址

您可以選擇要預設的地址。

可從以下站點訪問通訊簿元件： **我的帳戶** 按一下 **通訊簿** 或通過導航 `/content/geometrixx-outdoors/en/user/account/address-book.html`。

![chlimage_1-14](/help/sites-administering/assets/chlimage_1-14.png)

您可以按一下 **添加新地址……** 在通訊簿中添加新地址。 它開啟一個可以填寫的表單，然後按一下 **添加地址**。

>[!NOTE]
>
>您可以在通訊簿中輸入多個地址。

簽出購物車時，將使用通訊簿：

![chlimage_1-15](/help/sites-administering/assets/chlimage_1-15.png)

地址保留在下面 `user_home/profile/addresses`。
例如，對於Alison Parker，它位於/home/users/geometrixx/aparker@geometrixx.info/profile/addresses下

您可以選擇要預設的地址，此資訊會保留在購物者的個人資料中，而不是與地址一起。 配置檔案屬性 `address.default` 為值設定選定地址的路徑。

### 特定於客戶的定價 {#customer-specific-pricing}

電子商務引擎使用上下文（實質上是購物者資訊）來確定它所持的價格，然後將正確的資訊提供回AEM去。

## 購物車和訂單 {#shopping-cart-and-orders}

購物者在購物時將瀏覽產品頁面並選擇項目，將其放在購物車中。 當他們繼續結帳時，可以下訂單。

### 匿名購物者 {#anonymous-shoppers}

匿名客戶可以：

* 查看產品
* 將產品添加到其購物車
* 執行結帳以下單

>[!NOTE]
>
>在簽出之前，可能需要根據實例地址資訊或客戶註冊的配置進行配置。

### 註冊購物者 {#registered-shoppers}

註冊客戶可以：

* 登錄其帳戶
* 查看產品
* 將產品添加到其購物車
* 執行結帳以下單
* 查看和跟蹤以前的訂單

### 購物車內容概述 {#shopping-cart-content-overview}

購物車提供：

* 所選項的概覽
* 連結到所選項目的產品頁
* 能夠：

   * 更新單個物料的數量
   * 刪除單個項目

![電子商務_購物車](/help/sites-administering/assets/ecommerce_shoppingcart.png)

購物車根據使用的引擎進行保存：

* 通AEM用程式將購物車儲存在cookie中。
* 某些電子商務引擎可以在會話中儲存購物車。

在兩種情況下，物料都會在車中（並且可以恢復）通過登錄/註銷（但僅在同一台電腦/瀏覽器上）。 例如：

* 瀏覽 `anonymous` 將產品添加到購物車
* 登錄身份 `Allison Parker`  — 她的手推車空空
* 將產品添加到她的購物車
* 註銷 — 購物車將顯示 `anonymous`

* 再次登錄為 `Allison Parker`  — 其產品已恢復

>[!NOTE]
>
>匿名購物車只能在同一台電腦/瀏覽器上還原。

>[!NOTE]
>
>建議不要test使用 `admin` 帳戶，因為這可能與 `admin` 電子商務引擎（例如hybris）的帳戶。

>[!NOTE]
>
>可以將hybris配置為在定義的時間段後刪除掛起的cart。

在結帳前，價格更改會在發生時反映（在兩個系統中）。

### 訂單資訊 {#order-information}

根據您的實施資訊，訂單資訊會保存在電子商務引擎中，或AEM者，此資訊由提供AEM。

儲存了各種資訊，其中可包括：

* **訂單 ID**

   訂單的參考編號。

* **已下單**

   下訂單的日期。

* **狀態**

   訂單狀態；例如，「已發運」。

* **貨幣**

   訂單的幣種。

* **內容項**

   排序的項清單。

* **小計**

   訂購物料的總成本。

* **稅金**

   訂單上應繳的稅金金額。

* **送貨**

   運費。

* **總計**

   訂單總值；訂購的物品、稅款和批款。

* **帳單地址**

   應發送發票的地址。

* **付款 Token**

   付款方式。

* **付款狀態**

   付款的狀態。

* **送貨地址**

   貨物應運往的地址。

* **送貨方法**

   運輸方式；比如陸，海，空。

* **追蹤編號**

   航運公司使用的任何跟蹤編號。

* **追蹤連結**

   用於在發運時跟蹤訂單的連結。

>[!NOTE]
>
>建立順序嚮導中使用的欄位取決於是否有為位置定義的觸摸優化腳手架。 在通用示例中，可以在以下位置找到：
>`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`

當訂單保存在訂單控AEM制台中時，每個訂單都顯示以下內容：

* 購物車中的物料數
* 訂單的總值
* 訂單時
* 狀態

![chlimage_1-16](/help/sites-administering/assets/chlimage_1-16.png)

### 訂單跟蹤 {#order-tracking}

下訂單後，購物者通常會返回：

* 檢查訂單的狀態
* 從訂單中刪除產品
* 將產品添加到訂單

在收到訂單交貨後，購物者可能還希望查看一段時間內的訂單歷史記錄。

訂單履行和跟蹤通常由電子商務引擎管理。 可以使用「訂單歷史記AEM錄」元件顯示資訊，該元件顯示所有相關詳細資訊，包括所應用的憑單和促銷。 例如：

![chlimage_1-17](/help/sites-administering/assets/chlimage_1-17.png)

## 結帳 {#checkout}

簽出使用標準表AEM單實現。 這使營銷經理能夠定制營銷內容的體驗。

然後，電子商務使用來自表單的輸入來管理結AEM賬過程。

### 付款安全性 {#payment-security}

支付詳細資訊（包括信用卡資訊）通常由電子商務引擎管理。 將AEM這種事務性資訊轉發到引擎（然後從其轉發到支付處理服務）。

可實現支付卡行業(PCI)合規性。

### 訂單確認 {#confirmation-of-order}

訂單已在螢幕上確認，可以使用 [訂單跟蹤](#order-tracking)。

## 搜尋 {#search-features}

![chlimage_1-18](/help/sites-administering/assets/chlimage_1-18.png)

由AEM於產品使用標準頁，因此您可以使用標準搜索元件建立搜索頁。

如果您需要更徹底的實施，您可以：

* 使用所需功能擴展預設搜索元件。
* 在中實施搜索方法 `CommerceService` 然後在搜索頁上使用e-commerce搜索元件。

當使用電子商務引擎時，電子商務搜索API可以在電子商務引擎解決方案中完全實現，因此您可以使用出廠時提供的電子商務搜索元件。 多面搜索允許您搜索JCR和/或引擎：
