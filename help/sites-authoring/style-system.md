---
title: 樣式系統
seo-title: 樣式系統
description: 樣式系統允許模板作者在元件的內容策略中定義樣式類，以便內容作者在編輯頁面上的元件時能夠選擇它們。 這些樣式可以替代元件的視覺變化，讓元件更具彈性。
seo-description: 樣式系統允許模板作者在元件的內容策略中定義樣式類，以便內容作者在編輯頁面上的元件時能夠選擇它們。 這些樣式可以替代元件的視覺變化，讓元件更具彈性。
uuid: 0d857650-8738-49e6-b431-f69c088be74f
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: e3ccddb6-be5e-4e5f-a017-0eed263555ce
translation-type: tm+mt
source-git-commit: 0985ba24f7430381fccc40faf3a316d3abd85a30
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 1%

---


# 樣式系統{#style-system}

樣式系統允許模板作者在元件的內容策略中定義樣式類，以便內容作者在編輯頁面上的元件時能夠選擇它們。 這些樣式可以替代元件的視覺變化，讓元件更具彈性。

這樣就不需要為每個樣式開發自定義元件，或自定義元件對話框以啟用這種樣式功能。 它可提供更多可重複使用的元件，可快速輕鬆地配合內容作者的需求，毋需進行任何AEM後端開發。

## 使用案例{#use-case}

範本作者不僅需要設定元件如何為內容作者運作的能力，還需要設定元件的多種替代視覺變化。

同樣地，內容作者不僅需要建構和排列內容的能力，還需要選擇內容的視覺呈現方式。

Style System針對範本作者和內容作者的需求提供統一的解決方案：

* 範本作者可在元件的內容原則中定義樣式類別。
* 然後，內容作者可以在編輯頁面上的元件時，從下拉式清單中選取這些類別，以套用對應的樣式。

然後，樣式類會插入元件的裝飾包裝元件上，讓元件開發人員不需要處理樣式，而不需要提供其CSS規則。

## 概覽 {#overview}

使用「樣式系統」通常採用下列形式。

1. 網頁設計人員會建立不同的元件視覺變化。

1. HTML開發人員會提供元件的HTML輸出以及所要實作的視覺變化。

1. HTML開發人員會定義對應於每個視覺變化且要插入在元素上、包住元件的CSS類別。

1. HTML開發人員會針對每個視覺變化建置對應的CSS程式碼（和選擇性的JS程式碼），讓它們看起來都如定義。

1. AEM開發人員將提供的CSS（和選用的JS）放入[用戶端程式庫](/help/sites-developing/clientlibs.md)中，並加以部署。

1. AEM開發人員或範本作者會設定頁面範本並編輯每個樣式元件的原則、新增已定義的CSS類別、為每個樣式指定好用的名稱，以及指出哪些樣式可以合併。

1. 然後，AEM頁面作者就可以透過元件工具列的樣式選單，在頁面編輯器中選擇設計的樣式。

請注意，AEM實際上只會執行最後三個步驟。 這表示不需AEM，就可完成所有必要的CSS和Javascript開發。

實際實作樣式只需要在AEM上部署，並在所需範本的元件中選取。

下圖說明了樣式系統的體系結構。

![aem-style-system](assets/aem-style-system.png)

## 使用{#use}

