---
title: 如何設定示範的MongoDB
seo-title: 如何設定示範的MongoDB
description: 如何為一個製作例項和一個發佈例項設定MSRP
seo-description: 如何為一個製作例項和一個發佈例項設定MSRP
uuid: d2035a9e-f05c-4f90-949d-7cdae9646750
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 0b126218-b142-4d33-a28c-a91ab4fe99ac
role: Admin
exl-id: 7e257b34-a0f5-47db-b1a9-e26333c287d9
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 0%

---

# 如何設定示範的MongoDB {#how-to-setup-mongodb-for-demo}

## 簡介 {#introduction}

本教學課程說明如何為&#x200B;*一個author*&#x200B;例項和&#x200B;*一個publish*&#x200B;例項設定[MSRP](msrp.md)。

透過此設定，社群內容可從製作和發佈環境中存取，而無須轉送或反向復寫使用者產生的內容(UGC)。

此配置適用於&#x200B;*非生產*&#x200B;環境，如開發和/或演示。

**生 ** 產環境應：**

* 使用複製副本集運行MongoDB
* 使用SolrCloud
* 包含多個發佈者例項

## MongoDB {#mongodb}

### 安裝MongoDB {#install-mongodb}

* 從[https://www.mongodb.org/](https://www.mongodb.org/)下載MongoDB

   * 作業系統選擇：

      * Linux
      * Mac 10.8
      * Windows 7
   * 版本選擇：

      * 至少使用2.6版


* 基本配置

   * 按照MongoDB安裝說明操作。
   * 週一配置：

      * 無需配置蒙古或共用。
   * 已安裝的MongoDB資料夾將稱為&lt;mongo-install>。
   * 定義的資料目錄路徑將稱為&lt;mongo-dbpath>。


* MongoDB可在與AEM相同的主機上運行或遠程運行。

### 啟動MongoDB {#start-mongodb}

* &lt;mongo-install>/bin/mongod —dbpath  &lt;mongo-dbpath>

這將使用預設埠27017啟動MongoDB伺服器。

* 若為Mac，請以開頭arg &#39;ulimit -n 2048&#39;增加ulimit

>[!NOTE]
>
>如果在&#x200B;*AEM之後啟動MongoDB*，則&#x200B;**重新啟動**&#x200B;所有&#x200B;**AEM**&#x200B;執行個體，以便它們正確地連接到MongoDB。

### 示範生產選項：安裝MongoDB複製副本集 {#demo-production-option-setup-mongodb-replica-set}

以下命令是在localhost上設定具有3個節點的複製副本集的示例：

* `bin/mongod --port 27017 --dbpath data --replSet rs0&`
* `bin/mongo`

   * `cfg = {"_id": "rs0","version": 1,"members": [{"_id": 0,"host": "127.0.0.1:27017"}]}`
   * `rs.initiate(cfg)`

* `bin/mongod --port 27018 --dbpath data1 --replSet rs0&`
* `bin/mongod --port 27019 --dbpath data2 --replSet rs0&`
* `bin/mongo`

   * `rs.add("127.0.0.1:27018")`
   * `rs.add("127.0.0.1:27019")`
   * `rs.status()`

## Solr {#solr}

### 安裝Solr {#install-solr}

* 從[Apache Lucene](https://archive.apache.org/dist/lucene/solr/)下載Solr:

   * 適用於任何作業系統。
   * Solr 7.0版。
   * Solr需要Java 1.7或更高版本。

* 基本配置

   * 按照「示例」Solr設定操作。
   * 不需要任何服務。
   * 已安裝的Solr資料夾將稱為&lt;solr-install>。

### 為AEM Communities配置Solr {#configure-solr-for-aem-communities}

若要設定MSRP示範的Solr集合，需做出兩項決定（選取主要檔案的連結以取得詳細資訊）:

1. 以獨立模式或[SolrCloud模式](msrp.md#solrcloudmode)運行Solr。
1. 安裝[standard](msrp.md#installingstandardmls)或[advanced](msrp.md#installingadvancedmls)多語言搜尋(MLS)。

### 獨立Solr {#standalone-solr}

運行Solr的方法可能因安裝的版本和方式而異。 [Solr參考指南](https://archive.apache.org/dist/lucene/solr/ref-guide/)是權威文檔。

為簡單起見，以4.10版為例，以獨立模式啟動Solr :

* cd到&lt;solrinstall>/example
* java -jar start.jar

這將使用預設埠8983啟動Solr HTTP伺服器。 您可以瀏覽至Solr主控台以取得Solr主控台以進行測試。

* 預設Solr控制台：[http://localhost:8983/solr/](http://localhost:8983/solr/)

>[!NOTE]
>
>如果Solr Console不可用，請檢查&lt;solrinstall>/example/logs下的日誌。 查看SOLR是否嘗試綁定到無法解析的特定主機名(例如&quot;user-macbook-pro&quot;)。
如果是，請使用此主機名的新條目（如127.0.0.1 user-macbook-pro）更新etc/hosts檔案，Solr將正確啟動。

### SolrCloud {#solrcloud}

要運行非常基本（非生產）的solrCloud設定，請從以下位置開始：

* `java -Dbootstrap_confdir=./solr/collection1/conf -Dbootstrap_conf=true -DzkRun -jar start.jar`

## 將MongoDB標識為通用儲存 {#identify-mongodb-as-common-store}

啟動製作並發佈AEM例項（如有必要）。

如果AEM在MongoDB啟動之前執行，則需要重新啟動AEM執行個體。

請依照主要檔案頁面的指示操作：[MSRP - MongoDB Common Store](msrp.md)

## 測試 {#test}

若要測試及驗證MongoDB公用存放區，請在發佈執行個體上張貼註解，並在製作執行個體上檢視，以及在MongoDB和Solr中檢視UGC:

1. 在發佈執行個體上，瀏覽至[社群元件指南](http://localhost:4503/content/community-components/en/comments.html)頁面並選取註解元件。
1. 登入以張貼留言：
1. 在注釋文本輸入框中輸入文本，然後按一下&#x200B;**[!UICONTROL Post]**

   ![貼文留言](assets/post-comment.png)

1. 只要檢視[作者例項](http://localhost:4502/content/community-components/en/comments.html)上的註解（可能仍以管理員/管理員身分登入）。

   ![view-comment](assets/view-comment.png)

   注意：雖然作者上的&#x200B;*asipath*&#x200B;下有JCR節點，但這些節點是用於SCF框架的。 實際的UGC不在JCR中，而是在MongoDB中。

1. 在mongodb **[!UICONTROL Communities]** > **[!UICONTROL 集合]** > **[!UICONTROL 內容]**&#x200B;中檢視UGC

   ![ugc-content](assets/ugc-content.png)

1. 在Solr中查看UGC:

   * 瀏覽至Solr儀表板：[http://localhost:8983/solr/](http://localhost:8983/solr/)。
   * 要選擇`collection1`的用戶`core selector`。
   * 選取 `Query`.
   * 選取 `Execute Query`.

   ![ugc-solr](assets/ugc-solr.png)

## 疑難排解 {#troubleshooting}

### 未顯示UGC {#no-ugc-appears}

1. 確保MongoDB已安裝並正常運行。

1. 確認MSRP已設為預設提供者：

   * 在所有製作和發佈AEM例項上，重新造訪[儲存設定控制台](srp-config.md)或檢查AEM存放庫：

   * 在JCR中，如果[/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)不包含[srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc)節點，表示儲存提供者為JSRP。
   * 如果srpc節點存在且包含節點[defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration),defaultconfiguration的屬性應將MSRP定義為預設提供程式。

1. 確認選取MSRP後AEM重新啟動。
