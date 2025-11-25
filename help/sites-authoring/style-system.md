---
title: 樣式系統
description: 樣式系統可讓範本作者在元件的內容原則中定義樣式類別，讓內容作者在編輯頁面上的元件時能夠選取這些類別。 這些樣式可作為元件的替代視覺變體，使其更靈活。
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: 1772368a-f5c9-440c-a92a-0f1d34cc4bf8
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 1%

---

# 樣式系統{#style-system}

樣式系統可讓範本作者在元件的內容原則中定義樣式類別，讓內容作者在編輯頁面上的元件時能夠選取這些類別。 這些樣式可作為元件的替代視覺變體，讓元件更靈活。

如此一來，您就不需要為每個樣式開發自訂元件，或是自訂元件對話方塊以啟用此類樣式功能。 這可導向更多可重複使用的元件，這些元件可以快速輕鬆地配合內容作者的需求，而無需任何AEM後端開發。

## 使用案例 {#use-case}

範本作者不僅需要為內容作者設定元件運作方式的能力，還需要設定元件的數個替代視覺變數。

同樣地，內容作者不僅需要建構和排列其內容的能力，還需要選取視覺呈現的方式。

樣式系統針對範本作者與內容作者的需求，提供統一的解決方案：

* 範本作者可以在元件的內容原則中定義樣式類別。
* 內容作者接著可以在編輯頁面上的元件時，從下拉式清單中選取這些類別，以套用對應的樣式。

接著，樣式類別會插入到元件的裝飾包裝函式元素上，如此一來，元件開發人員就不需要在提供其CSS規則之後，再處理樣式了。

## 概觀 {#overview}

通常，使用「樣式系統」會採用下列形式。

1. 網頁設計工具會建立元件的不同視覺變數。

1. HTML開發人員會獲得元件的HTML輸出，以及要實施的所需視覺變數。

1. HTML開發人員會定義與每個視覺變數相對應的CSS類別，並會插入到元件包裝的元素上。

1. HTML開發人員會針對每個視覺變數實作對應的CSS程式碼（以及選用的JS程式碼），使其外觀與定義一致。

1. AEM開發人員將提供的CSS （和選用的JS）放置在[使用者端資料庫](/help/sites-developing/clientlibs.md)中並進行部署。

1. AEM開發人員或範本作者會設定頁面範本，並編輯每個已設定樣式元件的原則，新增定義的CSS類別、為每種樣式提供好記的名稱，並指出可組合的樣式。

1. 接著，AEM頁面作者就能透過元件工具列的樣式選單，在頁面編輯器中選擇設計的樣式。

請注意，AEM中實際只執行最後三個步驟。 這表示所有必要的CSS和JavaScript開發都可以不使用AEM完成。

若要實際實作樣式，只需要在AEM上部署，並在所需範本的元件中選取。

下圖說明「樣式系統」的架構。

![aem-style-system](assets/aem-style-system.png)

## 使用 {#use}

