---
title: 部署最佳實務
seo-title: 部署最佳實務
description: 部署和維護最佳實務。
seo-description: 部署和維護最佳實務。
uuid: 4546ed2c-43d5-40f3-874f-567b324e78c2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 4b5c0677-c630-4fae-867e-4f4583ac8507
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 部署最佳實務{#deploying-best-practices}

部署最佳實務說明如何以最有效率且最有效的方式部署或維護AEM。 這份不斷增加的主題清單包含AEM中的多個領域。

以下區域提供有關部署和維護最佳做法和建議的文檔：

* [OAK](#oak)
* [社群](#communities)
* [UI](#ui)
* [效能](#performance)

如需管理、開發或撰寫的最佳實務，請參閱下列其中一項：

* [管理最佳實務](/help/sites-administering/administer-best-practices.md)
* [制定最佳做法](/help/sites-developing/best-practices.md)
* [編寫最佳實務](/help/sites-authoring/best-practices.md)

在下表中說明並連結特定檔案。

## OAK {#oak}

[Oak](/help/sites-deploying/platform.md) 是可擴充且具效能的階層式內容儲存庫，是AEM的基礎。

<table>
 <tbody>
  <tr>
   <td><p>可擴充性、效能和災難恢復</p> </td>
   <td><a href="/help/sites-deploying/performance.md">效能與可擴充性</a></td>
   <td>提供白皮書，討論技術敏捷性、高效能和可靠的災難恢復功能</td>
  </tr>
  <tr>
   <td>建議的OAK部署</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">建議的部署</a></td>
   <td>說明部署方案</td>
  </tr>
  <tr>
   <td>Mongo拓撲</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Mongo拓撲最佳實踐</a></td>
   <td>介紹mongo拓撲——何時使用哪種拓撲。</td>
  </tr>
  <tr>
   <td>資料儲存選項</td>
   <td><a href="/help/sites-deploying/data-store-config.md">配置節點和資料儲存</a></td>
   <td>本檔案說明有關儲存二進位資料和內容節點的最佳做法。 包括有關使用Amazon S3資料儲存的資訊。</td>
  </tr>
  <tr>
   <td>在OAK中搜尋</td>
   <td><a href="/help/sites-deploying/best-practices-for-queries-and-indexing.md">查詢和索引的最佳做法</a><br /> </td>
   <td>說明如何為內容建立索引的最佳實務。</td>
  </tr>
 </tbody>
</table>

## 社群 {#communities}

AEM Communities可簡化內部部署社群的建立和管理。 以下說明AEM Communities的最佳實務：

[社群內容商店](/help/communities/working-with-srp.md) -討論使用者產生的內容(UGC)的新共用儲存功能，以及選擇基礎拓撲的 [考量](/help/communities/topologies.md)。

[建議的社群部署](/help/sites-deploying/recommended-deploys.md#considerations-for-aem-communities) -說明建議的社群部署。 |

## UI {#ui}

以下說明使用者介面的最佳實務：

[客戶的使用者介面建議](/help/sites-deploying/ui-recommendations.md)

AEM目前有兩個UI:在同一版本中提供經典和觸控最佳化UI。 因此，客戶必須決定在專案實施期間要使用哪些項目。 本檔案旨在協助您找到正確的選擇。

## 效能 {#performance}

以下列出有關效能的最佳實踐：

<table>
 <tbody>
  <tr>
   <td>質量保證的最佳做法</td>
   <td><a href="/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance">質量保證的最佳做法</a></td>
   <td>針對發佈環境上的效能測試，明確定義測試概念所涉及問題的標準 <em>化概</em> 述。 QA工程師、項目經理和系統管理員對此感興趣。</td>
  </tr>
  <tr>
   <td>搭配使用 Dispatcher 與 CDN</td>
   <td><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html#using-dispatcher-with-a-cdn">搭配使用 Dispatcher 與 CDN</a></td>
   <td>內容傳遞網路 (CDN) (例如 Akamai Edge Delivery 或 Amazon Cloud Front) 會從接近使用者的位置傳遞內容。</td>
  </tr>
  <tr>
   <td>效能最佳化</td>
   <td><a href="/help/sites-deploying/configuring-performance.md">效能最佳化</a></td>
   <td>關鍵問題是您的網站回應訪客要求所花的時間。</td>
  </tr>
  <tr>
   <td>效能測試</td>
   <td><a href="/help/sites-deploying/best-practices-for-performance-testing.md">效能測試的最佳實務</a></td>
   <td>說明在AEM部署上執行效能測試的最佳實務。<br /> </td>
  </tr>
 </tbody>
</table>

