---
title: 頁面範本 — 靜態
description: 範本可用來建立頁面，並定義哪些元件可以在選取的範圍中使用
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
exl-id: b934ac41-78b9-497f-ba95-b05ef1e5660e
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1601'
ht-degree: 2%

---

# 頁面範本 — 靜態{#page-templates-static}

範本可用來建立頁面，並定義哪些元件可以在選取的範圍中使用。 範本是節點的階層，其結構與要建立的頁面相同，但沒有任何實際內容。

每個範本都會提供您一系列可供使用的元件。

* 範本是由[元件](/help/sites-developing/components.md)所建置；
* 元件使用並允許存取Widget，這些用於呈現內容。

>[!NOTE]
>
>[也提供可編輯的範本](/help/sites-developing/page-templates-editable.md)，為提供最大彈性和最新功能的建議範本型別。

## 範本的屬性和子節點 {#properties-and-child-nodes-of-a-template}

範本是cq：Template型別的節點，具有下列屬性和子節點：

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
   <td>目前的範本。 範本為節點型別cq：Template。<br /> </td>
  </tr>
  <tr>
   <td> allowedChildren </td>
   <td> String[]</td>
   <td>允許作為此範本之子範本的範本路徑。<br /> </td>
  </tr>
  <tr>
   <td> allowedParents</td>
   <td> String[]</td>
   <td>允許作為此範本之父範本的範本路徑。<br /> </td>
  </tr>
  <tr>
   <td> allowedPaths</td>
   <td> String[]</td>
   <td>允許以此範本為基礎的頁面路徑。<br /> </td>
  </tr>
  <tr>
   <td> jcr:created</td>
   <td> 日期</td>
   <td>建立範本的日期。<br /> </td>
  </tr>
  <tr>
   <td> jcr：description</td>
   <td> 字串</td>
   <td>範本的描述。<br /> </td>
  </tr>
  <tr>
   <td> jcr:title</td>
   <td> 字串</td>
   <td>範本的標題。<br /> </td>
  </tr>
  <tr>
   <td> 排名</td>
   <td> 長</td>
   <td>範本的排名。 用來在使用者介面中顯示範本。<br /> </td>
  </tr>
  <tr>
   <td> jcr：content</td>
   <td> cq:PageContent</td>
   <td>包含範本內容的節點。<br /> </td>
  </tr>
  <tr>
   <td> thumbnail.png</td>
   <td> nt：file</td>
   <td>範本的縮圖。<br /> </td>
  </tr>
  <tr>
   <td> icon.png</td>
   <td> nt：file</td>
   <td>範本的圖示。<br /> </td>
  </tr>
 </tbody>
</table>

範本是頁面的基礎。

若要建立頁面，必須將範本（節點樹狀結構`/apps/<myapp>/template/<mytemplate>`）複製到網站樹狀結構中的對應位置：如果使用&#x200B;**網站**&#x200B;索引標籤建立頁面，就會發生這種情況。

此複製動作也會提供頁面的初始內容（通常是僅限最上層內容）和屬性sling：resourceType，也就是用來呈現頁面的頁面元件路徑（子節點jcr：content中的所有專案）。

## 範本的結構方式 {#how-templates-are-structured}

我們需要考慮兩個方面：

* 範本本身的結構
* 使用範本時產生的內容結構

### 範本的結構 {#the-structure-of-a-template}

範本是在型別&#x200B;**cq：Template**&#x200B;的節點下建立。

![screen_shot_2012-02-13at63646pm](assets/screen_shot_2012-02-13at63646pm.png)

您可以設定各種屬性，特別是：

* **jcr：title** — 範本的標題；建立頁面時顯示在對話方塊中。
* **jcr：description** — 範本的說明；建立頁面時顯示在對話方塊中。

此節點包含jcr：content (cq：PageContent)節點，會用作結果頁面內容節點的基礎；這會使用sling：resourceType參考要用於呈現新頁面實際內容的元件。

![screen_shot_2012-02-13at64010pm](assets/screen_shot_2012-02-13at64010pm.png)

此元件用於在建立新頁面時定義內容的結構和設計。

![screen_shot_2012-02-13at64137pm](assets/screen_shot_2012-02-13at64137pm.png)

### 範本產生的內容 {#the-content-produced-by-a-template}

範本是用來建立型別`cq:Page`的頁面（如前所述，頁面是一種特殊型別的元件）。 每個AEM頁面都有結構化節點`jcr:content`。 此特性：

