---
title: SRP的Solr配置
seo-title: SRP的Solr配置
description: Apache Solr安裝可透過使用不同集合，在節點存放區(Oak)和公用存放區(SRP)之間共用
seo-description: Apache Solr安裝可透過使用不同集合，在節點存放區(Oak)和公用存放區(SRP)之間共用
uuid: 7356343d-073c-4266-bdcb-c7e999281476
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e228f1db-91ea-4ec3-86da-06d89d74bc72
role: Administrator
exl-id: a9fc9c06-b9e6-4a5e-ab5e-0930ecd4b51b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1483'
ht-degree: 2%

---

# SRP {#solr-configuration-for-srp}的Solr配置

## AEM平台解決方案{#solr-for-aem-platform}

[Apache Solr](https://lucene.apache.org/solr/)安裝可在[node store](../../help/sites-deploying/data-store-config.md)(Oak)和[common store](working-with-srp.md)(SRP)之間使用不同集合來共用。

如果Oak和SRP集合都大量使用，可能會基於效能原因安裝第二個Solr。

對於生產環境，[SolrCloud mode](#solrcloud-mode)提供了比獨立模式（單個本地Solr設定）更好的效能。

### 需求 {#requirements}

下載並安裝Apache Solr:

* [7.0版](https://archive.apache.org/dist/lucene/solr/7.0.0/)

* Solr需要Java 1.7或更高版本
* 不需要任何服務
* 運行模式的選擇：

   * 獨立模式
   * [SolrCloud模式](#solrcloud-mode) （建議用於生產環境）

* 多語言搜尋選擇(MLS)

   * [安裝標準MLS](#installing-standard-mls)
   * [安裝進階MLS](#installing-advanced-mls)

## SolrCloud模式{#solrcloud-mode}

[](https://cwiki.apache.org/confluence/display/solr/SolrCloud) 建議將SolrCloudmode用於生產環境。在SolrCloud模式下運行時，必須先安裝並配置SolrCloud，然後才能安裝多語言搜索(MLS)。

建議您按照SolrCloud指示安裝：

* 同一伺服器上的3個SolrCloud節點。
* 外部的Apache ZooKeeper。

還建議配置JVM以優化記憶體使用和垃圾回收。

### JVM配置示例{#jvm-configuration-example}

```shell
JVM_OPTS="-server -Xmx2048m -XX:MaxPermSize=768M -XX:+UseConcMarkSweepGC -XX:+CMSClassUnloadingEnabled -Xloggc:../logs/gc.log -XX:+PrintGCDetails -XX:+PrintGCDateStamps -Djava.awt.headless=true"
```

### SolrCloud安裝命令{#solrcloud-setup-commands}

在SolrCloud模式下運行時，在MLS安裝之前，必須使用並了解以下SolrCloud設定命令。

#### 1.將配置上載到ZooKeeper {#upload-a-configuration-to-zookeeper}

參考資料：
[https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities](https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities)

用法：
sh 。/scripts/cloud-scripts/zkcli.sh \
-cmd upconfig \
-zkhost *server:port* \
-confname *myconfig-name *\
-solrhome *solr-home-path* \
-confdir *config-dir*

#### 2.建立集合{#create-a-collection}

參考資料：
[https://cwiki.apache.org/confluence/display/solr/Solr+Start+Script+Reference#SolrStartScriptReference-Create](https://cwiki.apache.org/confluence/display/solr/Solr+Start+Script+Reference#SolrStartScriptReference-Create)

使用狀況:
./bin/solr建立 \
-c *mycollection-name*\
-d *config-dir* \
-n *myconfig-name* \
-p *port*\
-s *number-of-shards&lt;a1/* \
-rf *number-of-replicas*

#### 3.將集合連結到配置集{#link-a-collection-to-a-configuration-set}

將集合連結到已上載到ZooKeeper的配置。

參考資料：
[https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities](https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities)

用法：
sh 。/scripts/cloud-scripts/zkcli.sh \
-cmd linkconfig \
-zkhost *server:port* \
-collection *mycollection-name* \
-confname *myconfig-name*

### 標準與高級MLS {#comparison-of-standard-and-advanced-mls}的比較

AEM Communities的多語言搜尋(MLS)是為Solr平台所建置，可改善所有支援語言（包括英文）的搜尋。

AEM社群的MLS可作為標準MLS或進階MLS使用。 標準MLS僅包含Solr組態設定，並排除任何外掛程式或資源檔案。 進階MLS是更全面的解決方案，包含Solr組態設定、外掛程式和相關資源

標準MLS包含下列語言的內容搜尋增強功能：

* 英語：改善嘗試比對字詞衍生的靜態。
* 日文：改善半形字元的日文Token化。

進階MLS包含下列語言的內容搜尋增強功能：

* 英語：用旅鼠器取代了司機。
* 德文：已新增解壓縮程式。
* 法語：已新增條件處理。
* 簡體中文：新增更聰明的Tokenizer。
* 各種語言：新增調整器、停止字詞清單和正規化程式。

進階MLS支援下列33種語言。

| 阿拉伯文 | 德文 | 挪威文 |
|---|---|---|
| 保加利亞文 | 希臘文 | 波蘭文 |
| 中文 (簡體) | 海地克里奧爾 | 葡萄牙文 |
| 繁體中文 | 希伯來文 | 羅馬尼亞文 |
| 捷克文 | 匈牙利文 | 俄文 |
| 丹麥文 | 印尼語 | 斯洛伐克文 |
| 荷蘭文 | 義大利文 | 斯洛文尼亞文 |
| 英文 | 日文 | 西班牙文 |
| 愛沙尼亞文 | 韓文 | 瑞典文 |
| 芬蘭文 | 拉脫維亞文 | 泰語 |
| 法文 | 立陶宛文 | 土耳其文 |

#### AEM 6.1 Solr搜尋、標準MLS和進階MLS {#comparison-of-aem-solr-search-standard-mls-and-advanced-mls}的比較

**注意**:AEM 6.1是指AEM 6.1 Communities FP3及舊版。

![compare-solr-mls](assets/compare-solr-mls.png)

### 安裝標準MLS {#installing-standard-mls}

為了收集SRP（MSRP或DSRP），為支援標準多語言搜索(MLS)，必須修改Solr的兩個配置檔案：

* **schema.xml**
* **solrconfig.xml**

適用於Solr 4.10的標準MLS檔案(schema.xml、solrconfig.xml)。

適用於Solr 5.x的標準MLS檔案(schema.xml、solrconfig.xml)。

標準MLS檔案會儲存在AEM存放庫中。

**注意**:Solr檔案儲存在msrp/資料夾中，但也用於DSRP（不需要變更）。

**下載指示**:視 `solrX` 情況 `solr4` 將 `solr5` 取代為或。

1. 使用CRXDE|Lite，查找：

   * `/libs/social/config/datastore/msrp/solrX/schema.xml`
   * `/libs/social/config/datastore/msrp/solrX/solrconfig.xml`

1. 下載到部署Solr的本地伺服器。

   * 找到`jcr:content`節點的`jcr:data`屬性。
   * 選擇`view`以開始下載。
   * 請確定檔案的名稱和編碼皆為適當(UTF8)。

1. 按照獨立模式或SolrCloud模式的安裝說明操作。

#### SolrCloud模式 — 標準MLS {#solrcloud-mode-standard-mls}

1. 在SolrCloud模式下安裝和配置Solr。
1. 準備新配置：

   1. 建立new-config-dir*，如`solr-install-dir*/myconfig/`

   1. 將現有Solr配置目錄的內容複製到&#x200B;*new-config-dir*

      * 對於Solr4:複製`solr-install-dir/example/solr/collection1/conf/`
      * 對於Solr5:複製`solr-install-dir/server/solr/configsets/data_driven_schema_configs/`
   1. 將下載的&#x200B;**schema.xml**&#x200B;和&#x200B;**solrconfig.xml**&#x200B;複製到&#x200B;*new-config-dir*&#x200B;以覆寫現有檔案。


1. [將新配置上](#upload-a-configuration-to-zookeeper) 載到ZooKeeper。
1. [建立一](#create-a-collection) 個集合，指定必要的參數，如分片數、副本數和配置名。
1. 如果在建立集合期間未*提供配置名稱，則[將此新建立的集合](#link-a-collection-to-a-configuration-set)與上載到ZooKeeper的配置連結。

1. 若為MSRP，請執行[MSRP重新索引工具](msrp.md#msrp-reindex-tool)，除非這是新安裝。

#### 獨立模式 — 標準MLS {#standalone-mode-standard-mls}

1. 以獨立模式安裝Solr。
1. 如果運行Solr5，請建立集合1（類似於Solr4）:

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

1. 在Solr配置目錄中備份&#x200B;**schema.xml**&#x200B;和&#x200B;**solrconfig.xml**，例如：

   * 對於Solr4:`solr-install-dir/example/solr/collection1/conf/`
   * 為Solr5建立：`solr-install-dir/server/solr/collection1/conf/`

1. 將下載的&#x200B;**schema.xml**&#x200B;和&#x200B;**solrconfig.xml**&#x200B;複製到同一目錄。

1. 重新啟動Solr。
1. 若為MSRP，請執行[MSRP重新索引工具](#msrpreindextool)，除非這是新安裝。

### 安裝高級MLS {#installing-advanced-mls}

為了支援進階MLS,SRP收集（MSRP或DSRP），除了自訂結構和Solr組態外，還需要新的Solr外掛程式。 所有必要項目都封裝成可下載的zip檔案。 此外，還包括安裝指令碼，以便在獨立模式部署Solr時使用。

若要取得進階MLS套件，請參閱檔案部署區段中的[AEM進階MLS](deploy-communities.md#aem-advanced-mls) 。

要開始安裝SolrCloud或獨立模式，請執行以下操作：

* 將AEM-SOLR-MLS zip封存下載至托管Solr的伺服器。
* 拆開封存檔。

#### SolrCloud模式 — 高級MLS {#solrcloud-mode-advanced-mls}

安裝說明 — 注意Solr4和Solr5的幾項差異：

1. 在SolrCloud模式下安裝和配置Solr。
1. 將進階MLS套件的內容解壓縮至磁碟。 內容包括：

   * **schema.xml**
   * **solrconfig.xml**
   * **秒數/資** 料夾
   * **設定檔/資** 料夾
   * **extra-libs/資** 料夾

1. 準備新配置：

   1. 建立&#x200B;*new-config-dir*

      * 例如`solr-install-dir/myconfig/`
      * 建立子資料夾`stopwords/`和`lang/`
   1. 將現有Solr配置目錄的內容複製到&#x200B;*new-config-dir*

      * 對於Solr4:複製`solr-install-dir/example/solr/collection1/conf/`
      * 對於Solr5:複製`solr-install-dir/server/solr/configsets/data_driven_schema_configs/`
   1. 將擷取的&#x200B;**schema.xml**&#x200B;和&#x200B;**solrconfig.xml**&#x200B;複製到&#x200B;*new-config-dir*&#x200B;以覆寫現有檔案。
   1. 對於Solr5:將`solr_install_dir/server/solr/configsets/sample_techproducts_configs/conf/lang/*.txt`複製到`new-config-dir/lang/`
   1. 將擷取的&#x200B;**stopwords/**&#x200B;資料夾複製至&#x200B;*new-config-dir*，產生`new-config-dir/stopwords/*.txt`



1. [將新設定上](#upload-a-configuration-to-zookeeper) 傳至ZooKeeper
1. 複製新的&#x200B;**profiles/**&#x200B;資料夾……

   * 對於Solr4:複製到每個節點的資源/資料夾
   * 對於Solr5:複製到每個Solr安裝的伺服器/資源/資料夾。 如果所有節點都在同一個Solr安裝目錄中，則此步驟僅執行一次。

1. 在solr-home目錄（包含solr.xml）中，為SolrCloud中的每個節點建立&#x200B;**lib/**&#x200B;資料夾。 將jar從以下位置複製到每個節點上的新lib/資料夾：

   * **從進階MLS套** 件中擷取的額外libs/
   * *solr-install-dir/contrib/extraction/lib/* jar
   * *solr-install-dir/dist/solr-cell*.jar
   * *solr-install-dir/contrib/clustering/lib/* jar
   * *solr-install-dir/dist/solr-clustering*.jar
   * *solr-install-dir/contribut/langid/lib/* jar
   * *solr-install-dir/dist/solr-langid*.jar
   * *solr-install-dir/contrib/velocity/lib/* jar
   * *solr-install-dir/dist/solr-velocity*.jar
   * *solr-install-dir/contrib/analysis-extras/lib/* jar
   * *solr install-dir/contrib/analysis-extras/lucene-libs/* jar

1. [建立一](#create-a-collection) 個集合，指定必要的參數，如分片數、副本數和配置名。
1. 如果在建立集合期間提供的配置名稱為&#x200B;*not*，則[將此新建立的集合](#link-a-collection-to-a-configuration-set)與上載到ZooKeeper的配置連結。

1. 若為MSRP，請執行[MSRP重新索引工具](#msrpreindextool)，除非這是新安裝。

#### 獨立模式 — 高級MLS {#standalone-mode-advanced-mls}

進階MLS套件中包含安裝指令碼。

將軟體包的內容提取到托管獨立Solr伺服器的伺服器後，只需執行安裝指令碼即可安裝必要的資源和配置檔案。

* 以獨立模式安裝Solr。
* 如果運行Solr5，請建立集合1（類似於Solr4）:

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

* 運行安裝指令碼：安裝[-v 4|5] [-d solhome] [-c集合路徑]
其中：

   * -d索爾赫姆

      Solr安裝目錄

   * -c集合路徑

      索爾中的收集路徑

   * --說明

      打印命令行選項

   * -v [4|5]

      為solr設定版本

* Solr 4.10.4的示例：

   * Install.bat -v 4 -d c:/solr-4.10.4 -c:/solr-4.10.4/example/solr/collection1

* Solr 5.4.0的示例：

   * Install.sh -v 5 -d /tmp/solr-5.4.0 -c /tmp/solr-5.4.0/server/solr/collection1

**注意**:

* 安裝指令碼將先備份schema.xml和solrconfig.xml，然後再通過附加「.orig」來安裝新版本

### 關於solrconfig.xml {#about-solrconfig-xml}

**solrconfig.xml**&#x200B;檔案控制自動提交間隔和搜索可見性，需要測試和調整。

`<autoCommit>`:預設情況下， AutoCommit時間間隔（硬提交到穩定儲存）設定為15秒。搜索可見性預設為使用預提交索引。

要更改搜索以使用更新的索引來反映由於提交而發生的更改，請將包含的`openSearcher`更改為true。

`autoSoftCommit`:「軟」提交可確保更改可見（索引已更新），但不確保更改同步到穩定儲存（硬提交）。結果是效能的改善。 預設情況下，`autoSoftCommit`被禁用，包含的`maxTime`設定為–1。
