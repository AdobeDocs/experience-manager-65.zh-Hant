---
title: 將元件資料與Adobe Analytics屬性對應
seo-title: 將元件資料與Adobe Analytics屬性對應
description: 了解如何使用SiteCatalyst屬性對應元件資料。
seo-description: 了解如何使用SiteCatalyst屬性對應元件資料。
uuid: b08ab37f-ad58-4c04-978f-8e21a3823ae8
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6c1f8869-62d9-4fac-aa0d-b99bb0e86d6b
docset: aem65
exl-id: c7c0c705-ec16-40f5-ad08-193f82d01263
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 0%

---

# 使用Adobe Analytics屬性映射元件資料{#mapping-component-data-with-adobe-analytics-properties}

將元件新增至架構，以收集要傳送至Adobe Analytics的資料。 設計用來收集分析資料的元件會將資料儲存在適當的&#x200B;**CQ變數**&#x200B;中。 將這類元件新增至架構時，架構會顯示CQ變數清單，以便您能分別前往適當的&#x200B;**Analytics變數**。

![aa-11](assets/aa-11.png)

開啟&#x200B;**AEM檢視**&#x200B;時，Analytics變數會出現在內容尋找器中。

![aa-12](assets/aa-12.png)

您可以使用相同的&#x200B;**CQ變數**&#x200B;對應多個Analytics變數。

![chlimage_1-68](assets/chlimage_1-68.png)

當頁面載入且符合下列條件時，會將對應的資料傳送至Adobe Analytics:

* 頁面與框架相關聯。
* 頁面使用新增至架構的元件。

請依照下列程式，將CQ元件變數與Adobe Analytics報表屬性對應。

1. 在&#x200B;**AEM檢視**&#x200B;中，將追蹤元件從sidekick拖曳至架構。 例如，從&#x200B;**General**&#x200B;類別中拖動&#x200B;**Page**&#x200B;元件元件。

   ![aa-13](assets/aa-13.png)

   有數個預設元件群組：**一般**、**商務**、**社區**、**Search&amp;Promote**&#x200B;和&#x200B;**其他**。 您的AEM例項可設定為顯示不同的群組和元件。

1. 若要將Adobe Analytics變數與元件中定義的變數對應，請從內容尋找器將&#x200B;**Analytics變數**&#x200B;拖曳至追蹤元件上的欄位。 例如，將`Page Name (pageName)`拖曳至`pagedata.title`。

   ![aa-14](assets/aa-14.png)

   >[!NOTE]
   >
   >為架構選取的報表套裝ID(RSID)會決定內容尋找器中顯示的Adobe Analytics變數。

