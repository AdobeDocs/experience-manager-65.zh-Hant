---
title: MSRP - MongoDB儲存資源提供程式
seo-title: MSRP - MongoDB Storage Resource Provider
description: 設定AEM Communities以將關係資料庫用作其公用儲存
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

當AEM Communities配置為使用MSRP作為其公共儲存時，用戶生成的內容(UGC)可從所有作者和發佈實例訪問，而無需同步或複製。

另請參閱 [SRP選項的特點](working-with-srp.md#characteristics-of-srp-options) 和 [推薦的拓撲](topologies.md)。

## 要求 {#requirements}

* [蒙戈DB](https://www.mongodb.org/):

   * 版本2.6或更高版本
   * 無需配置蒙古語或共用
   * 強烈建議使用 [複製副本集](#mongoreplicaset)
   * 可以在與同一主機上運行，也AEM可以遠程運行

* [阿帕奇索爾](https://lucene.apache.org/solr/):

   * Solr 7.0版
   * Solr需要Java 1.7或更高版本
   * 不需要服務
   * 運行模式選擇：
      * 獨立模式
      * [SolrCloud模式](solr.md#solrcloud-mode) （建議用於生產環境）
   * 選擇多語言搜索(MLS):
      * [安裝標準MLS](solr.md#installing-standard-mls)
      * [安裝高級MLS](solr.md#installing-advanced-mls)

## MongoDB配置 {#mongodb-configuration}

### 選擇MSRP {#select-msrp}

的 [儲存配置控制台](srp-config.md) 允許選擇預設儲存配置，該配置可標識要使用的SRP實現。

在作者中，要訪問「儲存配置」控制台：

* 從全局導航中，選擇 **[!UICONTROL 工具]** > **[!UICONTROL 社區]** > **[!UICONTROL 儲存配置]**。

![msrp](assets/msrp.png)

* 選擇 **[!UICONTROL MongoDB儲存資源提供程式(MSRP)]**
* **[!UICONTROL mongoDB 設定]**

   * **[!UICONTROL mongoDB URI]**

      *預設*:mongodb://localhost/?maxPoolSize=10&amp;waitQueueMultiple=5&amp;readPreference=secondaryPreferred

   * **[!UICONTROL mongoDB 資料庫]**

      *預設*:社區

   * **[!UICONTROL mongoDB UGC 集合]**

      *預設*:內容

   * **[!UICONTROL mongoDB 附件集合]**

      *預設*:附件

* **[!UICONTROL Solr配置]**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Zookeeper Host**

      在 [SolrCloud模式](solr.md#solrcloud-mode) 使用外部ZooKeeper，將此值設定為 `HOST:PORT` 動物園守護者，比如 *my.server.com:2181*

      對於ZooKeeper整合，輸入逗號分隔 `HOST:PORT` 值，如 *host1:2181,host2:2181*

      如果使用內部ZooKeeper以獨立模式運行Solr，請保留空白。
      *預設*: *&lt;blank>*

      * **[!UICONTROL 索爾URL]**
用於在獨立模式下與Solr通信的URL。
如果在SolrCloud模式下運行，請保留為空。

         *預設*:https://127.0.0.1:8983/solr/

      * **[!UICONTROL 索爾集合]**
Solr集合名稱。

         *預設*:集合1

* 選擇 **[!UICONTROL 提交]**

>[!NOTE]
>
>mongoDB資料庫，預設為名稱 `communities`，不應設定為正用於的資料庫的名稱 [節點儲存或資料儲存（二進位）](../../help/sites-deploying/data-store-config.md)。 另請參閱 [6.5中AEM的儲存元素](../../help/sites-deploying/storage-elements-in-aem-6.md)。

### MongoDB複製副本集 {#mongodb-replica-set}

對於生產環境，強烈建議設定複製副本集，即MongoDB伺服器的群集，該群集實現主輔複製和自動故障切換。

要瞭解有關副本集的詳細資訊，請訪問MongoDB [複製](https://docs.mongodb.org/manual/replication/) 文檔。

要使用複製副本集並瞭解如何定義應用程式與MongoDB實例之間的連接，請訪問MongoDB [連接字串URI格式](https://docs.mongodb.org/manual/reference/connection-string/) 文檔。

#### 用於連接到副本集的示例URL  {#example-url-for-connecting-to-a-replica-set}

```shell
# Example url for:
# servers "mongoserver1", "mongoserver2", "mongoserver3"
# replica set 'rs0'
# port numbers only necessary if not default port 27017
mongodb://mongoserver1:<mongoport1>,mongoserver2:<mongoport2>,mongoserver3:<mongoport3>/?replicaSet=rs0&maxPoolSize=100&waitQueueMultiple=50&readPreference=secondaryPreferred
```

## Solr 設定 {#solr-configuration}

通過使用不同集合，節點儲存(Oak)和公共儲存(MSRP)之間可以共用Solr安裝。

如果Oak和MSRP系列都被集中使用，則可能出於效能原因安裝第二個Solr。

對於生產環境， [SolrCloud模式](solr.md#solrcloud-mode) 與獨立模式（單個本地Solr設定）相比，提供了更高的效能。

有關配置詳細資訊，請參閱 [SRP的Solr配置](solr.md)。

### 升級 {#upgrading}

如果從配置有MSRP的早期版本升級，則需要：

1. 執行 [升級到AEM Communities](upgrade.md)
1. 安裝新的Solr配置檔案
   * 對於 [標準MLS](solr.md#installing-standard-mls)
   * 對於 [高級MLS](solr.md#installing-advanced-mls)
1. 重新索引MSRP請參閱一節 [MSRP重新索引工具](#msrp-reindex-tool)

## 發佈配置 {#publishing-the-configuration}

MSRP必須被標識為所有作者和發佈實例上的公用儲存。

要在發佈環境中使相同的配置可用，請登錄到作者實例，然後執行以下步驟：

* 從主菜單導航到 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 複製]**。
* 選擇 **[!UICONTROL 激活樹]**
* **[!UICONTROL 開始路徑]**:
   * 瀏覽到 `/etc/socialconfig/srpc/`
* 選擇 **[!UICONTROL 激活]**

## 管理用戶資料 {#managing-user-data}

有關 *用戶*。 *用戶配置檔案* 和 *用戶組*，通常輸入到發佈環境中，訪問

* [用戶同步](sync.md)
* [管理用戶和用戶組](users.md)

## MSRP重新索引工具 {#msrp-reindex-tool}

在安裝新配置檔案或修復損壞的Solr索引時，有一個HTTP終結點，用於為MSRP重新索引Solr。

使用此工具， MongoDB是 *真* MSRP;只需對MongoDB執行備份。

可以重新索引整個UGC樹，或者只對特定子樹進行索引，如*path *data參數所指定。

此工具可以使用cURL或任何其他HTTP工具從命令行運行。

重新索引時，記憶體與由*batchSize *data參數控制的效能之間存在折中，該參數指定每批重新索引多少個UGC記錄。

合理的預設值為5000:

* 如果記憶體有問題，請指定一個較小的數字
* 如果速度是問題，請指定更大的數字以提高速度

### 使用cURL命令運行MSRP重新索引工具 {#running-msrp-reindex-tool-using-curl-command}

以下cURL命令顯示HTTP請求對儲存在MSRP中的UGC重新編製索引所需的內容。

基本格式為：

cURL -u *簽名* -d *資料* *重新索引URL*

*簽名* = administrator-id:password例如：管理員：管理員

*資料* = &quot;batchSize=*大小*&amp;路徑=*路徑&quot;*

*大小* =每個操作要重新索引的UGC條目數
`/content/usergenerated/asi/mongo/`

*路徑* =要重新索引的UGC樹的根位置

* 要重新索引所有UGC，請指定 `asipath`物業
   `/etc/socialconfig/srpc/defaultconfiguration`
* 要將索引限制到某個UGC，請指定 `asipath`

*重新索引URL* = SRP重新索引的終結點
`http://localhost:4503/services/social/datastore/mongo/reindex`

>[!NOTE]
>
>如果 [重新索引DSRP Solr](dsrp.md), URL為 **/services/social/datastore/rdb/reindex**

### MSRP重新索引示例 {#msrp-reindex-example}

```shell
curl -s -u admin:admin -d 'batchSize=10000&path=/content/usergenerated/asi/mongo/' http://localhost:4503/services/social/datastore/mongo/reindex
```

## 如何演示MSRP {#how-to-demo-msrp}

要為演示或開發環境設定MSRP，請參閱 [如何設定MongoDB以進行演示](demo-mongo.md)。

## 疑難排解 {#troubleshooting}

### UGC在MongoDB中不可見 {#ugc-not-visible-in-mongodb}

通過檢查儲存選項的配置，確保MSRP已配置為預設提供程式。 預設情況下，儲存資源提供程式是JSRP。

在所有作者和發佈AEM實例上，重訪 [儲存配置控制台](srp-config.md) 或檢查存AEM儲庫：

* 在JCR中，如果 [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

   * 不包含 [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) 節點，表示儲存提供程式是JSRP。
   * 如果srpc節點存在並包含節點 [預設配置](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)，預設配置的屬性應將MSRP定義為預設提供程式。

### 升級後UGC消失 {#ugc-disappears-after-upgrade}

如果從現有的AEM Communities6.0站點升級，則必須轉換任何預先存在的UGC，以符合 [SRP](srp.md) 升級到AEM Communities6.3後的API。

GitHub上有一個開源工具可用於此目的：

* [AEM CommunitiesUGC遷移工具](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

可自定義遷移工具，以將UGC從早期版本的社AEM區導出，導入AEM Communities6.1或更高版本。

### 錯誤 — 未定義欄位provider_id {#error-undefined-field-provider-id}

如果日誌中出現以下錯誤，則表明未正確配置Solr架構檔案。

#### JsonMappingException:未定義的欄位提供程式id {#jsonmappingexception-undefined-field-provider-id}

```xml
Caused by: com.fasterxml.jackson.databind.JsonMappingException: undefined field provider_id
at com.fasterxml.jackson.databind.ser.DefaultSerializerProvider.serializeValue(DefaultSerializerProvider.java:129)
at com.fasterxml.jackson.databind.ObjectMapper.writeValue(ObjectMapper.java:1819)
at com.adobe.cq.social.scf.core.BaseSocialComponent.toJSONString(BaseSocialComponent.java:196)
... 124 common frames omitted
```

要解決錯誤，請按照 [安裝標準MLS](solr.md#installing-standard-mls)，確保：

* XML配置檔案已複製到正確的Solr位置。
* 新配置檔案替換現有配置檔案後重新啟動了Solr。

### 到MongoDB的安全連接失敗 {#secure-connection-to-mongodb-fails}

如果由於缺少類定義而嘗試與MongoDB伺服器建立安全連接失敗，則必須更新MongoDB驅動程式包， `mongo-java-driver`，可從公共主資料庫獲得。

1. 從下載驅動程式 [https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar](https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar) (2.13.2版或更高版本)。
1. 將捆綁包複製到實例的「crx-quickstart/install」文AEM件夾。
1. 重新啟動AEM實例。

## 資源 {#resources}

* [帶AEMMongoDB](../../help/sites-deploying/aem-with-mongodb.md)
* [MongoDB文檔](https://docs.mongodb.org/)
