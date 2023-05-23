---
title: SPA 藍圖
seo-title: SPA Blueprint
description: 本文檔描述了任何框架都應履行的一SPA般、與框架無關的合同，以在中實施可編SPA輯的組AEM件。
seo-description: This document describes the general, framework-independent contract that any SPA framework should fulfill in order to implement editable SPA components within AEM.
uuid: 48f2d415-ec34-49dc-a8e1-6feb5a8a5bbe
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 04ac8203-320b-4671-aaad-6e1397b12b6f
docset: aem65
exl-id: 383f84fd-455c-49a4-9e2b-1c4757cc188b
source-git-commit: afd2afe182d65e64c0ad851b86021886078a9dd5
workflow-type: tm+mt
source-wordcount: '2079'
ht-degree: 1%

---

# SPA 藍圖{#spa-blueprint}

要使作者能夠AEM使SPA用編輯器編輯SPA內容，必SPA須滿足以下要求：

>[!NOTE]
>
>編輯SPA器是需要基於框架的SPA客戶端呈現(例如，反應或Angular)的項目的推薦解決方案。

## 簡介 {#introduction}

本文檔介紹任何框架SPA為在中實施可編輯元件而應履行的AEM一般合同(即支援層SPA的類AEM型)。

>[!NOTE]
>
>以下要求獨立於框架。 如果滿足這些要求，則可以提供由模組、元件和服務組成的框架特定層。
>
>**這些要求已滿足中的「反應和Angular」框AEM架。** 只有在您希望實施另一個框架以便與一起使用時，此藍圖中的要求才AEM相關。

>[!CAUTION]
>
>儘管SPA其功能AEM與框架無關，但目前只支援React和Angular框架。

要使作者能夠使用頁面編輯AEM器來編輯由單頁應用程式框架公開的資料，項目必須能夠解釋表示儲存在儲存庫中的應用程式所儲存資料的語義的模型AEM結構。 為了實現這一目標，提供了兩個框架無關庫：這樣 `PageModelManager` 和 `ComponentMapping`。

### PageModelManager {#pagemodelmanager}

的 `PageModelManager` 庫作為NPM包提供，供項目使SPA用。 它隨附SPA並充當資料模型管理器。

它代表SPAJSON結構抽象出代表實際內容結構的JSON結構的檢索和管理。 它還負責與同步，以SPA在必須重新呈現其元件時通知它。

請參閱NPM包 [@adobe/aem-spa-page-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager)

初始化 `PageModelManager`，庫首先載入提供的應用程式根模型（通過參數、元屬性或當前URL）。 如果庫標識當前頁面的模型不是它讀取的根模型的一部分，並將其作為子頁面的模型包含。

![page_model_consolidation](assets/page_model_consolidation.png)

### 元件映射 {#componentmapping}

的 `ComponentMapping` 模組作為NPM包提供到前端項目。 它儲存前端元件，並為將前SPA端元件映射到資源類AEM型提供方法。 這樣，在分析應用程式的JSON模型時，就可以動態解析元件。

模型中存在的每個項都包含 `:type` 顯示資源類AEM型的欄位。 裝載後，前端元件可以使用它從基礎庫接收到的模型片段來呈現自己。

#### 動態模型到元件對應 {#dynamic-model-to-component-mapping}

有關動態模型到元件映射如何在Javascript SDK中發生的詳細資訊，SPA請參AEM閱文章 [動態模型到元件的映SPA射](/help/sites-developing/spa-dynamic-model-to-component-mapping.md)。

### 框架特定層 {#framework-specific-layer}

每個前端框架必須實現第三層。 第三個庫負責與底層庫交互，並提供一系列整合良好且易於使用的入口點，以便與資料模型交互。

本文檔的其餘部分描述了此中間框架特定層的要求，並希望與框架無關。 通過遵守以下要求，可以為項目元件提供框架特定層，以便與負責管理資料模型的底層庫交互。

## 一般概念 {#general-concepts}

