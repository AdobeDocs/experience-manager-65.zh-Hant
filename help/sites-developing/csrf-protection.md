---
title: CSRF保護框架
seo-title: CSRF保護框架
description: 該框架利用令牌來保證客戶端請求的合法性
seo-description: 該框架利用令牌來保證客戶端請求的合法性
uuid: 7cb222ba-fc7a-46ee-8b49-a5f39a53580b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f453427d-c813-48b7-b2f9-adadea39c67d
exl-id: e6b0f8f7-54b0-4dd6-86ad-5516954c6d90
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 0%

---

# CSRF保護框架{#the-csrf-protection-framework}

除了Apache Sling Referrer Filter外，Ache還提供新的CSRF保護架構，以防止這類攻擊。

該框架利用令牌來保證客戶端請求的合法性。 當表單傳送至用戶端時產生代號，並在表單傳回至伺服器時驗證。

>[!NOTE]
>
>匿名使用者的發佈例項上沒有代號。

## 需求 {#requirements}

### 相依關係 {#dependencies}

任何依賴`granite.jquery`相關性的元件都將自動受益於CSRF保護框架。 如果任何元件的情況不是這樣，則必須先將相依性聲明為`granite.csrf.standalone`，然後才能使用框架。

### 複製加密密鑰{#replicating-crypto-keys}

若要使用代號，您必須將`/etc/keys/hmac`二進位檔複製到部署中的所有例項。 將HMAC密鑰複製到所有實例的一個方便方法是建立包含密鑰的包，並通過包管理器在所有實例上安裝它。

>[!NOTE]
>
>也請務必進行必要的[Dispatcher設定變更](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html)，以便使用CSRF保護架構。

>[!NOTE]
>
>如果您將資訊清單快取與網頁應用程式搭配使用，請務必將「**&amp;ast;**」新增至資訊清單，以確保Token不會讓CSRF代號產生呼叫離線。 如需詳細資訊，請參閱此[link](https://www.w3.org/TR/offline-webapps/)。
>
>如需CSRF攻擊的詳細資訊及緩解方法，請參閱[跨網站請求偽造OWASP頁面](https://owasp.org/www-community/attacks/csrf)。
