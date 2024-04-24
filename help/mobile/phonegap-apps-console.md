---
title: 使用應用程式控制檯建立和編輯應用程式
description: 請依照本頁面的說明操作，瞭解如何使用應用程式主控台建立和編輯應用程式。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 49e0b3f6-7ac7-4417-9c31-cc3d3c2305f3
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2675'
ht-degree: 1%

---

# 使用應用程式控制檯建立和編輯應用程式{#creating-and-editing-apps-using-the-apps-console}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）的專案，使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md)。

AEM行動應用程式開發程式認可了擁有不同專業知識的使用者對行動應用程式開發的貢獻。 下列程式圖說明內容作者和應用程式開發人員執行工作的一般順序。

![chlimage_1-10](assets/chlimage_1-10.gif)

有關如何執行行銷人員工作的資訊會顯示在此頁面上。 如需開發人員工作的相關資訊，請參閱建立PhoneGap應用程式。

## 行動應用程式的結構 {#the-structure-of-mobile-applications}

AEM Mobile提供Phonegap應用程式藍圖，供您建立行動應用程式。 藍圖會定義您建立的應用程式結構。 應用程式包含下列專案：

* 根頁面。
* 應用程式的語言變化。
* 語言變數的首頁。

### Phonegap應用程式的根目錄 {#the-root-of-a-phonegap-app}

您在AEM中建立的行動應用程式根頁面，會顯示在應用程式主控台中。

根頁面儲存在建立應用程式時所指定之應用程式的「目的地路徑」屬性下方（預設路徑為/content/phonegap/apps）。 頁面名稱是應用程式的Name屬性。 例如，網站根頁面的預設URL命名為 `myphonegapapp` 是 `http://localhost:4502/content/phonegap/apps/myphonegapapp.html`.

![chlimage_1-146](assets/chlimage_1-146.png)

### PhoneGap應用程式的語言變化 {#the-language-variation-of-a-phonegap-app}

根頁面的第一個子頁面是應用程式的語言變體。 每個頁面的名稱是建立應用程式的語言。 例如，English是應用程式的英文變數名稱。

**注意：** 預設的PhoneGap Blueprint只會建立英文應用程式。 您的開發人員可以修改Blueprint，以便建立更多語言變體。

![chlimage_1-147](assets/chlimage_1-147.png)

語言頁面有兩個用途：

* 頁面內容是應用程式語言變數的垃圾頁面。
* 頁面屬性可控制應用程式的幾個設計方面，例如用於請求內容更新的URL，以及有關連線至雲端組建和Adobe Analytics服務整合的資訊。

![chlimage_1-148](assets/chlimage_1-148.png)

### 首頁 {#the-home-page}

開啟應用程式時，會出現應用程式語言變化的「首頁」或index.html頁面。 首頁為使用者提供一個功能表，其中包含應用程式中各個頁面的連結。 段落系統可讓您新增元件至頁面以建立內容。

## 建立行動應用程式 {#creating-a-mobile-application}

行動應用程式以定義頁面結構和屬性的Blueprint為基礎。 您可以設定下列應用程式屬性：

* **標題：** 應用程式標題。
* **目的地路徑：** 儲存應用程式的存放庫位置。 保留預設值，以根據應用程式名稱建立路徑。

* **名稱：** 預設值為移除空白字元的Title屬性值。 CQ會使用名稱來參照應用程式，例如代表應用程式的儲存庫節點。
* **說明：** 應用程式的說明。
* **伺服器URL：** 為應用程式提供無線內容(OTA)更新的URL。 預設值是用來建立應用程式（取自外部器服務）之執行個體的發佈伺服器URL。 請注意，這必須是發佈伺服器執行個體，而非作者（需要驗證）。

您也可以提供影像檔案，以用作應用程式縮圖、選取要使用的PhoneGap Build設定，並選取要使用的行動應用程式分析設定。 此影像僅會作為縮圖，在Experience Manager的行動應用程式主控台內代表您的行動應用程式。

其他（和選用）標籤可用於建立雲端服務，以及將Adobe Mobile Services SDK外掛程式整合至您的應用程式。

