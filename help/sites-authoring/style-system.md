---
title: 樣式系統
seo-title: Style System
description: 「樣式系統」允許模板作者在元件的內容策略中定義樣式類，以便內容作者能夠在頁面上編輯元件時選擇它們。 這些樣式可以是元件的視覺變體，使其更靈活。
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

「樣式系統」允許模板作者在元件的內容策略中定義樣式類，以便內容作者能夠在頁面上編輯元件時選擇它們。 這些樣式可以是元件的可替換視覺變體，使元件更加靈活。

這樣就無需為每個樣式開發自定義元件或自定義元件對話框以啟用此類樣式功能。 它導致了更多可重用的元件，這些元件可以快速而輕鬆地適應內容作者的需要，而AEM無需任何後端開發。

## 使用案例 {#use-case}

模板作者不僅需要配置元件如何為內容作者工作的能力，還需要配置元件的許多可替代的視覺變體。

同樣，內容作者不僅需要構造和排列其內容的能力，還需要選擇內容的視覺呈現方式。

Style System為模板作者和內容作者的要求提供了統一的解決方案：

* 模板作者可以在元件的內容策略中定義樣式類。
* 然後，內容作者可以在編輯頁面上的元件時從下拉清單中選擇這些類，以應用相應的樣式。

然後，將樣式類插入到元件的裝飾包裝元件上，以便元件開發人員不需要處理除提供其CSS規則之外的樣式。

## 概觀 {#overview}

使用「樣式系統」通常採用以下形式。

1. Web設計器會建立元件的不同可視變體。

1. 該HTML顯影劑具有要實施的元件的HTML輸出和期望的視覺變化。

1. HTML開發者定義與每個可視變體對應的CSS類，這些類將被插入到包裝元件的元素上。

1. HTML開發者為每個視覺變體實現相應的CSS代碼（和可選的JS代碼），以便它們看起來與定義的一樣。

1. 開AEM發人員將提供的CSS（和可選JS）放在 [客戶端庫](/help/sites-developing/clientlibs.md) 部署。

1. 開AEM發人員或模板作者配置頁面模板並編輯每個樣式元件的策略，添加已定義的CSS類，為每個樣式提供用戶友好的名稱，並指示可以組合哪些樣式。

1. 然AEM後，頁面作者可以通過元件工具欄的樣式菜單在頁面編輯器中選擇設計的樣式。

請注意，實際中只執行最後三個步AEM驟。 這意味著無需進行所有必要的CSS和Javascript開發AEM。

實際實施樣式僅需要在所需模AEM板的元件上部署和選擇。

下圖說明了「樣式系統」的體系結構。

![aem-style系統](assets/aem-style-system.png)

## 使用 {#use}

