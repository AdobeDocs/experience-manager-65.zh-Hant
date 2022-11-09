---
title: 樣式系統
seo-title: Style System
description: 樣式系統允許模板作者在元件的內容策略中定義樣式類，以便內容作者能夠在編輯頁面上的元件時選擇它們。 這些樣式可作為元件的替代視覺變化，使其更具彈性。
seo-description: The Style System allows a template author to define style classes in the content policy of a component so that a content author is able to select them when editing the component on a page. These styles can be alternative visual variations of a component, making it more flexible.
uuid: 0d857650-8738-49e6-b431-f69c088be74f
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: e3ccddb6-be5e-4e5f-a017-0eed263555ce
exl-id: 1772368a-f5c9-440c-a92a-0f1d34cc4bf8
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1312'
ht-degree: 2%

---

# 樣式系統{#style-system}

樣式系統允許模板作者在元件的內容策略中定義樣式類，以便內容作者能夠在編輯頁面上的元件時選擇它們。 這些樣式可作為元件的替代視覺變化，讓元件更具彈性。

這樣就不需要為每個樣式開發自定義元件，或自定義元件對話框以啟用此類樣式功能。 它可產生更多可重複使用的元件，無需任何AEM後端開發，即可快速輕鬆地適應內容作者的需求。

## 使用案例 {#use-case}

範本作者不僅需要設定元件如何為內容作者運作的功能，還需要設定元件的多個替代視覺變數。

同樣地，內容作者不僅需要結構化及排列其內容的能力，還需要選取內容的視覺呈現方式。

樣式系統提供統一的解決方案，可滿足範本作者和內容作者的需求：

* 範本作者可在元件的內容原則中定義樣式類別。
* 然後，內容作者在編輯頁面上的元件時，可從下拉式清單中選取這些類別，以套用對應的樣式。

樣式類隨後插入到元件的裝飾包裝元素上，因此元件開發人員不需要處理樣式（不提供其CSS規則）。

## 總覽 {#overview}

使用樣式系統通常採用以下形式。

1. 網頁設計器會建立元件的不同視覺變化。

1. HTML顯影器被提供元件的HTML輸出和要實施的所需的視覺變化。

1. HTML開發人員定義與每個視覺變化對應並要插入到包裝元件的元素上的CSS類。

1. HTML開發人員會針對每個視覺變異實施對應的CSS程式碼（以及選用的JS程式碼），使其看起來如定義。

1. AEM開發人員將提供的CSS（和選用JS）放在 [用戶端程式庫](/help/sites-developing/clientlibs.md) 並進行部署。

1. AEM開發人員或範本作者會設定頁面範本並編輯每個已設定樣式元件的原則、新增定義的CSS類別、為每個樣式提供好記的名稱，並指出可結合哪些樣式。

1. 然後，AEM頁面作者可以透過元件工具列的樣式選單，在頁面編輯器中選擇設計樣式。

請注意，系統只會在AEM中實際執行最後三個步驟。 這表示所有必要CSS和Javascript的所有開發都可以在沒有AEM的情況下完成。

實際實作樣式只需在AEM上部署，並在所需範本的元件中選取即可。

下圖說明樣式系統的架構。

![aem-style-system](assets/aem-style-system.png)

## 使用 {#use}

