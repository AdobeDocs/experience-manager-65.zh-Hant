---
title: OWASP Top 10
seo-title: OWASP Top 10
description: 瞭解AEM如何應對前10大OWASP安全性風險。
seo-description: 瞭解AEM如何應對前10大OWASP安全性風險。
uuid: a5a7e130-e15b-47ae-ba21-448f9ac76074
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: e5323ae8-bc37-4bc6-bca6-9763e18c8e76
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# OWASP Top 10{#owasp-top}

Open [Web Application Security Project](https://www.owasp.org) (OWASP)會維護他們認為十大Web應用程式安全 [性風險的清單](https://www.owasp.org/index.php/OWASP_Top_Ten_Project)。

下面列出了這些內容，以及CRX如何處理這些內容的說明。

## 1.注射 {#injection}

* SQL —— 由設計防止：預設儲存庫設定既不包括也不需要傳統資料庫，所有資料都儲存在內容儲存庫中。 所有存取權限僅限已驗證的使用者，且只能透過JCR API執行。 僅搜索查詢(SELECT)支援SQL。 此外，SQL還提供值綁定支援。
* LDAP —— 無法插入LDAP，因為驗證模組會過濾輸入，並使用綁定方法執行用戶導入。
* OS —— 應用程式內不執行shell。

## 2.跨網站指令碼(XSS) {#cross-site-scripting-xss}

一般的緩解措施是使用以 [OWASP Encoder和](https://www.owasp.org/index.php/OWASP_Java_Encoder_Project) AntiSamy為基礎的伺服器端XSS保護程式庫，來編碼使用者產生的內容的所有輸出 [](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project)。

XSS是測試和開發期間的最優先順序，而發現的任何問題（通常）都會立即解決。

## 3.中斷驗證和會話管理 {#broken-authentication-and-session-management}

AEM採用音效和證實可行的驗證技術， [仰賴Apache Jackrabbit](https://jackrabbit.apache.org/)[和Apache Sling](https://sling.apache.org/)。 AEM不會使用瀏覽器/HTTP工作階段。

## 4.不安全的直接物件參考 {#insecure-direct-object-references}

所有對資料對象的訪問都由儲存庫介導，因此受基於角色的訪問控制的限制。

## 5.跨網站偽造要求(CSRF) {#cross-site-request-forgery-csrf}

跨網站偽造要求(CSRF)可借由自動將加密Token注入所有表單和AJAX要求，並在每個POST的伺服器上驗證此Token，來減輕。

此外，AEM會隨附反向連結標題型篩選器，此篩選器可設定為僅允許來自明確白名單主機的POST請求。

## 6.安全性配置錯誤 {#security-misconfiguration}

無法保證所有軟體都正確設定。 但是，我們努力提供盡可能多的指導，使配置盡可能簡單。 此外，AEM隨附整合 [的Security Healthchecks](/help/sites-administering/operations-dashboard.md) ，可協助您一目瞭然地監控安全性設定。

請參閱安 [全檢查清單](/help/sites-administering/security-checklist.md) ，以取得詳細資訊，提供逐步強化指示。

## 7.不安全的加密儲存 {#insecure-cryptographic-storage}

口令作為加密散列儲存在用戶節點中；預設情況下，這些節點僅由管理員和用戶自己讀取。

敏感資料（如第三方憑據）使用FIPS 140-2認證的加密庫以加密形式儲存。

## 8.無法限制URL存取 {#failure-to-restrict-url-access}

儲存庫允許通過訪問控 [制項為任何給定路徑上的任何給定用戶或組設定細粒度的權限（由JCR指定）](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html) 。 存取限制由儲存庫強制執行。

## 9.傳輸層保護不足 {#insufficient-transport-layer-protection}

由伺服器設定減輕（例如僅使用HTTPS）。

## 10.未驗證的重新導向和轉送 {#unvalidated-redirects-and-forwards}

借由將使用者提供目的地的所有重新導向限制在內部位置，減輕重新導向的影響。