要演示該功能，我們將使用 [WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hant)核心元件的實施 [標題元件](https://www.adobe.com/go/aem_cmp_title_v2) 例如，

以下部分 [作為內容作者](#as-a-content-author) 和 [作為模板作者](#as-a-template-author) 介紹如何使用WKND的Style系統testStyle系統的功能。

如果希望將「樣式系統」用於您自己的元件，請執行以下操作：

1. 將CSS作為客戶端庫安裝，如一節中所述 [概述](#overview)。
1. 配置要使內容作者可用的CSS類，如一節中所述 [作為模板作者](#as-a-template-author)。
1. 然後，內容作者可以使用一節中所述的樣式 [作為內容作者](#as-a-content-author)。

### 作為內容作者 {#as-a-content-author}

1. 安裝WKND項目後，導航到WKND的英語母版頁， `http://<host>:<port>/sites.html/content/wknd/language-masters/en` 編輯頁面。
1. 選擇 **標題** 元件進一步向下

   ![作者的風格系統](assets/style-system-author.png)

1. 點擊或按一下 **樣式** 按鈕 **清單** 元件以開啟樣式菜單並更改元件的外觀。

   ![選擇樣式](assets/style-system-author2.png)

   >[!NOTE]
   >
   >在此示例中， **顏色** 樣式(**黑色**。 **白色**, **灰色**)互斥，而 **樣式** 選項&#x200B;**下划線**。 **右對齊**, **微間距**)。 這可在范 [本中設定為範本作者](#as-a-template-author)。

### 作為模板作者 {#as-a-template-author}

1. 在編輯WKND的英語母版頁時， `http://<host>:<port>/sites.html/content/wknd/language-masters/en`，通過 **頁面資訊 — >編輯模板**。

   ![編輯範本](assets/style-system-edit-template.png)

1. 編輯策略 **標題** 通過按一下或按一下 **策略** 按鈕

   ![編輯策略](assets/style-system-edit-policy.png)

1. 在屬性的「樣式」頁籤上，可以查看樣式的配置方式。

   ![編輯屬性](assets/style-system-properties.png)

   * **組名稱：** 樣式可以在樣式菜單中分組，內容作者在配置元件樣式時將看到該樣式菜單。
   * **樣式可以組合：** 允許同時選擇該組中的多個樣式。
   * **樣式名稱：** 配置元件樣式時將顯示給內容作者的樣式的說明。
   * **CSS類：** 與樣式關聯的CSS類的實際名稱。

   使用拖動手柄排列組的順序和組內的樣式。 使用添加或刪除表徵圖可添加或刪除組內的組或樣式。

>[!CAUTION]
>
>配置為元件策略的樣式屬性的CSS類（以及任何必需的Javascript）必須部署為 [客戶端庫](/help/sites-developing/clientlibs.md) 為了工作。

## 設定 {#setup}

核心元件版本2及更高版本已完全啟用，可以利用Style System，並且不需要其他配置。

只有在為您自己的自定義元件啟用「樣式系統」或 [啟用「編輯」對話框中的可選樣式頁籤。](#enable-styles-tab-edit)

### 在「設計」對話框中啟用「樣式」頁籤 {#enable-styles-tab-design}

為了使元件與「樣式系統AEM」一起使用並在其設計對話框中顯示樣式頁籤，元件開發人員必須在元件上包含具有以下設定的樣式頁籤：

* `path = "/mnt/overlay/cq/gui/components/authoring/dialog/style/tab_design/styletab"`
* `sling:resourceType = "granite/ui/components/coral/foundation/include"`

配置了元件後，頁面作者配置的樣式將自動插入裝飾元素AEM上，該裝飾元素將自動AEM環繞每個可編輯元件。 元件本身不需要做其他任何事情來實現這一點。

### 在「編輯」對話框中啟用「樣式」頁籤 {#enable-styles-tab-edit}

從6.5.3.0版開始AEM，「編輯」對話框中的可選「樣式」頁籤現在可用。 與「設計對話框」頁籤不同，「編輯」對話框中的頁籤對於「樣式系統」的功能並非必不可少，但對於內容作者來說，它是設定樣式的可選替代介面。

編輯對話框頁籤可以以與設計對話框頁籤類似的方式包括：

* `path = "/mnt/overlay/cq/gui/components/authoring/dialog/style/tab_edit/styletab"`
* `sling:resourceType = "granite/ui/components/coral/foundation/include"`

>[!NOTE]
>
>預設情況下，「編輯」對話框上的「樣式」頁籤未啟用。

### 帶元素名稱的樣式 {#styles-with-element-names}

開發人員還可以使用 `cq:styleElements` string array屬性。 然後，在設計對話框中策略的「樣式」頁籤中，模板作者還可以選擇要為每個樣式設定的元素名稱。 這將設定包裝元素的元素名稱。

此屬性在 `cq:Component` 的下界。 例如：

* `/apps/<yoursite>/components/content/list@cq:styleElements=[div,section,span]`

>[!CAUTION]
>
>避免為可組合的樣式定義元素名稱。 定義多個元素名稱時，優先順序順序為：
>
>1. HTL優先於一切： `data-sly-resource="${'path/to/resource' @ decorationTagName='span'}`
>1. 然後，在多個活動樣式中，將採用元件策略中配置的樣式清單中的第一個樣式。
>1. 最後，元件 `cq:htmlTag`/ `cq:tagName` 將被視為回退值。

>


此定義樣式名稱的功能對於非常通用的元件（如「佈局容器」或「內容片段」元件）非常有用，以便為它們提供附加含義。

例如，它允許給佈局容器提供語義，如 `<main>`。 `<aside>`。 `<nav>`的子菜單。
