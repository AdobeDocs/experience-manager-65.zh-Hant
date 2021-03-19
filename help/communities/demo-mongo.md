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
role: 管理員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 1%

---


# 如何為演示設定MongoDB {#how-to-setup-mongodb-for-demo}

## 簡介 {#introduction}

本教學課程說明如何為&#x200B;*一個作者*&#x200B;例項和&#x200B;*一個publish*&#x200B;例項設定[MSRP](msrp.md)。

透過此設定，社群內容可從作者和發佈環境存取，而不需正向或反向複製使用者產生的內容(UGC)。

此配置適用於&#x200B;*非生產*&#x200B;環境，例如開發和／或演示。

**生產 ** 環境應：**

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

   * 請遵循MongoDB安裝指示。
   * 按mongod配置：

      * 不需要配置蒙古檔案或共用。
   * 已安裝的MongoDB資料夾將稱為&lt;mongo-install>。
   * 定義的資料目錄路徑將稱為&lt;mongo-dbpath>。


* MongoDB可能與在同一台主機上運AEM行或遠程運行。

### 啟動MongoDB {#start-mongodb}

* &lt;mongo-install>/bin/mongod —dbpath  &lt;mongo-dbpath>

這將使用預設埠27017啟動MongoDB伺服器。

* 對於Mac，請使用start arg &#39;ulimit -n 2048&#39;增加ulimit

>[!NOTE]
>
>如果MongoDB在&#x200B;*之後啟動* AEM,**restart**&#x200B;所有&#x200B;**AEM**&#x200B;實例，則它們會正確連接到MongoDB。

### 示範製作選項：設定MongoDB複製副本集{#demo-production-option-setup-mongodb-replica-set}

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
   * Solr需要Java 1.7或更新版本。

* 基本配置

   * 請遵循「範例」Solr設定。
   * 不需要任何服務。
   * 已安裝的Solr資料夾將稱為&lt;solr-install>。

### 為AEM Communities配置Solr {#configure-solr-for-aem-communities}

若要設定MSRP的Solr系列以進行示範，需要做兩項決定（如需詳細資訊，請選取主要檔案的連結）:

1. 在獨立或[SolrCloud模式](msrp.md#solrcloudmode)中運行Solr。
1. 安裝[standard](msrp.md#installingstandardmls)或[advanced](msrp.md#installingadvancedmls)多語言搜尋(MLS)。

### 獨立Solr {#standalone-solr}

運行Solr的方法可能因安裝版本和方式而異。 [Solr參考指南](https://archive.apache.org/dist/lucene/solr/ref-guide/)是權威文檔。

為簡單起見，以4.10版為例，以獨立模式啟動Solr:

* cd to &lt;solrinstall>/example
* java -jar start.jar

這將使用預設埠8983啟動Solr HTTP伺服器。 您可以瀏覽至Solr Console以取得Solr主控台進行測試。

* 預設Solr控制台：[http://localhost:8983/solr/](http://localhost:8983/solr/)

>[!NOTE]
>
>如果Solr Console不可用，請檢查&lt;solrinstall>/example/logs下的日誌。 查看SOLR是否嘗試綁定到無法解析的特定主機名(如「user-macbook-pro」)。
如果是，請使用此主機名的新條目（如127.0.0.1 user-macbook-pro）更新etc/hosts檔案，Solr將正常啟動。

### SolrCloud {#solrcloud}

要運行非常基本（非生產）的solrCloud設定，請從以下位置開始：

* `java -Dbootstrap_confdir=./solr/collection1/conf -Dbootstrap_conf=true -DzkRun -jar start.jar`

## 將MongoDB標識為公用儲存{#identify-mongodb-as-common-store}

視需要啟動作AEM者並發佈例項。

如AEM果在啟動MongoDB之前運行，則AEM需要重新啟動實例。

請依照主要檔案頁面上的指示進行：[MSRP - MongoDB Common Store](msrp.md)

## 測試 {#test}

若要測試並驗證MongoDB公用商店，請在發佈例項上張貼意見，並在作者例項上檢視，以及在MongoDB和Solr中檢視UGC:

1. 在發佈實例上，瀏覽至[Community Components Guide](http://localhost:4503/content/community-components/en/comments.html)頁並選擇Comments元件。
1. 登入以張貼留言：
1. 在注釋文本輸入框中輸入文本，然後按一下&#x200B;**[!UICONTROL Post]**

   ![留言後](assets/post-comment.png)

1. 只要檢視[author instance](http://localhost:4502/content/community-components/en/comments.html)（可能仍以管理員／管理員身分登入）的注釋即可。

   ![view-comment](assets/view-comment.png)

   注意：雖然作者在&#x200B;*asipath*&#x200B;下有JCR節點，但這些節點是用於SCF框架的。 實際的UGC不在JCR中，它在MongoDB中。

1. 在mongodb **[!UICONTROL Communities]** > **[!UICONTROL Collections]** > **[!UICONTROL Content]**&#x200B;中查看UGC

   ![ugc-content](assets/ugc-content.png)

1. 在Solr中檢視UGC:

   * 瀏覽至Solr控制面板：[http://localhost:8983/solr/](http://localhost:8983/solr/)。
   * 用戶`core selector`選擇`collection1`。
   * 選取 `Query`.
   * 選取 `Execute Query`.

   ![ugc-solr](assets/ugc-solr.png)

## 疑難排解 {#troubleshooting}

### 未顯示UGC {#no-ugc-appears}

1. 請確定MongoDB已安裝並正常運行。

1. 請確定MSRP已設定為預設提供者：

   * 在所有作者和發AEM布實例上，請重新訪問[儲存配置控制台](srp-config.md)或檢查存AEM儲庫：

   * 在JCR中，如果[/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)不包含[srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc)節點，表示儲存提供商是JSRP。
   * 如果srpc節點存在並包含節點[defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)，則defaultconfiguration的屬性應將MSRP定義為預設提供程式。

1. 請確定在AEM選取MSRP後重新啟動。
