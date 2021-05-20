---
title: MSRP - MongoDB儲存資源提供程式
seo-title: MSRP - MongoDB儲存資源提供程式
description: 設定AEM Communities以使用關係資料庫作為其公用儲存
seo-description: 設定AEM Communities以使用關係資料庫作為其公用儲存
uuid: 9fc06d4f-a60f-4ce3-8586-bcc836aa7de6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 048f7b30-20c3-4567-bd32-38cf2643cf39
role: Administrator
exl-id: 799d5ae1-caac-4c92-8835-696ad25de553
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 1%

---

# MSRP - MongoDB儲存資源提供程式{#msrp-mongodb-storage-resource-provider}

## 關於MSRP {#about-msrp}

當AEM Communities設定為使用MSRP作為其常見存放區時，使用者產生的內容(UGC)可從所有製作和發佈執行個體存取，而無須同步或復寫。

另請參閱[SRP選項的特性](working-with-srp.md#characteristics-of-srp-options)和[建議拓撲](topologies.md)。

## 需求 {#requirements}

* [MongoDB](https://www.mongodb.org/):

   * 2.6版或更高版本
   * 無需配置蒙古或共用
   * 強烈建議使用[複製副本集](#mongoreplicaset)
   * 可在與AEM相同的主機上運行或遠程運行

* [Apache Solr](https://lucene.apache.org/solr/):

   * Solr 7.0版
   * Solr需要Java 1.7或更高版本
   * 不需要任何服務
   * 運行模式的選擇：
      * 獨立模式
      * [SolrCloud模式](solr.md#solrcloud-mode) （建議用於生產環境）
   * 多語言搜尋(MLS)的選擇：
      * [安裝標準MLS](solr.md#installing-standard-mls)
      * [安裝進階MLS](solr.md#installing-advanced-mls)

## MongoDB配置{#mongodb-configuration}

### 選擇MSRP {#select-msrp}

[儲存配置控制台](srp-config.md)允許選擇預設儲存配置，以確定要使用的SRP實施。

在作者上，要訪問儲存配置控制台：

* 從全局導航中，選擇&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 社區]** > **[!UICONTROL 儲存配置]**。

![msrp](assets/msrp.png)

* 選擇&#x200B;**[!UICONTROL MongoDB儲存資源提供程式(MSRP)]**
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

      在[SolrCloud模式](solr.md#solrcloud-mode)中使用外部ZooKeeper運行時，將此值設定為ZooKeeper的`HOST:PORT`，如&#x200B;*my.server.com:2181*

      對於ZooKeeper整體，輸入逗號分隔的`HOST:PORT`值，例如&#x200B;*host1:2181,host2:2181*

      如果使用內部ZooKeeper以獨立模式運行Solr，請保留空白。
      *預設*:  *&lt;blank>*

      * **[!UICONTROL Solr]**
URL用於以獨立模式與Solr通訊的URL。如果在SolrCloud模式中執行，請保留空白。

         *預設*:https://127.0.0.1:8983/solr/

      * **[!UICONTROL Solr集]**
合Solr集合名稱。

         *預設*:集合1

* 選擇&#x200B;**[!UICONTROL 提交]**

>[!NOTE]
>
>預設為名稱`communities`的mongoDB資料庫不應設定為用於[節點儲存或資料（二進位）儲存](../../help/sites-deploying/data-store-config.md)的資料庫的名稱。 另請參閱[AEM 6.5](../../help/sites-deploying/storage-elements-in-aem-6.md)中的儲存元素。

### MongoDB複製副本集{#mongodb-replica-set}

對於生產環境，強烈建議設定一個複製副本集，即實現主次複製和自動故障切換的MongoDB伺服器群集。

要了解有關副本集的更多資訊，請訪問MongoDB的[Replication](https://docs.mongodb.org/manual/replication/)文檔。

要使用副本集並了解如何定義應用程式和MongoDB實例之間的連接，請訪問MongoDB的[連接字串URI格式](https://docs.mongodb.org/manual/reference/connection-string/)文檔。

#### 用於連接到副本集{#example-url-for-connecting-to-a-replica-set}的示例Url

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

對於生產環境，[SolrCloud mode](solr.md#solrcloud-mode)提供了比獨立模式（單個本地Solr設定）更好的效能。

有關配置詳細資訊，請參閱[SRP](solr.md)的Solr配置。

### 升級 {#upgrading}

如果從使用MSRP設定的舊版升級，必須：

1. 執行[升級至AEM Communities](upgrade.md)
1. 安裝新的Solr配置檔案
   * 針對[標準MLS](solr.md#installing-standard-mls)
   * 針對[進階MLS](solr.md#installing-advanced-mls)
1. 重新索引MSRP
請參閱[MSRP重新索引工具](#msrp-reindex-tool)節

## 發佈配置{#publishing-the-configuration}

MSRP必須識別為所有製作和發佈執行個體上的通用商店。

若要讓相同的設定可在發佈環境中使用，請登入您的製作例項，並遵循步驟：

* 從主菜單導航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 複製]**。
* 選擇&#x200B;**[!UICONTROL 激活樹]**
* **[!UICONTROL 開始路徑]**:
   * 瀏覽至`/etc/socialconfig/srpc/`
* 選擇&#x200B;**[!UICONTROL 激活]**

## 管理用戶資料{#managing-user-data}

如需&#x200B;*users*、*user profiles*&#x200B;和&#x200B;*user groups*&#x200B;的相關資訊，通常在發佈環境中輸入，請瀏覽

* [使用者同步](sync.md)
* [管理使用者和使用者群組](users.md)

## MSRP重新索引工具{#msrp-reindex-tool}

安裝新組態檔或修復損壞的Solr索引時，會出現HTTP端點來重新索引MSRP的Solr。

使用此工具，MongoDB是MSRP *truth*&#x200B;的來源；只需備份MongoDB即可。

整個UGC樹可以重新編列索引，或者只能依照*path *data參數所指定的特定子樹。

可使用cURL或任何其他HTTP工具從命令列執行此工具。

重新索引時，由*batchSize *data參數控制的記憶體與效能之間有取捨，該參數指定每個批次重新索引的UGC記錄數。

合理的違約為5000:

* 如果記憶體有問題，請指定較小的數字
* 如果速度有問題，請指定較大的數字以增加速度

### 使用cURL命令{#running-msrp-reindex-tool-using-curl-command}執行MSRP重新索引工具

下列cURL命令顯示HTTP要求對儲存在MSRP中的UGC重新編列索引的必要條件。

基本格式為：

cURL -u *signin* -d *data* *reindex-url*

*signin*  = administrator-id:password例如：admin:admin

*data*  = &quot;batchSize=*size*&amp;path=*path&quot;*

*size*  =每個操作要重新索引的UGC項目數 
`/content/usergenerated/asi/mongo/`

*path*  =要重新索引的UGC樹的根位置

* 要重新索引所有UGC，請指定`asipath`
   `/etc/socialconfig/srpc/defaultconfiguration`
* 若要將索引限制為某些UGC，請指定`asipath`的子樹

*reindex-url*  = SRP重新索引的端點 
`http://localhost:4503/services/social/datastore/mongo/reindex`

>[!NOTE]
>
>如果您是[重新索引DSRP Solr](dsrp.md)，則URL為&#x200B;**/services/social/datastore/rdb/reindex**

### MSRP重新索引範例{#msrp-reindex-example}

```shell
curl -s -u admin:admin -d 'batchSize=10000&path=/content/usergenerated/asi/mongo/' http://localhost:4503/services/social/datastore/mongo/reindex
```

## 如何示範MSRP {#how-to-demo-msrp}

若要針對示範或開發環境設定MSRP，請參閱[HowTo Setup MongoDB for Demo](demo-mongo.md)。

## 疑難排解 {#troubleshooting}

### MongoDB {#ugc-not-visible-in-mongodb}中不顯示UGC

檢查儲存選項的設定，確認MSRP已設為預設提供者。 依預設，儲存資源提供者為JSRP。

在所有製作和發佈AEM例項上，重新造訪[儲存設定控制台](srp-config.md)或檢查AEM存放庫：

* 在JCR中，如果[/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

   * 不包含[srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc)節點，表示儲存提供者為JSRP。
   * 如果srpc節點存在且包含節點[defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration),defaultconfiguration的屬性應將MSRP定義為預設提供程式。

### 升級{#ugc-disappears-after-upgrade}後UGC消失

如果從現有的AEM Communities 6.0網站升級，在升級至AEM Communities 6.3後，必須轉換任何預先存在的UGC，以符合[SRP](srp.md) API所需的結構。

GitHub上提供開放原始碼工具，目的如下：

* [AEM Communities UGC移轉工具](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

移轉工具可自訂，以從舊版AEM社群匯出UGC，匯入至AEM Communities 6.1或更新版本。

### 錯誤 — 未定義的欄位提供程式id {#error-undefined-field-provider-id}

如果日誌中出現以下錯誤，則表示Solr架構檔案配置不正確。

#### JsonMappingException:未定義的欄位提供程式id {#jsonmappingexception-undefined-field-provider-id}

```xml
Caused by: com.fasterxml.jackson.databind.JsonMappingException: undefined field provider_id
at com.fasterxml.jackson.databind.ser.DefaultSerializerProvider.serializeValue(DefaultSerializerProvider.java:129)
at com.fasterxml.jackson.databind.ObjectMapper.writeValue(ObjectMapper.java:1819)
at com.adobe.cq.social.scf.core.BaseSocialComponent.toJSONString(BaseSocialComponent.java:196)
... 124 common frames omitted
```

若要解決此錯誤，請依照[安裝標準MLS](solr.md#installing-standard-mls)的指示，確定：

* XML配置檔案被複製到正確的Solr位置。
* 新配置檔案替換現有配置檔案後，Solr重新啟動。

### MongoDB的安全連接失敗{#secure-connection-to-mongodb-fails}

如果嘗試使MongoDB伺服器的安全連接由於缺少類定義而失敗，則必須更新MongoDB驅動程式包`mongo-java-driver`，該包可從公共Maven儲存庫獲得。

1. 從[https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar](https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar)下載驅動程式(2.13.2版或更新版本)。
1. 將套件組合複製到AEM執行個體的「crx-quickstart/install」資料夾。
1. 重新啟動AEM執行個體。

## 資源 {#resources}

* [AEM與MongoDB](../../help/sites-deploying/aem-with-mongodb.md)
* [MongoDB檔案](https://docs.mongodb.org/)
