---
title: 連線到SQL資料庫
description: 存取外部SQL資料庫，讓您的AEM應用程式可以和資料互動
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 1082b2d7-2d1b-4c8c-a31d-effa403b21b2
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 0%

---

# 連線到SQL資料庫{#connecting-to-sql-databases}

存取外部SQL資料庫，讓您的CQ應用程式可以與資料互動：

1. [建立或取得匯出JDBC驅動程式套件的OSGi套件](#bundling-the-jdbc-database-driver)。
1. [設定JDBC資料來源集區提供者](#configuring-the-jdbc-connection-pool-service)。
1. [取得資料來源物件，並在您的程式碼中建立連線](#connecting-to-the-database)。

## 整合JDBC資料庫驅動程式 {#bundling-the-jdbc-database-driver}

某些資料庫廠商以OSGi套件組合提供JDBC驅動程式，例如[MySQL](https://dev.mysql.com/downloads/connector/j/)。 如果資料庫的JDBC驅動程式無法做為OSGi套件組合使用，請取得驅動程式JAR並將其包裝在OSGi套件組合中。 組合必須匯出與資料庫伺服器互動所需的套件。 組合也必須匯入它參照的套件。

下列範例使用Maven[&#128279;](https://felix.apache.org/documentation/subprojects/apache-felix-maven-bundle-plugin-bnd.html)的Bundle外掛程式將HSQLDB驅動程式包裝在OSGi套件中。 POM會指示外掛程式內嵌識別為相依性的hsqldb.jar檔案。 所有org.hsqldb套裝軟體都會匯出。

外掛程式會自動決定要匯入哪些套件，並將它們列在套件組合的MANIFEST.MF檔案中。 如果CQ伺服器上沒有任何套裝軟體，安裝時就不會啟動套裝軟體。 兩種可能的解決方案如下：

* 在POM中指出套件是選用的。 當JDBC連線實際上不需要封裝成員時，請使用此解決方案。 使用Import-Package元素來指示可選套件，如以下範例所示：

  `<Import-Package>org.jboss.*;resolution:=optional,*</Import-Package>`
* 將包含套件的JAR檔案包裝在匯出套件的OSGi套件組合中，並部署該套件。 當程式碼執行期間需要套件成員時，請使用此解決方案。

瞭解原始程式碼可讓您決定要使用哪個解決方案。 您也可以嘗試任一解決方案並執行測試以驗證解決方案。

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

* [Microsoft® SQL Server](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
* [Oracle](https://www.oracle.com/database/technologies/appdev/jdbc-downloads.html)
* [IBM® DB2®](https://www.ibm.com/support/pages/download-db2-fix-packs-version-db2-linux-unix-and-windows)

### 設定JDBC連線集區服務 {#configuring-the-jdbc-connection-pool-service}

新增使用JDBC驅動程式建立資料來源物件之「JDBC連線集區」服務的組態。 您的應用程式程式碼使用此服務來取得物件並連線到資料庫。

JDBC連線集區( `com.day.commons.datasource.jdbcpool.JdbcPoolService`)是工廠服務。 如果您需要使用不同屬性（例如唯讀或讀取/寫入存取權）的連線，請建立多個組態。

使用CQ時，有數種方法可管理此類服務的組態設定；如需完整詳細資訊，請參閱[設定OSGi](/help/sites-deploying/configuring-osgi.md)。

下列屬性可用於設定集區連線服務。 屬性名稱會在Web主控台中顯示。 `sling:OsgiConfig`節點的對應名稱會出現在括弧中。 顯示HSQLDB伺服器和別名為`mydb`之資料庫的範例值：

* JDBC驅動程式類別( `jdbc.driver.class`)：用來實作java.sql.Driver介面的Java™類別，例如`org.hsqldb.jdbc.JDBCDriver`。 資料型別為`String`。

* JDBC連線URI ( `jdbc.connection.uri`)：用來建立連線的資料庫URL，例如`jdbc:hsqldb:hsql//10.36.79.223:9001/mydb`。 URL的格式必須適用於java.sql.DriverManager類別的getConnection方法。 資料型別為`String`。

* 使用者名稱( `jdbc.username`)：用來向資料庫伺服器驗證的使用者名稱。 資料型別為`String`。

* 密碼( `jdbc.password`)：用來驗證使用者的密碼。 資料型別為`String`。

* 驗證查詢( `jdbc.validation.query`)：用來驗證連線是否成功的SQL陳述式，例如`select 1 from INFORMATION_SCHEMA.SYSTEM_USERS`。 資料型別為`String`。

* 預設為唯讀(default.readonly)：當您希望連線提供唯讀存取權時，請選取此選項。 資料型別為`Boolean`。
* 依預設自動認可( `default.autocommit`)：選取此選項可針對傳送至資料庫的每個SQL命令建立個別交易，且每個交易都會自動認可。 當您在程式碼中明確確認交易時，請勿選取此選項。 資料型別為`Boolean`。

* 集區大小( `pool.size`)：可供資料庫使用的同時連線數目。 資料型別為`Long`。

* 集區等待( `pool.max.wait.msec`)：連線要求逾時之前所經過的時間量。 資料型別為`Long`。

* 資料來源名稱( `datasource.name`)：此資料來源的名稱。 資料型別為`String`。

* 其他服務屬性( `datasource.svc.properties`)：要附加至連線URL的一組名稱/值組。 資料型別為`String[]`。

JDBC連線集區服務是工廠服務。 因此，如果您使用`sling:OsgiConfig`節點來設定連線服務，節點的名稱必須包含工廠服務PID，後面接著&#x200B;*`-alias`*。 您使用的別名在該PID的所有設定節點中必須是唯一的。 範例節點名稱是`com.day.commons.datasource.jdbcpool.JdbcPoolService-myhsqldbpool`。

![chlimage_1-7](assets/chlimage_1-7a.png)

### 連線到資料庫 {#connecting-to-the-database}

在您的Java™程式碼中，使用DataSourcePool服務取得您建立之組態的`javax.sql.DataSource`物件。 DataSourcePool服務提供傳回指定資料來源名稱`DataSource`物件的`getDataSource`方法。 作為方法引數，請使用您為JDBC連線集區組態指定的資料來源名稱（或`datasource.name`）屬性值。

下列範例JSP程式碼會取得hsqldbds資料來源的執行個體、執行簡單的SQL查詢，並顯示傳回的結果數目。

#### 執行資料庫查閱的JSP {#jsp-that-performs-a-database-lookup}

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
>如果getDataSource方法因找不到資料來源而擲回例外狀況，請確定連線集區服務設定正確。 驗證屬性名稱、值和資料型別。
>

<!-- Link below redirects to the "Get started with AEM Sites - WKND tutorial"
>[!NOTE]
>
>To learn how to inject a DataSourcePool into an OSGi bundle, see [Injecting a DataSourcePool Service into an Adobe Experience Manager OSGi bundle](https://helpx.adobe.com/experience-manager/using/datasourcepool.html). -->
