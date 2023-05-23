---
title: RDBMS在AEM6.4中的支援
seo-title: RDBMS Support in AEM 6.4
description: 瞭解6.4中的關係資料庫持AEM久性支援和可用的配置選項。
seo-description: Learn about the relational database persistence support in AEM 6.4 and the available configuration options.
uuid: c8422b0d-c6df-488d-bb6a-af92c9afda50
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 6a754d42-da30-4c2f-8b9c-369e1f1f92b5
docset: aem65
feature: Configuring
exl-id: 1e34c5ca-9e08-4b2a-901c-ab28aeb4a807
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 0%

---

# RDBMS在AEM6.4中的支援{#rdbms-support-in-aem}

## 概觀 {#overview}

支援中的關係資料AEM庫持久性是使用Document Microkernel實現的。 Document Microkernel是還用於實現MongoDB持久性的基礎。

它由基於Mongo Java API的Java API組成。 還提供了BlobStore API的實現。 預設情況下，Blob儲存在資料庫中。

有關實施詳情的詳細資訊，請參閱 [RDBDocumentStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBDocumentStore.html) 和 [RDBBlobStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBBlobStore.html) 文檔。

>[!NOTE]
>
>支援 **PostgreSQL 9.4** 也提供了，但僅用於演示。 它將不能用於生產環境。

## 支援的資料庫 {#supported-databases}

有關中關係資料庫支援級別的詳細信AEM息，請參見 [「技術要求」頁](/help/sites-deploying/technical-requirements.md)。

## 配置步驟 {#configuration-steps}

通過配置 `DocumentNodeStoreService` OSGi服務。 除了MongoDB外，它還擴展為支援關係資料庫持久性。

要使資料源工作，需要配置資料源AEM。 此操作通過 `org.apache.sling.datasource.DataSourceFactory.config` 的子菜單。 相應資料庫的JDBC驅動程式需要作為OSGi捆綁包在本地配置中單獨提供。

有關為JDBC驅動程式建立OSGi捆綁包的步驟，請參閱 [文檔](https://sling.apache.org/documentation/bundles/datasource-providers.html#convert-driver-jars-to-bundle) 在阿帕奇·斯靈網站上。

在捆綁包到位後，按照以下步驟配置AEMRDB持久性：

1. 確保資料庫守護程式已啟動，並且您有可用的活動資料AEM庫。
1. 將AEM6.3jar複製到安裝目錄。
1. 建立名為 `crx-quickstart\install` 的子菜單。
1. 通過在中建立具有以下名稱的配置檔案來配置文檔節點儲存 `crx-quickstart\install` 目錄：

   * `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

1. 通過在中建立具有以下名稱的另一個配置檔案來配置資料源和JDBC參數 `crx-quickstart\install` 資料夾：

   * `org.apache.sling.datasource.DataSourceFactory-oak.config`
   >[!NOTE]
   >
   >有關每個受支援資料庫的資料源配置的詳細資訊，請參見 [資料源配置選項](/help/sites-deploying/rdbms-support-in-aem.md#data-source-configuration-options)。

1. 接下來，準備JDBC OSGi捆綁包，以與AEM:

   1. 在 `crx-quickstart/install` 資料夾，建立名為 `9`。

   1. 將JDBC jar放在新資料夾中。

1. 最後，AEM從 `crx3` 和 `crx3rdb` 運行模式：

   ```java
   java -jar quickstart.jar -r crx3,crx3rdb
   ```

## 資料源配置選項 {#data-source-configuration-options}

的 `org.apache.sling.datasource.DataSourceFactory-oak.config` OSGi配置用於配置在資料庫持久層和資料AEM庫持久層之間通信所需的參數。

以下配置選項可用：

* `datasource.name:` 資料源名稱。 預設為 `oak`。

* `url:` 需要與JDBC一起使用的資料庫的URL字串。 每個資料庫類型都有其自己的URL字串格式。 有關詳細資訊，請參見 [URL字串格式](/help/sites-deploying/rdbms-support-in-aem.md#url-string-formats) 下。

* `driverClassName:` JDBC驅動程式類名。 這取決於您要使用的資料庫，隨後取決於連接到該資料庫所需的驅動程式。 以下是所有受支援資料庫的類名AEM:

   * `org.postgresql.Driver` 用於PostgreSQL;
   * `com.ibm.db2.jcc.DB2Driver` DB2;
   * `oracle.jdbc.OracleDriver` oracle;
   * `com.mysql.jdbc.Driver` 用於MySQL和MariaDB（實驗）;
   * c `om.microsoft.sqlserver.jdbc.SQLServerDriver` 用於MicrosoftSQL Server（實驗）。

* `username:` 資料庫運行的用戶名。

* `password:` 資料庫密碼。

### URL字串格式 {#url-string-formats}

在資料源配置中使用不同的URL字串格式，這取決於需要使用的資料庫類型。 以下是當前支援的資料庫格AEM式清單：

* `jdbc:postgresql:databasename` 用於PostgreSQL;
* `jdbc:db2://localhost:port/databasename` DB2;
* `jdbc:oracle:thin:localhost:port:SID` oracle;
* `jdbc:mysql://localhost:3306/databasename` 用於MySQL和MariaDB（實驗）;
* `jdbc:sqlserver://localhost:1453;databaseName=name` 用於MicrosoftSQL Server（實驗）。

## 已知限制 {#known-limitations}

雖然RDBMS持久性支AEM持將多個實例與單個資料庫併發使用，但併發安裝不支援。

為瞭解決此問題，請確保先使用單個成員運行安裝，並在第一個成員完成安裝後添加其他成員。
