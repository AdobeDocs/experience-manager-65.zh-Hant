---
title: 建立標籤至AEM應用程式
seo-title: 建立標籤至AEM應用程式
description: 以程式設計方式在自訂AEM應用程式中處理標籤或擴充標籤
seo-description: 以程式設計方式在自訂AEM應用程式中處理標籤或擴充標籤
uuid: 0549552e-0d51-4162-b418-babf4ceee046
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 032aea1f-0105-4299-8d32-ba6bee78437f
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# 建立標籤至AEM應用程式{#building-tagging-into-an-aem-application}

為了以程式設計方式處理自訂AEM應用程式中的標籤或擴充標籤，本頁說明

* [標籤API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html)

與

* [標籤框架](/help/sites-developing/framework.md)

有關標籤的相關資訊，請參見：

* [管理標籤](/help/sites-administering/tags.md) ，以取得建立和管理標籤以及已套用內容標籤的相關資訊。
* [使用標籤](/help/sites-authoring/tags.md) ，以取得標籤內容的相關資訊。

## 標籤API概述 {#overview-of-the-tagging-api}

在AEM中實作標 [記架構](/help/sites-developing/framework.md) ，可讓您使用JCR API管理標籤和標籤內容。 TagManager可確保在字串陣列屬性中輸入為值的標籤不會重複，它會移除指向非現有標籤的TagID，並更新已移動或合併標籤的TagID。 `cq:tags` TagManager使用JCR觀察偵聽器來恢復任何不正確的更改。 主要類別位於com.day.cq.ta [ting](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/package-summary.html) package:

* JcrTagManagerFactory —— 返回基於JCR的實施 `TagManager`。 這是標籤API的參考實作。
* `TagManager` -允許依路徑和名稱來解析和建立標籤。
* `Tag` -定義標籤對象。

### 取得JCR架構的TagManager {#getting-a-jcr-based-tagmanager}

若要擷取TagManager例項，您需要有JCR `Session` 並呼叫 `getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

在典型的Sling內容中，您也可以調整以 `TagManager` 下項目 `ResourceResolver`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### 檢索標籤對象 {#retrieving-a-tag-object}

可 `Tag` 以通過解析現有標 `TagManager`記或建立新標籤來檢索：

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

若是JCR架構的實作(對應 `Tags` 至JCR `Nodes`)，若您擁有資源(例如 `adaptTo``/etc/tags/default/my/tag`)，則可直接使用Sling&#39;s機制：

```java
Tag tag = resource.adaptTo(Tag.class);
```

雖然標籤只能從*a資源（非節點）轉換*，但標籤可以*轉換為*a節點和資源：

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>無法直接 `Node` 自 `Tag` 動調整，因 `Node` 為不實作Sling `Adaptable.adaptTo(Class)` 方法。

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
>有效 `RangeIterator` 使用方式為：
>
>`com.day.cq.commons.RangeIterator`

### 刪除標籤 {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### 複製標籤 {#replicating-tags}

可以將複製服務( `Replicator`)與標籤一起使用，因為標籤類型 `nt:hierarchyNode`:

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## 在用戶端標籤 {#tagging-on-the-client-side}

`CQ.tagging.TagInputField` 是用於輸入標籤的表單Widget。 它有一個彈出式選單，可供從現有標籤中選取，包括自動完成功能和許多其他功能。 它的xtype是 `tags`。

## 標籤廢棄項目收集器 {#the-tag-garbage-collector}

標籤廢棄項目收集器是一種後台服務，可清除隱藏和未使用的標籤。 隱藏和未使用的標籤是下 `/etc/tags` 方具有屬 `cq:movedTo` 性且不用於內容節點的標籤——它們的計數為零。 通過使用此延遲刪除過程，內容節點(即屬性 `cq:tags` )不必作為移動或合併操作的一部分進行更新。 屬性中的參 `cq:tags` 照在更新屬性時會自動 `cq:tags` 更新，例如透過頁面屬性對話方塊。

標籤廢棄項目收集器依預設每天執行一次。 This can be configured at:

```xml
http://localhost:4502/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector
```

## 標籤搜尋和標籤清單 {#tag-search-and-tag-listing}

搜尋標籤和標籤清單的運作方式如下：

* 搜尋TagID會搜尋屬性設為TagID並依循 `cq:movedTo` TagID的標 `cq:movedTo` 記。

* 搜尋標籤「標題」僅搜尋沒有屬性的標 `cq:movedTo` 記。

## 不同語言的標籤 {#tags-in-different-languages}

如管理標籤的說明檔案中所述，在「管理不同語 [言中的標籤](/help/sites-administering/tags.md#managing-tags-in-different-languages)」一節中 `title`，可以定義不同語言的標籤。 然後，語言敏感屬性會新增至標籤節點。 此屬性的格式 `jcr:title.<locale>`為，例如 `jcr:title.fr` 用於法語翻譯。 `<locale>` 必須是小寫的ISO地區設定字串，並使用&quot;_&quot;而非&quot;-&quot;，例如： `de_ch`。

將 **Animals** 標籤新增至 **Products** 頁面時，值會新增至節點/content/geometrixx/en/products/jcr:content的 `stockphotography:animals``cq:tags` 屬性。 轉換是從標籤節點引用的。

伺服器端API有本地化的 `title`相關方法：

* [com.day.cq.tating.Tag](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/Tag.html)

   * getLocalizedTitle（地區設定）
   * getLocalizedTitlePaths()
   * getLocalizedTitles()
   * getTitle（地區設定）
   * getTitlePath（地區設定）

* [com.day.cq.tating.TagManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/TagManager.html)

   * canCreateTagByTitle(String tagTitlePath, Locale)
   * createTagByTitle(String tagTitlePath, Locale locale)
   * resolveByTitle(String tagTitlePath, Locale)

在AEM中，語言可從頁面語言或使用者語言取得：

* 要在JSP中檢索頁面語言，請執行以下操作：

   * `currentPage.getLanguage(false)`

* 要在JSP中檢索用戶語言，請執行以下操作：

   * `slingRequest.getLocale()`

`currentPage` 和 `slingRequest` 可透過 [&lt;cq:definedObjects>標籤在JSP中使用](/help/sites-developing/taglib.md) 。

對於標籤，本地化取決於上下文，因 `titles`為標籤可以以頁面語言、用戶語言或任何其他語言顯示。

### 將新語言添加到「編輯標籤」對話框 {#adding-a-new-language-to-the-edit-tag-dialog}

下列程式說明如何將新語言（芬蘭文）新增至「標籤編 **輯」對話** 框：

1. 在 **CRXDE**&#x200B;中，編輯節點的多 `languages` 值屬性 `/etc/tags`。

1. 添加 `fi_fi` -代表芬蘭語地區設定——並保存更改。

在「標籤」控制台中編輯標籤時，新語言（芬蘭文）現在可在頁面屬性的標籤對話方塊和「編 **輯標籤** 」對話方 **塊中使用** 。

>[!NOTE]
>
>新語言必須是AEM認可的語言之一，例如，它必須以節點的形式提供 `/libs/wcm/core/resources/languages`。

