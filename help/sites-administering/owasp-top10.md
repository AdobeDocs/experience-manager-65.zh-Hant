---
title: OWASP前10名
seo-title: OWASP Top 10
description: 了解AEM如何應對前10大OWASP安全風險。
seo-description: Learn how AEM deals with the top 10 OWASP security risks.
uuid: a5a7e130-e15b-47ae-ba21-448f9ac76074
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: e5323ae8-bc37-4bc6-bca6-9763e18c8e76
exl-id: 8b2a2f1d-8286-4ba5-8fe2-627509c72a45
feature: Security
source-git-commit: 2bae11eafb875f01602c39c0dba00a888e11391a
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---

# OWASP前10名{#owasp-top}

[開放Web應用程式安全項目](https://www.owasp.org)(OWASP)維護一個清單，列出它們認為的[前10個Web應用程式安全風險](https://www.owasp.org/index.php/OWASP_Top_Ten_Project)。

下面列出了這些檔案，以及CRX如何處理這些檔案的說明。

## 1.注射 {#injection}

* SQL — 設計阻止：預設儲存庫設定既不包括也不要求傳統資料庫，所有資料都儲存在內容儲存庫中。 所有存取權限僅限已驗證的使用者，且只能透過JCR API執行。 僅搜索查詢(SELECT)支援SQL。 此外，SQL還提供值綁定支援。
* LDAP — 無法插入LDAP，因為驗證模組會篩選輸入，並使用捆綁方法執行用戶導入。
* OS — 應用程式內未執行任何殼層執行。

## 2.跨網站指令碼(XSS) {#cross-site-scripting-xss}

一般的緩解做法是使用基於[OWASP Encoder](https://www.owasp.org/index.php/OWASP_Java_Encoder_Project)和[AntiSamy](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project)的伺服器端XSS保護庫對用戶生成的內容的所有輸出進行編碼。

在測試和開發期間，XSS都是最優先順序，而發現的任何問題（通常）都可立即解決。

## 3.失效驗證和會話管理 {#broken-authentication-and-session-management}

AEM使用聲音和經驗證的驗證技術，依賴[Apache Jackrabbit](https://jackrabbit.apache.org/)和[Apache Sling](https://sling.apache.org/)。 AEM中未使用瀏覽器/HTTP工作階段。

## 4.不安全的直接對象引用 {#insecure-direct-object-references}

對資料對象的所有訪問都由儲存庫介導，因此受基於角色的訪問控制的限制。

## 5.跨網站請求偽造(CSRF) {#cross-site-request-forgery-csrf}

自動將密碼編譯Token插入所有表單和AJAX請求，並針對每個POST在伺服器上驗證此Token，借此緩解跨網站請求偽造(CSRF)。

此外，AEM隨附反向連結標題型篩選器，此篩選器可設定為&#x200B;*only*&#x200B;允許來自特定主機的POST請求（在清單中定義）。

## 6.安全配置錯誤 {#security-misconfiguration}

無法保證所有軟體都始終正確配置。 然而，我們努力提供盡可能多的指導，並盡可能簡化配置。 此外，AEM隨[整合的Security Healthchecks](/help/sites-administering/operations-dashboard.md)一起提供，可幫助您一目瞭然地監控安全配置。

請查看[安全檢查清單](/help/sites-administering/security-checklist.md)以了解為您提供逐步強化說明的詳細資訊。

## 7.不安全的加密儲存 {#insecure-cryptographic-storage}

密碼儲存為用戶節點中的加密哈希；預設情況下，這些節點僅由管理員和用戶自己讀取。

敏感資料（如第三方憑證）使用經FIPS 140-2認證的加密庫以加密形式儲存。

## 8.未能限制URL存取 {#failure-to-restrict-url-access}

儲存庫允許通過訪問控制項為任何給定用戶或組設定[微調權限（如JCR所指定）](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html)，以在任何給定路徑上。 存取限制由存放庫強制執行。

## 9.傳輸層保護不足 {#insufficient-transport-layer-protection}

由伺服器配置緩解（例如僅使用HTTPS）。

## 10.未驗證的重定向和轉發 {#unvalidated-redirects-and-forwards}

限制使用者提供目的地的所有重新導向至內部位置，借此緩解。
