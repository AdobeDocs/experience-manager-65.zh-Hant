---
title: 內容交付
seo-title: Content Delivery
description: 內容交付
seo-description: null
uuid: 1e7bea34-ca50-41ed-8295-fa182c27fa69
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 3d65cc6b-5721-472f-a805-588d50f3571b
exl-id: 85e73679-684e-402f-8186-8b56d8bd9372
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 1%

---

# 內容交付{#content-delivery}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

移動應用應能根據需要使用任何和AEM所有內容來提供目標應用體驗。

這包括使用資產、站點內容、 CaaS內容（空中）和可能具有其自身結構的定製內容。

>[!NOTE]
>
>**空中內容** 可以通過ContentSync處理程式從以上任意位置獲得。 它可用於通過zip批處理包和交貨，以及維護更新或這些包。

Content Services提供的資料有三種主要類型：

1. **Assets**
1. **打包的HTML內容(HTML/CSS/JS)**
1. **渠道獨立內容**

![chlimage_1-154](assets/chlimage_1-154.png)

## Assets {#assets}

資產集合是AEM包含對其他集合的引用的構造。

資產集合可通過Content Services公開。 在請求中調用資產集合將返回資產清單的對象，包括其URL。 通過URL訪問資產。 URL在對象中提供。 例如：

* 頁實體返回包含影像引用的JSON（頁對象）。 影像引用是用於獲取影像資產二進位檔案的URL。
* 對資料夾中資產清單的請求返回JSON，其中包含該資料夾中所有實體的詳細資訊。 那個清單是個對象。 JSON具有URL引用，用於獲取該資料夾中每個資產的資產二進位檔案。

### 資產優化 {#asset-optimization}

Content Services的一個關鍵價值是能夠返回針對設備優化的資產。 這減少了本地設備儲存需求並提高了應用程式效能。

基於API請求中提供的資訊，資產優化將是伺服器端函式。 如果可能，應快取資產格式副本，這樣類似的請求就不需要重新生成資產格式副本。

### 資產工作流 {#assets-workflow}

資產工作流如下所示：

1. 開箱即用AEM的資產參考
1. 建立給定其模型的資產參考實體
1. 編輯實體

   1. 挑選資產或資產收集
   1. 自定義JSON呈現

下圖顯示 **資產參考工作流**:

![chlimage_1-155](assets/chlimage_1-155.png)

### 管理資產 {#managing-assets}

Content Services提供了對可AEM能未通過其他內容引用的托管資AEM產的訪問。

#### 現有托管資產 {#existing-managed-assets}

現有的AEM Sites和資產用戶正在使用AEM Assets管理其所有渠道的所有數字資料。 他們正在開發一款本地移動應用，需要使用由AEM Assets管理的多種資產。 例如徽標、背景影像、按鈕表徵圖等。

當前，這些資源分佈在Assets儲存庫周圍。 應用程式需要引用的檔案位於：

* /content/dam/geometrixx-outdoors/brand/logo_light.png
* /content/dam/geometrixx-outdoors/brand/logo_dark.png
* /content/dam/geometrixx-outdoors/styles/backgrounds/gray_blue.jpg
* /content/dam/geometrixx-outdoors/brand/icons/app/cart.png
* /content/dam/geometrixx-outdoors/brand/icons/app/home.png

#### 訪問CS資產實體 {#accessing-cs-asset-entities}

讓我們暫且擱置通過API使頁面可用的步驟(該頁面將在AEMUI說明中覆蓋)，並假定已完成。 資產實體已建立並添加到「appImages」空間。 已在空間下為組織目的建立其他資料夾。 因此，資產實體儲存在AEMJCR中，如下：

* /content/entities/appImages/logos/logo_light
* /content/entities/appImages/logos/logo_dark
* /content/entities/appImages/bkgnd/gray_blue
* /content/entities/appImages/icons/cart
* /content/entities/appImages/icons/home

#### 獲取可用資產實體清單 {#getting-a-list-of-available-asset-entities}

應用開發者可以通過檢索資產實體來獲取可用資產的清單。 Content Services空間終結點可以通過Web服務API SDK提供該資訊。

結果將是JSON格式的對象，該對象將提供「表徵圖」資料夾中的資產清單。

![chlimage_1-156](assets/chlimage_1-156.png)

#### 獲取影像 {#getting-an-image}

JSON為每個影像提供由Content Services生成的URL。

要獲取「購物車」映像的二進位檔案，請再次使用客戶端庫。

## 打包的HTML內容 {#packaged-html-content}

HTML內容是需要維護內容佈局的客戶所需要的。 這對於使用Web容器（如Cordova Webview）來顯示內容的本機應用程式非常有用。

內AEM容服務將能夠通過API向移動應用提供HTML內容。 希望將內AEM容作為HTML公開的客戶將建立指向內容源的HTML頁AEM面實體。

將考慮以下選項：

* **Zip檔案：** 為了在設備上正確顯示，頁面的所有引用材料（css、JavaScript、資產等）都有最佳的顯示機會。  — 將包含在具有響應的單個壓縮檔案中。 將調整HTML頁中的引用，以使用這些檔案的相對路徑。
* **流：** 從獲取所需檔案的清單AEM。 然後使用該清單請求所有檔案(HTML、CSS、JS等) 以後的請求。

![chlimage_1-157](assets/chlimage_1-157.png)

## 渠道獨立內容 {#channel-independent-content}

渠道獨立內容是一種公開內AEM容結構（如頁面）而不必擔心佈局、元件或其他渠道特定資訊的方法。

這些內容實體是使用內容模型生成的，以AEM將結構轉換為JSON格式。 生成的JSON資料包含有關內容資料的資訊，該資訊與儲存庫AEM分離。 這包括返回元資料AEM和指向資產的引用連結以及內容結構之間的關係，包括實體層次結構。

### 管理與渠道無關的內容 {#managing-channel-independent-content}

內容可以通過多種方式訪問該應用。

1. GET內AEM容ZIPS通過空中

   * 內容同步處理程式可以直接或通過調用現有內容呈現程式更新zip包

      * 平台處理程式
      * AEMM處理程式
      * 自定義處理程式

1. 直接通過內容GET器

   * 出廠設定預設投注程式
   * AEM Mobile/內容服務內容呈現器
   * 自定義呈現
