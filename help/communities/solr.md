---
title: SRP的Solr配置
seo-title: SRP的Solr配置
description: Apache Solr安裝可通過使用不同的集合在節點儲存(Oak)和公共儲存(SRP)之間共用
seo-description: Apache Solr安裝可通過使用不同的集合在節點儲存(Oak)和公共儲存(SRP)之間共用
uuid: 7356343d-073c-4266-bdcb-c7e999281476
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e228f1db-91ea-4ec3-86da-06d89d74bc72
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# SRP的Solr配置 {#solr-configuration-for-srp}

## Solr for AEM Platform {#solr-for-aem-platform}

Apache Solr [(](https://lucene.apache.org/solr/) Apache Solr [)安裝可以通過使用不同的](../../help/sites-deploying/data-store-config.md) 集合在節點儲存 [(Oak)和](working-with-srp.md) 公共儲存(SRP)之間共用。

如果Oak和SRP系列都被大量使用，則可基於效能原因安裝第二個Solr。

對於生產環境， [SolrCloud模式比獨立模式](#solrcloud-mode) （單一本機Solr設定）提供更佳的效能。

### 需求 {#requirements}

下載並安裝Apache Solr:

* [4.10版](https://archive.apache.org/dist/lucene/solr/4.10.4/) 或 [5版](https://archive.apache.org/dist/lucene/solr/5.5.3/)

* Solr需要Java 1.7或更新版本
* 無需服務
* 運行模式選擇：

   * 獨立模式
   * [SolrCloud模式](#solrcloud-mode) （建議用於生產環境）

* 多語言搜尋選擇(MLS)

   * [安裝標準MLS](#installing-standard-mls)
   * [安裝進階MLS](#installing-advanced-mls)

## SolrCloud模式 {#solrcloud-mode}

[建議生產環境使用SolrCloud](https://cwiki.apache.org/confluence/display/solr/SolrCloud) 模式。 在SolrCloud模式中執行時，必須先安裝並設定SolrCloud，才能安裝多語言搜尋(MLS)。

建議您依照SolrCloud指示進行安裝：

* 同一伺服器上的3個SolrCloud節點
* 外部Apache ZooKeeper

此外，建議您設定JVM以調整記憶體使用和廢棄項目收集。

### JVM配置示例 {#jvm-configuration-example}

```shell
JVM_OPTS="-server -Xmx2048m -XX:MaxPermSize=768M -XX:+UseConcMarkSweepGC -XX:+CMSClassUnloadingEnabled -Xloggc:../logs/gc.log -XX:+PrintGCDetails -XX:+PrintGCDateStamps -Djava.awt.headless=true"
```

### SolrCloud設定命令 {#solrcloud-setup-commands}

在SolrCloud模式中執行時，在安裝MLS之前，必須使用並瞭解下列SolrCloud設定命令。

#### 1.上傳組態至ZooKeeper {#upload-a-configuration-to-zookeeper}

參考：[https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities](https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities)

用法：sh./scripts/cloud-scripts/zkcli.sh \
-cmd upconfig \
-zkhost *server:port* \
-confname *myconfig-name *\
-solrhome *solr-home-path* \
-confdir *config-dir*

#### 2.建立系列 {#create-a-collection}

參考：[https://cwiki.apache.org/confluence/display/solr/Solr+Start+Script+Reference#SolrStartScriptReference-Create](https://cwiki.apache.org/confluence/display/solr/Solr+Start+Script+Reference#SolrStartScriptReference-Create)

使用狀況:
./bin/solr create \
-c *mycollection-name*\
-d *config-dir* \
-n *myconfig-name* \
-p端 *口*\
-s *碎片數* \
-rf *副本數*

#### 3.將系列連結至組態集 {#link-a-collection-to-a-configuration-set}

將系列連結至已上傳至ZooKeeper的設定。

參考：[https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities](https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities)

用法：sh./scripts/cloud-scripts/zkcli.sh \
-cmd linkconfig \
-zkhost *server:port* \
-collection *mycollection-name* \
-confname *myconfig-name*

### 標準MLS與先進MLS的比較 {#comparison-of-standard-and-advanced-mls}

AEM Communities的多語言搜尋(MLS)是專為Solr平台所建立，可改善所有支援語言（包括英文）的搜尋。

AEM社群的MLS可以是標準MLS或進階MLS。 標準MLS僅包含Solr組態設定，並排除任何外掛程式或資源檔案。 進階MLS是更完整的解決方案，包含Solr組態設定、外掛程式和相關資源

標準MLS包含下列語言的內容搜尋增強功能：

* 英文：用於嘗試匹配單詞導子的改進設定器
* 日文：改良的半寬字元日文Token化

進階MLS包含下列語言的內容搜尋增強功能：

* 英文：用浮毛機取代修腳機
* 德文：添加的解壓縮器
* 法文：新增的條件處理
* 簡體中文：新增更聰明的Tokenizer
* 各種語言：新增更精簡、停止字詞清單和標準化程式。

Advanced MLS支援下列33種語言。

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

#### AEM 6.1 Solr搜尋、標準MLS與進階MLS的比較 {#comparison-of-aem-solr-search-standard-mls-and-advanced-mls}

**注意**:AEM 6.1指AEM 6.1 Communities FP3及更早版本。

![chlimage_1-283](assets/chlimage_1-283.png)

### 安裝標準MLS {#installing-standard-mls}

對於SRP收集（MSRP或DSRP），為了支援標準多語言搜索(MLS)，必須修改Solr的兩個配置檔案：

* **schema.xml**
* **solrconfig.xml**

Solr 4.10適用的標準MLS檔案(schema.xml、solrconfig.xml)

Solr 5的標準MLS檔案(schema.xml、solrconfig.xml)

標準MLS檔案會儲存在AEM儲存庫中。

**注意**:Solr檔案儲存在msrp/資料夾中，但也用於DSRP（不需要變更）。

**下載指示**:以 `solrX` 或 `solr4``solr5` 適當取代

1. 使用CRXDE|Lite，找到

   * /libs/social/config/datastore/msrp/*solrX*/**schema.xml**
   * /libs/social/config/datastore/msrp/*solrX*/**solrconfig.xml**

1. 下載至部署Solr的本機伺服器

   * 找到 `jcr:content` 節點的屬 `jcr:data` 性
   * 選擇 `view` 以開始下載
   * 確定檔案已儲存為適當的名稱和編碼(UTF8)

1. 依照獨立或SolrCloud模式的安裝指示進行

#### SolrCloud模式——標準MLS {#solrcloud-mode-standard-mls}

1. 在SolrCloud模式下安裝和配置Solr
1. 準備新配置：

   1. 創 *建new-config-dir* ，如 *solr-install-dir*/myconfig/

   1. 將現有Solr配置目錄的內容復 *制到new-config-dir*

      * 對於Solr4:copy *solr-install-dir*/example/solr/collection1/conf/&amp;ast;
      * 針對Solr5:copy *solr-install-dir*/server/solr/configsets/data_driven_schema_configs/&amp;ast;
   1. 將下載的 **schema.xml****和solrconfig.xml複製** 到new-config-dir ** ，以覆寫現有檔案


1. [將新組態上傳](#upload-a-configuration-to-zookeeper) 至ZooKeeper
1. [建立指定必要參數的集合](#create-a-collection) ，如分片數、複製副本數和配置名稱。
1. 如果設定名稱*未*在建立系列時提供，請將此新建立的 [系列與上傳至ZooKeeper的設定連結](#link-a-collection-to-a-configuration-set) 。

1. 對於MSRP，請執行 [MSRP重新索引工具](msrp.md#msrp-reindex-tool)，除非這是新安裝

#### 獨立模式——標準MLS {#standalone-mode-standard-mls}

1. 以獨立模式安裝Solr
1. 如果執行Solr5，請建立系列1（類似於Solr4）:

   * ./bin/solr啟動
   * ./bin/solr create_core -c collection1 -d sample_techproducts_configs

1. Solr **config目錄中的** Backup schema.xml和 **solrconfig.xml** ，例如：

   * 對於Solr4: *solr-install-dir*/example/solr/collection1/conf/
   * 為Solr5建立： *solr-install-dir*/server/solr/collection1/conf/

1. 將下載的 **schema.xml****** 和solrconfig.xml複製到相同目錄

1. 重新啟動Solr
1. 對於MSRP，請執行 [MSRP重新索引工具](#msrpreindextool)，除非這是新安裝

### 安裝進階MLS {#installing-advanced-mls}

若要支援進階MLS的SRP集合（MSRP或DSRP），除了自訂架構和Solr組態外，還需要新的Solr外掛程式。 所有必要項目都封裝在可下載的zip檔案中。 此外，安裝指令碼也隨附在獨立模式下部署Solr時使用。

若要取得進階MLS套件，請參 [閱檔案部署區段中的AEM Advanced MLS](deploy-communities.md#aem-advanced-mls) 。

若要開始安裝SolrCloud或獨立模式：

* 下載AEM-SOLR-MLS zip封存至代管Solr的伺服器
* 解壓縮存檔

#### SolrCloud模式——進階MLS {#solrcloud-mode-advanced-mls}

安裝說明——注意Solr4和Solr5的幾點差異：

1. 在SolrCloud模式下安裝和配置Solr
1. 將進階MLS套件的內容解壓縮至磁碟。 內容應包括：

   * **schema.xml**
   * **solrconfig.xml**
   * **stopwords/** folder
   * **配置檔案／資料夾**
   * **extra-libs/** folder

1. 準備新配置：

   1. 建立 *新配置目錄*

      * 例如 *solr-install-dir*/myconfig/
      * 建立子檔案夾stopwords/和lang/
   1. 將現有Solr配置目錄的內容復 *制到new-config-dir*

      * 對於Solr4:Copy *solr-install-dir*/example/solr/collection1/conf/&amp;ast;
      * 針對Solr5:復 *制solr-install-dir*/server/solr/configsets/data_driven_schema_configs/&amp;ast;
   1. 將解壓縮 **的schema.xml****和solrconfig.xml複製** 到new-config-dir ** ，以覆寫現有檔案
   1. 針對Solr5:將 *solr_install_dir*/server/solr/configsets/sample_techproducts_configs/conf/lang/&amp;ast;.txt&quot;複製到 *new-config-dir*/lang/
   1. 將提取 **的stopwords/** folder複製 *到new-config-dir* ，生成 *new-config-dir*/stopwords/&amp;ast;.txt



1. [將新組態上傳](#upload-a-configuration-to-zookeeper) 至ZooKeeper
1. 複製新的 **配置檔案/** 資料夾……

   * 對於Solr4:複製到每個節點的資源／資料夾
   * 針對Solr5:複製到每個Solr安裝的伺服器／資源／資料夾。 如果所有節點都位於同一個Solr安裝目錄中，則僅執行一次此步驟。

1. 在SolrCloud中 **每個節點** 的solr-home目錄（包含solr.xml）中建立lib/資料夾。 將jar從以下位置複製到每個節點上的新lib/資料夾：

   * **從進階MLS套件擷取的extra-libs/** extra-libs
   * *solr-install-dir/contrib/extraction/lib/* jar
   * *solr-install-dir/dist/solr-cell*.jar
   * *solr-install-dir/contrib/clustering/lib/* jar
   * *solr-install-dir/dist/solr-clustering*.jar
   * *solr-install-dir/contrib/langid/lib/* jar
   * *solr-install-dir/dist/solr-langid*.jar
   * *solr-install-dir/contrib/velocity/lib/* jar
   * *solr-install-dir/dist/solr-velocity*.jar
   * *solr-install-dir/contrib/analysis-extras/lib/* jar
   * *solr-install-dir/contrib/analysis-extras/lucene-libs/* jar

1. [建立指定必要參數的集合](#create-a-collection) ，如分片數、複製副本數和配置名稱。
1. 如果在建立系列 *時未提供* ，請將此新建立的 [系列與上傳至ZooKeeper的設定連結](#link-a-collection-to-a-configuration-set) 。

1. 對於MSRP，請執行 [MSRP重新索引工具](#msrpreindextool)，除非這是新安裝

#### 獨立模式——進階MLS {#standalone-mode-advanced-mls}

進階MLS套件中包含安裝指令碼。

將軟體包的內容解壓縮到托管獨立Solr伺服器的伺服器後，只需執行安裝指令碼以安裝必要的資源和配置檔案。

* 以獨立模式安裝Solr
* 如果執行Solr5，請建立系列1（類似於Solr4）:

   * ./bin/solr啟動
   * ./bin/solr create_core -c collection1 -d sample_techproducts_configs

* 運行安裝指令碼：安 [裝-v 4|5] - [d solhome] -c收集路徑 []:

   * -d solrhome

      Solr安裝目錄

   * -c集合路徑

      索爾中的收集路徑

   * --說明

      打印命令行選項

   * -v [4|5]

      為solr設定版本

* Solr 4.10.4的範例：

   * Install.bat -v 4 -d c:/solr-4.10.4 -c:/solr-4.10.4/example/solr/collection1

* Solr 5.4.0的範例：

   * Install.sh -v 5 -d /tmp/solr-5.4.0 -c /tmp/solr-5.4.0/server/solr/collection1

**注意**:

* 在安裝新版本之前，安裝指令碼將通過附加&quot;。orig&quot;來備份schema.xml和solrconfig.xml

### 關於solrconfig.xml {#about-solrconfig-xml}

solrconfig.xml **** 檔案可控制自動提交間隔和搜尋可見度，而且需要測試和調整。

&lt;autoCommit>:預設情況下， autoCommit間隔（對穩定儲存的硬提交）設定為15秒。 搜索可見性預設為使用預提交索引。

要將搜索更改為使用更新的索引來反映由於提交而發生的更改，請將包含的&lt;openSearcher>更改為true。

&lt;autoSoftCommit>:「軟」提交可確保更改可見（索引已更新），但不確保更改同步到穩定儲存（硬提交）。 結果是效能的提升。 預設情況下，&lt;autoSoftCommit>在包含的&lt;maxTime>設定為-1時被禁用。
