---
title: MSRP - MongoDB儲存資源提供程式
seo-title: MSRP - MongoDB Storage Resource Provider
description: 設定AEM Communities以使用關係資料庫作為其公用儲存
seo-description: Set up AEM Communities to use a relational database as its common store
uuid: 9fc06d4f-a60f-4ce3-8586-bcc836aa7de6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 048f7b30-20c3-4567-bd32-38cf2643cf39
role: Admin
exl-id: 799d5ae1-caac-4c92-8835-696ad25de553
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1191'
ht-degree: 1%

---

# MSRP - MongoDB儲存資源提供程式 {#msrp-mongodb-storage-resource-provider}

## 關於MSRP {#about-msrp}

當AEM Communities設定為使用MSRP作為其常見存放區時，使用者產生的內容(UGC)可從所有製作和發佈執行個體存取，而無須同步或復寫。

另請參閱 [SRP選項的特點](working-with-srp.md#characteristics-of-srp-options) 和 [建議的拓撲](topologies.md).

## 要求 {#requirements}

* [MongoDB](https://www.mongodb.org/):

   * 2.6版或更高版本
   * 無需配置蒙古或共用
   * 強烈建議使用 [副本集](#mongoreplicaset)
   * 可在與AEM相同的主機上運行或遠程運行

* [阿帕奇索爾](https://lucene.apache.org/solr/):

   * Solr 7.0版
   * Solr需要Java 1.7或更高版本
   * 不需要任何服務
   * 運行模式的選擇：
      * 獨立模式
      * [SolrCloud模式](solr.md#solrcloud-mode) （建議用於生產環境）
   * 多語言搜尋(MLS)的選擇：
      * [安裝標準MLS](solr.md#installing-standard-mls)
      * [安裝進階MLS](solr.md#installing-advanced-mls)

## MongoDB配置 {#mongodb-configuration}

### 選擇MSRP {#select-msrp}

此 [儲存配置控制台](srp-config.md) 允許選擇預設儲存配置，以確定要使用的SRP實施。

在作者上，要訪問儲存配置控制台：

* 在全局導航中，選擇 **[!UICONTROL 工具]** > **[!UICONTROL 社群]** > **[!UICONTROL 儲存配置]**.

![msrp](assets/msrp.png)

* 選擇 **[!UICONTROL MongoDB儲存資源提供程式(MSRP)]**
* **[!UICONTROL mongoDB 設定]**

   * **[!UICONTROL mongoDB URI]**

      *預設*:mongodb://localhost/?maxPoolSize=10&amp;waitQueueMultiple=5&amp;readPreference=secondaryPreferred

   * **[!UICONTROL mongoDB 資料庫]**

      *預設*:社群

   * **[!UICONTROL mongoDB UGC 集合]**

      *預設*:內容

   * **[!UICONTROL mongoDB 附件集合]**

      *預設*:附件

* **[!UICONTROL SolrConfiguration]**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Zookeeper Host**

      執行時 [SolrCloud模式](solr.md#solrcloud-mode) 使用外部ZooKeeper，將此值設定為 `HOST:PORT` ZooKeeper，例如 *my.server.com:2181*

      對於ZooKeeper整體，請輸入逗號分隔 `HOST:PORT` 值，例如 *host1:2181,host2:2181*

      如果使用內部ZooKeeper以獨立模式運行Solr，請保留空白。
      *預設*: *&lt;blank>*

      * **[!UICONTROL Solr URL]**
用於以獨立模式與Solr通信的URL。
如果在SolrCloud模式中執行，請保留空白。

         *預設*:https://127.0.0.1:8983/solr/

      * **[!UICONTROL Solr集合]**
Solr集合名稱。

         *預設*:集合1

* 選擇 **[!UICONTROL 提交]**

>[!NOTE]
>
>mongoDB資料庫，預設為名稱 `communities`，不應將設為所用資料庫的名稱 [節點儲存或資料（二進位）儲存](../../help/sites-deploying/data-store-config.md). 另請參閱 [AEM 6.5中的儲存元素](../../help/sites-deploying/storage-elements-in-aem-6.md).

### MongoDB複製副本集 {#mongodb-replica-set}

對於生產環境，強烈建議設定一個複製副本集，即實現主次複製和自動故障切換的MongoDB伺服器群集。

要了解有關副本集的更多資訊，請訪問MongoDB的 [復寫](https://docs.mongodb.org/manual/replication/) 檔案。

要使用副本集並了解如何定義應用程式和MongoDB實例之間的連接，請訪問MongoDB的 [連接字串URI格式](https://docs.mongodb.org/manual/reference/connection-string/) 檔案。

#### 用於連接到副本集的示例Url  {#example-url-for-connecting-to-a-replica-set}

```shell
# Example url for:
# servers "mongoserver1", "mongoserver2", "mongoserver3"
# replica set 'rs0'
# port numbers only necessary if not default port 27017
mongodb://mongoserver1:<mongoport1>,mongoserver2:<mongoport2>,mongoserver3:<mongoport3>/?replicaSet=rs0&maxPoolSize=100&waitQueueMultiple=50&readPreference=secondaryPreferred
```

## Solr 設定 {#solr-configuration}

Solr安裝可透過使用不同集合在節點存放區(Oak)和公用存放區(MSRP)之間共用。

如果Oak和MSRP集合都被集中使用，可能會基於效能原因安裝第二個Solr。

針對生產環境， [SolrCloud模式](solr.md#solrcloud-mode) 與獨立模式（單個本地Solr設定）相比，提供了更好的效能。

如需設定詳細資訊，請參閱 [SRP的Solr配置](solr.md).

### 升級 {#upgrading}

如果從使用MSRP設定的舊版升級，必須：

1. 執行 [升級至AEM Communities](upgrade.md)
1. 安裝新的Solr配置檔案
   * 針對 [標準MLS](solr.md#installing-standard-mls)
   * 針對 [進階MLS](solr.md#installing-advanced-mls)
1. 重新索引MSRP請參閱一節 [MSRP重新索引工具](#msrp-reindex-tool)

## 發佈設定 {#publishing-the-configuration}

MSRP必須識別為所有製作和發佈執行個體上的通用商店。

若要讓相同的設定可在發佈環境中使用，請登入您的製作例項，並遵循步驟：

* 從主功能表導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 復寫]**.
* 選擇 **[!UICONTROL 激活樹]**
* **[!UICONTROL 開始路徑]**:
   * 瀏覽至 `/etc/socialconfig/srpc/`
* 選擇 **[!UICONTROL 啟動]**

## 管理使用者資料 {#managing-user-data}

如需 *使用者*, *使用者設定檔* 和 *使用者群組*，通常會在發佈環境中輸入，請造訪

* [使用者同步](sync.md)
* [管理使用者和使用者群組](users.md)

## MSRP重新索引工具 {#msrp-reindex-tool}

安裝新組態檔或修復損壞的Solr索引時，會出現HTTP端點來重新索引MSRP的Solr。

使用此工具，MongoDB是 *真理* MSRP;只需備份MongoDB即可。

整個UGC樹可以重新編列索引，或者只能依照*path *data參數所指定的特定子樹。

可使用cURL或任何其他HTTP工具從命令列執行此工具。

重新索引時，由*batchSize *data參數控制的記憶體與效能之間有取捨，該參數指定每個批次重新索引的UGC記錄數。

合理的違約為5000:

* 如果記憶體有問題，請指定較小的數字
* 如果速度有問題，請指定較大的數字以增加速度

### 使用cURL命令執行MSRP重新索引工具 {#running-msrp-reindex-tool-using-curl-command}

下列cURL命令顯示HTTP要求對儲存在MSRP中的UGC重新編列索引的必要條件。

基本格式為：

cURL -u *簽入* -d *資料* *reindex-url*

*簽入* = administrator-id:password例如：admin:admin

*資料* = &quot;batchSize=*大小*&amp;path=*路徑*

*大小* =每個操作要重新索引的UGC條目數
`/content/usergenerated/asi/mongo/`

*路徑* =要重新索引的UGC樹的根位置

* 要重新索引所有UGC，請指定 `asipath`屬性
   `/etc/socialconfig/srpc/defaultconfiguration`
* 若要將索引限制為某些UGC，請指定 `asipath`

*reindex-url* = SRP重新索引的端點
`http://localhost:4503/services/social/datastore/mongo/reindex`

>[!NOTE]
>
>如果您 [重新索引DSRP Solr](dsrp.md)，則URL為 **/services/social/datastore/rdb/reindex**

### MSRP重新索引範例 {#msrp-reindex-example}

```shell
curl -s -u admin:admin -d 'batchSize=10000&path=/content/usergenerated/asi/mongo/' http://localhost:4503/services/social/datastore/mongo/reindex
```

## 如何示範MSRP {#how-to-demo-msrp}

若要設定MSRP以供示範或開發環境使用，請參閱 [如何設定演示的MongoDB](demo-mongo.md).

## 疑難排解 {#troubleshooting}

### UGC在MongoDB中不可見 {#ugc-not-visible-in-mongodb}

檢查儲存選項的設定，確認MSRP已設為預設提供者。 依預設，儲存資源提供者為JSRP。

在所有製作和發佈AEM例項上，重新造訪 [儲存配置控制台](srp-config.md) 或檢查AEM存放庫：

* 在JCR中，如果 [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

   * 不包含 [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) 節點，表示儲存提供者為JSRP。
   * 如果srpc節點存在且包含節點 [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration),defaultconfiguration的屬性應將MSRP定義為預設提供者。

### 升級後UGC消失 {#ugc-disappears-after-upgrade}

如果從現有的AEM Communities 6.0網站升級，必須轉換任何先前的UGC，以符合 [SRP](srp.md) 升級至AEM Communities 6.3後的API。

GitHub上提供開放原始碼工具，目的如下：

* [AEM Communities UGC移轉工具](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

移轉工具可自訂，以從舊版AEM社群匯出UGC，匯入至AEM Communities 6.1或更新版本。

### 錯誤 — 未定義欄位提供程式ID {#error-undefined-field-provider-id}

如果日誌中出現以下錯誤，則表示Solr架構檔案配置不正確。

#### JsonMappingException:未定義欄位提供程式id {#jsonmappingexception-undefined-field-provider-id}

```xml
Caused by: com.fasterxml.jackson.databind.JsonMappingException: undefined field provider_id
at com.fasterxml.jackson.databind.ser.DefaultSerializerProvider.serializeValue(DefaultSerializerProvider.java:129)
at com.fasterxml.jackson.databind.ObjectMapper.writeValue(ObjectMapper.java:1819)
at com.adobe.cq.social.scf.core.BaseSocialComponent.toJSONString(BaseSocialComponent.java:196)
... 124 common frames omitted
```

若要解決此錯誤，請依照 [安裝標準MLS](solr.md#installing-standard-mls)，確保：

* XML配置檔案被複製到正確的Solr位置。
* 新配置檔案替換現有配置檔案後，Solr重新啟動。

### MongoDB安全連接失敗 {#secure-connection-to-mongodb-fails}

如果嘗試使MongoDB伺服器的安全連接由於缺少類定義而失敗，則必須更新MongoDB驅動程式包， `mongo-java-driver`，可從公用maven存放庫取得。

1. 從下載驅動程式 [https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar](https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar) (2.13.2版或更新版本)。
1. 將套件組合複製到AEM執行個體的「crx-quickstart/install」資料夾。
1. 重新啟動AEM執行個體。

## 資源 {#resources}

* [AEM與MongoDB](../../help/sites-deploying/aem-with-mongodb.md)
* [MongoDB檔案](https://docs.mongodb.org/)
