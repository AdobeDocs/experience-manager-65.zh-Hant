---
title: SPA Blueprint
seo-title: SPA Blueprint
description: 本檔案說明任何SPA架構都應履行的一般、獨立於架構的合約，以便在AEM中實作可編輯的SPA元件。
seo-description: 本檔案說明任何SPA架構都應履行的一般、獨立於架構的合約，以便在AEM中實作可編輯的SPA元件。
uuid: 48f2d415-ec34-49dc-a8e1-6feb5a8a5bbe
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 04ac8203-320b-4671-aaad-6e1397b12b6f
docset: aem65
exl-id: 383f84fd-455c-49a4-9e2b-1c4757cc188b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2112'
ht-degree: 0%

---

# SPA Blueprint{#spa-blueprint}

為了讓作者能使用AEM SPA編輯器來編輯SPA的內容，SPA必須符合一些要求，本檔案將加以說明。

>[!NOTE]
>
>若專案需要SPA架構的用戶端轉譯(例如React或Angular),SPA Editor是建議的解決方案。

## 簡介 {#introduction}

本檔案說明任何SPA架構在AEM中實作可編輯SPA元件時，都應履行的一般合約(即AEM支援層的類型)。

>[!NOTE]
>
>下列需求與架構無關。 如果滿足這些要求，則可提供由模組、元件和服務組成的框架特定層。
>
>**AEM中的React和Angular架構已符合這些需求。** 只有在您想要實作其他框架以搭配AEM使用時，此Blueprint中的需求才相關。

>[!CAUTION]
>
>雖然AEM的SPA功能與架構無關，目前僅支援React和Angular架構。

若要讓作者能使用AEM頁面編輯器來編輯單頁應用程式架構公開的資料，專案必須能夠解譯模型的結構，該結構代表為AEM存放庫內的應用程式所儲存資料的語義。 為實現此目標，提供兩個無框架庫：`PageModelManager`和`ComponentMapping`。

### PageModelManager {#pagemodelmanager}

`PageModelManager`程式庫是以NPM套件的形式提供，供SPA專案使用。 隨附於SPA，可擔任資料模型管理員。

它代表SPA抽象出代表實際內容結構的JSON結構的擷取與管理。 它也負責與SPA同步，以告知其必須重新呈現元件的時間。

請參閱NPM套件[@adobe/aem-spa-page-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager)

初始化`PageModelManager`時，程式庫會先載入提供給應用程式的根模型（透過參數、中繼屬性或目前的URL）。 如果庫標識當前頁的模型不是其讀取的根模型的一部分，並將其作為子頁的模型包含。

![page_model_consolidation](assets/page_model_consolidation.png)

### 元件映射 {#componentmapping}

`ComponentMapping`模組作為NPM包提供給前端項目。 它會儲存前端元件，並提供讓SPA將前端元件對應至AEM資源類型的方式。 這可在剖析應用程式的JSON模型時，啟用元件的動態解析。

模型中呈現的每個項目都包含顯示AEM資源類型的`:type`欄位。 裝載時，前端元件可使用從基礎庫接收的模型片段來呈現自身。

#### 元件映射的動態模型{#dynamic-model-to-component-mapping}

如需有關AEM適用的Javascript SPA SDK中如何進行動態模型與元件對應的詳細資訊，請參閱文章[SPA適用的動態模型與元件對應](/help/sites-developing/spa-dynamic-model-to-component-mapping.md)。

### 框架特定層{#framework-specific-layer}

每個前端框架必須實現第三層。 此第三個程式庫負責與基礎程式庫互動，並提供一系列整合完善且易於使用的入口點，以便與資料模型互動。

本檔案的其餘部分說明了這一中間框架特定層的要求，並希望與框架無關。 通過遵循以下要求，可為項目元件提供框架特定層，以便與負責管理資料模型的底層庫交互。

## 一般概念{#general-concepts}

### 頁面模型{#page-model}

頁面的內容結構會儲存在AEM中。 頁面模型可用來映射及實例化SPA元件。 SPA開發人員會建立對應至AEM元件的SPA元件。 為此，他們會使用資源類型(或AEM元件的路徑)作為唯一索引鍵。

SPA元件必須與頁面模型同步，並隨著內容的任何變更而更新。 必須使用運用動態元件的模式，依照提供的頁面模型結構，即時實例化元件。

### 元欄位{#meta-fields}

