---
title: 連接到SQL資料庫
seo-title: 連接到SQL資料庫
description: 存取外部SQL資料庫，讓您的AEM應用程式可與資料互動
seo-description: 存取外部SQL資料庫，讓您的AEM應用程式可與資料互動
uuid: 0af0ed08-9487-4c37-87ce-049c9b4c1ea2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 11a11803-bce4-4099-9b50-92327608f37b
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71

---


# 連接到SQL資料庫{#connecting-to-sql-databases}

存取外部SQL資料庫，讓您的CQ應用程式可與資料互動：

1. [建立或獲取導出JDBC驅動程式包的OSGi包](#bundling-the-jdbc-database-driver)。
1. [配置JDBC資料源池提供程式](#configuring-the-jdbc-connection-pool-service)。
1. [取得資料來源物件並在程式碼中建立連線](#connecting-to-the-database)。

## 捆綁JDBC資料庫驅動程式 {#bundling-the-jdbc-database-driver}

某些資料庫供應商在OSGi包中提供JDBC驅動程式，例如 [MySQL](https://www.mysql.com/downloads/connector/j/)。 如果資料庫的JDBC驅動程式不能作為OSGi包，請獲取驅動程式JAR並將其包在OSGi包中。 Bundle必須導出與資料庫伺服器交互所需的包。 包還必須導入它引用的包。

以下示例使用 [Maven的Bundle插件](https://felix.apache.org/site/apache-felix-maven-bundle-plugin-bnd.html) ，將HSQLDB驅動程式包在OSGi包中。 POM指示插件嵌入標識為相關性的hsqldb.jar檔案。 所有org.hsqldb包都將導出。

外掛程式會自動決定要匯入的封裝，並將它們列在封裝的MANIFEST.MF檔案中。 如果CQ伺服器上沒有任何軟體包，則在安裝時將不啟動軟體包。 兩種可能的解決方案如下：

* 在POM中指出包是可選的。 當JDBC連接實際上不需要包成員時，請使用此解決方案。 使用Import-Package元素來指示可選包，如下例所示：

   `<Import-Package>org.jboss.*;resolution:=optional,*</Import-Package>`
* 將包含包的JAR檔案包裝在導出包的OSGi包中，並部署包。 當代碼執行期間需要包成員時，請使用此解決方案。

瞭解原始碼後，您就可決定要使用哪一種解決方案。 您也可以試用任一解決方案並執行測試以驗證解決方案。

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

下列連結會開啟某些常用資料庫產品的下載頁面：

* [Microsoft SQL Server](https://www.microsoft.com/en-us/download/details.aspx?displaylang=en&id=11774)
* [Oracle](https://www.oracle.com/technetwork/database/features/jdbc/index-091264.html)
* [IBM DB2](https://www-01.ibm.com/support/docview.wss?uid=swg27007053)

### 配置JDBC連接池服務 {#configuring-the-jdbc-connection-pool-service}

為使用JDBC驅動程式建立資料源對象的JDBC連接池服務添加配置。 您的應用程式碼使用此服務獲取對象並連接到資料庫。

JDBC連接池( `com.day.commons.datasource.jdbcpool.JdbcPoolService`)是工廠服務。 如果需要使用不同屬性（例如只讀或讀／寫訪問）的連接，請建立多個配置。

使用CQ時，管理此類服務的配置設定有幾種方法；如需 [完整詳細資訊](/help/sites-deploying/configuring-osgi.md) ，請參閱設定OSGi。

以下屬性可用於配置共用連接服務。 屬性名稱會列在Web控制台中顯示的位置。 節點的相應名稱將 `sling:OsgiConfig` 顯示在括弧中。 HSQLDB伺服器和別名為：的資料庫的示例值如 `mydb`下：

* JDBC驅動程式類( `jdbc.driver.class`):例如，用於實現java.sql.Driver介面的Java類 `org.hsqldb.jdbc.JDBCDriver`。 資料類型為 `String`。

* JDBC連接URI( `jdbc.connection.uri`):用於建立連接的資料庫的URL，例如 `jdbc:hsqldb:hsql//10.36.79.223:9001/mydb`。 URL的格式必須有效，才能與java.sql.DriverManager類的getConnection方法一起使用。 資料類型為 `String`。

* 用戶名( `jdbc.username`):用於向資料庫伺服器驗證的用戶名。 資料類型為 `String`。

* 密碼( `jdbc.password`):用於用戶驗證的密碼。 資料類型為 `String`。

* 驗證查詢( `jdbc.validation.query`):用於驗證連接是否成功的SQL陳述式，例如 `select 1 from INFORMATION_SCHEMA.SYSTEM_USERS`。 資料類型為 `String`。

* 預設情況下為只讀(default.readonly):當您希望連接提供只讀訪問時，請選擇此選項。 資料類型為 `Boolean`。
* 預設情況下自動提交( `default.autocommit`):選擇此選項可為發送到資料庫的每個SQL命令建立單獨的事務，並自動提交每個事務。 在代碼中明確提交事務時，請不要選擇此選項。 資料類型為 `Boolean`。

* 池大小( `pool.size`):要為資料庫提供的同時連接數。 資料類型為 `Long`。

* 池等待( `pool.max.wait.msec`):連線要求逾時前的時間量。 資料類型為 `Long`。

* 資料來源名稱( `datasource.name`):此資料源的名稱。 資料類型為 `String`。

* 其他服務屬性( `datasource.svc.properties`):要附加至連線URL的一組名稱／值配對。 資料類型為 `String[]`。

JDBC連接池服務是工廠。 因此，如果使用節 `sling:OsgiConfig` 點配置連接服務，則節點的名稱必須包括工廠服務PID，後面跟 *`-alias`*。 對於該PID的所有配置節點，您使用的別名必須是唯一的。 節點名稱示例為 `com.day.commons.datasource.jdbcpool.JdbcPoolService-myhsqldbpool`。

![chlimage_1-7](assets/chlimage_1-7a.png)

### 連接到資料庫 {#connecting-to-the-database}

在Java代碼中，使用DataSourcePool服務獲取所 `javax.sql.DataSource` 建立配置的對象。 DataSourcePool服務提供了返 `getDataSource` 回給定資料源名 `DataSource` 稱的對象的方法。 作為方法參數，請使用為JDBC連接池配置指定的Datasource Name( `datasource.name`或)屬性的值。

以下示例JSP代碼獲取hsqldbds資料源的實例，執行簡單SQL查詢，並顯示返回的結果數。

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
>如果getDataSource方法由於找不到資料來源而引發異常，請確定連線池服務設定正確。 驗證屬性名稱、值和資料類型。


>[!NOTE]
>
>如要瞭解如何將DataSourcePool注入OSGi套裝，請參 [閱將DataSourcePool服務注入Adobe Experience Manager OSGi套裝](https://helpx.adobe.com/experience-manager/using/datasourcepool.html)。

