---
title: JCR整合
seo-title: JCR Integration
description: 您必須在JCR層級整合的秘訣
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

## 偏好使用Sling資源API而非JCR API {#prefer-the-sling-resource-api-to-jcr-api}

Sling API的運作層級比JCR API高、更抽象。 這可讓您的程式碼更可重複使用，且獨立於基礎儲存。 這樣，在需要時可更輕鬆地通過ResourceProvider機制包含外部虛擬資料。

## 盡可能避免查詢 {#avoid-queries-wherever-possible}

導覽存放庫以擷取資料的速度，一律快於執行查詢。 在某些情況下，需要進行查詢，例如最終用戶查詢或需要從整個儲存庫中查找結構化內容，但在所有其他情況下，最好導航到必要的節點。 呈現邏輯中應一律避免查詢，例如導覽元件、「最近的項目清單」、項目計數等。 在這些情況下，最好逐步了解階層或預先快取結果，以便在轉譯時直接使用。

## 限制JCR觀測範圍 {#restrict-the-scope-of-jcr-observation}

監聽存放庫中的事件時，請務必盡量縮小範圍。 例如，最好在 `/etc/mycompany` 而不是在 `/etc`. 切勿監聽存放庫根目錄中的事件。 此外，請確定回呼方法在無法執行時，能盡快執行。

## 避免使用JCR管理員存取權 {#eliminate-use-of-jcr-admin-access}

自AEM 6起，登入管理已遭取代，因為已從ResourceResolverFactory取得管理工作階段。 相反地，應為需要此類型的訪問的後台操作建立服務帳戶，並且可以使用ResourceResolverFactory為此帳戶獲取ResourceResolver。