1. 對其他元件和變數重複前兩個步驟。

   >[!NOTE]
   >
   >您可以對應多個Analytics變數(例如`props`、`eVars`、`events`)至相同的CQ變數(例如`pagedata.title`

   >[!CAUTION]
   >
   >強烈建議：
   >    
   >    * `eVars` 和 `props` 會對應至以或開頭的CQ變 `pagedata.X` 數  `eventdata.X`
      >    
      >    
   * 而事件應對應至以`eventdata.events.X`開頭的變數


1. 若要讓架構可在您網站的發佈執行個體上使用，請開啟sidekick的&#x200B;**Page**&#x200B;標籤，然後按一下&#x200B;**Activate Framework。**

## 映射產品相關變數{#mapping-product-related-variables}

AEM會使用慣例來命名原本要對應至Adobe Analytics產品相關屬性的產品相關變數和事件：

| CQ變數 | Analytics變數 | 說明 |
|---|---|---|
| `product.category` | `product.category` （轉換變數） | 產品類別。 |
| `product.sku` | `product.sku` （轉換變數） | 產品SKU。 |
| `product.quantity` | `product.quantity` （轉換變數） | 要購買的產品數量。 |
| `product.price` | `product.price` （轉換變數） | 產品價格。 |
| `product.events.<eventName>` | 與報表中的產品建立關聯的成功事件。 | `product.events` 是eventName事件的前置 *詞。* |
| `product.evars.<eVarName>` | 要與產品相關聯的轉換變數(`eVar`)。 | `product.evars` 是名為eVarName之eVar變數的 *前置詞。* |

數個AEM Commerce元件會使用這些變數名稱。

>[!NOTE]
>
>請勿將Adobe Analytics產品屬性對應至CQ變數。 如表所述，設定產品相關對應實際上等同於對應產品變數。

### 檢查Adobe Analytics的報表{#checking-reports-on-adobe-analytics}

1. 使用提供給AEM的相同憑證登入Adobe Analytics網站。
1. 請確定選取的RSID是前述步驟中使用的RSID。
1. 在&#x200B;**報表**（位於頁面左側）中，選取&#x200B;**自訂轉換**，然後選取&#x200B;**自訂轉換1-10**&#x200B;並選取與`eVar7`對應的變數

1. 根據您使用的Adobe Analytics版本，您平均需要等待45分鐘，報表才會更新為使用搜尋詞；例如茄子

## 搭配Adobe Analytics架構{#using-the-content-finder-cf-with-adobe-analytics-frameworks}使用內容尋找器(cf#)

起初，當您開啟Adobe Analytics架構時，內容尋找器會在下方包含預先定義的Analytics變數：

* 流量
* 轉換
* 事件

當選取RSID時，屬於該RSID的所有變數都會新增至清單。\
需要`cf#`，才能將Analytics變數對應至不同追蹤元件上顯示的CQ變數。 請參閱設定基本追蹤的架構。

根據為架構選取的檢視，內容尋找器將由Analytics變數(在AEM檢視中)或CQ變數（在Analytics檢視中）填入。

可透過下列方式操作清單：

1. 在&#x200B;**AEM檢視**&#x200B;中時，可依據使用3個篩選按鈕選取的變數類型來篩選清單：

   * 如果未選擇&#x200B;*按鈕*，則清單顯示完整清單。
   * 如果選取&#x200B;**流量**&#x200B;按鈕，清單只會顯示屬於「流量」區段的變數。
   * 如果選取了&#x200B;**轉換**&#x200B;按鈕，清單只會顯示屬於轉換區段的變數。
   * 如果選取了&#x200B;**Events**&#x200B;按鈕，清單只會顯示屬於「事件」區段的變數。

   >[!NOTE]
   >
   >一次只能有一個活動的篩選按鈕。

   >[!NOTE]
   >
   >Search&amp;Promote變數也屬於「轉換」區段。

   1. 清單也具有搜尋功能，可根據在搜尋欄位中輸入的文字來篩選元素。
   1. 如果在搜尋清單中的元素時啟用了篩選選項，則系統也會根據使用中按鈕來篩選顯示的結果。
   1. 您可以隨時使用旋轉箭頭按鈕重新載入清單。
   1. 若在架構上選取了多個RSID，則清單中的所有變數將會使用所選RSID內使用的所有標籤來顯示。


1. 在Adobe Analytics檢視中時，「內容尋找器」會顯示屬於拖曳至CQ檢視中的追蹤元件的所有CQ變數。

   * 例如，如果&#x200B;**下載元件**&#x200B;是CQ檢視中只拖曳一個&#x200B;*（有兩個可映射的變數* eventdata.downloadLink *和* eventdata.events.startDownload *），則切換至Adobe Analytics檢視時，「內容尋找器」看起來會像這樣：*

   ![aa-22](assets/aa-22.png)

   * 這些變數可拖放至屬於3個變數區段（**Traffic**、**Conversion**&#x200B;和&#x200B;**Events**）其中之一的任何Adobe Analytics變數上。

   * 在CQ檢視中將新追蹤元件拖曳至架構時，屬於元件的CQ變數會自動新增至Adobe Analytics檢視的「內容尋找器」(cf#)。
   >[!NOTE]
   >
   >一次只能將一個CQ變數對應至Adobe Analytics變數

## 使用AEM檢視和Analytics檢視{#using-aem-view-and-analytics-view}

在任何指定時間，使用者都可以選擇在架構頁面上時，在2種檢視Adobe Analytics對應的方式之間切換。 這2個檢視從2個不同的角度提供框架內對應的更佳概覽。

### AEM檢視{#aem-view}

![aa-23](assets/aa-23.png)

以上影像為例，**AEM檢視**&#x200B;具有下列屬性：

1. 這是框架開啟時的預設視圖。
1. 左側：內容尋找器(cf#)是根據所選RSID由Adobe Analytics變數填入。
1. 標籤標題(**AEM view**&#x200B;和&#x200B;**Analytics view**):使用這些來切換兩個檢視。

1. **AEM檢視**:

   1. 如果框架具有從其父級繼承的元件，則這些元件和映射到這些元件的變數將列在此處。

      1. 繼承的元件被鎖定。
      1. 要解鎖繼承的元件，只需按兩下元件名稱旁的掛鎖
      1. 要恢復繼承，必須刪除未鎖定的元件；之後，它將重新獲得其鎖定地位。
   1. **拖曳元件至此處，將其納入分析架構中**:可從Sidekick拖曳元件並放置在此處。
   1. 您可以找到分析架構中目前包含的所有元件：

      1. 若要新增元件，請從sidekick的「元件」標籤中拖曳一個元件
      1. 要刪除元件及其所有映射，請從元件的上下文菜單中選擇「刪除」，然後在確認對話框上接受刪除。
      1. 請記住，元件只能從其建立的架構中刪除，而無法從傳統意義上的子架構中刪除（只能覆蓋）。


### 分析檢視{#analytics-view}

![aa-24](assets/aa-24.png)

1. 此檢視可透過切換至架構上的&#x200B;**Analytics檢視**&#x200B;標籤來存取。
1. 左側：根據拖曳至CQ檢視中架構的元件，由CQ變數填入的內容尋找器(cf#)。
1. 標籤標題(**AEM view**&#x200B;和&#x200B;**Analytics view**):使用這些來切換兩個檢視。

1. 三個表格（流量、轉換、事件）列出所有可用的Adobe Analytics變數。 屬於選取的RSID。 此處顯示的對應應與AEM檢視中的對應相同：

   * **流量**:

      * 對應至CQ變數(`eventdata.downloadLink`)的流量變數(`prop1`)

      * 當元件旁邊有掛鎖時，這表示它繼承自父框架，因此無法編輯
   * **轉換**:

      * 對應至CQ變數(`pagedata.title`)的轉換變數(`eVar1`)

      * 對應至內嵌新增之Javascript運算式的轉換變數(`eVar3`)，方法是連按兩下CQ變數欄位並手動輸入程式碼
   * **事件**:

      * 已對應至CQ事件(`eventdata.events.pageView`)的事件變數(`event1`)



>[!NOTE]
>
>任何表格的CQ變數欄也可以內嵌填入，方法是連按兩下欄位並新增文字。 這些欄位接受javascript作為輸入。
>
>* 例如，在`prop3`旁邊，您可以新增
>* `'`* `Adobe:'+pagedata.title+':'+pagedata.sitesection`\
   >  使用&#x200B;*:*（冒號）並加上前置詞&#x200B;*Adobe*&#x200B;作為`prop3`，傳送與&#x200B;*網站區段*&#x200B;串連之頁面的&#x200B;*標題*

>



>[!CAUTION]
>
>任何指定時間都只能將一個CQ變數對應至Adobe Analytics變數。
