---
title: 使用Adobe Analytics屬性映射元件資料
seo-title: Mapping Component Data with Adobe Analytics Properties
description: 瞭解如何使用SiteCatalyst屬性映射元件資料。
seo-description: Learn how to map component data with SiteCatalyst properties.
uuid: b08ab37f-ad58-4c04-978f-8e21a3823ae8
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6c1f8869-62d9-4fac-aa0d-b99bb0e86d6b
docset: aem65
exl-id: c7c0c705-ec16-40f5-ad08-193f82d01263
source-git-commit: 58594be73372e128ba999a8290615fbcb447084e
workflow-type: tm+mt
source-wordcount: '1445'
ht-degree: 0%

---

# 使用Adobe Analytics屬性映射元件資料{#mapping-component-data-with-adobe-analytics-properties}

將元件添加到框架中以收集要發送到Adobe Analytics的資料。 用於收集分析資料的元件將資料儲存在適當的 **CQ變數**。 將此類元件添加到框架時，框架將顯示CQ變數清單，以便您可以將每個變數都添加到相應的 **分析變數**。

![aa-11](assets/aa-11.png)

當 **AEM視圖** 開啟內容查找器中顯示的分析變數。

![aa-12](assets/aa-12.png)

可以使用相同的變數映射多個分析變數 **CQ變數**。

![chlimage_1-68](assets/chlimage_1-68.png)

當載入頁並滿足以下條件時，映射的資料將發送到Adobe Analytics:

* 該頁與框架關聯。
* 該頁使用添加到框架的元件。

請按下列步驟將CQ元件變數與Adobe Analytics報告屬性映射。

1. 在 **AEM視圖**，將跟蹤元件從側腳拖到框架上。 例如，拖動 **頁面** 元件 **常規** 的子菜單。

   ![aa-13](assets/aa-13.png)

   有幾個預設元件組： **常規**。 **商業**。 **社區**, **其他**。 實例AEM可配置為顯示不同的組和元件。

1. 要用元件中定義的變數映射Adobe Analytics變數，請拖動 **分析變數** 從內容查找器到跟蹤元件上的欄位。 例如，拖動 `Page Name (pageName)` 至 `pagedata.title`。

   ![aa-14](assets/aa-14.png)

   >[!NOTE]
   >
   >為框架選擇的報告套件ID(RSID)確定了內容查找器中顯示的Adobe Analytics變數。

1. 對其它元件和變數重複前兩個步驟。

   >[!NOTE]
   >
   >可以映射多個分析變數(例如 `props`。 `eVars`。 `events`)到同一CQ變數(例如 `pagedata.title`)

   >[!CAUTION]
   >
   >強烈建議：
   >
   >* `eVars` 和 `props` 映射到以下任一值開頭的CQ變數 `pagedata.X` 或 `eventdata.X`
   >* 而事件應映射到以 `eventdata.events.X`


1. 要使框架在網站的發佈實例上可用，請開啟 **頁面** 頁籤，然後按一下 **激活框架。**

## 映射產品相關變數 {#mapping-product-related-variables}

使AEM用約定來命名與產品相關的變數和事件，這些變數和事件應映射到與Adobe Analytics產品相關的屬性：

| CQ變數 | 分析變數 | 說明 |
|--- |--- |--- |
| `product.category` | `product.category` （轉換變數） | 產品類別。 |
| `product.sku` | `product.sku` （轉換變數） | 產品SKU。 |
| `product.quantity` | `product.quantity` （轉換變數） | 正在購買的產品數。 |
| `product.price` | `product.price` （轉換變數） | 產品價格。 |
| `product.events.<eventName>` | 要與報告中的產品關聯的成功事件。 | `product.events` 是名為 *eventName。* |
| `product.evars.<eVarName>` | 轉換變數( `eVar`)與產品關聯。 | `product.evars` 是名為的eVar變數的前置詞 *eVarName。* |

幾個AEMCommerce元件使用這些變數名稱。

>[!NOTE]
>
>不要將Adobe Analytics產品屬性映射到CQ變數。 如表中所述，配置與產品相關的映射實際上等效於映射Products變數。

### 檢查有關Adobe Analytics的報告 {#checking-reports-on-adobe-analytics}

1. 使用提供給的相同憑據登錄Adobe Analytics網AEM站。
1. 確保所選RSID是前面步驟中使用的RSID。
1. 在 **報告** （在頁面左側）選擇 **自定義轉換**，則 **自定義轉換1-10** 並選擇與 `eVar7`

1. 根據您使用的Adobe Analytics版本，您需要平均等待45分鐘，才能使用搜索詞更新報告；例如茄子

## 將Content Finder(cf#)與Adobe Analytics框架配合使用 {#using-the-content-finder-cf-with-adobe-analytics-frameworks}

最初，當您開啟Adobe Analytics框架時，內容查找器將包含以下預定義的分析變數：

* 流量
* 轉換
* 事件

當選擇RSID時，屬於該RSID的所有變數都將添加到清單中。\
的 `cf#` 需要將分析變數映射到不同跟蹤元件上存在的CQ變數。 請參閱設定基本跟蹤框架。

根據為框架選擇的視圖，內容查找器將由分析變數（在視圖中）或CQ變數(在分AEM析視圖中)填充。

