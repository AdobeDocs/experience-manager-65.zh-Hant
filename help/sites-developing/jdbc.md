---
title: 連接到SQL資料庫
seo-title: Connecting to SQL Databases
description: 訪問外部SQL資料庫，以便您的AEM應用程式可以與資料交互
seo-description: Access an external SQL database to so that your AEM applications can interact with the data
uuid: 0af0ed08-9487-4c37-87ce-049c9b4c1ea2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 11a11803-bce4-4099-9b50-92327608f37b
exl-id: 1082b2d7-2d1b-4c8c-a31d-effa403b21b2
source-git-commit: e147605ff4d5c3d2403632285956559db235c084
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 0%

---

# 連接到SQL資料庫{#connecting-to-sql-databases}

訪問外部SQL資料庫，以便您的CQ應用程式可以與資料交互：

1. [建立或獲取導出JDBC驅動程式包的OSGi捆綁包](#bundling-the-jdbc-database-driver)。
1. [配置JDBC資料源池提供程式](#configuring-the-jdbc-connection-pool-service)。
1. [獲取資料源對象並在代碼中建立連接](#connecting-to-the-database)。

## 捆綁JDBC資料庫驅動程式 {#bundling-the-jdbc-database-driver}

一些資料庫供應商在OSGi捆綁包中提供JDBC驅動程式，例如 [MySQL](https://dev.mysql.com/downloads/connector/j/)。 如果資料庫的JDBC驅動程式不能作為OSGi包使用，請獲取驅動程式JAR並將其包裝在OSGi包中。 該捆綁包必須導出與資料庫伺服器交互所需的包。 束還必須導入它引用的包。

以下示例使用 [用於Maven的捆綁插件](https://felix.apache.org/documentation/subprojects/apache-felix-maven-bundle-plugin-bnd.html) 將HSQLDB驅動程式包裝到OSGi包中。 POM指示插件嵌入標識為依賴項的hsqldb.jar檔案。 所有org.hsqldb包都將導出。

插件自動確定要導入的包，並將它們列在包的MANIFEST.MF檔案中。 如果CQ伺服器上沒有任何軟體包，則該軟體包不會在安裝時啟動。 兩種可能的解決方案如下：

* 在POM中指明包是可選的。 當JDBC連接實際上不需要包成員時，請使用此解決方案。 使用Import-Package元素指示可選包，如以下示例所示：

   `<Import-Package>org.jboss.*;resolution:=optional,*</Import-Package>`
* 將包含在導出包的OSGi捆綁包中的包的JAR檔案包裝，並部署該捆綁包。 在代碼執行過程中需要包成員時，請使用此解決方案。

通過瞭解原始碼，您可以決定使用哪個解決方案。 您還可以嘗試任一解決方案並執行測試以驗證該解決方案。

### 捆綁hsqldb.jar的POM {#pom-that-bundles-hsqldb-jar}

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>hsqldb-jdbc-driver-bundle</artifactId>
  <version>0.0.1-SNAPSHOT</version>
  <name>wrapper-bundle-hsqldb-driver</name>
  <url>www.adobe.com</url>
  <description>Exports the HSQL JDBC driver</description>
  <packaging>bundle</packaging>
  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  </properties>
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.felix</groupId>
        <artifactId>maven-bundle-plugin</artifactId>
        <version>1.4.3</version>
        <extensions>true</extensions>
        <configuration>
         <instructions>
            <Embed-Dependency>*</Embed-Dependency>
            <_exportcontents>org.hsqldb.*</_exportcontents>
          </instructions>
        </configuration>
      </plugin>
    </plugins>
  </build>
  <dependencies>
    <dependency>
      <groupId>hsqldb</groupId>
      <artifactId>hsqldb</artifactId>
      <version>2.2.9</version>
    </dependency>
  </dependencies>
</project>
```

以下連結開啟某些常用資料庫產品的下載頁：

* [Microsoft® SQL Server](https://www.microsoft.com/en-us/download/details.aspx?displaylang=en&amp;id=11774)
* [Oracle](https://www.oracle.com/database/technologies/appdev/jdbc-downloads.html)
* [IBM® DB2®](https://www.ibm.com/support/pages/download-db2-fix-packs-version-db2-linux-unix-and-windows)

### 配置JDBC連接池服務 {#configuring-the-jdbc-connection-pool-service}

為JDBC連接池服務添加配置，該服務使用JDBC驅動程式建立資料源對象。 應用程式碼使用此服務獲取對象並連接到資料庫。

JDBC連接池( `com.day.commons.datasource.jdbcpool.JdbcPoolService`)是出廠服務。 如果需要使用不同屬性的連接，例如只讀或讀/寫訪問，請建立多個配置。

使用CQ時，有幾種方法管理此類服務的配置設定；見 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 的雙曲餘切值。

以下屬性可用於配置池連接服務。 屬性名稱在Web控制台中顯示時列出。 對應的名稱 `sling:OsgiConfig` 節點出現在括弧中。 HSQLDB伺服器和別名為 `mydb`:

* JDBC驅動程式類( `jdbc.driver.class`):用於實現java.sql.Driver介面的Java™類，例如 `org.hsqldb.jdbc.JDBCDriver`。 資料類型為 `String`。

* JDBC連接URI( `jdbc.connection.uri`):用於建立連接的資料庫的URL，例如 `jdbc:hsqldb:hsql//10.36.79.223:9001/mydb`。 URL的格式必須有效，才能與java.sql.DriverManager類的getConnection方法一起使用。 資料類型為 `String`。

* 用戶名( `jdbc.username`):用於向資料庫伺服器進行身份驗證的用戶名。 資料類型為 `String`。

* 密碼( `jdbc.password`):用於用戶身份驗證的密碼。 資料類型為 `String`。

* 驗證查詢( `jdbc.validation.query`):用於驗證連接是否成功的SQL陳述式，例如 `select 1 from INFORMATION_SCHEMA.SYSTEM_USERS`。 資料類型為 `String`。

* 預設情況下只讀(default.readonly):當希望連接提供只讀訪問時，選擇此選項。 資料類型為 `Boolean`。
* 預設情況下自動提交( `default.autocommit`):選擇此選項可為發送到資料庫的每個SQL命令建立單獨的事務，並自動提交每個事務。 在代碼中顯式提交事務時，不要選擇此選項。 資料類型為 `Boolean`。

* 池大小( `pool.size`):要為資料庫提供的同時連接數。 資料類型為 `Long`。

* 池等待( `pool.max.wait.msec`):連接請求超時之前的時間。 資料類型為 `Long`。

* 資料源名稱( `datasource.name`):此資料源的名稱。 資料類型為 `String`。

* 其他服務屬性( `datasource.svc.properties`):要附加到連接URL的一組名稱/值對。 資料類型為 `String[]`。

JDBC連接池服務是工廠。 因此，如果您使用 `sling:OsgiConfig` 要配置連接服務的節點，節點的名稱必須包括出廠服務PID ，然後是 *`-alias`*。 對於該PID的所有配置節點，您使用的別名必須唯一。 示例節點名稱為 `com.day.commons.datasource.jdbcpool.JdbcPoolService-myhsqldbpool`。

![chlimage_1-7](assets/chlimage_1-7a.png)

### 連接到資料庫 {#connecting-to-the-database}

在Java™代碼中，使用DataSourcePool服務獲取 `javax.sql.DataSource` 對象。 DataSourcePool服務提供 `getDataSource` 方法返回 `DataSource` 給定資料源名稱的對象。 作為方法參數，使用資料源名稱(或 `datasource.name`)屬性。

下面的示例JSP代碼獲取hsqldbds資料源的實例，執行簡單的SQL查詢，並顯示返回的結果數。

#### 執行資料庫查找的JSP {#jsp-that-performs-a-database-lookup}

```java
<%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false"%><%
%><%@ page import="com.day.commons.datasource.poolservice.DataSourcePool" %><%
%><%@ page import="javax.sql.DataSource" %><%
%><%@ page import="java.sql.Connection" %><%
%><%@ page import="java.sql.SQLException" %><%
%><%@ page import="java.sql.Statement" %><%
%><%@ page import="java.sql.ResultSet"%><%
%><html>
<cq:include script="head.jsp"/>
<body>
<%DataSourcePool dspService = sling.getService(DataSourcePool.class);
  try {
     DataSource ds = (DataSource) dspService.getDataSource("hsqldbds");
     if(ds != null) {
         %><p>Obtained the datasource!</p><%
         %><%final Connection connection = ds.getConnection();
          final Statement statement = connection.createStatement();
          final ResultSet resultSet = statement.executeQuery("SELECT * from INFORMATION_SCHEMA.SYSTEM_USERS");
          int r=0;
          while(resultSet.next()){
             r=r+1;
          }
          resultSet.close();
          %><p>Number of results: <%=r%></p><%
      }
   }catch (Exception e) {
        %><p>error! <%=e.getMessage()%></p><%
    }
%></body>
</html>
```

>[!NOTE]
>
>如果getDataSource方法由於找不到資料源而引發異常，請確保連接池服務配置正確。 驗證屬性名稱、值和資料類型。

<!-- Link below redirects to the "Get started with AEM Sites - WKND tutorial"
>[!NOTE]
>
>To learn how to inject a DataSourcePool into an OSGi bundle, see [Injecting a DataSourcePool Service into an Adobe Experience Manager OSGi bundle](https://helpx.adobe.com/experience-manager/using/datasourcepool.html). -->
