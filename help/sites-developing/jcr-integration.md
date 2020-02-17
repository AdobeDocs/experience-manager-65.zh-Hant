---
title: JCR整合
seo-title: JCR整合
description: 必須在JCR層級整合的秘訣
seo-description: 必須在JCR層級整合的秘訣
uuid: 11518baf-521e-471d-ad4f-2baa76075cfa
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: e6647a11-a36e-4808-bb61-29b2895c6b1d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# JCR整合{#jcr-integration}

## 偏好Sling Resource API而非JCR API {#prefer-the-sling-resource-api-to-jcr-api}

Sling API的運作層級比JCR API更高、更抽象。 這可讓您的程式碼更可重複使用，而且獨立於基礎儲存空間。 這樣，如果需要，可以更輕鬆地通過ResourceProvider機制包括外部虛擬資料。

## 盡可能避免查詢 {#avoid-queries-wherever-possible}

與運行查詢相比，瀏覽儲存庫以檢索資料總是更快。 有時需要查詢，例如最終用戶查詢或需要從整個儲存庫中查找結構化內容，但是對於所有其他情況，則最好導航到所需節點。 在演算邏輯中，例如導覽元件、「最近的項目清單」、項目計數等，一律應避免查詢。 在這些情況下，最好逐一瀏覽階層或預先快取結果，以便在轉譯時直接使用。

## 限制JCR觀測範圍 {#restrict-the-scope-of-jcr-observation}

在監聽儲存庫中的事件時，請務必盡可能縮小範圍。 例如，在網站上監聽活動比在網站 `/etc/mycompany` 上監聽要好 `/etc`。 切勿在儲存庫根目錄中監聽事件。 此外，請確定回呼方法在沒有可執行的項目時，能盡快執行。

## 免除使用JCR管理員存取權 {#eliminate-use-of-jcr-admin-access}

自AEM 6起，登入管理已過時，從ResourceResolverFactory取得管理工作階段亦已過時。 相反，應為需要此類訪問的後端辦公室操作建立服務帳戶，並可使用ResourceResolverFactory獲取此帳戶的ResourceResolver。