為了演示此功能，我們將使用 [WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hant)核心元件的實作 [標題元件](https://www.adobe.com/go/aem_cmp_title_v2) 作為範例。

以下幾節 [作為內容作者](#as-a-content-author) 和 [作為範本作者](#as-a-template-author) 介紹如何使用WKND的樣式系統測試樣式系統的功能。

如果要將樣式系統用於您自己的元件，請執行以下操作：

1. 將CSS安裝為用戶端程式庫，如一節所述 [概述](#overview).
1. 設定您要讓內容作者使用的CSS類別，如一節所述 [作為範本作者](#as-a-template-author).
1. 然後，內容作者就可以使用區段中所述的樣式 [作為內容作者](#as-a-content-author).

### 作為內容作者 {#as-a-content-author}

1. 安裝WKND專案後，請導覽至WKND的英文主版首頁() `http://<host>:<port>/sites.html/content/wknd/language-masters/en` 和編輯頁面。
1. 選取 **標題** 元件繼續向下

   ![作者的樣式系統](assets/style-system-author.png)

1. 點選或按一下 **樣式** 按鈕 **清單** 元件，以開啟樣式菜單並更改元件的外觀。

   ![選取樣式](assets/style-system-author2.png)

   >[!NOTE]
   >
   >在此範例中， **顏色** 樣式(**黑色**, **白色**，和 **灰色**)互斥，而 **樣式** 選項(**畫底線**, **靠右對齊**，和 **迷你間距**)即可結合。 這可在范 [本中設定為範本作者](#as-a-template-author)。

### 作為範本作者 {#as-a-template-author}

1. 編輯WKND的英語首頁時，請訪問 `http://<host>:<port>/sites.html/content/wknd/language-masters/en`，請透過 **頁面資訊 — >編輯模板**.

   ![編輯範本](assets/style-system-edit-template.png)

1. 編輯 **標題** 元件，點選或按一下 **原則** 按鈕。

   ![編輯原則](assets/style-system-edit-policy.png)

1. 在屬性的樣式標籤上，您可以查看樣式的設定方式。

   ![編輯屬性](assets/style-system-properties.png)

   * **組名稱：** 在內容作者在設定元件樣式時會看到的樣式選單中，可將樣式分組。
   * **樣式可結合：** 允許同時選取該群組中的多種樣式。
   * **樣式名稱：** 設定元件樣式時，內容作者會看到的樣式說明。
   * **CSS類：** 與樣式關聯的CSS類的實際名稱。

   使用拖動控點來排列組的順序和組內的樣式。 使用「添加」或「刪除」表徵圖可添加或刪除組內的組或樣式。

>[!CAUTION]
>
>配置為元件策略樣式屬性的CSS類（以及任何必要的Javascript）必須部署為 [用戶端程式庫](/help/sites-developing/clientlibs.md) 才能工作。

## 設定 {#setup}

核心元件2版和更新版本已完全啟用，以利用樣式系統，且不需要額外設定。

只有在為自己的自定義元件或 [在「編輯」對話方塊中，啟用可選樣式標籤。](#enable-styles-tab-edit)

### 在「設計」對話框中啟用樣式頁簽 {#enable-styles-tab-design}

為了使元件與AEM樣式系統一起使用並在其設計對話框中顯示樣式頁簽，元件開發人員必須在元件上包含具有以下設定的樣式頁簽：

* `path = "/mnt/overlay/cq/gui/components/authoring/dialog/style/tab_design/styletab"`
* `sling:resourceType = "granite/ui/components/coral/foundation/include"`

設定元件後，頁面作者所設定的樣式會由AEM自動插入裝飾元素上，AEM會自動包住每個可編輯的元件。 元件本身不需要做其他任何動作，即可實現此目標。

### 在編輯對話框中啟用樣式頁簽 {#enable-styles-tab-edit}

自AEM 6.5.3.0版起，「編輯」對話方塊中的選用樣式標籤現已可用。 與「設計對話框」頁簽不同，「編輯」對話框中的頁簽對於樣式系統的功能不是必不可少的，但是是內容作者設定樣式的可選替代介面。

編輯對話框頁簽可以與設計對話框頁簽類似的方式包含：

* `path = "/mnt/overlay/cq/gui/components/authoring/dialog/style/tab_edit/styletab"`
* `sling:resourceType = "granite/ui/components/coral/foundation/include"`

>[!NOTE]
>
>預設情況下，不會啟用「編輯」對話框上的樣式頁簽。

### 含有元素名稱的樣式 {#styles-with-element-names}

開發人員也可以使用 `cq:styleElements` 字串陣列屬性。 然後，在設計對話方塊內原則的樣式標籤中，範本作者也可以選擇要針對每個樣式設定的元素名稱。 這會設定包裝元素的元素名稱。

此屬性設定於 `cq:Component` 節點。 例如：

* `/apps/<yoursite>/components/content/list@cq:styleElements=[div,section,span]`

>[!CAUTION]
>
>請避免為可結合的樣式定義元素名稱。 定義多個元素名稱時，優先順序的順序為：
>
>1. HTL優先於所有項目： `data-sly-resource="${'path/to/resource' @ decorationTagName='span'}`
>1. 然後，在多個活動樣式中，會採用元件策略中配置的樣式清單中的第一個樣式。
>1. 最後，元件 `cq:htmlTag`/ `cq:tagName` 會視為後援值。

>


定義樣式名稱的功能對於非常通用的元件（如「版面容器」或「內容片段」元件）非常有用，以便提供其他含義。

例如，它允許「佈局容器」被賦予語義，如 `<main>`, `<aside>`, `<nav>`、等
