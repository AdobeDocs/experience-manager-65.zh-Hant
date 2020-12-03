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
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '1915'
ht-degree: 0%

---


# AEM標籤框架{#aem-tagging-framework}

若要標籤內容並運用AEM標籤基礎架構：

* 標籤必須作為[分類根節點](#taxonomy-root-node)下的` [cq:Tag](#tags-cq-tag-node-type)`類型節點存在

* 標籤內容節點的NodeType必須包含[ `cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin
* [TagID](#tagid)會新增至內容節點的[ `cq:tags`](#tagged-content-cq-tags-property)屬性，並解析至類型` [cq:Tag](#tags-cq-tag-node-type)`的節點

## 標籤：cq：標籤節點類型{#tags-cq-tag-node-type}

標籤的聲明在`cq:Tag.`類型的節點中在儲存庫中捕獲

標籤可以是簡單單字（例如，sky）或表示階層式分類法（例如，水果／蘋果，即通用水果和更具體的蘋果）。

標籤由唯一的TagID識別。

標籤包含可選的中繼資訊，例如標題、本地化標題和說明。 標題應顯示在使用者介面中，而非TagID（若有）。

標籤框架也能夠限製作者和網站訪客僅使用特定、預先定義的標籤。

### 標籤特性{#tag-characteristics}

* 節點類型為`cq:Tag`
* 節點名稱是` [TagID](#tagid)`的元件
* ` [TagID](#tagid)`一律包含[namespace](#tag-namespace)

* 可選`jcr:title`屬性（要在UI中顯示的標題）

* 可選`jcr:description`屬性

* 包含子節點時，稱為[container tag](#container-tags)
* 儲存在名為[分類根節點](#taxonomy-root-node)的基本路徑下的儲存庫中

### 標記 ID {#tagid}

TagID標識解析到儲存庫中標籤節點的路徑。

通常，TagID是從namespace開始的速記TagID，也可以是從[分類根節點](#taxonomy-root-node)開始的絕對TagID。

當標籤內容時，如果內容尚不存在，則` [cq:tags](#tagged-content-cq-tags-property)`屬性會新增至內容節點，而TagID會新增至屬性的String陣列值。

TagID由[namespace](#tag-namespace)和本機TagID組成。 [容器](#container-tags) 標語子標籤，代表分類法中的階層順序。子標籤可用來參照與任何本機TagID相同的標籤。 例如，即使內容是含有子標籤的容器標籤，例如「水果／蘋果」和「水果／香蕉」，也允許使用「水果」標籤內容。

### 分類根節點{#taxonomy-root-node}

分類根節點是儲存庫中所有標籤的基本路徑。 分類根節點必須&#x200B;*not*&#x200B;是類型`  cq   :Tag`的節點。

在AEM中，基本路徑為`/content/  cq   :tags`，根節點的類型為`  cq   :Folder`。

### 標籤命名空間{#tag-namespace}

名稱空間允許將事物分組。 最典型的使用案例是每個（網站）網站（例如，公用、內部和入口網站）或每個大型應用程式（例如WCM、資產、社群）擁有命名空間，但命名空間可用於各種其他需求。 使用者介面中使用名稱空間，僅顯示適用於目前內容的標籤子集（即特定名稱空間的標籤）。

標籤的命名空間是分類子樹中的第一級，該級是緊挨在[分類根節點](#taxonomy-root-node)下的節點。 namespace是`cq:Tag`類型的節點，其父代不是`cq:Tag`節點類型。

所有標籤都有命名空間。 如果未指定命名空間，則將標籤指派給預設命名空間，即TagID `default`（標題為`Standard Tags),`，即`/content/cq:tags/default.`）

### 容器標籤{#container-tags}

容器標籤是`cq:Tag`類型的節點，包含任意數目和類型的子節點，因此可以使用自訂中繼資料來增強標籤模型。

此外，分類法中的容器標籤（或超標籤）是所有子標籤的子總和：例如，使用水果／蘋果標籤的內容也被視為使用水果標籤，即搜索僅使用水果標籤的內容也會查找使用水果／蘋果標籤的內容。

### 解析TagID {#resolving-tagids}

如果標籤ID包含冒號&quot;:&quot;，冒號會將名稱空間與標籤或子分類分類分開，然後使用正常斜槓&quot;/&quot;分開。 如果標籤ID沒有冒號，則會隱含預設命名空間。

標籤的標準和唯一位置位於/content/cq:tags下方。

參考非現有路徑或路徑的標籤不指向cq：標籤節點被視為無效且被忽略。

下表顯示一些TagID範例、其元素，以及TagID解析為儲存庫中絕對路徑的方式：

下表顯示一些TagID範例、其元素，以及TagID解析為儲存庫中絕對路徑的方式：
下表顯示一些TagID範例、其元素，以及TagID解析為儲存庫中絕對路徑的方式：

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
   <td>dam:fruit/apple/braeburn</td>
   <td>壩</td>
   <td>水果／蘋果／佈雷本</td>
   <td>水果，蘋果</td>
   <td>braeburn</td>
   <td>/content/cq:tags/dam/frout/apple/braeburn</td>
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

### 標籤標題的本地化{#localization-of-tag-title}

當標籤包含可選標題字串(`jcr:title`)時，可新增屬性`jcr:title.<locale>`來本地化要顯示的標題。

如需詳細資訊，請參閱

* [不同語言的標籤](/help/sites-developing/building.md#tags-in-different-languages) -說明API的使用
* [以不同語言管理標籤](/help/sites-administering/tags.md#managing-tags-in-different-languages) -說明使用標籤控制台

### 存取控制 {#access-control}

標籤作為[分類根節點](#taxonomy-root-node)下的節點存在。 允許或拒絕作者和站點訪客在給定名稱空間中建立標籤，可以通過在儲存庫中設定適當的ACL來實現。

此外，拒絕某些標籤或名稱空間的讀取權限將控制將標籤應用於特定內容的能力。

典型做法包括：

* 允許對所有名稱空間（在`/content/cq:tags`下添加／修改）的`tag-administrators`組／角色寫訪問。 此群組隨附AEM現成可用功能。

* 允許用戶／作者讀取對所有應該對其可讀取的名稱空間（大部分）的訪問權。
* 允許用戶／作者對用戶／作者可自由定義標籤的命名空間進行寫入訪問（`/content/cq:tags/some_namespace`下的add_node）

## 可標籤內容：cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

為了讓應用程式開發人員將標籤附加到內容類型，節點的註冊([CND](https://jackrabbit.apache.org/node-type-notation.html))必須包括`cq:Taggable`混合或`cq:OwnerTaggable`混合。

`cq:OwnerTaggable` mixin繼承自`cq:Taggable`，其目的是指出內容可由擁有者／作者分類。 在AEM中，它只是`cq:PageContent`節點的屬性。 標籤框架不需要`cq:OwnerTaggable` mixin。

>[!NOTE]
>
>建議僅在匯總內容項目（或其jcr:content節點）的頂層節點上啟用標籤。 範例包括：
>
>* 頁面(`cq:Page`)，其中`jcr:content`節點類型`cq:PageContent`，其中包含`cq:Taggable`混音。
   >
   >
* 資產(`cq:Asset`)，其中`jcr:content/metadata`節點一律具有`cq:Taggable` mixin。

>



### 節點類型標籤(CND){#node-type-notation-cnd}

節點類型定義作為CND檔案存在於儲存庫中。 CND符號定義為JCR文檔[此處](https://jackrabbit.apache.org/node-type-notation.html)的一部分。

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

## 標籤內容：cq:tags屬性{#tagged-content-cq-tags-property}

`cq:tags`屬性是一個String陣列，當作者或網站訪客將一或多個TagID套用至內容時，這些TagID會被用來儲存。 該屬性僅在添加到以`[cq:Taggable](#taggable-content-cq-taggable-mixin)` mixin定義的節點時有意義。

>[!NOTE]
>
>若要運用AEM標籤功能，自訂開發的應用程式不應定義`cq:tags`以外的標籤屬性。

## 移動和合併標籤{#moving-and-merging-tags}

以下是使用[標籤控制台](/help/sites-administering/tags.md)移動或合併標籤時儲存庫中效果的說明：

* 將標籤A移動或合併到`/content/cq:tags`下的標籤B時：

   * 標籤A未刪除，並獲取`cq:movedTo`屬性。
   * 標籤B已建立（在移動時）並獲取`cq:backlinks`屬性。

* `cq:movedTo` 指向標籤B。此屬性表示標籤A已移動或合併到標籤B。移動標籤B將相應地更新此屬性。標籤A因此會隱藏，並且僅保存在儲存庫中，以解析指向標籤A的內容節點中的標籤ID。標籤廢棄項目收集器會移除標籤A等標籤，不再有內容節點指向標籤A。
`cq:movedTo`屬性的特殊值為`nirvana`:它將在標籤刪除時應用，但無法從儲存庫中刪除，因為必須保留具有`cq:movedTo`的子標籤。

   >[!NOTE]
   >
   >`cq:movedTo`屬性只會在符合下列任一條件時，新增至已移動或合併的標籤：
   > 1. 標籤用於內容（亦即它有參考）或
   > 1. 標籤包含已移動的子項。


* `cq:backlinks` 將參照保持在另一個方向，即保留已移動到標籤B或與標籤B合併的所有標籤的清單。當標籤B移動／合併／刪 `cq:movedTo`除時，或標籤B啟動時，這通常需要保持屬性的最新狀態，在此情況下，其所有的回溯連結標籤也必須啟用。

   >[!NOTE]
   >
   >`cq:backlinks`屬性只會在符合下列任一條件時，新增至已移動或合併的標籤：
   >
   > 1. 標籤用於內容（亦即它有參考）或    >
   > 1. 標籤包含已移動的子項。


* 讀取內容節點的`cq:tags`屬性涉及以下解析：

   1. 如果`/content/cq:tags`下沒有相符項目，則不會傳回任何標籤。
   1. 如果標籤具有`cq:movedTo`屬性集，則會遵循參考的標籤ID。
只要後面的標籤有`cq:movedTo`屬性，就會重複此步驟。

   1. 如果後面的標籤沒有`cq:movedTo`屬性，則會讀取標籤。

* 要在標籤已移動或合併時發佈更改，必須複製`cq:Tag`節點及其所有回鏈：當標籤在標籤管理主控台中啟動時，就會自動執行此動作。

* 稍後對頁面`cq:tags`屬性的更新會自動清除「舊」參照。 觸發此項是因為透過API解析移動的標籤會傳回目標標籤，因此提供目標標籤ID。

>[!NOTE]
>
>標籤移動與標籤移轉不同。

## 標籤遷移{#tags-migration}

Experience Manager 6.4版以上的標籤會儲存在`/content/cq:tags`下，而之前儲存在`/etc/tags`下。 但是，在Adobe Experience Manager已從舊版升級的情況下，標籤仍會出現在舊位置`/etc/tags`下。 在升級的系統中，標籤需要在`/content/cq:tags`下遷移。

>[!NOTE]
>
>在「標籤的頁面屬性」頁面中，建議使用標籤ID(`geometrixx-outdoors:activity/biking`)，而非硬式編碼標籤基本路徑（例如`/etc/tags/geometrixx-outdoors/activity/biking`）。
>
>若要列出標籤，可使用`com.day.cq.tagging.servlets.TagListServlet`。

>[!NOTE]
>
>建議使用標籤管理器API作為資源。

### 如果升級的AEM例項支援TagManager API {#upgraded-instance-support-tagmanager-api}

1. 在元件開始時，TagManager API會偵測它是否為升級的AEM例項。 在升級的系統中，標籤儲存在`/etc/tags`下。

1. 然後，TagManager API會在向後相容性模式下執行，這表示API使用`/etc/tags`作為基本路徑。 如果沒有，則使用新位置`/content/cq:tags`。

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

該指令碼將讀取所有在`cq:movedTo/cq:backLinks`屬性值中具有`/etc/tags`的標籤。 然後，它會重複擷取的結果集，並將`cq:movedTo`和`cq:backlinks`屬性值解析為`/content/cq:tags`路徑（在該值中偵測到`/etc/tags`的情況下）。

### 如果升級的AEM例項在Classic UI {#upgraded-instance-runs-classic-ui}上執行

>[!NOTE]
>
>傳統UI不符合零停機時間要求，也不支援新的標籤庫路徑。 如果您想要使用`/etc/tags`以外的傳統UI，則需先建立`cq-tagging`元件重新啟動。

若是TagManager API支援並在Classic UI中執行的升級AEM例項：

1. 使用tagId或新標籤位置`/content/cq:tags`取代對舊標籤基本路徑`/etc/tags`的參考後，您就可將標籤移轉至CRX中新位置`/content/cq:tags`，然後再重新啟動元件。

1. 將標籤移轉至新位置後，請執行上述指令碼。
