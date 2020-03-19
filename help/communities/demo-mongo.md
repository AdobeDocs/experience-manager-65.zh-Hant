---
title: 如何設定MongoDB以進行示範
seo-title: 如何設定MongoDB以進行示範
description: 如何為一個作者實例和一個發佈實例設定MSRP
seo-description: 如何為一個作者實例和一個發佈實例設定MSRP
uuid: d2035a9e-f05c-4f90-949d-7cdae9646750
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 0b126218-b142-4d33-a28c-a91ab4fe99ac
translation-type: tm+mt
source-git-commit: d6c8bbb9aa763a2eb6660b6b6755aba75241e394

---


# 如何設定MongoDB以進行示範 {#how-to-setup-mongodb-for-demo}

## 簡介 {#introduction}

本教學課程說明如何為一 [個作者例項和一個發佈例項設](msrp.md) 定 *MSRP* ( *MSRP* )。

透過此設定，社群內容可從作者和發佈環境存取，而不需正向或反向複製使用者產生的內容(UGC)。

此配置適用於非 *生產環境* ，例如開發和／或展示。

**生產&#x200B;*環境*應：**

* 使用複製副本集運行MongoDB
* 使用SolrCloud
* 包含多個發佈者例項

## MongoDB {#mongodb}

### 安裝MongoDB {#install-mongodb}

* 從https://www.mongodb.org/下載MongoDB [。](https://www.mongodb.org/)

   * 作業系統選擇：

      * Linux
      * Mac 10.8
      * Windows 7
   * 版本選擇：

      * 至少使用2.6版


* 基本配置

   * 依照MongoDB安裝指示
   * 為mongod配置

      * 無需配置蒙古檔案或共用
   * 已安裝的MongoDB資料夾將稱為&lt;mongo-install>
   * 定義的資料目錄路徑將稱為&lt;mongo-dbpath>


* MongoDB可能與AEM在同一台主機上運行，或遠程運行

### 啟動MongoDB {#start-mongodb}

* &lt;mongo-install>/bin/mongod —dbpath &lt;mongo-dbpath>

這將使用預設埠27017啟動MongoDB伺服器。

* 對於Mac，請使用start arg &#39;ulimit -n 2048&#39;增加ulimit

>[!NOTE]
>
>如果MongoDB是在 *AEM後啟動* ，請重 **新啟動所有** AEM **** 例項，以便正確連線至MongoDB。

### 示範製作選項：設定MongoDB複製副本集 {#demo-production-option-setup-mongodb-replica-set}

以下命令是在localhost上設定具有3個節點的複製副本集的示例：

* bin/mongod —port 27017 —dbpath資料—replSet rs0&amp;
* bin/mongo

   * cfg = {&quot;_id&quot;:&quot;rs0&quot;,&quot;version&quot;:1,&quot;members&quot;: [{&quot;_id&quot;:0,「主機」:&quot;127.0.0.1:27017&quot;}]}
   * rs.initiate(cfg)

* bin/mongod —port 27018 —dbpath data1 —replSet rs0&amp;
* bin/mongod —port 27019 —dbpath data2 —replSet rs0&amp;
* bin/mongo

   * rs.add(&quot;127.0.0.1:27018&quot;)
   * rs.add(&quot;127.0.0.1:27019&quot;)
   * rs.status()

## Solr {#solr}

### 安裝Solr {#install-solr}

