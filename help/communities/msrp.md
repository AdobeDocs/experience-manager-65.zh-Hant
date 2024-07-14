---
title: MSRP - MongoDB儲存資源提供者
description: 設定AEM Communities以使用關聯式資料庫作為其公用存放區
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 799d5ae1-caac-4c92-8835-696ad25de553
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1142'
ht-degree: 0%

---

# MSRP - MongoDB儲存資源提供者 {#msrp-mongodb-storage-resource-provider}

## 關於MSRP {#about-msrp}

當AEM Communities設定為使用MSRP作為其通用存放區時，使用者產生的內容(UGC)可從所有製作和發佈執行個體存取，而不需要同步或復寫。

另請參閱[SRP選項的特性](working-with-srp.md#characteristics-of-srp-options)和[建議的拓撲](topologies.md)。

## 要求 {#requirements}

* [MongoDB](https://www.mongodb.org/)：

   * 2.6版或更新版本
   * 不需要設定mongos或分片
   * 強烈建議使用[復本集](#mongoreplicaset)
   * 可以在與AEM相同的主機上執行或遠端執行

* [Apache Solr](https://lucene.apache.org/solr/)：

   * Solr 7.0版
   * Solr需要Java 1.7或更高版本
   * 不需要服務
   * 選擇執行模式：
      * 獨立模式
      * [SolrCloud模式](solr.md#solrcloud-mode) （建議用於生產環境）
   * 多語言搜尋(MLS)選項：
      * [安裝標準MLS](solr.md#installing-standard-mls)
      * [安裝進階MLS](solr.md#installing-advanced-mls)

## MongoDB設定 {#mongodb-configuration}

### 選取MSRP {#select-msrp}

[儲存設定主控台](srp-config.md)允許選取預設儲存設定，以識別要使用哪個SRP實作。

在作者中，若要存取「儲存設定」主控台：

* 從全域導覽中，選取&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 社群]** > **[!UICONTROL 儲存設定]**。

![msrp](assets/msrp.png)

* 選取&#x200B;**[!UICONTROL MongoDB儲存資源提供者(MSRP)]**
* **[!UICONTROL mongoDB組態]**

   * **[!UICONTROL mongoDB URI]**

     *預設*： mongodb://localhost/?maxPoolSize=10&amp;waitQueueMultiple=5&amp;readPreference=secondaryPreferred

   * **[!UICONTROL mongoDB資料庫]**

     *預設*： communities

   * **[!UICONTROL mongoDB UGC集合]**

     *預設*：內容

   * **[!UICONTROL mongoDB附件集合]**

     *預設*：附件

* **[!UICONTROL SolrConfiguration]**

   * **[Zookeeper](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)主機**

     使用外部ZooKeeper在[SolrCloud模式](solr.md#solrcloud-mode)中執行時，請將此值設定為ZooKeeper的`HOST:PORT`，例如&#x200B;*my.server.com:2181*

     對於ZooKeeper Ensemble，請輸入逗號分隔的`HOST:PORT`值，例如&#x200B;*host1:2181，host2:2181*

     如果使用內部ZooKeeper以獨立模式執行Solr，則保留空白。
     *預設*： *&lt;blank>*

      * **[!UICONTROL Solr URL]**
在獨立模式下用來與Solr通訊的URL。
若以SolrCloud模式執行，則保留空白。
        *預設*： https://127.0.0.1:8983/solr/

      * **[!UICONTROL Solr集合]**
Solr集合名稱。
        *預設*： collection1

* 選取&#x200B;**[!UICONTROL 提交]**

>[!NOTE]
>
>預設名稱為`communities`的mongoDB資料庫不應設為用於[節點存放區或資料（二進位）存放區](../../help/sites-deploying/data-store-config.md)的資料庫名稱。 另請參閱AEM 6.5](../../help/sites-deploying/storage-elements-in-aem-6.md)中的[儲存元素。

### MongoDB復本集 {#mongodb-replica-set}

對於生產環境，強烈建議設定復本集，即實作主要次要復寫及自動容錯移轉的MongoDB伺服器叢集。

若要深入瞭解復本集，請瀏覽MongoDB的[復寫](https://docs.mongodb.org/manual/replication/)檔案。

若要使用復本集並瞭解如何定義應用程式與MongoDB執行個體之間的連線，請瀏覽MongoDB的[連線字串URI格式](https://docs.mongodb.org/manual/reference/connection-string/)檔案。

#### 連線到復本集的Url範例  {#example-url-for-connecting-to-a-replica-set}

```shell
# Example url for:
# servers "mongoserver1", "mongoserver2", "mongoserver3"
# replica set 'rs0'
# port numbers only necessary if not default port 27017
mongodb://mongoserver1:<mongoport1>,mongoserver2:<mongoport2>,mongoserver3:<mongoport3>/?replicaSet=rs0&maxPoolSize=100&waitQueueMultiple=50&readPreference=secondaryPreferred
```

## Solr 設定 {#solr-configuration}

可以使用不同的集合，在節點存放區(Oak)與共用存放區(MSRP)之間共用Solr安裝。

如果Oak和MSRP集合都大量使用，則可能會基於效能原因安裝第二個Solr。

在生產環境中，[SolrCloud模式](solr.md#solrcloud-mode)比獨立模式（單一本機Solr設定）提供更優異的效能。

如需組態詳細資訊，請參閱SRP](solr.md)的[Solr組態。

### 升級 {#upgrading}

如果從以MSRP設定的舊版升級，則需要：

1. 執行[升級至AEM Communities](upgrade.md)
1. 安裝新的Solr組態檔
   * 針對[標準MLS](solr.md#installing-standard-mls)
   * 針對[進階MLS](solr.md#installing-advanced-mls)
1. 重新索引MSRP
請參閱[MSRP重新索引工具](#msrp-reindex-tool)小節

## 發佈設定 {#publishing-the-configuration}

MSRP必須識別為所有製作和發佈執行個體上的通用存放區。

若要在發佈環境中使用相同的設定，請登入您的製作執行個體並依照下列步驟進行：

* 從主功能表瀏覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 作業]** > **[!UICONTROL 復寫]**。
* 選取&#x200B;**[!UICONTROL 啟動樹狀結構]**
* **[!UICONTROL 開始路徑]**：
   * 瀏覽至`/etc/socialconfig/srpc/`
* 選取&#x200B;**[!UICONTROL 啟動]**

## 管理使用者資料 {#managing-user-data}

如需&#x200B;*使用者*、*使用者設定檔*&#x200B;和&#x200B;*使用者群組*&#x200B;的相關資訊（通常已進入發佈環境），請造訪

* [使用者同步](sync.md)
* [管理使用者和使用者群組](users.md)

## MSRP重新索引工具 {#msrp-reindex-tool}

安裝新組態檔或修復損壞的Solr索引時，有HTTP端點可為MSRP重新索引Solr。

使用此工具，MongoDB是MSRP的&#x200B;*真相*&#x200B;來源；僅需備份MongoDB。

您可以重新索引整個UGC樹狀結構，或只重新索引特定的子樹狀結構，如*path *data引數所指定。

此工具可使用cURL或任何其他HTTP工具從命令列執行。

重新索引時，會權衡由*batchSize *data引數（指定每個批次重新索引的UGC記錄數）控制的記憶體與效能。

合理的預設值為5000：

* 如果記憶體有問題，請指定較小的數字
* 如果速度有問題，請指定較大的數字以增加速度

### 使用cURL命令執行MSRP重新索引工具 {#running-msrp-reindex-tool-using-curl-command}

以下cURL命令顯示HTTP要求重新索引儲存在MSRP中的UGC所需的專案。

基本格式為：

cURL -u *登入* -d *資料* *重新索引 — url*

*登入* =系統管理員ID：密碼
例如： admin：admin

*資料* = &quot;batchSize=*size*&amp;path=*path&quot;*

*size* =每個作業要重新索引的UGC專案數
`/content/usergenerated/asi/mongo/`

*path* =要重新索引的UGC樹狀結構的根位置

* 若要重新索引所有UGC，請指定的`asipath`屬性值
  `/etc/socialconfig/srpc/defaultconfiguration`
* 若要將索引限製為某些UGC，請指定`asipath`的子樹狀結構

*reindex-url* =重新索引SRP的端點
`http://localhost:4503/services/social/datastore/mongo/reindex`

>[!NOTE]
>
>如果您[正在重新索引DSRP Solr](dsrp.md)，則URL是&#x200B;**/services/social/datastore/rdb/reindex**

### MSRP重新索引範例 {#msrp-reindex-example}

```shell
curl -s -u admin:admin -d 'batchSize=10000&path=/content/usergenerated/asi/mongo/' http://localhost:4503/services/social/datastore/mongo/reindex
```

## 如何示範MSRP {#how-to-demo-msrp}

若要設定MSRP用於示範或開發環境，請參閱[如何設定MongoDB用於示範](demo-mongo.md)。

## 疑難排解 {#troubleshooting}

### UGC在MongoDB中不可見 {#ugc-not-visible-in-mongodb}

檢查儲存選項的設定，確定MSRP已設定為預設提供者。 依預設，儲存資源提供者為JSRP。

在所有作者和發佈AEM執行個體上，重新造訪[儲存設定主控台](srp-config.md)或檢查AEM存放庫：

* 在JCR中，若為[/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

   * 不包含[srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc)節點，這表示儲存提供者是JSRP。
   * 如果srpc節點存在且包含節點[defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)，則defaultconfiguration的屬性應該將MSRP定義為預設提供者。

### 升級後UGC消失 {#ugc-disappears-after-upgrade}

如果從現有的AEM Communities 6.0網站升級，在升級至AEM Communities 6.3後，必須轉換任何預先存在的UGC以符合[SRP](srp.md) API所需的結構。

GitHub上有一個開放原始碼工具可用於此用途：

* [AEM Communities UGC移轉工具](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

可自訂移轉工具，從舊版AEM Social Communities匯出UGC，以匯入AEM Communities 6.1或更新版本。

### 錯誤 — 未定義的欄位provider_id {#error-undefined-field-provider-id}

如果記錄中出現以下錯誤，則表示Solr結構描述檔案未正確設定。

#### JsonMappingException：未定義的欄位provider_id {#jsonmappingexception-undefined-field-provider-id}

```xml
Caused by: com.fasterxml.jackson.databind.JsonMappingException: undefined field provider_id
at com.fasterxml.jackson.databind.ser.DefaultSerializerProvider.serializeValue(DefaultSerializerProvider.java:129)
at com.fasterxml.jackson.databind.ObjectMapper.writeValue(ObjectMapper.java:1819)
at com.adobe.cq.social.scf.core.BaseSocialComponent.toJSONString(BaseSocialComponent.java:196)
... 124 common frames omitted
```

若要解決錯誤，在遵循[安裝標準MLS](solr.md#installing-standard-mls)的指示時，請確定：

* XML組態檔已複製到正確的Solr位置。
* Solr在新的組態檔取代現有的組態檔之後重新啟動。

### 與MongoDB的安全連線失敗 {#secure-connection-to-mongodb-fails}

如果嘗試建立與MongoDB伺服器的安全連線由於缺少類別定義而失敗，則必須更新可從公共maven存放庫取得的MongoDB驅動程式套件`mongo-java-driver`。

1. 從[https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar](https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar) （2.13.2版或更新版本）下載驅動程式。
1. 將套件組合複製到AEM例項的「crx-quickstart/install」資料夾。
1. 重新啟動AEM執行個體。

## 資源 {#resources}

* [AEM與MongoDB](../../help/sites-deploying/aem-with-mongodb.md)
* [MongoDB檔案](https://docs.mongodb.org/)
