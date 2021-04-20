---
title: 在應用程式中建立標AEM記
seo-title: 在應用程式中建立標AEM記
description: 以程式設計方式在自訂應用程式中處理標籤或擴充標AEM記
seo-description: 以程式設計方式在自訂應用程式中處理標籤或擴充標AEM記
uuid: 0549552e-0d51-4162-b418-babf4ceee046
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 032aea1f-0105-4299-8d32-ba6bee78437f
feature: Tagging
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 0%

---


# 將標籤構建AEM到應用程式{#building-tagging-into-an-aem-application}

為了以程式設計方式處理自訂應用程式中的標籤或擴充AEM標籤，本頁說明

* [標籤API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html)

與

* [標籤框架](/help/sites-developing/framework.md)

有關標籤的相關資訊，請參見：

* [管理](/help/sites-administering/tags.md) 標籤，以取得建立和管理標籤的相關資訊，以及已套用內容標籤的資訊。
* [使用標](/help/sites-authoring/tags.md) 記內容的相關資訊。

## 標籤API {#overview-of-the-tagging-api}概述

在中實施[標籤框架](/help/sites-developing/framework.md)AEM允許使用JCR API管理標籤和標籤內容。 TagManager可確保在`cq:tags`字串陣列屬性中輸入的值標籤不會重複，它會移除指向非現有標籤的TagID，並更新已移動或合併標籤的TagID。 TagManager使用JCR觀察偵聽器來恢復任何不正確的更改。 主類位於[com.day.cq.tating](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/package-summary.html)軟體包中：

* JcrTagManagerFactory —— 返回基於JCR的`TagManager`實施。 這是標籤API的參考實作。
* `TagManager` -允許依路徑和名稱來解析和建立標籤。
* `Tag` -定義標籤對象。

### 取得JCR架構的TagManager {#getting-a-jcr-based-tagmanager}

若要擷取TagManager例項，您必須有JCR `Session`，並呼叫`getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

在典型的Sling內容中，您也可以從`ResourceResolver`調整至`TagManager`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### 檢索標籤對象{#retrieving-a-tag-object}

`Tag`可透過`TagManager`擷取，方法是解析現有標籤或建立新標籤：

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

對於JCR架構的實作（將`Tags`對應至JCR `Nodes`），如果您有資源（例如`/content/cq:tags/default/my/tag`），則可直接使用Sling的`adaptTo`機制：

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
>無法直接從`Node`改編為`Tag`，因為`Node`不實作Sling `Adaptable.adaptTo(Class)`方法。

### 獲取和設定標籤{#getting-and-setting-tags}

```java
// Getting the tags of a Resource:
Tag[] tags = tagManager.getTags(resource);

// Setting tags to a Resource:
tagManager.setTags(resource, tags);
```

### 搜索標籤{#searching-for-tags}

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
>使用的有效`RangeIterator`是：
>
>`com.day.cq.commons.RangeIterator`

### 刪除標籤{#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### 複製標籤{#replicating-tags}

可以將複製服務(`Replicator`)與標籤一起使用，因為標籤的類型為`nt:hierarchyNode`:

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## 在客戶端{#tagging-on-the-client-side}上標籤

`CQ.tagging.TagInputField` 是用於輸入標籤的表單Widget。它有一個彈出式選單，可供從現有標籤中選取，包括自動完成功能和許多其他功能。 其xtype為`tags`。

## 標籤廢棄項目收集器{#the-tag-garbage-collector}

標籤廢棄項目收集器是一種後台服務，可清除隱藏和未使用的標籤。 隱藏和未使用的標籤是位於`/content/cq:tags`下方的標籤，具有`cq:movedTo`屬性且不用於內容節點——它們的計數為零。 通過使用此延遲刪除過程，內容節點（即`cq:tags`屬性）不必作為移動或合併操作的一部分進行更新。 當`cq:tags`屬性更新時，`cq:tags`屬性中的引用會自動更新，例如透過頁面屬性對話方塊。

標籤廢棄項目收集器依預設每天執行一次。 This can be configured at:

```xml
http://localhost:4502/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector
```

## 標籤搜索和標籤清單{#tag-search-and-tag-listing}

搜尋標籤和標籤清單的運作方式如下：

* 搜尋TagID會搜尋屬性`cq:movedTo`設為TagID並遵循`cq:movedTo` TagID的標籤。

* 搜尋標籤標題只會搜尋沒有`cq:movedTo`屬性的標籤。

## 不同語言的標籤{#tags-in-different-languages}

如標籤管理說明檔案中所述，在[管理不同語言的標籤](/help/sites-administering/tags.md#managing-tags-in-different-languages)一節中，標籤`title`可以定義為不同語言。 然後，語言敏感屬性會新增至標籤節點。 此屬性的格式為`jcr:title.<locale>`，例如`jcr:title.fr`，用於法文翻譯。 `<locale>` 必須是小寫的ISO地區設定字串，並使用&quot;_&quot;而非&quot;-&quot;，例如： `de_ch`.

將&#x200B;**Animals**&#x200B;標籤添加到&#x200B;**Products**&#x200B;頁面時，值`stockphotography:animals`將添加到節點/content/geometrixx/en/products/jcr:content的屬性`cq:tags`中。 轉換是從標籤節點引用的。

伺服器端API已本地化`title`相關方法：

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

`currentPage` 和 `slingRequest` 可在JSP中透過標籤使 [&lt;cq:definedobjects>](/help/sites-developing/taglib.md) 用。

對於標籤，本地化取決於上下文，因為標籤`titles`可以以頁面語言、用戶語言或任何其他語言顯示。

### 將新語言添加到編輯標籤對話框{#adding-a-new-language-to-the-edit-tag-dialog}

以下過程說明如何向&#x200B;**標籤編輯**&#x200B;對話框添加新語言（芬蘭文）:

1. 在&#x200B;**CRXDE**&#x200B;中，編輯節點`/content/cq:tags`的多值屬性`languages`。

1. 新增`fi_fi` —— 代表芬蘭語地區設定——並儲存變更。

在&#x200B;**標籤**&#x200B;主控台中編輯標籤時，新語言（芬蘭文）現在可在頁面屬性的標籤對話方塊和&#x200B;**編輯標籤**&#x200B;對話方塊中使用。

>[!NOTE]
>
>新語言必須是其中一AEM種公認的語言，即它必須作為`/libs/wcm/core/resources/languages`下的節點提供。

