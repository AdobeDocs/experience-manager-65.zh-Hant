---
title: 內容傳送
description: 內容傳送
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: 85e73679-684e-402f-8186-8b56d8bd9372
source-git-commit: fd8bb7d3d9040e0a7a6b2f65751445f41aeab73e
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 1%

---

# 內容傳送{#content-delivery}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）的專案，使用SPA編輯器。 [深入了解](/help/sites-developing/spa-overview.md)。

行動應用程式應該能夠視需要使用AEM中的所有內容，以提供鎖定目標的應用程式體驗。

這包括使用資產、網站內容、CaaS內容（透過The-Air）內容，以及可能有專屬結構的自訂內容。

>[!NOTE]
>
>**無線內容** 可以透過ContentSync處理常式來自上述任何一項。 它可用來透過ZIP將封裝和傳送分批以及維護這些封裝的更新。

Content Services提供三種主要型別的資料：

1. **Assets**
1. **封裝的HTML內容(HTML/CSS/JS)**
1. **獨立於管道的內容**

![chlimage_1-154](assets/chlimage_1-154.png)

## Assets {#assets}

資產集合是包含其他集合參考的AEM建構。

資產集合可以透過Content Services公開。 呼叫請求中的資產集合時，會傳回資產清單中的物件，包括其URL。 資產可透過URL存取。 URL是在物件中提供的。 例如：

* 頁面實體會傳回包含影像參考的JSON（頁面物件）。 影像參考是用來取得影像資產二進位檔的URL。
* 對資料夾中資產清單的請求會傳回JSON以及該資料夾中所有實體的詳細資訊。 該清單是一個物件。 JSON的URL參照用來取得該資料夾中每個資產的二進位檔案。

### 資產最佳化 {#asset-optimization}

Content Services的重要價值在於可傳回已針對裝置最佳化的資產。 這樣可以減少本機裝置的儲存需求，並改善應用程式效能。

資產最佳化是一種伺服器端函式，根據API請求中提供的資訊。 應儘可能快取資產轉譯，使類似的請求不需要重新產生資產轉譯。

### 資產工作流程 {#assets-workflow}

資產工作流程如下：

1. AEM中現成可用的資產參考
1. 根據模型建立資產參考實體
1. 編輯實體

   1. 挑選資產或資產集合
   1. 自訂JSON演算

下圖顯示 **資產參考工作流程**：

![chlimage_1-155](assets/chlimage_1-155.png)

### 管理資產 {#managing-assets}

Content Services可讓您存取無法透過其他AEM內容參考的AEM管理的資產。

#### 現有的受管理資產 {#existing-managed-assets}

AEM Sites和Assets的使用者正使用AEM Assets來管理其所有頻道的所有數位資料。 他們正在開發原生行動應用程式，且需要使用AEM Assets管理的數個資產。 例如標誌、背景影像和按鈕圖示。

目前，這些功能會分散在資產存放庫中。 應用程式必須參考的檔案如下：

* /content/dam/geometrixx-outdoors/brand/logo_light.png
* /content/dam/geometrixx-outdoors/brand/logo_dark.png
* /content/dam/geometrixx-outdoors/styles/backgrounds/grey_blue.jpg
* /content/dam/geometrixx-outdoors/brand/icons/app/cart.png
* /content/dam/geometrixx-outdoors/brand/icons/app/home.png

#### 存取CS資產實體 {#accessing-cs-asset-entities}

暫時將透過API提供頁面的步驟放在一邊(AEM UI說明將涵蓋此頁面)，並假設此步驟已完成。 已建立資產實體並新增至「appImages」空間。 已在空間下建立其他資料夾以供組織使用。 因此，資產實體在AEM JCR中儲存為：

* /content/entities/appImages/logos/logo_light
* /content/entities/appImages/logos/logo_dark
* /content/entities/appImages/bkgnd/gray_blue
* /content/entities/appImages/icons/cart
* /content/entities/appImages/icons/home

#### 取得可用資產實體清單 {#getting-a-list-of-available-asset-entities}

應用程式開發人員可透過擷取資產實體來取得可用資產清單。 內容服務空間端點可透過網站服務API SDK提供該資訊。

結果會是JSON格式的物件，提供「圖示」資料夾中的資產清單。

![chlimage_1-156](assets/chlimage_1-156.png)

#### 取得影像 {#getting-an-image}

JSON會為Content Services產生的每個影像提供一個URL至影像。

若要取得「購物車」影像的二進位檔，系統會再次使用使用者端資料庫。

## 封裝的HTML內容 {#packaged-html-content}

需要維護內容配置的客戶需要HTML內容。 這對於使用Web容器（例如Cordova Webview）顯示內容的原生應用程式非常有用。

AEM Content Services會透過API將HTML內容提供給行動應用程式。 想要將AEM內容公開為HTML的客戶可以建立指向AEM內容來源的HTML頁面實體。

考量到下列選項：

* **Zip檔案：** 為了儘可能在裝置上正確顯示，頁面參考的資料 — css、JavaScript、資產等會包含在含有回應的單一壓縮檔案中。 可以調整「HTML」頁面中的參照，以使用這些檔案的相對路徑。
* **串流：** 從AEM取得必要檔案的資訊清單。 然後使用該資訊清單來要求所有具有後續要求的檔案(HTML、CSS、JS等)。

![chlimage_1-157](assets/chlimage_1-157.png)

## 與頻道無關的內容 {#channel-independent-content}

獨立於管道的內容是一種公開AEM內容建構（例如頁面）而不需擔心版面、元件或其他管道特定資訊的方式。

這些內容實體是使用內容模型產生的，用於將AEM結構轉譯為JSON格式。 產生的JSON資料包含與AEM存放庫分離的內容資料相關資訊。 這包括傳回資產的中繼資料和AEM參考連結，以及內容結構（包括實體階層）之間的關係。

### 管理獨立於管道的內容 {#managing-channel-independent-content}

內容可以透過數種方式進入應用程式。

1. 透過AEM Over-The-AirGET內容ZIP

   * 內容同步處理常式可以直接更新zip套件，或呼叫現有的內容轉譯器

      * 平台處理常式
      * AEM處理常式
      * 自訂處理常式

1. 直接透過內容轉譯器GET內容

   * 現成可用的預設Sling轉譯器
   * AEM Mobile/Content Services內容轉譯器
   * 自訂轉譯
