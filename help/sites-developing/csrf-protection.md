---
title: CSRF保護框架
seo-title: CSRF保護框架
description: 該框架利用令牌來保證客戶端請求是合法的
seo-description: 該框架利用令牌來保證客戶端請求是合法的
uuid: 7cb222ba-fc7a-46ee-8b49-a5f39a53580b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f453427d-c813-48b7-b2f9-adadea39c67d
translation-type: tm+mt
source-git-commit: c83c77c5c313099944dd73c8cbe63d429d84a518
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 0%

---


# CSRF保護框架{#the-csrf-protection-framework}

除了Apache Sling Referrer Filter外，Adobe也提供新的CSRF Protection Framework以防範此類攻擊。

該框架利用Token來保證客戶端請求的合法性。 當表單傳送至用戶端時產生代號，當表單傳回至伺服器時驗證。

>[!NOTE]
>
>匿名使用者的發佈例項上沒有Token。

## 要求{#requirements}

### 相依關係 {#dependencies}

任何依賴於`granite.jquery`相關性的元件都將自動受益於CSRF保護框架。 如果您的任何元件不是這樣，則必須聲明從屬關係至`granite.csrf.standalone`，才能使用框架。

### 複製加密密鑰{#replicating-crypto-keys}

為了使用Token，您需要將`/etc/keys/hmac`二進位檔複製到部署中的所有例項。 將HMAC密鑰複製到所有實例的一個便利方法是建立包含密鑰的軟體包，並通過包管理器在所有實例上安裝該軟體包。

>[!NOTE]
>
>請確定您還必須對[Dispatcher配置進行](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html)更改，以便使用CSRF保護框架。

>[!NOTE]
>
>如果您將資訊清單快取與您的網頁應用程式搭配使用，請務必將&quot;**&amp;ast;**&quot;新增至資訊清單，以確保Token不會使CSRF代號產生呼叫離線。 如需詳細資訊，請參閱此[link](https://www.w3.org/TR/offline-webapps/)。
>
>如需CSRF攻擊的詳細資訊以及減少攻擊的方法，請參閱[跨網站偽造要求OWASP頁面](https://owasp.org/www-community/attacks/csrf)。
