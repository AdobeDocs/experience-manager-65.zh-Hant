---
title: AEM 標記框架
description: 標籤內容並使用AEM標籤基礎結構
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
feature: Tagging
exl-id: 53a37449-ef87-4fa6-82de-88fdc24cf988
source-git-commit: 8dafa901bc628ee5e4823e9f8811bf4d09b7e072
workflow-type: tm+mt
source-wordcount: '1642'
ht-degree: 0%

---


# AEM 標記框架 {#aem-tagging-framework}

標籤可讓內容分類並整理。 標籤可依名稱空間和分類法來分類。 如需使用標籤的詳細資訊：

* 檢視檔案 [使用標籤](/help/sites-authoring/tags.md) 有關將內容標籤為內容作者的資訊。
* 檢視檔案 [管理標籤](/help/sites-administering/tags.md) 供管理員檢視如何建立和管理標籤，以及已對哪些內容標籤套用。

本文主要說明在AEM中支援標籤的基本架構，以及如何作為開發人員使用它。

## 簡介 {#introduction}

若要標籤內容並使用AEM標籤基礎結構：

* 標籤必須作為型別的節點存在 `[cq:Tag](#tags-cq-tag-node-type)` 在 [分類根節點。](#taxonomy-root-node)

* 標籤的內容節點的 `NodeType` 必須包括 [`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin.
* 此 [`TagID`](#tagid) 新增至內容節點的 [`cq:tags`](#tagged-content-cq-tags-property) 屬性並解析為型別的節點 ` [cq:Tag](#tags-cq-tag-node-type)`.

## 標籤：cq：Tag節點型別  {#tags-cq-tag-node-type}

標籤的宣告會擷取到存放庫中的型別節點中 `cq:Tag`.

標籤可以是簡單的單字(例如， `sky`)或代表階層式分類法(例如， `fruit/apple`，表示兩者 `fruit` 以及更具體的 `apple`)。

標籤由唯一的TagID識別。

標籤具有可選的中繼資訊，例如標題、當地語系化的標題和說明。 出現時，標題應顯示在使用者介面中，而不是TagID。

標籤架構也提供將作者和網站訪客限製為僅使用特定、預先定義的標籤的功能。

### 標籤特性 {#tag-characteristics}

* 節點型別為 `cq:Tag`n
* 節點名稱是 [標籤ID](#tagid).
* 此 [標籤ID](#tagid) 一律包含 [名稱空間。](#tag-namespace)
* 此 `jcr:title` 屬性（在UI中顯示的標題）為選用。
* 此 `jcr:description` 屬性為選用。
* 當包含子節點時，標籤會稱為 [容器標籤。](#container-tags)
* 標籤儲存在存放庫中，位於名為的基本路徑下方 [分類根節點。](#taxonomy-root-node)

由於標籤只是JCR節點，節點名稱當然必須遵守 [JCR命名慣例。](naming-conventions.md)

### 標記 ID {#tagid}

TagID會識別解析為存放庫中的標籤節點的路徑。

通常TagID是以名稱空間開頭的速記TagID，也可以是以 [分類根節點。](#taxonomy-root-node)

標籤內容時，如果內容尚不存在， `[cq:tags](#tagged-content-cq-tags-property)` 屬性會新增至內容節點，而TagID會新增至屬性的 `String` 陣列值。

TagID包含 [名稱空間](#tag-namespace) 後面接著本機TagID。 [容器標籤](#container-tags) 具有代表分類法中階層順序的子標籤。 子標籤可用於參照與任何本機TagID相同的標籤。 例如，使用下列專案標籤內容： `fruit` 允許存在，即使它是包含子標籤的容器標籤，例如 `fruit/apple` 和 `fruit/banana`.

### 分類根節點 {#taxonomy-root-node}

分類根節點是存放庫中所有標籤的基本路徑。 分類根節點不得為型別的節點 `cq:Tag`.

在AEM中，基底路徑為 `/content/cq:tags` 且根節點的型別為 `cq:Folder`.

### 標籤名稱空間 {#tag-namespace}

名稱空間可讓您將專案分組。 最典型的使用案例是每個網站（例如公用、內部和入口網站）或大型應用程式（例如WCM、Assets、Communities）的名稱空間。 但名稱空間可用於各種其他需求。 在使用者介面中使用名稱空間，以僅顯示適用於目前內容的標籤子集（即特定名稱空間的標籤）。

標籤的名稱空間是分類子樹狀結構中的第一個層級，也就是 [分類根節點](#taxonomy-root-node). 名稱空間是型別的節點 `cq:Tag` 其父項不是 `cq:Tag` 節點型別。

所有標籤都有名稱空間。 如果未指定名稱空間，則會將標籤指派給預設名稱空間TagID `default` 加上標題 `Standard Tags`，即 `/content/cq:tags/default`.

### 容器標籤 {#container-tags}

容器標籤是型別的節點 `cq:Tag` 包含任何數量及型別的子節點，可讓您使用自訂中繼資料來增強標籤模型。

此外，分類法中的容器標籤（或超級標籤）可作為所有子標籤的總和。 例如，內容標籤為 `fruit/apple` 視為已標籤 `fruit` 以及。 也就是說，搜尋標籤有 `fruit` 也會找到以標籤的內容 `fruit/apple`.

### 解析標籤ID {#resolving-tagids}

如果TagID包含冒號(`:`)，冒號會將名稱空間與標籤或子分類法分開，以斜線(`/`)。 如果TagID沒有冒號，則會隱含預設名稱空間。

以下為標籤的標準及唯一位置 `/content/cq:tags`.

標籤參照不存在的路徑或不指向 `cq:Tag` 節點會被視為無效，並予以忽略。

下表顯示一些TagID範例、其元素，以及TagID如何解析為存放庫中的絕對路徑：

| 標記 ID | 命名空間 | 本機ID | 容器標籤 | 分葉標籤 | 存放庫絕對標籤路徑 |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`、`apple` | `braeburn` | `/content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | 無 | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | 無 | 無 | 無，名稱空間 | `/content/cq:tags/dam` |
| `/content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `/content/cq:tags/category/car` |

### 標籤標題本地化 {#localization-of-tag-title}

當標籤包含可選標題字串( `jcr:title`)，則您可新增屬性，將顯示的標題本地化 `jcr:title.<locale>`.

如需詳細資訊，請參閱下列檔案：

* [不同語言的標籤](/help/sites-developing/building.md#tags-in-different-languages)，說明API的使用
* [管理不同語言的標籤](/help/sites-administering/tags.md#managing-tags-in-different-languages)，說明標籤主控台的使用

### 存取控制 {#access-control}

標籤會作為節點存在於下的存放庫中 [分類根節點](#taxonomy-root-node). 若要允許或拒絕作者和網站訪客在指定的名稱空間中建立標籤，可在存放庫中設定適當的ACL。

此外，拒絕某些標籤或名稱空間的讀取許可權會控制將標籤套用至特定內容的能力。

典型做法包括：

* 允許 `tag-administrators` 群組/角色對所有名稱空間的寫入許可權(新增/修改 `/content/cq:tags`)。 此群組隨附AEM立即可用。
* 允許使用者/作者讀取他們應該可以讀取的所有名稱空間（幾乎全部）。
* 允許使用者/作者寫入對標籤應由使用者/作者自由定義的名稱空間的存取權（在下新增節點） `/content/cq:tags/some_namespace`)

## 可標籤內容：cq：Taggable Mixin {#taggable-content-cq-taggable-mixin}

對於要將標籤附加至內容型別的應用程式開發人員，節點的註冊([CND](https://jackrabbit.apache.org/jcr/node-type-notation.html))必須包含 `cq:Taggable` mixin或 `cq:OwnerTaggable` mixin.

此 `cq:OwnerTaggable` mixin，繼承自 `cq:Taggable`，表示內容可依所有者/作者分類。 在AEM中，它只是 `cq:PageContent` 節點。 此 `cq:OwnerTaggable` 標籤框架不需要mixin。

>[!NOTE]
>
>建議僅在彙總內容專案的頂層節點(或其 `jcr:content` 節點)。 範例包括：
>
>* 頁面(`cq:Page`)其中 `jcr:content`節點屬於型別 `cq:PageContent` 其中包括 `cq:Taggable` mixin
>* 資產( `cq:Asset`)其中 `jcr:content/metadata` 節點一律具有 `cq:Taggable` mixin
>

### 節點型別標籤法(CND) {#node-type-notation-cnd}

節點型別定義以CND檔案的形式存在於存放庫中。 CND標籤法定義為JCR檔案的一部分 [此處](https://jackrabbit.apache.org/jcr/node-type-notation.html).

AEM中包含的「節點型別」的基本定義如下：

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

## 標籤內容： cq：tags屬性 {#tagged-content-cq-tags-property}

此 `cq:tags` 屬性是 `String` 陣列，用來儲存作者或網站訪客套用至內容的一或多個TagID。 屬性只有在新增至使用定義的節點時才有意義 `[cq:Taggable](#taggable-content-cq-taggable-mixin)` mixin.

>[!NOTE]
>
>若要使用AEM標籤功能，自訂開發的應用程式不應定義以外的標籤屬性 `cq:tags`.

## 移動和合併標籤 {#moving-and-merging-tags}

以下說明使用移動或合併標籤時，在存放庫中所產生的效果 [標籤主控台](/help/sites-administering/tags.md)：

* 將標籤A移動或合併至下的標籤B時 `/content/cq:tags`：

   * 標籤A未刪除並取得 `cq:movedTo` 屬性。
   * 標籤B已建立（如果發生移動），並取得 `cq:backlinks` 屬性。

* `cq:movedTo` 指向標籤B。

   * 此屬性表示標籤A已移動或合併到標籤B中。移動標籤B會相應地更新此屬性。 標籤A因此會隱藏，並只會保留在存放庫中，以解析指向標籤A的內容節點中的標籤ID。標籤垃圾回收器會移除標籤A之類的標籤，而內容節點不再指向這些標籤。

   * 的特殊值 `cq:movedTo` 屬性為 `nirvana`. 它會在標籤刪除時套用，但無法從存放庫中移除，因為有子標籤具有 `cq:movedTo` 必須保留。

  >[!NOTE]
  >
  >此 `cq:movedTo` 只有在符合下列任一條件時，屬性才會新增至移動或合併的標籤：
  >
  >1. 標籤用於內容中（表示它有參考）或
  >1. 標籤具有已移動的子系。

* `cq:backlinks` 使參照保持在另一個方向。 也就是說，它會保留已移至標籤B或與標籤B合併的所有標籤清單。這通常需要保留 `cq:movedTo` 屬性是當標籤B移動/合併/刪除或是當標籤B啟動時的最新狀態，在這種情況下，其所有反向連結標籤也必須啟動。

  >[!NOTE]
  >
  >此 `cq:backlinks` 只有在符合下列任一條件時，屬性才會新增至移動或合併的標籤：
  >
  >1. 標籤用於內容中（表示它有參考）或
  >1. 標籤具有已移動的子系。

* 讀取 `cq:tags` 內容節點的屬性涉及以下解析度：

   1. 如果底下沒有相符專案 `/content/cq:tags`，不會傳回任何標籤。

   1. 如果標籤具有 `cq:movedTo` 屬性集，則會接著參考的標籤ID。

      * 只要後續的標籤具有 `cq:movedTo` 屬性。

   1. 如果追蹤的標籤沒有 `cq:movedTo` 屬性，則會讀取標籤。

* 若要在移動或合併標籤後發佈變更，請 `cq:Tag` 節點及其所有反向連結都必須複製。 在標籤管理主控台中啟動標籤時，會自動完成此作業。

* 稍後更新頁面的 `cq:tags` 屬性會自動清除舊參照。 由於透過API解析移動的標籤會傳回目的地標籤，因此會觸發此動作，進而提供目的地標籤ID。

>[!NOTE]
>
>標籤的移動與標籤的移轉不同。

## 標籤移轉 {#tags-migration}

自Adobe Experience Manager 6.4起，標籤會儲存在 `/content/cq:tags` 而舊版會將標籤儲存在 `/etc/tags`.

從6.4之前的版本升級AEM系統時，標籤必須移轉至 `/content/cq:tags`. 請參閱檔案 [AEM 6.5中的常見存放庫重組](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tags) 以取得詳細資訊。
