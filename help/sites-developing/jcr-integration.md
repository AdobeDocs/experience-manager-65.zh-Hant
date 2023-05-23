---
title: JCR整合
seo-title: JCR Integration
description: 必須在JCR級別整合的提示
seo-description: Tips for when you must integrate at the JCR level
uuid: 11518baf-521e-471d-ad4f-2baa76075cfa
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: e6647a11-a36e-4808-bb61-29b2895c6b1d
exl-id: 170474c1-c7f4-446c-bda4-84768d44a078
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# JCR整合{#jcr-integration}

## 選擇Sling資源API而不是JCR API {#prefer-the-sling-resource-api-to-jcr-api}

Sling API在比JCR API更高、更抽象的級別工作。 這樣，您的代碼就可以更加可重用，並且獨立於基礎儲存。 這樣，在需要時可以更輕鬆地通過ResourceProvider機制包括外部虛擬資料。

## 盡可能避免查詢 {#avoid-queries-wherever-possible}

與運行查詢相比，瀏覽儲存庫以檢索資料的速度總是更快。 在某些情況下，需要進行查詢，例如最終用戶查詢或需要從整個儲存庫中查找結構化內容，但是，對於所有其他情況，最好導航到必要的節點。 在呈現邏輯（如導航元件、「最近的項目清單」、項目計數等）中，應始終避免查詢。 在這些情況下，最好瀏覽層次結構或預快取結果，以便在呈現結果時直接使用結果。

## 限制JCR觀測範圍 {#restrict-the-scope-of-jcr-observation}

當偵聽儲存庫中的事件時，必須盡可能縮小範圍。 例如，最好是在 `/etc/mycompany` 比聽 `/etc`。 切勿偵聽儲存庫根目錄中的事件。 此外，確保回調方法在無法執行時盡快執行。

## 消除JCR管理員訪問的使用 {#eliminate-use-of-jcr-admin-access}

從6AEM開始，登錄管理已被棄用，從ResourceResolverFactory獲取管理會話也已棄用。 相反，應為需要此類訪問的後台辦公室操作建立服務帳戶，並且ResourceResolverFactory可用於為此帳戶獲取ResourceResolver。
