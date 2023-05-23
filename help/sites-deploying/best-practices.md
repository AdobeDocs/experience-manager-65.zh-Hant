---
title: 部署最佳做法
seo-title: Deploying Best Practices
description: 部署和維護最佳做法。
seo-description: Deploying and maintaining best practices.
uuid: 4546ed2c-43d5-40f3-874f-567b324e78c2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 4b5c0677-c630-4fae-867e-4f4583ac8507
exl-id: 4cbc0a30-d5f6-40ff-b7f6-8d64762e1970
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 9%

---

# 部署最佳做法{#deploying-best-practices}

部署最佳做法介紹如何以盡可能最AEM高效和最有效的方式部署或維護。 這個不斷增加的主題清單包括了多個AEM領域。

以下領域提供了有關部署和維護最佳做法和建議的文檔：

* [橡樹](#oak)
* [社群](#communities)
* [UI](#ui)
* [效能](#performance)

有關管理、開發或創作的最佳做法，請參閱以下內容之一：

* [管理最佳做法](/help/sites-administering/administer-best-practices.md)
* [制定最佳做法](/help/sites-developing/best-practices.md)
* [編寫最佳做法](/help/sites-authoring/best-practices.md)

具體文檔將在隨後的表中進行描述和連結。

## 橡樹 {#oak}

[橡樹](/help/sites-deploying/platform.md) 是可擴展且效能高的分層內容儲存庫，是其基礎AEM。

<table>
 <tbody>
  <tr>
   <td><p>可擴充性、效能和災難恢復</p> </td>
   <td><a href="/help/sites-deploying/performance.md">效能和可擴充性</a></td>
   <td>提供白皮書，討論技術靈活性、高效能和可靠的災難恢復功能</td>
  </tr>
  <tr>
   <td>建議的OAK部署</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">建議的部署</a></td>
   <td>描述部署方案</td>
  </tr>
  <tr>
   <td>Mongo拓撲</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Mongo拓撲最佳實踐</a></td>
   <td>描述mongo拓撲 — 何時使用哪種拓撲。</td>
  </tr>
  <tr>
   <td>資料儲存選項</td>
   <td><a href="/help/sites-deploying/data-store-config.md">配置節點和資料儲存</a></td>
   <td>本文檔介紹有關儲存二進位資料和內容節點的最佳做法。 包括有關使用AmazonS3資料儲存的資訊。</td>
  </tr>
  <tr>
   <td>在OAK中搜索</td>
   <td><a href="/help/sites-deploying/best-practices-for-queries-and-indexing.md">查詢和索引的最佳做法</a><br /> </td>
   <td>介紹如何索引內容的最佳做法。</td>
  </tr>
 </tbody>
</table>

## 社群 {#communities}

AEM Communities簡化了內部社區的建立和管理。 下面介紹了AEM Communities的最佳做法：

[社區內容儲存](/help/communities/working-with-srp.md)  — 討論用戶生成內容(UGC)的新共用儲存功能以及選擇底層內容的注意事項 [拓撲](/help/communities/topologies.md)。

[建議的社區部署](/help/sites-deploying/recommended-deploys.md#considerations-for-aem-communities)  — 介紹建議的社區部署。 |

## UI {#ui}

下面介紹了用戶介面的最佳實踐：

[面向客戶的用戶介面Recommendations](/help/sites-deploying/ui-recommendations.md)

當AEM前有兩個UI:在同一版本中提供經典和觸控優化用戶介面。 因此，客戶必須在項目實施期間決定使用哪個。 本文檔旨在幫助找到正確的選擇。

## 效能 {#performance}

下面列出了有關效能的最佳做法：

<table>
 <tbody>
  <tr>
   <td>質量保證的最佳做法</td>
   <td><a href="/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance">質量保證的最佳做法</a></td>
   <td>對與為您的Testtest而專門定義「概念」相關問題的標準化概述 <em>發佈</em> 環境。 QA工程師、項目經理和系統管理員對此非常感興趣。</td>
  </tr>
  <tr>
   <td>搭配 CDN 使用 Dispatcher</td>
   <td><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html#using-dispatcher-with-a-cdn">搭配 CDN 使用 Dispatcher</a></td>
   <td>內容傳遞網路 (CDN) (例如 Akamai Edge Delivery 或 Amazon Cloud Front) 會從接近使用者的位置傳遞內容。</td>
  </tr>
  <tr>
   <td>效能優化</td>
   <td><a href="/help/sites-deploying/configuring-performance.md">效能優化</a></td>
   <td>一個關鍵問題是您的網站響應訪問者請求所花費的時間。</td>
  </tr>
  <tr>
   <td>效能測試</td>
   <td><a href="/help/sites-deploying/best-practices-for-performance-testing.md">效能測試的最佳做法</a></td>
   <td>介紹在部署上運行效能test的最AEM佳做法。<br /> </td>
  </tr>
 </tbody>
</table>
