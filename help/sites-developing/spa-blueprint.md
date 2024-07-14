---
title: SPA 藍圖
description: 本檔案說明任何SPA架構都應該履行的一般且獨立於架構的合約，以便在AEM內實作可編輯的SPA元件。
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
exl-id: 383f84fd-455c-49a4-9e2b-1c4757cc188b
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '2043'
ht-degree: 0%

---

# SPA 藍圖{#spa-blueprint}

若要讓作者能使用AEM SPA編輯器編輯SPA的內容，SPA必須滿足以下需求：本檔案將說明這些需求。

>[!NOTE]
>
>對於需要以SPA框架為基礎的使用者端轉譯(例如React或Angular)專案，建議使用SPA編輯器解決方案。

## 簡介 {#introduction}

本檔案說明任何SPA架構都應該履行的一般合約(即AEM支援層的型別)，以便在AEM內實作可編輯的SPA元件。

>[!NOTE]
>
>下列需求與架構無關。 如果滿足這些需求，則可以提供框架特定的層，該層由模組、元件和服務組成。
>
>**AEM中的React和Angular架構已符合這些需求。**&#x200B;只有當您想要實作其他框架以搭配AEM使用時，此藍圖中的需求才相關。

>[!CAUTION]
>
>雖然AEM的SPA功能與框架無關，但目前僅支援React和Angular框架。

若要讓作者能使用AEM頁面編輯器來編輯單頁應用程式架構所公開的資料，專案必須能夠解譯代表為AEM存放庫中應用程式儲存之資料語意的模型結構。 為了達成此目標，提供了兩個與架構無關的資料庫： `PageModelManager`和`ComponentMapping`。

### PageModelManager {#pagemodelmanager}

`PageModelManager`程式庫是以NPM封裝的形式提供，以供SPA專案使用。 它可與SPA搭配使用，並作為資料模型管理員。

它會代表SPA抽象化代表實際內容結構的JSON結構的擷取和管理。 此外也負責與SPA同步，以便在必須重新呈現元件時通知。

檢視NPM套件[@adobe/aem-spa-page-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager)

初始化`PageModelManager`時，程式庫會先載入應用程式提供的根模型（透過引數、中繼屬性或目前的URL）。 如果元件庫識別目前頁面的模型不是其擷取的根模型的一部分，並包含它作為子頁面的模型。

![page_model_consolidation](assets/page_model_consolidation.png)

### 元件對應 {#componentmapping}

`ComponentMapping`模組是以NPM封裝形式提供給前端專案。 它會儲存前端元件，並提供SPA將前端元件對應至AEM資源型別的方法。 如此一來，在剖析應用程式的JSON模型時，就能啟用元件的動態解析。

模型中每個專案都包含公開AEM資源型別的`:type`欄位。 掛載時，前端元件可使用從基礎程式庫收到的模型片段來轉譯自身。

#### 動態模型到元件對應 {#dynamic-model-to-component-mapping}

如需如何在AEM的JavaScript SPA SDK中發生動態模型到元件對應的詳細資訊，請參閱文章[SPA的動態模型到元件對應](/help/sites-developing/spa-dynamic-model-to-component-mapping.md)。

### 框架特定層 {#framework-specific-layer}

必須為每個前端框架實作第三層。 此第三個程式庫負責與基礎程式庫互動，並提供一系列整合良好且簡單易用的入口點，以便與資料模型互動。

本檔案的其餘部分說明此中介架構特定層的需求，並渴望與架構無關。 遵循下列需求，即可為專案元件提供架構專用層，以便與負責管理資料模型的基礎程式庫互動。

## 一般概念 {#general-concepts}

### 頁面模型 {#page-model}

頁面的內容結構儲存在AEM中。 頁面模型可用來對應及例項化SPA元件。 SPA開發人員建立對應至SPA元件的AEM元件。 為此，它們使用資源型別(或AEM元件的路徑)作為唯一索引鍵。

SPA元件必須和頁面模型同步，並更新以相應地變更其內容。 使用動態元件的陣列必須用來按照提供的頁面模型結構即時例項化元件。

### 中繼欄位 {#meta-fields}