* 組建：按一下這裡的管理設定並設定您的build.phonegap.com組建服務。 然後從下拉式清單，選取新建立的PhoneGap Build雲端服務。
* Analytics：按一下管理設定並設定您的 [AdobeMobile Services SDK](https://experienceleague.adobe.com/docs/mobile-services/using/home.html) 雲端服務。 然後從下拉式清單，選取新建立的行動服務以整合至行動應用程式。

>[!NOTE]
>
>開發人員可使用AEM PhoneGap Starter Kit建立應用程式，並將其新增至主控台。

下列程式會使用Touch UI建立行動應用程式。

1. 在邊欄上，按一下「應用程式」 。
1. 按一下建立圖示。

   ![正方形內由加號指示的「建立」圖示。](do-not-localize/chlimage_1-7.png)

1. （可選）在進階標籤上，提供應用程式的說明，並視需要變更伺服器URL。
1. （選擇性）如果您使用PhoneGap Build編譯應用程式，請在「建置」標籤上選取要使用的組態。

   若要建立PhoneGap Build設定，請按一下「管理設定」。

1. （選用）如果您是使用SiteCatalyst追蹤應用程式活動，請在Analytics索引標籤上選取要使用的設定。

   若要建立行動應用程式設定，請按一下管理設定。

1. （選擇性）若要提供應用程式圖示，請按一下「瀏覽」按鈕，從您的檔案系統選取影像檔案，然後按一下「開啟」。
1. 按一下「建立」。

### 變更行動應用程式的屬性 {#changing-the-properties-of-a-mobile-application}

建立行動應用程式後，您可以變更屬性。

#### 變更標題、說明和圖示 {#change-the-title-description-and-icon}

1. 在邊欄上，按一下「應用程式」 。
1. 選取要設定的應用程式，然後按一下「檢視頁面屬性」圖示。

   ![圓形內以字母I表示的「檢視頁面屬性」圖示。](do-not-localize/chlimage_1-8.png)

1. 若要變更屬性值，請按一下「編輯」圖示。

   ![鉛筆所指示的編輯圖示。](do-not-localize/chlimage_1-9.png)

1. 設定「基本」和「進階」屬性，然後按一下「完成」圖示。

   ![以核取記號符號表示的「完成」圖示。](do-not-localize/chlimage_1-10.png)

#### 設定應用程式的語言變化 {#configure-a-language-variation-of-the-application}

1. 在邊欄上，按一下「應用程式」 。
1. 按一下以深入探究您要在應用程式Admin Console中編輯的行動應用程式。 選取要設定的應用程式語言版本，然後按一下「檢視應用程式屬性」圖示。

   ![在圓圈內以字母I表示的「檢視應用程式屬性」圖示。](do-not-localize/chlimage_1-11.png)

1. 若要變更屬性值，請按一下「編輯」圖示。

   ![鉛筆所指示的編輯圖示。](do-not-localize/chlimage_1-12.png)

1. 在「基本」、「進階」、「建置」和「Analytics」標籤上設定屬性，然後按一下「完成」圖示。

   ![以核取記號符號表示的「完成」圖示。](do-not-localize/chlimage_1-13.png)

### 編寫行動應用程式的內容 {#authoring-the-content-of-a-mobile-application}

建立行動應用程式後，請新增用作應用程式UI的內容。

1. 在邊欄上，按一下「應用程式」 。
1. 按一下應用程式，然後按一下英文。
1. 編輯首頁，或視需要新增子頁面。

### 將內容移動至行動應用程式 {#moving-content-to-mobile-applications}

AEM發佈執行個體上的Content Sync快取會作為行動應用程式的內容存放庫使用：

* 開發人員編譯應用程式時，應用程式會包含Content Sync快取中的內容。
* 快取中的內容可供已安裝的行動應用程式用來更新應用程式內容。

行動應用程式包含更新命令，可下載和安裝更新的應用程式內容。 當應用程式執行個體傳送更新請求時，Content Sync會判斷自上次更新或安裝應用程式以來哪些內容已變更，並提供新內容。

![chlimage_1-149](assets/chlimage_1-149.png)

若要讓更新的內容可供應用程式使用，請更新Content Sync快取。 第一次更新快取時，會新增所有發佈的內容。 後續更新只會新增自上次更新以來已變更的已發佈內容。

Content Sync也會追蹤更新何時發生。 有了這些資訊，Content Sync就可以判斷要傳送給行動應用程式的快取更新。

在您要更新快取的執行處理上執行下列程式。 例如，如果您的應用程式要求更新發佈執行個體，請在發佈執行個體上執行程式。

1. 在邊欄上，按一下應用程式，然後按一下您的應用程式。
1. 選取啟動顯示頁面，然後按一下「更新快取」圖示。

   ![更新快取圖示以帶有回收符號的條狀橫條圖示表示。](do-not-localize/chlimage_1-14.png)

### 使用應用程式範本 {#using-app-templates}

這是Apps 6.1 Feature Pack 2提供的功能，可讓您輕鬆使用現有的應用程式範本，在AEM中建立新的應用程式。

什麼是應用程式範本？ 將其視為代表應用程式基準或基礎的頁面範本和元件的集合。
根據其他應用程式的範本建立應用程式時，您會得到其起點代表在其中建立該應用程式之應用程式的應用程式。

您必須擁有現有的行動應用程式範本（或已安裝具備應用程式範本的應用程式），才能使用此功能。

最新AEM Apps 6.1範例套件包含具有應用程式範本的Geometrixx應用程式更新版本。 或者，您可以安裝也提供範本的StarterKit。

根據應用程式範本建立應用程式的步驟：

1. 確保您已安裝最新的AEM Apps 6.1 Feature Pack和參考範例套件
1. 從左側邊欄按一下「應用程式」 。

![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. 按一下頂端的+建立按鈕，然後選取建立應用程式。
1. 向您出示應用程式範本清單後，請選取一項：

![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. 按一下「下一步」。
1. 提供應用程式ID和標題，不過您可能也要包含名稱和說明。

   1. 您也可以瀏覽AEM資產，以提供PNG （支援的PhoneGap圖示格式）作為圖示。
   1. 請記得，在「管理應用程式」方塊中建立應用程式後，您可以編輯所有這些欄位。 應用程式ID除外，一旦設定了應用程式ID，您就無法加以變更。

![chlimage_1-150](assets/chlimage_1-150.png)

1. 按一下建立按鈕，畫面會顯示兩個選項：完成（返回應用程式目錄檢視）或管理應用程式（開啟應用程式控制面板）。
1. 建立後，您應該會在應用程式目錄中看到新應用程式的清單：

![chlimage_1-3](assets/chlimage_1-3.jpeg)

1. 按一下應用程式以開啟，表示您已成功根據現有應用程式的範本建立新應用程式。

>[!NOTE]
>
>如果您從AEM解除安裝Geometrixx Outdoors參考應用程式套件，並根據其範本建立應用程式，則該應用程式將無法再正常運作。 Geometrixx Outdoors應用程式可以移除，但如果其他行動應用程式正在使用它，則必須保留應用程式範本。

## 探索範例Geometrixx Outdoors應用程式 {#exploring-the-sample-geometrixx-outdoors-app}

Geometrixx Outdoors應用程式是範例PhoneGap應用程式，示範預設PhoneGap應用程式Blueprint和範例行動元件的功能。

若要開啟應用程式，請從邊欄按一下行動應用程式，然後選取Geometrixx Outdoors應用程式。

### 常見頁面功能 — Geometrixx行動應用程式 {#common-page-features-geometrixx-mobile-app}

行動應用程式的每個頁面都包含下列功能：

* 返回父頁面的返回按鈕。 首頁沒有顯示上一頁按鈕。
* 提供指令和連結功能表的可消耗邊欄：

   * 開啟「位置」頁面。
   * 開啟購物車。
   * 登入。
   * 更新應用程式。

* 段落系統，用於新增元件和建立內容。

### 首頁 — Geometrixx行動應用程式 {#the-home-page-geometrixx-mobile-app}

首頁的內容包含下列導覽工具：

* 選單清單元件會提供「齒輪」、「評論」、「新聞」和「關於我們」子頁面的連結。
* 可顯示子頁面的撥動轉盤元件。

### 齒輪頁面 — Geometrixx行動應用程式 {#the-gear-page-geometrixx-mobile-app}

「齒輪」頁面可讓使用者存取產品頁面。 選單清單元件可讓您存取「齒輪」頁面的子頁面。 子頁面是網站具有功能的產品類別。

* 季數
* 服裝
* 性別
* 活動

每個類別頁面都使用與「齒輪」頁面相同的內容結構。 輪播可讓您存取子頁面，這些子頁面是產品的子類別。 子類別頁面包含產品清單，提供產品頁面的連結。

### 產品頁面 — Geometrixx行動應用程式 {#the-products-page-geometrixx-mobile-app}

「產品」頁面及其子頁面的階層會實施產品頁面的分類系統。 階層每個分支中的最低頁面是包含ng Product元件的產品頁面。

應用程式使用者無法使用「產品」頁面。 「齒輪」頁面提供每個產品頁面的存取權。

### 評論頁面 — Geometrixx行動應用程式 {#the-reviews-page-geometrixx-mobile-app}

包含上一頁按鈕。 段落系統可讓您新增元件。

使用應用程式時，可以從英文頁面的輪播存取「稽核」頁面。

### 新聞頁面 — Geometrixx行動應用程式 {#the-news-page-geometrixx-mobile-app}

包含上一頁按鈕。 段落系統可讓您新增元件。

使用應用程式時，可從英文頁面的輪播取得「新聞」頁面。

### 我們的相關頁面 — Geometrixx行動應用程式 {#the-about-us-page-geometrixx-mobile-app}

「關於我們」頁面包含數個雙欄列元件。 每一欄都包含影像或文字元件。 元件可編輯，而段落系統可讓您新增元件。

使用應用程式時，可以從英文頁面的轉盤存取「關於我們」頁面。

### 位置頁面 — Geometrixx行動應用程式 {#the-locations-page-geometrixx-mobile-app}

「位置」頁面包含「位置」元件。

使用應用程式時，可以從英文頁面上的功能表清單使用「位置」頁面。

## 行動元件範例 {#sample-mobile-components}

編寫行動應用程式的頁面時，Sidekick會立即提供數個元件。 元件屬於PhoneGap元件群組。

### 撥動傳送 {#swipe-carousel}

撥動轉盤元件是展示和導覽網站頁面的工具。 此元件包含一個輪播，可在頁面連結清單上方的頁面上循環播放影像。 編輯元件，以指定要公開的頁面和轉盤行為。

請注意，影像會以特定方式顯示在關聯至影像之頁面的轉盤中。 當頁面未與影像關聯時，只會顯示連結清單。

![chlimage_1-151](assets/chlimage_1-151.png)

**轉盤屬性索引標籤**

設定輪播的行為：

* 播放速度：顯示下一個影像前每個影像顯示的時間（以毫秒為單位）。
* 過渡時間：影像過渡的動畫持續時間（毫秒）。
* 控制項樣式：為在影像之間移動而提供的控制項型別。

**清單屬性索引標籤**

指定產生頁面清單的方式：

* 建立清單使用：用來指定要在轉盤中包含的頁面的方法。 請參閱建立頁面清單。
* 排序依據：選取要用於排序頁面清單的頁面屬性。 例如，選取jcr：title依標題的字母順序排序頁面。
* 上限：要包含的最大頁數。 此屬性適用於以搜尋為基礎的建立頁面清單方法。

#### 建立頁面清單 {#building-the-page-list}

撥動轉盤元件為「使用建置清單」屬性提供下列值。 編輯對話方塊會根據您選取的值而變更：

**子頁面**

元件會列出特定頁面的所有子頁面。 選取這個值之後，請在「子頁面」標籤上選取頁面，或指定沒有值來列出目前頁面的子頁面。

**固定清單**

指定包含頁面的清單。 選取此值後，請設定當您選取「固定清單」時顯示的「固定清單」標籤上的清單：

* 若要新增頁面，請按一下「新增專案」，然後瀏覽頁面。
* 使用向上和向下箭頭圖示在清單中移動頁面。
* 按一下移除按鈕，從清單中移除頁面。

Order By屬性不會影響固定清單的順序。

**搜尋**

使用關鍵字搜尋結果填入清單。 會在您指定之頁面的子系中執行搜尋：

1. 若要指定搜尋的根頁面，請使用[開始於]屬性來選取頁面路徑。 指定目前頁面下方沒有要搜尋的路徑。
1. 在「搜尋查詢」屬性中，輸入搜尋關鍵字。

**進階搜尋**

使用填入清單 [Querybuilder](/help/sites-developing/querybuilder-api.md) 查詢。

### 影像 {#image}

將影像新增至應用程式內容。

### 文字 {#text}

將RTF文字新增至您的應用程式內容。

### 商店位置 {#store-locations}

「商店位置」元件為使用者提供尋找商業銷售點的工具：

* 搜尋
* 鄰近或遠離裝置GPS座標的位置清單。

元件要求存放庫包含每個存放區的位置資訊。 範例位置安裝在/etc/commerce/locations/adobe節點上。 ![chlimage_1-152](assets/chlimage_1-152.png)

### 兩欄列 {#two-column-row}

可讓您將並排元件新增至頁面。

![chlimage_1-153](assets/chlimage_1-153.png)
