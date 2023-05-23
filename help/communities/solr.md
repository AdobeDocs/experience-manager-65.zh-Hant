---
title: SRP的Solr配置
seo-title: Solr Configuration for SRP
description: 通過使用不同的集合，可以在節點儲存(Oak)和公共儲存(SRP)之間共用Apache Solr安裝
seo-description: An Apache Solr installation may be shared between the node store (Oak) and common store (SRP) by using different collections
uuid: 7356343d-073c-4266-bdcb-c7e999281476
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e228f1db-91ea-4ec3-86da-06d89d74bc72
role: Admin
exl-id: a9fc9c06-b9e6-4a5e-ab5e-0930ecd4b51b
source-git-commit: ce6d24e53a27b64a5d0a9db2e4b6672bd77cf9ec
workflow-type: tm+mt
source-wordcount: '1424'
ht-degree: 2%

---

# SRP的Solr配置 {#solr-configuration-for-srp}

## 面向平台AEM的Solr {#solr-for-aem-platform}

安 [阿帕奇索爾](https://solr.apache.org/) 安裝可在 [節點儲存](../../help/sites-deploying/data-store-config.md) （橡木）和 [普通商店](working-with-srp.md) (SRP)。

如果Oak和SRP集合都被集中使用，則可能出於效能原因安裝第二個Solr。

對於生產環境， [SolrCloud模式](#solrcloud-mode) 與獨立模式（單個本地Solr設定）相比，提供了更高的效能。

### 要求 {#requirements}

下載並安裝Apache Solr:

* [7.0版](https://archive.apache.org/dist/lucene/solr/7.0.0/)

* Solr需要Java™ 1.7或更高版本
* 不需要服務
* 運行模式選擇：

   * 獨立模式
   * [SolrCloud模式](#solrcloud-mode) （建議用於生產環境）

* 多語言搜索(MLS)選擇

   * [安裝標準MLS](#installing-standard-mls)
   * [安裝高級MLS](#installing-advanced-mls)

## SolrCloud模式 {#solrcloud-mode}

[索爾雲](https://solr.apache.org/guide/6_6/solrcloud.html) 建議在生產環境中使用模式。 在SolrCloud模式下運行時，必須先安裝並配置SolrCloud，然後才能安裝多語言搜索(MLS)。

建議按照SolrCloud說明安裝：

* 同一伺服器上的3個SolrCloud節點。
* 外部Apache ZooKeeper。

還建議將JVM配置為調整記憶體使用和垃圾回收。

### JVM配置示例 {#jvm-configuration-example}

```shell
JVM_OPTS="-server -Xmx2048m -XX:MaxPermSize=768M -XX:+UseConcMarkSweepGC -XX:+CMSClassUnloadingEnabled -Xloggc:../logs/gc.log -XX:+PrintGCDetails -XX:+PrintGCDateStamps -Djava.awt.headless=true"
```

### SolrCloud設定命令 {#solrcloud-setup-commands}

在SolrCloud模式下運行時，在MLS安裝、使用和瞭解以下SolrCloud設定命令之前，是必要的。

#### 1。將配置上載到ZooKeeper {#upload-a-configuration-to-zookeeper}

參考：
[https://solr.apache.org/guide/6_6/command-line-utilities.html](https://solr.apache.org/guide/6_6/command-line-utilities.html)

用法：噓。/scripts/cloud-scripts/zkcli.sh \
-cmd upconfig \
-zkhost *伺服器：埠* \
-confname *myconfig name *\
-solhome *索爾 — 主路徑* \
-confdir *配置目錄*

#### 2.建立集合 {#create-a-collection}

參考：
[https://solr.apache.org/guide/6_6/solr-control-script-reference.html#SolrControlScriptReference-Create](https://solr.apache.org/guide/6_6/solr-control-script-reference.html#SolrControlScriptReference-Create)

使用狀況:
./bin/solr建立 \
-c *mycollection名稱*\
-d *配置目錄* \
-n *myconfig名稱* \
-p *埠*\
-s *碎片數* \
-rf *副本數*

#### 3.將集合連結到配置集 {#link-a-collection-to-a-configuration-set}

將集合連結到已上載到ZooKeeper的配置。

參考：
[https://solr.apache.org/guide/6_6/command-line-utilities.html](https://solr.apache.org/guide/6_6/command-line-utilities.html)

用法：噓。/scripts/cloud-scripts/zkcli.sh \
-cmd連結配置 \
-zkhost *伺服器：埠* \
 — 集合 *mycollection名稱* \
-confname *myconfig名稱*

### 標準MLS與先進MLS的比較 {#comparison-of-standard-and-advanced-mls}

針對AEM Communities的多語言搜索(MLS)是為索爾平台而構建的，旨在提供所有支援語言（包括英語）的改進搜索。

AEM Communities的MLS可以作為標準MLS或高級MLS提供。 標準MLS僅包括Solr配置設定，並排除任何插件或資源檔案。 高級MLS是更全面的解決方案，包括Solr配置設定以及插件和相關資源

標準MLS包括以下語言的內容搜索功能增強：

* 英語：用於嘗試匹配字導子的改進的Stemmer。
* 日語：對半形字元的日文標籤化進行了改進。

高級MLS包括以下語言的內容搜索功能增強：

* 英語：用旅鼠替換了司機。
* 德語：已添加解碼器。
* 法語：已添加刪除處理。
* 中文（簡體）:已添加更智慧的標籤器。
* 各種語言：已添加一個修整器、停止字清單和正常化器。

總之，高級MLS支援以下33種語言。

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

#### 6.AEM1 Solr搜索、標準MLS和高級MLS的比較 {#comparison-of-aem-solr-search-standard-mls-and-advanced-mls}

**注釋**:AEM6.1指AEM6.1社區FP3及更早版本。

![比較 — solr-mls](assets/compare-solr-mls.png)

### 安裝標準MLS {#installing-standard-mls}

對於SRP集合（MSRP或DSRP），要支援標準多語言搜索(MLS)，必須修改Solr的兩個配置檔案：

* **schema.xml**
* **solrconfig.xml**

用於Solr 4.10的標準MLS檔案(schema.xml、solrconfig.xml)。

用於Solr 5.x的標準MLS檔案(schema.xml、solrconfig.xml)。

標準MLS檔案儲存在儲存AEM庫中。

**注釋**:Solr檔案儲存在msrp/資料夾中，但它們也用於DSRP（無需更改）。

**下載說明**:替換 `solrX` 與 `solr4` 或 `solr5` 視情況而定。

1. 使用CRXDE|Lite，找到：

   * `/libs/social/config/datastore/msrp/solrX/schema.xml`
   * `/libs/social/config/datastore/msrp/solrX/solrconfig.xml`

1. 下載到部署Solr的本地伺服器。

   * 查找 `jcr:content` 節點 `jcr:data` 屬性。
   * 要開始下載，請選擇 `view`。
   * 確保檔案以適當的名稱和編碼(UTF8)保存。

1. 按照獨立模式或SolrCloud模式的安裝說明進行操作。

#### SolrCloud模式 — 標準MLS {#solrcloud-mode-standard-mls}

1. 在SolrCloud模式下安裝和配置Solr。
1. 準備新配置：

   1. 建立new-config-dir*，如 `solr-install-dir*/myconfig/`

   1. 將現有Solr配置目錄的內容複製到 *新配置目錄*

      * 對於Solr4:複製 `solr-install-dir/example/solr/collection1/conf/`
      * 對於Solr5:複製 `solr-install-dir/server/solr/configsets/data_driven_schema_configs/`
   1. 複製下載的 **schema.xml** 和 **solrconfig.xml** 至 *新配置目錄* 以覆蓋現有檔案。


1. [上載新配置](#upload-a-configuration-to-zookeeper) 去動物園守護者。
1. [建立集合](#create-a-collection) 指定必要的參數，如分片數、副本數和配置名稱。
1. 如果在建立集合期間未提供*配置名稱， [連結新建立的集合](#link-a-collection-to-a-configuration-set) 上載到ZooKeeper的配置。

1. 對於MSRP，運行 [MSRP重新索引工具](msrp.md#msrp-reindex-tool)，除非此安裝是新安裝。

#### 獨立模式 — 標準MLS {#standalone-mode-standard-mls}

1. 在獨立模式下安裝Solr。
1. 如果運行Solr5，請建立集合1（與Solr4類似）:

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

1. 備份 **schema.xml** 和 **solrconfig.xml** 在Solr配置目錄中，例如：

   * 對於Solr4: `solr-install-dir/example/solr/collection1/conf/`
   * 為Solr5建立： `solr-install-dir/server/solr/collection1/conf/`

1. 複製下載的 **schema.xml** 和 **solrconfig.xml** 到同一目錄。

1. 重新啟動Solr。
1. 對於MSRP，運行 [MSRP重新索引工具](#msrpreindextool)，除非此安裝是新安裝。

### 安裝高級MLS {#installing-advanced-mls}

為了支援高級MLS,SRP集合（MSRP或DSRP）需要除自定義架構和Solr配置外還需要新的Solr插件。 所有必需項都打包到可下載的zip檔案中。 此外，在以獨立模式部署Solr時，還會包含安裝指令碼。

要獲取高級MLS包，請參見 [高AEM級MLS](deploy-communities.md#aem-advanced-mls) 中。

要開始安裝SolrCloud或獨立模式，請：

* 下載AEM-SOLR-MLS zip存檔到承載Solr的伺服器。
* 解壓縮存檔。

#### SolrCloud模式 — 高級MLS {#solrcloud-mode-advanced-mls}

安裝說明 — 注意Solr4和Solr5的幾點不同：

1. 在SolrCloud模式下安裝和配置Solr。
1. 將高級MLS包的內容解壓到磁碟。 內容應包括：

   * **schema.xml**
   * **solrconfig.xml**
   * **非字詞/** 資料夾
   * **配置檔案/** 資料夾
   * **額外libs/** 資料夾

1. 準備新配置：

   1. 建立 *新配置目錄*

      * 例如 `solr-install-dir/myconfig/`
      * 建立子資料夾 `stopwords/` 和 `lang/`
   1. 將現有Solr配置目錄的內容複製到 *新配置目錄*

      * 對於Solr4:複製 `solr-install-dir/example/solr/collection1/conf/`
      * 對於Solr5:複製 `solr-install-dir/server/solr/configsets/data_driven_schema_configs/`
   1. 複製提取的 **schema.xml** 和 **solrconfig.xml** 至 *新配置目錄* 以覆蓋現有檔案。
   1. 對於Solr5:複製 `solr_install_dir/server/solr/configsets/sample_techproducts_configs/conf/lang/*.txt` 至 `new-config-dir/lang/`
   1. 複製提取的 **非字詞/** 資料夾 *新配置目錄* 導致 `new-config-dir/stopwords/*.txt`



1. [上載新配置](#upload-a-configuration-to-zookeeper) 到動物園守護者
1. 複製新 **配置檔案/** 資料夾……

   * 對於Solr4:複製到每個節點的資源/資料夾
   * 對於Solr5:複製到每個Solr安裝的伺服器/資源/資料夾。 如果所有節點都位於同一Solr安裝目錄中，則此步驟僅執行一次。

1. 建立 **lib/** solrCloud中每個節點的solr-home目錄（包含solr.xml）中的資料夾。 將jar從以下位置複製到每個節點上的新lib/資料夾：

   * **額外libs/** 從高級MLS包中提取
   * *solr install-dir/contb/extraction/lib/*.jar
   * *solr-install-dir/dist/solr-cell*.jar
   * *solr install-dir/contrub/clustering/lib/*.jar
   * *solr-install-dir/dist/solr-clustering*.jar
   * *solr install-dir/contrib/langid/lib/*.jar
   * *solr-install-dir/dist/solr-langid*.jar
   * *solr install-dir/contrb/velocity/lib/*.jar
   * *solr-install-dir/dist/solr-velocity*.jar
   * *solr install-dir/contrib/analysis-extras/lib/*.jar
   * *solr install-dir/contrib/analysis-extras/lucene-libs/*.jar

1. [建立集合](#create-a-collection) 指定必要的參數，如分片數、副本數和配置名稱。
1. 如果配置名 *不* 在收藏時提供， [連結新建立的集合](#link-a-collection-to-a-configuration-set) 上載到ZooKeeper的配置。

1. 對於MSRP，運行 [MSRP重新索引工具](#msrpreindextool)，除非此安裝是新安裝。

#### 獨立模式 — 高級MLS {#standalone-mode-advanced-mls}

高級MLS包中包含安裝指令碼。

將包內容解壓到托管獨立Solr伺服器的伺服器後，運行安裝指令碼以安裝必要的資源和配置檔案。

* 在獨立模式下安裝Solr。
* 如果運行Solr5，請建立集合1（與Solr4類似）:

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

* 運行安裝指令碼：安裝 [-v 4|5] [-d索爾霍姆] [-c集合路徑]
其中：

   * -d索爾霍姆

      Solr安裝目錄

   * -c集合路徑

      索爾中的集合路徑

   * --說明

      打印命令行選項

   * -v [4|5]

      為solr設定版本

* Solr 4.10.4示例：

   * Install.bat -v 4 -d c:/solr-4.10.4 -c:/solr-4.10.4/example/solr/collection1

* Solr 5.4.0示例：

   * Install.sh -v 5 -d /tmp/solr-5.4.0 -c /tmp/solr-5.4.0/server/solr/collection1

**注意**:

* 安裝指令碼在通過附加&quot;。orig&quot;安裝新版本之前，將備份schema.xml和solrconfig.xml

### 關於solrconfig.xml {#about-solrconfig-xml}

的 **solrconfig.xml** 檔案控制自動提交間隔和搜索可見性，並需要測試和調整。

`<autoCommit>`:預設情況下，自動提交間隔（即硬提交到穩定儲存）設定為15秒。 搜索可見性預設為使用預提交索引。

要更改搜索以使用更新的索引來反映由於提交而發生的更改，請更改包含的 `openSearcher` 是真的。

`autoSoftCommit`:「軟」提交可確保更改可見（索引已更新），但不確保更改同步到穩定儲存（硬提交）。 結果是效能的改善。 預設情況下， `autoSoftCommit` 已禁用 `maxTime` 設定為–1。
