---
title: 使用Adobe Analytics屬性對應元件資料
description: 瞭解如何使用SiteCatalyst屬性對應元件資料。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: c7c0c705-ec16-40f5-ad08-193f82d01263
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '1449'
ht-degree: 0%

---

# 使用Adobe Analytics屬性對應元件資料{#mapping-component-data-with-adobe-analytics-properties}

將元件新增至框架，以收集要傳送至Adobe Analytics的資料。 設計用來收集分析資料的元件，會將資料儲存在適當的&#x200B;**CQ變數**&#x200B;中。 當您將這類元件新增到框架時，該框架會顯示CQ變數清單，以便您可以將每個變數新增到適當的&#x200B;**Analytics變數**。

![aa-11](assets/aa-11.png)

當&#x200B;**AEM檢視**&#x200B;開啟時，Analytics變數會出現在內容尋找器中。

![aa-12](assets/aa-12.png)

您可以使用相同的&#x200B;**CQ變數**&#x200B;對應多個Analytics變數。

![chlimage_1-68](assets/chlimage_1-68.png)

當頁面載入且符合下列條件時，會將對應的資料傳送至Adobe Analytics：

* 頁面與框架相關聯。
* 頁面會使用新增至框架的元件。

使用以下程式，將CQ元件變數與Adobe Analytics報表屬性對應。

1. 在&#x200B;**AEM檢視**&#x200B;中，將追蹤元件從sidekick拖曳到架構上。 例如，從&#x200B;**一般**&#x200B;類別拖曳&#x200B;**頁面**&#x200B;元件。

   ![aa-13](assets/aa-13.png)

   有幾個預設元件群組： **一般**、**Commerce**、**社群**&#x200B;和&#x200B;**其他**。 您的AEM執行個體可設定為顯示不同的群組和元件。

1. 若要使用元件中定義的變數對應Adobe Analytics變數，請從內容尋找器將&#x200B;**Analytics變數**&#x200B;拖曳至追蹤元件上的欄位。 例如，將`Page Name (pageName)`拖曳至`pagedata.title`。

   ![aa-14](assets/aa-14.png)

   >[!NOTE]
   >
   >為框架選取的報表套裝ID (RSID)會決定顯示在內容尋找器中的Adobe Analytics變數。

1. 對其他元件和變數重複前兩個步驟。

   >[!NOTE]
   >
   >您可以將多個Analytics變數（例如`props`、`eVars`、`events`）對應到相同的CQ變數（例如`pagedata.title`）

   >[!CAUTION]
   >
   >強烈建議：
   >
   >* `eVars`和`props`對應到以`pagedata.X`或`eventdata.X`開頭的CQ變數
   >* 而事件應該對應到以`eventdata.events.X`開頭的變數

1. 若要讓架構可在您網站的發佈執行個體上使用，請開啟sidekick的&#x200B;**頁面**&#x200B;標籤，然後按一下&#x200B;**啟動架構**。

## 對應產品相關變數 {#mapping-product-related-variables}

AEM使用慣例來命名產品相關變數和事件，這些變數和事件會對應至Adobe Analytics產品相關屬性：

| CQ變數 | 分析變數 | 說明 |
|--- |--- |--- |
| `product.category` | `product.category` （轉換變數） | 產品類別。 |
| `product.sku` | `product.sku` （轉換變數） | 產品sku。 |
| `product.quantity` | `product.quantity` （轉換變數） | 正在購買的產品數量。 |
| `product.price` | `product.price` （轉換變數） | 產品價格。 |
| `product.events.<eventName>` | 與報表中的產品建立關聯的成功事件。 | `product.events`是名為&#x200B;*eventName.*&#x200B;之事件的前置詞 |
| `product.evars.<eVarName>` | 要與產品產生關聯的轉換變數( `eVar`)。 | `product.evars`是名為&#x200B;*eVarName.*&#x200B;之eVar變數的前置詞 |

有幾個AEM Commerce元件會使用這些變數名稱。

>[!NOTE]
>
>請勿將Adobe Analytics Products屬性對應至CQ變數。 依照表格所述設定產品相關對應，實際上等同於對應產品變數。

### 在Adobe Analytics上檢查報告 {#checking-reports-on-adobe-analytics}

1. 使用提供給AEM的相同憑證登入Adobe Analytics網站。
1. 請確定選取的RSID是先前步驟中所使用的RSID。
1. 在&#x200B;**報表** （頁面左側）中，選取&#x200B;**自訂轉換**，然後選取&#x200B;**自訂轉換1-10**，並選取與`eVar7`相對應的變數

1. 根據您使用的Adobe Analytics版本，您平均需要等待45分鐘，報表才會更新為使用的搜尋字詞；例如，範例中的eggplant

## 搭配Adobe Analytics架構使用內容尋找器(cf#) {#using-the-content-finder-cf-with-adobe-analytics-frameworks}

最初，當您開啟Adobe Analytics架構時，內容尋找器會包含以下預先定義的Analytics變數：

* 流量
* 轉換
* 事件

選取RSID時，屬於該RSID的所有變數都會新增到清單中。\
需要`cf#`才能將Analytics變數對應到出現在不同追蹤元件上的CQ變數。 請參閱設定基本追蹤的框架。

根據為框架選取的檢視，內容尋找器將由Analytics變數(在AEM檢視中)或CQ變數（在Analytics檢視中）填入。

清單可透過下列方式操作：

