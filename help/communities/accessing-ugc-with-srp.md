---
title: 使用SRP訪問UGC
seo-title: Accessing UGC with SRP
description: 當站點配置為使用ASRP或MSRP時，實際UGC不會儲存在節AEM點儲存(JCR)中
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

# 使用SRP訪問UGC {#accessing-ugc-with-srp}

## 關於SRP {#about-srp}

所有AEM Communities元件和功能都構建在 [社會構成框架](/help/communities/scf.md)，它調用SocialResourceProvider API以訪問所有用戶生成的內容(UGC)。

在建立社區站點之前， [儲存資源提供程式(SRP)](/help/communities/working-with-srp.md) 必須配置為選擇與基礎一致的實現 [拓撲](/help/communities/topologies.md)。 SRP實現基於三個儲存選項：

1. [ASRP](/help/communities/asrp.md) -Adobe按需儲存
1. [MSRP](/help/communities/msrp.md) - MongoDB
1. [JSRP](/help/communities/jsrp.md) - JCR

## 關於UGC儲存 {#about-ugc-storage}

要瞭解UGC的儲存，重要的是，當站點配置為使用ASRP或MSRP時，實際UGC不會儲存在 [節點儲存](/help/sites-deploying/data-store-config.md) (JCR)。

雖然JCR中可能存在對UGC進行陰影處理以提供有用元資料的節點，但這些節點不會與實際UGC混淆。

請參閱 [儲存資源提供程式概述。](/help/communities/srp.md)

## 最佳實踐 {#best-practice}

在開發定制元件時，開發人員應當謹慎地對當前所選拓撲進行編碼，從而保留將來遷移到新拓撲的靈活性。

### 假設JCR不可用 {#assume-jcr-not-available}

應避免針對JCR的方法。

使用的方法：

* Sling API（Sling資源）

   * 不假定有JCR節點

* OSGi事件

   * 不假定有JCR事件

* [社會資源實用程式](/help/communities/socialutils.md#socialresourceutilities-package)
* [SCFU實用性](/help/communities/socialutils.md#scfutilities-package)

要避免的方法：

* 節點API
* JCR事件
* 工作流啟動程式（使用JCR事件）

### 使用搜索集合 {#use-search-collections}

不同的SRP可以具有不同的本機查詢語言。 建議使用 [com.adobe.cq.social.ugc.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) 程式包以運行相應的查詢語言。

有關詳細資訊，請參見 [搜索要件](/help/communities/search-implementation.md)。

## 資源 {#resources}

* [社區內容儲存](/help/communities/working-with-srp.md)  — 討論UGC公用儲存的可用SRP選項
* [儲存資源提供程式概述](/help/communities/srp.md)  — 簡介和儲存庫使用概述
* [SRP和UGC軟體包](/help/communities/srp-and-ugc.md) - SRP實用程式方法和示例
* [搜索要件](/help/communities/search-implementation.md)  — 搜索UGC的基本資訊
* [SocialUtils重構](/help/communities/socialutils.md)  — 將過時的實用程式方法映射到當前SRP實用程式方法
