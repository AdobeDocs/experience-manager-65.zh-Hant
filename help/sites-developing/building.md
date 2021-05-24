---
title: 在AEM應用程式中建立標籤
seo-title: 在AEM應用程式中建立標籤
description: 以程式設計方式使用標籤，或在自訂AEM應用程式中擴充標籤
seo-description: 以程式設計方式使用標籤，或在自訂AEM應用程式中擴充標籤
uuid: 0549552e-0d51-4162-b418-babf4ceee046
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 032aea1f-0105-4299-8d32-ba6bee78437f
feature: 標記
exl-id: d885520d-d0ed-45fa-8511-faa2495d667a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 0%

---

# 在AEM應用程式中建立標籤{#building-tagging-into-an-aem-application}

為了以程式設計方式使用自訂AEM應用程式中的標籤或擴充標籤，本頁說明的使用

* [標籤API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html)

與

* [標籤框架](/help/sites-developing/framework.md)

如需標籤的相關資訊，請參閱：

* [管](/help/sites-administering/tags.md) 理標籤，以取得建立和管理標籤的相關資訊，以及套用了哪些內容標籤。
* [使用標](/help/sites-authoring/tags.md) 記內容的相關資訊。

## 標籤API {#overview-of-the-tagging-api}概述

在AEM中實作[標籤架構](/help/sites-developing/framework.md)可使用JCR API管理標籤和標籤內容。 TagManager可確保在`cq:tags`字串陣列屬性上輸入作為值的標籤不會重複，它會移除指向非現有標籤的TagID，並更新已移動或合併標籤的TagID。 TagManager使用JCR觀察監聽器來回復任何不正確的變更。 主類位於[com.day.cq.tagging](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/package-summary.html)包中：

* JcrTagManagerFactory — 傳回`TagManager`以JCR為基礎的實作。 這是標籤API的參考實作。
* `TagManager`  — 可依路徑和名稱解析及建立標籤。
* `Tag`  — 定義標籤物件。

### 獲取基於JCR的TagManager {#getting-a-jcr-based-tagmanager}

若要擷取TagManager例項，您需要有JCR `Session`並呼叫`getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

在一般的Sling內容中，您也可以從`ResourceResolver`調整為`TagManager`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### 檢索標籤對象{#retrieving-a-tag-object}

透過`TagManager`可解析現有標籤或建立新標籤來擷取`Tag`:

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

對於以JCR為基礎的實作（將`Tags`對應至JCR `Nodes`），如果您有資源（例如`/content/cq:tags/default/my/tag`），則可直接使用Sling的`adaptTo`機制：

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
>無法直接從`Node`調整為`Tag`，因為`Node`不實作Sling `Adaptable.adaptTo(Class)`方法。

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
>使用的有效`RangeIterator`為：
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

## 在用戶端{#tagging-on-the-client-side}上標籤

`CQ.tagging.TagInputField` 是用於輸入標籤的表單小工具。它有一個彈出式功能表，可從現有標籤中選取，包括自動完成功能和許多其他功能。 其類型為`tags`。

## 標籤垃圾收集器{#the-tag-garbage-collector}

標籤垃圾收集器是一種背景服務，可清除隱藏且未使用的標籤。 隱藏和未使用的標籤是位於`/content/cq:tags`下方的標籤，其具有`cq:movedTo`屬性且未用於內容節點 — 其計數為零。 使用此延遲刪除程式，內容節點（即`cq:tags`屬性）不必隨著移動或合併操作而更新。 更新`cq:tags`屬性時，`cq:tags`屬性中的參照會自動更新，例如透過頁面屬性對話方塊。

標籤垃圾收集器預設會每天執行一次。 這可在下列位置進行設定：

```xml
http://localhost:4502/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector
```

## 標籤搜索和標籤清單{#tag-search-and-tag-listing}

搜尋標籤和標籤清單的運作方式如下：

* 搜尋TagID會搜尋將`cq:movedTo`屬性設為TagID並貫穿`cq:movedTo` TagID的標籤。

* 搜尋標籤標題只會搜尋沒有`cq:movedTo`屬性的標籤。

## 不同語言的標籤{#tags-in-different-languages}

如管理標籤的檔案所述，在[管理不同語言的標籤](/help/sites-administering/tags.md#managing-tags-in-different-languages)區段中，標籤`title`可以以不同語言定義。 接著，會將語言敏感屬性新增至標籤節點。 此屬性的格式為`jcr:title.<locale>`，例如`jcr:title.fr`，以取得法文翻譯。 `<locale>` 必須是小寫的ISO區域設定字串，並使用&quot;_&quot;而非&quot;-&quot;，例如： `de_ch`.

將&#x200B;**Animals**&#x200B;標籤添加到&#x200B;**Products**&#x200B;頁面時，將值`stockphotography:animals`添加到節點/content/geometrixx/en/products/jcr:content的屬性`cq:tags`中。 轉譯會從標籤節點參考。

伺服器端API已本地化`title`相關方法：

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

`currentPage` 和 `slingRequest` 可在JSP中通過標籤使 [&lt;cq:definedobjects>](/help/sites-developing/taglib.md) 用。

對於標籤，本地化取決於上下文，因為標籤`titles`可以以頁面語言、用戶語言或任何其他語言顯示。

### 在「編輯標籤」對話框{#adding-a-new-language-to-the-edit-tag-dialog}中添加新語言

以下過程說明如何向&#x200B;**標籤編輯**&#x200B;對話框添加新語言（芬蘭文）:

1. 在&#x200B;**CRXDE**&#x200B;中，編輯節點`/content/cq:tags`的多值屬性`languages`。

1. 添加`fi_fi` — 表示芬蘭語地區設定 — 並保存更改。

現在，在&#x200B;**Tagging**&#x200B;控制台中編輯標籤時，頁面屬性的標籤對話方塊和&#x200B;**Edit Tag**&#x200B;對話方塊中都可使用新語言（芬蘭文）。

>[!NOTE]
>
>新語言必須是AEM認可的語言之一，亦即，它必須是`/libs/wcm/core/resources/languages`下方的節點。