為展示此功能，我們將以[WKND](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)實作核心元件的[title元件](https://www.adobe.com/go/aem_cmp_title_v2)為例。

以下章節[作為內容作者](#as-a-content-author)和[作為範本作者](#as-a-template-author)說明如何使用WKND的樣式系統來測試樣式系統的功能。

如果要將樣式系統用於自己的元件，請執行以下操作：

1. 如[概述](#overview)一節所述，將CSS安裝為用戶端程式庫。
1. 如[ As a Template Author](#as-a-template-author)一節所述，設定您要讓內容作者使用的CSS類別。
1. 然後，內容作者可使用[一節中所述的樣式，作為內容作者](#as-a-content-author)。

### 身為內容作者{#as-a-content-author}

1. 安裝WKND專案後，導覽至WKND的英文主版首頁`http://<host>:<port>/sites.html/content/wknd/language-masters/en`並編輯該頁面。
1. 在頁面下方選擇&#x200B;**Title**&#x200B;元件

   ![作者的樣式系統](assets/style-system-author.png)

1. 點選或按一下&#x200B;**List**&#x200B;元件工具列上的&#x200B;**Styles**&#x200B;按鈕，以開啟樣式選單並變更元件的外觀。

   ![選取樣式](assets/style-system-author2.png)

   >[!NOTE]
   >
   >在本例中，**Colors**&#x200B;樣式（**Black**、**White**&#x200B;和&#x200B;**Gray**）是互斥的，而&#x200B;**Style**&#x200B;選項（**Underline**,a12/>右對齊&#x200B;**和**&#x200B;微小間距&#x200B;**）可結合。**&#x200B;這可在范 [本中設定為範本作者](#as-a-template-author)。

### 作為模板作者{#as-a-template-author}

1. 在`http://<host>:<port>/sites.html/content/wknd/language-masters/en`編輯WKND的英文主版頁面時，請透過&#x200B;**頁面資訊->編輯範本**&#x200B;編輯頁面範本。

   ![編輯範本](assets/style-system-edit-template.png)

1. 點選或按一下元件的&#x200B;**Policy**&#x200B;按鈕，編輯&#x200B;**Title**&#x200B;元件的策略。

   ![編輯原則](assets/style-system-edit-policy.png)

1. 在屬性的「樣式」索引標籤上，您可以看到樣式的設定方式。

   ![編輯屬性](assets/style-system-properties.png)

   * **群組名稱：** 在內容作者在設定元件樣式時會看到的樣式選單中，可將樣式分組。
   * **可組合樣式：** 允許同時選取該群組中的多種樣式。
   * **樣式名稱：** 設定元件樣式時，將顯示給內容作者的樣式說明。
   * **CSS類：** 與樣式關聯的CSS類的實際名稱。

   使用拖動控制滑塊來排列組的順序和組內的樣式。 使用新增或刪除圖示來新增或移除群組或群組中的樣式。

>[!CAUTION]
>
>為了工作，必須將配置為元件策略樣式屬性的CSS類（以及任何必要的Javascript）部署為[客戶端庫](/help/sites-developing/clientlibs.md)。

## 設定 {#setup}

核心元件版本2及更新版本已完全啟用，以利用樣式系統，而且不需額外設定。

只需執行下列步驟，即可為您自己的自訂元件啟用樣式系統，或在「編輯」對話方塊中啟用選用的「樣式」標籤。](#enable-styles-tab-edit)[

### 在設計對話框{#enable-styles-tab-design}中啟用樣式頁籤

若要讓元件搭配AEM的「樣式系統」運作，並在其設計對話方塊中顯示樣式標籤，元件開發人員必須在元件上加入具有下列設定的樣式標籤：

* `path = "/mnt/overlay/cq/gui/components/authoring/dialog/style/tab_design/styletab"`
* `sling:resourceType = "granite/ui/components/coral/foundation/include"`

在設定元件後，頁面作者所設定的樣式將會由AEM自動插入裝飾元素上，AEM會自動環繞每個可編輯的元件。 元件本身不需要做其他任何動作，就能達成此目標。

### 在編輯對話框{#enable-styles-tab-edit}中啟用樣式頁籤

自AEM 6.5.3.0版起，「編輯對話方塊」(Edit Dialog)中的「樣式」(Styles)頁籤現已可供使用。 與「設計對話框」頁籤不同，「編輯對話框」中的頁籤對於「樣式系統」的運作並不重要，但對於內容作者來說，它是設定樣式的可選替代介面。

編輯對話框頁籤可以以與設計對話框頁籤類似的方式包括：

* `path = "/mnt/overlay/cq/gui/components/authoring/dialog/style/tab_edit/styletab"`
* `sling:resourceType = "granite/ui/components/coral/foundation/include"`

>[!NOTE]
>
>「編輯」(Edit)對話框上的「樣式」(Styles)頁籤預設不啟用。

### 元素名稱{#styles-with-element-names}的樣式

開發人員也可以使用`cq:styleElements`字串陣列屬性，設定元件上樣式的允許元素名稱清單。 然後，在設計對話方塊中原則的「樣式」索引標籤中，範本作者也可以選擇要針對每個樣式設定的元素名稱。 這將設定包裝器元素的元素名稱。

此屬性在`cq:Component`節點上設定。 例如：

* `/apps/<yoursite>/components/content/list@cq:styleElements=[div,section,span]`

>[!CAUTION]
>
>避免為可組合的樣式定義元素名稱。 定義多個元素名稱時，優先順序為：
>
>1. HTL優先於一切：`data-sly-resource="${'path/to/resource' @ decorationTagName='span'}`
>1. 然後，在多個作用中樣式中，會選取元件原則中設定之樣式清單中的第一個樣式。
>1. 最後，元件的`cq:htmlTag`/ `cq:tagName`將視為備援值。

>



此定義樣式名稱的功能對於非常一般的元件（例如「版面容器」或「內容片段」元件）非常有用，以提供其他意義。

例如，它可讓配置容器具有`<main>`、`<aside>`、`<nav>`等語義。
