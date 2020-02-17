---
title: 使用SRP存取UGC
seo-title: 使用SRP存取UGC
description: 當網站設定為使用ASRP或MSRP時，實際UGC不會儲存在AEM的節點儲存區(JCR)中
seo-description: 當網站設定為使用ASRP或MSRP時，實際UGC不會儲存在AEM的節點儲存區(JCR)中
uuid: 30549f93-e370-4b8b-a35a-69e05884227e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 72d4022c-43ba-49e0-b94c-f2beabaef64d
docset: aem65
translation-type: tm+mt
source-git-commit: 70e6f2d8366456e5091b7b775dc40914948921ab

---


# 使用SRP存取UGC{#accessing-ugc-with-srp}

## 關於SRP {#about-srp}

所有AEM Communities元件和功能都建立在 [social元件架構(SCF)](/help/communities/scf.md)，此架構會呼叫SocialResourceProvider API以存取所有使用者產生的內容(UGC)。

在建立社區站點之前，必 [須配置儲存資源提供器(SRP)](/help/communities/working-with-srp.md) ，以選擇與底層拓撲一致的 [實施](/help/communities/topologies.md)。 SRP實施基於三種儲存選項：

1. [ASRP](/help/communities/asrp.md) - Adobe隨選儲存空間
1. [MSRP](/help/communities/msrp.md) - MongoDB
1. [JSRP](/help/communities/jsrp.md) - JCR

## 關於UGC儲存 {#about-ugc-storage}

有關UGC儲存的重要資訊是，當網站設定為使用ASRP或MSRP時，實際UGC不會儲存在AEM的 [節點儲存](/help/sites-deploying/data-store-config.md) (JCR)。

雖然JCR中可能有節點將UGC陰影化，以提供有用的中繼資料，但這些節點不會與實際的UGC混淆。

請參 [閱儲存資源提供方概述。](/help/communities/srp.md)

## 最佳實務 {#best-practice}

在開發自定義元件時，開發人員應當注意獨立於當前所選拓撲編碼，從而保留將來遷移到新拓撲的靈活性。

### 假設JCR不可用 {#assume-jcr-not-available}

應避免JCR的特定方法。

使用方法：

* Sling API(Sling Resource)

   * 不假設有JCR節點

* OSGi活動

   * 不假設有JCR事件

* [SocialResourceUtilities](/help/communities/socialutils.md#socialresourceutilities-package)
* [SCFUtilities](/help/communities/socialutils.md#scfutilities-package)

避免的方法：

* 節點API
* JCR事件
* 工作流程啟動程式（使用JCR事件）

### 使用搜尋系列 {#use-search-collections}

不同的SRP可以有不同的原生查詢語言。 建議使用com.adobe.cq.so [cial.ugc.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) package中的方法來執行適當的查詢語言。

如需詳細資訊，請參 [閱Search Essentials](/help/communities/search-implementation.md)。

## 資源 {#resources}

* [社群內容儲存](/help/communities/working-with-srp.md) -討論UGC公用商店的可用SRP選擇
* [儲存資源提供方概述](/help/communities/srp.md) -簡介和儲存庫使用概述
* [SRP和UGC Essentials](/help/communities/srp-and-ugc.md) - SRP實用程式方法和示例
* [Search Essentials](/help/communities/search-implementation.md) —— 搜尋UGC的基本資訊
* [SocialUtils重構](/help/communities/socialutils.md) -將不建議使用的公用程式方法對應至目前的SRP公用程式方法