可通過以下方式操縱清單：

1. 在 **AEM視圖**，根據使用3個篩選器按鈕選擇的變數類型，可以篩選清單：

   * 如果 *無按鈕* 的子菜單。
   * 如果 **流量** 按鈕，清單將僅顯示屬於「流量」節的變數。
   * 如果 **轉換** 按鈕，清單將僅顯示屬於「轉換」部分的變數。
   * 如果 **事件** 按鈕，清單將只顯示屬於「事件」部分的變數。

   >[!NOTE]
   >
   >一次只能激活一個篩選器按鈕。

   1. 該清單還具有搜索功能，該搜索功能根據在搜索欄位中輸入的文本過濾元素。
   1. 如果在搜索清單中的元素時激活了篩選器選項，則顯示的結果也將根據活動按鈕進行篩選。
   1. 可以隨時使用旋轉箭頭按鈕重新載入清單。
   1. 如果在框架上選擇了多個RSID，則使用選定RSID內使用的所有標籤將顯示清單中的所有變數。


1. 在Adobe Analytics視圖中時，Content Finder顯示屬於在CQ視圖中拖動的跟蹤元件的所有CQ變數。

   * 例如，在 **下載元件** 是 *只拖* 在CQ視圖中(具有兩個可映射的變數 *eventdata.downloadLink* 和 *eventdata.events.start下載*)，切換到Adobe Analytics視圖時， Content Finder的外觀將如下所示：

   ![aa-22](assets/aa-22.png)

   * 可將變數拖放到屬於3個變數部分之一的任何Adobe Analytics變數(**流量**。 **轉換** 和 **事件**)。

   * 在CQ視圖中將新跟蹤元件拖到框架上時，屬於該元件的CQ變數將自動添加到Adobe Analytics視圖中的Content Finder(cf#)中。
   >[!NOTE]
   >
   >在任何給定時間，只能將一個CQ變數映射到Adobe Analytics變數。

## 使用AEM視圖和分析視圖 {#using-aem-view-and-analytics-view}

在任何給定時間，用戶都可以選擇在框架頁面上查看Adobe Analytics映射的兩種方式之間切換。 這2個視圖從2個不同的角度提供了框架內映射的更好概覽。

### 視AEM圖 {#aem-view}

![aa-23](assets/aa-23.png)

以上影像為例， **AEM視圖** 具有以下屬性：

1. 這是框架開啟時的預設視圖。
1. 左側：內容查找器(cf#)由基於所選RSID的Adobe Analytics變數填充。
1. 頁籤標題(**AEM視圖** 和 **分析視圖**):使用這些視圖在兩個視圖之間切換。

1. **AEM視圖**:

   1. 如果框架具有從其父級繼承的元件，則這些元件將與映射到這些元件的變數一起列在此處。

      1. 已鎖定繼承的元件。
      1. 要解鎖繼承的元件，只需按兩下元件名稱旁的掛鎖
      1. 要恢復繼承，必須刪除未鎖定的元件；之後它將重新獲得鎖定狀態。
   1. **將元件拖到此處，以將其包括在分析框架中**:元件可從Sidekick中拖動並放在此處。
   1. 您可以找到分析框架中當前包含的所有元件：

      1. 要添加元件，請從側腳的「元件」頁籤中拖動一個元件
      1. 要刪除元件及其所有映射，請從元件的上下文菜單中選擇「刪除」，然後在確認對話框上接受刪除。
      1. 請記住，元件只能從建立於的框架中刪除，不能從傳統意義上的子框架中刪除（只能覆蓋）。


### 分析視圖 {#analytics-view}

![aa-24](assets/aa-24.png)

1. 通過切換到 **分析視圖** 的子菜單。
1. 左側：Content Finder(cf#)由CQ變數填充，這些變數基於在CQ視圖中拖到框架上的元件。
1. 頁籤標題(**AEM視圖** 和 **分析視圖**):使用這些視圖在兩個視圖之間切換。

1. 三個表（通信、轉換、事件）列出所有可用的Adobe Analytics變數。 屬於選定的RSID。 此處顯示的映射應與視圖中的映AEM射相同：

   * **流量**:

      * 流量變數( `prop1`)映射到CQ變數( `eventdata.downloadLink`)

      * 當元件旁邊有掛鎖時，這意味著它繼承自父框架，因此無法編輯
   * **轉換**:

      * 轉換變數( `eVar1`)映射到CQ變數( `pagedata.title`)

      * 轉換變數( `eVar3`)映射到內嵌添加的javascript表達式，方法是按兩下CQ變數欄位並手動輸入代碼
   * **Event**:

      * 事件變數( `event1`)映射到CQ事件( `eventdata.events.pageView`)



>[!NOTE]
>
>任何表的CQ變數列也可以內聯填充，方法是按兩下該欄位並向其中添加文本。 這些欄位接受javascript作為輸入。
>
>例如，在 `prop3` 可以添加：
>     `'`* `Adobe:'+pagedata.title+':'+pagedata.sitesection`\
發送 *標題* 與其連接的頁 *站點節* 使用 *:* （冒號）和前置詞 *Adobe* 如 `prop3`

>[!CAUTION]
在任何給定時間，只能將一個CQ變數映射到Adobe Analytics變數。
