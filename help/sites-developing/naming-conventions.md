---
title: 命名慣例
seo-title: 命名慣例
description: 儲存庫中的節點受Java內容儲存庫的命名約定的約束
seo-description: 儲存庫中的節點受Java內容儲存庫的命名約定的約束
uuid: 0515c5c5-3e93-4710-983f-c08c146467fc
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 198098c0-432b-4a93-a94e-2552337435dd
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# 命名慣例{#naming-conventions}

儲存庫中的節點受 [Java內容儲存庫的命名約定所約束](/help/sites-developing/the-basics.md#java-content-repository)。 不過，AEM會針對頁面節點的名稱，加入更多約定。

## 頁面的命名慣例 {#naming-conventions-for-pages}

這些命名慣例會在不同層級實作：

* JcrUtil:JCR公用程式的AEM [實作](#jcr-utilities)。
* PageManager:「頁 [面管理器](#page-manager) 」提供頁面層級操作的方法。
* 根據使用的UI:

   * [標準、可觸控的UI](#standard-ui)
   * [傳統 UI](#classic-ui)

### JCR實用程式 {#jcr-utilities}

[JcrUtil](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/commons/jcr/JcrUtil.html) 是JCR實用程式的AEM實現。 驗證名稱的特別感興趣的是它控制的字元映射和以下驗證：

* `isValidName`

   * 檢查名稱是否不為空，且僅包含有效字元。
   * 可用來檢查建議的名稱是否有效。

* `createValidName`

   * 這會從任意字串中建立有效的標籤。
   * 它可用來從標題建立名稱。

### 頁面管理員 {#page-manager}

[PageManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) 根據 [JCRUtil](#jcr-utilities)，提供頁面層級操作的方法。

### 標準UI {#standard-ui}

標準、可觸控的UI:

* 驗證名稱時，請根據PageManager所施加的限制：

   * 提供頁面標題以轉換為節點名稱
   * 提供了顯式節點名稱

### 傳統 UI {#classic-ui}

傳統的UI會施加更嚴格的限制：

* 在以下任一情況下驗證顯式節點名稱時的名稱：

   * 提供頁面標題以轉換為節點名稱
   * 提供了顯式節點名稱

* 有效字元(只有這些字元在從傳統UI中建立頁面時，即使允許其他字元， `PageManagerImpl` 實際上也有效):

   * &#39;a&#39;到&#39;z&#39;
   * A到Z
   * &#39;0&#39;到&#39;9&#39;
   * _（下划線）
   * `-` （破折號／減號）