為了示範此功能，我們將使用核心元件的[標題元件](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hant)的[WKND](https://www.adobe.com/go/aem_cmp_title_v2_tw)實作作為範例。

下列章節[As a Content Author](#as-a-content-author)及[As a Template Author](#as-a-template-author)說明如何使用WKND的樣式系統測試樣式系統的功能。

如果您希望對自己的元件使用「樣式系統」，請執行下列動作：

1. 將CSS安裝為使用者端程式庫，如[概觀](#overview)一節中所述。
1. 依照[As a Template Author](#as-a-template-author)一節中的說明，設定您想要可供內容作者使用的CSS類別。
1. 然後，內容作者就可以使用如[As a Content Author](#as-a-content-author)一節中所述的樣式。

### 作為內容作者 {#as-a-content-author}

1. 安裝WKND專案後，導覽至WKND的英文主版首頁`http://<host>:<port>/sites.html/content/wknd/language-masters/en`並編輯該頁面。
1. 選取頁面下方的&#x200B;**Title**&#x200B;元件

   作者的![樣式系統](assets/style-system-author.png)

1. 按一下&#x200B;**清單**&#x200B;元件工具列上的&#x200B;**樣式**&#x200B;按鈕，開啟樣式功能表並變更元件的外觀。

   ![選取樣式](assets/style-system-author2.png)

   >[!NOTE]
   >
   >在此範例中，**色彩**&#x200B;樣式（**黑色**、**白色**&#x200B;和&#x200B;**灰色**）是互斥的，而&#x200B;**樣式**&#x200B;選項（**底線**、**靠右對齊**&#x200B;和&#x200B;**最小間距**）可以合併。 這可在范 [本中設定為範本作者](#as-a-template-author)。

### 作為範本作者 {#as-a-template-author}

1. 在`http://<host>:<port>/sites.html/content/wknd/language-masters/en`編輯WKND的英文主版首頁時，請透過&#x200B;**頁面資訊>編輯範本**&#x200B;編輯頁面的範本。

   ![編輯範本](assets/style-system-edit-template.png)

1. 點選或按一下元件的&#x200B;**原則**&#x200B;按鈕，編輯&#x200B;**Title**&#x200B;元件的原則。

   ![編輯原則](assets/style-system-edit-policy.png)

1. 在屬性的「樣式」標籤上，您可以看到樣式的設定方式。

   ![編輯屬性](assets/style-system-properties.png)

   * **群組名稱：**&#x200B;樣式可在樣式選單中組成群組，內容作者在設定元件樣式時會看到該樣式選單。
   * **可組合樣式：**&#x200B;允許同時選取該群組中的多個樣式。
   * **樣式名稱：**&#x200B;設定元件樣式時，內容作者會看到的樣式說明。
   * **CSS類別：**&#x200B;與樣式關聯的CSS類別的實際名稱。

   使用拖曳操作框來排列群組的順序以及群組內的樣式。 使用新增或刪除圖示來新增或移除群組內的群組或樣式。

>[!CAUTION]
>
>設定為元件原則的樣式屬性的CSS類別(以及任何必要的JavaScript)必須部署為[使用者端資料庫](/help/sites-developing/clientlibs.md)才能運作。

## 設定 {#setup}

核心元件2版和更新版本已完全啟用，以運用樣式系統，無需額外設定。

若要為您自己的自訂元件啟用樣式系統，或[在「編輯」對話方塊中啟用選用的「樣式」索引標籤，則只需執行下列步驟。](#enable-styles-tab-edit)

### 在設計對話方塊中啟用樣式標籤 {#enable-styles-tab-design}

為了使元件可與AEM的樣式系統搭配使用並在其設計對話方塊中顯示樣式標籤，元件開發人員必須包含樣式標籤，且元件上須有下列設定：

* `path = "/mnt/overlay/cq/gui/components/authoring/dialog/style/tab_design/styletab"`
* `sling:resourceType = "granite/ui/components/coral/foundation/include"`

在設定元件後，AEM會自動將頁面作者設定的樣式插入裝飾元素上，讓AEM自動包裝在每個可編輯元件周圍。 元件本身不需要執行任何其他動作，就能讓此動作發生。

### 在編輯對話方塊中啟用樣式索引標籤 {#enable-styles-tab-edit}

自AEM版本6.5.3.0起，「編輯」對話方塊中的選用「樣式」索引標籤現已可用。 與「設計」對話方塊索引標籤不同，「編輯」對話方塊中的索引標籤對於樣式系統的運作並非必要，但它是內容作者設定樣式的選用替代介面。

編輯對話方塊索引標籤可以類似設計對話方塊索引標籤的方式加入：

* `path = "/mnt/overlay/cq/gui/components/authoring/dialog/style/tab_edit/styletab"`
* `sling:resourceType = "granite/ui/components/coral/foundation/include"`

>[!NOTE]
>
>依預設，「編輯」對話方塊上的「樣式」索引標籤不會啟用。

### 具有元素名稱的樣式 {#styles-with-element-names}

開發人員也可以使用`cq:styleElements`字串陣列屬性，為元件上的樣式設定允許的元素名稱清單。 然後在設計對話方塊中原則的「樣式」索引標籤中，範本作者也可以選擇要為每個樣式設定的元素名稱。 這會設定包裝函式元素的元素名稱。

此屬性設定在`cq:Component`節點上。 例如：

* `/apps/<yoursite>/components/content/list@cq:styleElements=[div,section,span]`

>[!CAUTION]
>
>避免為可組合的樣式定義元素名稱。 定義多個元素名稱時，優先順序為：
>
>1. HTL優先於所有專案： `data-sly-resource="${'path/to/resource' @ decorationTagName='span'}`
>1. 然後，在多個作用中樣式中，會採用元件原則中設定的樣式清單中的第一個樣式。
>1. 最後，元件的`cq:htmlTag`/ `cq:tagName`將被視為遞補值。
>

這種定義樣式名稱的功能對於非常一般的元件（例如佈局容器或內容片段元件）非常有用，可為其提供額外的含義。

例如，它允許配置容器具有如`<main>`、`<aside>`、`<nav>`等語意。
