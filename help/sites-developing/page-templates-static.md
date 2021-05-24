---
title: 頁面範本 — 靜態
seo-title: 頁面範本 — 靜態
description: 模板用於建立頁面，並定義哪些元件可在選定範圍內使用
seo-description: 模板用於建立頁面，並定義哪些元件可在選定範圍內使用
uuid: 7a473c19-9565-476e-9e54-ab179da04d71
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: cfd90e8f-9b9b-4d0b-be31-828469b961de
docset: aem65
exl-id: b934ac41-78b9-497f-ba95-b05ef1e5660e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1648'
ht-degree: 1%

---

# 頁面範本 — 靜態{#page-templates-static}

模板用於建立頁面，並定義哪些元件可在選定範圍內使用。 範本是節點的階層，其結構與要建立的頁面相同，但沒有任何實際內容。

每個範本都會提供一系列可供使用的元件。

* 範本由[元件](/help/sites-developing/components.md)組成；
* 元件使用和允許訪問介面工具集，這些元件用於呈現內容。

>[!NOTE]
>
>[也提](/help/sites-developing/page-templates-editable.md) 供可編輯的範本，且為最具彈性和最新功能的建議範本類型。

## 模板{#properties-and-child-nodes-of-a-template}的屬性和子節點

範本是cq:Template類型的節點，具有以下屬性和子節點：

<table>
 <tbody>
  <tr>
   <td><strong>名稱 <br /> </strong></td>
   <td><strong>類型 <br /> </strong></td>
   <td><strong>說明 <br /> </strong></td>
  </tr>
  <tr>
   <td>.<br /> </td>
   <td> cq:Template</td>
   <td>目前的範本。 範本的節點類型為cq:Template。<br /> </td>
  </tr>
  <tr>
   <td> allowedChildren </td>
   <td> String[]</td>
   <td>允許作為此模板子項的模板的路徑。<br /> </td>
  </tr>
  <tr>
   <td> allowedParents</td>
   <td> 字串[]</td>
   <td>允許作為此模板父項的模板的路徑。<br /> </td>
  </tr>
  <tr>
   <td> allowedPaths</td>
   <td> 字串[]</td>
   <td>允許基於此模板的頁的路徑。<br /> </td>
  </tr>
  <tr>
   <td> jcr:created</td>
   <td> 日期</td>
   <td>建立模板的日期。<br /> </td>
  </tr>
  <tr>
   <td> jcr:description</td>
   <td> 字串</td>
   <td>模板的說明。<br /> </td>
  </tr>
  <tr>
   <td> jcr:title</td>
   <td> 字串</td>
   <td>模板的標題。<br /> </td>
  </tr>
  <tr>
   <td> 排名</td>
   <td> 長整數</td>
   <td>範本的排名。 用於在用戶介面中顯示模板。<br /> </td>
  </tr>
  <tr>
   <td> jcr:content</td>
   <td> cq:PageContent</td>
   <td>包含模板內容的節點。<br /> </td>
  </tr>
  <tr>
   <td> thumbnail.png</td>
   <td> nt:file</td>
   <td>模板的縮略圖。<br /> </td>
  </tr>
  <tr>
   <td> icon.png</td>
   <td> nt:file</td>
   <td>模板的表徵圖。<br /> </td>
  </tr>
 </tbody>
</table>

範本是頁面的基礎。

要建立頁面，必須將模板（節點樹`/apps/<myapp>/template/<mytemplate>`）複製到站點樹中的相應位置：如果使用&#x200B;**Websites**&#x200B;標籤建立頁面，就會發生此情況。

此複製動作也會提供頁面的初始內容（通常僅限頂層內容）和屬性sling:resourceType，用於轉譯頁面的頁面元件路徑（子節點jcr:content中的所有內容）。

## 範本的結構方式{#how-templates-are-structured}

需要考慮兩個方面：

* 模板本身的結構
* 使用範本時產生的內容結構

### 模板{#the-structure-of-a-template}的結構

在&#x200B;**cq:Template**&#x200B;類型的節點下建立模板。

![screen_shot_2012-02-13at63646pm](assets/screen_shot_2012-02-13at63646pm.png)

可以設定各種屬性，特別是：

* **jcr:title**  — 範本的title;建立頁面時顯示在對話方塊中。
* **jcr:description**  — 範本的說明；建立頁面時顯示在對話方塊中。

此節點包含jcr:content(cq:PageContent)節點，可作為產生頁面之內容節點的基礎；這會參考，使用sling:resourceType，用於轉譯新頁面實際內容的元件。

![screen_shot_2012-02-13at64010pm](assets/screen_shot_2012-02-13at64010pm.png)

建立新頁面時，此元件用於定義內容的結構和設計。

