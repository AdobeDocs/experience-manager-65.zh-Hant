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

除了Apache Sling引用過濾器之外，Adobe還提供了新的CSRF保護框架來防止此類攻擊。

該框架利用令牌來保證客戶端請求的合法性。 當表單被發送到客戶端時生成令牌，當表單被發回到伺服器時驗證令牌。

>[!NOTE]
>
>匿名用戶的發佈實例上沒有令牌。

## 要求 {#requirements}

### 相依性 {#dependencies}

依賴於 `granite.jquery` 依賴項將自動從CSRF保護框架中受益。 如果任何元件的情況不是這樣，則必須聲明依賴關係 `granite.csrf.standalone` 才能使用框架。

### 複製加密密鑰 {#replicating-crypto-keys}

為了利用令牌，您需要將HMAC二進位檔案複製到部署中的所有實例。 請參閱 [複製HMAC密鑰](/help/sites-administering/encapsulated-token.md#replicating-the-hmac-key) 的子菜單。

>[!NOTE]
>
>確保您也 [調度程式配置更改](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) 以便使用CSRF保護框架。

>[!NOTE]
>
>如果將清單快取用於Web應用程式，請確保添加「」**&amp;ast;**&quot;到清單，以確保令牌不使CSRF令牌生成調用離線。 有關詳細資訊，請參閱 [連結](https://www.w3.org/TR/offline-webapps/)。
>
>有關CSRF攻擊及其緩解方法的詳細資訊，請參見 [跨站點請求偽造OWASP頁](https://owasp.org/www-community/attacks/csrf)。
