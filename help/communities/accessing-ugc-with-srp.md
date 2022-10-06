---
title: 使用SRP存取UGC
seo-title: Accessing UGC with SRP
description: 將網站設定為使用ASRP或MSRP時，實際UGC不會儲存在AEM節點存放區(JCR)中
seo-description: When a site is configured to use ASRP or MSRP, the actual UGC is not be stored in AEM's node store (JCR)
uuid: 30549f93-e370-4b8b-a35a-69e05884227e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 72d4022c-43ba-49e0-b94c-f2beabaef64d
docset: aem65
exl-id: 1157366f-2cc5-46e4-8ec6-e66fe5d0a0f6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# 使用SRP存取UGC {#accessing-ugc-with-srp}

## 關於SRP {#about-srp}

所有AEM Communities元件和功能都建置在 [社會構成框架](/help/communities/scf.md)，此API會呼叫SocialResourceProvider API以存取所有使用者產生的內容(UGC)。

在建立社群網站之前， [儲存資源提供程式(SRP)](/help/communities/working-with-srp.md) 必須設定為選取與基礎一致的實作 [拓撲](/help/communities/topologies.md). SRP實作以三種儲存選項為基礎：

1. [ASRP](/help/communities/asrp.md) -Adobe按需儲存
1. [MSRP](/help/communities/msrp.md) - MongoDB
1. [JSRP](/help/communities/jsrp.md) - JCR

## 關於UGC儲存 {#about-ugc-storage}

有關UGC儲存的重要資訊是，當網站設定為使用ASRP或MSRP時，實際UGC不會儲存在AEM中 [節點存放區](/help/sites-deploying/data-store-config.md) (JCR)。

雖然JCR中可能有節點陰影UGC以提供有用的中繼資料，但這些節點不會與實際UGC混淆。

請參閱 [儲存資源提供程式概述。](/help/communities/srp.md)

## 最佳實務 {#best-practice}

在開發自定義元件時，開發人員應注意獨立於當前選擇的拓撲進行編碼，從而保留將來遷移到新拓撲的靈活性。

### 假設JCR不可用 {#assume-jcr-not-available}

應避免JCR專屬方法。

使用方法：

* Sling API（Sling資源）

   * 不假定有JCR節點

* OSGi事件

   * 不假設有JCR事件

* [SocialResourceUtilities](/help/communities/socialutils.md#socialresourceutilities-package)
* [SCFUtilities](/help/communities/socialutils.md#scfutilities-package)

避免的方法：

* 節點API
* JCR事件
* 工作流程啟動器（使用JCR事件）

### 使用搜尋集合 {#use-search-collections}

不同的SRP可以有不同的原生查詢語言。 建議您使用 [com.adobe.cq.social.ugc.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) 套件來執行適當的查詢語言。

如需詳細資訊，請參閱 [搜尋要點](/help/communities/search-implementation.md).

## 資源 {#resources}

* [社群內容儲存](/help/communities/working-with-srp.md)  — 討論UGC通用商店的可用SRP選擇
* [儲存資源提供程式概述](/help/communities/srp.md)  — 簡介和存放庫使用概觀
* [SRP和UGC要點](/help/communities/srp-and-ugc.md) - SRP實用程式方法和示例
* [搜尋要點](/help/communities/search-implementation.md)  — 搜索UGC的基本資訊
* [SocialUtils重構](/help/communities/socialutils.md)  — 將已棄用的實用程式方法映射到當前SRP實用程式方法
