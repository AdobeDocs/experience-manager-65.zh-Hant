---
title: 計數基礎
seo-title: Tally Essentials
description: 計數類概述
seo-description: Tally class overview
uuid: c369c6a1-9ced-4b5c-af43-8c03236eaa52
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 9941ba90-3d40-4c90-bca8-5db49603cbfa
exl-id: 0b508df9-1a24-4728-a254-f913eeb9b391
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# 計數基礎 {#tally-essentials}

Tally是一個抽象類，提供一種標準方法，收整合員對特定產品和服務的價值的反饋。 不支援匿名反饋。 站點訪問者必須註冊並登錄以參與和登錄以更改其反饋。 登錄要求通過防止多個帖子來促進調節和提高反饋的價值。

通過擴展抽象計數類可以建立自定義計數元件。

[喜歡](essentials-liking.md) 是表達積極意見的簡單形式。

[投票](essentials-voting.md) 是表達正面或負面意見的簡單形式的統計。

[評級](rating-basics.md) 是用星系表達從正面到負面的各種觀點的統計。

截至AEM6.1，輪詢元件不再可用。

[評論](reviews-basics.md) 是SCF元件，它是 [評論](essentials-comments.md) 和 [評級](rating-basics.md)。

## 客戶端基本知識 {#essentials-for-client-side}

* [客戶端自定義](client-customize.md)

## 伺服器端軟體包 {#essentials-for-server-side}

* [計數API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [計數端點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [伺服器端自定義](server-customize.md)

### 訪問已發佈的記數(UGC) {#accessing-posted-tallies-ugc}

UGC應使用一種標準的審核方法來審核。
請參閱 [調節用戶生成的內容](moderate-ugc.md)。

截至AEM6.1社區，使用 [普通商店](working-with-srp.md) UGC包括對UGC的寫程式訪問，而不考慮選擇的儲存選項（如ASRP、MSRP或JSRP）。

**UGC在儲存庫中的位置和格式可能會發生更改，但不會發出警告**。

請參閱：

* [儲存資源提供程式概述](srp.md)  — 簡介和儲存庫使用概述。
* [SRP和UGC軟體包](srp-and-ugc.md) - SRP實用程式方法和示例。
* [使用SRP訪問UGC](accessing-ugc-with-srp.md)  — 編碼准則。
* [SocialUtils重構](socialutils.md)  — 將過時的實用程式方法映射到當前SRP實用程式方法。
