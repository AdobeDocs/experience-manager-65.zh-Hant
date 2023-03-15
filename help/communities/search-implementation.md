---
title: 搜尋要點
seo-title: Search Essentials
description: 在社群中搜尋
seo-description: Search in Communities
uuid: 5f35a033-2069-499e-9cdb-db25781312f0
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 300aa9f3-596f-42bc-8d46-e535f2bc4379
exl-id: 8af5ee58-19d7-47b6-b45d-e88006703a5d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1184'
ht-degree: 4%

---

# 搜尋要點 {#search-essentials}

## 概觀 {#overview}

搜尋功能是AEM Communities的一項基本功能。 除了 [AEM platform search](../../help/sites-deploying/queries-and-indexing.md) 功能，AEM Communities提供 [UGC搜尋API](#ugc-search-api) 以搜尋使用者產生的內容(UGC)。 UGC具有唯一屬性，因為它是單獨輸入和儲存的，與其他AEM內容和用戶資料分開。

對於Communities，一般會搜尋以下兩項：

* 社群成員張貼的內容

   * 使用AEM Communities的UGC搜尋API。

* 使用者和使用者群組（使用者資料）

   * 使用AEM平台搜尋功能。

開發人員在建立建立或管理UGC的自訂元件時，會關注檔案的本節。

## 安全性和卷影節點 {#security-and-shadow-nodes}

對於自訂元件，必須使用 [SocialResourceUtilities](socialutils.md#socialresourceutilities-package) 方法。 建立和搜尋UGC的公用程式方法將建立所需 [陰影節點](srp.md#about-shadow-nodes-in-jcr) 並確保成員對請求具有正確的權限。

未透過SRP公用程式管理的是與協調相關的屬性。

請參閱 [SRP和UGC要點](srp-and-ugc.md) 有關用於訪問UGC和ACL卷影節點的實用程式方法的資訊。

## UGC搜尋API {#ugc-search-api}

此 [UGC常用商店](working-with-srp.md) 由多種儲存資源提供者(SRP)之一提供，每個提供者可能具有不同的原生查詢語言。 因此，無論選擇何種SRP，自訂程式碼都應使用 [UGC API套件](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) (*com.adobe.cq.social.ugc.api*)，會叫用適合所選SRP的查詢語言。

### ASRP搜索 {#asrp-searches}

針對 [ASRP](asrp.md),UGC會儲存在Adobe雲中。 雖然UGC在CRX中不可見， [審核](moderate-ugc.md) 可在製作和發佈環境中使用。 使用 [UGC搜尋API](#ugc-search-api) ASRP與其他SRP的作用相同。

當前不存在用於管理ASRP搜索的工具。

建立可供搜尋的自訂屬性時，必須遵循 [命名需求](#naming-of-custom-properties).

### MSRP搜尋 {#msrp-searches}

針對 [MSRP](msrp.md),UGC會儲存在MongoDB中，設定為使用Solr進行搜尋。 UGC不會顯示在CRX中，但 [審核](moderate-ugc.md) 可在製作和發佈環境中使用。

關於MSRP和Solr:

* MSRP不會使用AEM平台的內嵌解決方案。
* 如果為AEM平台使用遠端解決方案，則可與MSRP共用，但應使用不同的集合。
* Solr可配置為標準搜索或多語言搜索(MLS)。
* 如需設定詳細資訊，請參閱 [Solr配置](msrp.md#solr-configuration) MSRP.

自訂搜尋功能應使用 [UGC搜尋API](#ugc-search-api).

建立可供搜尋的自訂屬性時，必須遵循 [命名需求](#naming-of-custom-properties).

### JSRP搜尋 {#jsrp-searches}

針對 [JSRP](jsrp.md),UGC會儲存在 [Oak](../../help/sites-deploying/platform.md) 和只會顯示在其輸入之AEM作者或發佈例項的存放庫中。

由於UGC通常是在發佈環境中輸入，因此對於多發佈者生產系統，必須設定 [發佈叢集](topologies.md)，而非發佈伺服器陣列，以便從所有發佈者看到輸入的內容。

針對JSRP，在發佈環境中輸入的UGC將永遠無法顯示在製作環境中。 所以 [審核](moderate-ugc.md) 工作會在發佈環境中進行。

自訂搜尋功能應使用 [UGC搜尋API](#ugc-search-api).

#### Oak Indexing {#oak-indexing}

雖然AEM平台搜尋不會自動建立Oak索引，但自AEM 6.2起，已針對AEM Communities新增索引，以改善效能，並在顯示UGC搜尋結果時提供分頁支援。

如果自訂屬性正在使用中，且搜尋速度緩慢，則需要為自訂屬性建立其他索引，以提升其效能。 要保持便攜性，請遵守 [命名需求](#naming-of-custom-properties) 建立可供搜尋的自訂屬性時。

要修改現有索引或建立自定義索引，請參閱 [Oak查詢和索引](../../help/sites-deploying/queries-and-indexing.md).

此 [Oak Index Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/oak-index-manager.html) 可從ACS AEM公域取得。 它提供：

* 現有索引的視圖。
* 啟動重新索引的能力。

若要在 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)，位置為：

* `/oak:index/socialLucene`

![social-lucene](assets/social-lucene.png)

## 索引搜索屬性 {#indexed-search-properties}

### 預設搜索屬性 {#default-search-properties}

以下是用於各種Communities功能的一些可搜索屬性：

| **屬性** | **資料類型** |
|---|---|
| 已標幟 | *布林值* |
| isSpam | *布林值* |
| 讀取 | *布林值* |
| 影響 | *布林值* |
| 附件 | *布林值* |
| 情緒 | *長整數* |
| 已標籤 | *布林值* |
| 已新增 | *日期* |
| modifiedDate | *日期* |
| 狀態 | *字串* |
| userIdentifier | *字串* |
| 回復 | *長整數* |
| jcr:title | *字串* |
| jcr:description | *字串* |
| sling:resourceType | *字串* |
| allowThreadedReply | *布林值* |
| isDraft | *布林值* |
| publishDate | *日期* |
| publishJobId | *字串* |
| 已回答 | *布林值* |
| 喬森納 | *布林值* |
| 標籤 | *字串* |
| cq:Tag | *字串* |
| author_display_name | *字串* |
| location_t | *字串* |
| parentPath | *字串* |
| parentTitle | *字串* |

### 自訂屬性的命名 {#naming-of-custom-properties}

新增自訂屬性時，為了讓這些屬性可供排序和使用 [UGC搜尋API](#ugc-search-api)，它 *必填* 為屬性名稱添加尾碼。

尾碼適用於使用結構的查詢語言：

* 它會將屬性識別為可搜尋。
* 它會識別資料類型。

Solr是使用結構的查詢語言的範例。

| **字尾** | **資料類型** |
|---|---|
| _b | *布林值* |
| _dt | *日曆* |
| _d | *雙精度* |
| _tl | *長整數* |
| _s | *字串* |
| _t | *文字* |

**附註:**

* *文字* 是被標籤的字串， *字串* 不是。 使用 *文字* 模糊（更像這樣）搜索。

* 對於多值類型，請將&#39;s&#39;新增至尾碼，例如：

   * `viewDate_dt`:單一日期屬性
   * `viewDates_dts`:日期屬性清單

## 篩選條件 {#filters}

包括 [註解系統](essentials-comments.md) 支援在其端點上新增篩選參數。

AND和OR邏輯的篩選語法如下表示（如在進行URL編碼前所示）:

* 要指定OR，請使用一個帶逗號分隔值的篩選器參數：

   * `filter=name eq 'Jennifer',name eq 'Jen'`

* 若要指定AND，請使用多個篩選參數：

   * `filter = name eq 'Jackson'&filter=message eq 'testing'`

預設實作 [搜尋元件](search.md) 會使用此語法，如在 [社群元件指南](components-guide.md). 若要實驗，請瀏覽至 [http://localhost:4503/content/community-components/en/search.html](http://localhost:4503/content/community-components/en/search.html).

篩選運算子包括：

| EQ | 等於 |
|---|---|
| NE | 不等於 |
| LT | 小於 |
| LTE | 小於或等於 |
| GE | 大於 |
| GET | 大於或等於 |
| LIKE | 模糊匹配 |

URL必須參考Communities元件（資源），而非元件放置所在的頁面：

* 正確：論壇元件
   * `/content/community-components/en/forum/jcr:content/content/forum.social.json`
* 錯誤：論壇頁面
   * `/content/community-components/en/forum.social.json`

## SRP工具 {#srp-tools}

Adobe Marketing Cloud GitHub專案包含：

[AEM Communities SRP工具](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

此存放庫包含管理SRP中資料的工具。

目前，有一個Servlet可從任何SRP中刪除所有UGC。

例如，要刪除ASRP中的所有UGC:

```shell
curl -X POST http://localhost:4502/services/social/srp/cleanup?path=/content/usergenerated/asi/cloud -uadmin:admin
```

## 疑難排解 {#troubleshooting}

### Solr查詢 {#solr-query}

若要協助疑難排解Solr查詢的問題，請為

`com.adobe.cq.social.srp.impl.SocialSolrConnector`。

實際的Solr查詢會在除錯記錄中顯示URL編碼：

對索爾的查詢是： `sort=timestamp+desc&bl=en&pl=en&start=0&rows=10 &q=%2Btitle_t:(hello)+%2Bprovider_id:\/content/usergenerated/asi/mongo/content/+%2Bresource_type_s:&df=provider_id&trf=verbatim&fq={!cost%3D100}report_suite:mongo`

的值 `q` 參數為查詢。 解碼URL編碼後，查詢即可傳遞至Solr Admin Query工具，以進行進一步除錯。

## 相關資源 {#related-resources}

* [社群內容儲存](working-with-srp.md)  — 討論UGC通用商店的可用SRP選擇。
* [儲存資源提供程式概述](srp.md)  — 簡介和存放庫使用概觀。
* [使用SRP存取UGC](accessing-ugc-with-srp.md)  — 編碼准則。
* [SocialUtils重構](socialutils.md)  — 取代SocialUtils的SRP公用程式方法。
* [搜尋和搜尋結果元件](search.md)  — 將UGC搜索功能添加到模板。