頁面模型會運用JSON模型匯出工具，其本身是以[Sling Model](https://sling.apache.org/documentation/bundles/models.html) API為基礎。 可匯出的Sling模型會公開下列欄位清單，以便讓基礎程式庫解譯資料模型：

* `:type`:AEM資源的類型（預設=資源類型）
* `:children`:當前資源的分層子項。子項不是目前資源的內部內容的一部分（可在代表頁面的項目上找到）
* `:hierarchyType`:資源的階層類型。`PageModelManager`目前支援頁面類型

* `:items`:目前資源的子內容資源（巢狀結構，僅存在於容器上）
* `:itemsOrder`:訂了孩子的名單。JSON地圖物件無法保證其欄位的順序。 API的使用者同時擁有地圖和目前的陣列，便能享有這兩種結構的優點
* `:path`:項目的內容路徑（顯示在代表頁面的項目上）

另請參閱[AEM Content Services快速入門。](https://helpx.adobe.com/experience-manager/kt/sites/using/content-services-tutorial-use.html)

### 框架特定模組{#framework-specific-module}

分開關注有助於促進項目實施。 因此，應提供npm專屬套件。 此包負責聚合和公開基本模組、服務和元件。 這些元件必須封裝資料模型管理邏輯，並提供對項目元件期望的資料的訪問。 模組也負責傳遞性地公開基礎程式庫的有用入口點。

為方便程式庫的互操作性，Adobe建議架構特定模組捆綁下列程式庫。 如有必要，層可以先封裝和調整基礎API，再將其公開給專案。

* [@adobe/aem-spa-page-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager)
* [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

#### 實作 {#implementations}

#### React {#react}

npm模組：[@adobe-aem-react-editable-components](https://www.npmjs.com/package/@adobe/aem-react-editable-components)

#### Angular {#angular}

npm模組：即將推出

## 主要服務和元件{#main-services-and-components}

下列實體應按照每個框架的具體准則執行。 基於框架架構，實現方式可能大不相同，但必須提供描述的功能。

### 模型提供程式{#the-model-provider}

專案元件必須將模型片段的存取權委派給模型提供者。 然後，模型提供程式負責監聽對模型的指定片段所做的更改，並將更新的模型返回到委派元件。

要執行此操作，模型提供程式必須註冊到` [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)`。 然後，當發生變更時，會接收並將更新的資料傳遞至委派元件。 根據慣例，將承載模型片段的委派元件可用的屬性命名為`cqModel`。 實作可免費提供此屬性給元件，但應考慮到與架構架構整合、可探索性和易用性等方面。

### 元件HTML解碼器{#the-component-html-decorator}

元件裝飾器負責裝飾每個元件實例的元素的外部HTML，並具有頁面編輯器預期的一系列資料屬性和類名。

#### 元件聲明{#component-declaration}

必須將下列中繼資料新增至專案元件產生的外部HTML元素。 它們可讓頁面編輯器擷取對應的編輯設定。

* `data-cq-data-path`:相對於  `jcr:content`

#### 編輯功能聲明和佔位符{#editing-capability-declaration-and-placeholder}

必須將下列中繼資料和類別名稱新增至專案元件產生的外部HTML元素。 它們可讓頁面編輯器提供相關功能。

* `cq-placeholder`:標識空元件佔位符的類名
* `data-emptytext`:元件例項為空時要由覆蓋顯示的標籤

**空元件的佔位符**

每個元件都必須擴充一個功能，當元件識別為空時，該功能會使用預留位置和相關覆蓋圖專用的資料屬性和類別名稱來裝飾外部HTML元素。

**論構件的空虛性**

* 元件在邏輯上是空的嗎？
* 元件為空時，覆蓋圖所顯示的標籤應該是什麼？

### 容器 {#container}

容器是用於包含和呈現子元件的元件。 為此，容器會反覆其模型的`:itemsOrder`、`:items`和`:children`屬性。

容器會從` [ComponentMapping](/help/sites-developing/spa-blueprint.md#componentmapping)`程式庫的存放區動態取得子元件。 然後，容器會使用「模型提供者」功能擴充子元件，最後將其實例化。

### 頁面 {#page}

`Page`元件擴展`Container`元件。 容器是用來包含和呈現子元件（包括子頁）的元件。 為此，容器會反覆其模型的`:itemsOrder`、`:items`和`:children`屬性。 `Page`元件動態地從[ComponentMapping](/help/sites-developing/spa-blueprint.md#componentmapping)庫的儲存中獲取子元件。 `Page`負責實例化子元件。

### 回應式格線 {#responsive-grid}

回應式格線元件是容器。 它包含表示其列的模型提供程式的特定變體。 「響應網格」及其列負責裝飾項目元件的外部HTML元素，其中包含模型中的特定類名。

回應式格線元件應已預先對應至其AEM對應項目，因為此元件很複雜，且很少自訂。

#### 特定模型欄位{#specific-model-fields}

* `gridClassNames:` 為響應網格提供的類名
* `columnClassNames:` 提供回應式欄的類別名稱

另請參閱npm資源[@adobe/aem-react-editable-components#srccomponentsresponsvegridjsx](https://www.npmjs.com/package/@adobe/aem-react-editable-components#srccomponentsresponsivegridjsx)

#### 響應網格{#placeholder-of-the-reponsive-grid}的佔位符

SPA元件會對應至圖形容器（例如回應式格線），且在製作內容時必須新增虛擬子預留位置。 當SPA的內容由頁面編輯器製作時，該內容會使用iframe嵌入到編輯器中，而`data-cq-editor`屬性會新增到該內容的檔案節點。 當`data-cq-editor`屬性存在時，容器必須包含HTMLElement，以表示作者在頁面中插入新元件時與之互動的區域。

例如：

```
<div data-cq-data-path={"path/to/the/responsivegrid/*"} className="new section aem-Grid-newComponent"/>
```

>[!NOTE]
>
>頁面編輯器目前需要範例中使用的類別名稱。
>
>* `"new section"`:指示當前元素是容器的佔位符
>* `"aem-Grid-newComponent"`:將元件標準化以進行版面編寫

>



#### 元件映射{#component-mapping}

可以封裝和擴展底層的[`Component Mapping`](/help/sites-developing/spa-blueprint.md#componentmapping)庫及其`MapTo`函式，以提供與當前元件類附帶的編輯配置相關的功能。

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

在上述實作中，在[元件對應](/help/sites-developing/spa-blueprint.md#componentmapping)存放區中實際註冊之前，會以空白功能擴充專案元件。 要完成此操作，請封裝並擴展[`ComponentMapping`](/help/sites-developing/spa-blueprint.md#componentmapping)庫，以引入`EditConfig`配置對象的支援：

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

## 與頁面編輯器{#contract-with-the-page-editor}合約

專案元件至少必須產生下列資料屬性，才能讓編輯器與它們互動。

* `data-cq-data-path`:元件的相對路徑，如所 `PageModel` 提供(例如 `"root/responsivegrid/image"`)。不應將此屬性新增至頁面。

總之，要讓頁面編輯器將項目元件解釋為可編輯，必須遵守以下合同：

* 提供預期的屬性，以將前端元件實例與AEM資源關聯。
* 提供可建立空佔位符的預期屬性和類名系列。
* 提供可拖放資產的預期類別名稱。

### 典型HTML元素結構{#typical-html-element-structure}

下列片段說明頁面內容結構的典型HTML表示法。 以下是幾個重要點：

* 回應式格線元素會包含以`aem-Grid--`為首碼的類別名稱
* 回應式欄元素會包含以`aem-GridColumn--`為首碼的類別名稱
* 將響應網格（也是父網格的列）包裝，例如兩個前置詞不出現在同一元素上
* 與可編輯資源對應的元素會包含`data-cq-data-path`屬性。 請參閱本檔案的[與頁面編輯器](#contract-wtih-the-page-editor)合約一節。

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

## 導航和路由{#navigation-and-routing}

應用程式擁有路由。 前端開發人員必須先實作導覽元件(對應至AEM導覽元件)。 此元件會轉譯URL連結以搭配一系列路由使用，以顯示或隱藏內容片段。

基礎的[ `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager)庫及其` [ModelRouter](/help/sites-developing/spa-routing.md)`模組（預設啟用）負責預取並提供對與給定資源路徑關聯的模型的訪問。

這兩個實體與路由概念相關，但` [ModelRouter](/help/sites-developing/spa-routing.md)`只負責使` [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)`載入與當前應用程式狀態同步的資料模型。

如需詳細資訊，請參閱[SPA模型路由](/help/sites-developing/spa-routing.md)一文。

## SPA在動作中{#spa-in-action}

請繼續前往檔案[AEM](/help/sites-developing/spa-getting-started-react.md)中的SPA快速入門，了解簡單SPA如何運作並親自體驗SPA。

## 進一步閱讀{#further-reading}

如需AEM中SPA的詳細資訊，請參閱下列檔案：

* [SPA制](/help/sites-developing/spa-overview.md) 作概述，以取得AEM中SPA和通訊模型的概觀
* [AEM中的SPA快速](/help/sites-developing/spa-getting-started-react.md) 入門，以取得簡單SPA及其運作方式的指南
