---
title: 頁面模板 — 靜態
seo-title: Page Templates - Static
description: 模板用於建立頁面並定義可在所選範圍內使用的元件
seo-description: A Template is used to create a Page and defines which components can be used within the selected scope
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
source-wordcount: '1626'
ht-degree: 1%

---

# 頁面模板 — 靜態{#page-templates-static}

「模板」用於建立頁面，並定義可在選定範圍內使用的元件。 模板是節點的層次結構，其結構與要建立的頁面相同，但沒有任何實際內容。

每個模板都將為您提供可供使用的元件選擇。

* 模板由 [元件](/help/sites-developing/components.md);
* 元件使用和允許訪問小部件，這些部件用於呈現內容。

>[!NOTE]
>
>[可編輯模板](/help/sites-developing/page-templates-editable.md) 也是最靈活和最新功能的推薦模板類型。

## 模板的屬性和子節點 {#properties-and-child-nodes-of-a-template}

模板是cq:Template類型的節點，具有以下屬性和子節點：

<table>
 <tbody>
  <tr>
   <td><strong>名稱 <br /> </strong></td>
   <td><strong>類型 <br /> </strong></td>
   <td><strong>說明 <br /> </strong></td>
  </tr>
  <tr>
   <td>. <br /> </td>
   <td> cq:Template</td>
   <td>當前模板。 模板為節點類型cq:Template。<br /> </td>
  </tr>
  <tr>
   <td> 允許的子項 </td>
   <td> 字串[]</td>
   <td>允許作為此模板子項的模板的路徑。<br /> </td>
  </tr>
  <tr>
   <td> 允許父項</td>
   <td> 字串[]</td>
   <td>允許作為此模板父級的模板的路徑。<br /> </td>
  </tr>
  <tr>
   <td> 允許的路徑</td>
   <td> 字串[]</td>
   <td>允許基於此模板的頁面的路徑。<br /> </td>
  </tr>
  <tr>
   <td> jcr:created</td>
   <td> 日期</td>
   <td>模板的建立日期。<br /> </td>
  </tr>
  <tr>
   <td> jcr：說明</td>
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
   <td>模板的級別。 用於在用戶介面中顯示模板。<br /> </td>
  </tr>
  <tr>
   <td> jcr：內容</td>
   <td> cq:PageContent</td>
   <td>包含模板內容的節點。<br /> </td>
  </tr>
  <tr>
   <td> thumbnail.png</td>
   <td> nt：檔案</td>
   <td>模板的縮略圖。<br /> </td>
  </tr>
  <tr>
   <td> icon.png</td>
   <td> nt：檔案</td>
   <td>模板的表徵圖。<br /> </td>
  </tr>
 </tbody>
</table>

模板是頁面的基礎。

要建立頁面，必須複製模板（節點 — 樹） `/apps/<myapp>/template/<mytemplate>`)到站點樹中的相應位置：如果使用 **網站** 頁籤。

此複製操作還為頁面提供其初始內容（通常僅限頂級內容）和屬性sling:resourceType，用於呈現頁面的頁面元件的路徑（子節點jcr:content中的所有內容）。

## 模板的結構 {#how-templates-are-structured}

需要考慮兩個方面：

* 模板本身的結構
* 使用模板時生成的內容的結構

### 模板的結構 {#the-structure-of-a-template}

在類型的節點下建立模板 **cq：模板**。

![screen_shot_2012-02-13at63646pm](assets/screen_shot_2012-02-13at63646pm.png)

可以設定各種屬性，特別是：

* **jcr：標題**  — 模板的標題；建立頁面時顯示。
* **jcr：說明**  — 模板說明；建立頁面時顯示。

該節點包含一個jcr:content(cq:PageContent)節點，該節點用作生成頁面的內容節點的基礎；此引用使用sling:resourceType，用於呈現新頁面的實際內容的元件。

![screen_shot_2012-02-13at64010pm](assets/screen_shot_2012-02-13at64010pm.png)

建立新頁面時，此元件用於定義內容的結構和設計。

![screen_shot_2012-02-13at64137pm](assets/screen_shot_2012-02-13at64137pm.png)

### 模板生成的內容 {#the-content-produced-by-a-template}

