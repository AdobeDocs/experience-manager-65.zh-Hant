---
title: 搜尋要點
seo-title: 搜尋要點
description: 在社群中搜尋
seo-description: 在社群中搜尋
uuid: 5f35a033-2069-499e-9cdb-db25781312f0
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 300aa9f3-596f-42bc-8d46-e535f2bc4379
exl-id: 8af5ee58-19d7-47b6-b45d-e88006703a5d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 4%

---

# Search Essentials {#search-essentials}

## 概覽 {#overview}

搜尋功能是AEM Communities的一項基本功能。 除了[AEM平台搜尋](../../help/sites-deploying/queries-and-indexing.md)功能外，AEM Communities還提供[UGC搜尋API](#ugc-search-api)以搜尋使用者產生的內容(UGC)。 UGC具有唯一屬性，因為它是單獨輸入和儲存的，與其他AEM內容和用戶資料分開。

對於Communities，一般會搜尋以下兩項：

* 社群成員張貼的內容

   * 使用AEM Communities的UGC搜尋API。

* 使用者和使用者群組（使用者資料）

   * 使用AEM平台搜尋功能。

開發人員在建立建立或管理UGC的自訂元件時，會關注檔案的本節。

## 安全性和卷影節點{#security-and-shadow-nodes}

對於自訂元件，必須使用[SocialResourceUtilities](socialutils.md#socialresourceutilities-package)方法。 建立和搜索UGC的實用程式方法將建立所需的[卷影節點](srp.md#about-shadow-nodes-in-jcr)，並確保成員具有該請求的正確權限。

未透過SRP公用程式管理的是與協調相關的屬性。

有關用於訪問UGC和ACL卷影節點的實用程式方法的資訊，請參閱[SRP和UGC Essentials](srp-and-ugc.md)。

## UGC搜尋API {#ugc-search-api}

[UGC公用儲存區](working-with-srp.md)由多種儲存資源提供器(SRP)之一提供，每個提供器可能具有不同的本機查詢語言。 因此，無論選擇什麼SRP，自訂程式碼都應使用[UGC API套件](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html)(*com.adobe.cq.social.ugc.api*)中的方法，以叫用適合所選SRP的查詢語言。

### ASRP搜索{#asrp-searches}

對於[ASRP](asrp.md),UGC儲存在Adobe雲中。 雖然UGC在CRX中不可見，但作者和發佈環境皆提供[moderation](moderate-ugc.md)。 使用[UGC搜尋API](#ugc-search-api)對ASRP的作用與其他SRP相同。

當前不存在用於管理ASRP搜索的工具。

建立可搜尋的自訂屬性時，必須符合[命名需求](#naming-of-custom-properties)。

### MSRP搜尋{#msrp-searches}

對於[MSRP](msrp.md),UGC儲存在配置為使用Solr進行搜索的MongoDB中。 UGC將不會顯示在CRX中，但[moderation](moderate-ugc.md)可同時從製作和發佈環境使用。

關於MSRP和Solr:

* MSRP不會使用AEM平台的內嵌解決方案。
* 如果為AEM平台使用遠端解決方案，則可與MSRP共用，但應使用不同的集合。
* Solr可配置為標準搜索或多語言搜索(MLS)。
* 如需設定詳細資訊，請參閱MSRP適用的[Solr設定](msrp.md#solr-configuration)。

自訂搜尋功能應使用[UGC搜尋API](#ugc-search-api)。

建立可搜尋的自訂屬性時，必須符合[命名需求](#naming-of-custom-properties)。

### JSRP搜索{#jsrp-searches}

對於[JSRP](jsrp.md),UGC會儲存在[Oak](../../help/sites-deploying/platform.md)中，且只會顯示在輸入UGC的AEM作者或發佈例項的存放庫中。

由於UGC通常是在發佈環境中輸入，對於多發佈者生產系統，因此必須配置[發佈叢集](topologies.md)而非發佈叢集，以便從所有發佈者看到輸入的內容。

針對JSRP，在發佈環境中輸入的UGC將永遠無法顯示在製作環境中。 因此，所有[moderation](moderate-ugc.md)工作都會在發佈環境中進行。

自訂搜尋功能應使用[UGC搜尋API](#ugc-search-api)。

#### Oak索引{#oak-indexing}

雖然AEM平台搜尋不會自動建立Oak索引，但自AEM 6.2起，已針對AEM Communities新增索引，以改善效能，並在顯示UGC搜尋結果時提供分頁支援。

如果自訂屬性正在使用中，且搜尋速度緩慢，則需要為自訂屬性建立其他索引，以提升其效能。 若要維持可移植性，在建立可搜尋的自訂屬性時，請遵循[命名需求](#naming-of-custom-properties)。

若要修改現有索引或建立自訂索引，請參閱[Oak Querys and Indexing](../../help/sites-deploying/queries-and-indexing.md)。

[Oak Index Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/oak-index-manager.html)可從ACS AEM公域取得。 它提供：

* 現有索引的視圖。
* 啟動重新索引的能力。

若要檢視[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)中的現有Oak索引，位置為：

* `/oak:index/socialLucene`

![social-lucene](assets/social-lucene.png)

## 索引搜索屬性{#indexed-search-properties}

### 預設搜索屬性{#default-search-properties}

以下是用於各種Communities功能的一些可搜索屬性：

| **屬性** | **資料類型** |
|---|---|
| 已標幟 | *布林值 (Boolean)* |
| isSpam | *布林值 (Boolean)* |
| 讀取 | *布林值 (Boolean)* |
| 影響 | *布林值 (Boolean)* |
| 附件 | *布林值 (Boolean)* |
| 情緒 | *長整數* |
| 已標籤 | *布林值 (Boolean)* |
| 已新增 | *日期* |
| modifiedDate | *日期* |
| 狀態 | *String* |
| userIdentifier | *字串* |
| 回復 | *長整數* |
| jcr:title | *字串* |
| jcr:description | *字串* |
| sling:resourceType | *字串* |
| allowThreadedReply | *布林值 (Boolean)* |
| isDraft | *布林值 (Boolean)* |
| publishDate | *日期* |
| publishJobId | *字串* |
| 已回答 | *布林值 (Boolean)* |
| 喬森納 | *布林值 (Boolean)* |
| 標籤 | *字串* |
| cq:Tag | *字串* |
| author_display_name | *字串* |
| location_t | *字串* |
| parentPath | *字串* |
| parentTitle | *字串* |

### 自訂屬性的命名{#naming-of-custom-properties}

新增自訂屬性時，為了讓這些屬性可見於以[UGC搜尋API](#ugc-search-api)建立的排序和搜尋中，在屬性名稱中新增尾碼是&#x200B;*required*。

尾碼適用於使用結構的查詢語言：

* 它會將屬性識別為可搜尋。
* 它會識別資料類型。

Solr是使用結構的查詢語言的範例。

| **字尾** | **資料類型** |
|---|---|
| _b | *布林值 (Boolean)* |
| _dt | *日曆* |
| _d | *雙精準數* |
| _tl | *長整數* |
| _s | *字串* |
| _t | *文字* |

**附註:**

* ** 文字是標籤字串， ** 字串不是。使用&#x200B;*文字*&#x200B;來執行模糊（更類似於此）搜尋。

* 對於多值類型，請將&#39;s&#39;新增至尾碼，例如：

   * `viewDate_dt`:單一日期屬性
   * `viewDates_dts`:日期屬性清單

## 濾鏡 {#filters}

包括[注釋系統](essentials-comments.md)的元件支援將篩選參數添加到其端點。

AND和OR邏輯的篩選語法如下表示（如在進行URL編碼前所示）:

* 要指定OR，請使用一個帶逗號分隔值的篩選器參數：

   * `filter=name eq 'Jennifer',name eq 'Jen'`

* 若要指定AND，請使用多個篩選參數：

   * `filter = name eq 'Jackson'&filter=message eq 'testing'`

[搜尋元件](search.md)的預設實作使用此語法，如[社群元件指南](components-guide.md)中開啟「搜尋結果」頁面的URL所示。 若要實驗，請瀏覽至[http://localhost:4503/content/community-components/en/search.html](http://localhost:4503/content/community-components/en/search.html)。

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

## SRP工具{#srp-tools}

Adobe Marketing Cloud GitHub專案包含：

[AEM Communities SRP工具](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

此存放庫包含管理SRP中資料的工具。

目前，有一個Servlet可從任何SRP中刪除所有UGC。

例如，要刪除ASRP中的所有UGC:

```shell
curl -X POST http://localhost:4502/services/social/srp/cleanup?path=/content/usergenerated/asi/cloud -uadmin:admin
```

## 疑難排解 {#troubleshooting}

### Solr查詢{#solr-query}

若要協助疑難排解Solr查詢的問題，請為

`com.adobe.cq.social.srp.impl.SocialSolrConnector`。

實際的Solr查詢會在除錯記錄中顯示URL編碼：

對索爾的查詢是：`sort=timestamp+desc&bl=en&pl=en&start=0&rows=10 &q=%2Btitle_t:(hello)+%2Bprovider_id:\/content/usergenerated/asi/mongo/content/+%2Bresource_type_s:&df=provider_id&trf=verbatim&fq={!cost%3D100}report_suite:mongo`

`q`參數的值為查詢。 解碼URL編碼後，查詢即可傳遞至Solr Admin Query工具，以進行進一步除錯。

## 相關資源 {#related-resources}

* [社群內容儲存](working-with-srp.md)  — 討論UGC通用商店可用的SRP選項。
* [儲存資源提供程式概述](srp.md)  — 簡介和儲存庫使用概述。
* [使用SRP存取UGC](accessing-ugc-with-srp.md)  — 編碼准則。
* [SocialUtils重構](socialutils.md)  — 取代SocialUtils的SRP公用程式方法。
* [搜尋和搜尋結果元件](search.md)  — 將UGC搜尋功能新增至範本。
