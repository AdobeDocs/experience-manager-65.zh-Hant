---
title: AEM 6.4中的RDBMS支援
seo-title: AEM 6.4中的RDBMS支援
description: 了解AEM 6.4中的關係資料庫持續性支援，以及可用的設定選項。
seo-description: 了解AEM 6.4中的關係資料庫持續性支援，以及可用的設定選項。
uuid: c8422b0d-c6df-488d-bb6a-af92c9afda50
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 6a754d42-da30-4c2f-8b9c-369e1f1f92b5
docset: aem65
feature: 設定
exl-id: 1e34c5ca-9e08-4b2a-901c-ab28aeb4a807
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---

# AEM 6.4{#rdbms-support-in-aem}中的RDBMS支援

## 概覽 {#overview}

使用文檔微內覈實現了對AEM中關係資料庫持久性的支援。 文檔微內核是實現MongoDB持久性的基礎。

它包含以Mongo Java API為基礎的Java API。 也提供BlobStore API的實作。 預設情況下，Blob儲存在資料庫中。

有關實施詳細資訊，請參閱[RDBDocumentStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBDocumentStore.html)和[RDBBlobStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBBlobStore.html)文檔。

>[!NOTE]
>
>此外，也支援&#x200B;**PostgreSQL 9.4**，但僅用於示範用途。 它將無法用於生產環境。

## 支援的資料庫{#supported-databases}

有關AEM中關係資料庫支援級別的詳細資訊，請參閱[技術要求頁](/help/sites-deploying/technical-requirements.md)。

## 配置步驟{#configuration-steps}

儲存庫是通過配置`DocumentNodeStoreService` OSGi服務建立的。 除了MongoDB外，它還擴展了它以支援關係資料庫持久性。

資料來源必須使用AEM進行設定，才能運作。 這是透過`org.apache.sling.datasource.DataSourceFactory.config`檔案完成。 相應資料庫的JDBC驅動程式需要作為本地配置內的OSGi包單獨提供。

有關為JDBC驅動程式建立OSGi套件組合的步驟，請參閱Apache Sling網站上的此[檔案](https://sling.apache.org/documentation/bundles/datasource-providers.html#convert-driver-jars-to-bundle)。

套件組合就緒後，請依照下列步驟以使用RDB持續性設定AEM:

1. 確保資料庫守護程式已啟動，並且您有可與AEM一起使用的活動資料庫。
1. 將AEM 6.3 jar複製到安裝目錄。
1. 在安裝目錄中建立名為`crx-quickstart\install`的資料夾。
1. 通過在`crx-quickstart\install`目錄中建立以下名稱的配置檔案來配置文檔節點儲存：

   * `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

1. 通過在`crx-quickstart\install`資料夾中建立另一個具有以下名稱的配置檔案來配置資料源和JDBC參數：

   * `org.apache.sling.datasource.DataSourceFactory-oak.config`
   >[!NOTE]
   >
   >有關每個受支援資料庫的資料源配置的詳細資訊，請參閱[資料源配置選項](/help/sites-deploying/rdbms-support-in-aem.md#data-source-configuration-options)。

1. 接下來，準備要與AEM一起使用的JDBC OSGi套件組合：

   1. 在`crx-quickstart/install`資料夾中，建立名為`9`的資料夾。

   1. 將JDBC jar放置在新資料夾中。

1. 最後，以`crx3`和`crx3rdb`執行模式啟動AEM :

   ```java
   java -jar quickstart.jar -r crx3,crx3rdb
   ```

## 資料源配置選項{#data-source-configuration-options}

`org.apache.sling.datasource.DataSourceFactory-oak.config` OSGi配置用於配置AEM和資料庫持久層之間通信所需的參數。

可使用下列設定選項：

* `datasource.name:` 資料來源名稱。預設值為`oak`。

* `url:` 需要與JDBC一起使用的資料庫的URL字串。每個資料庫類型都有其自己的URL字串格式。 如需詳細資訊，請參閱下方的[URL字串格式](/help/sites-deploying/rdbms-support-in-aem.md#url-string-formats)。

* `driverClassName:` JDBC驅動程式類名。這會因您要使用的資料庫以及隨後連接到該資料庫所需的驅動程式而異。 以下是AEM支援的所有資料庫的類名：

   * `org.postgresql.Driver` (適用於PostgreSQL;
   * `com.ibm.db2.jcc.DB2Driver` DB2;
   * `oracle.jdbc.OracleDriver` oracle;
   * `com.mysql.jdbc.Driver` （MySQL和MariaDB）;
   * c `om.microsoft.sqlserver.jdbc.SQLServerDriver` for Microsoft SQL Server（實驗性）。

* `username:` 資料庫運行的用戶名。

* `password:` 資料庫密碼。

### URL字串格式{#url-string-formats}

根據需要使用的資料庫類型，在資料源配置中使用不同的URL字串格式。 以下是AEM目前支援的資料庫格式清單：

* `jdbc:postgresql:databasename` (適用於PostgreSQL;
* `jdbc:db2://localhost:port/databasename` DB2;
* `jdbc:oracle:thin:localhost:port:SID` oracle;
* `jdbc:mysql://localhost:3306/databasename` （MySQL和MariaDB）;
* `jdbc:sqlserver://localhost:1453;databaseName=name` （實驗）。

## 已知限制{#known-limitations}

雖然RDBMS持續性支援同時使用具有單一資料庫的多個AEM例項，但不支援同時安裝。

要解決此問題，請確保先使用單個成員運行安裝，然後在完成安裝後添加其他成員。