* 屬於cq：PageContent型別
* 是儲存已定義內容定義的結構化節點型別
* 具有屬性`sling:resourceType`，以參考包含用於轉譯內容之sling指令碼的元件

### 預設範本 {#default-templates}

AEM隨附各種現成可用的預設範本。 有時候，您可能會想要依原樣使用這些範本。 在此情況下，您必須確保範本可供您的網站使用。

例如，AEM提供數個範本，包括內容頁面和首頁。

| **標題** | **Component** | **位置** | **用途** |
|---|---|---|---|
| 首頁 | homepage | geometrixx | Geometrixx首頁範本。 |
| 內容頁面 | contentpage | geometrixx | Geometrixx內容頁面範本。 |

#### 顯示預設範本 {#displaying-default-templates}

若要檢視存放庫中所有範本的清單，請依照下列步驟進行：

1. 在CRXDE Lite中，開啟&#x200B;**工具**&#x200B;功能表並按一下&#x200B;**查詢**。

1. 在「查詢」索引標籤中
1. 以&#x200B;**型別**&#x200B;形式選取&#x200B;**XPath**。

1. 在&#x200B;**查詢**&#x200B;輸入欄位中，輸入下列字串：
//element(&#42;， cq：Template)

1. 按一下&#x200B;**執行**。 清單會顯示在結果方塊中。