* 從 [Apache Lucene下載Solr](https://archive.apache.org/dist/lucene/solr/):

   * 適用於任何作業系統
   * 使用4.10版或5版
   * Solr需要Java 1.7或更新版本

* 基本配置

   * 遵循「範例」Solr設定
   * 無需服務
   * 已安裝的Solr資料夾將稱為&lt;solr-install>

### 為AEM Communities設定Solr {#configure-solr-for-aem-communities}

若要設定MSRP的Solr系列以進行示範，需要做兩項決定（如需詳細資訊，請選取主要檔案的連結）:

1. 在獨立或 [SolrCloud模式下執行Solr](msrp.md#solrcloudmode)
1. 安裝 [標準](msrp.md#installingstandardmls) 或進 [階多語言搜](msrp.md#installingadvancedmls) 尋(MLS)

### 獨立Solr {#standalone-solr}

運行Solr的方法可能因安裝版本和方式而異。 Solr參 [考指南](https://archive.apache.org/dist/lucene/solr/ref-guide/) ，即權威檔案。

為簡單起見，以4.10版為例，以獨立模式啟動Solr:

* cd to &lt;solrinstall>/example
* java -jar start.jar

這將使用預設埠8983啟動Solr HTTP伺服器。 您可以瀏覽至Solr主控台，以取得Solr主控台進行測試。

* 預設Solr控制台： [http://localhost:8983/solr/](http://localhost:8983/solr/)

>[!NOTE]
>
>如果Solr Console不可用，請檢查&lt;solrinstall>/example/logs下的日誌。 查看SOLR是否嘗試綁定到無法解析的特定主機名(如「user-macbook-pro」)。
如果是，請使用此主機名的新條目（如127.0.0.1 user-macbook-pro）更新etc/hosts檔案，Solr將正常啟動。

### SolrCloud {#solrcloud}

要運行非常基本（非生產）的solrCloud設定，請從以下位置開始：

* java -Dbootstrap_confdir=。/solr/collection1/conf -Dbootstrap_conf=true -DzkRun -jar start.jar

## 將MongoDB標識為通用儲存 {#identify-mongodb-as-common-store}

視需要啟動作者並發佈AEM例項。

如果AEM在MongoDB啟動之前執行，則AEM例項將需要重新啟動。

請依照主要檔案頁面上的指示進行： [MSRP - MongoDB通用商店](msrp.md)

## 測試 {#test}

若要測試並驗證MongoDB公用商店，請在發佈例項上張貼意見，並在作者例項上檢視，以及在MongoDB和Solr中檢視UGC:

1. 在發佈實例上，瀏覽至「社群組 [件指南」頁](http://localhost:4503/content/community-components/en/comments.html) ，然後選擇「注釋」元件。
1. 登入以張貼留言：
1. 在注釋文字輸入方塊中輸入文字，然後按一下「貼 **[!UICONTROL 文」]**

   ![chlimage_1-191](assets/chlimage_1-191.png)

1. 只要檢視作者例項 [的注釋](http://localhost:4502/content/community-components/en/comments.html) （可能仍以管理員／管理員身分登入）。

   ![chlimage_1-192](assets/chlimage_1-192.png)

   注意：雖然作者在asipath下有JCR節 *點* ，但這些節點是用於SCF框架的。 實際的UGC不在JCR中，它在MongoDB中。

1. 在mongodb社群>系列> **[!UICONTROL 內容中檢視UGC]**

   ![chlimage_1-193](assets/chlimage_1-193.png)

1. 在Solr中檢視UGC:

   * 瀏覽至Solr控制面板： [http://localhost:8983/solr/](http://localhost:8983/solr/)
   * 要選 `core selector` 擇的用戶 `collection1`
   * 選取 `Query`
   * 選取 `Execute Query`
   ![chlimage_1-194](assets/chlimage_1-194.png)

## 疑難排解 {#troubleshooting}

### 未顯示UGC {#no-ugc-appears}

1. 請確定MongoDB已安裝並正常運行。

1. 請確定MSRP已設定為預設提供者：

   * 在所有作者和發佈AEM例項上，請重新造訪「儲 [存設定」主控台](srp-config.md)
   或檢查AEM資料庫：

   * 在JCR中，如 [果/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

      * 不包含srpc節 [點](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) ，這表示儲存提供程式是JSRP
      * 如果srpc節點存在並包含節點 [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)，則defaultconfiguration的屬性應將MSRP定義為預設提供程式


1. 請確定AEM在選取MSRP後重新啟動。
