---
title: AEM 6.4中的RDBMS支援
seo-title: AEM 6.4中的RDBMS支援
description: 瞭解AEM 6.4中的關聯式資料庫永續性支援以及可用的設定選項。
seo-description: 瞭解AEM 6.4中的關聯式資料庫永續性支援以及可用的設定選項。
uuid: c8422b0d-c6df-488d-bb6a-af92c9afda50
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 6a754d42-da30-4c2f-8b9c-369e1f1f92b5
docset: aem65
translation-type: tm+mt
source-git-commit: 38ef8fc8d80009c8ca79aca9e45cf10bd70e1f1e
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---


# AEM 6.4{#rdbms-support-in-aem}中的RDBMS支援

## 概覽 {#overview}

AEM中對關係型資料庫永續性的支援是使用Document Microkernel實作的。 Document Microkernel也是實現MongoDB持久性的基礎。

它包含以Mongo Java API為基礎的Java API。 還提供了BlobStore API的實現。 預設情況下，blob儲存在資料庫中。

有關實施詳細資訊，請參見[RDBDocumentStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBDocumentStore.html)和[RDBBlobStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBBlobStore.html)文檔。

>[!NOTE]
>
>另外也提供對&#x200B;**PostgreSQL 9.4**&#x200B;的支援，但僅供示範之用。 它不適用於生產環境。

## 支援的資料庫{#supported-databases}

如需AEM中關聯式資料庫支援層級的詳細資訊，請參閱[技術需求頁面](/help/sites-deploying/technical-requirements.md)。

## 配置步驟{#configuration-steps}

儲存庫是通過配置`DocumentNodeStoreService` OSGi服務建立的。 除了MongoDB外，它還擴展了它以支援關係資料庫持久性。

若要運作，資料來源必須使用AEM進行設定。 這是透過`org.apache.sling.datasource.DataSourceFactory.config`檔案完成。 在本地配置中，需要分別以OSGi捆綁包的形式提供相應資料庫的JDBC驅動程式。

如需建立JDBC驅動程式的OSGi組合的步驟，請參閱Apache Sling網站上的此[documentation](https://sling.apache.org/documentation/bundles/datasource-providers.html#convert-driver-jars-to-bundle)。

在套件就位後，請依照下列步驟來設定AEM的RDB永續性：

1. 請確定資料庫守護程式已啟動，且您有可與AEM搭配使用的作用中資料庫。
1. 將AEM 6.3 jar複製至安裝目錄。
1. 在安裝目錄中建立名為`crx-quickstart\install`的資料夾。
1. 通過在`crx-quickstart\install`目錄中建立具有以下名稱的配置檔案來配置文檔節點儲存：

   * `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

1. 通過在`crx-quickstart\install`資料夾中建立另一個具有以下名稱的配置檔案來配置資料源和JDBC參數：

   * `org.apache.sling.datasource.DataSourceFactory-oak.config`
   >[!NOTE]
   >
   >有關每個支援資料庫的資料源配置的詳細資訊，請參見[資料源配置選項](/help/sites-deploying/rdbms-support-in-aem.md#data-source-configuration-options)。

1. 接下來，準備要與AEM搭配使用的JDBC OSGi搭售：

   1. 在`crx-quickstart/install`資料夾中，建立名為`9`的資料夾。

   1. 將JDBCjar放在新資料夾中。

1. 最後，使用`crx3`和`crx3rdb`執行模式啟動AEM:

   ```java
   java -jar quickstart.jar -r crx3,crx3rdb
   ```

## 資料源配置選項{#data-source-configuration-options}

`org.apache.sling.datasource.DataSourceFactory-oak.config` OSGi組態可用來設定AEM與資料庫永續層通訊所需的參數。

可使用下列配置選項：

* `datasource.name:` 資料來源名稱。預設值為`oak`。

* `url:` 需要與JDBC一起使用的資料庫的URL字串。每個資料庫類型都有其自己的URL字串格式。 如需詳細資訊，請參閱下方的[URL字串格式](/help/sites-deploying/rdbms-support-in-aem.md#url-string-formats)。

* `driverClassName:` JDBC驅動程式類名。這將因您要使用的資料庫以及隨後連接到資料庫所需的驅動程式而異。 以下是AEM支援之所有資料庫的類別名稱：

   * `org.postgresql.Driver` for PostgreSQL;
   * `com.ibm.db2.jcc.DB2Driver` DB2;
   * `oracle.jdbc.OracleDriver` 對Oracle;
   * `com.mysql.jdbc.Driver` 對於MySQL和MariaDB（實驗性）;
   * c `om.microsoft.sqlserver.jdbc.SQLServerDriver` for Microsoft SQL Server（實驗性）。

* `username:` 資料庫運行的用戶名。

* `password:` 資料庫口令。

### URL字串格式{#url-string-formats}

根據需要使用的資料庫類型，資料源配置中會使用不同的URL字串格式。 以下是AEM目前支援之資料庫的格式清單：

* `jdbc:postgresql:databasename` for PostgreSQL;
* `jdbc:db2://localhost:port/databasename` DB2;
* `jdbc:oracle:thin:localhost:port:SID` 對Oracle;
* `jdbc:mysql://localhost:3306/databasename` 對於MySQL和MariaDB（實驗性）;
* `jdbc:sqlserver://localhost:1453;databaseName=name` for Microsoft SQL Server（實驗性）。

## 已知限制{#known-limitations}

雖然RDBMS永續性支援將多個AEM例項與單一資料庫同時使用，但並行安裝則不受支援。

為瞭解決這個問題，請務必先使用單一成員運行安裝，然後在完成安裝後添加其他成員。

