---
title: Jave內容儲存庫中節點的命名約定
description: 儲存庫中的節點受Java內容儲存庫的命名約定的約束
uuid: 0515c5c5-3e93-4710-983f-c08c146467fc
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 198098c0-432b-4a93-a94e-2552337435dd
exl-id: 01c6bb29-1d2d-4a45-b291-0e8d97c01a08
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 7%

---

# 命名慣例{#naming-conventions}

儲存庫中的節點受 [Java內容儲存庫](/help/sites-developing/the-basics.md#java-content-repository)。 但AEM是會對頁節點名稱作進一步約定。

## 頁面命名約定 {#naming-conventions-for-pages}

這些命名約定在不同級別實施：

* JcrUtil:執AEM行 [JCR實用程式](#jcr-utilities)。
* PageManager:這樣 [頁面管理器](#page-manager) 提供了頁級操作的方法。
* 根據所使用的UI:

   * [標準、支援觸摸的UI](#standard-ui)
   * [傳統 UI](#classic-ui)

### JCR實用程式 {#jcr-utilities}

[JcrUtil](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/commons/jcr/JcrUtil.html) 是JCR實AEM用程式的實現。 對驗證名稱特別感興趣的是它控制的字元映射和以下驗證：

* `isValidName`

   * 檢查名稱是否不為空且僅包含有效字元。
   * 可用於檢查建議的名稱是否有效。

* `createValidName`

   * 這將從任意字串中建立有效標籤。
   * 它可用於從標題建立名稱。

### 頁面管理器 {#page-manager}

[頁面管理器](https://helpx.adobe.com/tw/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) 提供基於的頁級操作方法 [JCRUtil](#jcr-utilities)。

### 標準 UI {#standard-ui}

標準的觸控式UI:

* 根據PageManager施加的限制驗證名稱，當以下任一時間：

   * 提供頁標題以轉換為節點名稱
   * 提供了顯式節點名稱

### 傳統 UI {#classic-ui}

經典UI施加了更嚴格的限制：

* 在以下任一情況下驗證顯式節點名稱時的名稱：

   * 提供頁標題以轉換為節點名稱
   * 提供了顯式節點名稱

* 有效字元(即使從經典UI中建立頁面時，也只有這些字元實際有效 `PageManagerImpl` 將允許額外字元):

   * 「a」到「z」
   * 「A」到「Z」
   * 「0」到「9」
   * _（下划線）
   * `-` （破折號/減號）
