---
title: 開發報表
seo-title: 開發報表
description: AEM提供以報表架構為基礎的標準報表選項
seo-description: AEM提供以報表架構為基礎的標準報表選項
uuid: 1b406d15-bd77-4531-84c0-377dbff5cab2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 50fafc64-d462-4386-93af-ce360588d294
exl-id: 3891150e-9972-4bbc-ad61-7f46a1f9bbb4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '5252'
ht-degree: 0%

---

# 開發報表{#developing-reports}

AEM提供選取[標準報表](/help/sites-administering/reporting.md)的選項，其中大部分是以報表架構為基礎。

使用架構，您可以擴充這些標準報表，或開發您自己的全新報表。 報表架構與現有CQ5概念和原則緊密整合，讓開發人員可以將其現有的CQ5知識作為開發報表的跳板。

對於隨AEM傳送的標準報表：

* 這些報表是在報表架構上建置：

   * [元件報表](/help/sites-administering/reporting.md#component-report)
   * [頁面活動報表](/help/sites-administering/reporting.md#page-activity-report)
   * [使用者報表](/help/sites-administering/reporting.md#user-report)
   * [工作流程例項報表](/help/sites-administering/reporting.md#workflow-instance-report)

* 下列報告以個別原則為基礎，因此無法延伸：

   * [磁碟使用情況](/help/sites-administering/reporting.md#disk-usage)
   * [運行狀況檢查](/help/sites-administering/reporting.md#health-check)
   * [工作流程報表](/help/sites-administering/reporting.md#workflow-report)

>[!NOTE]
>
>教學課程[建立您自己的報表 — 範例](#creating-your-own-report-an-example)也顯示可使用下列原則的數量。
>
>您也可以參考標準報表，以查看其他實作範例。

>[!NOTE]
>
>在下列範例和定義中，會使用下列標籤法：
>
>* 每行定義一個節點或一個屬性，其中：
   >
   >  
* `N:<name> [<nodeType>]`
   >
   >     
   描述名稱為`<*name*>`且節點類型為&#x200B;`<*nodeType*>`*的節點。*
   >
   >  
* `P:<name> [<propertyType]`
   >
   >     
   描述名稱為`<*name*>`的屬性和屬性類型為`<*propertyType*>`的屬性。
   >
   >  
* `P:<name> = <value>`
   >
   >     
   描述必須設定為`<value>`值的屬性`<name>`。
   >
   >
* 縮進顯示節點之間的分層依賴關係。
>* 以分隔的項目 |表示可能的項目清單；例如，類型或名稱：

>
>  
例如`String|String[]`表示屬性可以是String或String[]。
>
>* `[]` 描述陣列；例如[] 字串或查詢定義中的節 [點陣列](#query-definition)。
>
>
除非另有說明，否則預設類型為：
>
>* 節點 — `nt:unstructured`
>* 屬性 - `String`


## 報告框架{#reporting-framework}

報告框架遵循下列原則：

* 它完全以CQ5 QueryBuilder執行的查詢所傳回的結果集為基礎。
* 結果集定義報表中顯示的資料。 結果集中的每一列都對應於報表表格檢視中的一列。
* 可在結果集上執行的操作類似於RDBMS概念；主要是&#x200B;*分組*&#x200B;和&#x200B;*聚合*。

* 大多數資料檢索和處理都是在伺服器端完成的。
* 用戶端需自行負責顯示預先處理的資料。 只有次要的處理工作（例如在儲存格內容中建立連結）會在用戶端執行。

報表架構（由標準報表的結構圖示）使用下列建置區塊，由處理佇列饋送：

![chlimage_1-248](assets/chlimage_1-248.png)

### 報表頁面{#report-page}

報表頁面：

* 是標準CQ5頁面。
* 是以[標準CQ5範本為基礎，並針對報表](#report-template)進行設定。

### 報表庫{#report-base}

[ `reportbase`元件](#report-base-component)構成任何報表的基礎，如下所示：

* 保留[query](#the-query-and-data-retrieval)的定義，該定義提供基礎的資料結果集。

* 是經過調整的段落系統，將包含新增到報表的所有列(`columnbase`)。
* 定義可用的圖表類型和當前活動的圖表類型。
* 定義編輯對話方塊，讓使用者設定報表的某些方面。

### 列基{#column-base}

每列都是[ `columnbase`元件](#column-base-component)的實例，其中：

* 是段落，由個別報表的parsys(`reportbase`)使用。
* 定義指向[基礎結果集](#the-query-and-data-retrieval)的連結；即定義此結果集中引用的特定資料及其處理方式。
* 保留其他定義；例如可用的匯總和篩選，以及任何預設值。

### 查詢與資料檢索{#the-query-and-data-retrieval}

查詢：

* 定義為[ `reportbase`](#report-base)元件的一部分。
* 是以[CQ QueryBuilder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html)為基礎。
* 擷取用作報表基礎的資料。 結果集（表）的每一行都與查詢返回的節點綁定。 然後，從此資料集中提取[個別欄](#column-base-component)的特定資訊。

* 通常包含：

   * 根路徑。

      這會指定要搜索的儲存庫的子樹。

      為了有助於將效能影響降至最低，建議（嘗試）將查詢限制在儲存庫的特定子樹。 根路徑可在[報表範本](#report-template)中預先定義，或由使用者在[設定（編輯）對話方塊](#configuration-dialog)中設定。

   * [一或多個條件](#query-definition)。

      這些規定是為了產生（初始）結果集；例如，節點類型限制或屬性限制。

**這裡的關鍵點是，查詢結果集中返回的每個單一節點都用於在報表上產生單一列（因此為1:1關係）。**

開發人員必須確保為報表定義的查詢會傳回適用於該報表的節點集。 但是，節點本身並不需要保留所有所需資訊，這也可以從父節點和/或子節點派生。 例如，用於[用戶報告](/help/sites-administering/reporting.md#user-report)的查詢根據節點類型（在本例中為`rep:user`）選擇節點。 但是，此報告中的大多數列不直接從這些節點獲取其資料，而是從子節點`profile`獲取資料。

### 處理佇列{#processing-queue}

[query](#the-query-and-data-retrieval)會傳回要在報表上顯示為列的資料結果集。 在將結果集中的每一行（伺服器端）在[幾個階段](#phases-of-the-processing-queue)中進行處理，然後轉送到客戶端以顯示在報告上。

這允許：

* 從基礎結果集中提取和導出值。

   例如，它可讓您透過計算兩個屬性值之間的差異，將兩個屬性值視為單一值處理。

* 解析提取的值；這可以以多種方式完成。

   例如，路徑可對應至標題（如個別&#x200B;*jcr:title*&#x200B;屬性中較人類看得懂的內容）。

* 在不同點套用篩選。
* 視需要建立複合值。

   例如，由顯示給使用者的文字、要用於排序的值，以及用於建立連結的其他URL組成（在用戶端上）。

#### 處理佇列{#workflow-of-the-processing-queue}的工作流程

下列工作流程代表處理佇列：

![chlimage_1-249](assets/chlimage_1-249.png)

#### 處理佇列的階段{#phases-of-the-processing-queue}

其中詳細步驟和元素包括：

1. 使用值擷取器將[初始查詢(reportbase)](#query-definition)傳回的結果轉換為基本結果集。

   根據[列類型](#column-specific-definitions)自動選擇值提取器。 它們用於從基礎JCR查詢中讀取值，並從中建立結果集；之後，可以應用進一步處理。 例如，對於`diff`類型，值提取器讀取兩個屬性，計算單個值，然後將其添加到結果集中。 無法配置值提取器。

1. 對包含原始資料的初始結果集應用[初始過濾](#column-specific-definitions)（*raw*&#x200B;階段）。

1. 值為[preprocessed](#processing-queue);為&#x200B;*apply*&#x200B;階段定義。

1. [篩選](#column-specific-definitions) (指派給預 ** 處理階段)會對預處理的值執行。

1. 值會解析；根據[定義的resolver](#processing-queue)。
1. [篩選](#column-specific-definitions) (指派給解 ** 析階段)會對解析的值執行。

1. 資料是[分組並匯總](#column-specific-definitions)。
1. 將陣列資料轉換為（字串型）清單，即可加以解析。

   這是將多值結果轉換為可顯示的清單的隱式步驟；根據多值JCR屬性的儲存格值需要此變數。

1. 值會再次[預先處理](#processing-queue);為&#x200B;*afterApply*&#x200B;階段定義。

1. 資料已排序。
1. 處理的資料被傳輸到客戶機。

>[!NOTE]
>
>在`reportbase`元件上定義返回基本資料結果集的初始查詢。
>
>處理佇列的其他元素是在`columnbase`元件上定義。

## 報告構建和配置{#report-construction-and-configuration}

建立和設定報表需要下列項目：

* a [報表元件定義的位置](#location-of-report-components)
* a [ `reportbase`元件](#report-base-component)
* 一個或多個[ `columnbase`元件](#column-base-component)
* a [頁面元件](#page-component)
* a [報表設計](#report-design)
* a [報表範本](#report-template)

### 報表元件的位置{#location-of-report-components}

預設報告元件保存在`/libs/cq/reporting/components`下。

不過，強烈建議您不要更新這些節點，而是在`/apps/cq/reporting/components`下或更適當的`/apps/<yourProject>/reports/components`下建立自己的元件節點。

其中（例如）:

```
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:components [sling:Folder]
```

在此下，您可建立報表的根，在此下，報表基元件和欄基元件：

```
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:components [sling:Folder]
                N:<reportname> [sling:Folder]
                        N:<reportname> [cq:Component]  // report base component
                        N:<columnname> [cq:Component]  // column base component
```

### 頁面元件{#page-component}

報表頁面必須使用`/libs/cq/reporting/components/reportpage`的`sling:resourceType`。

自訂的頁面元件在大部分情況下不應是必要的。

## 報表基元件{#report-base-component}

每個報表類型都需要從`/libs/cq/reporting/components/reportbase`衍生的容器元件。

此元件可作為整個報表的容器，並提供下列資訊：

* [查詢定義](#query-definition)。
* 用於設定報表的[（選用）對話方塊](#configuration-dialog)。
* 報表中整合的任何[Charts](#chart-definitions)。

```
N:<reportname> [cq:Component]
    P:sling:resourceSuperType = "cq/reporting/components/reportbase"
    N:charting
    N:dialog [cq:Dialog]
    N:queryBuilder
```

### 查詢定義{#query-definition}

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

   可用於將結果集限制為具有特定屬性和特定值的節點。 如果指定了多個約束，則節點必須滿足所有約束（AND操作）。

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

   會傳回上次由`admin`使用者修改的所有`textimage`元件。

* `nodeTypes`

   用於將結果集限制為指定的節點類型。 可以指定多個節點類型。

* `mandatoryProperties`

   可用於將結果集限制為具有指定屬性&#x200B;*all*&#x200B;的節點。 屬性的值不會納入考量。

所有項目皆為選用項目，且可視需要加以組合，但您至少必須定義其中一個項目。

### 圖表定義{#chart-definitions}

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

   保留活動圖表的定義。

   * `active`

      由於可定義多個設定，因此您可以使用此設定來定義目前使用中的設定。 這些節點由一組節點定義(這些節點沒有強制命名約定，但標準報告通常使用`0`、`1`。 `x`)，每個都有下列屬性：

      * `id`

         活動圖表的標識。 這必須符合圖表`definitions`之一的id。

* `definitions`

   定義報表可能可用的圖表類型。 要使用的`definitions`將由`active`設定指定。

   定義是使用節點陣列指定的(通常名為`0`、`1`。 `x`)，且每個都具有下列屬性：

   * `id`

      圖表標識。

   * `type`

      可用圖表的類型。 選擇：

      * `pie`
圓形圖。僅從目前資料產生。

      * `lineseries`
一系列線（代表實際快照的連結點）。僅從歷史資料產生。
   * 其他屬性可用，取決於圖表類型：

      * 對於圖表類型`pie`:

         * `maxRadius` ( `Double/Long`)

            餅圖允許的最大半徑；因此，圖表允許的最大大小（無圖例）。 若已定義`fixedRadius`，則忽略。

         * `minRadius` ( `Double/Long`)

            餅圖允許的最小半徑。 若已定義`fixedRadius`，則忽略。

         * `fixedRadius` ( `Double/Long`)定義圓形圖的固定半徑。
      * 對於圖表類型[`lineseries`](/help/sites-administering/reporting.md#display-limits):

         * `totals` ( `Boolean`)

            如果應該顯示顯示&#x200B;**Total**的其他行，則為true。
預設: `false`

         * `series` ( `Long`)

            要顯示的行/系列數。
預設值：`9`（這也是允許的最大值）

         * `hoverLimit` ( `Long`)

            要為其顯示彈出窗口的聚合快照的最大數量（顯示在每條水準線上的點，表示不同值），即當用戶將滑鼠移到圖表圖例中的不同值或相應標籤上時。

            預設值：`35`（亦即，若目前圖表設定中有超過35個不同值，則完全不會顯示快顯視窗）。

            另外有10個快顯視窗的限制，可同時顯示（當將滑鼠移到圖例文字上時，可顯示多個快顯視窗）。



### 配置對話框{#configuration-dialog}

每個報表都可以有設定對話方塊，讓使用者可為報表指定各種參數。 開啟報表頁面時，可透過&#x200B;**Edit**&#x200B;按鈕存取此對話方塊。

此對話方塊是標準的CQ [dialog](/help/sites-developing/components-basics.md#dialogs)，可依此方式設定（如需詳細資訊，請參閱[CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog)）。

範例對話方塊如下所示：

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

提供數個預先設定的元件；在對話方塊中，使用`xtype`屬性並搭配值`cqinclude`可以參考下列項目：

* **`title`**

   `/libs/cq/reporting/components/commons/title`

   定義報表標題的文字欄位。

* **`description`**

   `/libs/cq/reporting/components/commons/description`

   文字區域以定義報表說明。

* **`processing`**

   `/libs/cq/reporting/components/commons/processing`

   報表處理模式的選取器（手動/自動載入資料）。

* **`scheduling`**

   `/libs/cq/reporting/components/commons/scheduling`

   用於為歷史圖表安排快照的選擇器。

>[!NOTE]
>
>必須使用`.infinity.json`尾碼包含引用的元件（請參閱上例）。

### 根路徑 {#root-path}

此外，還可為報表定義根路徑：

* **`rootPath`**

   這會將報表限制在存放庫的特定區段（樹狀或子樹狀），這是效能最佳化建議的報表。 根路徑由每個報告頁的`report`節點的`rootPath`屬性指定（建立頁面時從範本取用）。

   可由下列項目指定：

   * [報表範本](#report-template)（作為固定值或作為設定對話方塊的預設值）。
   * 使用者（使用此參數）

## 列基元件{#column-base-component}

每個列類型都需要從`/libs/cq/reporting/components/columnbase`派生的元件。

欄元件定義下列組合：

* [列特定查詢](#column-specific-query)配置。
* [解析器和預處理](#resolvers-and-preprocessing)。
* [欄特定定義](#column-specific-definitions)(例如篩選器和匯總；`definitions`子節點)。
* [欄預設值](#column-default-values)。
* [客戶端篩選器](#client-filter)從伺服器返回的資料中提取要顯示的資訊。
* 此外，列元件必須提供`cq:editConfig`的適當實例。 定義所需的[事件和動作](#events-and-actions)。
* [一般列](#generic-columns)的配置。

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

另請參閱[定義新報表](#defining-your-new-report)。

### 列特定查詢{#column-specific-query}

這會定義特定資料擷取（從[報表資料結果集](#the-query-and-data-retrieval)），以用於個別欄。

```xml
N:definitions
    N:queryBuilder
        P:property [String|String[]]
        P:subPath
        P:secondaryProperty [String|String[]]
        P:secondarySubPath
```

* `property`

   定義用於計算實際儲存格值的屬性。

   如果屬性定義為String[] ，則會掃描（依序）多個屬性以尋找實際值。

   例如，在下列案例中：

   `property = [ "jcr:lastModified", "jcr:created" ]`

   對應的值提取器（此處控制）將：

   * 檢查是否有jcr:lastModified屬性可用，如果有，請使用它。
   * 如果沒有jcr:lastModified屬性可用，則將改用jcr:created的內容。

* `subPath`

   如果結果不位於查詢返回的節點上，`subPath`將定義屬性的實際位置。

* `secondaryProperty`

   定義第二個屬性，該屬性也必須用於計算實際儲存格值；這將僅用於某些列類型（diff和sortable）。

   例如，在「工作流實例報告」中，指定的屬性用於儲存開始時間和結束時間之間時間差的實際值（以毫秒為單位）。

* `secondarySubPath`

   與subPath類似，使用`secondaryProperty`時。

在大多數情況下，只會使用`property`。

### 客戶端篩選器{#client-filter}

客戶端篩選器從伺服器返回的資料中提取要顯示的資訊。

>[!NOTE]
>
>此篩選器會在套用完整個伺服器端處理後，在clientside執行。

```xml
N:definitions
    N:data
        P:clientFilter [String]
```

`clientFilter` 定義為JavaScript函式，其可：

* 作為輸入，接收一個參數；從伺服器傳回的資料（因此已完全預先處理）
* 作為輸出，返回篩選（已處理）值；從輸入資訊中提取或導出的資料

下列範例會從元件路徑中擷取對應的頁面路徑：

```
function(v) {
    var sepPos = v.lastIndexOf('/jcr:content');
    if (sepPos < 0) {
        return v;
    }
    return v.substring(sepPos + '/jcr:content'.length, v.length);
}
```

### 解析器和預處理{#resolvers-and-preprocessing}

[處理佇列](#processing-queue)定義各種解析器並設定預處理：

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

   定義要使用的解析器。 可使用下列解析器：

   * `const`

      將值映射至其他值；例如，這可用來將常數（例如`en`）解析為其等值`English`。

   * `default`

      預設解析器。 這是一個虛擬解析器，它實際上不解析任何內容。

   * `page`

      將路徑值解析為適當頁面的路徑；更精確地，指向相應的`jcr:content`節點。 例如， `/content/.../page/jcr:content/par/xyz`解析為`/content/.../page/jcr:content`。

   * `path`

      通過可選地附加子路徑並從解析路徑處的節點屬性（由`resolverConfig`定義）獲取實際值來解析路徑值。 例如，`/content/.../page/jcr:content`的`path`可解析為`jcr:title`屬性的內容，這表示頁面路徑已解析為頁面標題。

   * `pathextension`

      通過預定路徑並從已解析路徑上的節點的屬性中獲取實際值來解析值。 例如，值`de`可能會由路徑（如`/libs/wcm/core/resources/languages`）加上前置詞，從屬性`language`取值，將國家/地區代碼`de`解析為語言說明`German`。

* `resolverConfig`

   提供解析程式的定義；可用選項取決於所選`resolver`:

   * `const`

      使用屬性來指定要解析的常數。 屬性的名稱會定義要解析的常數；屬性的值會定義解析的值。

      例如，具有&#x200B;**Name**= `1`和&#x200B;**Value** `=One`的屬性將解析為1對1。

   * `default`

      無可用配置。

   * `page`

      * `propertyName` (可選)

         定義應用於解析值的屬性名稱。 若未指定，則會使用預設值&#x200B;*jcr:title*（頁面標題）;對於`page`解析程式，這表示先將路徑解析為頁面路徑，再進一步解析為頁面標題。
   * `path`

      * `propertyName` (可選)

         指定應用於解析值的屬性名稱。 如果未指定，則使用預設值`jcr:title`。

      * `subPath` (可選)

         此屬性可用來指定要在解析值之前附加至路徑的尾碼。
   * `pathextension`

      * `path` （強制）

         定義要前置的路徑。

      * `propertyName` （強制）

         定義實際值所在的解析路徑上的屬性。

      * `i18n` （可選）類型布林值)

         確定解析的值是否應為&#x200B;*國際化*（即使用[CQ5的國際化服務](/help/sites-administering/tc-manage.md)）。



* `preprocessing`

   預處理是可選的，可以（單獨）綁定到處理階段&#x200B;*apply*&#x200B;或&#x200B;*applyAfter*:

   * `apply`

      初始預處理階段（表示處理隊列](#processing-queue)中的[步驟3）。

   * `applyAfter`

      在預處理後套用（在處理佇列的表示中](#processing-queue)步驟9）。[

#### 解析器 {#resolvers}

解析器用於提取所需資訊。 各種解析器的範例包括：

**康斯特**

以下將解析字串`New version created`的內容值`VersionCreated`。

請參閱 `/libs/cq/reporting/components/auditreport/typecol/definitions/data`.

```xml
N:data
    P:resolver=const
    N:resolverConfig
        P:VersionCreated="New version created"
```

**頁面**

解析對應頁面之jcr:content(child)節點上jcr:description屬性的路徑值。

請參閱 `/libs/cq/reporting/components/compreport/pagecol/definitions/data`.

```xml
N:data
    P:resolver=page
    N:resolverConfig
        P:propertyName="jcr:description"
```

**路徑**

以下檔案解析`/content/.../page`屬性內容的路徑，這表示頁面路徑已解析為頁面標題。`jcr:title`

請參閱 `/libs/cq/reporting/components/auditreport/pagecol/definitions/data`.

```xml
N:data
    P:resolver=path
    N:resolverConfig
        P:propertyName="jcr:title"
        P:subPath="/jcr:content"
```

**路徑擴充功能**

以下內容會以路徑副檔名`/libs/wcm/core/resources/languages`為值`de`前置詞，然後從屬性`language`取用值，將國家/地區代碼`de`解析為語言說明`German`。

請參閱 `/libs/cq/reporting/components/userreport/languagecol/definitions/data`.

```xml
N:data
    P:resolver=pathextension
    N:resolverConfig
        P:path="/libs/wcm/core/resources/languages"
        P:propertyName="language"
```

#### 預處理 {#preprocessing}

`preprocessing`定義可套用至：

* 原始值：

   原始值的預處理定義直接在`apply`和/或`applyAfter`上指定。

* 值（在其匯總狀態中）:

   如有必要，可為每個匯總提供個別定義。

   要指定聚合值的顯式預處理，預處理定義必須駐留在相應的`aggregated`子節點(`apply/aggregated`, `applyAfter/aggregated`)上。 如果需要對不同聚合進行顯式預處理，則預處理定義位於具有相應聚合名稱的子節點上（例如`apply/aggregated/min/max`或其他聚合）。

您可以指定下列其中一項，以在預處理期間使用：

* [查找和替](#preprocessing-find-and-replace-patterns)
換模式找到時，指定的模式（定義為規則表達式）被另一個模式替換；例如，這可用來擷取原始字串的子字串。

* [資料類型格式化程式](#preprocessing-data-type-formatters)

   將數值轉換為相對字串；例如，代表1小時時差的值「」會解析為字串，例如`1:24PM (1 hour ago)`。

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

#### 預處理 — 查找和替換模式{#preprocessing-find-and-replace-patterns}

對於預處理，您可以指定位於的`pattern`（定義為[規則運算式](https://en.wikipedia.org/wiki/Regular_expression)或規則運算式），然後以`replace`模式取代：

* `pattern`

   用來尋找子字串的規則運算式。

* `replace`

   將用作原始字串的替換字串或字串的表示。 這通常表示規則運算式`pattern`所定位之字串的子字串。

取代範例可劃分為：

* 對於具有以下兩個屬性的節點`definitions/data/preprocessing/apply`:

   * `pattern`: `(.*)(/jcr:content)(/|$)(.*)`
   * `replace`:  `$1`

* 字串的送達方式為：

   * `/content/geometrixx/en/services/jcr:content/par/text`

* 將分為四節：

   * `$1` -  `(.*)` -  `/content/geometrixx/en/services`
   * `$2` -  `(/jcr:content)` -  `/jcr:content`
   * `$3` -  `(/|$)` -  `/`
   * `$4` -  `(.*)` -  `par/text`

* 並以`$1`表示的字串取代：

   * `/content/geometrixx/en/services`

#### 前置處理 — 資料類型格式化程式{#preprocessing-data-type-formatters}

這些格式化程式會將數值轉換為相對字串。

例如，這可用於允許`min`、`avg`和`max`匯總的時間欄。 由於`min`/ `avg`/ `max`匯總顯示為&#x200B;*時間差*(例如`10 days ago`)，則需要資料格式化程式。 為此，將`datedelta`格式化器應用於`min`/ `avg`/ `max`匯總值。 如果`count`匯總也可用，則不需要格式化程式，原始值也不需要。

目前可用的資料類型格式化程式包括：

* `format`

   資料類型格式化程式：

   * `duration`

      持續時間是兩個定義日期之間的時間範圍。 例如，工作流程動作的開始和結束(從2/13/11 11:23h開始，一小時後在2/13/11 12:23h結束)花了1小時。

      它會將數值（解譯為毫秒）轉換為持續時間字串；例如，`30000`格式為* `30s`。*

   * `datedelta`

      Datadelta是過去某個日期到「現在」的時間範圍（因此，如果稍後時間檢視報表，結果會不同）。

      它會將數值（以天為單位解譯為時間差）轉換為相對日期字串。 例如，1的格式為1天前。

下列範例定義`min`和`max`匯總的`datedelta`格式：

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

### 列特定定義{#column-specific-definitions}

欄的特定定義會定義該欄可用的篩選器和匯總。

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

      用於擷取匯總所需的部分日期（例如，依年分組，以取得每年匯總的資料）。

   * `sortable`

      用於使用不同值（如來自不同屬性）來排序和顯示的值。
   此外， 以上任何項目皆可定義為多值；例如， `string[]`定義字串的陣列。

   值提取器由列類型選擇。 如果某個值提取器可用於列類型，則使用此提取器。 否則，會使用預設值提取器。

   類型可（可選）取參數。 例如， `timeslot:year`會從日期欄位擷取年份。 類型及其參數：

   * `timeslot`  — 值可與的對應常數比 `java.utils.Calendar`較。

      * `timeslot:year` - `Calendar.YEAR`
      * `timeslot:month-of-year` -  `Calendar.MONTH`
      * `timeslot:week-of-year` -  `Calendar.WEEK_OF_YEAR`
      * `timeslot:day-of-month` -  `Calendar.DAY_OF_MONTH`
      * `timeslot:day-of-week` -  `Calendar.DAY_OF_WEEK`
      * `timeslot:day-of-year` -  `Calendar.DAY_OF_YEAR`
      * `timeslot:hour-of-day` -  `Calendar.HOUR_OF_DAY`
      * `timeslot:minute-of-hour` -  `Calendar.MINUTE`


* `groupable`

   定義報表是否可依此欄分組。

* `filters`

   篩選定義。

   * `filterType`

      可用的篩選器包括：

      * `string`

         字串型篩選。
   * `id`

      篩選器識別碼。

   * `phase`

      可用階段：

      * `raw`

         篩選器會套用至原始資料。

      * `preprocessed`

         篩選器會套用至預先處理的資料。

      * `resolved`

         篩選器會套用至解析的資料。


* `aggregates`

   匯總定義。

   * `text`

      匯總的文字名稱。 如果未指定`text`，則會採用匯總的預設說明；例如， `minimum`將用於`min`匯總。

   * `type`

      匯總類型。 可用的匯總包括：

      * `count`

         計算列數。

      * `count-nonempty`

         計算非空行的數量。

      * `min`

         提供最小值。

      * `max`

         提供最大值。

      * `average`

         提供平均值。

      * `sum`

         提供所有值的總和。

      * `median`

         提供中位數值。

      * `percentile95`

         採用所有值的第95個百分位數。

### 列預設值{#column-default-values}

這可用來定義欄的預設值：

```xml
N:defaults
    P:aggregate
```

* `aggregate`

   有效的`aggregate`值與`aggregates`下`type`的值相同(請參閱[欄特定定義（定義 — 篩選器/匯總）](#column-specific-definitions))。

### 事件和動作{#events-and-actions}

「編輯配置」定義偵聽器偵測的必要事件，以及這些事件發生後要套用的動作。 如需背景資訊，請參閱元件開發](/help/sites-developing/components.md)簡介。[

必須定義下列值，以確保滿足所有必要動作：

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

### 一般列{#generic-columns}

一般欄是擴充功能，其中（大部分）欄定義儲存在欄節點（而非元件節點）的例項上。

它們會針對個別一般元件使用您自訂的（標準）對話方塊。 此對話框允許報告用戶定義報告頁上一般列的列屬性(使用菜單選項&#x200B;**列屬性……**)。

例如，**使用者報表**&#x200B;的&#x200B;**一般**&#x200B;欄；請參閱`/libs/cq/reporting/components/userreport/genericcol`。

要使列成為泛型：

* 將列的`definition`節點的`type`屬性設定為`generic`。

   請參閱 `/libs/cq/reporting/components/userreport/genericcol/definitions`

* 在列的`definition`節點下指定（標準）對話框定義。

   請參閱 `/libs/cq/reporting/components/userreport/genericcol/definitions/dialog`

   * 對話方塊的欄位必須參照與對應元件屬性（包括其路徑）相同的名稱。

      例如，如果要使通用對話框配置通用列的類型，請使用名稱為`./definitions/type`的欄位。

   * 使用UI/對話框定義的屬性優先於`columnbase`元件上定義的屬性。

* 定義編輯配置。

   請參閱 `/libs/cq/reporting/components/userreport/genericcol/cq:editConfig`

* 使用標準AEM方法來定義（其他）欄屬性。

   請注意，對於在元件實例和列實例上定義的屬性，列實例上的值優先。

   通用列的可用屬性包括：

   * `jcr:title`  — 列名
   * `definitions/aggregates`  — 匯總
   * `definitions/filters`  — 篩選器
   * `definitions/type` — 欄的類型（必須在對話方塊中定義，使用選取器/組合方塊或隱藏欄位）
   * `definitions/data/resolver` 和( `definitions/data/resolverConfig` 但不 `definitions/data/preprocessing` 能) `.../clientFilter` — 解析程式和設定
   * `definitions/queryBuilder`  — 查詢產生器設定
   * `defaults/aggregate`  — 預設匯總

   若是&#x200B;**使用者報表**&#x200B;上一般欄的新例項，則使用對話方塊定義的屬性會保留在下：

   `/etc/reports/userreport/jcr:content/report/columns/genericcol/settings/generic`

## 報表設計{#report-design}

設計會定義哪些欄類型可用於建立報表。 它還定義了添加列的段落系統。

強烈建議您為每個報表建立個別設計。 這可確保完全的彈性。 另請參閱[定義新報表](#defining-your-new-report)。

預設報告元件保存在`/etc/designs/reports`下。

報表的位置取決於元件的位置：

* `/etc/designs/reports/<yourReport>` 如果報表位於  `/apps/cq/reporting`

* `/etc/designs/<yourProject>/reports/<*yourReport*>` 對於使用模式的報 `/apps/<yourProject>/reports` 表

必需的設計屬性在`jcr:content/reportpage/report/columns`上註冊（例如`/etc/designs/reports/<reportName>/jcr:content/reportpage/report/columns`）:

* `components`

   報表上允許的任何元件和/或元件群組。

* `sling:resourceType`

   值`cq/reporting/components/repparsys`的屬性。

範例設計程式碼片段（取自元件報表的設計）為：

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

不需要指定個別欄的設計。 可在設計模式中定義可用列。

>[!NOTE]
>
>建議您不要對標準報表設計進行任何變更。 這是為了確保您不會在升級或安裝Hotfix時遺失任何變更。
>
>如果您想自訂標準報表，請複製報表及其設計。

>[!NOTE]
>
>建立報表時，可自動建立預設欄。 這些在範本中指定。

## 報表範本{#report-template}

每種報表類型都必須提供範本。 這些是標準的[CQ範本](/help/sites-developing/templates.md)，可依此設定。

範本必須：

* 將`sling:resourceType`設為`cq/reporting/components/reportpage`

* 指明要使用的設計
* 通過`sling:resourceType`屬性建立引用容器(`reportbase`)元件的`report`子節點

範本片段範例（取自元件報表範本）為：

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

範本片段範例顯示根路徑的定義（取自使用者報表範本）為：

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

預設報告模板位於`/libs/cq/reporting/templates`下。

不過，強烈建議您不要更新這些節點，而是在`/apps/cq/reporting/templates`下或更適當的`/apps/<yourProject>/reports/templates`下建立自己的元件節點。

舉例來說，（請參閱[報表元件的位置](#location-of-report-components)）:

```xml
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
```

在此底下，您可建立範本的根：

```xml
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
                N:<reportname> [sling:Folder]
```

## 建立您自己的報表 — 範例{#creating-your-own-report-an-example}

### 定義新報表{#defining-your-new-report}

若要定義新報表，您必須建立並設定：

1. 報表元件的根。
1. 報表庫元件。
1. 一個或多個列基元件。
1. 報表設計。
1. 報表範本的根。
1. 報表範本。

為了說明這些步驟，以下範例定義了一份報告，其中列出儲存庫內的所有OSGi設定；即`sling:OsgiConfig`節點的所有實例。

>[!NOTE]
>
>複製現有報表，然後自訂新版本是另一種方法。

1. 為新報表建立根節點。

   例如，在`/apps/cq/reporting/components/osgireport`底下。

   ```xml
   N:cq [nt:folder]
       N:reporting [sling:Folder]
           N:components [sling:Folder]
               N:osgireport [sling:Folder]
   ```

1. 定義報表庫。 例如，`/apps/cq/reporting/components/osgireport`下的`osgireport[cq:Component]`。

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

   這會定義報表基礎元件，其功能包括：

   * 搜索`sling:OsgiConfig`類型的所有節點
   * 顯示`pie`和`lineseries`圖表
   * 提供對話方塊供使用者設定報表

1. 定義第一列（列基）元件。 例如，`/apps/cq/reporting/components/osgireport`下的`bundlecol[cq:Component]`。

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

   這會定義一個列基元件，該元件包括：

   * 搜尋並傳回從伺服器收到的值；在此例中，每個`sling:OsgiConfig`節點的`jcr:path`屬性
   * 提供`count`匯總
   * 無法分組
   * 標題`Bundle`（表中的列標題）
   * 在sidekick組`OSGi Report`中
   * 在指定事件中刷新

   >[!NOTE]
   >
   >在此示例中，沒有`N:data`和`P:clientFilter`的定義。 這是因為從伺服器收到的值是以1:1為基礎傳回的 — 這是預設行為。
   >
   >這與定義相同：
   >
   >
   ```
   >N:data [nt:unstructured]
   >   P:clientFilter [String] = "function(v) { return v; }"
   >```
   >
   >其中，函式只會傳回其收到的值。

1. 定義報表設計。 例如，`/etc/designs/reports`下的`osgireport[cq:Page]`。

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

1. 為新報表範本建立根節點。

   例如，在`/apps/cq/reporting/templates/osgireport`底下。

   ```xml
   N:cq [nt:folder]
       N:reporting [sling:Folder]
           N:templates [sling:Folder]
               N:osgireport [cq:Template]
   ```

1. 定義報表範本。 例如，`/apps/cq/reporting/templates`下的`osgireport[cq:Template]`。

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

   這會定義一個範本，其中：

   * 定義產生報表的`allowedPaths` — 在上述案例中，位於`/etc/reports`下方
   * 提供範本的標題和說明
   * 提供範本清單中要使用的縮圖影像（上方未列出此節點的完整定義 — 最簡單的方式是從現有報表複製thumbnail.png例項）。

### 建立新報表的例項{#creating-an-instance-of-your-new-report}

現在可以建立新報表的例項：

1. 開啟&#x200B;**Tools**&#x200B;控制台。

1. 在左窗格中選擇&#x200B;**Reports**。
1. 然後&#x200B;**新建……**。 定義&#x200B;**標題**&#x200B;和&#x200B;**名稱**，從範本清單中選擇新的報表類型（**OSGi報表範本**），然後按一下&#x200B;**建立**。
1. 您的新報表例項會出現在清單中。 按兩下以開啟。
1. 從sidekick拖曳元件（在此範例中，**OSGi報表**&#x200B;群組中的&#x200B;**Bundle**）以建立第一欄，並[啟動報表定義](/help/sites-administering/reporting.md#the-basics-of-report-customization)。

   >[!NOTE]
   >
   >由於此示例沒有任何可分組的列，因此圖表將不可用。 要查看圖表，請將`groupable`設定為`true`:
   >
   >
   ```
   >N:osgireport [sling:Folder]
   > N:bundlecol [cq:Component]
   > N:definitions [nt:unstructured]
   > P:groupable [Boolean] = true
   >```

## 配置報告框架服務{#configuring-the-report-framework-services}

本節說明實作報表架構之OSGi服務的進階設定選項。

您可以使用Web主控台的「設定」功能表來檢視這些項目（例如`http://localhost:4502/system/console/configMgr`）。 使用AEM時，有數種方法可管理這類服務的組態設定；如需詳細資訊和建議實務，請參閱[設定OSGi](/help/sites-deploying/configuring-osgi.md) 。

### 基本服務(Day CQ Reporting Configuration){#basic-service-day-cq-reporting-configuration}

* **** 時區定義為建立的時區歷史資料。這是為了確保歷史圖表為全球每位使用者顯示相同的資料。
* **** 本地定義要與時區一起用於歷史 **** 資料的地區。區域設定用於確定某些特定於區域設定的日曆設定（例如，一週的第一天是星期日還是星期一）。

* **快照** 路徑定義儲存歷史圖表快照的根路徑。
* **報表** 路徑定義報表所在的路徑。快照服務將使用此功能來確定要為其實際拍攝快照的報表。
* **每** 日快照定義每日快照拍攝時的每小時。指定的小時位於伺服器的本地時區。
* **每小時** 快照定義了每小時快照拍攝時的每小時分鐘。
* **行（最大）** 定義了為每個快照儲存的最大行數。應合理選擇此值；如果太高，則會影響儲存庫的大小，如果太低，資料可能不準確，因為歷史資料的處理方式。
* **若已啟用**，則可使用選取器來建立假的歷史 `fakedata` 資料；如果已停用，則使用選 `fakedata` 取器會擲回例外狀況。

   由於資料是假的，因此只能&#x200B;**&#x200B;用於測試和偵錯。

   使用`fakedata`選擇器會以隱含方式完成報表，因此所有現有資料都會遺失；資料可以手動還原，但這可能會是個耗時的程式。

* **快照** 用戶定義了可用於拍攝快照的可選用戶。

   基本上，快照是為已完成報告的用戶拍攝的。 在某些情況下（例如，在發佈系統上，此使用者不存在，因為其帳戶尚未復寫），您會想要指定一個使用的後援使用者。

   此外，指定使用者可能會帶來安全風險。

* **強制快照用戶**，如果啟用，則所有快照將與在快照用戶 *下指定的用戶*&#x200B;一起拍攝。如果處理不正確，可能會對安全性造成嚴重影響。

### 快取設定（日CQ報告快取）{#cache-settings-day-cq-reporting-cache}

* **** 啟用可讓您啟用或停用報表資料的快取。啟用報表快取，會在數個請求期間將報表資料保留在記憶體中。 這可能會提高效能，但會導致記憶體消耗增加，在極端情況下，可能會導致記憶體不足。
* **** TTL會定義快取報表資料的時間（以秒為單位）。數字越高，效能越好，但若資料在某個時段內變更，則可能也會傳回不正確的資料。
* **最大** 項定義了任何時候要快取的報表數量上限。

>[!NOTE]
>
>每個使用者和語言的報表資料可能不同。 因此，系統會根據報表、使用者和語言快取報表資料。 這表示`2`的&#x200B;**最大條目**&#x200B;值實際上快取以下任一項的資料：
>
>* 使用不同語言設定的兩個使用者，一個報表
>* 一個使用者和兩個報表

>


