---
title: 開發報告
seo-title: Developing Reports
description: 提AEM供基於報告框架的標準報告選擇
seo-description: AEM provides a selection of standard reports based on a reporting framework
uuid: 1b406d15-bd77-4531-84c0-377dbff5cab2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 50fafc64-d462-4386-93af-ce360588d294
exl-id: 3891150e-9972-4bbc-ad61-7f46a1f9bbb4
source-git-commit: 071bc0e36ed2d8eb4ce7bd0ba46823adc0e43095
workflow-type: tm+mt
source-wordcount: '5238'
ht-degree: 0%

---


# 開發報告 {#developing-reports}

AEM提供 [標準報表](/help/sites-administering/reporting.md) 其中大部分基於報告框架。

使用該框架，您可以擴展這些標準報告，也可以開發自己的全新報告。 報告框架與現有的CQ5概念和原則緊密整合，以便開發人員可以將他們對CQ5的現有知識用作開發報告的跳板。

對於與以下項交付的標準報AEM告：

* 這些報告是基於報告框架構建的：

   * [元件報表](/help/sites-administering/reporting.md#component-report)
   * [頁面活動報表](/help/sites-administering/reporting.md#page-activity-report)
   * [使用者報表](/help/sites-administering/reporting.md#user-report)
   * [工作流程例項報表](/help/sites-administering/reporting.md#workflow-instance-report)

* 下列報告基於個別原則，因此不能擴展：

   * [磁碟使用情況](/help/sites-administering/reporting.md#disk-usage)
   * [運行狀況檢查](/help/sites-administering/reporting.md#health-check)
   * [工作流報告](/help/sites-administering/reporting.md#workflow-report)

>[!NOTE]
>
>教程 [建立您自己的報告 — 示例](#creating-your-own-report-an-example) 還顯示了可以使用的原則。
>
>您還可以參考標準報告，以查看其他實施示例。

>[!NOTE]
>
>在下面的示例和定義中使用了以下符號：
>
>* 每行定義一個節點或一個屬性，其中：
   >  `N:<name> [<nodeType>]` :描述名稱為 `<*name*>` 和節點類型 `<*nodeType*>`*。*
   >  `P:<name> [<propertyType]` :描述名稱為 `<*name*>` 和屬性類型 `<*propertyType*>`。
   >  `P:<name> = <value>` :描述屬性 `<name>` 必須設定為 `<value>`。
>
>* 縮排顯示節點之間的層次相關性。
>* 分隔為 |表示可能項的清單；例如，類型或名稱；例如 `String|String[]` 表示屬性可以是String或String[]。
>
>* `[]` 描述陣列；例如字串[] 或節點陣列，如 [查詢定義](#query-definition)。
>
>除非另有說明，否則預設類型為：
>
>* 節點 —  `nt:unstructured`
>* 屬性 - `String`


## 報告框架 {#reporting-framework}

報告框架遵循以下原則：

* 它完全基於由CQ5 QueryBuilder執行的查詢返回的結果集。
* 結果集定義報表中顯示的資料。 結果集中的每一行都對應於報表的表格視圖中的一行。
* 可在結果集上執行的操作類似於RDBMS概念；主要 *分組* 和 *聚合*。

* 大多數的資料檢索和處理都是在伺服器端完成的。
* 客戶端僅負責顯示預處理的資料。 客戶端只執行次要處理任務（例如，在單元格內容中建立連結）。

報告框架（通過標準報告的結構說明）使用以下由處理隊列饋送的構造塊：

![chlimage_1-248](assets/chlimage_1-248.png)

### 報告頁 {#report-page}

報告頁：

* 是標準CQ5頁。
* 基於 [標準CQ5模板，為報表配置](#report-template)。

### 報表庫 {#report-base}

的 [ `reportbase` 元件](#report-base-component) 構成任何報告之基礎：

* 保留 [查詢](#the-query-and-data-retrieval) 提供資料的基礎結果集。

* 是包含所有列( `columnbase`)。
* 定義哪些圖表類型可用以及哪些當前處於活動狀態。
* 定義「編輯」對話框，該對話框允許用戶配置報告的某些方面。

### 列基 {#column-base}

每列都是 [ `columnbase` 元件](#column-base-component) :

* 是段落，由parsys( `reportbase`)。
* 定義到 [基礎結果集](#the-query-and-data-retrieval);即定義此結果集中引用的特定資料及其處理方式。
* 包含其他定義；例如可用的聚合和篩選器以及任何預設值。

### 查詢與資料檢索 {#the-query-and-data-retrieval}

查詢：

* 定義為 [ `reportbase`](#report-base) 元件。
* 基於 [CQ查詢生成器](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html)。
* 檢索用作報表基礎的資料。 結果集（表）的每一行都與查詢返回的節點相關聯。 特定資訊 [單個列](#column-base-component) 從此資料集中提取。

* 通常包括：

   * 根路徑。

      這指定要搜索的儲存庫的子樹。

      為幫助最小化效能影響，建議（嘗試）將查詢限制在儲存庫的特定子樹中。 根路徑可以在 [報表模板](#report-template) 或由 [「配置（編輯）」對話框](#configuration-dialog)。

   * [一個或多個條件](#query-definition)。

      這些結果被強加以產生（初始）結果集；它們包括節點類型限制或屬性約束。

**這裡的關鍵點是，查詢結果集中返回的每個單個節點都用於在報表上生成一行（因此為1:1關係）。**

開發人員必須確保為報表定義的查詢返回適合該報表的節點集。 但是，節點本身不需要保存所有所需資訊，這也可以從父節點和/或子節點派生。 例如，用於 [用戶報告](/help/sites-administering/reporting.md#user-report) 根據節點類型選擇節點（在本例中） `rep:user`)。 但是，此報表中的大多數列不會直接從這些節點獲取其資料，而是從子節點獲取資料 `profile`。

### 處理隊列 {#processing-queue}

的 [查詢](#the-query-and-data-retrieval) 返回要作為行顯示在報表上的資料的結果集。 處理結果集中的每一行（伺服器端），在 [幾個階段](#phases-of-the-processing-queue)，然後轉到客戶端以在報告中顯示。

這允許：

* 從基礎結果集提取和導出值。

   例如，它允許您通過計算兩個屬性值之間的差值，將兩個屬性值作為單個值處理。

* 解析提取的值；這可以通過多種方式實現。

   例如，路徑可以映射到標題（如在各自的更易人讀的內容中） *jcr：標題* 屬性)。

* 在不同點上應用濾鏡。
* 如有必要，建立複合值。

   例如，由顯示給用戶的文本、用於排序的值和用於建立連結的附加URL組成。

#### 處理隊列的工作流 {#workflow-of-the-processing-queue}

以下工作流表示處理隊列：

![chlimage_1-249](assets/chlimage_1-249.png)

#### 處理隊列的階段 {#phases-of-the-processing-queue}

其中詳細步驟和元素包括：

1. 轉換由 [初始查詢(reportbase)](#query-definition) 使用值提取器輸入基本結果集。

   根據 [列類型](#column-specific-definitions)。 它們用於從基礎JCR查詢中讀取值並從中建立結果集；之後，可應用進一步處理。 例如， `diff` 類型，值提取器讀取兩個屬性，計算單個值，然後將其添加到結果集。 無法配置值提取器。

1. 對於包含原始資料的初始結果集， [初始濾波](#column-specific-definitions) (*生* )。

1. 值為 [預處理](#processing-queue);定義 *應用* 。

1. [篩選](#column-specific-definitions) (分配給 *預處理* 階段)。

1. 值被解析；根據 [定義的解析器](#processing-queue)。
1. [篩選](#column-specific-definitions) (分配給 *已解決* 階段)。

1. 資料是 [分組和聚合](#column-specific-definitions)。
1. 通過將陣列資料轉換為（基於字串）清單來解析陣列資料。

   這是一個將多值結果轉換為可顯示的清單的隱式步驟；基於多值JCR屬性的（未聚合）單元格值是必需的。

1. 值再次 [預處理](#processing-queue);定義 *應用後* 。

1. 資料已排序。
1. 處理的資料被傳送到客戶機。

>[!NOTE]
>
>返回基本資料結果集的初始查詢是在 `reportbase` 元件。
>
>處理隊列的其他元素在 `columnbase` 元件。

## 報告構造和配置 {#report-construction-and-configuration}

構建和配置報告時需要以下內容：

* a [報告元件定義的位置](#location-of-report-components)
* a [ `reportbase` 元件](#report-base-component)
* 一個或更多， [ `columnbase` 元件](#column-base-component)
* a [頁面元件](#page-component)
* a [報表設計](#report-design)
* a [報表模板](#report-template)

### 報表元件的位置 {#location-of-report-components}

預設報告元件保存於 `/libs/cq/reporting/components`。

但是，強烈建議您不要更新這些節點，而是在以下位置建立自己的元件節點 `/apps/cq/reporting/components` 或者如果合適 `/apps/<yourProject>/reports/components`。

其中（例如）:

```
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:components [sling:Folder]
```

在此下，您為報表建立根，在此下，報表基元件和列基元件：

```
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:components [sling:Folder]
                N:<reportname> [sling:Folder]
                        N:<reportname> [cq:Component]  // report base component
                        N:<columnname> [cq:Component]  // column base component
```

### 頁面元件 {#page-component}

報告頁必須使用 `sling:resourceType` 共 `/libs/cq/reporting/components/reportpage`。

定製的頁面元件不應是必需的（在大多數情況下）。

## 報表基元件 {#report-base-component}

每個報告類型都需要從中派生的容器元件 `/libs/cq/reporting/components/reportbase`。

此元件作為整個報表的容器，並提供以下資訊：

* 的 [查詢定義](#query-definition)。
* 安 [（可選）對話框](#configuration-dialog) 中。
* 任意 [圖表](#chart-definitions) 併入報告。

```
N:<reportname> [cq:Component]
    P:sling:resourceSuperType = "cq/reporting/components/reportbase"
    N:charting
    N:dialog [cq:Dialog]
    N:queryBuilder
```

### 查詢定義 {#query-definition}

```xml
N:queryBuilder
    N:propertyConstraints
    [
        N:<name> // array of nodes (name irrelevant), each with the following properties:
            P:name
            P:value
    ]
    P:nodeTypes [String|String[]]
    P:mandatoryProperties [String|String[]
  ]
```

* `propertyConstraints`

   可用於將結果集限制到具有特定屬性且具有特定值的節點。 如果指定了多個約束，則節點必須滿足所有約束（AND操作）。

   例如：

   ```
   N:propertyConstraints
    [
    N:0
    P:sling:resourceType
    P:foundation/components/textimage
    N:1
    P:jcr:modifiedBy
    P:admin
    ]
   ```

   將返回所有 `textimage` 上次由 `admin` 。

* `nodeTypes`

   用於將結果集限制為指定的節點類型。 可以指定多個節點類型。

* `mandatoryProperties`

   可用於將結果集限制到具有 *全部* 的子菜單。 屬性的值未被考慮在內。

所有項都是可選的，可根據需要組合，但必須至少定義其中一項。

### 圖表定義 {#chart-definitions}

```xml
N:charting
    N:settings
        N:active [cq:WidgetCollection]
        [
            N:<name> // array of nodes, each with the following property
                P:id   // must match the id of a child node of definitions
        ]
    N:definitions [cq:WidgetCollection]
    [
        N:<name> // array of nodes, each with the following properties
            P:id
            P:type
            // additional, chart type specific configurations
    ]
```

* `settings`

   保存活動圖表的定義。

   * `active`

      由於可以定義多個設定，因此可以使用此設定定義當前處於活動狀態的設定。 這些由節點陣列定義(這些節點沒有強制命名約定，但標準報告通常使用 `0`。 `1`.. `x`)，每個具有以下屬性：

      * `id`

         活動圖表的標識。 這必須與圖表之一的ID匹配 `definitions`。

* `definitions`

   定義可能可用於報表的圖表類型。 的 `definitions` 將由 `active` 的子菜單。

   定義使用節點陣列指定(通常也稱為 `0`。 `1`.. `x`)，每個都具有以下屬性：

   * `id`

      圖表標識。

   * `type`

      可用的圖表類型。 從以下位置選擇：

      * `pie`
餅圖。 僅從當前資料生成。

      * `lineseries`
一系列線（代表實際快照的連接點）。 僅從歷史資料生成。
   * 其他屬性可用，具體取決於圖表類型：

      * 圖表類型 `pie`:

         * `maxRadius` ( `Double/Long`)

            餅圖允許的最大半徑；因此圖表允許的最大大小（無圖例）。 如果忽略 `fixedRadius` 。

         * `minRadius` ( `Double/Long`)

            餅圖允許的最小半徑。 如果忽略 `fixedRadius` 。

         * `fixedRadius` ( `Double/Long`)定義餅圖的固定半徑。
      * 圖表類型 [`lineseries`](/help/sites-administering/reporting.md#display-limits):

         * `totals` ( `Boolean`)

            如果顯示的附加行為 **合計** 應顯示。
預設: `false`

         * `series` ( `Long`)

            要顯示的行/系列數。
預設： `9` （這也是允許的最大值）

         * `hoverLimit` ( `Long`)

            要為其顯示彈出窗口的聚合快照（每個水準線上顯示的點，表示不同值）的最大數量，即當用戶在圖表圖例中的不同值或相應標籤上滑鼠懸停時。

            預設： `35` （即，如果當前圖表設定適用的不同值超過35個，則根本不顯示彈出窗口）。

            可以並行顯示的彈出窗口數量還限制為10個（當在圖例文本上進行滑鼠懸停時，可顯示多個彈出窗口）。



### 「配置」對話框 {#configuration-dialog}

每個報告都可以有一個配置對話框，允許用戶為報告指定各種參數。 此對話框可通過 **編輯** 按鈕。

此對話框是標準CQ [對話](/help/sites-developing/components-basics.md#dialogs) 可以這樣配置(請參見 [CQ對話框](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog) )的正平方根。

示例對話框如下所示：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    jcr:primaryType="cq:Dialog"
    height="{Long}424">
    <items jcr:primaryType="cq:WidgetCollection">
        <props jcr:primaryType="cq:Panel">
            <items jcr:primaryType="cq:WidgetCollection">
                <title
                    jcr:primaryType="cq:Widget"
                    path="/libs/cq/reporting/components/commons/title.infinity.json"
                    xtype="cqinclude"/>
                <description
                    jcr:primaryType="cq:Widget"
                    path="/libs/cq/reporting/components/commons/description.infinity.json"
                    xtype="cqinclude"/>
                <rootPath
                    jcr:primaryType="cq:Widget"
                    fieldLabel="Root path"
                    name="./report/rootPath"
                    rootPath=""
                    rootTitle="Repository root"
                    xtype="pathfield"/>
                <processing
                    jcr:primaryType="cq:Widget"
                    path="/libs/cq/reporting/components/commons/processing.infinity.json"
                    xtype="cqinclude"/>
                <scheduling
                    jcr:primaryType="cq:Widget"
                    path="/libs/cq/reporting/components/commons/scheduling.infinity.json"
                    xtype="cqinclude"/>
            </items>
        </props>
    </items>
</jcr:root>
```

提供了幾個預配置的元件；可以在對話框中引用， `xtype` 值為 `cqinclude`:

* **`title`**

   `/libs/cq/reporting/components/commons/title`

   定義報表標題的文本欄位。

* **`description`**

   `/libs/cq/reporting/components/commons/description`

   Textarea以定義報表說明。

* **`processing`**

   `/libs/cq/reporting/components/commons/processing`

   報表處理模式的選擇器（手動/自動載入資料）。

* **`scheduling`**

   `/libs/cq/reporting/components/commons/scheduling`

   用於為歷史圖表安排快照的選擇器。

>[!NOTE]
>
>必須使用 `.infinity.json` 尾碼（請參閱上例）。

### 根路徑 {#root-path}

此外，還可以為報告定義根路徑：

* **`rootPath`**

   這會將報告限制在儲存庫的某個部分（樹或子樹），這是效能優化的建議。 根路徑由 `rootPath` 屬性 `report` 每個報表頁的節點（建立頁時從模板獲取）。

   可以通過以下方式指定：

   * 這樣 [報表模板](#report-template) （作為固定值或作為配置對話框的預設值）。
   * 用戶（使用此參數）

## 列基元件 {#column-base-component}

每個列類型都需要從 `/libs/cq/reporting/components/columnbase`。

列元件定義以下組合：

* 的 [列特定查詢](#column-specific-query) 配置。
* 的 [解析器和預處理](#resolvers-and-preprocessing)。
* 的 [列特定定義](#column-specific-definitions) (如過濾器和聚合； `definitions` 子節點)。
* [列預設值](#column-default-values)。
* 的 [客戶端篩選器](#client-filter) 從伺服器返回的資料中提取要顯示的資訊。
* 此外，列元件必須提供適合的 `cq:editConfig`。 定義 [事件和操作](#events-and-actions) 。
* 的配置 [通用列](#generic-columns)。

```
N:<columnname> [cq:Component]
    P:componentGroup
    P:jcr:title
    P:sling:resourceSuperType = "cq/reporting/components/columnbase"
    N:cq:editConfig [cq:EditConfig] // <a href="#events-and-actions">Events and Actions</a>
    N:defaults // <a href="#column-default-values">Column Default Values</a>
    N:definitions
      N:queryBuilder // <a href="#column-specific-query">Column Specific Query</a>
        P:property [String|String[]] // Column Specific Query
        P:subPath // Column Specific Query
        P:secondaryProperty [String|String[]] // Column Specific Query
        P:secondarySubPath // Column Specific Query
      N:data
        P:clientFilter [String] // <a href="#client-filter">Client Filter</a>
        P:resolver // <a href="#resolvers-and-preprocessing">Resolvers and Preprocessing</a>
        N:resolverConfig // Resolvers and Preprocessing
        N:preprocessing // Resolvers and Preprocessing
      P:type // <a href="#column-specific-definitions">Column Specific Definitions</a>
      P:groupable [Boolean] // Column Specific Definitions
      N:filters [cq:WidgetCollection] // Column Specific Definitions
      N:aggregates [cq:WidgetCollection] // Column Specific Definitions
```

另請參閱 [定義新報表](#defining-your-new-report)。

### 列特定查詢 {#column-specific-query}

這定義了特定資料提取(從 [報表資料結果集](#the-query-and-data-retrieval))，用於單列。

```xml
N:definitions
    N:queryBuilder
        P:property [String|String[]]
        P:subPath
        P:secondaryProperty [String|String[]]
        P:secondarySubPath
```

* `property`

   定義用於計算實際單元格值的屬性。

   如果屬性定義為字串[] 掃描多個屬性（按順序）以查找實際值。

   例如，在以下情況下：

   `property = [ "jcr:lastModified", "jcr:created" ]`

   相應的值提取器（此處控制）將：

   * 檢查是否存在jcr:lastModified屬性，如果可用，則使用它。
   * 如果沒有jcr:lastModified屬性可用，則將改用jcr:created的內容。

* `subPath`

   如果結果不在查詢返回的節點上， `subPath` 定義屬性的實際位置。

* `secondaryProperty`

   定義另一個屬性，該屬性還必須用於計算實際單元格值；這將僅用於某些列類型（diff和sortable）。

   例如，在「工作流實例報表」中，指定的屬性用於儲存開始時間和結束時間之間時間差的實際值（以毫秒為單位）。

* `secondarySubPath`

   與subPath類似，當 `secondaryProperty` 的子菜單。

在大多數情況下， `property` 的下界。

### 客戶端篩選器 {#client-filter}

客戶機過濾器從伺服器返回的資料中提取要顯示的資訊。

>[!NOTE]
>
>在應用整個伺服器端處理之後，將執行此篩選器。

```xml
N:definitions
    N:data
        P:clientFilter [String]
```

`clientFilter` 定義為JavaScript函式，該函式：

* 作為輸入，接收一個參數；從伺服器返回的資料（因此已完全預處理）
* 作為輸出，返回篩選（處理）的值；從輸入資訊中提取或導出的資料

下面的示例從元件路徑中提取相應的頁路徑：

```
function(v) {
    var sepPos = v.lastIndexOf('/jcr:content');
    if (sepPos < 0) {
        return v;
    }
    return v.substring(sepPos + '/jcr:content'.length, v.length);
}
```

### 解析器和預處理 {#resolvers-and-preprocessing}

的 [處理隊列](#processing-queue) 定義各種解析器並配置預處理：

```xml
N:definitions
    N:data
        P:resolver
        N:resolverConfig
        N:preprocessing
            N:apply
            N:applyAfter
```

* `resolver`

   定義要使用的解析器。 以下解析器可用：

   * `const`

      將值映射到其他值；例如，它用於解析常數，如 `en` 其等價值 `English`。

   * `default`

      預設解析程式。 這是一個虛擬的解析器，它實際上不解決任何問題。

   * `page`

      將路徑值解析為相應頁的路徑；更準確地說，是 `jcr:content` 的下界。 比如說， `/content/.../page/jcr:content/par/xyz` 已決定 `/content/.../page/jcr:content`。

   * `path`

      通過可選地附加子路徑並從節點的屬性中取實際值(如由 `resolverConfig`)。 例如， `path` 共 `/content/.../page/jcr:content` 可以解析為 `jcr:title` 屬性，這表示頁面路徑解析為頁面標題。

   * `pathextension`

      通過預掛起路徑並從解析路徑上的節點屬性中獲取實際值來解析值。 例如， `de` 可能由如 `/libs/wcm/core/resources/languages`，從屬性中取值 `language`，以解析國家/地區代碼 `de` 到語言說明 `German`。

* `resolverConfig`

   提供解析程式的定義；可用選項取決於 `resolver` 選定：

   * `const`

      使用屬性指定要解析的常數。 屬性名稱定義要解析的常數；屬性值定義解析的值。

      例如，具有 **名稱**= `1` 和 **值** `=One` 1比1。

   * `default`

      沒有可用的配置。

   * `page`

      * `propertyName` (可選)

         定義應用於解析值的屬性的名稱。 如果未指定，則預設值為 *jcr：標題* （頁面標題）;為 `page` 解析器，這意味著首先將路徑解析為頁面路徑，然後進一步解析為頁面標題。
   * `path`

      * `propertyName` (可選)

         指定應用於解析值的屬性的名稱。 如果未指定，則預設值為 `jcr:title` 的子菜單。

      * `subPath` (可選)

         此屬性可用於指定在解析值之前附加到路徑的尾碼。
   * `pathextension`

      * `path` （強制）

         定義要優先的路徑。

      * `propertyName` （強制）

         定義實際值所在的已解析路徑上的屬性。

      * `i18n` （可選）類型布爾值)

         確定是否應將解析的值 *國際化* (即使用 [CQ5的國際化服務](/help/sites-administering/tc-manage.md))。



* `preprocessing`

   預處理是可選的，可以（單獨）綁定到處理階段 *應用* 或 *應用後*:

   * `apply`

      初始預處理階段([步驟3表示處理隊列](#processing-queue))。

   * `applyAfter`

      預處理後應用([步驟9表示處理隊列](#processing-queue))。

#### 解析器 {#resolvers}

解析器用於提取所需資訊。 各種解決方案的示例有：

**孔斯特**

以下將解析的常數值 `VersionCreated` 到字串 `New version created`。

請參閱 `/libs/cq/reporting/components/auditreport/typecol/definitions/data`.

```xml
N:data
    P:resolver=const
    N:resolverConfig
        P:VersionCreated="New version created"
```

**Page**

將路徑值解析為相應頁的jcr:content(child)節點上的jcr:description屬性。

請參閱 `/libs/cq/reporting/components/compreport/pagecol/definitions/data`.

```xml
N:data
    P:resolver=page
    N:resolverConfig
        P:propertyName="jcr:description"
```

**路徑**

下面將解析 `/content/.../page` 內容 `jcr:title` 屬性，這表示頁面路徑解析為頁面標題。

請參閱 `/libs/cq/reporting/components/auditreport/pagecol/definitions/data`.

```xml
N:data
    P:resolver=path
    N:resolverConfig
        P:propertyName="jcr:title"
        P:subPath="/jcr:content"
```

**路徑擴展**

以下項會預留一個值 `de` 路徑擴展 `/libs/wcm/core/resources/languages`，然後從屬性中獲取值 `language`，以解析國家/地區代碼 `de` 到語言說明 `German`。

請參閱 `/libs/cq/reporting/components/userreport/languagecol/definitions/data`.

```xml
N:data
    P:resolver=pathextension
    N:resolverConfig
        P:path="/libs/wcm/core/resources/languages"
        P:propertyName="language"
```

#### 預處理 {#preprocessing}

的 `preprocessing` 定義可應用於以下任一項：

* 原始值：

   原始值的預處理定義在 `apply` 和/或 `applyAfter` 直接輸入。

* 值：

   如有必要，可為每個聚合提供單獨的定義。

   要指定聚合值的顯式預處理，預處理定義必須駐留在相應的上 `aggregated` 子節點( `apply/aggregated`。 `applyAfter/aggregated`)。 如果需要對不同聚合進行顯式預處理，則預處理定義位於具有相應聚合名稱的子節點上(例如 `apply/aggregated/min/max` 或其他聚合)。

您可以指定預處理期間使用的以下任一項：

* [查找和替換模式](#preprocessing-find-and-replace-patterns)
當找到時，指定的模式（定義為規則運算式）將被另一個模式替換；例如，可以使用它提取原文的子字串。

* [資料類型格式化程式](#preprocessing-data-type-formatters)

   將數字值轉換為相對字串；例如，表示1小時時差的值「」將解析為字串，如 `1:24PM (1 hour ago)`。

例如：

```xml
N:definitions
    N:data
        N:preprocessing
            N:apply|applyAfter
                P:pattern         // regex
                P:replace         // replacement for regex
                // and/or
                P:format          // data type formatter
```

#### 預處理 — 查找和替換模式 {#preprocessing-find-and-replace-patterns}

對於預處理，可以指定 `pattern` (定義為 [規則運算式](https://en.wikipedia.org/wiki/Regular_expression) 或regex)的 `replace` 模式：

* `pattern`

   用於定位子字串的規則運算式。

* `replace`

   將用作原始字串的替換項的字串或字串的表示形式。 這通常表示規則運算式所定位的字串的子字串 `pattern`。

示例替換可分為：

* 對於節點 `definitions/data/preprocessing/apply` 具有以下兩個屬性：

   * `pattern`: `(.*)(/jcr:content)(/|$)(.*)`
   * `replace`: `$1`

* 字串到達時為：

   * `/content/geometrixx/en/services/jcr:content/par/text`

* 將分為四部分：

   * `$1` - `(.*)` - `/content/geometrixx/en/services`
   * `$2` - `(/jcr:content)` - `/jcr:content`
   * `$3` - `(/|$)` - `/`
   * `$4` - `(.*)` - `par/text`

* 並替換為由 `$1`:

   * `/content/geometrixx/en/services`

#### 預處理 — 資料類型格式化程式 {#preprocessing-data-type-formatters}

這些格式化程式將數值轉換為相對字串。

例如，此選項可用於允許 `min`。 `avg` 和 `max` 聚合。 作為 `min`/ `avg`/ `max` 聚合顯示為 *時差* (例如 `10 days ago`)，它們需要資料格式化程式。 為此， `datedelta` 格式化程式應用於 `min`/ `avg`/ `max` 聚合值。 如果 `count` 聚合也可用，因此它不需要格式化程式，原始值也不需要。

當前可用的資料類型格式化程式有：

* `format`

   資料類型格式化程式：

   * `duration`

      持續時間是兩個定義日期之間的時間跨度。 例如，工作流操作的開始和結束時間為1小時，從2/13/11 11:23h開始，到1小時後2/13/11 12:23h結束。

      它將數值（解釋為毫秒）轉換為持續時間字串；比如說， `30000` 格式為* `30s`.*

   * `datedelta`

      Datadelta是過去某個日期到「現在」之間的時間跨度（因此，如果在稍後的時間點查看報告，則會產生不同的結果）。

      它將數字值（解釋為以天為單位的時差）轉換為相對日期字串。 例如，1的格式是1天前。

以下示例定義 `datedelta` 格式 `min` 和 `max` 聚合：

```xml
N:definitions
    N:data
        N:preprocessing
            N:apply
                N:aggregated
                    N:min
                        P:format = "datedelta"
                    N:max
                        P:format = "datedelta"
```

### 列特定定義 {#column-specific-definitions}

特定於列的定義定義可用於該列的篩選器和聚合。

```xml
N:definitions
    P:type
    P:groupable [Boolean]
    N:filters [cq:WidgetCollection]
    [
        N:<name> // array of nodes (names irrelevant) with the following properties:
            P:filterType
            P:id
            P:phase
    ]
    N:aggregates [cq:WidgetCollection]
    [
        N:<name> // array of nodes (names irrelevant) with the following properties:
            P:text
            P:type
    ]
```

* `type`

   以下是標準選項：

   * `string`
   * `number`
   * `int`
   * `date`
   * `diff`
   * `timeslot`

      用於提取聚合所需日期的部分（例如，按年分組以獲取每年的聚合資料）。

   * `sortable`

      用於使用不同值（如從不同屬性中取得）進行排序和顯示的值。
   另外， 以上任何一項都可以定義為多值；比如說， `string[]` 定義字串陣列。

   值提取器由列類型選擇。 如果值提取器可用於列類型，則使用此提取器。 否則，使用預設值提取器。

   類型可（可選）採用參數。 比如說， `timeslot:year` 從日期欄位提取年份。 類型及其參數：

   * `timeslot`  — 該值可與Contern Contrants `java.utils.Calendar`。

      * `timeslot:year` - `Calendar.YEAR`
      * `timeslot:month-of-year` - `Calendar.MONTH`
      * `timeslot:week-of-year` - `Calendar.WEEK_OF_YEAR`
      * `timeslot:day-of-month` - `Calendar.DAY_OF_MONTH`
      * `timeslot:day-of-week` - `Calendar.DAY_OF_WEEK`
      * `timeslot:day-of-year` - `Calendar.DAY_OF_YEAR`
      * `timeslot:hour-of-day` - `Calendar.HOUR_OF_DAY`
      * `timeslot:minute-of-hour` - `Calendar.MINUTE`


* `groupable`

   定義是否可以按此列對報表進行分組。

* `filters`

   篩選器定義。

   * `filterType`

      可用篩選器包括：

      * `string`

         基於字串的篩選器。
   * `id`

      篩選器標識符。

   * `phase`

      可用階段：

      * `raw`

         篩選器應用於原始資料。

      * `preprocessed`

         對預處理的資料應用篩選器。

      * `resolved`

         篩選器應用於已解析的資料。


* `aggregates`

   聚合定義。

   * `text`

      聚合的文本名稱。 如果 `text` 未指定，則將採用聚合的預設描述；比如說， `minimum` 將用於 `min` 集合。

   * `type`

      聚合類型。 可用聚合包括：

      * `count`

         計算行數。

      * `count-nonempty`

         計算非空行數。

      * `min`

         提供最小值。

      * `max`

         提供最大值。

      * `average`

         提供平均值。

      * `sum`

         提供所有值的總和。

      * `median`

         提供中值。

      * `percentile95`

         取所有值的第95百分位。

### 列預設值 {#column-default-values}

這用於定義列的預設值：

```xml
N:defaults
    P:aggregate
```

* `aggregate`

   有效 `aggregate` 值與 `type` 在 `aggregates` （請參見） [列特定定義（定義 — 篩選器/聚合）](#column-specific-definitions) )。

### 事件和操作 {#events-and-actions}

「編輯配置」定義監聽程式檢測的必要事件以及這些事件發生後要應用的操作。 查看 [元件開發簡介](/help/sites-developing/components.md) 的子菜單。

必須定義以下值，以確保滿足所有所需操作：

```xml
N:cq:editConfig [cq:EditConfig]
    P:cq:actions [String[]] = "insert", "delete"
    P:cq:dialogMode = "floating"
    P:cq:layout = "auto"
    N:cq:listeners [cq:EditListenersConfig]
        P:aftercreate = "REFRESH_INSERTED"
        P:afterdelete = "REFRESH_SELF"
        P:afteredit = "REFRESH_SELF"
        P:afterinsert = "REFRESH_INSERTED"
        P:aftermove = "REFRESH_SELF"
        P:afterremove = "REFRESH_SELF"
```

### 一般列 {#generic-columns}

泛型列是擴展，其中（大多數）列定義儲存在列節點的實例（而不是元件節點）上。

它們使用（標準）對話框，您可以為單個類屬元件定制該對話框。 此對話框允許報表用戶在報表頁上定義泛型列的列屬性（使用菜單選項） **列屬性……**)。

例如 **泛型** 列 **用戶報告**;見 `/libs/cq/reporting/components/userreport/genericcol`。

要使列為泛型：

* 設定 `type` 列的屬性 `definition` 節點到 `generic`。

   請參閱 `/libs/cq/reporting/components/userreport/genericcol/definitions`

* 在列的 `definition` 的下界。

   請參閱 `/libs/cq/reporting/components/userreport/genericcol/definitions/dialog`

   * 對話框的欄位必須引用與相應元件屬性（包括其路徑）相同的名稱。

      例如，如果要通過對話框使泛型列的類型可配置，請使用名稱為 `./definitions/type`。

   * 使用UI/對話框定義的屬性優先於在 `columnbase` 元件。

* 定義編輯配置。

   請參閱 `/libs/cq/reporting/components/userreport/genericcol/cq:editConfig`

* 使用標AEM準方法定義（附加）列屬性。

   請注意，對於在元件實例和列實例上都定義的屬性，列實例上的值優先。

   泛型列可用的屬性包括：

   * `jcr:title`  — 列名稱
   * `definitions/aggregates`  — 聚合
   * `definitions/filters`  — 篩選器
   * `definitions/type` — 列的類型（必須在對話框中定義，使用選擇器/組合框或隱藏欄位）
   * `definitions/data/resolver` 和 `definitions/data/resolverConfig` （但不） `definitions/data/preprocessing` 或 `.../clientFilter`) — 解析程式和配置
   * `definitions/queryBuilder`  — 查詢生成器配置
   * `defaults/aggregate`  — 預設聚合

   在上的泛型列的新實例中 **用戶報告** 使用對話框定義的屬性保留在以下位置：

   `/etc/reports/userreport/jcr:content/report/columns/genericcol/settings/generic`

## 報表設計 {#report-design}

設計定義了哪些列類型可用於建立報告。 它還定義了添加列的段落系統。

強烈建議您為每個報告建立單個設計。 這確保了完全的靈活性。 另請參閱 [定義新報表](#defining-your-new-report)。

預設報告元件保存於 `/etc/designs/reports`。

報告的位置可取決於元件所在的位置：

* `/etc/designs/reports/<yourReport>` 如果報告位置偏離 `/apps/cq/reporting`

* `/etc/designs/<yourProject>/reports/<*yourReport*>` 對於使用 `/apps/<yourProject>/reports` 圖案

在上註冊所需的設計屬性 `jcr:content/reportpage/report/columns` (例如， `/etc/designs/reports/<reportName>/jcr:content/reportpage/report/columns`):

* `components`

   報告中允許的任何元件和/或元件組。

* `sling:resourceType`

   具有值的屬性 `cq/reporting/components/repparsys`。

示例設計代碼段（取自元件報告的設計）為：

```xml
<!-- ... -->
    <jcr:content
        jcr:primaryType="nt:unstructured"
        jcr:title="Component Report"
        sling:resourceType="wcm/core/components/designer">
        <reportpage jcr:primaryType="nt:unstructured">
            <report jcr:primaryType="nt:unstructured">
                <columns
                    jcr:primaryType="nt:unstructured"
                    sling:resourceType="cq/reporting/components/repparsys"
                    components="group:Component Report"/>
            </report>
        </reportpage>
    </jcr:content>
<!-- ... -->
```

不需要為各個列指定設計。 可在設計模式下定義可用列。

>[!NOTE]
>
>建議不要對標準報告設計進行任何更改。 這是為了確保在升級或安裝修補程式時不會丟失任何更改。
>
>如果要自定義標準報表，請複製報表及其設計。

>[!NOTE]
>
>在建立報表時，可以自動建立預設列。 這些是在模板中指定的。

## 報表模板 {#report-template}

每個報告類型都必須提供模板。 這些是標準 [CQ模板](/help/sites-developing/templates.md) 可以這樣配置。

模板必須：

* 設定 `sling:resourceType` 至 `cq/reporting/components/reportpage`

* 指示要使用的設計
* 建立 `report` 引用容器的子節點( `reportbase`)元件 `sling:resourceType` 屬性

示例模板段（取自元件報告模板）為：

```xml
<!-- ... -->
    <jcr:content
        cq:designPath="/etc/designs/reports/compreport"
        jcr:primaryType="cq:PageContent"
        sling:resourceType="cq/reporting/components/reportpage">
        <report
            jcr:primaryType="nt:unstructured"
            sling:resourceType="cq/reporting/components/compreport/compreport"/>
    </jcr:content>
<!-- .. -->
```

顯示根路徑（取自用戶報告模板）定義的示例模板片段是：

```xml
<!-- ... -->
    <jcr:content
        cq:designPath="/etc/designs/reports/userreport"
        jcr:primaryType="cq:PageContent"
        sling:resourceType="cq/reporting/components/reportpage">
        <report
            jcr:primaryType="nt:unstructured"
            rootPath="/home/users"
            sling:resourceType="cq/reporting/components/compreport/compreport"/>
    </jcr:content>
<!-- .. -->
```

預設報告模板保存在 `/libs/cq/reporting/templates`。

但是，強烈建議您不要更新這些節點，而是在以下位置建立自己的元件節點 `/apps/cq/reporting/templates` 或者如果合適 `/apps/<yourProject>/reports/templates`。

其中，作為示例(另請參見 [報表元件的位置](#location-of-report-components)):

```xml
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
```

在此下，您為模板建立根：

```xml
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
                N:<reportname> [sling:Folder]
```

## 建立您自己的報告 — 示例 {#creating-your-own-report-an-example}

### 定義新報表 {#defining-your-new-report}

要定義新報告，必須建立和配置：

1. 報表元件的根。
1. 報表基元件。
1. 一個或多個列基元件。
1. 報告設計。
1. 報表模板的根。
1. 報表模板。

為了說明這些步驟，以下示例定義了一個報告，其中列出了儲存庫中的所有OSGi配置；即所有 `sling:OsgiConfig` 的下界。

>[!NOTE]
>
>複製現有報告，然後自定義新版本是一種替代方法。

1. 為新報表建立根節點。

   例如，在 `/apps/cq/reporting/components/osgireport`。

   ```xml
   N:cq [nt:folder]
       N:reporting [sling:Folder]
           N:components [sling:Folder]
               N:osgireport [sling:Folder]
   ```

1. 定義報表庫。 例如 `osgireport[cq:Component]` 在 `/apps/cq/reporting/components/osgireport`。

   ```xml
   N:osgireport [sling:Folder]
       N:osgireport [cq:Component]
           P:sling:resourceSuperType [String] = "cq/reporting/components/reportbase"
           N:charting [nt:unstructured]
               N:settings [nt:unstructured]
                   N:active [cq:WidgetCollection]
                       N:0 [nt:unstructured]
                           P:id [String] = "pie"
                       N:1 [nt:unstructured]
                           P:id [String] = "lineseries"
               N:definitions [cq:WidgetCollections]
                   N:0 [nt:unstructured]
                       P:id [String] = "pie"
                       P:maxRadius [Long] = 180
                       P:type [String] = "pie"
                   N:1 [nt:unstructured]
                       P:id [String] = "lineseries"
                       P:type [String] = "lineseries"
           N:dialog [cq:Dialog]
               P:height [Long] = 424
               N:items [cq:WidgetCollection]
                   N:props [cq:Panel]
                       N:items [cq:WidgetCollection]
                           N:title [cq:Widget]
                               P:path [String] = "/libs/cq/reporting/components/commons/title.infinity.json"
                               P:xtype [String] = "cqinclude"
                           N:description [cq:Widget]
                               P:path [String] = "/libs/cq/reporting/components/commons/description.infinity.json"
                               P:xtype [String] = "cqinclude"
                           N:rootPath [cq:Widget]
                               P:fieldLabel [String] = "Root path"
                               P:name [String] = "./report/rootPath"
                               P:xtype [String] = "pathfield"
                           N:processing [cq:Widget]
                               P:path [String] = "/libs/cq/reporting/components/commons/processing.infinity.json"
                               P:xtype [String] = "cqinclude"
                           N:scheduling [cq:Widget]
                               P:path [String] = "/libs/cq/reporting/components/commons/scheduling.infinity.json"
                               P:xtype [String] = "cqinclude"
           N:queryBuilder [nt:unstructured]
               P:nodeTypes [String[]] = "sling:OsgiConfig"
   ```

   這定義了一個報表基元件，它：

   * 搜索所有類型的節點 `sling:OsgiConfig`
   * 顯示 `pie` 和 `lineseries` 圖表
   * 為用戶提供了配置報告的對話框

1. 定義第一列（列基）元件。 例如 `bundlecol[cq:Component]` 在 `/apps/cq/reporting/components/osgireport`。

   ```xml
   N:osgireport [sling:Folder]
       N:bundlecol [cq:Component]
           P:componentGroup [String] = "OSGi Report"
           P:jcr:title = "Bundle"
           P:sling:resourceSuperType [String] = "cq/reporting/components/columnbase"
           N:cq:editConfig [cq:EditConfig]
               P:cq:actions [String[]] = "insert", "delete"
               P:cq:dialogMode [String] = "floating"
               P:cq:layout [String] = "auto"
               N:cq:listeners [cq:EditListenersConfig]
                   P:aftercreate [String] "REFRESH_INSERTED"
                   P:afterdelete [String] "REFRESH_SELF"
                   P:afteredit [String] "REFRESH_SELF"
                   P:afterinsert [String] "REFRESH_INSERTED"
                   P:aftermove [String] "REFRESH_SELF"
                   P:afterremove [String] "REFRESH_SELF"
           N:defaults [nt:unstructured]
               P:aggregate [String] = "count"
           N:definitions [nt:unstructured]
               P:groupable [Boolean] = false
               P:type [String] = "string"
               N:queryBuilder [nt:unstructured]
                   P:property [String] = "jcr:path"
   ```

   這定義了列基元件，該元件：

   * 搜索並返回從伺服器接收的值；在這種情況下，該屬性 `jcr:path` 每 `sling:OsgiConfig` 節點
   * 提供 `count` 集合
   * 不可分組
   * 有標題 `Bundle` （表中的列標題）
   * 在旁邊隊 `OSGi Report`
   * 刷新指定的事件

   >[!NOTE]
   >
   >在本示例中，沒有 `N:data` 和 `P:clientFilter`。 這是因為從伺服器收到的值是按1:1返回的 — 這是預設行為。
   >
   >這與定義相同：
   >
   >
   ```
   >N:data [nt:unstructured]
   >   P:clientFilter [String] = "function(v) { return v; }"
   >```
   >
   >其中，函式只返回其接收的值。

1. 定義報表設計。 例如 `osgireport[cq:Page]` 在 `/etc/designs/reports`。

   ```xml
   N:osgireport [cq:Page]
       N:jcr:content [nt:unstructured]
           P:jcr:title [String] = "OSGi report"
           P:sling:resourceType [String] = "wcm/core/components/designer"
           N:reportpage [nt:unstructured]
               N:report [nt:unstructured]
                   N:columns [nt:unstructured]
                       P:components [String] = "group:OSGi Report"
                       P:sling:resourceType [String] = "cq/reporting/components/repparsys"
   ```

1. 為新報表模板建立根節點。

   例如，在 `/apps/cq/reporting/templates/osgireport`。

   ```xml
   N:cq [nt:folder]
       N:reporting [sling:Folder]
           N:templates [sling:Folder]
               N:osgireport [cq:Template]
   ```

1. 定義報表模板。 例如 `osgireport[cq:Template]` 在 `/apps/cq/reporting/templates`。

   ```xml
   N:osgireport [cq:Template]
       P:allowedPaths [String[]] = "/etc/reports(/.*)?"
       P:jcr:description [String] = "Use this report generator to create a new OSGi report."
       P:jcr:title [String] = "OSGi Report Template"
       P:ranking [Long] = 100
       P:shortTitle [String] = "OSGi Report"
       N:jcr:content [cq:PageContent]
           P:cq:designPath [String] = "/etc/designs/reports/osgireport"
           P:sling:resourceType [String] = "cq/reporting/components/reportpage"
           N:report [nt:unstructured]
               P:rootPath [String] = "/"
               P:sling:resourceType [String] = "cq/reporting/components/osgireport/osgireport"
       N:thumbnail.png [nt:file]
   ```

   這定義了一個模板：

   * 定義 `allowedPaths` 對於結果報告 — 在上例中，位於 `/etc/reports`
   * 提供模板的標題和說明
   * 提供在模板清單中使用的縮略圖（上面未列出此節點的完整定義 — 最容易從現有報告中複製thumbnail.png實例）。

### 建立新報表的實例 {#creating-an-instance-of-your-new-report}

現在可以建立新報告的實例：

1. 開啟 **工具** 控制台。

1. 選擇 **報告** 的下界。
1. 然後 **新建……** 的子菜單。 定義 **標題** 和 **名稱**，選擇新報告類型( **OSGi報表模板**)，然後按一下 **建立**。
1. 您的新報告實例將出現在清單中。 按兩下此按鈕以開啟。
1. 拖動元件(對於此示例， **捆綁** 的 **OSGi報告** 組)以建立第一列和 [啟動報表定義](/help/sites-administering/reporting.md#the-basics-of-report-customization)。

   >[!NOTE]
   >
   >由於此示例沒有任何可分組的列，因此圖表將不可用。 要查看圖表，請設定 `groupable` 至 `true`:
   >
   >
   ```
   >N:osgireport [sling:Folder]
   > N:bundlecol [cq:Component]
   > N:definitions [nt:unstructured]
   > P:groupable [Boolean] = true
   >```

## 配置Report Framework服務 {#configuring-the-report-framework-services}

本節介紹用於實現報告框架的OSGi服務的高級配置選項。

可使用Web控制台的「配置」菜單查看這些內容(例如， `http://localhost:4502/system/console/configMgr`)。 使用時，AEM有幾種方法管理此類服務的配置設定；見 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 的子菜單。

### 基本服務（第CQ天報告配置） {#basic-service-day-cq-reporting-configuration}

* **時區** 定義為建立的時區歷史資料。 這是為了確保歷史圖表顯示全球每個用戶的相同資料。
* **區域設定** 定義要與 **時區** 歷史資料。 區域設定用於確定某些特定於區域設定的日曆設定（例如，一週的第一天是星期日還是星期一）。

* **快照路徑** 定義儲存歷史圖表快照的根路徑。
* **報告路徑** 定義報告所在的路徑。 快照服務使用此功能來確定要實際為其拍攝快照的報告。
* **每日快照** 定義每天拍攝快照的小時數。 指定的小時在伺服器的本地時區。
* **每小時快照** 定義拍攝每小時快照時的分鐘數。
* **行（最大）** 定義為每個快照儲存的最大行數。 應合理選擇該值；如果太高，則會影響儲存庫的大小，如果太低，則資料可能不準確，因為歷史資料的處理方式。
* **假資料**，如果啟用，則可以使用 `fakedata` 選擇器；如果禁用，則使用 `fakedata` 選擇器將引發異常。

   因為資料是假的，所以 *僅* 用於測試和調試。

   使用 `fakedata` selector將隱式完成報告，因此所有現有資料都將丟失；資料可以手動恢復，但這可能是一個耗時的過程。

* **快照用戶** 定義可用於拍攝快照的可選用戶。

   基本上，為完成報告的用戶拍攝快照。 可能存在您希望指定備用用戶的情況（例如，在發佈系統上，此用戶不存在，因為其帳戶尚未複製）。

   此外，指定用戶可能會帶來安全風險。

* **強制快照用戶**，如果啟用，則所有快照都將使用在下指定的用戶拍攝 *快照用戶*。 如果處理不正確，可能會對安全造成嚴重影響。

### 快取設定（第CQ天報告快取） {#cache-settings-day-cq-reporting-cache}

* **啟用** 允許您啟用或禁用報表資料的快取。 啟用報告快取將在多個請求期間將報告資料保留在記憶體中。 這可能會提高效能，但會導致記憶體消耗增加，在極端情況下可能導致記憶體不足。
* **TTL** 定義快取報告資料的時間（秒）。 數量越高，效能越好，但如果資料在時間段內發生更改，也可能返回不準確的資料。
* **最大條目數** 定義每次要快取的報告的最大數量。

>[!NOTE]
>
>每個用戶和語言的報告資料可能不同。 因此，按報告、用戶和語言快取報告資料。 這意味著 **最大條目數** 值 `2` 實際快取資料：
>
>* 兩個具有不同語言設定的用戶的一個報告
>* 一個用戶和兩個報告
>