模板用於建立類型的頁面 `cq:Page` （如前所述，頁面是特殊類型的元件）。 每個AEM頁面都有結構化節點 `jcr:content`。 此特性：

* 為cq:PageContent類型
* 是保存已定義內容定義的結構化節點類型
* 有一個 `sling:resourceType` 引用用於呈現內容的sling指令碼的元件

### 預設模板 {#default-templates}

附AEM加了許多現成的預設模板。 在某些情況下，您可能希望按原樣使用模板。 在這種情況下，您需要確保該模板可用於您的網站。

例如，附AEM帶了多個模板，包括內容頁和首頁。

| **標題** | **Component** | **位置** | **用途** |
|---|---|---|---|
| 首頁 | homepage | 幾何 | Geometrixx首頁模板。 |
| 內容頁面 | 內容頁 | 幾何 | Geometrixx內容頁面模板。 |

#### 顯示預設模板 {#displaying-default-templates}

要查看儲存庫中所有模板的清單，請按如下步驟操作：

1. 在CRXDE Lite中，開啟 **工具** 的 **查詢**。

1. 在「查詢」頁籤中
1. 作為 **類型**&#x200B;選中 **XPath**。

1. 在 **查詢** 輸入欄位，輸入以下字串：//element(&#42;, cq：模板)

1. 按一下 **執行**。 清單顯示在結果框中。

