---
title: 連接到SQL資料庫
seo-title: Connecting to SQL Databases
description: 存取外部SQL資料庫，以便您的AEM應用程式與資料互動
seo-description: Access an external SQL database to so that your AEM applications can interact with the data
uuid: 0af0ed08-9487-4c37-87ce-049c9b4c1ea2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 11a11803-bce4-4099-9b50-92327608f37b
exl-id: 1082b2d7-2d1b-4c8c-a31d-effa403b21b2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---

# 連接到SQL資料庫{#connecting-to-sql-databases}

存取外部SQL資料庫，以便您的CQ應用程式可與資料互動：

1. [建立或獲取導出JDBC驅動程式包的OSGi包](#bundling-the-jdbc-database-driver).
1. [配置JDBC資料源池提供程式](#configuring-the-jdbc-connection-pool-service).
1. [取得資料來源物件並在程式碼中建立連線](#connecting-to-the-database).

## 綁定JDBC資料庫驅動程式 {#bundling-the-jdbc-database-driver}

某些資料庫供應商在OSGi捆綁包中提供JDBC驅動程式，例如 [MySQL](https://www.mysql.com/downloads/connector/j/). 如果資料庫的JDBC驅動程式不能作為OSGi包，請獲取驅動程式JAR，並將其包裝在OSGi包中。 該套件必須導出與資料庫伺服器交互所需的包。 套件組合也必須匯入其參照的套件。

下列範例使用 [適用於Maven的套件組合外掛程式](https://felix.apache.org/site/apache-felix-maven-bundle-plugin-bnd.html) 將HSQLDB驅動程式包裝在OSGi捆綁包中。 POM會指示外掛程式內嵌識別為相依性的hsqldb.jar檔案。 所有org.hsqldb包都導出。

外掛程式會自動判斷要匯入的套件，並將其列在套件組合的MANIFEST.MF檔案中。 如果CQ伺服器上沒有任何套件，則安裝時不會啟動套件組合。 兩種可能的解決方案如下：

* 在POM中指出這些套件為選用。 當JDBC連接實際上不需要包成員時，請使用此解決方案。 使用Import-Package元素來指示可選包，如以下示例所示：

   `<Import-Package>org.jboss.*;resolution:=optional,*</Import-Package>`
* 包裝JAR檔案，這些檔案包含匯出套件的OSGi套件組合中的套件，然後部署套件組合。 當程式碼執行期間需要套件成員時，請使用此解決方案。

您對原始碼的了解可讓您決定要使用哪個解決方案。 您也可以嘗試任一解決方案並執行測試以驗證解決方案。

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

下列連結會開啟某些熱門資料庫產品的下載頁面：

* [Microsoft SQL Server](https://www.microsoft.com/en-us/download/details.aspx?displaylang=en&amp;id=11774)
* [Oracle](https://www.oracle.com/technetwork/database/features/jdbc/index-091264.html)
* [IBM DB2](https://www-01.ibm.com/support/docview.wss?uid=swg27007053)

### 配置JDBC連接池服務 {#configuring-the-jdbc-connection-pool-service}

為使用JDBC驅動程式建立資料源對象的JDBC連接池服務添加配置。 您的應用程式代碼使用此服務來獲取對象並連接到資料庫。

JDBC連接池( `com.day.commons.datasource.jdbcpool.JdbcPoolService`)是工廠服務。 如果您需要使用不同屬性（例如只讀或讀/寫訪問）的連接，請建立多個配置。

使用CQ時，有數種方法可管理這類服務的組態設定；請參閱 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以取得完整詳細資訊。

以下屬性可用於配置池連接服務。 屬性名稱會如Web控制台中的顯示一樣列出。 的對應名稱 `sling:OsgiConfig` 節點以括弧顯示。 顯示了HSQLDB伺服器和具有別名的資料庫的示例值 `mydb`:

* JDBC驅動程式類( `jdbc.driver.class`):用於實現java.sql.Driver介面的Java類，例如 `org.hsqldb.jdbc.JDBCDriver`. 資料類型為 `String`.

* JDBC連接URI( `jdbc.connection.uri`):用於建立連接的資料庫的URL，例如 `jdbc:hsqldb:hsql//10.36.79.223:9001/mydb`. URL的格式必須有效，才能與java.sql.DriverManager類的getConnection方法一起使用。 資料類型為 `String`.

* 使用者名稱( `jdbc.username`):用於與資料庫伺服器進行身份驗證的用戶名。 資料類型為 `String`.

* 密碼( `jdbc.password`):用於驗證用戶的密碼。 資料類型為 `String`.

* 驗證查詢( `jdbc.validation.query`):用於驗證連接是否成功的SQL陳述式，例如 `select 1 from INFORMATION_SCHEMA.SYSTEM_USERS`. 資料類型為 `String`.

* 預設為Readonly(default.readonly):當希望連接提供只讀訪問時，選擇此選項。 資料類型為 `Boolean`.
* 預設情況下自動提交( `default.autocommit`):選擇此選項可為發送到資料庫的每個SQL命令建立單獨的事務，並自動提交每個事務。 在代碼中顯式提交事務時，請勿選擇此選項。 資料類型為 `Boolean`.

* 池大小( `pool.size`):要提供給資料庫的同時連接的數量。 資料類型為 `Long`.

* 池等待( `pool.max.wait.msec`):連線請求逾時前的時間。 資料類型為 `Long`.

* 資料源名稱( `datasource.name`):此資料源的名稱。 資料類型為 `String`.

* 其他服務屬性( `datasource.svc.properties`):您要附加至連線URL的一組名稱/值組。 資料類型為 `String[]`.

JDBC連接池服務是工廠。 因此，若您使用 `sling:OsgiConfig` 要配置連接服務的節點，節點的名稱必須包括工廠服務PID，後面跟 *`-alias`*. 您使用的別名對於該PID的所有配置節點都必須是唯一的。 節點名稱的範例為 `com.day.commons.datasource.jdbcpool.JdbcPoolService-myhsqldbpool`.

![chlimage_1-7](assets/chlimage_1-7a.png)

### 連接到資料庫 {#connecting-to-the-database}

在Java代碼中，使用DataSourcePool服務來獲取 `javax.sql.DataSource` 物件。 DataSourcePool服務提供 `getDataSource` 傳回 `DataSource` 給定資料源名稱的對象。 作為方法參數，請使用資料源名稱的值(或 `datasource.name`)為JDBC連接池配置指定的屬性。

以下示例JSP代碼獲取hsqldbds資料源的實例，執行簡單的SQL查詢，並顯示返回的結果數。

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
>如果getDataSource方法由於找不到資料源而擲回例外狀況，請確保連接池服務配置正確。 驗證屬性名稱、值和資料類型。

>[!NOTE]
>
>要了解如何將DataSourcePool插入OSGi捆綁包，請參閱 [將DataSourcePool服務注入Adobe Experience Manager OSGi套件組合](https://helpx.adobe.com/experience-manager/using/datasourcepool.html).