1. 在&#x200B;**AEM檢視**&#x200B;中，可以使用三個篩選按鈕，根據選取的變數型別來篩選清單：

   * 如果未選取&#x200B;*按鈕*，清單會顯示完整清單。
   * 如果選取&#x200B;**流量**&#x200B;按鈕，清單將僅顯示屬於流量區段的變數。
   * 如果選取&#x200B;**轉換**&#x200B;按鈕，清單將僅顯示屬於轉換區段的變數。
   * 如果選取&#x200B;**事件**&#x200B;按鈕，清單只會顯示屬於事件區段的變數。

   >[!NOTE]
   >
   >一次只能啟用一個篩選器按鈕。

   1. 清單也有搜尋功能，可依據在搜尋欄位中輸入的文字篩選元素。
   1. 如果在搜尋清單中的元素時啟用了篩選選項，則顯示的結果也會根據活動按鈕進行篩選。
   1. 清單可隨時使用旋轉箭頭按鈕重新載入。
   1. 如果在架構上選取了多個RSID，清單中的所有變數都會使用選取的RSID內使用的所有標籤來顯示。

1. 在Adobe Analytics檢視中，內容尋找器會顯示屬於CQ檢視中拖曳之追蹤元件的所有CQ變數。

   * 例如，如果&#x200B;**Download元件**&#x200B;是CQ檢視中唯一拖曳的&#x200B;*元件* （有兩個可對應的變數&#x200B;*eventdata.downloadLink*&#x200B;和&#x200B;*eventdata.events.startDownload*），當切換至Adobe Analytics檢視時，內容尋找器會變成這樣：

   ![aa-22](assets/aa-22.png)

   * 可將變數拖放至屬於三個變數區段（**流量**、**轉換**&#x200B;和&#x200B;**事件**）其中之一的任何Adobe Analytics變數上。

   * 將新的追蹤元件拖曳至CQ檢視的框架時，屬於該元件的CQ變數會自動新增至Adobe Analytics檢視的內容尋找器(cf#)。

   >[!NOTE]
   >
   >在任何指定時間，都只能將一個CQ變數對應至Adobe Analytics變數。

## 使用AEM檢視和Analytics檢視 {#using-aem-view-and-analytics-view}

在任何指定時間，使用者在框架頁面上時，可以在兩種檢視Adobe Analytics對應的方式之間切換。 這兩個檢視從兩個不同的角度提供架構內對應的更佳概述。

### AEM檢視 {#aem-view}

![aa-23](assets/aa-23.png)

以上圖為例，**AEM檢視**&#x200B;有下列屬性：

1. 這是框架開啟時的預設檢視。
1. 左側：內容尋找器(cf#)會由Adobe Analytics變數根據所選的RSID填入。
1. Tab標頭(**AEM檢視**&#x200B;和&#x200B;**Analytics檢視**)：使用這些標頭在兩個檢視之間切換。

1. **AEM檢視**：

   1. 如果框架具有從其父項繼承的元件，則會在此處列出這些元件，以及對應到元件的變數。

      1. 繼承的元件將被鎖定。
      1. 若要解除鎖定繼承的元件，請連按兩下元件名稱旁的掛鎖
      1. 若要還原繼承，請刪除已解鎖的元件；之後會重新獲得其鎖定狀態。

   1. **將元件拖曳到此處以包括在Analytics架構中**：可以從Sidekick將元件拖曳到這裡。
   1. 您可以找到目前包含在分析框架中的所有元件：

      1. 若要新增元件，請從sidekick的「元件」標籤中拖曳一個元件
      1. 若要刪除元件及其所有對應，請從元件的前後關聯功能表中選取「刪除」，然後在確認對話方塊上接受刪除。
      1. 請記住，元件只能從建立該元件的架構中刪除，且無法從傳統意義上的子架構中刪除（只能覆寫元件）。

### 分析檢視 {#analytics-view}

![aa-24](assets/aa-24.png)

1. 切換至架構上的&#x200B;**Analytics檢視**&#x200B;索引標籤，即可存取此檢視。
1. 左側：內容尋找器(cf#)由CQ變數填入，該變數會根據CQ檢視中拖曳至框架的元件而定。
1. Tab標頭(**AEM檢視**&#x200B;和&#x200B;**Analytics檢視**)：使用這些標頭在兩個檢視之間切換。

1. 三個表格（流量、轉換、事件）列出所有可用的Adobe Analytics變數。 屬於選取的RSID。 此處顯示的對應應與AEM檢視中的對應相同：

   * **流量**：

      * 流量變數( `prop1`)對應到CQ變數( `eventdata.downloadLink`)

      * 當元件旁邊有掛鎖時，這表示它繼承自父框架，因此無法編輯

   * **轉換**：

      * 轉換變數( `eVar1`)對應到CQ變數( `pagedata.title`)

      * 在CQ變數欄位上連按兩下，並手動輸入程式碼，轉換變數(`eVar3`)對應到內嵌新增的JavaScript運算式

   * **事件**：

      * 事件變數( `event1`)對應至CQ事件( `eventdata.events.pageView`)

>[!NOTE]
>
>您也可以連按兩下欄位並在其中新增文字，以內嵌填入任何表格的CQ變數欄。 這些欄位接受JavaScript作為輸入。
>
>例如，您可以在`prop3`旁邊新增：
>     `'`* `Adobe:'+pagedata.title+':'+pagedata.sitesection`\
>若要傳送與其&#x200B;*sitesection*&#x200B;串連之頁面的&#x200B;*title*，請使用&#x200B;*：* （冒號），並以&#x200B;*Adobe*&#x200B;做為`prop3`
>

>[!CAUTION]
>
>在任何指定時間，都只能將一個CQ變數對應至Adobe Analytics變數。