![screen_shot_2012-02-13at64137pm](assets/screen_shot_2012-02-13at64137pm.png)

### 範本{#the-content-produced-by-a-template}產生的內容

範本可用來建立`cq:Page`類型的頁面（如前所述，頁面是特殊類型的元件）。 每個AEM頁面都有一個結構化節點`jcr:content`。 此特性：

* 屬於cq:PageContent類型
* 是包含定義內容定義的結構化節點類型
* 具有`sling:resourceType`屬性，可參考保有用於轉譯內容的sling指令碼的元件

### 預設模板{#default-templates}

AEM隨附許多可立即使用的預設範本。 在某些情況下，您可能會想要依原樣使用範本。 在此情況下，您必須確保範本可供您的網站使用。

例如，AEM隨附數個範本，包括內容頁面和首頁。

| **標題** | **元件** | **位置** | **用途** |
|---|---|---|---|
| 首頁 | homepage | geometrixx | Geometrixx首頁模板。 |
| 內容頁面 | contentpage | geometrixx | Geometrixx內容頁面範本。 |

#### 顯示預設模板{#displaying-default-templates}

要查看儲存庫中所有模板的清單，請按如下步驟操作：

1. 在CRXDE Lite中，開啟&#x200B;**工具**&#x200B;菜單，然後按一下&#x200B;**查詢**。

1. 在查詢索引標籤中
1. 作為&#x200B;**類型**，選擇&#x200B;**XPath**。

1. 在&#x200B;**Query**輸入欄位中，輸入以下字串：
//element(*, cq:Template)

1. 按一下&#x200B;**執行**。 清單顯示在結果框中。

