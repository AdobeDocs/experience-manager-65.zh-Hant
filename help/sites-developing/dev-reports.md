---
title: 開發報表
description: Adobe Experience Manager (AEM)根據報告架構提供多種標準報告
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 3891150e-9972-4bbc-ad61-7f46a1f9bbb4
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '5177'
ht-degree: 0%

---


# 開發報表 {#developing-reports}

Adobe Experience Manager (AEM)提供了一系列[標準報告](/help/sites-administering/reporting.md)，其中大部分都以報告架構為基礎。

使用框架，您可以擴充這些標準報表，或開發您自己的新報表。 報告架構與現有的CQ5概念和原則緊密整合，因此開發人員可以利用他們對CQ5的現有知識作為開發報告的跳板。

對於透過AEM傳送的標準報表：

* 這些報表是以報告架構為基礎：

   * [元件報表](/help/sites-administering/reporting.md#component-report)
   * [頁面活動報表](/help/sites-administering/reporting.md#page-activity-report)
   * [使用者報表](/help/sites-administering/reporting.md#user-report)
   * [工作流程例項報表](/help/sites-administering/reporting.md#workflow-instance-report)

* 下列報表是根據個別原則，因此無法擴充：

   * [磁碟使用情況](/help/sites-administering/reporting.md#disk-usage)
   * [健康情況檢查](/help/sites-administering/reporting.md#health-check)
   * [工作流程報告](/help/sites-administering/reporting.md#workflow-report)

>[!NOTE]
>
>教學課程[建立您自己的報表 — 範例](#creating-your-own-report-an-example)也說明可以使用多少下列原則。
>
>您也可以參閱標準報表，以瞭解其他實作範例。

>[!NOTE]
>
>在下列範例和定義中，使用下列標籤法：
>
>* 每一行會定義一個節點或屬性，其中：
>  `N:<name> [<nodeType>]` ：說明名稱為`<*name*>`且節點型別為&#x200B;`<*nodeType*>`*.*的節點
>  `P:<name> [<propertyType]` ：描述名稱為`<*name*>`且屬性型別為`<*propertyType*>`的屬性。
>  `P:<name> = <value>` ：說明必須設定為`<value>`值的屬性`<name>`。
>
>* 縮排顯示節點之間的階層式相依性。
>* 專案分隔方式 | 代表可能專案的清單；例如，型別或名稱；例如，`String|String[]`表示屬性可以是String或String[]。
>
>* `[]`描繪陣列；例如String[]或節點陣列，如[查詢定義](#query-definition)中。
>
>除非另有說明，否則預設型別為：
>
>* 節點 — `nt:unstructured`
>* 屬性 — `String`

## 報告框架 {#reporting-framework}

報表架構的運作原理如下：

* 它完全以CQ5 QueryBuilder執行的查詢所傳回的結果集為基礎。
* 結果集會定義報表中顯示的資料。 結果集中的每一列對應於報告表格檢視中的列。
* 可在結果集上執行的操作類似於RDBMS概念；主要是&#x200B;*群組*&#x200B;和&#x200B;*彙總*。

* 大部分的資料擷取與處理作業都在伺服器端進行。
* 使用者端應自行負責顯示預先處理的資料。 使用者端只會執行次要的處理工作（例如，在儲存格內容中建立連結）。

報表架構（以標準報表的結構說明）會使用以下建置區塊，由處理佇列饋送：

![chlimage_1-248](assets/chlimage_1-248.png)

### 報告頁面 {#report-page}

報告頁面為：

* 標準CQ5頁面。
* 根據為報告](#report-template)設定的[標準CQ5範本。

### 報表基礎 {#report-base}

[`reportbase`元件](#report-base-component)構成任何報表的基礎，因為它：

* 保留傳遞基礎結果資料集的[查詢](#the-query-and-data-retrieval)的定義。

* 它是經過調整的段落系統，包含新增至報告的所有欄( `columnbase`)。
* 定義哪些圖表型別可用以及哪些目前作用中。
* 定義「編輯」對話方塊，使用者可在此對話方塊中設定報表的某些方面。

### 欄基底 {#column-base}

每個資料行都是[`columnbase`元件](#column-base-component)的執行個體，該元件：

* 是段落，由個別報表的parsys ( `reportbase`)使用。
* 定義連至[基礎結果集](#the-query-and-data-retrieval)的連結。 也就是說，它定義了此結果集中參照的特定資料，以及處理方式。
* 保留其他定義；例如可用的彙總和篩選以及任何預設值。

### 查詢與資料擷取 {#the-query-and-data-retrieval}

查詢：

* 定義為[`reportbase`](#report-base)元件的一部分。
* 是以[CQ QueryBuilder](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/search/QueryBuilder.html)為基礎。
* 擷取用作報表基礎的資料。 結果集（表格）的每一列都會繫結至查詢傳回的節點。 接著會從此資料集中擷取[個別資料行](#column-base-component)的特定資訊。

* 通常包含：

   * 根路徑。

     這會指定要搜尋之存放庫的子樹狀結構。

     為了協助將效能影響降至最低，建議（嘗試）將查詢限制在存放庫的特定子樹狀結構。 根路徑可在[報告範本](#report-template)中預先定義，或由使用者在[組態（編輯）對話方塊](#configuration-dialog)中設定。

   * [一或多個條件](#query-definition)。

     這些條件會強制執行，以產生（初始）結果集；例如，它們包括對節點型別的限制或屬性限制。

**此處的要點是，查詢結果集中傳回的每個單一節點都會用來在報告上產生單一列（所以是1:1關係）。**

開發人員必須確定為報表定義的查詢會傳回適合該報表的節點集。 但是，節點本身不需要保留所有必要的資訊，這也可以從父節點和/或子節點衍生。 例如，用於[使用者報告](/help/sites-administering/reporting.md#user-report)的查詢會根據節點型別選取節點（在此例中為`rep:user`）。 不過，此報告上的大多數欄不會直接從這些節點取得資料，而是從子節點`profile`取得資料。

### 處理佇列 {#processing-queue}

[查詢](#the-query-and-data-retrieval)會傳回資料結果集，以便在報表中顯示為資料列。 結果集中的每一列都會在[數個階段](#phases-of-the-processing-queue)中處理（伺服器端），然後再傳輸到使用者端以在報表上顯示。

這允許：

* 從基礎結果集擷取和衍生值。

  例如，它可讓您計算兩個屬性值之間的差異，將兩個屬性值處理為單一值。

* 解析擷取的值；這可以用多種方式完成。

  例如，路徑可以對應到標題（如同個別&#x200B;*jcr：title*&#x200B;屬性中更易於人類閱讀的內容）。

* 在不同點套用篩選器。
* 建立複合值（如有必要）。

  例如，由向使用者顯示的文字、要用於排序的值以及用於建立連結的其他URL （在使用者端）組成。

#### 處理佇列的工作流程 {#workflow-of-the-processing-queue}

以下工作流程代表處理佇列：

![chlimage_1-249](assets/chlimage_1-249.png)

#### 處理佇列的階段 {#phases-of-the-processing-queue}

其中詳細步驟和元素為：

1. 使用值擷取器將[初始查詢(reportbase)](#query-definition)傳回的結果轉換為基本結果集。

   根據[資料行型別](#column-specific-definitions)自動選擇值擷取器。 它們用於從基礎JCR查詢讀取值，並從這些值建立結果集；之後，可以應用進一步處理。 例如，對於`diff`型別，值擷取器會讀取兩個屬性，並計算之後新增至結果集的單一值。 無法設定值擷取器。

1. 對於包含原始資料的初始結果集，套用[初始篩選](#column-specific-definitions) （*原始*&#x200B;階段）。

1. 值為[已預先處理](#processing-queue)；如為&#x200B;*套用*&#x200B;階段所定義。

1. [篩選](#column-specific-definitions) （指派給&#x200B;*預先處理*&#x200B;階段）是在預先處理的值上執行。

1. 已解析值；根據[定義的解析器](#processing-queue)。
1. [篩選](#column-specific-definitions) （指派給&#x200B;*已解決*&#x200B;階段）是在已解決的值上執行。

1. 資料為[分組和彙總](#column-specific-definitions)。
1. 陣列資料可透過將其轉換為（字串型）清單來解析。

   此隱含步驟會將多值結果轉換為可顯示的清單；以多值JCR屬性為基礎的（未彙總）儲存格值需要此隱含步驟。

1. 值再次是[已預先處理](#processing-queue)；如為&#x200B;*afterApply*&#x200B;階段所定義。

1. 資料會排序。
1. 處理的資料會傳輸到使用者端。

>[!NOTE]
>
>傳回基礎資料結果集的初始查詢已在`reportbase`元件上定義。
>
>在`columnbase`元件上定義了處理佇列的其他元素。

## 報告建構和設定 {#report-construction-and-configuration}

建構和設定報表需要下列專案：

* 報表元件定義的[位置](#location-of-report-components)
* [`reportbase`元件](#report-base-component)
* 一或多個[`columnbase`元件](#column-base-component)
* [頁面元件](#page-component)
* [報表設計](#report-design)
* [報告範本](#report-template)

### 報表元件的位置 {#location-of-report-components}

預設報告元件儲存在`/libs/cq/reporting/components`下。

不過，建議您不要更新這些節點，而是在`/apps/cq/reporting/components`下建立您自己的元件節點，或者如果更適合`/apps/<yourProject>/reports/components`。

其中（例如）：

```
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:components [sling:Folder]
```

您可以在此下建立報表的根，並在其下建立報表基底元件和欄基底元件：

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

報告頁面必須使用`/libs/cq/reporting/components/reportpage`的`sling:resourceType`。

自訂的頁面元件不是必要專案（通常是）。

## 報表基礎元件 {#report-base-component}

每個報表型別都需要衍生自`/libs/cq/reporting/components/reportbase`的容器元件。

此元件可作為整個報表的容器，並提供下列專案的資訊：

* [查詢定義](#query-definition)。
* 用於設定報告的[ （選擇性）對話方塊](#configuration-dialog)。
* 任何與報告整合的[圖表](#chart-definitions)。

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

  將結果集限制在具有特定值的特定屬性的節點中。 如果指定了多個限制，則節點必須滿足所有限制（AND作業）。

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

  會傳回`admin`使用者上次修改的所有`textimage`元件。

* `nodeTypes`

  用於將結果集限製為指定的節點型別。 可以指定多個節點型別。

* `mandatoryProperties`

  將結果集限製為具有&#x200B;*所有*&#x200B;指定屬性的節點。 未說明屬性的值。

全部都是選用專案，可視需要加以合併，但您至少必須定義其中一個。

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

  保留使用中圖表的定義。

   * `active`

     由於可以定義多個設定，因此您可以使用此項來定義哪些設定目前為使用中。 這些是由節點陣列所定義(這些節點沒有強制性的命名慣例，但標準報表通常使用`0`、`1`。 `x`)，每個都具有下列屬性：

      * `id`

        使用中圖表的識別。 這必須符合其中一個圖表`definitions`的識別碼。

* `definitions`

  定義報表可能可用的圖表型別。 要使用的`definitions`由`active`設定指定。

  使用節點陣列（通常也稱為`0`、`1`）指定定義。 `x`)，每個都具有下列屬性：

   * `id`

     圖表的識別。

   * `type`

     可用的圖表型別。 選取自：

      * `pie`
圓形圖。 僅從目前的資料產生。

      * `lineseries`
一連串的直線（代表實際快照的連線點）。 僅從歷史資料產生。

   * 根據圖表型別，可使用其他屬性：

      * 對於圖表型別`pie`：

         * `maxRadius` ( `Double/Long`)

           圓餅圖允許的最大半徑；因此圖表允許的大小上限（沒有圖例）。 如果已定義`fixedRadius`，則忽略。

         * `minRadius` ( `Double/Long`)

           圓餅圖允許的最小半徑。 如果已定義`fixedRadius`，則忽略。

         * `fixedRadius` ( `Double/Long`)
定義圓形圖的固定半徑。

      * 對於圖表型別[`lineseries`](/help/sites-administering/reporting.md#display-limits)：

         * `totals` ( `Boolean`)

           如果應該顯示其他顯示&#x200B;**總計**的行，則為True。
預設： `false`

         * `series` ( `Long`)

           要顯示的行/數列數目。
預設值： `9` （這也是允許的最大值）

         * `hoverLimit` ( `Long`)

           要顯示快顯視窗的彙總快照的最大數量（在每個水平線上顯示的點，代表不同的值）。 也就是說，當使用者確實將滑鼠移至圖表圖例中的不重複值或對應標籤上時。

           預設值： `35` （也就是說，如果超過35個不同的值適用於目前的圖表設定，則完全不會顯示快顯視窗）。

           此外還有10個可平行顯示的快顯視窗限制（將滑鼠移到圖例文字上方時，會顯示多個快顯視窗）。

### 設定對話方塊 {#configuration-dialog}

每個報告都可以有一個設定對話方塊，允許使用者為報告指定各種引數。 報表頁面開啟時，可透過&#x200B;**編輯**&#x200B;按鈕存取此對話方塊。

此對話方塊是標準的CQ [對話方塊](/help/sites-developing/components-basics.md#dialogs)，可以如此設定（如需詳細資訊，請參閱[CQ.Dialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Dialog)）。

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

提供了數個預先設定的元件；這些元件可在對話方塊中使用`xtype`屬性（值為`cqinclude`）參照：

* **`title`**

  `/libs/cq/reporting/components/commons/title`

  用於定義報告標題的文字欄位。

* **`description`**

  `/libs/cq/reporting/components/commons/description`

  定義報表說明的文字區域。

* **`processing`**

  `/libs/cq/reporting/components/commons/processing`

  報表處理模式的選擇器（手動/自動載入資料）。

* **`scheduling`**

  `/libs/cq/reporting/components/commons/scheduling`

  用於為歷史圖表排程快照的選擇器。

>[!NOTE]
>
>必須使用`.infinity.json`尾碼包含參照的元件（請參閱上述範例）。

### 根路徑 {#root-path}

此外，您也可以為報表定義根路徑：

* **`rootPath`**

  這會將報表限制在存放庫的特定區段（樹狀結構或子樹狀結構），這是效能最佳化的建議。 根路徑是由每個報告頁面`report`節點的`rootPath`屬性所指定（在建立頁面時從範本取得）。

  可透過以下方式指定：

   * [報告範本](#report-template) （以固定值或設定對話方塊的預設值）。
   * 使用者（使用此引數）

## 欄基本元件 {#column-base-component}

每個資料行型別都需要衍生自`/libs/cq/reporting/components/columnbase`的元件。

欄元件會定義下列專案的組合：

* [資料行特定查詢](#column-specific-query)組態。
* [解析器與前置處理](#resolvers-and-preprocessing)。
* [資料行特定定義](#column-specific-definitions) （例如篩選和彙總； `definitions`子節點）。
* [資料行預設值](#column-default-values)。
* [使用者端篩選器](#client-filter)會從伺服器傳回的資料擷取顯示資訊。
* 此外，資料行元件必須提供適當的`cq:editConfig`執行個體。 以定義所需的[事件和動作](#events-and-actions)。
* [泛型資料行](#generic-columns)的組態。

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

另請參閱[定義您的新報告](#defining-your-new-report)。

### 欄特定查詢 {#column-specific-query}

這會定義特定資料擷取（從[報告資料結果集](#the-query-and-data-retrieval)），以用於個別欄。

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

  如果屬性定義為String[]，則會掃描多個屬性（依序）以尋找實際值。

  例如，如果有：

  `property = [ "jcr:lastModified", "jcr:created" ]`

  對應的值擷取器（在這裡是控制對象）：

   * 檢查是否有可用的jcr：lastModified屬性，如果有，請使用它。
   * 如果沒有可用的jcr：lastModified屬性，則改用jcr：created的內容。

* `subPath`

  如果結果不在查詢傳回的節點上，`subPath`會定義屬性所在的位置。

* `secondaryProperty`

  第二個屬性，必須用來計算實際儲存格值。 此定義僅用於特定欄型別（差異和可排序）。

  例如，如果有「工作流程例項報表」，則指定的屬性會用於儲存開始與結束時間之間時間差的實際值（以毫秒為單位）。

* `secondarySubPath`

  與使用`secondaryProperty`時的subPath類似。

通常只會使用`property`。

### 使用者端篩選器 {#client-filter}

使用者端篩選器會從伺服器傳回的資料中擷取要顯示的資訊。

>[!NOTE]
>
>此篩選器會在套用整個伺服器端處理作業之後在使用者端執行。

```xml
N:definitions
    N:data
        P:clientFilter [String]
```

`clientFilter`是JavaScript函式，該函式：

* 作為輸入，會接收一個引數；資料會從伺服器傳回（如此已完成預先處理）
* 作為輸出，傳回篩選（已處理）值；從輸入資訊擷取或衍生的資料

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

### 解析器與預先處理 {#resolvers-and-preprocessing}

[處理佇列](#processing-queue)定義各種解析器，並設定前置處理：

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

  定義要使用的解析器。 下列解析器可供使用：

   * `const`

     將值對應到其他值；例如，這可用來將常數（例如`en`）解析為它的對等值`English`。

   * `default`

     預設解析程式。 這是虛擬解析程式，實際上不會解析任何內容。

   * `page`

     將路徑值解析為適當頁面的路徑；更準確地解析為對應的`jcr:content`節點。 例如，`/content/.../page/jcr:content/par/xyz`已解析為`/content/.../page/jcr:content`。

   * `path`

     解析路徑值，方法為選擇性附加子路徑，並在解析的路徑從節點的屬性（如`resolverConfig`所定義）中取得實際值。 例如，`/content/.../page/jcr:content`的`path`可以解析為`jcr:title`屬性的內容，這表示頁面路徑會解析為頁面標題。

   * `pathextension`

     藉由在路徑前面加上並從已解析路徑之節點的屬性中取得實際值來解析值。 例如，值`de`前面可能會加上一個路徑，例如`/libs/wcm/core/resources/languages`，從屬性`language`中取得值，以將國碼`de`解析為語言描述`German`。

* `resolverConfig`

  提供解析程式的定義。 可用的選項視選取的`resolver`而定：

   * `const`

     使用屬性來指定要解析的常數。 屬性的名稱會定義要解析的常數；屬性的值會定義解析的值。

     例如，具有&#x200B;**Name**= `1`和&#x200B;**Value** `=One`的屬性，會將1解析為1。

   * `default`

     沒有可用的設定。

   * `page`

      * `propertyName` (可選)

        定義用於解析值的屬性名稱。 如果未指定，則使用預設值&#x200B;*jcr：title* （頁面標題）；對於`page`解析程式，這表示先將路徑解析為頁面路徑，然後進一步解析為頁面標題。

   * `path`

      * `propertyName` (可選)

        指定用於解析值的屬性名稱。 如果未指定，則使用預設值`jcr:title`。

      * `subPath` (可選)

        此屬性可用於指定在解析值之前附加至路徑的後置字元。

   * `pathextension`

      * `path` （必要）

        定義要在前面加上的路徑。

      * `propertyName` （必要）

        定義實際值所在解析路徑上的屬性。

      * `i18n` （選擇性；輸入布林值）

        決定解析的值是否應為&#x200B;*國際化* （也就是使用[CQ5的國際化服務](/help/sites-administering/tc-manage.md)）。

* `preprocessing`

  前置處理是選擇性的，可以繫結（分別）到處理階段&#x200B;*apply*&#x200B;或&#x200B;*applyAfter*：

   * `apply`

     初始前置處理階段（[處理佇列](#processing-queue)的表示步驟3）。

   * `applyAfter`

     在預先處理之後套用([步驟9 （在處理佇列](#processing-queue)的表示中）。

#### 解析器 {#resolvers}

解析器可用來擷取所需的資訊。 各種解析器的範例包括：

**常數**

下列將`VersionCreated`的常數值解析為字串`New version created`。

請參閱`/libs/cq/reporting/components/auditreport/typecol/definitions/data`。

```xml
N:data
    P:resolver=const
    N:resolverConfig
        P:VersionCreated="New version created"
```

**Page**

解析對應頁面之jcr：content （子項）節點上jcr：description屬性的路徑值。

請參閱`/libs/cq/reporting/components/compreport/pagecol/definitions/data`。

```xml
N:data
    P:resolver=page
    N:resolverConfig
        P:propertyName="jcr:description"
```

**路徑**

以下將`/content/.../page`的路徑解析為`jcr:title`屬性的內容，這表示頁面路徑解析為頁面標題。

請參閱`/libs/cq/reporting/components/auditreport/pagecol/definitions/data`。

```xml
N:data
    P:resolver=path
    N:resolverConfig
        P:propertyName="jcr:title"
        P:subPath="/jcr:content"
```

**路徑副檔名**

下列專案會在值`de`前面加上路徑副檔名`/libs/wcm/core/resources/languages`，然後從屬性`language`中取得該值，以將國碼`de`解析為語言描述`German`。

請參閱`/libs/cq/reporting/components/userreport/languagecol/definitions/data`。

```xml
N:data
    P:resolver=pathextension
    N:resolverConfig
        P:path="/libs/wcm/core/resources/languages"
        P:propertyName="language"
```

#### 正在預先處理 {#preprocessing}

`preprocessing`定義可以套用至：

* 原始值：

  已在`apply`和/或`applyAfter`上直接指定原始值的預先處理定義。

* 彙總狀態下的值：

  如有必要，可以為每個彙總提供個別的定義。

  若要指定彙總值的明確前置處理，前置處理定義必須位於個別`aggregated`子節點( `apply/aggregated`， `applyAfter/aggregated`)。 如果需要明確預先處理不同的彙總，則預先處理定義會位於子節點上，且具有個別彙總的名稱（例如，`apply/aggregated/min/max`或其他彙總）。

您可以指定下列任一項在預先處理期間使用：

* [尋找和取代模式](#preprocessing-find-and-replace-patterns)
找到時，指定的模式（定義為規則運算式）會被其他模式取代；例如，這可用於擷取原始模式的子字串。

* [資料型別格式化程式](#preprocessing-data-type-formatters)

  將數值轉換為相對字串；例如，「代表一小時時間差的值」會解析為字串，例如`1:24PM (1 hour ago)`。

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

#### 預先處理 — 尋找與取代模式 {#preprocessing-find-and-replace-patterns}

若要預先處理，您可以指定位於並由`replace`模式取代的`pattern` （定義為[規則運算式](https://en.wikipedia.org/wiki/Regular_expression)或regex）：

* `pattern`

  用來尋找子字串的規則運算式。

* `replace`

  用來取代原始字串的字串或字串表示法。 這通常代表規則運算式`pattern`所定位的字串子字串。

範例取代可劃分為：

* 針對具有下列兩個屬性的節點`definitions/data/preprocessing/apply`：

   * `pattern`: `(.*)(/jcr:content)(/|$)(.*)`
   * `replace`: `$1`

* 字串的送達：

   * `/content/geometrixx/en/services/jcr:content/par/text`

* 分為四個區段：

   * `$1` - `(.*)` - `/content/geometrixx/en/services`
   * `$2` - `(/jcr:content)` - `/jcr:content`
   * `$3` - `(/|$)` - `/`
   * `$4` - `(.*)` - `par/text`

* 並取代為`$1`所代表的字串：

   * `/content/geometrixx/en/services`

#### 預先處理 — 資料型別格式化程式 {#preprocessing-data-type-formatters}

這些格式化程式會將數值轉換為相對字串。

例如，這可用於允許`min`、`avg`和`max`彙總的時間欄。 由於`min`/ `avg`/ `max`彙總會顯示為&#x200B;*時間差異* （例如`10 days ago`），因此它們需要資料格式器。 為此，`datedelta`格式化程式已套用至`min`/ `avg`/ `max`彙總值。 如果`count`彙總也可用，則不需要格式子，原始值也不需要。

目前可用的資料型別格式化程式包括：

* `format`

  資料型別格式化程式：

   * `duration`

     期間是兩個已定義日期之間的時間範圍。 例如，一小時工作流程動作的開始和結束，從2/13/11 11:23h開始，並在一小時後於2/13/11 12:23h結束。

     它將數值（解譯為毫秒）轉換為持續時間字串；例如，`30000`的格式為* `30s`。*

   * `datedelta`

     Datadelta是指過去某個日期到「現在」之間的時間範圍（因此，如果在之後的某個時間點檢視報表，會有不同的結果）。

     它會將此數值（解譯為以天為單位的時間差異）轉換為相對日期字串。 例如，1的格式為一天前。

下列範例定義`min`與`max`彙總的`datedelta`格式：

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

### 欄特定定義 {#column-specific-definitions}

欄特定定義會定義該欄可用的篩選器和彙總。

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

  下列專案可作為標準選項使用：

   * `string`
   * `number`
   * `int`
   * `date`
   * `diff`
   * `timeslot`

     用於擷取彙總所需的日期部分（例如，依年分組，以取得每年彙總的資料）。

   * `sortable`

     用於使用不同值（從不同屬性取得）進行排序和顯示的值。

  此外，上述任何專案都可以定義為多個值；例如，`string[]`會定義字串陣列。

  值擷取器是由欄型別所選擇。 如果值擷取器可用於欄型別，則會使用此擷取器。 否則，會使用預設值擷取器。

  型別可以（選擇性）接受引數。 例如，`timeslot:year`會從日期欄位中擷取年份。 型別及其引數：

   * `timeslot` — 這些值可與`java.utils.Calendar`的對應常數比較。

      * `timeslot:year` - `Calendar.YEAR`
      * `timeslot:month-of-year` - `Calendar.MONTH`
      * `timeslot:week-of-year` - `Calendar.WEEK_OF_YEAR`
      * `timeslot:day-of-month` - `Calendar.DAY_OF_MONTH`
      * `timeslot:day-of-week` - `Calendar.DAY_OF_WEEK`
      * `timeslot:day-of-year` - `Calendar.DAY_OF_YEAR`
      * `timeslot:hour-of-day` - `Calendar.HOUR_OF_DAY`
      * `timeslot:minute-of-hour` - `Calendar.MINUTE`

* `groupable`

  定義報表是否可依此欄分組。

* `filters`

  篩選器定義。

   * `filterType`

     可用的篩選器包括：

      * `string`

        字串型篩選器。

   * `id`

     篩選器識別碼。

   * `phase`

     可用的階段：

      * `raw`

        篩選器套用至原始資料。

      * `preprocessed`

        篩選條件會套用到已預先處理的資料。

      * `resolved`

        篩選器會套用至已解析的資料。

* `aggregates`

  彙總定義。

   * `text`

     彙總的文字名稱。 如果未指定`text`，則會採用彙總的預設描述。 例如，`minimum`用於`min`彙總。

   * `type`

     彙總型別。 可用的彙總包括：

      * `count`

        計算列數。

      * `count-nonempty`

        計算非空白列的數量。

      * `min`

        它提供最小值。

      * `max`

        它提供最大值。

      * `average`

        它提供平均值。

      * `sum`

        它會提供所有值的總和。

      * `median`

        它提供中間值。

      * `percentile95`

        使用所有值的第95個百分位數。

### 欄預設值 {#column-default-values}

定義欄的預設值：

```xml
N:defaults
    P:aggregate
```

* `aggregate`

  有效的`aggregate`值與`aggregates`下的`type`相同(請參閱[欄特定定義（定義 — 篩選器/彙總）](#column-specific-definitions) )。

### 事件與動作 {#events-and-actions}

「編輯組態」會定義監聽器偵測的必要事件，以及這些事件發生後要套用的動作。 如需背景資訊，請參閱[元件開發簡介](/help/sites-developing/components.md)。

必須定義下列值，以確保所有必要的動作都能得到滿足：

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

### 一般資料行 {#generic-columns}

Generic欄是擴充功能，其中（大部分）欄定義儲存在欄節點的例項（而非元件節點）上。

它們使用（標準）對話方塊，您可以針對個別類屬元件自訂該對話方塊。 此對話方塊可讓報表使用者定義報表頁面上一般欄的欄屬性（使用功能表選項&#x200B;**欄屬性……**）。

例如，**使用者報告**&#x200B;的&#x200B;**Generic**&#x200B;資料行。 請參閱`/libs/cq/reporting/components/userreport/genericcol`。

若要將欄設為類屬：

* 將資料行`definition`節點的`type`屬性設定為`generic`。

  檢視`/libs/cq/reporting/components/userreport/genericcol/definitions`

* 在欄的`definition`節點下指定（標準）對話方塊定義。

  檢視`/libs/cq/reporting/components/userreport/genericcol/definitions/dialog`

   * 對話方塊的欄位必須參照與對應元件屬性相同的名稱，包括其路徑。

     例如，如果要透過對話方塊設定泛型資料行的型別，請使用名稱為`./definitions/type`的欄位。

   * 使用UI/對話方塊定義的屬性優先於`columnbase`元件上定義的屬性。

* 定義編輯組態。

  檢視`/libs/cq/reporting/components/userreport/genericcol/cq:editConfig`

* 使用標準AEM方法來定義（其他）欄屬性。

  對於在元件和欄實體上定義的屬性，優先使用欄實體上的值。

  一般資料行可用的屬性包括：

   * `jcr:title` — 欄名稱
   * `definitions/aggregates` — 彙總
   * `definitions/filters` — 篩選器
   * `definitions/type` — 欄的型別（這必須在對話方塊中使用選取器/下拉式方塊或隱藏欄位定義）
   * `definitions/data/resolver`和`definitions/data/resolverConfig` （但不是`definitions/data/preprocessing`或`.../clientFilter`） — 解析程式和設定
   * `definitions/queryBuilder` — 查詢產生器設定
   * `defaults/aggregate` — 預設彙總

  如果&#x200B;**使用者報告**&#x200B;上有泛型資料行的新執行個體，則使用對話方塊定義的屬性會儲存在：

  `/etc/reports/userreport/jcr:content/report/columns/genericcol/settings/generic`

## 報表設計 {#report-design}

設計會定義哪些欄型別可用於建立報告。 它也會定義要新增欄的段落系統。

Adobe建議您為每個報告建立個別設計。 這麼做可確保完全的彈性。 請參閱[定義您的新報告](#defining-your-new-report)。

預設報告元件儲存在`/etc/designs/reports`下。

報表的位置取決於元件所在的位置：

* 如果報告在`/apps/cq/reporting`之下，`/etc/designs/reports/<yourReport>`就適合

* 使用`/apps/<yourProject>/reports`模式的報告的`/etc/designs/<yourProject>/reports/<*yourReport*>`

必要的設計屬性已登入在`jcr:content/reportpage/report/columns` （例如，`/etc/designs/reports/<reportName>/jcr:content/reportpage/report/columns`）：

* `components`

  報表上允許的任何元件和/或元件群組。

* `sling:resourceType`

  值為`cq/reporting/components/repparsys`的屬性。

以下是範例設計程式碼片段（取自元件報表的設計）：

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

不需要指定個別資料行的設計。 可用欄可在設計模式中定義。

>[!NOTE]
>
>Adobe建議您不要變更標準報表設計。 這是為了確保您在升級或安裝Hotfix時不會遺失任何變更。
>
>如果您想要自訂標準報表，請複製報表及其設計。

>[!NOTE]
>
>建立報表時，可自動建立預設欄。 這些在範本中指定。

## 報告範本 {#report-template}

每種報表型別都必須提供範本。 這些是標準的[CQ範本](/help/sites-developing/templates.md)，可依此設定。

範本必須：

* 將`sling:resourceType`設為`cq/reporting/components/reportpage`

* 指示要使用的設計
* 建立參照包含`sling:resourceType`屬性的容器(`reportbase`)元件的`report`子節點

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

範本片段範例(顯示根路徑（取自使用者報表範本）的定義)為：

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

預設報告範本保留在`/libs/cq/reporting/templates`下。

不過，Adobe建議您不要更新這些節點。 請改為在`/apps/cq/reporting/templates`下或更適當的`/apps/<yourProject>/reports/templates`下建立您自己的元件節點。

例如（另請參閱[報表元件](#location-of-report-components)的位置）：

```xml
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
```

在此底下，建立範本的根：

```xml
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
                N:<reportname> [sling:Folder]
```

## 建立自己的報表 — 範例 {#creating-your-own-report-an-example}

### 定義您的新報告 {#defining-your-new-report}

若要定義報表，請建立並設定：

1. 報表元件的根目錄。
1. 報表基礎元件。
1. 一或多個欄基本元件。
1. 報表設計。
1. 報表範本的根目錄。
1. 報表範本。

為了說明這些步驟，以下範例會定義一個報表，其中列出存放庫內的所有OSGi設定。 即`sling:OsgiConfig`節點的所有執行個體。

>[!NOTE]
>
>複製現有報表，然後自訂新版本是替代方法。

1. 為新報表建立根節點。

   例如，在`/apps/cq/reporting/components/osgireport`下。

   ```xml
   N:cq [nt:folder]
       N:reporting [sling:Folder]
           N:components [sling:Folder]
               N:osgireport [sling:Folder]
   ```

1. 定義您的報表基礎。 例如，`/apps/cq/reporting/components/osgireport`下的`osgireport[cq:Component]`。

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

   這會定義報表基礎元件，其可：

   * 搜尋型別`sling:OsgiConfig`的所有節點
   * 顯示`pie`和`lineseries`圖表
   * 提供對話方塊，供使用者設定報表

1. 定義您的第一欄（欄基底）元件。 例如，`/apps/cq/reporting/components/osgireport`下的`bundlecol[cq:Component]`。

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

   這會定義一個資料行基本元件，該元件：

   * 搜尋並傳回從伺服器收到的值；在此案例中，每個`sling:OsgiConfig`節點都有`jcr:path`屬性
   * 提供`count`彙總
   * 不可分組
   * 標題為`Bundle` （資料表中的資料行標題）
   * 在sidekick群組`OSGi Report`中
   * 指定事件的重新整理

   >[!NOTE]
   >
   >在此範例中，`N:data`和`P:clientFilter`沒有定義。 這是因為從伺服器收到的值是以1:1為基準傳回，這是預設行為。
   >
   >這與定義相同：
   >
   >```
   >N:data [nt:unstructured]
   >   P:clientFilter [String] = "function(v) { return v; }"
   >```
   >
   >其中函式只會傳回收到的值。

1. 定義您的報告設計。 例如，`/etc/designs/reports`下的`osgireport[cq:Page]`。

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

1. 為您的新報告範本建立根節點。

   例如，在`/apps/cq/reporting/templates/osgireport`下。

   ```xml
   N:cq [nt:folder]
       N:reporting [sling:Folder]
           N:templates [sling:Folder]
               N:osgireport [cq:Template]
   ```

1. 定義您的報表範本。 例如，`/apps/cq/reporting/templates`下的`osgireport[cq:Template]`。

   ```xml
   N:osgireport [cq:Template]
       P:allowedPaths [String[]] = "/etc/reports(/.*)?"
       P:jcr:description [String] = "Use this report generator to create an OSGi report."
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

   這會定義符合以下條件的範本：

   * 為產生的報告定義`allowedPaths` — 在上述案例中，在`/etc/reports`下的任何位置
   * 提供範本的標題和說明
   * 提供用於範本清單中的縮圖影像（上面未列出此節點的完整定義 — 最簡單的做法是複製現有報表中的thumbnail.png例項）。

### 建立新報告的例項 {#creating-an-instance-of-your-new-report}

您現在可以建立新報告的例項：

1. 開啟&#x200B;**工具**&#x200B;主控台。

1. 在左窗格中選取&#x200B;**報表**。
1. 然後&#x200B;**新增……** （從工具列）。 定義&#x200B;**Title**&#x200B;和&#x200B;**Name**，從範本清單中選取新的報表型別（**OSGi報表範本**），然後按一下&#x200B;**建立**。
1. 您的新報表例項會出現在清單中。 連按兩下以開啟。
1. 從Sidekick拖曳元件（例如，**OSGi報表**&#x200B;群組中的&#x200B;**套件**）以建立第一欄並[啟動報表定義](/help/sites-administering/reporting.md#the-basics-of-report-customization)。

   >[!NOTE]
   >
   >由於此範例沒有任何可分組的欄，因此無法使用圖表。 若要檢視圖表，請將`groupable`設為`true`：
   >
   >```
   >N:osgireport [sling:Folder]
   > N:bundlecol [cq:Component]
   > N:definitions [nt:unstructured]
   > P:groupable [Boolean] = true
   >```
   >

## 設定Report Framework服務 {#configuring-the-report-framework-services}

本節說明實作報表架構之OSGi服務的進階設定選項。

您可以使用網頁主控台的[設定]功能表（例如`http://localhost:4502/system/console/configMgr`提供）來檢視這些專案。 使用AEM時，有數種方法可管理此類服務的組態設定；請參閱[設定OSGi](/help/sites-deploying/configuring-osgi.md)以取得詳細資訊和建議的作法。

### 基本服務（Day CQ報告設定） {#basic-service-day-cq-reporting-configuration}

* **時區**&#x200B;定義建立時區歷史資料的時區。 這是為了確保歷史圖表可顯示全球每位使用者的相同資料。
* **地區設定**&#x200B;定義歷史資料要與&#x200B;**時區**&#x200B;搭配使用的地區設定。 地區設定是用來決定某些地區設定特定的行事曆設定（例如，一週的第一天是星期日還是星期一）。

* **快照路徑**&#x200B;定義儲存歷史圖表快照的根路徑。
* **報告的路徑**&#x200B;定義報告所在的路徑。 這由快照服務用來決定要實際製作快照的報表。
* **每日快照**&#x200B;定義每日快照的拍攝時間。 指定的小時在伺服器的本機時區中。
* **每小時快照**&#x200B;定義每小時快照的製作時間。
* **列（最大值）**&#x200B;定義每個快照所儲存的列數上限。 您應合理選擇此值。 如果太高，會影響存放庫的大小；如果太低，資料可能會因為歷史資料的處理方式而無法精確處理。
* **假資料**，若啟用，可使用`fakedata`選擇器建立假歷史資料；若停用，則使用`fakedata`選擇器會擲回例外狀況。

  因為資料是假的，所以它只能&#x200B;*只能*&#x200B;用於測試和偵錯。

  使用`fakedata`選擇器會以隱含方式完成報表，因此所有現有資料都會遺失。 資料可以手動還原，但此程式可能相當耗時。

* **快照使用者**&#x200B;定義了可用來建立快照的選用使用者。

  基本上，系統會為完成報表的使用者拍攝快照。 在某些情況下（例如，在發佈系統上，由於尚未復寫此使用者的帳戶，因此該使用者並不存在），您可能會想要指定改用的遞補使用者。

  此外，指定使用者可能會帶來安全性風險。

* **強制快照使用者**，如果啟用，則所有快照都是使用在&#x200B;*快照使用者*&#x200B;下指定的使用者來建立。 若未正確處理，可能會嚴重影響安全性。

### 快取設定（Day CQ報表快取） {#cache-settings-day-cq-reporting-cache}

* **啟用**&#x200B;可讓您啟用或停用報表資料的快取。 啟用報表快取可讓報表資料在數個請求期間保留在記憶體中。 這樣可能會提高效能，但會導致記憶體耗用率較高，在極端情況下可能會導致記憶體不足的情況。
* **TTL**&#x200B;定義快取報告資料的時間（秒）。 較高的數字可提升效能，但如果資料在時段內變更，也可能傳回不正確的資料。
* **最大專案數**&#x200B;定義了任何一次要快取的報表數量上限。

>[!NOTE]
>
>每個使用者和語言的報表資料可能不同。 因此，會根據報表、使用者和語言，快取報表資料。 這表示`2`的&#x200B;**最大專案**&#x200B;值實際上會快取下列任一專案的資料：
>
>* 一個報表，供擁有不同語言設定的兩個使用者使用
>* 一個使用者和兩個報告
>
