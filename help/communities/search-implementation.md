---
title: Search Essentials
seo-title: Search Essentials
description: 在社群中搜尋
seo-description: 在社群中搜尋
uuid: 5f35a033-2069-499e-9cdb-db25781312f0
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 300aa9f3-596f-42bc-8d46-e535f2bc4379
translation-type: tm+mt
source-git-commit: 9a4ae73c08657195da2741cccdb196bd7f7142c9
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 4%

---


# Search Essentials {#search-essentials}

## 概覽 {#overview}

搜尋功能是AEM Communities的必備功能。 除了[AEM平台搜尋](../../help/sites-deploying/queries-and-indexing.md)功能外，AEM Communities還提供[UGC搜尋API](#ugc-search-api)，以搜尋使用者產生的內容(UGC)。 UGC在輸入時具有唯一屬性，並與其他AEM內容和使用者資料分開儲存。

對於「社群」，通常搜尋的兩項功能為：

* 社群成員張貼的內容

   * 使用AEM Communities的UGC搜尋API。

* 使用者和使用者群組（使用者資料）

   * 使用AEM平台搜尋功能。

說明檔案的本節內容對於建立建立或管理UGC的自訂元件的開發人員而言十分有用。

## 安全性和卷影節點{#security-and-shadow-nodes}

對於自訂元件，必須使用[SocialResourceUtilities](socialutils.md#socialresourceutilities-package)方法。 建立和搜索UGC的實用程式方法將建立所需的[卷影節點](srp.md#about-shadow-nodes-in-jcr)，並確保成員具有正確的請求權限。

未通過SRP實用程式管理的是與協調相關的屬性。

有關用於訪問UGC和ACL卷影節點的實用方法的資訊，請參見[SRP和UGC Essentials](srp-and-ugc.md)。

## UGC搜尋API {#ugc-search-api}

[UGC公共儲存](working-with-srp.md)由多種儲存資源提供器(SRP)之一提供，每個儲存資源提供器可能具有不同的本地查詢語言。 因此，無論選擇何種SRP，自訂代碼都應使用[UGC API套件](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html)(*com.adobe.cq.social.ugc.api*)中的方法，這些方法將調用適合於所選SRP的查詢語言。

### ASRP搜索{#asrp-searches}

對於[ASRP](asrp.md),UGC會儲存在Adobe雲端。 雖然UGC在CRX中不可見，但[moderation](moderate-ugc.md)可從作者和發佈環境使用。 使用[UGC搜索API](#ugc-search-api)對ASRP的作用與對其他SRP的作用相同。

目前不存在用於管理ASRP搜索的工具。

建立可搜尋的自訂屬性時，必須符合[命名要求](#naming-of-custom-properties)。

### MSRP搜尋{#msrp-searches}

對於[MSRP](msrp.md),UGC儲存在配置為使用Solr進行搜索的MongoDB中。 UGC在CRX中不會顯示，但[moderation](moderate-ugc.md)可從作者和發佈環境使用。

關於MSRP和Solr:

* AEM平台的內嵌Solr不會用於MSRP。
* 如果將遠端Solr用於AEM平台，則可能會與MSRP共用，但他們應使用不同的系列。
* Solr可設定為標準搜尋或多語言搜尋(MLS)。
* 有關配置詳細資訊，請參見[Solr Configuration](msrp.md#solr-configuration) for MSRP。

自訂搜尋功能應使用[UGC搜尋API](#ugc-search-api)。

建立可搜尋的自訂屬性時，必須符合[命名要求](#naming-of-custom-properties)。

### JSRP搜索{#jsrp-searches}

對於[JSRP](jsrp.md),UGC會儲存在[Oak](../../help/sites-deploying/platform.md)中，且僅會顯示在輸入AEM作者的儲存庫或發佈例項中。

由於UGC通常是在發佈環境中輸入的，對於多發佈者生產系統，因此必須配置[發佈叢集](topologies.md)，而非發佈叢集，以便所有發佈者都能看到輸入的內容。

對於JSRP，在發佈環境中輸入的UGC在作者環境中將不可見。 因此，所有[協調](moderate-ugc.md)工作都會在發佈環境中進行。

自訂搜尋功能應使用[UGC搜尋API](#ugc-search-api)。

#### Oak索引{#oak-indexing}

雖然Oak索引不會自動為AEM平台搜尋建立，但是從AEM 6.2開始，已為AEM Communities新增這些索引，以改善效能並在呈現UGC搜尋結果時提供分頁支援。

如果自訂屬性正在使用中且搜尋速度緩慢，則需要為自訂屬性建立其他索引，以提高其效能。 若要維持可移植性，在建立可搜尋的自訂屬性時，請遵循[命名需求](#naming-of-custom-properties)。

要修改現有索引或建立自定義索引，請參閱[Oak Queries and Indexing](../../help/sites-deploying/queries-and-indexing.md)。

[Oak Index Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/oak-index-manager.html)可從ACS AEM Commons取得。 它提供：

* 現有索引的視圖。
* 啟動重新索引的能力。

若要在[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)中檢視現有的Oak索引，位置為：

* `/oak:index/socialLucene`

![social-lucene](assets/social-lucene.png)

## 索引搜索屬性{#indexed-search-properties}

### 預設搜索屬性{#default-search-properties}

以下是用於各種「社群」功能的一些可搜尋屬性：

| **屬性** | **資料類型** |
|---|---|
| isPratged | *布林值 (Boolean)* |
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
| 回覆 | *長整數* |
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

添加自定義屬性時，為了使這些屬性對使用[UGC搜索API](#ugc-search-api)建立的排序和搜索可見，需要&#x200B;**&#x200B;為屬性名稱添加尾碼。

尾碼用於使用架構的查詢語言：

* 它會將屬性識別為可搜尋。
* 它識別資料類型。

Solr是使用架構的查詢語言的示例。

| **字尾** | **資料類型** |
|---|---|
| _b | *布林值 (Boolean)* |
| _dt | *日曆* |
| _d | *雙精準數* |
| _tl | *長整數* |
| _s | *字串* |
| _t | *文字* |

**附註:**

* *Textis a* token化字串，  ** Stringis not.使用&#x200B;*Text*&#x200B;進行模糊搜尋（更類似此）。

* 對於多值類型，請在尾碼中添加「s」，例如：

   * `viewDate_dt`:單一日期屬性
   * `viewDates_dts`:dates屬性清單

## 濾鏡 {#filters}

包含[注釋系統](essentials-comments.md)的元件支援將過濾器參數添加到其端點。

AND和OR邏輯的篩選語法如下所示（在進行URL編碼前顯示）:

* 若要指定OR，請使用一個具有逗號分隔值的篩選參數：

   * `filter=name eq 'Jennifer',name eq 'Jen'`

* 要指定AND，請使用多個篩選參數：

   * `filter = name eq 'Jackson'&filter=message eq 'testing'`

[Search元件](search.md)的預設實作會使用此語法，如[Community Components指南](components-guide.md)中開啟「搜尋結果」頁面的URL所示。 若要實驗，請瀏覽至[http://localhost:4503/content/community-components/en/search.html](http://localhost:4503/content/community-components/en/search.html)。

篩選運算子有：

| EQ | 等於 |
|---|---|
| NE | 不等於 |
| LT | 小於 |
| LTE | 小於或等於 |
| GE | 大於 |
| GTE | 大於或等於 |
| 贊 | 模糊匹配 |

URL必須參照Communities元件（資源），而非放置元件的頁面：

* 正確：論壇元件
   * `/content/community-components/en/forum/jcr:content/content/forum.social.json`
* 錯誤：論壇頁面
   * `/content/community-components/en/forum.social.json`

## SRP工具{#srp-tools}

Adobe Marketing Cloud GitHub專案包含：

[AEM Communities SRP工具](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

此儲存庫包含用於管理SRP中資料的工具。

目前，有一個Servlet可以從任何SRP中刪除所有UGC。

例如，若要刪除ASRP中的所有UGC:

```shell
curl -X POST http://localhost:4502/services/social/srp/cleanup?path=/content/usergenerated/asi/cloud -uadmin:admin
```

## 疑難排解 {#troubleshooting}

### Solr查詢{#solr-query}

若要協助疑難排解Solr查詢的問題，請啟用

`com.adobe.cq.social.srp.impl.SocialSolrConnector`。

實際的Solr查詢會顯示在偵錯記錄中編碼的URL:

對索爾的查詢是：`sort=timestamp+desc&bl=en&pl=en&start=0&rows=10 &q=%2Btitle_t:(hello)+%2Bprovider_id:\/content/usergenerated/asi/mongo/content/+%2Bresource_type_s:&df=provider_id&trf=verbatim&fq={!cost%3D100}report_suite:mongo`

`q`參數的值是查詢。 一旦解碼URL編碼，查詢就可以傳遞至Solr Admin Query工具，以進一步除錯。

## 相關資源 {#related-resources}

* [社群內容儲存](working-with-srp.md) -討論UGC公用商店的可用SRP選擇。
* [儲存資源提供方概述](srp.md) -簡介和儲存庫使用概述。
* [使用SRP](accessing-ugc-with-srp.md) -編碼准則存取UGC。
* [SocialUtils重構](socialutils.md) -取代SocialUtils之SRP的公用程式方法。
* [搜尋和搜尋結果元件](search.md) -將UGC搜尋功能新增至範本。