在大多數情況下，您將使用現有模板並開發一個新模板供您使用。 請參閱 [開發頁面模板](#developing-page-templates) 的子菜單。

為網站啟用現有模板，並希望其顯示在 **建立頁** 在下面建立頁面時 **網站** 從 **網站** 控制台，將模板節點的allowedPaths屬性設定為： **/content(/)。&#42;)?**

## 模板設計的應用方式 {#how-template-designs-are-applied}

在UI中定義樣式時使用 [設計模式](/help/sites-authoring/default-components-designmode.md)，設計將保留在為其定義樣式的內容節點的準確路徑上。

>[!CAUTION]
>
>Adobe建議僅通過 [設計模式](/help/sites-authoring/default-components-designmode.md)。
>
>例如，在CRX DE中修改設計不是最佳做法，這種設計的應用可能與預期行為不同。

如果僅使用「設計模式」應用設計，則下面各節： [設計路徑解析](/help/sites-developing/page-templates-static.md#design-path-resolution)。 [決策樹](/help/sites-developing/page-templates-static.md#decision-tree)的 [示例](/help/sites-developing/page-templates-static.md#example) 不適用。

### 設計路徑解析 {#design-path-resolution}

當基於靜態模板呈現內容時，AEM將嘗試基於對內容分層結構的遍歷將最相關的設計和樣式應用到內容。

按AEM以下順序確定內容節點的最相關樣式：

* 如果存在內容節點的完整和精確路徑的設計（如在「設計模式」中定義設計時），則使用該設計。
* 如果父項的內容節點有設計，則使用該設計。
* 如果內容節點路徑上的任何節點都有設計，則使用該設計。

在最後兩種情況下，如果有多種適用的設計，請使用最接近內容節點的設計。

### 決策樹 {#decision-tree}

這是 [設計路徑解析](/help/sites-developing/page-templates-static.md#design-path-resolution) 邏輯。

![design_path_resolution](assets/design_path_resolution.png)

### 範例 {#example}

請考慮如下簡單的內容結構，其中設計可應用於任何節點：

`/root/branch/leaf`

下表說明了如AEM何選擇設計。

<table>
 <tbody>
  <tr>
   <td><strong>查找設計<br /> </strong></td>
   <td><strong>存在的設計<br /> </strong></td>
   <td><strong>選擇的設計<br /> </strong></td>
   <td><strong>評論</strong></td>
  </tr>
  <tr>
   <td><code class="code">leaf
      </code></td>
   <td><p><code>root</code></p> <p><code>branch</code></p> <p><code>leaf</code></p> </td>
   <td><code>leaf</code></td>
   <td>最精確的匹配總是被選中。<br /> </td>
  </tr>
  <tr>
   <td><code>leaf</code></td>
   <td><p><code>root</code></p> <p><code>branch</code></p> </td>
   <td><code>branch</code></td>
   <td>掉到樹下最接近的匹配位置。</td>
  </tr>
  <tr>
   <td><code>leaf</code></td>
   <td><code>root</code></td>
   <td><code>root</code></td>
   <td>如果其他所有方法都失敗，就拿剩下的東西。<br /> </td>
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
   <td><p>如果沒有完全匹配，請把樹上的那個拿下。</p> <p>假設這永遠適用，但更上一層樹可能過於具體。<br /> </p> </td>
  </tr>
 </tbody>
</table>

## 開發頁面模板 {#developing-page-templates}

頁AEM面模板只是用於建立新頁面的模型。 它們可以根據需要包含少量或盡可能多的初始內容，其角色是建立正確的初始節點結構，並將所需屬性（主要是sling:resourceType）設定為允許編輯和呈現。

### 建立新模板（基於現有模板） {#creating-a-new-template-based-on-an-existing-template}

不用說，可以從頭開始完全建立新模板，但通常會複製和更新現有模板，以節省您的時間和精力。 例如，Geometrixx中的模板可用於啟動。

要基於現有模板建立新模板，請執行以下操作：

1. 將現有模板（最好將定義盡可能接近要達到的目標）複製到新節點。

   模板通常儲存在 **/apps/&lt;website-name>/templates/&lt;template-name>**。

   >[!NOTE]
   >
   >可用模板清單取決於新頁面的位置以及在每個模板中指定的放置限制。 請參閱 [模板可用性](#templateavailibility)。

1. 更改 **jcr：標題** 來反映其新角色。 您還可以更新 **jcr：說明** 如果合適。 確保根據需要更改頁面的模板可用性。

   >[!NOTE]
   >
   >如果希望模板顯示在 **建立頁** 在下面建立頁面時 **網站** 從 **網站** 控制台，設定 `allowedPaths` 模板節點的屬性： `/content(/.*)?`

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. 複製模板所基於的元件(由 **sling:resourceType** 屬性 **jcr：內容** 節點)以建立新實例。

   元件通常儲存在 **/apps/&lt;website-name>/元件/&lt;component-name>**。

1. 更新 **jcr：標題** 和 **jcr：說明** 的子菜單。
1. 如果希望在模板選擇清單中顯示新的縮略圖，請替換thumbnail.png（大小為128 x 98像素）。
1. 更新 **sling:resourceType** 的 **jcr：內容** 節點以引用新元件。
1. 對模板和/或其基礎元件的功能或設計進行任何進一步更改。

   >[!NOTE]
   >
   >對 **/apps/&lt;website>/templates/&lt;template-name>** 節點將影響模板實例（如在選擇清單中）。
   對 **/apps/&lt;website>/元件/&lt;component-name>** 節點將影響使用模板時建立的內容頁面。

   現在，您可以使用新模板在網站內建立頁面。

>[!NOTE]
編輯器客戶端庫假定 `cq.shared` 內容頁中的命名空間，如果不存在JavaScript錯誤 `Uncaught TypeError: Cannot read property 'shared' of undefined` 將產生結果。
所有示例內容頁包含 `cq.shared`，因此基於它們的任何內容都自動包括 `cq.shared`。 但是，如果您決定從頭開始建立自己的內容頁面而不根據示例內容進行建立，則必須確保包括 `cq.shared` 命名空間。
請參閱 [使用客戶端庫](/help/sites-developing/clientlibs.md) 的上界。

## 使現有模板可用 {#making-an-existing-template-available}

此示例說明如何允許模板用於某些內容路徑。 建立新頁面時頁面作者可用的模板由中定義的邏輯確定 [模板可用性](/help/sites-developing/templates.md#template-availability)。

1. 在CRXDE Lite中，導航到要用於頁面的模板，例如新聞簡訊模板。
1. 更改 `allowedPaths` 用之物業及其他物業 [模板可用性](/help/sites-developing/templates.md#template-availability)。 比如說， `allowedPaths`: `/content/geometrixx-outdoors/[^/]+(/.*)?` 表示在以下任何路徑中都允許此模板 `/content/geometrixx-outdoors`。

   ![chlimage_1-89](assets/chlimage_1-89.png)
