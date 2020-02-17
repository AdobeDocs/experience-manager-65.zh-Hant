---
title: SPA藍圖
seo-title: SPA藍圖
description: 本檔案說明任何SPA架構在AEM中實施可編輯的SPA元件時，應履行的一般、不受架構影響的合約。
seo-description: 本檔案說明任何SPA架構在AEM中實施可編輯的SPA元件時，應履行的一般、不受架構影響的合約。
uuid: 48f2d415-ec34-49dc-a8e1-6feb5a8a5bbe
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 04ac8203-320b-4671-aaad-6e1397b12b6f
docset: aem65
translation-type: tm+mt
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# SPA藍圖{#spa-blueprint}

若要讓作者使用AEM SPA編輯器來編輯SPA的內容，SPA必須符合一些要求，本檔案中已說明這些要求。

>[!NOTE]
>
>SPA編輯器是建議的解決方案，適用於需要以SPA架構為基礎的用戶端轉換（例如React或Angular）的專案。

## 簡介 {#introduction}

本檔案說明任何SPA架構在AEM中實作可編輯的SPA元件時，應履行的一般合約（即AEM支援層）。

>[!NOTE]
>
>下列需求與架構無關。 如果滿足這些要求，則可以提供由模組、元件和服務組成的框架特定層。
>
>**AEM中的React和Angular架構已符合這些需求。** 此藍圖中的要求只有在您想要實作另一個與AEM搭配使用的架構時才相關。

>[!CAUTION]
>
>雖然AEM的SPA功能與架構無關，但目前僅支援React和Angular架構。

若要讓作者使用AEM頁面編輯器來編輯「單頁應用程式」架構所公開的資料，專案必須能夠解譯模型的結構，以表示AEM儲存庫中應用程式所儲存資料的語義。 為了實現此目標，提供了兩個框架不可知庫：還有 `PageModelManager` 那個 `ComponentMapping`。

### PageModelManager {#pagemodelmanager}

該 `PageModelManager` 庫作為NPM包提供，供SPA項目使用。 它隨附於SPA中，並擔任資料模型管理員。

它代表SPA，抽象出代表實際內容結構的JSON結構的檢索與管理。 此外，它還負責與SPA同步，讓它知道何時必須重新演算元件。

