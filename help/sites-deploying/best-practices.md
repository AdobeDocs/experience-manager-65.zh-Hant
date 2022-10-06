---
title: 部署最佳實務
seo-title: Deploying Best Practices
description: 部署和維護最佳實務。
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

# 部署最佳實務{#deploying-best-practices}

部署最佳實務說明如何以盡可能最有效率和最有效的方式部署或維護AEM。 這份不斷增加的主題清單包含AEM中的多個領域。

以下幾方面提供部署及維護最佳實務與建議的相關檔案：

* [OAK](#oak)
* [社群](#communities)
* [UI](#ui)
* [效能](#performance)

如需管理、開發或編寫的最佳實務，請參閱下列其中一項：

* [管理最佳實務](/help/sites-administering/administer-best-practices.md)
* [制定最佳做法](/help/sites-developing/best-practices.md)
* [製作最佳實務](/help/sites-authoring/best-practices.md)

下面的表中描述了特定文檔並連結到這些文檔。

## OAK {#oak}

[Oak](/help/sites-deploying/platform.md) 是可擴充且高效能的階層式內容存放庫，是AEM的基礎。

<table>
 <tbody>
  <tr>
   <td><p>可擴充性、效能和災難恢復</p> </td>
   <td><a href="/help/sites-deploying/performance.md">效能和可擴充性</a></td>
   <td>提供了一份白皮書，討論技術靈活性、高效能和健全的災難恢復功能</td>
  </tr>
  <tr>
   <td>建議的OAK部署</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">建議的部署</a></td>
   <td>說明部署方案</td>
  </tr>
  <tr>
   <td>蒙戈拓撲</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Mongo拓撲最佳實踐</a></td>
   <td>描述mongo拓撲 — 何時使用哪種拓撲。</td>
  </tr>
  <tr>
   <td>資料存放區選項</td>
   <td><a href="/help/sites-deploying/data-store-config.md">配置節點和資料儲存</a></td>
   <td>本檔案說明儲存二進位資料和內容節點的最佳實務。 包含使用Amazon S3資料存放區的相關資訊。</td>
  </tr>
  <tr>
   <td>在OAK中搜尋</td>
   <td><a href="/help/sites-deploying/best-practices-for-queries-and-indexing.md">查詢和建立索引的最佳實務</a><br /> </td>
   <td>說明如何為內容建立索引的最佳實務。</td>
  </tr>
 </tbody>
</table>

## 社群 {#communities}

AEM Communities可簡化內部部署社群的建立和管理作業。 以下說明AEM Communities的最佳實務：

[社群內容商店](/help/communities/working-with-srp.md)  — 討論用戶生成的內容(UGC)的新共用儲存功能，以及選擇基礎內容的注意事項 [拓撲](/help/communities/topologies.md).

[針對社群的建議部署](/help/sites-deploying/recommended-deploys.md#considerations-for-aem-communities)  — 說明Communities的建議部署。 |

## UI {#ui}

以下說明使用者介面的相關最佳實務：

[適用於客戶的使用者介面Recommendations](/help/sites-deploying/ui-recommendations.md)

AEM目前有兩個UI:在相同版本中使用傳統和觸控最佳化UI。 因此，客戶必須決定在專案實施期間要使用哪個項目。 本檔案旨在協助您找到正確的選擇。

## 效能 {#performance}

以下列出效能相關最佳實務：

<table>
 <tbody>
  <tr>
   <td>品質保證最佳實務</td>
   <td><a href="/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance">品質保證最佳實務</a></td>
   <td>針對您的 <em>發佈</em> 環境。 這主要是QA工程師、項目經理和系統管理員感興趣的。</td>
  </tr>
  <tr>
   <td>搭配 CDN 使用 Dispatcher</td>
   <td><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html#using-dispatcher-with-a-cdn">搭配 CDN 使用 Dispatcher</a></td>
   <td>內容傳遞網路 (CDN) (例如 Akamai Edge Delivery 或 Amazon Cloud Front) 會從接近使用者的位置傳遞內容。</td>
  </tr>
  <tr>
   <td>效能最佳化</td>
   <td><a href="/help/sites-deploying/configuring-performance.md">效能最佳化</a></td>
   <td>一個主要問題是您的網站回應訪客請求所花的時間。</td>
  </tr>
  <tr>
   <td>效能測試</td>
   <td><a href="/help/sites-deploying/best-practices-for-performance-testing.md">效能測試最佳實務</a></td>
   <td>說明在AEM部署上執行效能測試的最佳作法。<br /> </td>
  </tr>
 </tbody>
</table>
