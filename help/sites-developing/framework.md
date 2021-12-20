---
title: AEM標籤架構
seo-title: AEM Tagging Framework
description: 標籤內容並運用AEM標籤基礎結構
seo-description: Tag content and leverage the AEM Tagging infrastructure
uuid: f80a2cb1-359f-41dd-a70b-626d92cc3d4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: f69db472-9f5c-4c0d-9292-2920ef69feeb
docset: aem65
feature: Tagging
exl-id: 53a37449-ef87-4fa6-82de-88fdc24cf988
source-git-commit: 4db9279f2d15f2e08939ba453ae8ddbbc3c3d69f
workflow-type: tm+mt
source-wordcount: '1883'
ht-degree: 0%

---

# AEM標籤架構 {#aem-tagging-framework}

若要標籤內容並運用AEM標籤基礎結構：

* 標籤必須存在為類型的節點 ` [cq:Tag](#tags-cq-tag-node-type)` 在 [分類根節點](#taxonomy-root-node)

* 標籤內容節點的NodeType必須包含 [ `cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin
* 此 [TagID](#tagid) 會新增至內容節點的 [ `cq:tags`](#tagged-content-cq-tags-property) 屬性，並解析到類型的節點 ` [cq:Tag](#tags-cq-tag-node-type)`

## 標籤：cq：標籤節點類型  {#tags-cq-tag-node-type}

標籤的聲明被捕獲到儲存庫中類型的節點中 `cq:Tag.`

標籤可以是簡單的字詞（如sky），或代表階層分類法（如果果/蘋果，即通用水果和更具體的蘋果）。

標籤由唯一的TagID識別。

標籤包含選用的中繼資訊，例如標題、本地化標題和說明。 標題應顯示在使用者介面中，而非TagID（若存在）。

標籤架構也能限製作者和網站訪客僅使用特定、預先定義的標籤。

### 標籤特性 {#tag-characteristics}

* 節點類型為 `cq:Tag`
* 節點名稱是 ` [TagID](#tagid)`
* the ` [TagID](#tagid)` 一律包含 [命名空間](#tag-namespace)

* 可選 `jcr:title` 屬性（UI中顯示的標題）

* 可選 `jcr:description` 屬性

* 包含子節點時，稱為 [容器標籤](#container-tags)
* 儲存在存放庫中，位於名為的 [分類根節點](#taxonomy-root-node)

### 標記 ID {#tagid}

TagID可識別解析至儲存庫中標籤節點的路徑。

TagID通常是以命名空間開頭的速記TagID，也可以是以 [分類根節點](#taxonomy-root-node).

當內容經過標籤時，如果內容尚未存在，則 ` [cq:tags](#tagged-content-cq-tags-property)` 屬性會新增至內容節點，而TagID會新增至屬性的String陣列值。

TagID包含 [命名空間](#tag-namespace) 後面接著本機TagID。 [容器標籤](#container-tags) 具有子標籤，該子標籤表示分類中的分層順序。 子標籤可用來參考與任何本機TagID相同的標籤。 例如，可以使用&quot;fruit&quot;標籤內容，即使這是帶有子標籤的容器標籤，例如&quot;fruit/apple&quot;和&quot;fruit/banana&quot;。

### 分類根節點 {#taxonomy-root-node}

分類根節點是儲存庫中所有標籤的基本路徑。 分類根節點必須 *not* 是類型的節點 `  cq   :Tag`.

在AEM中，基本路徑為 `/content/  cq   :tags` 根節點是 `  cq   :Folder`.

### 標籤命名空間 {#tag-namespace}

命名空間可將項目分組。 最典型的使用案例是每個（網站）網站（例如公用、內部和入口網站）或每個大型應用程式（例如WCM、Assets、Communities）都有命名空間，但命名空間可用於各種其他需求。 使用者介面中使用命名空間，以僅顯示適用於目前內容的標籤子集（即特定命名空間的標籤）。

標籤的命名空間是分類子樹狀結構中的第一層，也就是緊接在 [分類根節點](#taxonomy-root-node). 命名空間是一種節點 `cq:Tag` 其父母 `cq:Tag`節點類型。

所有標籤都有命名空間。 若未指定命名空間，則會將標籤指派給預設命名空間，即TagID `default` (標題為 `Standard Tags),`是 `/content/cq:tags/default.`

### 容器標籤 {#container-tags}

容器標籤是類型的節點 `cq:Tag` 包含任何數目和類型的子節點，因此可以使用自訂中繼資料增強標籤模型。

此外，分類法中的容器標籤（或超標籤）是所有子標籤的子總和：例如，用水果/蘋果標籤的內容也被認為是用水果標籤的，即搜索僅用水果標籤的內容也會找到用水果/蘋果標籤的內容。

### 解析TagID {#resolving-tagids}

如果標籤ID包含冒號「：」，冒號會將命名空間與標籤或子分類法分開，然後以一般斜線「/」分開。 如果標籤ID沒有冒號，表示預設命名空間。

標籤的標準且唯一位置低於/content/cq:tags。

參考未指向cq的非現有路徑或路徑的標籤會視為無效，且會被忽略。

下表顯示一些範例TagID、其元素，以及TagID解析至存放庫中絕對路徑的方式：

下表顯示一些範例TagID、其元素，以及TagID解析至存放庫中絕對路徑的方式：

<table>
 <tbody>
  <tr>
   <td><strong>標記 ID<br /> </strong></td>
   <td><strong>命名空間</strong></td>
   <td><strong>本機ID</strong></td>
   <td><strong>容器標籤</strong></td>
   <td><strong>葉標籤</strong></td>
   <td><strong>存放庫<br /> 絕對標籤路徑</strong></td>
  </tr>
  <tr>
   <td>dam:fruit/apple/braburn</td>
   <td>壩</td>
   <td>水果/蘋果/佈雷本</td>
   <td>水果，蘋果</td>
   <td>布拉本</td>
   <td>/content/cq:tags/dam/fruit/apple/braburn</td>
  </tr>
  <tr>
   <td>顏色/紅色</td>
   <td>預設</td>
   <td>顏色/紅色</td>
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

當標籤包含選用的標題字串時( `jcr:title`)可新增屬性，將顯示的標題當地化 `jcr:title.<locale>`.

如需更多詳細資訊，請參閱

* [不同語言中的標籤](/help/sites-developing/building.md#tags-in-different-languages)  — 說明API的使用方式
* [管理不同語言中的標籤](/help/sites-administering/tags.md#managing-tags-in-different-languages)  — 說明如何使用標籤控制台

### 存取控制 {#access-control}

標籤存在於存放庫的 [分類根節點](#taxonomy-root-node). 您可以在存放庫中設定適當的ACL，以允許或拒絕作者和網站訪客在指定的命名空間中建立標籤。

此外，拒絕某些標籤或命名空間的讀取權限，將可控制將標籤套用至特定內容的能力。

典型做法包括：

* 允許 `tag-administrators` 組/角色寫入訪問所有命名空間(在 `/content/cq:tags`)。 此群組隨附AEM現成可用。

* 允許使用者/作者讀取應讀取之所有命名空間的存取權（大多為）。
* 允許使用者/作者撰寫存取使用者/作者應可自由定義標籤的命名空間(add_node，位於 `/content/cq:tags/some_namespace`)

## 可標籤內容：cq：可標籤的Mixin {#taggable-content-cq-taggable-mixin}

為了讓應用程式開發人員將標籤附加到內容類型，節點的註冊([CND](https://jackrabbit.apache.org/node-type-notation.html))必須包含 `cq:Taggable` mixin或 `cq:OwnerTaggable` 米辛。

此 `cq:OwnerTaggable` mixin，它繼承自 `cq:Taggable`，旨在指出內容可由擁有者/作者分類。 在AEM中，它只是 `cq:PageContent` 節點。 此 `cq:OwnerTaggable` 標籤架構不需要mixin。

>[!NOTE]
>
>建議僅在匯總內容項目的頂層節點（或其jcr:content節點）上啟用標籤。 範例包括：
>
>* 頁面( `cq:Page`)，其中 `jcr:content`節點的類型 `cq:PageContent` 包括 `cq:Taggable` 米辛。
>
>* 資產( `cq:Asset`)，其中 `jcr:content/metadata` 節點總是有 `cq:Taggable` 米辛。

>


### 節點類型標籤法(CND) {#node-type-notation-cnd}

儲存庫中的節點類型定義以CND檔案的形式存在。 CND標籤法是JCR檔案中的定義 [此處](https://jackrabbit.apache.org/node-type-notation.html).

AEM中包含之節點類型的基本定義如下：

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

## 標籤的內容：cq:tags屬性 {#tagged-content-cq-tags-property}

此 `cq:tags` 屬性是字串陣列，當作者或網站訪客將一或多個TagID套用至內容時，用來儲存這些TagID。 只有在新增至以 `[cq:Taggable](#taggable-content-cq-taggable-mixin)` 米辛。

>[!NOTE]
>
>若要運用AEM標籤功能，自訂開發的應用程式不應定義標籤屬性， `cq:tags`.

## 移動及合併標籤 {#moving-and-merging-tags}

以下說明使用移動或合併標籤時，儲存庫中的效果 [標籤主控台](/help/sites-administering/tags.md):

* 標籤A移動或合併至標籤B時位於 `/content/cq:tags`:

   * 標籤A未刪除，且會取得 `cq:movedTo` 屬性。
   * 標籤B已建立（若有移動）並取得 `cq:backlinks` 屬性。

* `cq:movedTo` 指向標籤B。此屬性表示標籤A已移動或合併到標籤B。移動標籤B將相應地更新此屬性。 因此，標籤A會隱藏，並僅保留在儲存庫中，以解析指向標籤A的內容節點中的標籤ID。標籤垃圾收集器會刪除標籤A之類的標籤，而不再將內容節點指向它們。
的特殊值 `cq:movedTo` 屬性為 `nirvana`:標籤刪除時會套用，但無法從存放庫中移除，因為存在具有的子標籤 `cq:movedTo` 必須保留。

   >[!NOTE]
   >
   >此 `cq:movedTo` 只有在符合下列任一條件時，才會將屬性新增至移動或合併的標籤：
   > 1. 標籤用於內容（表示有參考）或
   > 1. 標籤包含已移動的子項。


* `cq:backlinks` 保留反向引用，即保留已移動到標籤B或與標籤B合併的所有標籤的清單。這通常是保持 `cq:movedTo`屬性，直到標籤B移動/合併/刪除或標籤B啟動時為止，在此情況下，其所有反向連結標籤也必須啟動。

   >[!NOTE]
   >
   >此 `cq:backlinks` 只有在符合下列任一條件時，才會將屬性新增至移動或合併的標籤：
   >
   > 1. 標籤用於內容（表示有參考）OR >
   > 1. 標籤包含已移動的子項。


* 閱讀 `cq:tags` 內容節點的屬性包含下列解析：

   1. 如果下沒有匹配項 `/content/cq:tags`，則不會傳回任何標籤。
   1. 如果標籤具有 `cq:movedTo` 屬性集，則會遵循參考的標籤ID。
只要後面的標籤具有 `cq:movedTo` 屬性。

   1. 如果後面的標籤沒有 `cq:movedTo` 屬性，則會讀取標籤。

* 若要在移動或合併標籤時發佈變更， `cq:Tag` 節點及其所有反向連結必須複製：在標籤管理控制台中啟動標籤時，就會自動完成此作業。

* 稍後更新頁面的 `cq:tags` 屬性會自動清除「舊」參考。 觸發此動作是因為透過API解析移動的標籤會傳回目的地標籤，因而提供目的地標籤ID。

>[!NOTE]
>
>標籤的移動與標籤的移轉不同。

## 標籤移轉 {#tags-migration}

Experience Manager6.4以上的標籤會儲存在 `/content/cq:tags`，其先前儲存在 `/etc/tags`. 不過，在Adobe Experience Manager已從舊版升級的案例中，標籤仍會顯示在舊位置下 `/etc/tags`. 在升級的系統中，需要在 `/content/cq:tags`.

>[!NOTE]
>
>在標籤頁面的「頁面屬性」中，建議使用標籤ID(`geometrixx-outdoors:activity/biking`)，而非硬式編碼標籤基本路徑(例如 `/etc/tags/geometrixx-outdoors/activity/biking`)。
>
>要列出標籤， `com.day.cq.tagging.servlets.TagListServlet` 可供使用。

>[!NOTE]
>
>建議使用標籤管理程式API作為資源。

### 如果升級的AEM例項支援TagManager API {#upgraded-instance-support-tagmanager-api}

1. 元件開始時，TagManager API會偵測其是否為升級版AEM例項。 在升級的系統中，標籤儲存在 `/etc/tags`.

1. TagManager API接著會以回溯相容模式執行，這表示API會使用 `/etc/tags` 作為基本路徑。 否則會使用新位置 `/content/cq:tags`.

1. 更新標籤位置。

1. 將標籤移轉至新位置後，請執行下列指令碼：

```java
import org.apache.sling.api.resource.*
import javax.jcr.*

ResourceResolverFactory resourceResolverFactory = osgi.getService(ResourceResolverFactory.class);
ResourceResolver resolver = resourceResolverFactory.getAdministrativeResourceResolver(null);
Session session = resolver.adaptTo(Session.class);

def queryManager = session.workspace.queryManager;
def statement = "/jcr:root/content/cq:tags//element(*, cq:Tag)[jcr:contains(@cq:movedTo,\'/etc/tags\') or jcr:contains(@cq:backlinks,\'/etc/tags\')]";
def query = queryManager.createQuery(statement, "xpath");

println "query = ${query.statement}\n";

def tags = query.execute().getNodes();


tags.each { node ->
  def tagPath = node.path;
  println "tag = ${tagPath}";

  if(node.hasProperty("cq:movedTo") && node.getProperty("cq:movedTo").getValue().toString().startsWith("/etc/tags"))
    {
     def movedTo = node.getProperty("cq:movedTo").getValue().toString();

     println "cq:movedTo = ${movedTo} \n";

     movedTo = movedTo.replace("/etc/tags","/content/cq:tags");
     node.setProperty("cq:movedTo",movedTo);
     } else if(node.hasProperty("cq:backlinks")){

     String[] backLinks = node.getProperty("cq:backlinks").getValues();
     int count = 0;

     backLinks.each { value ->
             if(value.startsWith("/etc/tags")){
                     println "cq:backlinks = ${value}\n";
                     backLinks[count] = value.replace("/etc/tags","/content/cq:tags");
    }
             count++;
     }

    node.setProperty("cq:backlinks",backLinks);
  }
}
session.save();

println "---------------------------------Success-------------------------------------"
```

指令碼會擷取所有具有 `/etc/tags` 的值 `cq:movedTo/cq:backLinks` 屬性。 然後，它會反覆擷取的結果集，並解析 `cq:movedTo` 和 `cq:backlinks` 屬性值為 `/content/cq:tags` 路徑(在 `/etc/tags` 值中偵測到)。

### 如果升級的AEM執行個體在傳統UI上執行 {#upgraded-instance-runs-classic-ui}

>[!NOTE]
>
>傳統UI不符合零停機時間標準，也不支援新的標籤基路徑。 如果您想使用傳統UI，但 `/etc/tags` 需要建立後面 `cq-tagging` 元件重新啟動。

若是TagManager API支援並在傳統UI中執行的升級AEM例項：

1. 參考舊標籤基路徑後 `/etc/tags` 替換為使用tagId或新標籤位置 `/content/cq:tags`，您可以將標籤移轉至新位置 `/content/cq:tags` 在CRX中，接著重新啟動元件。

1. 將標籤移轉至新位置後，請執行上述指令碼。
