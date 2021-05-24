---
title: AEM標籤架構
seo-title: AEM標籤架構
description: 標籤內容並運用AEM標籤基礎結構
seo-description: 標籤內容並運用AEM標籤基礎結構
uuid: f80a2cb1-359f-41dd-a70b-626d92cc3d4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: f69db472-9f5c-4c0d-9292-2920ef69feeb
docset: aem65
feature: 標記
exl-id: 53a37449-ef87-4fa6-82de-88fdc24cf988
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1916'
ht-degree: 0%

---

# AEM標籤框架{#aem-tagging-framework}

若要標籤內容並運用AEM標籤基礎結構：

* 標籤必須作為[分類根節點](#taxonomy-root-node)下的` [cq:Tag](#tags-cq-tag-node-type)`類型節點存在

* 標籤內容節點的NodeType必須包含[ `cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin
* 將[TagID](#tagid)添加到內容節點的[ `cq:tags`](#tagged-content-cq-tags-property)屬性，並解析到類型` [cq:Tag](#tags-cq-tag-node-type)`的節點

## 標籤：cq：標籤節點類型{#tags-cq-tag-node-type}

標籤的聲明被捕獲到`cq:Tag.`類型的節點的儲存庫中

標籤可以是簡單的字詞（如sky），或代表階層分類法（如果果/蘋果，即通用水果和更具體的蘋果）。

標籤由唯一的TagID識別。

標籤包含選用的中繼資訊，例如標題、本地化標題和說明。 標題應顯示在使用者介面中，而非TagID（若存在）。

標籤架構也能限製作者和網站訪客僅使用特定、預先定義的標籤。

### 標籤特性{#tag-characteristics}

* 節點類型為`cq:Tag`
* 節點名稱是` [TagID](#tagid)`的元件
* ` [TagID](#tagid)`一律包含[namespace](#tag-namespace)

* 選用`jcr:title`屬性（要在UI中顯示的標題）

* 可選`jcr:description`屬性

* 包含子節點時，稱為[容器標籤](#container-tags)
* 儲存在名為[分類根節點](#taxonomy-root-node)的基路徑下的儲存庫中

### 標記 ID {#tagid}

TagID可識別解析至儲存庫中標籤節點的路徑。

TagID通常是以命名空間開頭的速記TagID，也可以是從[分類根節點](#taxonomy-root-node)開始的絕對TagID。

標籤內容時，如果內容尚未存在，則會將` [cq:tags](#tagged-content-cq-tags-property)`屬性新增至內容節點，並將TagID新增至屬性的String陣列值。

TagID由[namespace](#tag-namespace)組成，後面接著本機TagID。 [代表](#container-tags) 分類法中階層順序的容器標籤子標籤。子標籤可用來參考與任何本機TagID相同的標籤。 例如，可以使用&quot;fruit&quot;標籤內容，即使這是帶有子標籤的容器標籤，例如&quot;fruit/apple&quot;和&quot;fruit/banana&quot;。

### 分類根節點{#taxonomy-root-node}

分類根節點是儲存庫中所有標籤的基本路徑。 分類根節點必須&#x200B;*不*&#x200B;為`  cq   :Tag`類型的節點。

在AEM中，基本路徑為`/content/  cq   :tags`，根節點為`  cq   :Folder`類型。

### 標籤命名空間{#tag-namespace}

命名空間可將項目分組。 最典型的使用案例是每個（網站）網站（例如公用、內部和入口網站）或每個大型應用程式（例如WCM、Assets、Communities）都有命名空間，但命名空間可用於各種其他需求。 使用者介面中使用命名空間，以僅顯示適用於目前內容的標籤子集（即特定命名空間的標籤）。

標籤的命名空間是分類子樹中的第一級，即緊接在[分類根節點](#taxonomy-root-node)下的節點。 命名空間是`cq:Tag`類型的節點，其父代不是`cq:Tag`節點類型。

所有標籤都有命名空間。 如果未指定命名空間，則將標籤分配給預設命名空間，即TagID `default`(標題為`Standard Tags),`，即`/content/cq:tags/default.`

### 容器標籤{#container-tags}

容器標籤是包含任何數目和子節點類型的`cq:Tag`類型節點，因此可以使用自訂中繼資料來增強標籤模型。

此外，分類法中的容器標籤（或超標籤）是所有子標籤的子總和：例如，用水果/蘋果標籤的內容也被認為是用水果標籤的，即搜索僅用水果標籤的內容也會找到用水果/蘋果標籤的內容。

### 解析TagID {#resolving-tagids}

如果標籤ID包含冒號「：」，冒號會將命名空間與標籤或子分類法分開，然後以一般斜線「/」分開。 如果標籤ID沒有冒號，表示預設命名空間。

標籤的標準且唯一位置低於/content/cq:tags。

參考未指向cq的非現有路徑或路徑的標籤會視為無效，且會被忽略。

下表顯示一些範例TagID、其元素，以及TagID解析至存放庫中絕對路徑的方式：

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
   <td><strong>儲存庫<br />絕對標籤路徑</strong></td>
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

### 標籤標題的本地化{#localization-of-tag-title}

當標籤包含選用的標題字串(`jcr:title`)時，可借由新增屬性`jcr:title.<locale>`將顯示的標題本地化。

如需更多詳細資訊，請參閱

* [不同語言的標籤](/help/sites-developing/building.md#tags-in-different-languages)  — 說明API的使用方式
* [管理不同語言的標籤](/help/sites-administering/tags.md#managing-tags-in-different-languages)  — 說明「標籤」控制台的使用方式

### 存取控制 {#access-control}

標籤作為節點存在於[分類根節點](#taxonomy-root-node)下的儲存庫中。 您可以在存放庫中設定適當的ACL，以允許或拒絕作者和網站訪客在指定的命名空間中建立標籤。

此外，拒絕某些標籤或命名空間的讀取權限，將可控制將標籤套用至特定內容的能力。

典型做法包括：

* 允許`tag-administrators`組/角色對所有命名空間的寫入訪問（在`/content/cq:tags`下添加/修改）。 此群組隨附AEM現成可用。

* 允許使用者/作者讀取應讀取之所有命名空間的存取權（大多為）。
* 允許使用者/作者撰寫存取使用者/作者應可自由定義標籤的命名空間（`/content/cq:tags/some_namespace`底下的add_node）

## 可標籤內容：cq：可標籤的Mixin {#taggable-content-cq-taggable-mixin}

為了讓應用程式開發人員將標籤附加到內容類型，節點的註冊([CND](https://jackrabbit.apache.org/node-type-notation.html))必須包括`cq:Taggable` mixin或`cq:OwnerTaggable` mixin。

繼承自`cq:Taggable`的`cq:OwnerTaggable` mixin旨在指出內容可由擁有者/作者分類。 在AEM中，它只是`cq:PageContent`節點的屬性。 標籤框架不需要`cq:OwnerTaggable` mixin。

>[!NOTE]
>
>建議僅在匯總內容項目的頂層節點（或其jcr:content節點）上啟用標籤。 範例包括：
>
>* 頁面(`cq:Page`)，其中`jcr:content`節點為`cq:PageContent`類型，包含`cq:Taggable` mixin。
   >
   >
* 資產(`cq:Asset`)，其中`jcr:content/metadata`節點一律有`cq:Taggable` mixin。

>



### 節點類型標籤法(CND){#node-type-notation-cnd}

儲存庫中的節點類型定義以CND檔案的形式存在。 CND標籤法定義為JCR檔案[here](https://jackrabbit.apache.org/node-type-notation.html)的一部分。

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

## 標籤的內容：cq:tags屬性{#tagged-content-cq-tags-property}

`cq:tags`屬性是字串陣列，當作者或網站訪客將一或多個TagID套用至內容時，可用來儲存這些TagID。 只有在將屬性添加到以`[cq:Taggable](#taggable-content-cq-taggable-mixin)` mixin定義的節點時，該屬性才有意義。

>[!NOTE]
>
>若要利用AEM標籤功能，自訂開發的應用程式不應定義`cq:tags`以外的標籤屬性。

## 移動和合併標籤{#moving-and-merging-tags}

以下是使用[標籤控制台](/help/sites-administering/tags.md)移動或合併標籤時，儲存庫中效果的說明：

* 將標籤A移動或合併至`/content/cq:tags`下的標籤B時：

   * 標籤A未刪除，且會取得`cq:movedTo`屬性。
   * 標籤B會建立（若是移動）並取得`cq:backlinks`屬性。

* `cq:movedTo` 指向標籤B。此屬性表示標籤A已移動或合併到標籤B。移動標籤B將相應地更新此屬性。因此，標籤A會隱藏，並僅保留在儲存庫中，以解析指向標籤A的內容節點中的標籤ID。標籤垃圾收集器會刪除標籤A之類的標籤，而不再將內容節點指向它們。
`cq:movedTo`屬性的特殊值為`nirvana`:標籤刪除時會套用，但無法從存放庫中移除，因為必須保留具有`cq:movedTo`的子標籤。

   >[!NOTE]
   >
   >`cq:movedTo`屬性僅在符合下列任一條件時，才會新增至已移動或已合併的標籤：
   > 1. 標籤用於內容（表示有參考）或
   > 1. 標籤包含已移動的子項。


* `cq:backlinks` 保留另一個方向的引用，即保留已移動到標籤B或與標籤B合併的所有標籤的清單。在移動/合併/刪除標籤B和激活標籤B時，這 `cq:movedTo`通常需要保持屬性最新，在這種情況下，必須同時激活其所有反向連結標籤。

   >[!NOTE]
   >
   >`cq:backlinks`屬性僅在符合下列任一條件時，才會新增至已移動或已合併的標籤：
   >
   > 1. 標籤用於內容（表示有參考）或    >
   > 1. 標籤包含已移動的子項。


* 讀取內容節點的`cq:tags`屬性涉及以下解析：

   1. 如果`/content/cq:tags`下沒有相符項目，則不會傳回任何標籤。
   1. 如果標籤已設定`cq:movedTo`屬性，則會遵循參考的標籤ID。
只要後面的標籤具有`cq:movedTo`屬性，就會重複此步驟。

   1. 如果後面的標籤沒有`cq:movedTo`屬性，則會讀取標籤。

* 要在移動或合併標籤時發佈更改，必須複製`cq:Tag`節點及其所有反向連結：在標籤管理控制台中啟動標籤時，就會自動完成此作業。

* 稍後頁面的`cq:tags`屬性更新會自動清除「old」參考。 觸發此動作是因為透過API解析移動的標籤會傳回目的地標籤，因而提供目的地標籤ID。

>[!NOTE]
>
>標籤的移動與標籤的移轉不同。

## 標籤遷移{#tags-migration}

Experience Manager6.4以後的標籤儲存在`/content/cq:tags`下，而先前儲存在`/etc/tags`下。 不過，在Adobe Experience Manager已從舊版升級的案例中，標籤仍會顯示在舊位置`/etc/tags`下。 在升級的系統中，標籤需要在`/content/cq:tags`下遷移。

>[!NOTE]
>
>在「標籤的頁面屬性」頁面中，建議使用標籤ID(`geometrixx-outdoors:activity/biking`)，而非硬式編碼標籤基底路徑（例如`/etc/tags/geometrixx-outdoors/activity/biking`）。
>
>若要列出標籤，可使用`com.day.cq.tagging.servlets.TagListServlet`。

>[!NOTE]
>
>建議使用標籤管理程式API作為資源。

### 如果升級的AEM例項支援TagManager API {#upgraded-instance-support-tagmanager-api}

1. 元件開始時，TagManager API會偵測其是否為升級版AEM例項。 在升級的系統中，標籤儲存在`/etc/tags`下。

1. TagManager API接著會以回溯相容模式執行，這表示API使用`/etc/tags`作為基本路徑。 否則，將使用新位置`/content/cq:tags`。

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

指令碼會擷取`cq:movedTo/cq:backLinks`屬性值中包含`/etc/tags`的所有標籤。 然後，它反覆擷取的結果集，並將`cq:movedTo`和`cq:backlinks`屬性值解析為`/content/cq:tags`路徑（若值中偵測到`/etc/tags`）。

### 如果升級的AEM執行個體在傳統UI {#upgraded-instance-runs-classic-ui}上執行

>[!NOTE]
>
>傳統UI不符合零停機時間標準，也不支援新的標籤基路徑。 如果您想使用傳統UI，則需先建立`/etc/tags`，然後重新啟動`cq-tagging`元件。

若是TagManager API支援並在傳統UI中執行的升級AEM例項：

1. 使用tagId或新標籤位置`/content/cq:tags`取代對舊標籤基路徑`/etc/tags`的參考後，您可以將標籤移轉至CRX中的新位置`/content/cq:tags`，接著重新啟動元件。

1. 將標籤移轉至新位置後，請執行上述指令碼。