請參閱NPM [套件@adobe/cq-spa-page-model-manager](https://www.npmjs.com/package/@adobe/cq-spa-page-model-manager)

初始化應 `PageModelManager`用程式時，程式庫會先載入提供的應用程式根模型（透過參數、中繼屬性或目前的URL）。 如果庫標識當前頁的模型不屬於其讀取的根模型，並將其作為子頁的模型包含在內。

![page_model_consolidation](assets/page_model_consolidation.png)

### ComponentMapping {#componentmapping}

該 `ComponentMapping` 模組作為NPM包提供給前端項目。 它儲存前端元件，並提供SPA將前端元件對應至AEM資源類型的方式。 如此可在剖析應用程式的JSON模型時，啟用元件的動態解析度。

模型中的每個項目都包含一個 `:type` 欄位，可顯示AEM資源類型。 當裝載時，前端元件可以使用它從基礎庫接收到的模型片段進行自身渲染。

#### 動態模型到元件映射 {#dynamic-model-to-component-mapping}

如需AEM的Javascript SPA SDK中動態模型至元件對應的詳細資訊，請參閱SPA的動態模型至元件對 [應文章](/help/sites-developing/spa-dynamic-model-to-component-mapping.md)。

### 框架特定層 {#framework-specific-layer}

每個前端框架都必須實施第三層。 此第三個程式庫負責與基礎程式庫互動，並提供一系列整合良好且易於使用的入口點，以與資料模型互動。

本檔案的其餘部分描述了此中間框架特定層的要求，並希望與框架無關。 通過遵守以下要求，可以為項目元件提供一個框架特定層，以便與負責管理資料模型的底層庫交互。

## 一般概念 {#general-concepts}

### 頁面模型 {#page-model}

頁面的內容結構會儲存在AEM中。 頁面模型用於映射和實例化SPA元件。 SPA開發人員會建立SPA元件，並對應至AEM元件。 為此，他們會使用資源類型（或AEM元件的路徑）做為唯一索引鍵。

SPA元件必須與頁面模型同步，並隨之更新其內容。 必須使用運用動態元件的模式，依據提供的頁面模型結構即時執行個體化元件。

### 中繼欄位 {#meta-fields}

頁面模型運用JSON模型匯出器，它本身是以 [Sling Model](https://sling.apache.org/documentation/bundles/models.html) API為基礎。 可匯出的吊索模型會公開下列欄位清單，以便啟用基礎程式庫解譯資料模型：

* `:type`:AEM資源的類型（預設=資源類型）
* `:children`:當前資源的分層子項。 子項不屬於當前資源的內部內容（可在代表頁面的項目上找到）
* `:hierarchyType`:資源的分層類型。 目前 `PageModelManager` 支援頁面類型

* `:items`:目前資源的子內容資源（巢狀結構，僅存在於容器上）
* `:itemsOrder`:已排列子系的清單。 JSON地圖物件無法保證其欄位順序。 API的使用者同時擁有地圖和目前的陣列，可享有這兩種架構的優點
* `:path`:項目的內容路徑（顯示在代表頁面的項目上）

另請參 [閱「AEM Content services快速入門」。](https://helpx.adobe.com/experience-manager/kt/sites/using/content-services-tutorial-use.html)

### 框架特定模組 {#framework-specific-module}

分開顧慮有助於促進項目實施。 因此，應提供npm特定的套件。 此軟體包負責聚合和公開基本模組、服務和元件。 這些元件必須封裝資料模型管理邏輯，並提供對項目元件期望的資料的訪問。 該模組還負責傳遞性地暴露底層庫的有用入口點。

為了促進程式庫的互用性，Adobe建議架構特定模組整合下列程式庫。 如果需要，該層可以在將底層API暴露到項目之前封裝和調整它們。

* [@adobe/cq-spa-page-model-manager](https://www.npmjs.com/package/@adobe/cq-spa-page-model-manager)
* [@adobe/cq-spa-component-mapping](https://www.npmjs.com/package/@adobe/cq-spa-component-mapping)

#### 實施 {#implementations}

#### 反應 {#react}

npm模組： [@adobe/cq-react-editable-components](https://www.npmjs.com/package/@adobe/cq-react-editable-components)

#### 角度 {#angular}

npm模組：即將推出

## 主要服務與元件 {#main-services-and-components}

應按照每個框架的具體准則執行下列實體。 基於框架結構，實現方式可能差異很大，但必須提供描述的功能。

### 模型提供者 {#the-model-provider}

項目元件必須將模型片段的訪問權限委派給模型提供器。 然後模型提供者負責監聽對模型指定片段所做的變更，並將更新的模型傳回委託元件。

為此，模型提供者必須向註冊 ` [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)`。 然後，當發生變更時，它會接收並將更新的資料傳遞至委派元件。 根據慣例，將為將攜帶模型片段的委託元件提供的屬性命名 `cqModel`。 實作可免費提供此屬性給元件，但應考慮與架構架構整合、可探索性及易於使用等方面。

### 元件HTML Decorator {#the-component-html-decorator}

Component Decorator負責裝飾每個元件實例的元素的外部HTML，並具有頁面編輯器預期的一系列資料屬性和類名。

#### 元件聲明 {#component-declaration}

下列中繼資料必須新增至專案元件產生的外部HTML元素。 它們可讓頁面編輯器擷取對應的編輯設定。

* `data-cq-data-path`:資源相對於 `jcr:content`

#### 編輯功能聲明和佔位符 {#editing-capability-declaration-and-placeholder}

下列中繼資料和類別名稱必須新增至專案元件產生的外部HTML元素。 它們可讓頁面編輯器提供相關功能。

* `cq-placeholder`:用於標識空元件佔位符的類名
* `data-emptytext`:元件例項空白時，覆蓋顯示的標籤

**空元件的預留位置**

每個元件都必須擴充其功能，當元件識別為空白時，這些功能會使用預留位置和相關覆蓋專屬的資料屬性和類別名稱來裝飾外部HTML元素。

**論構件的虛性**

* 元件在邏輯上是空的嗎？
* 當元件為空時，覆蓋所顯示的標籤應是什麼？

### 容器 {#container}

容器是用於包含和渲染子元件的元件。 為此，容器會重複其 `:itemsOrder`模型 `:items` 和 `:children` 屬性。

容器會動態從程式庫的儲存區取得子 ` [ComponentMapping](/help/sites-developing/spa-blueprint.md#componentmapping)` 元件。 然後，容器會使用「模型提供者」功能來擴充子元件，並最終執行個體化它。

### 頁面 {#page}

該組 `Page` 件延伸該組 `Container` 件。 容器是用於包含和呈現子元件（包括子頁）的元件。 為此，容器會重複其 `:itemsOrder`模型 `:items`的 `:children` 、和屬性。 元 `Page` 件會動態從ComponentMapping程式庫的儲存區取得 [子元件](/help/sites-developing/spa-blueprint.md#componentmapping) 。 負責 `Page` 實例化子元件。

### 回應式格線 {#responsive-grid}

回應式格線元件是容器。 它包含表示其列的「模型提供器」的特定變型。 「自適應格線」及其列負責用模型中包含的特定類名裝飾項目元件的外部HTML元素。

回應式格線元件應預先對應至其AEM對應元件，因為此元件很複雜，而且很少加以自訂。

#### 特定模型欄位 {#specific-model-fields}

* `gridClassNames:` 為響應網格提供的類名
* `columnClassNames:` 為響應列提供的類名

另請參閱npm資 [源@adobe/cq-react-editable-componentsresponvegridjsx](https://www.npmjs.com/package/@adobe/cq-react-editable-components#srccomponentsresponsivegridjsx)

#### 回應式格線的預留位置 {#placeholder-of-the-reponsive-grid}

SPA元件會對應至圖形容器（例如回應式格線），且在製作內容時必須新增虛擬子預留位置。 當頁面編輯器編寫SPA內容時，該內容會使用iframe嵌入到編輯器中，並且 `data-cq-editor` 將屬性添加到該內容的文檔節點。 當屬 `data-cq-editor` 性存在時，容器必須包含HTMLElement，以表示在將新元件插入頁面時作者與之互動的區域。

例如：

```
<div data-cq-data-path={"path/to/the/responsivegrid/*"} className="new section aem-Grid-newComponent"/>
```

>[!NOTE]
>
>頁面編輯器目前需要範例中使用的類別名稱。
>
>* `"new section"`:指出目前元素是容器的預留位置
>* `"aem-Grid-newComponent"`:標準化版面製作的元件
>



#### Component Mapping {#component-mapping}

基礎組 [件映射庫及其功](/help/sites-developing/spa-blueprint.md#componentmapping)`MapTo` 能可以封裝和擴展，以提供與當前元件類附帶的編輯配置相關的功能。

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

在上述實施中，項目元件在實際註冊到元件映射儲存之前，以空 [洞功能擴展](/help/sites-developing/spa-blueprint.md#componentmapping) 。 通過封裝和擴展庫來 ` [ComponentMapping](/content.md#main-pars_header_906602219)` 引入對配置對象的 `EditConfig` 支援：

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

## 與頁面編輯器合約 {#contract-wtih-the-page-editor}

專案元件必須至少產生下列資料屬性，才能讓編輯者與它們互動。

* `data-cq-data-path`:由（例如，）提供的組 `PageModel` 件的相對路 `"root/responsivegrid/image"`徑。 不應將此屬性新增至頁面。

總之，要讓頁面編輯器將項目元件解釋為可編輯，項目元件必須遵守以下合同：

* 提供預期的屬性，將前端元件例項與AEM資源建立關聯。
* 提供可建立空佔位符的預期屬性和類名。
* 提供預期的類別名稱，以便拖放資產。

### 典型的HTML元素結構 {#typical-html-element-structure}

以下片段說明頁面內容結構的典型HTML表示法。 以下是幾個要點：

* 響應式格線元素承載預先固定的類別名稱 `aem-Grid--`
* 回應式欄元素會載入前置詞的類別名稱 `aem-GridColumn--`
* 將作為父網格的列的響應網格包起來，例如兩個前置詞不出現在同一元素上
* 與可編輯資源對應的元素會攜帶屬 `data-cq-data-path` 性。 請參閱 [本檔案的「與頁面編輯器](#contract-wtih-the-page-editor) 」一節。

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

## 導覽和路由 {#navigation-and-routing}

應用程式擁有路由。 前端開發人員首先需要實作導覽元件（對應至AEM導覽元件）。 此元件會轉譯URL連結，以搭配一系列路由使用，以顯示或隱藏內容片段。

基礎 [ 庫及 `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) 其模組(預設 ` [ModelRouter](/help/sites-developing/spa-routing.md)` 啟用)負責預取和提供對與給定資源路徑相關聯的模型的訪問。

這兩個實體與路由的概念有關，但 ` [ModelRouter](/help/sites-developing/spa-routing.md)` 它只負責使載入的資料模型 ` [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)` 與當前應用程式狀態同步。

如需詳細資訊， [請參閱文章](/help/sites-developing/spa-routing.md) 「SPA模型路由」。

## SPA的實際運作 {#spa-in-action}

請繼續閱讀AEM中的SPA快速入門檔案，瞭解簡單的SPA如何運作，並親自 [試驗SPA](/help/sites-developing/spa-getting-started-react.md)。

## 進一步閱讀 {#further-reading}

如需AEM中SPA的詳細資訊，請參閱下列檔案：

* [SPA製作概觀](/help/sites-developing/spa-overview.md) ，以取得AEM中SPA和通訊模型的概觀
* [AEM中的SPA快速入門](/help/sites-developing/spa-getting-started-react.md) ，以取得簡單SPA的指南及其運作方式
