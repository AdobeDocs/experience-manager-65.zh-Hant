---
title: 如何設定MongoDB以進行演示
seo-title: How to Setup MongoDB for Demo
description: 如何為一個作者實例和一個發佈實例設定MSRP
seo-description: How to setup MSRP for one author instance and one publish instance
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
source-wordcount: '774'
ht-degree: 0%

---

# 如何設定MongoDB以進行演示 {#how-to-setup-mongodb-for-demo}

## 簡介 {#introduction}

本教程介紹如何設定 [MSRP](msrp.md) 為 *一位作者* 實例和 *一篇* 實例。

通過此設定，可以從作者和發佈環境訪問社區內容，而無需向前或反向複製用戶生成的內容(UGC)。

此配置適用於 *非生產* 例如用於開發和/或演示的環境。

**A *生產* 環境應：**

* 使用複製副本集運行MongoDB
* 使用SolrCloud
* 包含多個發佈者實例

## 蒙戈DB {#mongodb}

### 安裝MongoDB {#install-mongodb}

* 從下載MongoDB [https://www.mongodb.org/](https://www.mongodb.org/)

   * 作業系統選擇：

      * Linux
      * Mac10.8
      * Windows 7
   * 版本選擇：

      * 至少使用2.6版


* 基本配置

   * 按照MongoDB安裝說明操作。
   * 為mongod配置：

      * 不需要配置蒙古人或共用。
   * 已安裝的MongoDB資料夾將稱為 &lt;mongo-install>。
   * 定義的資料目錄路徑將稱為 &lt;mongo-dbpath>。


* MongoDB可以在與主機相同的主機上運行AEM，也可以遠程運行。

### 啟動MongoDB {#start-mongodb}

* &lt;mongo-install>/bin/mongod -dbpath &lt;mongo-dbpath>

這將使用預設埠27017啟動MongoDB伺服器。

* 對於Mac，使用開頭arg &#39;ulimit -n 2048&#39;增加ulimit

>[!NOTE]
>
>如果MongoDB已啟動 *後* AEM **重新啟動** 全部 **AEM** 實例，以便它們正確連接到MongoDB。

### 演示製作選項：設定MongoDB複製副本集 {#demo-production-option-setup-mongodb-replica-set}

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

* 從下載Solr [阿帕奇盧塞內](https://archive.apache.org/dist/lucene/solr/):

   * 適用於任何作業系統。
   * Solr 7.0版。
   * Solr需要Java 1.7或更高版本。

* 基本配置

   * 按照「example」 Solr設定。
   * 不需要服務。
   * 安裝的Solr資料夾將稱為 &lt;solr-install>。

### 為AEM Communities配置解決方案 {#configure-solr-for-aem-communities}

要為MSRP配置Solr集合以進行演示，需要做出兩個決定（選擇指向主要文檔的連結以瞭解詳細資訊）:

1. 在獨立或 [SolrCloud模式](msrp.md#solrcloudmode)。
1. 安裝 [標準](msrp.md#installingstandardmls) 或 [先進](msrp.md#installingadvancedmls) 多語言搜索(MLS)。

### 獨立Solr {#standalone-solr}

運行Solr的方法可能因安裝版本和方式而異。 的 [太陽參考指南](https://archive.apache.org/dist/lucene/solr/ref-guide/) 是權威文檔。

為簡單起見，以4.10版為例，在獨立模式下啟動Solr:

* cd &lt;solrinstall>/示例
* java -jar start.jar

這將使用預設埠8983啟動Solr HTTP伺服器。 您可以瀏覽至Solr控制台以獲取Solr控制台以進行測試。

* 預設Solr控制台： [http://localhost:8983/solr/](http://localhost:8983/solr/)

>[!NOTE]
>
>如果Solr Console不可用，請檢查下面的日誌 &lt;solrinstall>/example/logs。 查看SOLR是否嘗試綁定到無法解析的特定主機名(如「user-macbook-pro」)。
如果是，則使用此主機名(如127.0.0.1 user-macbook-pro)和Solr的新條目更新etc/hosts檔案。

### 索爾雲 {#solrcloud}

要運行非常基本（非生產）的solrCloud安裝，請從以下位置開始：

* `java -Dbootstrap_confdir=./solr/collection1/conf -Dbootstrap_conf=true -DzkRun -jar start.jar`

## 將MongoDB標識為公用儲存 {#identify-mongodb-as-common-store}

如有必要，啟AEM動作者並發佈實例。

如AEM果在啟動MongoDB之前運行，則AEM需要重新啟動實例。

按照主文檔頁上的說明操作： [MSRP - MongoDB公用儲存](msrp.md)

## 測試 {#test}

要test和驗證MongoDB公用儲存，請發佈發佈實例的注釋並查看作者實例，以及在MongoDB和Solr中查看UGC:

1. 在發佈實例上，瀏覽到 [社區元件指南](http://localhost:4503/content/community-components/en/comments.html) 的子菜單。
1. 登錄以發佈評論：
1. 在注釋文本輸入框中輸入文本，然後按一下 **[!UICONTROL 帖子]**

   ![評論後](assets/post-comment.png)

1. 只需查看對 [作者實例](http://localhost:4502/content/community-components/en/comments.html) （可能仍以admin/admin身份登錄）。

   ![視圖注釋](assets/view-comment.png)

   注：當在 *輔助路徑* 作者認為，這些是為常設委員會框架提供的。 實際的UGC不在JCR中，而在MongoDB中。

1. 查看蒙古語中的UGC **[!UICONTROL 社區]** > **[!UICONTROL 集合]** > **[!UICONTROL 內容]**

   ![ugc內容](assets/ugc-content.png)

1. 在Solr中查看UGC:

   * 瀏覽到Solr儀表板： [http://localhost:8983/solr/](http://localhost:8983/solr/)。
   * 用戶 `core selector` 選擇 `collection1`。
   * 選取 `Query`.
   * 選取 `Execute Query`.

   ![ugc-solr](assets/ugc-solr.png)

## 疑難排解 {#troubleshooting}

### 未顯示UGC {#no-ugc-appears}

1. 確保MongoDB已安裝並正常運行。

1. 確保MSRP已配置為預設提供程式：

   * 在所有作者和發佈AEM實例上，重訪 [儲存配置控制台](srp-config.md) 或檢查存AEM儲庫：

   * 在JCR中，如果 [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/) 不包含 [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) 節點，表示儲存提供程式是JSRP。
   * 如果srpc節點存在並包含節點 [預設配置](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)，預設配置的屬性應將MSRP定義為預設提供程式。

1. 確保在選AEM擇MSRP後重新啟動。
