---
title: CSRF保護框架
seo-title: The CSRF Protection Framework
description: 該框架利用令牌來保證客戶端請求的合法性
seo-description: The framework makes use of tokens to guarantee that the client request is legitimate
uuid: 7cb222ba-fc7a-46ee-8b49-a5f39a53580b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f453427d-c813-48b7-b2f9-adadea39c67d
exl-id: e6b0f8f7-54b0-4dd6-86ad-5516954c6d90
source-git-commit: f841e3886771fb00eee6e476d7111d4a335a9d51
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# CSRF保護框架{#the-csrf-protection-framework}

除了Apache Sling Referrer Filter外，Ache還提供新的CSRF保護架構，以防止這類攻擊。

該框架利用令牌來保證客戶端請求的合法性。 當表單傳送至用戶端時產生代號，並在表單傳回至伺服器時驗證。

>[!NOTE]
>
>匿名使用者的發佈例項上沒有代號。

## 要求 {#requirements}

### 相依性 {#dependencies}

仰賴 `granite.jquery` 依賴性將自動受益於CSRF保護框架。 如果任何元件的情況不是這樣，則必須聲明相依性 `granite.csrf.standalone` 之後才能使用框架。

### 複製加密密鑰 {#replicating-crypto-keys}

若要使用代號，您需要將HMAC二進位檔復寫至部署中的所有執行個體。 請參閱 [複製HMAC密鑰](/help/sites-administering/encapsulated-token.md#replicating-the-hmac-key) 以取得更多詳細資訊。

>[!NOTE]
>
>請確定您也必須 [Dispatcher設定變更](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) 以便使用CSRF保護框架。

>[!NOTE]
>
>如果您將資訊清單快取與Web應用程式搭配使用，請務必新增「**&amp;ast;**」，以確定代號不會使CSRF代號產生呼叫離線。 如需詳細資訊，請參閱 [連結](https://www.w3.org/TR/offline-webapps/).
>
>如需CSRF攻擊的詳細資訊以及緩解這些攻擊的方法，請參閱 [「跨網站請求偽造OWASP」頁](https://owasp.org/www-community/attacks/csrf).
