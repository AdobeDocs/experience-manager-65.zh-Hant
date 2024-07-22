---
title: CSRF保護架構
description: 此框架會使用代號來保證使用者端請求是合法的
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: e6b0f8f7-54b0-4dd6-86ad-5516954c6d90
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 8d7c5b4962ea0dbd80cf78faa31238b2252f4a5c
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 1%

---

# CSRF保護架構{#the-csrf-protection-framework}

除了Apache Sling反向連結篩選條件之外，Adobe還提供新的CSRF保護架構以抵禦此類攻擊。

此框架會使用權杖來保證使用者端請求是合法的。 代號會在表單傳送至使用者端時產生，並在表單傳回伺服器時驗證。

>[!NOTE]
>
>匿名使用者的發佈執行個體上沒有代號。

## 要求 {#requirements}

### 相依性 {#dependencies}

任何依賴`granite.jquery`相依性的元件都可以自動受益於CSRF保護架構。 如果不是，則對於任何元件，您必須先宣告相依性給`granite.csrf.standalone`，才能使用架構。

### 復寫加密金鑰 {#replicating-crypto-keys}

若要使用權杖，您需要將HMAC二進位檔復寫至部署中的所有執行個體。 如需詳細資訊，請參閱[複製HMAC金鑰](/help/sites-administering/encapsulated-token.md#replicating-the-hmac-key)。

>[!NOTE]
>
>請務必也進行必要的Dispatcher設定變更，以使用CSRF Protection Framework：
>
>* [設定Adobe Experience Manager Dispatcher以防止CSRF攻擊](https://experienceleague.adobe.com/en/docs/experience-manager-dispatcher/using/configuring/configuring-dispatcher-to-prevent-csrf)
>* [Dispatcher概觀](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-dispatcher/using/dispatcher)

>[!NOTE]
>
>如果您將資訊清單快取與Web應用程式搭配使用，請務必將&quot;**&amp;amp；ast；**&quot;新增至資訊清單，以確定權杖不會使CSRF權杖產生呼叫離線。 如需詳細資訊，請參閱此[連結](https://www.w3.org/TR/offline-webapps/)。
>
如需有關CSRF攻擊和緩解其方法的詳細資訊，請參閱[跨網站請求偽造OWASP頁面](https://owasp.org/www-community/attacks/csrf)。
