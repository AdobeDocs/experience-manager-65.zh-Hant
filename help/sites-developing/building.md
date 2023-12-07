---
title: 將標籤建置到AEM應用程式中
description: 以程式設計方式處理自訂AEM應用程式內的標籤或擴展標籤
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
feature: Tagging
exl-id: d885520d-d0ed-45fa-8511-faa2495d667a
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 0%

---

# 將標籤建置到AEM應用程式中{#building-tagging-into-an-aem-application}

若要以程式設計方式使用自訂AEM應用程式中的標籤或擴充標籤，本頁會說明如何使用

* [標籤API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/tagging/package-summary.html)

那個會與

* [標籤框架](/help/sites-developing/framework.md)

如需關於標籤的相關資訊，請參閱：

* [管理標籤](/help/sites-administering/tags.md) 以取得關於建立和管理標籤，以及已對哪些內容標籤套用的資訊。
* [使用標籤](/help/sites-authoring/tags.md) 以取得關於標籤內容的資訊。

## 標籤API的總覽 {#overview-of-the-tagging-api}

實作 [標籤框架](/help/sites-developing/framework.md) 允許在AEM中使用JCR API管理標籤和標籤內容。 TagManager會確保在 `cq:tags` 字串陣列屬性不會重複，它會移除指向不存在標籤的TagID，並更新已移動或合併標籤的標籤ID。 TagManager會使用JCR觀察監聽器來回覆任何不正確的變更。 主要類別位於 [com.day.cq.tagg](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/tagging/package-summary.html) 封裝：

* JcrTagManagerFactory — 傳回JCR型實作 `TagManager`. 此版本為「標籤API」的參考實作。
* `TagManager`  — 允許依路徑和名稱解析和建立標籤。
* `Tag`  — 定義標籤物件。

### 取得JCR型TagManager {#getting-a-jcr-based-tagmanager}

若要擷取TagManager例項，您必須有JCR `Session` 並呼叫 `getTagManager(Session)`：

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

在一般Sling情境下，您也可以調整 `TagManager` 從 `ResourceResolver`：

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### 擷取標籤物件 {#retrieving-a-tag-object}

A `Tag` 可透過 `TagManager`，解析現有標籤或建立現有標籤：

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

對於以JCR為基礎的實作，其會 `Tags` 前往JCR `Nodes`，您可以直接使用Sling `adaptTo` 機制(如果您有資源，例如 `/content/cq:tags/default/my/tag`)：

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
>直接改寫自 `Node` 至 `Tag` 是不可能的，因為 `Node` 不實作Sling `Adaptable.adaptTo(Class)` 方法。

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
>有效的 `RangeIterator` 要使用的是：
>
>`com.day.cq.commons.RangeIterator`

### 刪除標記 {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### 複製標籤 {#replicating-tags}

可以使用復寫服務( `Replicator`)與標籤，因為標籤的型別為 `nt:hierarchyNode`：

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## 在使用者端上標籤 {#tagging-on-the-client-side}

表單Widget `CQ.tagging.TagInputField` 用於輸入標籤。 它有一個彈出式選單，可供您從現有標籤中選取，包括自動完成和許多其他功能。 其xtype為 `tags`.

## 標籤記憶體回收器 {#the-tag-garbage-collector}

標籤記憶體回收行程是一種背景服務，可清除隱藏且未使用的標籤。 隱藏和未使用的標籤是底下的標籤 `/content/cq:tags` 具有 `cq:movedTo` 屬性且不會在內容節點上使用 — 它們的計數為零。 透過使用此延遲刪除程式，內容節點(即 `cq:tags` 屬性)，不必隨著移動或合併作業進行更新。 中的參照 `cq:tags` 屬性會在 `cq:tags` 屬性會更新，例如透過頁面屬性對話方塊。

標籤記憶體回收行程預設為每天執行一次。 您可以在下列位置進行設定：

```xml
http://localhost:4502/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector
```

## 標籤搜尋和標籤清單 {#tag-search-and-tag-listing}

搜尋標籤和標籤清單的工作方式如下：

* 搜尋TagID會搜尋具有屬性的標籤 `cq:movedTo` 設為TagID並遵循 `cq:movedTo` 標籤ID。

* 搜尋標籤「標題」只會搜尋沒有欄位的標籤。 `cq:movedTo` 屬性。

## 不同語言的標籤 {#tags-in-different-languages}

如管理標籤的檔案一節中所述 [管理不同語言的標籤](/help/sites-administering/tags.md#managing-tags-in-different-languages)，標籤 `title`能以不同語言定義。 然後，區分語言的屬性會新增至標籤節點。 此屬性的格式為 `jcr:title.<locale>`例如， `jcr:title.fr` 以取得法文翻譯。 此 `<locale>` 必須為小寫ISO地區設定字串，並使用「_」而非「 — 」，例如： `de_ch`.

當 **動物** 標籤已新增至 **產品** 頁面，值 `stockphotography:animals` 會新增至屬性 `cq:tags` /content/geometrixx/en/products/jcr：content節點的 將從標籤節點引用翻譯。

伺服器端API已本地化 `title`相關方法：

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

此 `currentPage` 和 `slingRequest` 可在JSP中使用，透過 [&lt;cq:definedobjects>](/help/sites-developing/taglib.md) 標籤之間。

對於標籤，本地化取決於作為標籤的內容 `titles`能以頁面語言、使用者語言或任何其他語言顯示。

### 新增語言至編輯標籤對話方塊 {#adding-a-new-language-to-the-edit-tag-dialog}

下列程式說明如何將語言（芬蘭文）新增至 **標籤編輯** 對話方塊：

1. 在 **CRXDE**，編輯多值屬性 `languages` 節點的 `/content/cq:tags`.

1. 新增 `fi_fi`  — 代表芬蘭語言環境 — 並儲存變更。

新語言（芬蘭文）現在可以在頁面屬性的標籤對話方塊和 **編輯標籤** 對話方塊 **標籤** 主控台。

>[!NOTE]
>
>新語言必須是AEM認可的語言之一。 也就是說，它必須可作為下列節點使用 `/libs/wcm/core/resources/languages`.

>[!CAUTION]
>
>安裝Service Pack會將/content/cq：tags節點的languages屬性重設為預設值。 因此，在安裝之前，必須從屬性新增它。
