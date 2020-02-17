---
title: MSRP - MongoDB儲存資源提供程式
seo-title: MSRP - MongoDB儲存資源提供程式
description: 設定AEM Communities，以使用關聯式資料庫做為其公用儲存
seo-description: 設定AEM Communities，以使用關聯式資料庫做為其公用儲存
uuid: 9fc06d4f-a60f-4ce3-8586-bcc836aa7de6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 048f7b30-20c3-4567-bd32-38cf2643cf39
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# MSRP - MongoDB儲存資源提供程式 {#msrp-mongodb-storage-resource-provider}

## 關於MSRP {#about-msrp}

當AEM Communities設定為使用MSRP做為其公用儲存時，使用者產生的內容(UGC)可從所有作者和發佈例項存取，而不需同步或複製。

另請參 [閱SRP選項和建議的](working-with-srp.md#characteristics-of-srp-options)[拓撲特性](topologies.md)。

## 需求 {#requirements}

* [MongoDB](https://www.mongodb.org/):

   * 2.6版或更新版本
   * 無需配置蒙古檔案或共用
   * 強烈建議使用複製副本 [集](#mongoreplicaset)
   * 可能與AEM在相同的主機上執行，或遠端執行

* [Apache Solr](https://lucene.apache.org/solr/):

   * 4.10版或5版
   * Solr需要Java 1.7或更新版本
   * 無需服務
   * 運行模式選擇：
      * 獨立模式
      * [SolrCloud模式](solr.md#solrcloud-mode) （建議用於生產環境）
   * 多語言搜尋選擇(MLS)
      * [安裝標準MLS](solr.md#installing-standard-mls)
      * [安裝進階MLS](solr.md#installing-advanced-mls)

## MongoDB Configuration {#mongodb-configuration}

### 選擇MSRP {#select-msrp}

存 [儲配置控制台](srp-config.md) (Storage Configuration Console)允許選擇預設儲存配置，該配置標識要使用的SRP實施。

在作者中，要訪問儲存配置控制台：

* 從全域導覽：「工 **[!UICONTROL 具>社群>儲存設定」]**

![chlimage_1-28](assets/chlimage_1-28.png)

* Select **[!UICONTROL MongoDB Storage Resource Provider (MSRP)]**
* **[!UICONTROL mongoDB 設定]**

   * **[!UICONTROL mongoDB URI]**

      *預設*:mongodb://localhost/?maxPoolSize=10&amp;waitQueueMultiple=5&amp;readPreference=secondaryPreferred

   * **[!UICONTROL mongoDB 資料庫]**

      *預設*:社區

   * **[!UICONTROL mongoDB UGC 集合]**

      *預設*:內容

   * **[!UICONTROL mongoDB 附件集合]**

      *預設*:附件

* **[!UICONTROL SolrConfiguration]**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Zookeeper Host **

      在 [SolrCloud模式下與外部ZooKeeper一起執行時，將此值設為](solr.md#solrcloud-mode) ZooKeeper的值，例如 `HOST:PORT` my.server.com:2181 *For a ZooKeeper Ensemble，輸入逗號分隔*&#x200B;值，例如 `HOST:PORT`**host1:2181,host2:2181如果使用內部ZooKeeper以獨立模式運行Solr，請將其留空。
      *預設值*: *&lt;blank>*
   * **[!UICONTROL Solr URL]**在獨立模式下與Solr通訊的URL。
如果在SolrCloud模式中執行，請留空。
      *預設值*:https://127.0.0.1:8983/solr/
   * **[!UICONTROL Solr系列]**Solr系列名稱。
      *預設值*:collection1
* 選擇「提 **[!UICONTROL 交」]**

>[!NOTE]
>
>預設為名稱的mongoDB資料庫不 `communities`應設定為用於節點儲存或資料（二進位） [儲存的資料庫的名稱](../../help/sites-deploying/data-store-config.md)。 另請參閱 [AEM 6中的儲存元素](../../help/sites-deploying/storage-elements-in-aem-6.md)。

### MongoDB複製副本集 {#mongodb-replica-set}

對於生產環境，強烈建議設定複製副本集，即實施主從複製和自動故障切換的MongoDB伺服器群集。

要瞭解有關複製副本集的更多資訊，請訪問MongoDB的 [Replication](https://docs.mongodb.org/manual/replication/) 文檔。

要使用複製副本集並瞭解如何定義應用程式與MongoDB實例之間的連接，請訪問MongoDB的 [Connection String URI格式文檔](https://docs.mongodb.org/manual/reference/connection-string/) 。

#### 用於連接到複製副本集的示例Url {#example-url-for-connecting-to-a-replica-set}

```shell
# Example url for:
#     servers "mongoserver1", "mongoserver2", "mongoserver3"
#     replica set 'rs0'
# port numbers only necessary if not default port 27017
mongodb://mongoserver1:<mongoport1>,mongoserver2:<mongoport2>,mongoserver3:<mongoport3>/?replicaSet=rs0&maxPoolSize=100&waitQueueMultiple=50&readPreference=secondaryPreferred
```

## Solr 設定 {#solr-configuration}

Solr安裝可以通過使用不同的集合在節點儲存(Oak)和公共儲存(MSRP)之間共用。

如果Oak和MSRP系列都已大量使用，則可能會因效能原因安裝第二個Solr。

對於生產環境， [SolrCloud模式比獨立模式](solr.md#solrcloud-mode) （單一本機Solr設定）提供更佳的效能。

有關配置詳細資訊，請 [參閱SRP的Solr配置](solr.md)。

### 升級 {#upgrading}

如果從使用MSRP設定的舊版進行升級，則必須

1. 執行AEM [Communities升級](upgrade.md)
1. 安裝新的Solr配置檔案
   * 針對 [標準MLS](solr.md#installing-standard-mls)
   * 針對進 [階MLS](solr.md#installing-advanced-mls)
1. 重新索引MSRPSee區段 [MSRP重新索引工具](#msrp-reindex-tool)

## 發佈設定 {#publishing-the-configuration}

MSRP必須被識別為所有作者和發佈例項上的公用商店。

要使相同的配置在發佈環境中可用，請執行以下操作：

* 作者：
   * 從主菜單導航到「工 **[!UICONTROL 具」>「操作」>「複製」]**
   * 選擇 **[!UICONTROL 激活樹]**
   * **[!UICONTROL 開始路徑]**:
      * 瀏覽至 `/etc/socialconfig/srpc/`
   * 選取「啟 **[!UICONTROL 動」]**

## 管理使用者資料 {#managing-user-data}

如需使用者 *、使用者****、使用者*&#x200B;設定檔和使用者群組的相關資訊，請造訪

* [用戶同步](sync.md)
* [管理使用者和使用者群組](users.md)

## MSRP重新索引工具 {#msrp-reindex-tool}

在安裝新配置檔案或修復損壞的Solr索引時，有一個HTTP端點用於為MSRP的Solr重新編製索引。

MongoDB是MSRP的真 *相* ;只需對MongoDB執行備份。

整個UGC樹可以重新編製索引，或僅對*path *data參數指定的特定子樹進行索引。

此工具可使用cURL或任何其他HTTP工具從命令列執行。

在重新建立索引時，由*batchSize *data參數控制的記憶體與效能之間會進行權衡，此參數指定每批重新建立UGC記錄的數目。

合理的違約為5000:

* 如果記憶體有問題，請指定較小的數字
* 如果速度是問題，請指定較大的數目以增加速度

### 使用cURL命令執行MSRP重新索引工具 {#running-msrp-reindex-tool-using-curl-command}

以下cURL命令顯示HTTP要求重新索引儲存在MSRP中的UGC的必要項。

基本格式為：

cURL -u *簽名* -d *data**reindex-url*

*signin* = administrator-id:password例如：admin:admin

*data* = &quot;batchSize=*size*&amp;path=*path&quot;*

*size* =每個操作要重新索引的UGC條目數`/content/usergenerated/asi/mongo/`

*path* = UGC樹的根位置以重新索引

* 若要重新索引所有UGC，請指定 `asipath`的
   `/etc/socialconfig/srpc/defaultconfiguration`
* 若要將索引限制為某些UGC，請指定 `asipath`

*reindex-url* = SRP重新索引的端點`http://localhost:4503/services/social/datastore/mongo/reindex`

>[!NOTE]
>
>如果您正在 [重新索引DSRP Solr](dsrp.md)，則URL為 **/services/social/datastore/rdb/reindex**

### MSRP重新索引範例 {#msrp-reindex-example}

```shell
curl -s -u admin:admin -d 'batchSize=10000&path=/content/usergenerated/asi/mongo/' http://localhost:4503/services/social/datastore/mongo/reindex
```

## 如何示範MSRP {#how-to-demo-msrp}

若要為示範或開發環境設定MSRP，請參 [閱HowTo Setup MongoDB for Demo](demo-mongo.md)。

## 疑難排解 {#troubleshooting}

### UGC在MongoDB中不可見 {#ugc-not-visible-in-mongodb}

請檢查儲存選項的設定，以確定MSRP已設定為預設提供者。 預設情況下，儲存資源提供方是JSRP。

在所有作者和發佈AEM例項上，請重新造訪 [Storage Configuration Console](srp-config.md) ，或檢查AEM存放庫：

* 在JCR中，如 [果/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

   * 不包含srpc節 [點](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) ，這表示儲存提供程式是JSRP
   * 如果srpc節點存在並包含節點 [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)，則defaultconfiguration的屬性應將MSRP定義為預設提供程式

### 升級後UGC消失 {#ugc-disappears-after-upgrade}

如果從現有的AEM Communities 6.0網站升級，在升級至AEM Communities 6.3後，任何預先存在的UGC都必須轉換為符合 [SRP](srp.md) API所需的結構。

GitHub上提供開放原始碼工具，可用於：

* [AEM Communities UGC移轉工具](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

您可自訂移轉工具，從舊版AEM Social社群匯出UGC，以匯入至AEM Communities 6.1或更新版本。

### 錯誤——未定義的欄位provider_id {#error-undefined-field-provider-id}

如果日誌中出現以下錯誤，表示Solr架構檔案配置不正確。

#### JsonMappingException:未定義的欄位provider_id {#jsonmappingexception-undefined-field-provider-id}

```xml
Caused by: com.fasterxml.jackson.databind.JsonMappingException: undefined field provider_id
at com.fasterxml.jackson.databind.ser.DefaultSerializerProvider.serializeValue(DefaultSerializerProvider.java:129)
at com.fasterxml.jackson.databind.ObjectMapper.writeValue(ObjectMapper.java:1819)
at com.adobe.cq.social.scf.core.BaseSocialComponent.toJSONString(BaseSocialComponent.java:196)
... 124 common frames omitted
```

若要解決錯誤，請依照安裝標準MLS的 [指示進行](solr.md#installing-standard-mls)，請確保

* XML配置檔案被複製到正確的Solr位置
* 在新配置檔案替換現有配置檔案後，Solr重新啟動

### 與MongoDB的安全連接失敗 {#secure-connection-to-mongodb-fails}

如果嘗試與MongoDB伺服器建立安全連接時由於缺少類定義而失敗，則需要更新MongoDB驅動程式包(可從公共主儲存庫獲得 `mongo-java-driver`)。

1. 從https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar(2.13.2版 [或更新版本](https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar) )下載驅動程式
1. 將套件複製至AEM例項的「crx-quickstart/install」檔案夾
1. 重新啟動AEM例項

## 資源 {#resources}

* [AEM與MongoDB](../../help/sites-deploying/aem-with-mongodb.md)
* [MongoDB檔案](https://docs.mongodb.org/)

