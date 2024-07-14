---
title: 將標籤建置到AEM應用程式中
description: 以程式設計方式處理自訂AEM應用程式內的標籤或擴展標籤
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
feature: Developing,Tagging
exl-id: d885520d-d0ed-45fa-8511-faa2495d667a
solution: Experience Manager, Experience Manager Sites
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '868'
ht-degree: 0%

---

# 將標籤建置到AEM應用程式中{#building-tagging-into-an-aem-application}

若要以程式設計方式使用自訂AEM應用程式中的標籤或擴充標籤，本頁會說明如何使用

* [標籤API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/tagging/package-summary.html)

那個會與

* [標籤框架](/help/sites-developing/framework.md)

如需關於標籤的相關資訊，請參閱：

* [管理標籤](/help/sites-administering/tags.md)，以取得建立和管理標籤的相關資訊，以及已套用標籤的內容。
* [使用標籤](/help/sites-authoring/tags.md)以取得關於標籤內容的資訊。

## 標籤API的總覽 {#overview-of-the-tagging-api}

AEM中[標籤架構](/help/sites-developing/framework.md)的實作允許使用JCR API管理標籤和標籤內容。 TagManager會確保在`cq:tags`字串陣列屬性上作為值輸入的標籤不會重複，它會移除指向不存在標籤的TagID，並更新已移動或合併標籤的標籤ID。 TagManager會使用JCR觀察監聽器來回覆任何不正確的變更。 主要類別位於[com.day.cq.tagging](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/tagging/package-summary.html)封裝中：

* JcrTagManagerFactory — 傳回`TagManager`的JCR型實作。 此版本為「標籤API」的參考實作。
* `TagManager` — 允許依路徑和名稱解析及建立標籤。
* `Tag` — 定義標籤物件。

### 取得JCR型TagManager {#getting-a-jcr-based-tagmanager}

若要擷取TagManager執行個體，您必須有JCR `Session`，並且要呼叫`getTagManager(Session)`：

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

在一般Sling內容中，您也可以從`ResourceResolver`調整`TagManager`：

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### 擷取標籤物件 {#retrieving-a-tag-object}

可透過`TagManager`透過解析現有標籤或建立標籤來擷取`Tag`：

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

對於將`Tags`對應到JCR `Nodes`的JCR型實作，如果您有資源（例如`/content/cq:tags/default/my/tag`），可以直接使用Sling的`adaptTo`機制：

```java
Tag tag = resource.adaptTo(Tag.class);
```

雖然標籤只能從*資源（而非節點）轉換*而來，但標籤可以轉換為*節點和資源：

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>無法直接從`Node`調整為`Tag`，因為`Node`未實作Sling `Adaptable.adaptTo(Class)`方法。

### 取得和設定標籤 {#getting-and-setting-tags}

```java
// Getting the tags of a Resource:
Tag[] tags = tagManager.getTags(resource);

// Setting tags to a Resource:
tagManager.setTags(resource, tags);
```

### 搜尋標籤 {#searching-for-tags}

```java
// Searching for the Resource objects that are tagged with the tag object:
Iterator<Resource> it = tag.find();

// Retrieving the usage count of the tag object:
long count = tag.getCount();

// Searching for the Resource objects that are tagged with the tagID String:
 RangeIterator<Resource> it = tagManager.find(tagID);
```

>[!NOTE]
>
>要使用的有效`RangeIterator`為：
>
>`com.day.cq.commons.RangeIterator`

### 刪除標記 {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### 複製標籤 {#replicating-tags}

可以使用具有標籤的復寫服務( `Replicator`)，因為標籤的型別為`nt:hierarchyNode`：

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## 在使用者端上標籤 {#tagging-on-the-client-side}

表單Widget `CQ.tagging.TagInputField`用於輸入標籤。 它有一個彈出式選單，可供您從現有標籤中選取，包括自動完成和許多其他功能。 其xtype為`tags`。

## 標籤記憶體回收器 {#the-tag-garbage-collector}