頁面模型使用JSON模型匯出程式，其本身是以[Sling模型](https://sling.apache.org/documentation/bundles/models.html) API為基礎。 可匯出的Sling模型會顯示下列欄位清單，以啟用基礎程式庫來解譯資料模型：

* `:type`： AEM資源的型別（預設=資源型別）
* `:children`：目前資源的階層子系。 子系不屬於目前資源的內部內容（可在代表頁面的專案上找到）
* `:hierarchyType`：資源的階層型別。 `PageModelManager`目前支援頁面型別

* `:items`：目前資源的子內容資源（巢狀結構，僅存在於容器上）
* `:itemsOrder`：子項的已排序清單。 JSON對應物件無法保證其欄位的順序。 透過同時使用對應和目前的陣列，API的取用者便擁有兩種結構的優點
* `:path`：專案的內容路徑（存在於代表頁面的專案上）

另請參閱[AEM Content Services快速入門。](https://helpx.adobe.com/experience-manager/kt/sites/using/content-services-tutorial-use.html)

### 框架特定模組 {#framework-specific-module}

區隔關注點有助於促進專案實施。 因此，應該提供npm專屬套件。 此套件負責彙總及公開基本模組、服務和元件。 這些元件必須封裝資料模型管理邏輯，並提供專案元件所預期資料的存取權。 此模組也負責暫時公開基礎程式庫的實用進入點。

為了促進程式庫的互通性，Adobe建議框架特定的模組將下列程式庫捆綁。 如有必要，圖層可以在將底層API公開至專案之前，先進行封裝和調整。

* [@adobe/aem-spa-page-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager)
* [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

#### 實作 {#implementations}

#### React {#react}

npm模組： [@adobe/aem-react-editable-components](https://www.npmjs.com/package/@adobe/aem-react-editable-components)

#### angular {#angular}

npm模組： [@adobe/aem-angular-editable-components](https://www.npmjs.com/package/@adobe/aem-angular-editable-components)

## 主要服務與元件 {#main-services-and-components}

下列實體應根據每個框架的特定准則進行實施。 根據框架架構，實作可能會有很大的差異，但必須提供所描述的功能。

### 模型提供者 {#the-model-provider}

專案元件必須將模型片段的存取權委派給模型提供者。 然後，模型提供者會負責監聽對模型的指定片段所做的變更，並將更新的模型傳回委派元件。

為此，模型提供者必須向` [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)`註冊。 然後當變更發生時，它會接收更新後的資料並傳遞至委派元件。 根據慣例，可用於將承載模型片段的委派元件的屬性名為`cqModel`。 實作可免費為元件提供此屬性，但應考量與框架架構整合、可發現性和易用性等層面。

### 元件HTML裝飾器 {#the-component-html-decorator}

「元件裝飾器」負責以「頁面編輯器」所預期的一系列資料屬性和類別名稱，裝飾每個元件例項之元素的外部HTML。

#### 元件宣告 {#component-declaration}

下列中繼資料必須新增至專案元件產生的外部HTML元素。 它們可讓頁面編輯器擷取對應的編輯設定。

* `data-cq-data-path`：相對於`jcr:content`的資源路徑

#### 編輯功能宣告和預留位置 {#editing-capability-declaration-and-placeholder}

下列中繼資料和類別名稱必須新增至專案元件產生的外部HTML元素。 它們可讓頁面編輯器提供相關功能。

* `cq-placeholder`：識別空白元件預留位置的類別名稱
* `data-emptytext`：當元件執行個體為空白時，覆蓋圖所顯示的標籤

空白元件的&#x200B;**預留位置**

每個元件都必須延伸使用功能，以便在將元件識別為空白時，使用預留位置專用的資料屬性和類別名稱以及相關覆蓋來裝飾外部HTML元素。

**關於元件的空白**

* 元件在邏輯上是否為空白？
* 當元件為空白時，覆蓋圖應該顯示什麼標籤？

### 容器 {#container}

容器是用來包含和轉譯子元件的元件。 若要這麼做，容器會反複執行其模型的`:itemsOrder`、`:items`和`:children`屬性。

容器會從[`ComponentMapping`](/help/sites-developing/spa-blueprint.md#componentmapping)資料庫的存放區動態取得子元件。 容器接著會使用「模型提供者」功能擴充子元件，最後例項化它。

### 頁面 {#page}

`Page`元件會擴充`Container`元件。 容器是用來包含和轉譯子元件（包括子頁面）的元件。 若要這麼做，容器會反複執行其模型的`:itemsOrder`、`:items`和`:children`屬性。 `Page`元件會從[ComponentMapping](/help/sites-developing/spa-blueprint.md#componentmapping)程式庫的存放區動態取得子元件。 `Page`負責具現化子元件。

### 回應式格線 {#responsive-grid}

回應式格線元件是容器。 它包含模型提供者的特定變體，代表其欄。 回應式格線及其欄負責以模型中所包含的特定類別名稱裝飾專案元件的外部HTML元素。

回應式格線元件應預先對應至其AEM對應元件，因為此元件很複雜且很少自訂。

#### 特定模型欄位 {#specific-model-fields}

* `gridClassNames:`為回應式格線提供的類別名稱
* `columnClassNames:`為回應式資料行提供的類別名稱

#### 回應格線的預留位置 {#placeholder-of-the-reponsive-grid}

SPA元件會對應至圖形容器（例如回應式格線），且必須在編寫內容時新增虛擬子預留位置。 當頁面編輯器正在編寫SPA的內容時，該內容會使用iframe嵌入到編輯器中，並且`data-cq-editor`屬性會新增到該內容的檔案節點中。 當`data-cq-editor`屬性出現時，容器必須包含HTMLElement，以代表將新元件插入頁面時，作者互動的區域。

例如：

```
<div data-cq-data-path={"path/to/the/responsivegrid/*"} className="new section aem-Grid-newComponent"/>
```

>[!NOTE]
>
>範例中使用的類別名稱目前是頁面編輯器所需。
>
>* `"new section"`：表示目前的元素是容器的預留位置
>* `"aem-Grid-newComponent"`：標準化配置編寫的元件
>

#### 元件對應 {#component-mapping}

基礎的[`Component Mapping`](/help/sites-developing/spa-blueprint.md#componentmapping)程式庫及其`MapTo`函式可以封裝和延伸，以提供與目前元件類別隨附的編輯組態相關的函式。

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

在上述實作中，專案元件會在[元件對應](/help/sites-developing/spa-blueprint.md#componentmapping)存放區中實際登入之前，先以空白功能擴充。 這是透過封裝和擴充[`ComponentMapping`](/help/sites-developing/spa-blueprint.md#componentmapping)程式庫來完成，以引入`EditConfig`設定物件的支援：

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

## 與頁面編輯器訂約 {#contract-with-the-page-editor}

專案元件必須至少產生下列資料屬性，才能讓編輯器與其互動。

* `data-cq-data-path`： `PageModel`所提供的元件相對路徑（例如，`"root/responsivegrid/image"`）。 此屬性不應新增至頁面。

簡而言之，若要由頁面編輯器解譯為可編輯，專案元件必須符合下列合約：

* 提供預期屬性，以將前端元件執行個體與AEM資源建立關聯。
* 提供可建立空白預留位置的預期屬性系列和類別名稱。
* 提供預期的類別名稱，以啟用資產的拖放功能。

### 典型HTML元素結構 {#typical-html-element-structure}

以下片段說明頁面內容結構的典型HTML表示法。 以下是一些重要事項：

* 回應式格線元素含有前置詞為`aem-Grid--`的類別名稱
* 回應式資料行專案含有前置詞為`aem-GridColumn--`的類別名稱
* 回應式格線同時也是父格線的欄，因此會換行，例如前兩個字首未出現在相同元素上
* 對應至可編輯資源的元素包含`data-cq-data-path`屬性。 請參閱本檔案的[與頁面編輯器](#contract-wtih-the-page-editor)區段的合約。

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

## 導覽與路由 {#navigation-and-routing}

應用程式擁有路由。 前端開發人員首先需要實作導覽元件(對應至AEM導覽元件)。 此元件會轉譯URL連結，以便搭配顯示或隱藏內容片段的一系列路由使用。

基礎[`PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager)程式庫及其` [ModelRouter](/help/sites-developing/spa-routing.md)`模組（預設為啟用）負責預先擷取並提供與指定資源路徑關聯之模型的存取權。

這兩個實體與路由的概念有關，但` [ModelRouter](/help/sites-developing/spa-routing.md)`只負責讓` [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)`載入與目前應用程式狀態同步結構的資料模型。

如需詳細資訊，請參閱文章[SPA模型路由](/help/sites-developing/spa-routing.md)。

## SPA運作中 {#spa-in-action}

繼續檔案[AEM](/help/sites-developing/spa-getting-started-react.md)中的SPA快速入門，瞭解簡單SPA如何運作並親自實驗SPA。

## 延伸閱讀 {#further-reading}

如需AEM中SPA的詳細資訊，請參閱下列檔案：

* [SPA撰寫概觀](/help/sites-developing/spa-overview.md)，瞭解AEM中的SPA概觀和通訊模型
* [AEM中的SPA快速入門](/help/sites-developing/spa-getting-started-react.md)，瞭解簡單SPA的指南及其運作方式
