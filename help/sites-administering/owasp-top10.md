---
title: OWASP前10名
description: 瞭解AEM如何處理前10大OWASP安全性風險。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: 8b2a2f1d-8286-4ba5-8fe2-627509c72a45
feature: Security
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 0%

---

# OWASP前10名{#owasp-top}

此 [開啟Web應用程式安全性專案](https://owasp.org/) (OWASP)會維護一份清單，列出他們認為的 [前10大Web應用程式安全性風險](https://owasp.org/www-project-top-ten/).

以下列出，並說明CRX如何處理這些請求。

## 1.注入 {#injection}

* SQL — 設計防止：預設的存放庫設定既不包含也不需要傳統資料庫，所有資料都儲存在內容存放庫中。 所有存取權僅限已驗證身分的使用者使用，且只能透過JCR API執行。 僅搜尋查詢支援SQL (SELECT)。 此外，SQL還提供值繫結支援。
* LDAP — 無法插入LDAP，因為驗證模組會篩選輸入並使用繫結方法執行使用者匯入。
* OS — 應用程式內沒有執行殼層。

## 2.跨網站指令碼(XSS) {#cross-site-scripting-xss}

一般緩解作法是使用伺服器端XSS保護程式庫，根據以下基準編碼使用者產生內容的所有輸出： [OWASP編碼器](https://owasp.org/www-project-java-encoder/) 和 [AntiSamy](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project).

XSS在測試和開發期間是首要任務，發現的任何問題通常都會立即解決。

## 3.中斷的驗證和工作階段管理 {#broken-authentication-and-session-management}

AEM使用健全且經過驗證的驗證技術，依賴於 [Apache Jackrabbit](https://jackrabbit.apache.org/jcr/index.html) 和 [Apache Sling](https://sling.apache.org/). AEM中未使用瀏覽器/HTTP工作階段。

## 4.不安全的直接物件參考 {#insecure-direct-object-references}

對資料物件的所有存取都是由存放庫所介入，因此受到角色型存取控制的限制。

## 5.跨網站請求偽造(CSRF) {#cross-site-request-forgery-csrf}

跨網站請求偽造(CSRF)可藉由自動將密碼編譯權杖插入所有表單和AJAX請求，並在伺服器上驗證每個POST的此權杖來緩解。

此外，AEM隨附以反向連結標題為基礎的篩選器，可將其設定為 *僅限* 允許來自特定主機的POST請求（在清單中定義）。

## 6.安全性設定錯誤 {#security-misconfiguration}

無法保證所有軟體皆已正確設定。 不過，Adobe會努力提供儘可能多的指引，並儘可能簡化設定。 此外，AEM也隨附於 [整合式安全性健康情況檢查](/help/sites-administering/operations-dashboard.md) 協助您一眼監控安全性組態。

檢閱 [安全性檢查清單](/help/sites-administering/security-checklist.md) 以取得提供逐步強化指示的詳細資訊。

## 7.不安全的密碼編譯儲存 {#insecure-cryptographic-storage}

密碼會以密碼編譯雜湊的形式儲存在使用者節點中。 依預設，此類節點僅供管理員和使用者自己讀取。

機密資料（例如協力廠商憑證）會使用FIPS 140-2認證的密碼編譯程式庫，以加密形式儲存。

## 8.無法限制URL存取 {#failure-to-restrict-url-access}

存放庫允許設定 [微調許可權（由JCR指定）](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html) 對於任何指定路徑的任何指定使用者或群組，透過存取控制專案。 存取限制由存放庫強制執行。

## 9.傳輸層保護不足 {#insufficient-transport-layer-protection}

透過伺服器設定減輕（例如，僅使用HTTPS）。

## 10.未驗證的重新導向與轉送 {#unvalidated-redirects-and-forwards}

限制所有重新導向至使用者提供的內部位置目的地，即可緩解此問題。
