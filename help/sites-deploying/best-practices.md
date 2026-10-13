---
title: 部署最佳實務
description: 瞭解如何以最有效率且最有效率的方式部署及維護Adobe Experience Manager (AEM)。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 4cbc0a30-d5f6-40ff-b7f6-8d64762e1970
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 5ef752af-d616-5b23-8312-06964e46b208
    internal-label: Administering
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 13%
---
# 部署最佳實務{#deploying-best-practices}

部署最佳實務說明如何以最有效率和最有效率的方式部署或維護Adobe Experience Manager (AEM)。 這份不斷增加的主題清單包括AEM中的各個領域。

下列區域已有關於部署及維護最佳實務和建議的可用檔案：

* [Oak](#oak)
* [Communities](#communities)
* [UI](#ui)
* [效能](#performance)

如需管理、開發或編寫的最佳實務，請參閱下列其中一項：

* [管理最佳實務](/help/sites-administering/administer-best-practices.md)
* [開發最佳實務](/help/sites-developing/best-practices.md)
* [製作最佳實務](/help/sites-authoring/best-practices.md)

以下表格會說明並連結特定檔案。

## Oak {#oak}

[Oak](/help/sites-deploying/platform.md)是可擴充且高效能的分層式內容存放庫，是AEM的基礎。

<table>
 <tbody>
  <tr>
   <td><p>擴充性、效能和災難回覆</p> </td>
   <td><a href="/help/sites-deploying/performance.md">效能與擴充性</a></td>
   <td>提供白皮書，討論技術彈性、高效能及健全的災難回覆功能</td>
  </tr>
  <tr>
   <td>建議的Oak部署</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">建議的部署</a></td>
   <td>說明部署案例</td>
  </tr>
  <tr>
   <td>Mongo拓撲</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Mongo拓撲最佳實務</a></td>
   <td>說明mongo拓撲 — 何時使用哪個拓撲。</td>
  </tr>
  <tr>
   <td>資料存放區選項</td>
   <td><a href="/help/sites-deploying/data-store-config.md">設定節點和資料存放區</a></td>
   <td>本檔案說明有關儲存二進位資料和內容節點的最佳實務。 包含使用Amazon S3資料存放區的相關資訊。</td>
  </tr>
  <tr>
   <td>Oak中的搜尋</td>
   <td><a href="/help/sites-deploying/best-practices-for-queries-and-indexing.md">查詢和建立索引的最佳實務</a><br /> </td>
   <td>說明如何為內容建立索引的最佳實務。</td>
  </tr>
 </tbody>
</table>

## Communities {#communities}

AEM Communities可簡化內部部署社群的建立和管理。 AEM Communities的最佳實務說明如下：

[社群內容存放區](/help/communities/working-with-srp.md) — 討論使用者產生內容(UGC)的新共用存放區功能，以及選擇基礎[拓撲](/help/communities/topologies.md)的考量事項。

[社群的建議部署](/help/sites-deploying/recommended-deploys.md#considerations-for-aem-communities) — 說明社群的建議部署。 |

## UI {#ui}

有關使用者介面的最佳實務說明如下：

[客戶適用的使用者介面建議](/help/sites-deploying/ui-recommendations.md)

AEM目前在同一版本中有兩個UI：傳統和觸控最佳化UI。 因此，客戶必須在專案實作期間決定使用哪一個。 本檔案旨在協助您找到正確的選擇。

## 效能 {#performance}

效能相關最佳實務列於此處：

<table>
 <tbody>
  <tr>
   <td>高品質Assurance的最佳作法</td>
   <td><a href="/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance">高品質Assurance的最佳作法</a></td>
   <td>針對在您的<em>發佈</em>環境中進行效能測試時，定義測試概念所涉及問題的標準化概觀。 這主要是QA工程師、專案經理和系統管理員的興趣。</td>
  </tr>
  <tr>
   <td>搭配 CDN 使用 Dispatcher</td>
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html#using-dispatcher-with-a-cdn">搭配 CDN 使用 Dispatcher</a></td>
   <td>內容傳遞網路 (CDN) (例如 Akamai Edge Delivery 或 Amazon Cloud Front) 會從接近使用者的位置傳遞內容。</td>
  </tr>
  <tr>
   <td>效能最佳化</td>
   <td><a href="/help/sites-deploying/configuring-performance.md">效能最佳化</a></td>
   <td>關鍵問題是您的網站回應訪客要求所需的時間。</td>
  </tr>
  <tr>
   <td>效能測試</td>
   <td><a href="/help/sites-deploying/best-practices-for-performance-testing.md">效能測試的最佳實務</a></td>
   <td>說明在AEM部署上執行效能測試的最佳實務。<br /> </td>
  </tr>
 </tbody>
</table>
