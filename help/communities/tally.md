---
title: Tally Essentials
seo-title: Tally Essentials
description: 計數分類概覽
seo-description: 計數分類概覽
uuid: c369c6a1-9ced-4b5c-af43-8c03236eaa52
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 9941ba90-3d40-4c90-bca8-5db49603cbfa
translation-type: tm+mt
source-git-commit: 01f14c203e45b85c9d7733d88437bd56e3c27c8e

---


# Tally Essentials {#tally-essentials}

Tally是抽象類別，提供一套標準方法，可收集會員對特定產品和服務的評價意見。 不支援匿名意見回應。 網站訪客必須註冊並登入才能參與並登入，以變更其意見回應。 登入的要求可避免多則貼文，以協調並提升意見回應的價值。

可通過擴展抽象計數類來建立自定義計數元件。

[贊](essentials-liking.md) (Syok)是對數字的實施，是表達正面意見的簡單形式。

[投票](essentials-voting.md) ，是一種簡單的表達正面或負面意見的表決方式。

[評分](rating-basics.md) (Rating)是指使用星型系統來表達從正面到負面的一系列意見的統計。

自AEM 6.1起，民調問答元件不再可用。

[Reviews](reviews-basics.md) 是SCF元件，是注釋和評 [分的](essentials-comments.md) 混合 [](rating-basics.md)。

## 用戶端基本功能 {#essentials-for-client-side}

* [用戶端自訂](client-customize.md)

## 伺服器端的基本功能 {#essentials-for-server-side}

* [計數API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [計數端點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [伺服器端自訂](server-customize.md)

### 存取已張貼的記錄(UGC) {#accessing-posted-tallies-ugc}

UGC應使用其中一種標準的協調方法來協調。
請參 [閱協調使用者產生的內容](moderate-ugc.md)。

自AEM 6.1 Communities起，使用UGC的 [公用商店](working-with-srp.md) ，包括程式化存取UGC，不論選擇的儲存選項（例如ASRP、MSRP或JSRP）。

**UGC在儲存庫中的位置和格式可能會變更，但不會發出警告**。

請參閱：

* [儲存資源提供方概述](srp.md) -簡介和儲存庫使用概述
* [SRP和UGC Essentials](srp-and-ugc.md) - SRP實用程式方法和示例
* [使用SRP存取UGC](accessing-ugc-with-srp.md) —— 編碼准則
* [SocialUtils重構](socialutils.md) -將不建議使用的公用程式方法對應至目前的SRP公用程式方法

