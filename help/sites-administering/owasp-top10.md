---
title: OWASP前10
seo-title: OWASP Top 10
description: 瞭解如AEM何處理前10大OWASP安全風險。
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

# OWASP前10{#owasp-top}

的 [開啟Web應用程式安全項目](https://www.owasp.org) (OWASP)保存他們認為 [前10大Web應用程式安全風險](https://www.owasp.org/index.php/OWASP_Top_Ten_Project)。

下面列出了這些資訊，並解釋了CRX如何處理這些資訊。

## 1。注射 {#injection}

* SQL — 設計阻止：預設儲存庫設定既不包括也不需要傳統資料庫，所有資料都儲存在內容儲存庫中。 所有訪問都限於經過驗證的用戶，並且只能通過JCR API執行。 僅搜索查詢(SELECT)支援SQL。 此外，SQL還提供了值綁定支援。
* LDAP - LDAP注入是不可能的，因為驗證模組會過濾輸入並使用綁定方法執行用戶導入。
* OS — 應用程式內沒有執行Shell執行。

## 2.跨站點指令碼(XSS) {#cross-site-scripting-xss}

一般的緩解做法是使用基於的伺服器端XSS保護庫對用戶生成內容的所有輸出進行編碼 [OWASP編碼器](https://www.owasp.org/index.php/OWASP_Java_Encoder_Project) 和 [安蒂薩米](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project)。

XSS在測試和開發過程中都是頭等大事，發現的任何問題（通常）都會立即解決。

## 3.中斷的身份驗證和會話管理 {#broken-authentication-and-session-management}

使AEM用聲音和經驗證的身份驗證技術， [阿帕奇·傑克拉比特](https://jackrabbit.apache.org/) 和 [阿帕奇斯林](https://sling.apache.org/)。 未在中使用瀏覽器/HTTP會AEM話。

## 4.不安全的直接對象引用 {#insecure-direct-object-references}

對資料對象的所有訪問都由儲存庫進行中介，因此受基於角色的訪問控制的限制。

## 5.跨站點請求偽造(CSRF) {#cross-site-request-forgery-csrf}

跨站點請求偽造(CSRF)通過自動將加密令牌注入所有表單和請求AJAX，並在伺服器上為每個POST驗證此令牌而得到緩解。

此外，還附AEM帶了基於參考報頭的過濾器，該過濾器可配置為 *僅* 允許來自特定主機的POST請求（在清單中定義）。

## 6。安全配置錯誤 {#security-misconfiguration}

無法保證所有軟體始終正確配置。 但是，我們努力提供盡可能多的指導，使配置盡可能簡單。 此外，AEM船隻 [整合的安全運行狀況檢查](/help/sites-administering/operations-dashboard.md) 幫助您一目瞭然地監視安全配置。

請查看 [安全核對表](/help/sites-administering/security-checklist.md) 獲取更多資訊，這些資訊為您提供逐步強化指令。

## 7。不安全的加密儲存 {#insecure-cryptographic-storage}

口令作為加密散列儲存在用戶節點中；預設情況下，此類節點僅由管理員和用戶自己讀取。

敏感資料（如第三方憑據）使用FIPS 140-2認證的加密庫以加密形式儲存。

## 8.限制URL訪問失敗 {#failure-to-restrict-url-access}

儲存庫允許 [細粒度權限（由JCR指定）](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html) 通過訪問控制項，針對任何給定路徑上的任何給定用戶或組。 儲存庫強制實施訪問限制。

## 9。傳輸層保護不足 {#insufficient-transport-layer-protection}

通過伺服器配置減輕（例如，僅使用HTTPS）。

## 10.未驗證重定向和轉發 {#unvalidated-redirects-and-forwards}

通過將所有重定向限制到用戶提供的目的地到內部位置而減輕。
