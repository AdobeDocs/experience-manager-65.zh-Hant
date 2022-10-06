---
title: 在AEM應用程式中建立標籤
seo-title: Building Tagging into an AEM Application
description: 以程式設計方式使用標籤，或在自訂AEM應用程式中擴充標籤
seo-description: Programmatically work with tags or extending tags within a custom AEM application
uuid: 0549552e-0d51-4162-b418-babf4ceee046
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 032aea1f-0105-4299-8d32-ba6bee78437f
feature: Tagging
exl-id: d885520d-d0ed-45fa-8511-faa2495d667a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 0%

---

# 在AEM應用程式中建立標籤{#building-tagging-into-an-aem-application}

為了以程式設計方式使用自訂AEM應用程式中的標籤或擴充標籤，本頁說明的使用

* [標籤API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html)

與

* [標籤框架](/help/sites-developing/framework.md)

如需標籤的相關資訊，請參閱：

* [管理標籤](/help/sites-administering/tags.md) ，以取得建立和管理標籤以及套用內容標籤的相關資訊。
* [使用標籤](/help/sites-authoring/tags.md) 以取得標籤內容的相關資訊。

## 標籤API概觀 {#overview-of-the-tagging-api}

實施 [標籤框架](/help/sites-developing/framework.md) 在AEM中允許使用JCR API管理標籤和標籤內容。 TagManager可確保在 `cq:tags` 字串陣列屬性不會重複，會移除指向非現有標籤的TagID，並更新已移動或合併標籤的TagID。 TagManager使用JCR觀察監聽器來回復任何不正確的變更。 主要類別位於 [com.day.cq.tagging](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/package-summary.html) 包：

* JcrTagManagerFactory — 傳回以JCR為基礎的實作 `TagManager`. 這是標籤API的參考實作。
* `TagManager`  — 可依路徑和名稱解析及建立標籤。
* `Tag`  — 定義標籤物件。

### 取得JCR型TagManager {#getting-a-jcr-based-tagmanager}

若要擷取TagManager例項，您需要有JCR `Session` 和 `getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

在一般的Sling內容中，您也可以適應 `TagManager` 從 `ResourceResolver`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### 擷取標籤物件 {#retrieving-a-tag-object}

A `Tag` 可透過 `TagManager`，方法為解析現有標籤或建立新標籤：

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

針對JCR型實作，會映射 `Tags` JCR `Nodes`，您可以直接使用Sling的 `adaptTo` 機制(例如 `/content/cq:tags/default/my/tag`):

```java
Tag tag = resource.adaptTo(Tag.class);
```

雖然標籤只能從*資源（而非節點）轉換*，但標籤可以*轉換為*節點和資源：

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>直接從 `Node` to `Tag` 不可能，因為 `Node` 不實作Sling `Adaptable.adaptTo(Class)` 方法。

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
>有效 `RangeIterator` 若要使用：
>
>`com.day.cq.commons.RangeIterator`

### 刪除標籤 {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### 複製標籤 {#replicating-tags}

可以使用複製服務( `Replicator`)，因為標籤屬於類型 `nt:hierarchyNode`:

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## 在用戶端上標籤 {#tagging-on-the-client-side}

`CQ.tagging.TagInputField` 是用於輸入標籤的表單小工具。 它有一個彈出式功能表，可從現有標籤中選取，包括自動完成功能和許多其他功能。 其xtype為 `tags`.

## 標籤垃圾收集器 {#the-tag-garbage-collector}

標籤垃圾收集器是一種背景服務，可清除隱藏且未使用的標籤。 隱藏和未使用的標籤為下方的標籤 `/content/cq:tags` 有 `cq:movedTo` 屬性和不用於內容節點 — 它們的計數為零。 透過使用此延遲刪除程式，內容節點(即 `cq:tags` 屬性)，則不必隨著移動或合併操作而更新。 中的參考 `cq:tags` 屬性會在 `cq:tags` 屬性會更新，例如透過頁面屬性對話方塊。

標籤垃圾收集器預設會每天執行一次。 這可在下列位置進行設定：

```xml
http://localhost:4502/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector
```

## 標籤搜尋和標籤清單 {#tag-search-and-tag-listing}

搜尋標籤和標籤清單的運作方式如下：

* 搜尋TagID會搜尋具有屬性的標籤 `cq:movedTo` 設為TagID，並遵循 `cq:movedTo` TagIDs。

* 搜尋「標題」只會搜尋沒有 `cq:movedTo` 屬性。

## 不同語言中的標籤 {#tags-in-different-languages}

如管理標籤的檔案所述，位於 [管理不同語言中的標籤](/help/sites-administering/tags.md#managing-tags-in-different-languages)，標籤 `title`可定義為不同語言。 接著，會將語言敏感屬性新增至標籤節點。 此屬性的格式為 `jcr:title.<locale>`，例如 `jcr:title.fr` 翻譯成法語。 `<locale>` 必須是小寫的ISO區域設定字串，並使用&quot;_&quot;而非&quot;-&quot;，例如： `de_ch`.

當 **動物** 標籤已新增至 **產品** 頁面，值 `stockphotography:animals` 會新增至屬性 `cq:tags` /content/geometrixx/en/products/jcr:content. 轉譯會從標籤節點參考。

伺服器端API已本地化 `title` — 相關方法：

* [com.day.cq.tagging.Tag](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/Tag.html)

   * getLocalizedTitle（地區設定）
   * getLocalizedTitlePaths()
   * getLocalizedTitles()
   * getTitle（地區設定）
   * getTitlePath（地區設定）

* [com.day.cq.tagging.TagManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/TagManager.html)

   * canCreateTagByTitle（字串tagTitlePath，地區）
   * createTagByTitle（字串tagTitlePath，地區設定）
   * resolveByTitle（字串tagTitlePath，區域設定）

在AEM中，語言可從頁面語言或使用者語言取得：

* 要在JSP中檢索頁語言，請執行以下操作：

   * `currentPage.getLanguage(false)`

* 要在JSP中檢索用戶語言，請執行以下操作：

   * `slingRequest.getLocale()`

`currentPage` 和 `slingRequest` 在JSP中可通過 [&lt;cq:definedobjects>](/help/sites-developing/taglib.md) 標籤。

對於標籤，本地化取決於作為標籤的上下文 `titles`可以以頁面語言、使用者語言或任何其他語言顯示。

### 將新語言添加到編輯標籤對話框 {#adding-a-new-language-to-the-edit-tag-dialog}

以下程式說明如何將新語言（芬蘭文）新增至 **標籤編輯** 對話框：

1. 在 **CRXDE**，編輯多值屬性 `languages` 的 `/content/cq:tags`.

1. 新增 `fi_fi`  — 代表芬蘭語地區設定 — 並儲存變更。

新語言（芬蘭文）現在可在頁面屬性的標籤對話方塊和 **編輯標籤** 對話方塊 **標籤** 控制台。

>[!NOTE]
>
>新語言必須是AEM認可的語言之一，亦即需以下節點的形式提供 `/libs/wcm/core/resources/languages`.