### 頁面模型 {#page-model}

頁面的內容結構儲存在AEM中。 頁面模型用於映射和實例化組SPA件。 開SPA發人員創SPA建映射到元件AEM的元件。 為此，他們使用資源類型（或元件路徑）AEM作為唯一鍵。

組SPA件必須與頁面模型同步，並相應更新其內容的任何更改。 必須使用利用動態元件的模式來在提供的頁面模型結構後即時實例化元件。

### 元欄位 {#meta-fields}

頁面模型利用JSON模型導出器，它本身基於 [吊具模型](https://sling.apache.org/documentation/bundles/models.html) API。 可導出的sling模型公開以下欄位清單，以便使底層庫能夠解釋資料模型：

* `:type`:資源的類AEM型（預設=資源類型）
* `:children`:當前資源的層次子級。 子項不是當前資源內部內容的一部分（可以在代表頁面的項上找到）
* `:hierarchyType`:資源的分層類型。 的 `PageModelManager` 當前支援頁類型

* `:items`:當前資源的子內容資源（嵌套結構，僅存在於容器中）
* `:itemsOrder`:已排序子項清單。 JSON映射對象不保證其欄位的順序。 通過同時擁有映射和當前陣列，API的使用者可以同時獲得這兩種結構的優點
* `:path`:項的內容路徑（在表示頁面的項上存在）

另請參閱 [Content Services入門AEM。](https://helpx.adobe.com/experience-manager/kt/sites/using/content-services-tutorial-use.html)

### 框架特定模組 {#framework-specific-module}

分離關注點有助於促進項目實施。 因此，應提供npm特定的包。 此軟體包負責聚合和公開基本模組、服務和元件。 這些元件必須封裝資料模型管理邏輯並提供對項目元件期望的資料的訪問。 該模組還負責傳遞性地暴露底層庫的有用入口點。

為方便庫的互操作性，Adobe建議特定於框架的模組捆綁以下庫。 如果需要，該層可以在將底層API暴露到項目之前封裝並調整它們。

* [@adobe/aem-spa-page-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager)
* [@adobe/aem-spa元件映射](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

#### 實施 {#implementations}

#### 反應 {#react}

npm模組： [@adobe/aem react-editable-components](https://www.npmjs.com/package/@adobe/aem-react-editable-components)

#### Angular {#angular}

npm模組： [@adobe/aemangular可編輯的元件](https://www.npmjs.com/package/@adobe/aem-angular-editable-components)

## 主要服務和元件 {#main-services-and-components}

應根據每個框架的具體准則執行下列實體。 基於框架架構，實現方式可能有很大差異，但必須提供描述的功能。

### 模型提供程式 {#the-model-provider}

項目元件必須將對模型片段的訪問權限委託給模型提供程式。 然後，模型提供程式負責偵聽對模型指定片段所做的更改，並將更新的模型返回委託元件。

為此，模型提供程式必須註冊到 ` [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)`。 然後，當發生改變時，它接收並將更新的資料傳遞到委託元件。 按照慣例，為將承載模型片段的委託元件提供的屬性命名為 `cqModel`。 實施可免費向元件提供此屬性，但應考慮與框架體系結構的整合、可發現性和易用性等方面。

### 元件HTML裝飾器 {#the-component-html-decorator}

元件解碼器負責裝飾每個元件實例的元素的外部HTML，其中包含頁面編輯器預期的一系列資料屬性和類名。

#### 元件聲明 {#component-declaration}

以下元資料必須添加到項目元件生成的外部HTML元素中。 它們使頁面編輯器能夠檢索相應的編輯配置。

* `data-cq-data-path`:相對於 `jcr:content`

#### 編輯權能聲明和佔位符 {#editing-capability-declaration-and-placeholder}

以下元資料和類名必須添加到項目元件生成的外部HTML元素中。 它們使頁面編輯器能夠提供相關功能。

* `cq-placeholder`:標識空元件佔位符的類名
* `data-emptytext`:元件實例為空時由覆蓋顯示的標籤

**空元件佔位符**

每個元件都必須擴展一個功能，當元件被標識為空時，該功能將用特定於佔位符和相關重疊的資料屬性和類名來裝飾外部HTML元素。

**論構件的空性**

* 元件在邏輯上是否為空？
* 當元件為空時，覆蓋所顯示的標籤應是什麼？

### 容器 {#container}

容器是用於包含和呈現子元件的元件。 為此，容器在 `:itemsOrder`。 `:items` 和 `:children` 模型的屬性。

容器從儲存器動態獲取子元件 [`ComponentMapping`](/help/sites-developing/spa-blueprint.md#componentmapping) 的下界。 然後，容器使用「模型提供程式」功能擴展子元件，並最終實例化它。

### Page {#page}

的 `Page` 元件擴展 `Container` 元件。 容器是用於包含和呈現子元件（包括子頁）的元件。 為此，容器在 `:itemsOrder`。 `:items`, `:children` 模型的屬性。 的 `Page` 元件動態從儲存中獲取子元件 [元件映射](/help/sites-developing/spa-blueprint.md#componentmapping) 的下界。 的 `Page` 負責實例化子元件。

### 回應式格線 {#responsive-grid}

響應網格元件是容器。 它包含表示其列的模型提供程式的特定變型。 響應網格及其列負責用模型中包含的特定類名裝飾項目元件的外部HTML元素。

響應網格元件應預先映射到其對應AEM元件，因為此元件複雜且很少自定義。

#### 特定模型欄位 {#specific-model-fields}

* `gridClassNames:` 為響應網格提供的類名
* `columnClassNames:` 為響應列提供的類名

#### 回應網格的佔位符 {#placeholder-of-the-reponsive-grid}

該組SPA件被映射到諸如響應網格的圖形容器，並且當內容被創作時必須添加虛擬子佔位符。 當頁面編輯SPA器正在創作內容時，該內容將使用iframe和 `data-cq-editor` 屬性將添加到該內容的文檔節點。 當 `data-cq-editor` 屬性存在時，容器必須包含HTMLElement，以表示在將新元件插入頁面時作者與之交互的區域。

例如：

```
<div data-cq-data-path={"path/to/the/responsivegrid/*"} className="new section aem-Grid-newComponent"/>
```

>[!NOTE]
>
>該示例中使用的類名當前是頁面編輯器所需的。
>
>* `"new section"`:指示當前元素是容器的佔位符
>* `"aem-Grid-newComponent"`:將佈局創作的元件規範化
>


#### 元件映射 {#component-mapping}

底層 [`Component Mapping`](/help/sites-developing/spa-blueprint.md#componentmapping) 圖書館及其 `MapTo` 可以封裝和擴展功能以提供與當前元件類並列提供的編輯配置相關的功能。

```
const EditConfig = {

    emptyLabel: 'My Component',

    isEmpty: function() {
        return !this.props || !this.props.cqModel || this.props.cqModel.isEmpty;
    }
};

class MyComponent extends Component {

    render() {
        return <div className={'my-component'}></div>;
    }
}

MapTo('component/resource/path')(MyComponent, EditConfig);
```

在上述實施中，項目元件在實際註冊之前以空虛功能擴展 [元件映射](/help/sites-developing/spa-blueprint.md#componentmapping) 商店。 通過封裝和擴展 [`ComponentMapping`](/help/sites-developing/spa-blueprint.md#componentmapping) 圖書館介紹 `EditConfig` 配置對象：

```
/**
 * Configuration object in charge of providing the necessary data expected by the page editor to initiate the authoring. The provided data will be decorating the associated component
 *
 * @typedef {{}} EditConfig
 * @property {String} [dragDropName]       If defined, adds a specific class name enabling the drag and drop functionality
 * @property {String} emptyLabel           Label to be displayed by the placeholder when the component is empty. Optionally returns an empty text value
 * @property {function} isEmpty            Should the component be considered empty. The function is called using the context of the wrapper component giving you access to the component model
 */

/**
 * Map a React component with the given resource types. If an {@link EditConfig} is provided the <i>clazz</i> is wrapped to provide edition capabilities on the AEM Page Editor
 *
 * @param {string[]} resourceTypes                      - List of resource types for which to use the given <i>clazz</i>
 * @param {class} clazz                                 - Class to be instantiated for the given resource types
 * @param {EditConfig} [editConfig]                     - Configuration object for enabling the edition capabilities
 * @returns {class}                                     - The resulting decorated Class
 */
ComponentMapping.map = function map (resourceTypes, clazz, editConfig) {};
```

## 與頁面編輯器合同 {#contract-with-the-page-editor}

項目元件必須至少生成以下資料屬性，才能允許編輯器與它們交互。

* `data-cq-data-path`:元件的相對路徑 `PageModel` (例如， `"root/responsivegrid/image"`)。 不應將此屬性添加到頁面。

總之，要被頁面編輯器解釋為可編輯，項目元件必須遵守以下合同：

* 提供將前端元件實例與資源關聯的預期屬AEM性。
* 提供預期的一系列屬性和類名，以便建立空佔位符。
* 提供預期的類名，以便拖放資產。

### 典型HTML元結構 {#typical-html-element-structure}

以下片段說明了頁面內容結構的典型HTML表示形式。 以下是幾個重要點：

* 響應網格元素攜帶帶前置詞的類名 `aem-Grid--`
* 響應列元素攜帶帶前置詞的類名 `aem-GridColumn--`
* 將響應網格（也是父網格的列）包裝，例如兩個先前前置詞不出現在同一元素上
* 與可編輯資源對應的元素 `data-cq-data-path` 屬性。 查看 [與頁面編輯器合同](#contract-wtih-the-page-editor) 的子菜單。

```
<div data-cq-data-path="/content/page">
    <div class="aem-Grid aem-Grid--12 aem-Grid--default--12">
        <div class="aem-container aem-GridColumn aem-GridColumn--default--12" data-cq-data-path="/content/page/jcr:content/root/responsivegrid">
            <div class="aem-Grid aem-Grid--12 aem-Grid--default--12">
                <div class="cmp-image cq-dd-image aem-GridColumn aem-GridColumn--default--12" data-cq-data-path="/root/responsivegrid/image">
                    <img src="/content/we-retail-spa-sample/react/jcr%3acontent/root/responsivegrid/image.img.jpeg/1512113734019.jpeg">
                </div>
            </div>
        </div>
    </div>
</div>
```

## 導航和路由 {#navigation-and-routing}

應用擁有路由。 前端開發人員首先需要實現導航元件(映射到導AEM航元件)。 此元件將呈現要與一系列路由一起使用的URL連結，這些路由將顯示或隱藏內容片段。

底層 [ `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) 圖書館及其 ` [ModelRouter](/help/sites-developing/spa-routing.md)` 模組（預設啟用）負責預取和提供對與給定資源路徑關聯的模型的訪問。

兩個實體與路由的概念有關，但 ` [ModelRouter](/help/sites-developing/spa-routing.md)` 只負責 ` [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)` 載入了與當前應用程式狀態同步的資料模型。

請參閱文章 [模SPA型路由](/help/sites-developing/spa-routing.md) 的子菜單。

## SPA執行 {#spa-in-action}

通過繼續閱讀SPA文檔，瞭解一SPA個簡單的操作和實驗 [入SPA門AEM](/help/sites-developing/spa-getting-started-react.md)。

## 延伸閱讀 {#further-reading}

有關中的詳細SPA信AEM息，請參閱以下文檔：

* [創SPA作概述](/help/sites-developing/spa-overview.md) 有關SPAin和通AEM信模型的概述
* [入SPA門AEM](/help/sites-developing/spa-getting-started-react.md) 一個簡單的SPA指南
