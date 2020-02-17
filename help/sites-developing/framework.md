---
title: AEM標籤架構
seo-title: AEM標籤架構
description: 標籤內容並運用AEM標籤基礎架構
seo-description: 標籤內容並運用AEM標籤基礎架構
uuid: f80a2cb1-359f-41dd-a70b-626d92cc3d4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: f69db472-9f5c-4c0d-9292-2920ef69feeb
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# AEM標籤架構{#aem-tagging-framework}

若要標籤內容並運用AEM標籤基礎架構：

* 標籤必須作為分類根節點下 ` [cq:Tag](#tags-cq-tag-node-type)` 的類 [型節點](#taxonomy-root-node)

* 標籤內容節點的NodeType必須包含混 [`cq:Taggable`](#taggable-content-cq-taggable-mixin) 合
* TagID [會新增至內容節點的屬](#tagid) 性， [`cq:tags`](#tagged-content-cq-tags-property) 並解析至類型的節點 ` [cq:Tag](#tags-cq-tag-node-type)`

## 標籤：cq：標籤節點類型 {#tags-cq-tag-node-type}

標籤的聲明在儲存庫中捕獲，其類型為 `cq:Tag.`

標籤可以是簡單單字（例如，sky）或表示階層式分類法（例如，水果／蘋果，即通用水果和更具體的蘋果）。

標籤由唯一的TagID識別。

標籤包含可選的中繼資訊，例如標題、本地化標題和說明。 標題應顯示在使用者介面中，而非TagID（若有）。

標籤框架也能夠限製作者和網站訪客僅使用特定、預先定義的標籤。

### 標籤特性 {#tag-characteristics}

* 節點類型為 `cq:Tag`
* 節點名稱是 ` [TagID](#tagid)`
* 一律 ` [TagID](#tagid)` 包含命名空 [間](#tag-namespace)

* 可選 `jcr:title` 屬性（要在UI中顯示的標題）

* 可選屬 `jcr:description` 性

* 包含子節點時，稱為容 [器標籤](#container-tags)
* 儲存在名為分類根節點的基本路徑下 [的儲存庫中](#taxonomy-root-node)

### 標記 ID {#tagid}

TagID標識解析到儲存庫中標籤節點的路徑。

通常，TagID是以命名空間開始的速記TagID，也可以是從分類根節點開始的絕 [對TagID](#taxonomy-root-node)。

標籤內容時，如果內容尚不存在，則 ` [cq:tags](#tagged-content-cq-tags-property)` 會將屬性添加到內容節點中，並將TagID添加到屬性的字串陣列值中。

TagID包含命名空 [間](#tag-namespace) ，後面接著本機TagID。 [容器標籤](#container-tags) ，具有子標籤，代表分類法中的階層順序。 子標籤可用來參照與任何本機TagID相同的標籤。 例如，即使內容是含有子標籤的容器標籤，例如「水果／蘋果」和「水果／香蕉」，也允許使用「水果」標籤內容。

### 分類根節點 {#taxonomy-root-node}

分類根節點是儲存庫中所有標籤的基本路徑。 分類根節點不 *能* 是類型的節點 `  cq   :Tag`。

在AEM中，基本路徑為 `/content/  cq   :tags` 根節點類型 `  cq   :Folder`。

### 標籤命名空間 {#tag-namespace}

名稱空間允許將事物分組。 最典型的使用案例是每個（網站）網站（例如，公用、內部和入口網站）或每個大型應用程式（例如WCM、資產、社群）擁有命名空間，但命名空間可用於各種其他需求。 使用者介面中使用名稱空間，僅顯示適用於目前內容的標籤子集（即特定名稱空間的標籤）。

標籤的命名空間是分類子樹中的第一級，該子樹是緊接在分類根節點下 [的節點](#taxonomy-root-node)。 namespace是父代不是節 `cq:Tag` 點類型的節 `cq:Tag`點類型。

所有標籤都有命名空間。 如果未指定命名空間，則標籤會指派給預設命名空間，即TagID `default` (標題 `Standard Tags),`是 `/content/cq:tags/default.`

### 容器標籤 {#container-tags}

容器標籤是包含任意數 `cq:Tag` 目和類型子節點的類型節點，因此可以使用自訂中繼資料來增強標籤模型。

此外，分類法中的容器標籤（或超標籤）是所有子標籤的子總和：例如，使用水果／蘋果標籤的內容也被視為使用水果標籤，即搜索僅使用水果標籤的內容也會查找使用水果／蘋果標籤的內容。

### 解析TagID {#resolving-tagids}

如果標籤ID包含冒號&quot;:&quot;，冒號會將名稱空間與標籤或子分類分類分開，然後使用正常斜槓&quot;/&quot;分開。 如果標籤ID沒有冒號，則會隱含預設命名空間。

標籤的標準和唯一位置位於/content/cq:tags下方。

參考非現有路徑或路徑的標籤不指向cq：標籤節點被視為無效且被忽略。

下表顯示一些TagID範例、其元素，以及TagID解析為儲存庫中絕對路徑的方式：

下表顯示一些TagID範例、其元素，以及TagID解析為儲存庫中絕對路徑的方式：下表顯示一些TagID範例、其元素，以及TagID解析為儲存庫中絕對路徑的方式：

<table>
 <tbody>
  <tr>
   <td><strong>標記 ID<br /> </strong></td>
   <td><strong>命名空間</strong></td>
   <td><strong>本機ID</strong></td>
   <td><strong>容器標籤</strong></td>
   <td><strong>葉標籤</strong></td>
   <td><strong>Repository<br /> Absolute標籤路徑</strong></td>
  </tr>
  <tr>
   <td>dam:fruit/apple/braeburn</td>
   <td>壩</td>
   <td>水果／蘋果／佈雷本</td>
   <td>水果，蘋果</td>
   <td>braeburn</td>
   <td>/content/cq:tags/dam/fruit/apple/braeburn</td>
  </tr>
  <tr>
   <td>顏色／紅色</td>
   <td>預設</td>
   <td>顏色／紅色</td>
   <td>色彩</td>
   <td>紅色</td>
   <td>/content/cq:tags/default/color/red</td>
  </tr>
  <tr>
   <td>天空</td>
   <td>預設</td>
   <td>天空</td>
   <td>(無)</td>
   <td>天空</td>
   <td>/content/cq:tags/default/sky</td>
  </tr>
  <tr>
   <td>dam:</td>
   <td>壩</td>
   <td>(無)</td>
   <td>(無)</td>
   <td>（無，命名空間）</td>
   <td>/content/cq:tags/dam</td>
  </tr>
  <tr>
   <td>/content/cq:tags/category/car</td>
   <td>類別</td>
   <td>汽車</td>
   <td>汽車</td>
   <td>汽車</td>
   <td>/content/cq:tags/category/car</td>
  </tr>
 </tbody>
</table>

### 標籤標題的本地化 {#localization-of-tag-title}

當標籤包含選用的標題字串( `jcr:title`)時，可透過新增屬性來本地化顯示的標題 `jcr:title.<locale>`。

如需詳細資訊，請參閱

* [不同語言的標籤](/help/sites-developing/building.md#tags-in-different-languages) -說明API的使用
* [管理不同語言的標籤](/help/sites-administering/tags.md#managing-tags-in-different-languages) -說明使用標籤控制台

### 存取控制 {#access-control}

標籤作為分類根節點下的儲存庫 [中的節點存在](#taxonomy-root-node)。 允許或拒絕作者和站點訪客在給定名稱空間中建立標籤，可以通過在儲存庫中設定適當的ACL來實現。

此外，拒絕某些標籤或名稱空間的讀取權限將控制將標籤應用於特定內容的能力。

典型做法包括：

* 允許對所 `tag-administrators` 有名稱空間的組／角色寫訪問權限(在下添加／修 `/content/cq:tags`改)。 此群組隨附AEM現成可用功能。

* 允許用戶／作者讀取對所有應該對其可讀取的名稱空間（大部分）的訪問權。
* 允許用戶／作者對用戶／作者可自由定義標籤的名稱空間進行寫入訪問(在下面添加節 `/content/cq:tags/some_namespace`點)

## 可標籤內容：cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

為了讓應用程式開發人員將標籤附加至內容類型，節點的註冊([CND](https://jackrabbit.apache.org/node-type-notation.html))必須包含 `cq:Taggable` mixin或mixin `cq:OwnerTaggable` 。

繼承 `cq:OwnerTaggable` 自的mixin旨在 `cq:Taggable`指出內容可由擁有者／作者分類。 在AEM中，它只是節點的屬 `cq:PageContent` 性。 標籤 `cq:OwnerTaggable` 框架不需要混合素。

>[!NOTE]
>
>建議僅在匯總內容項目的頂層節點（或其jcr:content節點）上啟用標籤。 範例包括：
>
>* 頁面( `cq:Page`)，其中節 `jcr:content`點是包含 `cq:PageContent` 混合的類型 `cq:Taggable` 。
   >
   >
* 資產( `cq:Asset`)節點永 `jcr:content/metadata` 遠有混合項的 `cq:Taggable` 位置。
>



### 節點類型注釋(CND) {#node-type-notation-cnd}

節點類型定義作為CND檔案存在於儲存庫中。 CND符號在此定義為JCR文檔的一 [部分](https://jackrabbit.apache.org/node-type-notation.html)。

AEM中包含的「節點類型」基本定義如下：

```xml
[cq:Tag] > mix:title, nt:base
    orderable
    - * (undefined) multiple
    - * (undefined)
    + * (nt:base) = cq:Tag version

[cq:Taggable]
    mixin
    - cq:tags (string) multiple

[cq:OwnerTaggable] > cq:Taggable
    mixin
```

## 標籤內容：cq:tags屬性 {#tagged-content-cq-tags-property}

屬 `cq:tags` 性是一個String陣列，當作者或網站訪客將一或多個TagID套用至內容時，用來儲存這些TagID。 僅當將屬性添加到使用mixin定義的節點時，該屬性才有 ` [cq:Taggable](#taggable-content-cq-taggable-mixin)` 意義。

>[!NOTE]
>
>若要運用AEM標籤功能，自訂開發的應用程式不應定義標籤屬性 `cq:tags`。

## 移動和合併標籤 {#moving-and-merging-tags}

以下是使用標籤控制台移動或合併標籤時儲存庫中效果的 [說明](/help/sites-administering/tags.md):

* 當標籤A被移動或合併到標籤B時，位於 `/content/cq:tags`:

   * 標籤A不會刪除，且會取得 `cq:movedTo` 屬性。
   * 標籤B已建立（在移動時）並取得屬 `cq:backlinks` 性。

* `cq:movedTo` 指向標籤B。此屬性表示標籤A已移動或合併到標籤B。移動標籤B將相應地更新此屬性。 標籤A因此會隱藏，並且僅保存在儲存庫中，以解析指向標籤A的內容節點中的標籤ID。標籤廢棄項目收集器會移除標籤A等標籤，不再有內容節點指向標籤A。
屬性的特殊 `cq:movedTo` 值為 `nirvana`:它將在標籤被刪除時應用，但無法從儲存庫中刪除，因為必須保留具有 `cq:movedTo` 子標籤的子標籤。

   >[!NOTE]
   >
   >只有 `cq:movedTo` 符合下列任一條件時，才會將屬性新增至已移動或合併的標籤：
   > 1. 標籤用於內容（亦即它有參考）或
   > 1. 標籤包含已移動的子項。


* `cq:backlinks` 將參照保持在另一個方向，即保留已移動到標籤B或與標籤B合併的所有標籤的清單。當標籤B移動／合併／刪 `cq:movedTo`除時，或標籤B啟動時，這通常需要保持屬性的最新狀態，在此情況下，其所有的回溯連結標籤也必須啟用。

   >[!NOTE]
   >
   >只有 `cq:backlinks` 符合下列任一條件時，才會將屬性新增至已移動或合併的標籤：
   > 1. 標籤用於內容（亦即它有參考）或
   > 1. 標籤包含已移動的子項。


* 讀取內 `cq:tags` 容節點的屬性涉及到下列解決：

   1. 如果下方沒有相符項目 `/content/cq:tags`，則不會傳回標籤。
   1. 如果標籤有屬性 `cq:movedTo` 集，則會遵循參考的標籤ID。
只要後面的標籤有屬性，就會重複此 `cq:movedTo` 步驟。

   1. 如果後面的標籤沒有屬 `cq:movedTo` 性，則讀取標籤。

* 要在標籤已移動或合併時發佈更改，必須復 `cq:Tag` 制節點及其所有回鏈：當標籤在標籤管理主控台中啟動時，就會自動執行此動作。

* 稍後頁面屬性的更新 `cq:tags` 會自動清除「舊」參照。 觸發此項是因為透過API解析移動的標籤會傳回目標標籤，因此提供目標標籤ID。