在大多數情況下，您會取用現有範本，並開發新範本供您自用。 如需詳細資訊，請參閱[開發頁面範本](#developing-page-templates) 。

若要為您的網站啟用現有範本，並希望在從&#x200B;**網站**&#x200B;控制台的&#x200B;**網站**&#x200B;下建立頁面時，該範本顯示在&#x200B;**建立頁面**&#x200B;對話方塊中，請將範本節點的allowedPaths屬性設定為：**/content(/)。*)?**

## 如何套用範本設計{#how-template-designs-are-applied}

使用[設計模式](/help/sites-authoring/default-components-designmode.md)在UI中定義樣式時，設計會保存在要為其定義樣式的內容節點的確切路徑上。

>[!CAUTION]
>
>Adobe建議僅透過[設計模式](/help/sites-authoring/default-components-designmode.md)套用設計。
>
>例如，在CRX DE中修改設計並非最佳作法，且此類設計的應用可能會與預期行為不同。

如果設計僅使用設計模式應用，則以下部分[設計路徑解析度](/help/sites-developing/page-templates-static.md#design-path-resolution)、[決策樹](/help/sites-developing/page-templates-static.md#decision-tree)和[示例](/help/sites-developing/page-templates-static.md#example)不適用。

### 設計路徑解析度{#design-path-resolution}

根據靜態範本轉譯內容時，AEM會嘗試根據內容階層的周遊情形，將最相關的設計和樣式套用至內容。

AEM會依下列順序決定內容節點最相關的樣式：

* 如果有內容節點完整且精確路徑的設計（如在「設計模式」中定義設計時），則使用該設計。
* 如果父項的內容節點有設計，則使用該設計。
* 如果內容節點路徑上的任何節點都有設計，則使用該設計。

在最後兩種情況中，如果有多個適用的設計，請使用最接近內容節點的設計。

### 決策樹{#decision-tree}

這是[設計路徑解析](/help/sites-developing/page-templates-static.md#design-path-resolution)邏輯的圖形表示。

![design_path_resolution](assets/design_path_resolution.png)

### 範例 {#example}

請考慮如下的簡單內容結構，其中設計可應用於任何節點：

`/root/branch/leaf`

下表說明AEM將如何選擇設計。

<table>
 <tbody>
  <tr>
   <td><strong>尋找設計<br /> </strong></td>
   <td><strong>設計適用於<br /> </strong></td>
   <td><strong>已選擇設計<br /> </strong></td>
   <td><strong>評論</strong></td>
  </tr>
  <tr>
   <td><code class="code">leaf
      </code></td>
   <td><p><code>root</code></p> <p><code>branch</code></p> <p><code>leaf</code></p> </td>
   <td><code>leaf</code></td>
   <td>始終進行最準確的匹配。<br /> </td>
  </tr>
  <tr>
   <td><code>leaf</code></td>
   <td><p><code>root</code></p> <p><code>branch</code></p> </td>
   <td><code>branch</code></td>
   <td>回復到樹下最接近的匹配。</td>
  </tr>
  <tr>
   <td><code>leaf</code></td>
   <td><code>root</code></td>
   <td><code>root</code></td>
   <td>如果其他所有失敗，則取剩餘的。<br /> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><code>branch</code></td>
   <td><code>branch</code></td>
   <td> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><p><code>branch</code></p> <p><code class="code">leaf
       </code></p> </td>
   <td><code>branch</code></td>
   <td> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><p><code>root</code></p> <p><code class="code">branch
       </code></p> </td>
   <td><code>branch</code></td>
   <td> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><p><code>root</code></p> <p><code class="code">leaf
       </code></p> </td>
   <td><code>root</code></td>
   <td><p>如果沒有完全匹配，請取樹中的下一個。</p> <p>假設這將始終適用，但更上一層樹可能過於具體。<br /> </p> </td>
  </tr>
 </tbody>
</table>

## 開發頁面範本{#developing-page-templates}

AEM頁面範本只是用來建立新頁面的模型。 它們可視需要包含盡量少或多的初始內容，其角色為建立正確的初始節點結構，並將必要屬性（主要是sling:resourceType）設為允許編輯和轉譯。

### 建立新模板（基於現有模板）{#creating-a-new-template-based-on-an-existing-template}

不用說，您可以從頭開始完全建立新範本，但經常會複製並更新現有範本，以節省時間和精力。 例如，您可以使用Geometrixx中的範本來開始使用。

要根據現有模板建立新模板：

1. 將現有範本（最好以盡可能接近您想要達到的定義）複製到新節點。

   範本通常儲存在&#x200B;**/apps/&lt;website-name>/templates/&lt;template-name>**&#x200B;中。

   >[!NOTE]
   >
   >可用的範本清單取決於新頁面的位置，以及每個範本中指定的位置限制。 請參閱[範本可用性](#templateavailibility)。

1. 變更新範本節點的&#x200B;**jcr:title**&#x200B;以反映其新角色。 您也可以視需要更新&#x200B;**jcr:description**。 請務必視需要變更頁面的範本可用性。

   >[!NOTE]
   >
   >如果希望在從&#x200B;**網站**&#x200B;控制台在&#x200B;**網站**&#x200B;下建立頁面時，模板顯示在&#x200B;**建立頁面**&#x200B;對話框中，請將模板節點的`allowedPaths`屬性設定為：`/content(/.*)?`

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. 複製範本所依據的元件（由範本內&#x200B;**jcr:content**&#x200B;節點的&#x200B;**sling:resourceType**&#x200B;屬性指示）以建立新例項。

   元件通常儲存在&#x200B;**/apps/&lt;website-name>/components/&lt;component-name>**&#x200B;中。

1. 更新新元件的&#x200B;**jcr:title**&#x200B;和&#x200B;**jcr:description**。
1. 如果您想要在範本選取清單中顯示新的縮圖圖片，請取代thumbnail.png（大小為128 x 98 px）。
1. 更新範本&#x200B;**jcr:content**&#x200B;節點的&#x200B;**sling:resourceType**&#x200B;以參考新元件。
1. 對範本和/或其基礎元件的功能或設計進行任何進一步變更。

   >[!NOTE]
   >
   >對&#x200B;**/apps/&lt;website>/templates/&lt;template-name>**&#x200B;節點所做的更改將影響模板實例（如選擇清單中）。
   對&#x200B;**/apps/&lt;website>/components/&lt;component-name>**&#x200B;節點所做的變更，將影響使用範本時建立的內容頁面。

   您現在可以使用新範本在網站中建立頁面。

>[!NOTE]
編輯器用戶端程式庫會假設內容頁面中存在`cq.shared`命名空間，如果命名空間不存在，則會導致JavaScript錯誤`Uncaught TypeError: Cannot read property 'shared' of undefined`。
所有範例內容頁面皆包含`cq.shared`，因此任何以這些頁面為基礎的內容都會自動包含`cq.shared`。 不過，如果您決定從草稿開始建立自己的內容頁面，而不以範例內容為基礎，則必須確定包含`cq.shared`命名空間。
如需詳細資訊，請參閱[使用用戶端程式庫](/help/sites-developing/clientlibs.md)。

## 使現有模板可用{#making-an-existing-template-available}

此範例說明如何允許將範本用於特定內容路徑。 建立新頁面時頁面作者可用的範本，由[Template Availability](/help/sites-developing/templates.md#template-availability)中定義的邏輯決定。

1. 在CRXDE Lite中，導覽至您要用於頁面的範本，例如電子報範本。
1. 更改用於[模板可用性](/help/sites-developing/templates.md#template-availability)的`allowedPaths`屬性和其他屬性。 例如， `allowedPaths`:`/content/geometrixx-outdoors/[^/]+(/.*)?`表示可在`/content/geometrixx-outdoors`下的任何路徑中使用此範本。

   ![chlimage_1-89](assets/chlimage_1-89.png)
