---
title: 搜尋Essentials
description: 瞭解搜尋功能，這是AEM Communities的重要功能。 Communities也為使用者產生的內容提供搜尋API。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 8af5ee58-19d7-47b6-b45d-e88006703a5d
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 2%

---

# 搜尋Essentials {#search-essentials}

## 概觀 {#overview}

搜尋功能是Adobe Experience Manager (AEM) Communities的重要功能。 除了[AEM平台搜尋](../../help/sites-deploying/queries-and-indexing.md)功能外，AEM Communities還提供用於搜尋使用者產生的內容(UGC)的[UGC搜尋API](#ugc-search-api)。 UGC在輸入和儲存時，與其他AEM內容和使用者資料分開，因此有獨特的屬性。

針對Communities，通常會搜尋以下兩個專案：

* 社群成員張貼的內容

   * 它使用AEM Communities的UGC搜尋API。

* 使用者和使用者群組（使用者資料）

   * 它使用AEM平台搜尋功能。

建立自訂元件以建立或管理UGC的開發人員，可能會對說明檔案的此區段感興趣。

## 安全性與陰影節點 {#security-and-shadow-nodes}

自訂元件必須使用[SocialResourceUtilities](socialutils.md#socialresourceutilities-package)方法。 建立和搜尋UGC的公用程式方法會建立必要的[陰影節點](srp.md#about-shadow-nodes-in-jcr)，並確定成員擁有要求的正確許可權。

不透過SRP公用程式管理的內容為與仲裁相關的屬性。

請參閱[SRP和UGC Essentials](srp-and-ugc.md)，以取得有關用於存取UGC和ACL陰影節點的公用程式方法的資訊。

## UGC搜尋API {#ugc-search-api}

[UGC公用存放區](working-with-srp.md)是由不同的存放裝置資源提供者(SRP)之一所提供，每個提供者可能都有不同的原生查詢語言。 因此，無論選取的SRP為何，自訂程式碼都應該使用[UGC API套件](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) (*com.adobe.cq.social.ugc.api*)中的方法，它會叫用適合所選SRP的查詢語言。

### ASRP搜尋 {#asrp-searches}

對於[ASRP](asrp.md)，UGC儲存在Adobe雲端。 雖然UGC在CRX中不可見，但[調節](moderate-ugc.md)可在作者和Publish環境中使用。 [UGC搜尋API](#ugc-search-api)的使用在ASRP上的作用與其他SRP相同。

目前沒有管理ASRP搜尋的工具。

建立可搜尋的自訂屬性時，必須遵守[命名需求](#naming-of-custom-properties)。

### MSRP搜尋 {#msrp-searches}

針對[MSRP](msrp.md)，UGC儲存在設定為使用Solr進行搜尋的MongoDB中。 UGC在CRX中不可見，但[調節](moderate-ugc.md)可在作者和Publish環境中使用。

關於MSRP和Solr：

* AEM平台的內嵌Solr不用於MSRP。
* 如果針對AEM平台使用遠端Solr，則可與MSRP共用，但應使用不同的集合。
* Solr可設定為標準搜尋或多語言搜尋(MLS)。
* 如需組態詳細資訊，請參閱MSRP的[Solr組態](msrp.md#solr-configuration)。

自訂搜尋功能應該使用[UGC搜尋API](#ugc-search-api)。

建立可搜尋的自訂屬性時，必須遵守[命名需求](#naming-of-custom-properties)。

### JSRP搜尋 {#jsrp-searches}

對於[JSRP](jsrp.md)，UGC儲存在[Oak](../../help/sites-deploying/platform.md)中，並且只會在輸入它的AEM Author或Publish執行個體的存放庫中顯示。

由於UGC通常是在Publish環境中輸入，因此對於多發佈者生產系統，必須設定[發佈叢集](topologies.md)，而不是發佈陣列，以便所有發佈者都能看到輸入的內容。

若為JSRP，在Publish環境中輸入的UGC絕對不會顯示在製作環境中。 因此，所有[稽核](moderate-ugc.md)工作都會在Publish環境中進行。

自訂搜尋功能應該使用[UGC搜尋API](#ugc-search-api)。

#### Oak索引 {#oak-indexing}

雖然自AEM 6.2起，AEM平台搜尋不會自動建立Oak索引，但已為AEM Communities新增索引，以改進效能並在顯示UGC搜尋結果時支援分頁。

如果使用自訂屬性且搜尋速度緩慢，則必須為自訂屬性建立其他索引，以提高其效能。 若要維持可攜性，在建立可搜尋的自訂屬性時，請遵守[命名需求](#naming-of-custom-properties)。

若要修改現有索引或建立自訂索引，請參閱[Oak查詢與索引](../../help/sites-deploying/queries-and-indexing.md)。

[Oak索引管理員](https://adobe-consulting-services.github.io/acs-aem-commons/features/oak-index-manager.html)可從ACS AEM Commons取得。 它提供：

* 現有索引的檢視。
* 啟動重新索引的功能。

若要檢視[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)中的現有Oak索引，位置為：

* `/oak:index/socialLucene`

![social-lucene](assets/social-lucene.png)

## 索引搜尋屬性 {#indexed-search-properties}

### 預設搜尋屬性 {#default-search-properties}

以下是供各種Communities功能使用的一些可搜尋屬性：

| **屬性** | **資料型別** |
|---|---|
| isFlagged | *布林值* |
| isSpam | *布林值* |
| 讀取 | *布林值* |
| 影響 | *布林值* |
| 附件 | *布林值* |
| 情緒 | *長* |
| 已標幟 | *布林值* |
| 已新增 | *日期* |
| modifieddate | *日期* |
| 州別 | *字串* |
| userId | *字串* |
| 回覆 | *長* |
| jcr:title | *字串* |
| jcr：description | *字串* |
| sling:resourceType | *字串* |
| allowThreadedReply | *布林值* |
| isDraft | *布林值* |
| publishDate | *日期* |
| publishJobId | *字串* |
| 已回答 | *布林值* |
| chosenanswered | *布林值* |
| 標籤 | *字串* |
| cq：Tag | *字串* |
| author_display_name | *字串* |
| location_t | *字串* |
| parentpath | *字串* |
| parentTitle | *字串* |

### 命名自訂屬性 {#naming-of-custom-properties}

新增自訂屬性時，若要讓以[UGC搜尋API](#ugc-search-api)建立的排序和搜尋看見這些屬性，*需要*&#x200B;在屬性名稱中新增尾碼。

尾碼適用於使用結構的查詢語言：

* 它會將屬性識別為可搜尋。
* 它可識別資料型別。

Solr是使用結構描述的查詢語言範例。

| **尾碼** | **資料型別** |
|---|---|
| _b | *布林值* |
| _dt | *行事曆* |
| _d | *雙* |
| _tl | *長* |
| _s | *字串* |
| _t | *文字* |

**附註：**

* *Text*&#x200B;是代碼化字串，*String*&#x200B;不是。 使用&#x200B;*文字*&#x200B;進行模糊（類似這樣）搜尋。

* 對於多值型別，請在尾碼中新增&#39;s&#39;，例如：

   * `viewDate_dt`：單一日期屬性
   * `viewDates_dts`：日期屬性清單

## 篩選條件 {#filters}

包含[註解系統](essentials-comments.md)的元件除了其端點之外，也支援篩選引數。

AND和OR邏輯的篩選器語法如下（在URL編碼之前顯示）：

* 若要指定OR或使用帶有逗號分隔值的篩選器引數：

   * `filter=name eq 'Jennifer',name eq 'Jen'`

* 若要指定AND並使用多個篩選引數，請執行下列動作：

   * `filter = name eq 'Jackson'&filter=message eq 'testing'`

[搜尋元件](search.md)的預設實作會使用此語法，如在[社群元件指南](components-guide.md)中開啟搜尋結果頁面的URL中所見。 若要實驗，請瀏覽至[http://localhost:4503/content/community-components/en/search.html](http://localhost:4503/content/community-components/en/search.html)。

篩選器運運算元包括：

| EQ | 等於 |
|---|---|
| NE | 不等於 |
| LT | 小於 |
| LTE | 小於或等於 |
| GE | 大於 |
| GTE | 大於或等於 |
| 按讚 | 模糊比對 |

重要的是，URL應參考Communities元件（資源），而非該元件所在的頁面：

* 正確：論壇元件
   * `/content/community-components/en/forum/jcr:content/content/forum.social.json`
* 不正確：論壇頁面
   * `/content/community-components/en/forum.social.json`

## SRP工具 {#srp-tools}

有一個Adobe Experience Cloud GitHub專案，其中包含：

[AEM Communities SRP工具](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

此存放庫包含用於管理SRP中資料的工具。

目前有一個servlet可從任何SRP刪除所有UGC。

例如，若要刪除ASRP中的所有UGC：

```shell
curl -X POST http://localhost:4502/services/social/srp/cleanup?path=/content/usergenerated/asi/cloud -uadmin:admin
```

## 疑難排解 {#troubleshooting}

### Solr查詢 {#solr-query}

若要協助疑難排解Solr查詢的問題，請為啟用DEBUG記錄

`com.adobe.cq.social.srp.impl.SocialSolrConnector`。

實際Solr查詢會在偵錯記錄檔中顯示編碼的URL：

查詢至solr為： `sort=timestamp+desc&bl=en&pl=en&start=0&rows=10 &q=%2Btitle_t:(hello)+%2Bprovider_id:\/content/usergenerated/asi/mongo/content/+%2Bresource_type_s:&df=provider_id&trf=verbatim&fq={!cost%3D100}report_suite:mongo`

`q`引數的值為查詢。 解碼URL編碼後，即可將查詢傳遞到Solr管理查詢工具，以便進一步偵錯。

## 相關資源 {#related-resources}

* [社群內容存放區](working-with-srp.md) — 討論UGC公用存放區可用的可用的SRP選擇。
* [儲存資源提供者概觀](srp.md) — 簡介和存放庫使用概觀。
* [使用SRP存取UGC](accessing-ugc-with-srp.md) — 編碼准則。
* [SocialUtils重構](socialutils.md) — 取代SocialUtils的SRP公用程式方法。
* [搜尋和搜尋結果元件](search.md) — 正在新增UGC搜尋功能至範本。
