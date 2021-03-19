---
title: MSRP - MongoDB儲存資源提供程式
seo-title: MSRP - MongoDB儲存資源提供程式
description: 設定AEM Communities以使用關係資料庫作為其公共儲存
seo-description: 設定AEM Communities以使用關係資料庫作為其公共儲存
uuid: 9fc06d4f-a60f-4ce3-8586-bcc836aa7de6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 048f7b30-20c3-4567-bd32-38cf2643cf39
role: 管理員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# MSRP - MongoDB儲存資源提供程式{#msrp-mongodb-storage-resource-provider}

## 關於MSRP {#about-msrp}

將AEM Communities配置為使用MSRP作為其公共儲存時，用戶生成的內容(UGC)可從所有作者和發佈實例訪問，而無需同步或複製。

另請參見[SRP選項的特性](working-with-srp.md#characteristics-of-srp-options)和[建議拓撲](topologies.md)。

## 要求{#requirements}

* [MongoDB](https://www.mongodb.org/):

   * 2.6版或更新版本
   * 無需配置蒙古檔案或共用
   * 強烈建議使用[複製副本集](#mongoreplicaset)
   * 可在與同一台主機上運行AEM或遠程運行

* [Apache Solr](https://lucene.apache.org/solr/):

   * Solr 7.0版
   * Solr需要Java 1.7或更新版本
   * 無需服務
   * 運行模式選擇：
      * 獨立模式
      * [SolrCloud模式](solr.md#solrcloud-mode) （建議用於生產環境）
   * 多語言搜尋(MLS)選擇：
      * [安裝標準MLS](solr.md#installing-standard-mls)
      * [安裝進階MLS](solr.md#installing-advanced-mls)

## MongoDB配置{#mongodb-configuration}

### 選擇MSRP {#select-msrp}

[儲存配置控制台](srp-config.md)允許選擇預設儲存配置，該配置標識要使用的SRP實施。

在作者中，要訪問儲存配置控制台：

* 在全局導航中，選擇&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 社區]** > **[!UICONTROL 儲存配置]**。

![msrp](assets/msrp.png)

* 選擇&#x200B;**[!UICONTROL MongoDB儲存資源提供程式(MSRP)]**
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

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Zookeeper Host**

      在具有外部ZooKeeper的[SolrCloud模式](solr.md#solrcloud-mode)中運行時，將此值設定為ZooKeeper的`HOST:PORT`，如&#x200B;*my.server.com:2181*

      對於ZooKeeper Ensemble，輸入逗號分隔的`HOST:PORT`值，例如&#x200B;*host1:2181,host2:2181*

      如果使用內部ZooKeeper在獨立模式下執行Solr，請保留空白。
      *預設值*:  *&lt;blank>*

      * **[!UICONTROL Solr]**
URL用於在獨立模式下與Solr通訊的URL。如果在SolrCloud模式中執行，請留空。

         *預設值*:https://127.0.0.1:8983/solr/

      * **[!UICONTROL Solr]**
CollectionSolr系列名稱。

         *預設值*:collection1

* 選擇&#x200B;**[!UICONTROL 提交]**

>[!NOTE]
>
>預設為名稱`communities`的mongoDB資料庫不應設定為用於[節點儲存或資料（二進位）儲存](../../help/sites-deploying/data-store-config.md)的資料庫的名稱。 另請參見6.5](../../help/sites-deploying/storage-elements-in-aem-6.md)中AEM的[儲存元素。

### MongoDB複製副本集{#mongodb-replica-set}

對於生產環境，強烈建議設定複製副本集，即實施主次複製和自動故障切換的MongoDB伺服器群集。

要瞭解有關複製副本集的更多資訊，請訪問MongoDB的[Replication](https://docs.mongodb.org/manual/replication/)文檔。

要使用複製副本集並瞭解如何定義應用程式與MongoDB實例之間的連接，請訪問MongoDB的[連接字串URI格式](https://docs.mongodb.org/manual/reference/connection-string/)文檔。

#### 用於連接到複製副本集{#example-url-for-connecting-to-a-replica-set}的示例Url

```shell
# Example url for:
# servers "mongoserver1", "mongoserver2", "mongoserver3"
# replica set 'rs0'
# port numbers only necessary if not default port 27017
mongodb://mongoserver1:<mongoport1>,mongoserver2:<mongoport2>,mongoserver3:<mongoport3>/?replicaSet=rs0&maxPoolSize=100&waitQueueMultiple=50&readPreference=secondaryPreferred
```

## Solr 設定 {#solr-configuration}

Solr安裝可以通過使用不同的集合在節點儲存(Oak)和公共儲存(MSRP)之間共用。

如果Oak和MSRP系列都已大量使用，則可能會因效能原因安裝第二個Solr。

對於生產環境，[SolrCloud模式](solr.md#solrcloud-mode)可改善獨立模式（單一本機Solr設定）的效能。

有關配置詳細資訊，請參閱[ SRP](solr.md)的Solr配置。

### 升級{#upgrading}

如果從使用MSRP設定的舊版進行升級，則必須：

1. 執行[升級至AEM Communities](upgrade.md)
1. 安裝新的Solr配置檔案
   * 對於[標準MLS](solr.md#installing-standard-mls)
   * 對於[進階MLS](solr.md#installing-advanced-mls)
1. 重新索引MSRP
請參閱[MSRP重新索引工具](#msrp-reindex-tool)節

## 發佈配置{#publishing-the-configuration}

MSRP必須被識別為所有作者和發佈例項上的公用商店。

若要在發佈環境中提供相同的設定，請登入您的作者例項，然後依照下列步驟進行：

* 從主菜單導航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 複製]**。
* 選擇&#x200B;**[!UICONTROL 激活樹]**
* **[!UICONTROL 開始路徑]**:
   * 瀏覽至`/etc/socialconfig/srpc/`
* 選擇&#x200B;**[!UICONTROL 激活]**

## 管理用戶資料{#managing-user-data}

有關通常在發佈環境中輸入的&#x200B;*用戶*、*用戶配置檔案*&#x200B;和&#x200B;*用戶組*&#x200B;的資訊，請訪問

* [用戶同步](sync.md)
* [管理使用者和使用者群組](users.md)

## MSRP重新索引工具{#msrp-reindex-tool}

在安裝新配置檔案或修復損壞的Solr索引時，有一個HTTP端點用於為MSRP的Solr重新編製索引。

使用此工具，MongoDB是MSRP *truth*&#x200B;的源；只需對MongoDB執行備份。

整個UGC樹可以重新編製索引，或僅對*path *data參數指定的特定子樹進行索引。

此工具可使用cURL或任何其他HTTP工具從命令列執行。

在重新建立索引時，由*batchSize *data參數控制的記憶體與效能之間會進行權衡，此參數指定每批重新建立UGC記錄的數目。

合理的違約為5000:

* 如果記憶體有問題，請指定較小的數字
* 如果速度是問題，請指定較大的數目以增加速度

### 使用cURL命令{#running-msrp-reindex-tool-using-curl-command}執行MSRP重新索引工具

以下cURL命令顯示HTTP要求重新索引儲存在MSRP中的UGC的必要項。

基本格式為：

cURL -u *signin* -d *data* *reindex-url*

*signin* = administrator-id:password例如：admin:admin

*data* = &quot;batchSize=*size*&amp;path=*path&quot;*

*size* =每個操作要重新索引的UGC條目數 
`/content/usergenerated/asi/mongo/`

*path* = UGC樹的根位置以重新索引

* 若要重新索引所有UGC，請指定`asipath`
   `/etc/socialconfig/srpc/defaultconfiguration`
* 要將索引限制到某些UGC，請指定`asipath`的子樹

*reindex-url* = SRP重新索引的端點 
`http://localhost:4503/services/social/datastore/mongo/reindex`

>[!NOTE]
>
>如果您[重新索引DSRP Solr](dsrp.md)，則URL為&#x200B;**/services/social/datastore/rdb/reindex**

### MSRP重新索引示例{#msrp-reindex-example}

```shell
curl -s -u admin:admin -d 'batchSize=10000&path=/content/usergenerated/asi/mongo/' http://localhost:4503/services/social/datastore/mongo/reindex
```

## 如何演示MSRP {#how-to-demo-msrp}

要為演示或開發環境設定MSRP，請參閱[如何設定演示的MongoDB](demo-mongo.md)。

## 疑難排解 {#troubleshooting}

### UGC在MongoDB {#ugc-not-visible-in-mongodb}中不可見

請檢查儲存選項的設定，以確定MSRP已設定為預設提供者。 預設情況下，儲存資源提供方是JSRP。

在所有作者和發AEM布實例上，請重新訪問[儲存配置控制台](srp-config.md)或檢查存AEM儲庫：

* 在JCR中，如果[/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

   * 不包含[srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc)節點，表示儲存提供程式是JSRP。
   * 如果srpc節點存在並包含節點[defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)，則defaultconfiguration的屬性應將MSRP定義為預設提供程式。

### 升級{#ugc-disappears-after-upgrade}後UGC消失

如果從現有的AEM Communities6.0站點升級，則必須轉換任何預先存在的UGC，以符合升級至AEM Communities6.3後的[SRP](srp.md) API所需的結構。

GitHub上提供開放原始碼工具，可用於：

* [AEM CommunitiesUGC移轉工具](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

可自訂移轉工具，從舊版社交社群匯出UGCAEM，以匯入AEM Communities6.1或更新版本。

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

要解決錯誤，請按照[安裝標準MLS](solr.md#installing-standard-mls)的說明，確保：

* XML配置檔案被複製到正確的Solr位置。
* 在新配置檔案替換現有配置檔案後，Solr重新啟動。

### 與MongoDB的安全連接失敗{#secure-connection-to-mongodb-fails}

如果嘗試與MongoDB伺服器建立安全連接時由於缺少類定義而失敗，則需要更新MongoDB驅動程式包`mongo-java-driver`（可從公共主儲存庫獲得）。

1. 從[https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar](https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar)（2.13.2版或更新版本）下載驅動程式。
1. 將包複製到實例的「crx-quickstart/install」資料夾AEM中。
1. 重新啟動AEM實例。

## 資源 {#resources}

* [使AEM用MongoDB](../../help/sites-deploying/aem-with-mongodb.md)
* [MongoDB檔案](https://docs.mongodb.org/)