標籤記憶體回收行程是一種背景服務，可清除隱藏且未使用的標籤。 隱藏和未使用的標籤是`/content/cq:tags`以下的標籤，這些標籤具有`cq:movedTo`屬性，而且未用於內容節點 — 它們的計數為零。 透過使用這個延遲刪除程式，內容節點（即`cq:tags`屬性）不必隨著移動或合併操作而更新。 更新`cq:tags`屬性時（例如，透過頁面屬性對話方塊），`cq:tags`屬性中的參考會自動更新。

標籤記憶體回收行程預設為每天執行一次。 您可以在下列位置進行設定：

```xml
http://localhost:4502/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector
```

## 標籤搜尋和標籤清單 {#tag-search-and-tag-listing}

搜尋標籤和標籤清單的工作方式如下：

* 搜尋TagID會搜尋屬性`cq:movedTo`設為TagID並遵循`cq:movedTo` TagID的標籤。

* 搜尋標籤Title只會搜尋沒有`cq:movedTo`屬性的標籤。

## 不同語言的標籤 {#tags-in-different-languages}

如管理標籤的檔案中所述，在[管理不同語言的標籤](/help/sites-administering/tags.md#managing-tags-in-different-languages)一節中，可以使用不同語言定義標籤`title`。 然後，區分語言的屬性會新增至標籤節點。 這個屬性的格式為`jcr:title.<locale>`，例如，法文翻譯為`jcr:title.fr`。 `<locale>`必須是小寫的ISO地區設定字串，並使用「_」而非「 — 」，例如： `de_ch`。

將&#x200B;**Animals**&#x200B;標籤新增至&#x200B;**Products**&#x200B;頁面時，值`stockphotography:animals`會新增至節點/content/geometrixx/en/products/jcr：content的屬性`cq:tags`。 將從標籤節點引用翻譯。

伺服器端API已本地化`title`相關方法：

* [com.day.cq.tagging.Tag](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/tagging/Tag.html)

   * getLocalizedTitle（地區設定）
   * getLocalizedTitlePaths()
   * getLocalizedTitles()
   * getTitle（地區設定）
   * getTitlePath（地區設定）

* [com.day.cq.tagging.TagManager](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/tagging/TagManager.html)

   * canCreateTagByTitle(String tagTitlePath， Locale)
   * createTagByTitle(String tagTitlePath， Locale)
   * resolveByTitle(String tagTitlePath， Locale)

在AEM中，可以從頁面語言或使用者語言取得語言：

* 擷取JSP中的頁面語言：

   * `currentPage.getLanguage(false)`

* 擷取JSP中的使用者語言：

   * `slingRequest.getLocale()`

`currentPage`和`slingRequest`可透過[&lt;cq：definedObjects>](/help/sites-developing/taglib.md)標籤在JSP中使用。

對於標籤，本地化取決於內容，因為標籤`titles`可以頁面語言、使用者語言或任何其他語言顯示。

### 新增語言至編輯標籤對話方塊 {#adding-a-new-language-to-the-edit-tag-dialog}

下列程式說明如何將語言（芬蘭文）新增到&#x200B;**標籤編輯**&#x200B;對話方塊：

1. 在&#x200B;**CRXDE**&#x200B;中，編輯節點`/content/cq:tags`的多值屬性`languages`。

1. 新增`fi_fi` （代表芬蘭語言環境）並儲存變更。

在&#x200B;**標籤**&#x200B;主控台中編輯標籤時，現在可以在頁面屬性的標籤對話方塊和&#x200B;**編輯標籤**&#x200B;對話方塊中使用新語言（芬蘭文）。

>[!NOTE]
>
>新語言必須是AEM認可的語言之一。 也就是說，它必須能做為`/libs/wcm/core/resources/languages`以下的節點。

>[!CAUTION]
>
>透過官方更新套件（包括Service Pack、Security Service Pack、Extended Feature Pack、Cumulative Feature Pack、修補程式等）安裝標籤相關現成可用的內容，會將`/content/cq:tags`節點的languages屬性重設為預設值。 因此，在安裝之前，必須從屬性新增它。
