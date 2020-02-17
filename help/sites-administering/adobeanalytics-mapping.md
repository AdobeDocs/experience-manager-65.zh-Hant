---
title: 使用Adobe Analytics屬性對應元件資料
seo-title: 使用Adobe Analytics屬性對應元件資料
description: 瞭解如何使用SiteCatalyst屬性映射元件資料。
seo-description: 瞭解如何使用SiteCatalyst屬性映射元件資料。
uuid: b08ab37f-ad58-4c04-978f-8e21a3823ae8
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6c1f8869-62d9-4fac-aa0d-b99bb0e86d6b
docset: aem65
translation-type: tm+mt
source-git-commit: 6f49e01aa3e9841c7b2917870593452b778667d2

---


# 使用Adobe Analytics屬性對應元件資料{#mapping-component-data-with-adobe-analytics-properties}

將元件新增至架構，以收集要傳送至Adobe Analytics的資料。 用來收集分析資料的元件會將資料儲存在適當的 **CQ變數中**。 將此類元件新增至架構時，架構會顯示CQ變數清單，讓您可以將每個變數都新增至適當的 **Analytics變數**。

![aa-11](assets/aa-11.png)

當 **AEM檢視開啟** 時，Analytics變數會出現在內容搜尋器中。

![aa-12](assets/aa-12.png)

您可以使用相同的 **CQ變數來對應多個Analytics變數**。

![chlimage_1-68](assets/chlimage_1-68.png)

當頁面載入並符合下列條件時，會將映射的資料傳送至Adobe Analytics:

* 頁面與框架相關聯。
* 該頁使用添加到框架的元件。

請依照下列步驟，將CQ元件變數與Adobe Analytics報表屬性對應。

1. 在 **AEM檢視中**，將追蹤元件從sidekick拖曳至架構上。 例如，從「一般 **」類別拖曳** 「頁面」元 **件元件** 。

   ![aa-13](assets/aa-13.png)

   有數個預設元件群組：一般 **商務**, **社區**，促 **進和促**********&#x200B;進其他搜索。 您的AEM例項可以設定為顯示不同的群組和元件。

1. 若要將Adobe Analytics變數與元件中定義的變數對應，請將 **** Analytics變數從內容搜尋器拖曳至追蹤元件上的欄位。 例如，拖曳 `Page Name (pageName)` 至 `pagedata.title`。

   ![aa-14](assets/aa-14.png)

   >[!NOTE]
   >
   >為架構選取的報表套裝ID(RSID)會決定顯示在內容搜尋器中的Adobe Analytics變數。

1. 對其他元件和變數重複上述兩個步驟。

   >[!NOTE]
   >
   >您可以映射多個Analytics變數(例如 `props`、 `eVars`、 `events`)至相同的CQ變數(例如 `pagedata.title`)

   >[!CAUTION]
   >
   >強烈建議：
   >    
   >    * `eVars` 並 `props` 且映射至以或開頭的CQ變 `pagedata.X` 數 `eventdata.X`
      >    
      >    
   * 而事件應映射至變數，從 `eventdata.events.X`


1. 若要讓架構在您網站的發佈例項上可用，請開啟sidekick的 **Page** 標籤，然後按一下 **啟動架構。**

## 對應與產品相關的變數 {#mapping-product-related-variables}

AEM使用慣例來命名要對應至Adobe Analytics產品相關屬性的產品相關變數和事件：

| CQ變數 | Analytics變數 | 說明 |
|---|---|---|
| `product.category` | `product.category` （轉換變數） | 產品類別。 |
| `product.sku` | `product.sku` （轉換變數） | 產品sku。 |
| `product.quantity` | `product.quantity` （轉換變數） | 所購買的產品數。 |
| `product.price` | `product.price` （轉換變數） | 產品價格。 |
| `product.events.<eventName>` | 要與報表中的產品相關聯的成功事件。 | `product.events` 是名為eventName之事件的首 *碼。* |
| `product.evars.<eVarName>` | 要與產品關聯的 `eVar`轉換變數()。 | `product.evars` 是名為eVarName的eVar變數 *的首碼。* |

數個AEM Commerce元件會使用這些變數名稱。

>[!NOTE]
>
>請勿將Adobe Analytics產品屬性對應至CQ變數。 如表格中所述，設定產品相關映射實際上等同於映射產品變數。

### 檢查Adobe Analytics的報表 {#checking-reports-on-adobe-analytics}

1. 使用提供給AEM的相同認證登入Adobe Analytics網站。
1. 請確定選取的RSID是前述步驟中使用的RSID。
1. 在報 **表中** （位於頁面左側），依序選 **取自訂轉換**、 **自訂轉換1-10** ，並選取與 `eVar7`

1. 視您使用的Adobe Analytics版本而定，您需要等候平均45分鐘，才能使用搜尋詞更新報表；例如茄子

## 搭配Adobe Analytics架構使用內容搜尋器(cf#) {#using-the-content-finder-cf-with-adobe-analytics-frameworks}

一開始，當您開啟Adobe Analytics架構時，內容搜尋器會在下列位置包含預先定義的Analytics變數：

* 流量
* 轉換
* 事件

當選取RSID時，屬於該RSID的所有變數都會新增至清單。\
需 `cf#` 要將Analytics變數對應至不同追蹤元件上顯示的CQ變數。 請參閱設定基本追蹤的架構。

根據為架構選取的檢視，內容搜尋器將由Analytics變數（在AEM檢視中）或CQ變數（在Analytics檢視中）填入。

