---
title: Tally Essentials
description: 瞭解Tally如何是一個抽象類別，提供收整合員意見的標準方法，讓他們瞭解如何評估特定產品和服務。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 0b508df9-1a24-4728-a254-f913eeb9b391
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---

# Tally Essentials {#tally-essentials}

Tally是抽象類別，提供收整合員意見的標準方法，說明他們如何評估特定產品和服務。 不支援匿名意見反應。 網站訪客必須註冊並登入才能參與並登入以變更其意見反應。 登入要求有助於稽核，並藉由防止多個貼文而提升意見回饋的價值。

可藉由擴充抽象tally類別來建立自訂標籤元件。

[點讚](essentials-liking.md)是簡單的計數的實作，表示正面意見。

[投票](essentials-voting.md)是簡單形式的計數的實作，可表達正面或負面意見。

[評等](rating-basics.md)是計數的實作，它使用星型系統來表示從正面到負面的一系列意見。

自AEM 6.1起，不再提供輪詢元件。

[評論](reviews-basics.md)是[評論](essentials-comments.md)和[評等](rating-basics.md)的混合式SCF元件。

## 使用者端的Essentials {#essentials-for-client-side}

* [使用者端自訂](client-customize.md)

## 伺服器端的Essentials {#essentials-for-server-side}

* [總計API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [計數的端點](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [伺服器端自訂](server-customize.md)

### 存取已張貼的表格(UGC) {#accessing-posted-tallies-ugc}

UGC應使用其中一種標準仲裁方法進行仲裁。
請參閱[仲裁使用者產生的內容](moderate-ugc.md)。

截至AEM 6.1 Communities，使用UGC的[公用存放區](working-with-srp.md)時，無論選擇的存放區選項（例如ASRP、MSRP或JSRP）為何，都可程式化存取UGC。

**存放庫中UGC的位置和格式可能會變更，而不會出現警告**。

請參閱：

* [儲存資源提供者概觀](srp.md) — 簡介和存放庫使用概觀。
* [SRP與UGC Essentials](srp-and-ugc.md) - SRP公用程式方法與範例。
* [使用SRP存取UGC](accessing-ugc-with-srp.md) — 編碼准則。
* [SocialUtils重構](socialutils.md) — 將已棄用的公用程式方法對應到目前的SRP公用程式方法。
