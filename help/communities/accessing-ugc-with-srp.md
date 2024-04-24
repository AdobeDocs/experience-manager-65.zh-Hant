---
title: 使用SRP存取UGC
description: 當網站設定為使用ASRP或MSRP時，實際的UGC不會儲存在AEM節點存放區(JCR)中
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 1157366f-2cc5-46e4-8ec6-e66fe5d0a0f6
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# 使用SRP存取UGC {#accessing-ugc-with-srp}

## 關於SRP {#about-srp}

所有AEM Communities元件和功能都建立在 [社交元件架構(SCF)](/help/communities/scf.md)，會呼叫SocialResourceProvider API來存取所有使用者產生的內容(UGC)。

在建立社群網站之前， [儲存資源提供者(SRP)](/help/communities/working-with-srp.md) 必須設定為選取與基礎一致的實作 [拓撲](/help/communities/topologies.md). SRP實施會根據三個儲存選項：

1. [ASRP](/help/communities/asrp.md)  — 隨選Adobe儲存裝置
1. [MSRP](/help/communities/msrp.md) - MongoDb
1. [JSRP](/help/communities/jsrp.md) - JCR

## 關於UGC儲存 {#about-ugc-storage}

有關UGC的儲存，務必要瞭解的是，當網站設定為使用ASRP或MSRP時，實際的UGC並不會儲存在AEM中 [節點存放區](/help/sites-deploying/data-store-config.md) (JCR)。

雖然JCR中可能有遮蔽UGC以提供有用中繼資料的節點，但請勿將這些節點與實際UGC混淆。

另請參閱 [儲存資源提供者概觀。](/help/communities/srp.md)

## 最佳實務 {#best-practice}

在開發自訂元件時，開發人員應謹慎編寫程式碼，避免使用目前選擇的拓撲，以保留日後移至新拓撲的彈性。

### 假設JCR不可用 {#assume-jcr-not-available}

應避免使用JCR專屬方法。

使用的方法：

* Sling API （Sling資源）

   * 請勿假設有JCR節點

* OSGi事件

   * 不要假設有JCR事件

* [SocialResourceUtilities](/help/communities/socialutils.md#socialresourceutilities-package)
* [SCFUtilities](/help/communities/socialutils.md#scfutilities-package)

避免的方法：

* 節點API
* JCR事件
* 工作流程啟動器（使用JCR事件）

### 使用搜尋集合 {#use-search-collections}

不同的SRP可以有不同的原生查詢語言。 使用來自以下專案的方法： [com.adobe.cq.social.ugc.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) 封裝以執行適當的查詢語言。

如需詳細資訊，請參閱 [搜尋Essentials](/help/communities/search-implementation.md).

## 資源 {#resources}

* [社群內容儲存](/help/communities/working-with-srp.md)  — 討論UGC公用存放區的可用SRP選擇
* [儲存資源提供者概觀](/help/communities/srp.md)  — 簡介和存放庫使用概述
* [srp和UGC Essentials](/help/communities/srp-and-ugc.md) - SRP公用程式方法與範例
* [搜尋Essentials](/help/communities/search-implementation.md)  — 搜尋UGC的基本資訊
* [SocialUtils重構](/help/communities/socialutils.md)  — 將已棄用的公用程式方法對應到目前的SRP公用程式方法
