---
title: 6.4中的AEMRDBMS支援
seo-title: 6.4中的AEMRDBMS支援
description: 瞭解6.4中的關聯式資料庫永續性支AEM援以及可用的設定選項。
seo-description: 瞭解6.4中的關聯式資料庫永續性支AEM援以及可用的設定選項。
uuid: c8422b0d-c6df-488d-bb6a-af92c9afda50
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 6a754d42-da30-4c2f-8b9c-369e1f1f92b5
docset: aem65
feature: Configuring
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---


# 6.AEM4{#rdbms-support-in-aem}中的RDBMS支援

## 概覽 {#overview}

使用Document Microkernel實現了對關AEM系資料庫持久性的支援。 Document Microkernel也是實現MongoDB持久性的基礎。

它包含以Mongo Java API為基礎的Java API。 還提供了BlobStore API的實現。 預設情況下，blob儲存在資料庫中。

有關實施詳細資訊，請參見[RDBDocumentStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBDocumentStore.html)和[RDBBlobStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBBlobStore.html)文檔。

>[!NOTE]
>
>另外也提供對&#x200B;**PostgreSQL 9.4**&#x200B;的支援，但僅供示範之用。 它不適用於生產環境。

## 支援的資料庫{#supported-databases}

有關中關係型資料庫支援級別的詳細信AEM息，請參見[技術要求頁](/help/sites-deploying/technical-requirements.md)。

## 配置步驟{#configuration-steps}

儲存庫是通過配置`DocumentNodeStoreService` OSGi服務建立的。 除了MongoDB外，它還擴展了它以支援關係資料庫持久性。

為了讓它運作，需要配置資料源AEM。 這是透過`org.apache.sling.datasource.DataSourceFactory.config`檔案完成。 在本地配置中，需要分別以OSGi捆綁包的形式提供相應資料庫的JDBC驅動程式。

如需建立JDBC驅動程式的OSGi組合的步驟，請參閱Apache Sling網站上的此[documentation](https://sling.apache.org/documentation/bundles/datasource-providers.html#convert-driver-jars-to-bundle)。

在捆綁包就位後，請遵循下列步驟以配置RDBAEM持久性：

1. 確保資料庫守護程式已啟動，並且您有一個活動資料庫可用於AEM。
1. 將6AEM.3 jar複製到安裝目錄。
1. 在安裝目錄中建立名為`crx-quickstart\install`的資料夾。
1. 通過在`crx-quickstart\install`目錄中建立具有以下名稱的配置檔案來配置文檔節點儲存：

   * `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

1. 通過在`crx-quickstart\install`資料夾中建立另一個具有以下名稱的配置檔案來配置資料源和JDBC參數：

   * `org.apache.sling.datasource.DataSourceFactory-oak.config`
   >[!NOTE]
   >
   >有關每個支援資料庫的資料源配置的詳細資訊，請參見[資料源配置選項](/help/sites-deploying/rdbms-support-in-aem.md#data-source-configuration-options)。

1. 接著，準備要與以下項目一起使用的JDBC OSGi捆綁包AEM:

   1. 在`crx-quickstart/install`資料夾中，建立名為`9`的資料夾。

   1. 將JDBCjar放在新資料夾中。

1. 最後，AEM從`crx3`和`crx3rdb`執行模式開始：

   ```java
   java -jar quickstart.jar -r crx3,crx3rdb
   ```

## 資料源配置選項{#data-source-configuration-options}

`org.apache.sling.datasource.DataSourceFactory-oak.config` OSGi配置用於配置在資料庫持久層之間通信所AEM需的參數。

可使用下列配置選項：

* `datasource.name:` 資料來源名稱。預設值為`oak`。

* `url:` 需要與JDBC一起使用的資料庫的URL字串。每個資料庫類型都有其自己的URL字串格式。 如需詳細資訊，請參閱下方的[URL字串格式](/help/sites-deploying/rdbms-support-in-aem.md#url-string-formats)。

* `driverClassName:` JDBC驅動程式類名。這將因您要使用的資料庫以及隨後連接到資料庫所需的驅動程式而異。 以下是支援的所有資料庫的類名AEM:

   * `org.postgresql.Driver` for PostgreSQL;
   * `com.ibm.db2.jcc.DB2Driver` DB2;
   * `oracle.jdbc.OracleDriver` oracle;
   * `com.mysql.jdbc.Driver` 對於MySQL和MariaDB（實驗性）;
   * c `om.microsoft.sqlserver.jdbc.SQLServerDriver` for Microsoft SQL Server（實驗性）。

* `username:` 資料庫運行的用戶名。

* `password:` 資料庫口令。

### URL字串格式{#url-string-formats}

根據需要使用的資料庫類型，資料源配置中會使用不同的URL字串格式。 以下是目前支援之資料庫的格AEM式清單：

* `jdbc:postgresql:databasename` for PostgreSQL;
* `jdbc:db2://localhost:port/databasename` DB2;
* `jdbc:oracle:thin:localhost:port:SID` oracle;
* `jdbc:mysql://localhost:3306/databasename` 對於MySQL和MariaDB（實驗性）;
* `jdbc:sqlserver://localhost:1453;databaseName=name` for Microsoft SQL Server（實驗性）。

## 已知限制{#known-limitations}

雖然RDBMS持久性支AEM持在單個資料庫上同時使用多個實例，但併發安裝則不支援。

為瞭解決這個問題，請務必先使用單一成員運行安裝，然後在完成安裝後添加其他成員。