通常，您會取用現有範本並開發新的範本以供您自己使用。 如需詳細資訊，請參閱[開發頁面範本](#developing-page-templates)。

若要為您的網站啟用現有的範本，並且您想要在從&#x200B;**網站**&#x200B;主控台直接在&#x200B;**網站**&#x200B;下建立頁面時，將它顯示在&#x200B;**建立頁面**&#x200B;對話方塊中，請將範本節點的allowedPaths屬性設定為： **/content(/。&#42;)？**

## 範本設計的套用方式 {#how-template-designs-are-applied}

當使用[設計模式](/help/sites-authoring/default-components-designmode.md)在UI中定義樣式時，設計會持續保留在要定義樣式的內容節點的確切路徑。

>[!CAUTION]
>
>Adobe建議僅透過[設計模式](/help/sites-authoring/default-components-designmode.md)套用設計。
>
>例如，在CRXDE Lite中修改設計不是最佳做法，此類設計的應用可能會與預期行為有所不同。

如果設計僅使用設計模式套用，則下列區段、[設計路徑解析度](/help/sites-developing/page-templates-static.md#design-path-resolution)、[決策樹](/help/sites-developing/page-templates-static.md#decision-tree)和[範例](/help/sites-developing/page-templates-static.md#example)不適用。

### 設計路徑解析 {#design-path-resolution}

根據靜態範本呈現內容時，AEM會嘗試根據內容階層的周遊情況，將最相關的設計和樣式套用至內容。

AEM會依照下列順序決定內容節點最相關的樣式：

* 如果內容節點的完整確切路徑有設計（如同在設計模式中定義設計一樣），則使用該設計。
* 如果存在父項內容節點的設計，則使用該設計。
* 如果內容節點的路徑上有任何節點的設計，則使用該設計。

在後兩種情況下，如果有多個適用的設計，請使用最接近內容節點的設計。

### 決策樹 {#decision-tree}

這是[設計路徑解析](/help/sites-developing/page-templates-static.md#design-path-resolution)邏輯的圖形表示。

![design_path_resolution](assets/design_path_resolution.png)

### 範例 {#example}

請考量簡單的內容結構，如下所示，其中設計可套用至任何節點：

`/root/branch/leaf`

下表說明AEM如何選擇設計。

<table>
 <tbody>
  <tr>
   <td><strong>尋找設計對象<br /> </strong></td>
   <td><strong>設計存在於<br /> </strong></td>
   <td><strong>已選擇設計<br /> </strong></td>
   <td><strong>評論</strong></td>
  </tr>
  <tr>
   <td><code class="code">leaf
      </code></td>
   <td><p><code>root</code></p> <p><code>branch</code></p> <p><code>leaf</code></p> </td>
   <td><code>leaf</code></td>
   <td>一律採用最相符的專案。<br /> </td>
  </tr>
  <tr>
   <td><code>leaf</code></td>
   <td><p><code>root</code></p> <p><code>branch</code></p> </td>
   <td><code>branch</code></td>
   <td>回復到樹狀結構中最接近的下層相符專案。</td>
  </tr>
  <tr>
   <td><code>leaf</code></td>
   <td><code>root</code></td>
   <td><code>root</code></td>
   <td>如果其他所有專案都失敗，則取用剩餘的專案。<br /> </td>
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
   <td><p>如果沒有完全相符的專案，請取樹狀結構中較低的一個。</p> <p>假設這永遠適用，但樹狀結構往上可能太具體。<br /> </p> </td>
  </tr>
 </tbody>
</table>

## 開發頁面範本 {#developing-page-templates}

AEM頁面範本只是用來建立頁面的模型。 它們可以視需要包含儘可能少或儘可能多的初始內容，其角色是建立正確的初始節點結構，並將所需的屬性（主要是sling：resourceType）設定為允許編輯和呈現。

### 建立範本（根據現有範本） {#creating-a-new-template-based-on-an-existing-template}

新範本可以完全從頭建立，但通常會複製現有範本並更新，以節省您的時間和精力。 例如，Geometrixx中的範本可以用來協助您開始使用。

若要根據現有範本建立範本：

1. 將現有範本（最好使用儘可能接近您要達成之定義的範本）複製到新節點。

   範本儲存在&#x200B;**/apps/&lt;website-name>/templates/&lt;template-name>**&#x200B;中。

   >[!NOTE]
   >
   >可用範本的清單取決於新頁面的位置以及每個範本中指定的位置限制。 檢視[範本可用性](#templateavailibility)。

1. 變更新範本節點的&#x200B;**jcr：title**&#x200B;以反映其新角色。 您也可以更新&#x200B;**jcr：description** （如果適用）。 請務必視需要變更頁面的範本可用性。

   >[!NOTE]
   >
   >如果您想要在從&#x200B;**網站**&#x200B;主控台直接在&#x200B;**網站**&#x200B;下建立頁面時，在&#x200B;**建立頁面**&#x200B;對話方塊中顯示範本，請將範本節點的`allowedPaths`屬性設定為： `/content(/.*)?`

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. 複製範本所依據的元件（由範本內&#x200B;**jcr：content**&#x200B;節點的&#x200B;**sling：resourceType**&#x200B;屬性表示）以建立執行個體。

   元件儲存在&#x200B;**/apps/&lt;website-name>/components/&lt;component-name>**。

1. 更新新元件的&#x200B;**jcr：title**&#x200B;和&#x200B;**jcr：description**。
1. 如果您想要在範本選取範圍清單中顯示新的縮圖圖片（大小為128 x 98畫素），請取代thumbnail.png。
1. 更新範本&#x200B;**jcr：content**&#x200B;節點的&#x200B;**sling：resourceType**&#x200B;以參考新元件。
1. 對範本或其基礎元件（或兩者）的功能或設計進行其他變更。

   >[!NOTE]
   >
   >對&#x200B;**/apps/&lt;website>/templates/&lt;template-name>**&#x200B;節點所做的變更會影響範本執行個體（如選取專案清單中所示）。
   >
   >
   >對&#x200B;**/apps/&lt;website>/components/&lt;component-name>**&#x200B;節點所做的變更會影響使用範本時建立的內容頁面。

   您現在可以使用新範本在您的網站中建立頁面。

>[!NOTE]
>
>編輯器使用者端程式庫假設內容頁面中存在`cq.shared`名稱空間，如果沒有，則會產生JavaScript錯誤`Uncaught TypeError: Cannot read property 'shared' of undefined`。
>
>所有範例內容頁面都包含`cq.shared`，因此任何以這些頁面為基礎的內容都會自動包含`cq.shared`。 但是，如果您決定從頭開始建立自己的內容頁面，而不根據範例內容，則必須確定包括`cq.shared`名稱空間。
>
>如需進一步資訊，請參閱[使用使用者端資料庫](/help/sites-developing/clientlibs.md)。

## 讓現有範本可供使用 {#making-an-existing-template-available}

此範例說明如何允許範本用於特定內容路徑。 建立頁面時可供頁面作者使用的範本是由[範本可用性](/help/sites-developing/templates.md#template-availability)中定義的邏輯所決定。

1. 在CRXDE Lite中，導覽至您要用於頁面的範本，例如Newsletter範本。
1. 變更[範本可用性](/help/sites-developing/templates.md#template-availability)的`allowedPaths`屬性及其他屬性。 例如，`allowedPaths`： `/content/geometrixx-outdoors/[^/]+(/.*)?`表示此範本允許在`/content/geometrixx-outdoors`下的任何路徑中。

   ![chlimage_1-89](assets/chlimage_1-89.png)