可通過以下方式操控清單：

1. 在 **AEM檢視中**，可依據使用3個篩選按鈕選取的變數類型來篩選清單：

   * 如果 *未選取按鈕* ，清單會顯示完整清單。
   * 如果選 **取「流量** 」按鈕，清單只會顯示屬於「流量」區段的變數。
   * 如果選 **取「轉換** 」按鈕，清單只會顯示屬於「轉換」區段的變數。
   * 如果選 **取「事件** 」按鈕，清單只會顯示屬於「事件」區段的變數。
   >[!NOTE]
   >
   >一次只能使用一個篩選按鈕。

   >[!NOTE]
   >
   >Search&amp;Promote變數也屬於「轉換」區段。

   1. 清單也有搜尋功能，可根據搜尋欄位中輸入的文字來篩選元素。
   1. 如果在搜尋清單中的元素時啟用篩選選項，則也會根據作用中按鈕來篩選顯示的結果。
   1. 您可以隨時使用旋流箭頭按鈕重新載入清單。
   1. 如果在框架上選擇了多個RSID，則會使用所選RSID內使用的所有標籤來顯示清單中的所有變數。


1. 在Adobe Analytics檢視中時，Content Finder會顯示屬於CQ檢視中拖曳之追蹤元件的所有CQ變數。

   * 例如，在CQ檢視中， **Download元件是僅拖曳的元件** (此元件有兩個可映射的變數eventdata.downloadLink *和***** eventdata.events.startDownloadDownload)，當切換至Adobe Analytics檢視時，Content Finder會顯示為：
   ![aa-22](assets/aa-22.png)

   * 這些變數可拖放至屬於3個變數區段(流量、轉換和事件&#x200B;**)之一的任何Adobe Analytics變數**( **Traffic****、Conversion**&#x200B;和Events)。

   * 在CQ檢視中將新追蹤元件拖曳至架構時，屬於元件的CQ變數會自動新增至Adobe Analytics檢視的Content Finder(cf#)。
   >[!NOTE]
   >
   >一次只能將一個CQ變數對應至Adobe Analytics變數

## 使用AEM檢視和Analytics檢視 {#using-aem-view-and-analytics-view}

在任何指定時間，使用者都可以選擇在框架頁面上檢視Adobe Analytics映射的2種方式。 2個視圖從2個不同角度提供了框架內映射的更好概述。

### AEM檢視 {#aem-view}

![aa-23](assets/aa-23.png)

以上影像為例， **AEM檢視具有** 下列屬性：

1. 這是框架開啟時的預設視圖。
1. 左側：內容搜尋器(cf#)是由Adobe Analytics變數根據選取的RSID填入。
1. 標籤標題(**AEM檢視****和Analytics檢視**):使用這些功能在兩個視圖之間切換。

1. **AEM檢視**:

   1. 如果框架具有繼承自其父代的元件，則這些元件將列在此處，並與映射到元件的變數一起列出。

      1. 繼承的元件被鎖定。
      1. 若要解除鎖定繼承的元件，只需按兩下元件名稱旁的掛鎖即可
      1. 要恢復繼承，您必須刪除解鎖的元件；之後，它將重新獲得鎖定地位。
   1. **將元件拖曳至此處，將其納入分析架構中**:元件可從Sidekick拖曳並拖曳至此處。
   1. 您可以找到分析架構中目前包含的所有元件：

      1. 若要新增元件，請從sidekick的「元件」索引標籤拖曳元件
      1. 要刪除元件及其所有映射，請從元件的上下文菜單中選擇「刪除」，然後在確認對話框上接受刪除。
      1. 請記住，元件只能從其中建立的架構中刪除，而無法從傳統意義上從子架構中刪除（只能覆寫）。


### Analytics檢視 {#analytics-view}

![aa-24](assets/aa-24.png)

1. 此檢視可切換至架構上的 **Analytics檢視標籤** ，加以存取。
1. 左側：根據CQ檢視中拖曳至架構的元件，由CQ變數填入的Content Finder(cf#)。
1. 標籤標題(**AEM檢視****和Analytics檢視**):使用這些功能在兩個視圖之間切換。

1. 三個表格（流量、轉換、事件）會列出所有可用的Adobe Analytics變數。 屬於所選的RSID。 此處顯示的對應應與AEM檢視中的對應相同：

   * **流量**:

      * 對應至CQ變 `prop1`數()的流量變數( `eventdata.downloadLink`)

      * 當元件旁有Padlock時，這表示它繼承自父框架，因此無法編輯
   * **轉換**:

      * 轉換變數( `eVar1`)對應至CQ變數( `pagedata.title`)

      * 將轉換變數( `eVar3`)對應至內嵌新增的javascript運算式，方法是連按兩下CQ變數欄位並手動輸入程式碼
   * **事件**:

      * 映射到CQ `event1`事件( `eventdata.events.pageView`)的事件變數



>[!NOTE]
>
>任何表格的CQ變數欄也可以內嵌填入，方法是連按兩下欄位並新增文字。 這些欄位接受javascript作為輸入。
>
>* 例如，您可在 `prop3` 新增
>* `'`* `Adobe:'+pagedata.title+':'+pagedata.sitesection`\
   >  *若要傳送*&#x200B;與其網站&#x200B;*區段串連之頁面*&#x200B;的標題&#x200B;*，請使用*:（冒號）並加上 *Adobe* 前置詞 `prop3`
>



>[!CAUTION]
>
>在任何指定時間，只能將一個CQ變數對應至Adobe Analytics變數。

