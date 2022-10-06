---
title: 內容傳送
seo-title: Content Delivery
description: 內容傳送
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
ht-degree: 0%

---

# 內容傳送{#content-delivery}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

行動應用程式應可視需要使用AEM中的任何及所有內容，以提供目標應用程式體驗。

這包括使用資產、網站內容、CaaS內容（通過空中）和可能具有其自身結構的定製內容。

>[!NOTE]
>
>**空中內容** 可透過ContentSync處理常式來自上述任何一個。 它可用於批次封裝和透過zip傳送，以及維護更新或這些封裝。

內容服務提供的材料有三種主要類型：

1. **Assets**
1. **封裝HTML內容(HTML/CSS/JS)**
1. **獨立於頻道的內容**

![chlimage_1-154](assets/chlimage_1-154.png)

## Assets {#assets}

資產集合是AEM建構，包含對其他集合的參考。

資產集合可透過內容服務公開。 在請求中呼叫資產集合會傳回資產清單（包括其URL）的物件。 資產可透過URL存取。 URL提供在物件中。 例如：

* 頁面實體會傳回JSON（頁面物件），其中包含影像參考。 影像參考是用於取得影像資產二進位檔的URL。
* 若要求取得資料夾中的資產清單，系統會傳回JSON，其中包含該資料夾中所有實體的詳細資訊。 該清單是一個對象。 JSON的URL參考可用來取得該資料夾中每個資產的資產二進位檔。

### 資產最佳化 {#asset-optimization}

「內容服務」的關鍵價值在於能夠傳回已針對裝置最佳化的資產。 這可減少本機裝置儲存需求並改善應用程式效能。

根據API請求中提供的資訊，資產最佳化將是伺服器端函式。 盡可能快取資產轉譯，因此類似的請求不需要重新產生資產轉譯。

### Assets工作流程 {#assets-workflow}

資產工作流程如下：

1. AEM現成可用的資產參考資料
1. 根據資產參考實體的模型建立資產參考實體
1. 編輯實體

   1. 挑選資產或資產收集
   1. 自訂JSON轉譯

下圖顯示 **資產參考工作流程**:

![chlimage_1-155](assets/chlimage_1-155.png)

### 管理資產 {#managing-assets}

內容服務提供對AEM管理資產的存取，這些資產可能不會透過其他AEM內容參照。

#### 現有受管資產 {#existing-managed-assets}

現有的AEM Sites和Assets使用者正使用AEM Assets管理其所有管道的所有數位資料。 他們正在開發原生行動應用程式，且需要使用由AEM Assets管理的數個資產。 例如標誌、背景影像、按鈕圖示等。

目前，這些範本分散在資產存放庫中。 應用程式需要參考的檔案位於：

* /content/dam/geometrixx-outdoors/brand/logo_light.png
* /content/dam/geometrixx-outdoors/brand/logo_dark.png
* /content/dam/geometrixx-outdoors/styles/backgrounds/gray_blue.jpg
* /content/dam/geometrixx-outdoors/brand/icons/app/cart.png
* /content/dam/geometrixx-outdoors/brand/icons/app/home.png

#### 訪問CS Asset Entities {#accessing-cs-asset-entities}

現在先暫且說明如何透過API提供頁面的步驟(AEM UI說明將涵蓋此頁面)，然後假設已完成。 資產實體已建立並新增至「appImages」空間。 已在空間下建立其他資料夾以供組織使用。 因此，資產實體會儲存在AEM JCR中，如下所示：

* /content/entities/appImages/logos/logo_light
* /content/entities/appImages/logos/logo_dark
* /content/entities/appImages/bkgnd/gray_blue
* /content/entities/appImages/icons/cart
* /content/entities/appImages/icons/home

#### 取得可用資產實體的清單 {#getting-a-list-of-available-asset-entities}

應用程式開發人員可擷取資產實體，以取得可用資產的清單。 內容服務空間端點可以透過Web服務API SDK提供該資訊。

結果會是JSON格式的物件，提供「圖示」資料夾中的資產清單。

![chlimage_1-156](assets/chlimage_1-156.png)

#### 取得影像 {#getting-an-image}

JSON會為每個影像提供URL，由內容服務產生給影像。

若要取得「購物車」影像的二進位檔，系統會再次使用用戶端程式庫。

## 封裝HTML內容 {#packaged-html-content}

HTML內容是需要維護內容佈局的客戶所需的。 這對於使用Web容器（如Cordova Webview）來顯示內容的原生應用程式非常有用。

AEM Content Services將能透過API提供HTML內容給行動應用程式。 想要以HTML形式公開AEM內容的客戶將建立指向AEM內容來源的HTML頁面實體。

考量下列選項：

* **Zip檔案：** 為了在裝置上正確顯示，頁面的所有參考資料（css、JavaScript、資產等）都是最佳時機。  — 將包含在單一壓縮檔案中並附回應。 HTML頁面中的參考將會經過調整，以使用這些檔案的相對路徑。
* **串流：** 從AEM取得必要檔案的資訊清單。 然後使用該資訊清單來請求所有檔案(HTML、CSS、JS等) 和後續的要求。

![chlimage_1-157](assets/chlimage_1-157.png)

## 管道獨立內容 {#channel-independent-content}

管道獨立內容是公開AEM內容建構（例如頁面）的方式，不需擔心版面、元件或其他管道特定資訊。

這些內容實體是使用內容模型產生，以將AEM結構轉譯為JSON格式。 產生的JSON資料包含與AEM存放庫脫鈎的內容資料相關資訊。 這包括傳回中繼資料和AEM參考連結至資產，以及內容結構（包括實體階層）之間的關係。

### 管理與管道無關的內容 {#managing-channel-independent-content}

內容可透過數種方式存取應用程式。

1. GET內容透過AEM Over-the-Air ZIP

   * 內容同步處理常式可以直接更新zip套件，或呼叫現有內容轉譯者

      * 平台處理常式
      * AEMM處理常式
      * 自訂處理常式

1. 直接透過內容轉譯器GET內容

   * 現成可用的Sling預設轉譯器
   * AEM Mobile/內容服務內容轉譯器
   * 自訂轉譯
