---
title: 將標籤構建到應AEM用程式
seo-title: Building Tagging into an AEM Application
description: 以寫程式方式在自定義應用程式中使用標籤或擴展標AEM記
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

# 將標籤構建到應AEM用程式{#building-tagging-into-an-aem-application}

為了以寫程式方式處理自定義應用程式中的標籤或擴展AEM標籤，本頁介紹了

* [標籤API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html)

與

* [標籤框架](/help/sites-developing/framework.md)

有關標籤的相關資訊，請參見：

* [管理標籤](/help/sites-administering/tags.md) 有關建立和管理標籤的資訊，以及已應用了哪些內容標籤。
* [使用標籤](/help/sites-authoring/tags.md) 的子菜單。

## 標籤API概述 {#overview-of-the-tagging-api}

執行 [標籤框架](/help/sites-developing/framework.md) 允AEM許使用JCR API管理標籤和標籤內容。 TagManager可確保在 `cq:tags` string array屬性不重複，它會刪除指向非現有標籤的TagID，並更新已移動或合併標籤的TagID。 TagManager使用JCR觀察偵聽器來還原任何不正確的更改。 主類位於 [com.day.cq.ta](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/package-summary.html) 包：

* JcrTagManagerFactory — 返回基於JCR的 `TagManager`。 它是Tagging API的參考實現。
* `TagManager`  — 允許按路徑和名稱解析和建立標籤。
* `Tag`  — 定義標籤對象。

### 獲取基於JCR的TagManager {#getting-a-jcr-based-tagmanager}

要檢索TagManager實例，需要有JCR `Session` 打給 `getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

在典型的Sling上下文中，您還可以適應 `TagManager` 從 `ResourceResolver`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### 檢索標籤對象 {#retrieving-a-tag-object}

A `Tag` 可以通過 `TagManager`，通過解析現有標籤或建立新標籤：

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

用於基於JCR的實現，該 `Tags` 到JCR `Nodes`你可以直接用斯林 `adaptTo` 機制。 `/content/cq:tags/default/my/tag`):

```java
Tag tag = resource.adaptTo(Tag.class);
```

雖然標籤只能從*a資源（不是節點）轉換*，但標籤可以從*a節點和資源轉換*a。

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>直接從 `Node` 至 `Tag` 不可能，因為 `Node` 沒有實施Sling `Adaptable.adaptTo(Class)` 的雙曲餘切值。

### 獲取和設定標籤 {#getting-and-setting-tags}

```java
// Getting the tags of a Resource:
Tag[] tags = tagManager.getTags(resource);

// Setting tags to a Resource:
tagManager.setTags(resource, tags);
```

### 搜索標籤 {#searching-for-tags}

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
>有效 `RangeIterator` 要使用：
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

## 在客戶端添加標籤 {#tagging-on-the-client-side}

`CQ.tagging.TagInputField` 是用於輸入標籤的表單小部件。 它有一個彈出菜單，用於從現有標籤中進行選擇，包括自動完成和許多其他功能。 其xtype為 `tags`。

## 標籤垃圾收集器 {#the-tag-garbage-collector}

標籤垃圾回收器是一種後台服務，用於清除隱藏且未使用的標籤。 隱藏標籤和未使用標籤為下面的標籤 `/content/cq:tags` 有 `cq:movedTo` 屬性且未用於內容節點 — 它們的計數為零。 通過使用此延遲刪除過程，內容節點(即 `cq:tags` 屬性)不必作為移動或合併操作的一部分進行更新。 中的引用 `cq:tags` 屬性在 `cq:tags` 屬性將更新，例如通過頁面屬性對話框。

預設情況下，標籤垃圾收集器每天運行一次。 可以在以下位置配置此項：

```xml
http://localhost:4502/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector
```

## 標籤搜索和標籤清單 {#tag-search-and-tag-listing}

搜索標籤和標籤清單工作如下：

* 搜索TagID會搜索具有該屬性的標籤 `cq:movedTo` 設定為TagID，然後 `cq:movedTo` 標籤ID

* 搜索標籤標題僅搜索沒有標籤的標籤 `cq:movedTo` 屬性。

## 不同語言中的標籤 {#tags-in-different-languages}

如管理標籤的文檔中所述，在 [管理不同語言中的標籤](/help/sites-administering/tags.md#managing-tags-in-different-languages)，標籤 `title`可以用不同的語言定義。 然後，將語言敏感屬性添加到標籤節點。 此屬性的格式 `jcr:title.<locale>`，例如 `jcr:title.fr` 翻譯成法文。 `<locale>` 必須是小寫的ISO語言環境字串，並使用&quot;_&quot;而不是&quot;-&quot;，例如： `de_ch`。

當 **動物** 標籤已添加到 **產品** 頁，該值 `stockphotography:animals` 添加到屬性 `cq:tags` 節點/content/geometrixx/en/products/jcr:content。 從標籤節點引用轉換。

伺服器端API已本地化 `title` — 相關方法：

* [com.day.cq.taging.Tag](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/Tag.html)

   * getLocalizedTitle（區域設定）
   * getLocalizedTitlePaths()
   * getLocalizedTitles()
   * getTitle（區域設定）
   * getTitlePath（區域設定）

* [com.day.cq.taging.TagManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/TagManager.html)

   * canCreateTagByTitle（String tagTitlePath，區域設定）
   * createTagByTitle（String tagTitlePath，區域設定）
   * resolveByTitle（String tagTitlePath，區域設定）

在AEM中，語言可以從頁面語言或用戶語言獲得：

* 在JSP中檢索頁面語言：

   * `currentPage.getLanguage(false)`

* 在JSP中檢索用戶語言：

   * `slingRequest.getLocale()`

`currentPage` 和 `slingRequest` 在JSP中可通過 [&lt;cq:definedobjects>](/help/sites-developing/taglib.md) 標籤。

對於標籤，本地化取決於上下文作為標籤 `titles`可以以頁面語言、用戶語言或任何其他語言顯示。

### 向「編輯標籤」對話框添加新語言 {#adding-a-new-language-to-the-edit-tag-dialog}

以下過程介紹如何向 **標籤編輯** 對話框：

1. 在 **克爾克斯德**，編輯多值屬性 `languages` 的 `/content/cq:tags`。

1. 添加 `fi_fi`  — 代表芬蘭語言環境 — 並保存更改。

新語言（芬蘭語）現在可在頁面屬性的標籤對話框中使用， **編輯標籤** 編輯標籤時 **標籤** 控制台。

>[!NOTE]
>
>新語言需要是公認的語AEM言之一，即它需要作為下面的節點提供 `/libs/wcm/core/resources/languages`。
