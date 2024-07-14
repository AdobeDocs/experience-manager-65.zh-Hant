---
title: AEM 6.4中的RDBMS支援
description: 瞭解AEM 6.4中的關聯式資料庫持續性支援和可用的設定選項。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
docset: aem65
feature: Administering
exl-id: 1e34c5ca-9e08-4b2a-901c-ab28aeb4a807
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 0%

---

# AEM 6.4中的RDBMS支援{#rdbms-support-in-aem}

## 概觀 {#overview}

AEM對關聯式資料庫持續性的支援是使用Document Microkernel來實作。 檔案Microkernel是用來實作MongoDB持續性的基礎。

它包含以Mongo Java API為基礎的Java API。 也提供BlobStore API的實作。 根據預設，Blob會儲存在資料庫中。

如需實作詳細資訊的詳細資訊，請參閱[RDBDocumentStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBDocumentStore.html)和[RDBBlobStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBBlobStore.html)檔案。

>[!NOTE]
>
>也提供&#x200B;**PostgreSQL 9.4**&#x200B;的支援，但僅供示範之用。 它將不適用於生產環境。

## 支援的資料庫 {#supported-databases}

如需有關AEM中關聯式資料庫支援層級的詳細資訊，請參閱[技術需求頁面](/help/sites-deploying/technical-requirements.md)。

## 設定步驟 {#configuration-steps}

存放庫是透過設定`DocumentNodeStoreService` OSGi服務所建立。 除了MongoDB之外，還延伸支援關聯式資料庫持續性。

資料來源必須設定為AEM才能運作。 這是透過`org.apache.sling.datasource.DataSourceFactory.config`檔案完成。 個別資料庫的JDBC驅動程式需要在本機設定中單獨提供為OSGi套件組合。

如需建立JDBC驅動程式的OSGi套件組合的相關步驟，請參閱Apache Sling網站上的此[檔案](https://sling.apache.org/documentation/bundles/datasource-providers.html#convert-driver-jars-to-bundle)。

組合準備就緒後，請按照以下步驟使用RDB持續性設定AEM：

1. 請確定資料庫協助程式已啟動，而且您有可與AEM搭配使用的作用中資料庫。
1. 將AEM 6.3 jar複製到安裝目錄。
1. 在安裝目錄中建立名為`crx-quickstart\install`的資料夾。
1. 在`crx-quickstart\install`目錄中建立具有下列名稱的組態檔，以設定檔案節點存放區：

   * `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

1. 在`crx-quickstart\install`資料夾中建立另一個名稱如下的組態檔，以設定資料來源和JDBC引數：

   * `org.apache.sling.datasource.DataSourceFactory-oak.config`

   >[!NOTE]
   >
   >如需每個支援之資料庫的資料來源組態詳細資訊，請參閱[資料Source組態選項](/help/sites-deploying/rdbms-support-in-aem.md#data-source-configuration-options)。

1. 接下來，準備要與AEM搭配使用的JDBC OSGi套件組合：

   1. 在`crx-quickstart/install`資料夾中，建立名為`9`的資料夾。

   1. 將JDBC jar放在新資料夾中。

1. 最後，以`crx3`和`crx3rdb`執行模式啟動AEM：

   ```java
   java -jar quickstart.jar -r crx3,crx3rdb
   ```

## 資料Source設定選項 {#data-source-configuration-options}

`org.apache.sling.datasource.DataSourceFactory-oak.config` OSGi設定是用來設定AEM與資料庫持續層之間通訊所需的引數。

下列組態選項可供使用：

* `datasource.name:`資料來源名稱。 預設為 `oak`。

* `url:`需要與JDBC搭配使用的資料庫URL字串。 每種資料庫型別都有自己的URL字串格式。 如需詳細資訊，請參閱下方的[URL字串格式](/help/sites-deploying/rdbms-support-in-aem.md#url-string-formats)。

* `driverClassName:` JDBC驅動程式類別名稱。 根據您要使用的資料庫，以及隨後連線至資料庫所需的驅動程式，這會有所不同。 以下是AEM支援之所有資料庫的類別名稱：

   * PostgreSQL的`org.postgresql.Driver`；
   * DB2的`com.ibm.db2.jcc.DB2Driver`；
   * `oracle.jdbc.OracleDriver`用於Oracle；
   * MySQL和MariaDB的`com.mysql.jdbc.Driver` （實驗性）；
   * c `om.microsoft.sqlserver.jdbc.SQLServerDriver` for Microsoft SQL Server （實驗性）。

* `username:`執行資料庫的使用者名稱。

* `password:`資料庫密碼。

### url字串格式 {#url-string-formats}

根據需要使用的資料庫型別，在資料來源設定中使用不同的URL字串格式。 以下是AEM目前支援之資料庫的格式清單：

* PostgreSQL的`jdbc:postgresql:databasename`；
* DB2的`jdbc:db2://localhost:port/databasename`；
* `jdbc:oracle:thin:localhost:port:SID`用於Oracle；
* MySQL和MariaDB的`jdbc:mysql://localhost:3306/databasename` （實驗性）；
* Microsoft SQL Server的`jdbc:sqlserver://localhost:1453;databaseName=name` （實驗性）。

## 已知限制 {#known-limitations}

雖然RDBMS持續性支援同時使用單一資料庫的多個AEM執行個體，但並不支援同時安裝。

為了解決這個問題，請務必先以單一成員執行安裝，並在第一個成員完成安裝後新增其他成員。
