---
title: CSRF保護架構
seo-title: The CSRF Protection Framework
description: 此框架會使用代號來保證使用者端請求是合法的
seo-description: The framework makes use of tokens to guarantee that the client request is legitimate
uuid: 7cb222ba-fc7a-46ee-8b49-a5f39a53580b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f453427d-c813-48b7-b2f9-adadea39c67d
exl-id: e6b0f8f7-54b0-4dd6-86ad-5516954c6d90
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# CSRF保護架構{#the-csrf-protection-framework}

除了Apache Sling反向連結篩選條件之外，Adobe還提供新的CSRF保護架構以抵禦此類攻擊。

此框架會使用權杖來保證使用者端請求是合法的。 代號會在表單傳送至使用者端時產生，並在表單傳回伺服器時驗證。

>[!NOTE]
>
>匿名使用者的發佈執行個體上沒有代號。

## 要求 {#requirements}

### 相依性 {#dependencies}

任何依賴 `granite.jquery` 相依性會自動受益於CSRF Protection Framework。 若您的任何元件不是這種情況，您必須將相依性宣告至 `granite.csrf.standalone` 之後才能使用架構。

### 復寫加密金鑰 {#replicating-crypto-keys}

若要使用權杖，您需要將HMAC二進位檔復寫至部署中的所有執行個體。 另請參閱 [復寫HMAC金鑰](/help/sites-administering/encapsulated-token.md#replicating-the-hmac-key) 以取得更多詳細資料。

>[!NOTE]
>
>請務必也採取必要 [Dispatcher設定變更](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) 以使用CSRF保護架構。

>[!NOTE]
>
>如果您將資訊清單快取搭配網頁應用程式使用，請務必新增&quot;**&amp;ast；**」至資訊清單，以確定權杖不會使CSRF權杖產生呼叫離線。 如需詳細資訊，請參閱此 [連結](https://www.w3.org/TR/offline-webapps/).
>
>如需有關CSRF攻擊和緩解其方法的詳細資訊，請參閱 [跨網站請求偽造OWASP頁面](https://owasp.org/www-community/attacks/csrf).
