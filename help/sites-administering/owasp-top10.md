---
title: OWASP Top 10
seo-title: OWASP Top 10
description: 瞭解如AEM何應對前10大OWASP安全風險。
seo-description: 瞭解如AEM何應對前10大OWASP安全風險。
uuid: a5a7e130-e15b-47ae-ba21-448f9ac76074
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: e5323ae8-bc37-4bc6-bca6-9763e18c8e76
exl-id: 8b2a2f1d-8286-4ba5-8fe2-627509c72a45
feature: Security
translation-type: tm+mt
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 0%

---

# OWASP Top 10{#owasp-top}

[Open Web應用程式安全性項目](https://www.owasp.org)(OWASP)維護了[前10大Web應用程式安全性風險](https://www.owasp.org/index.php/OWASP_Top_Ten_Project)的清單。

下面列出了這些內容，以及CRX如何處理這些內容的說明。

## 1.注射{#injection}

* SQL —— 由設計防止：預設儲存庫設定既不包括也不需要傳統資料庫，所有資料都儲存在內容儲存庫中。 所有存取權限僅限已驗證的使用者，且只能透過JCR API執行。 僅搜索查詢(SELECT)支援SQL。 此外，SQL還提供值綁定支援。
* LDAP —— 無法插入LDAP，因為驗證模組會過濾輸入，並使用綁定方法執行用戶導入。
* OS —— 應用程式內不執行shell。

## 2.跨網站指令碼(XSS){#cross-site-scripting-xss}

一般的緩解做法是使用基於[OWASP Encoder](https://www.owasp.org/index.php/OWASP_Java_Encoder_Project)和[AntiSamy](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project)的伺服器端XSS保護庫，對用戶產生的內容的所有輸出進行編碼。

XSS是測試和開發期間的最優先順序，而發現的任何問題（通常）都會立即解決。

## 3.中斷的驗證和會話管理{#broken-authentication-and-session-management}

使AEM用音效和證實可行的驗證技術，依賴[Apache Jackrabbit](https://jackrabbit.apache.org/)和[Apache Sling](https://sling.apache.org/)。 瀏覽器/HTTP會話不用於AEM。

## 4.不安全的直接對象引用{#insecure-direct-object-references}

所有對資料對象的訪問都由儲存庫介導，因此受基於角色的訪問控制的限制。

## 5.跨網站偽造要求(CSRF){#cross-site-request-forgery-csrf}

跨網站偽造要求(CSRF)可借由自動將加密Token注入所有表單和要求，並在伺服器上針對每個POSTAJAX驗證此Token，來減輕。

此外，AEM附帶反向連結標題篩選器，可設定為&#x200B;*only*，允許特定主機（定義於清單中）的POST要求。

## 6.安全性配置錯誤{#security-misconfiguration}

無法保證所有軟體都正確設定。 但是，我們努力提供盡可能多的指導，使配置盡可能簡單。 此外，AEM隨附[整合式Security Healthchecks](/help/sites-administering/operations-dashboard.md)，可協助您一目瞭然地監控安全性設定。

請參閱[安全檢查清單](/help/sites-administering/security-checklist.md)以取得詳細資訊，其中提供逐步強化指示。

## 7.不安全的加密儲存{#insecure-cryptographic-storage}

口令作為加密散列儲存在用戶節點中；預設情況下，這些節點僅由管理員和用戶自己讀取。

敏感資料（如第三方憑據）使用FIPS 140-2認證的加密庫以加密形式儲存。

## 8.無法限制URL存取{#failure-to-restrict-url-access}

儲存庫允許通過訪問控制條目對任何給定路徑上的任何給定用戶或組設定[細粒度權限（由JCR指定）](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html)。 存取限制由儲存庫強制執行。

## 9.傳輸層保護不足{#insufficient-transport-layer-protection}

由伺服器設定減輕（例如僅使用HTTPS）。

## 10.未驗證的重定向和轉發{#unvalidated-redirects-and-forwards}

借由將使用者提供目的地的所有重新導向限制在內部位置，減輕重新導向的影響。
