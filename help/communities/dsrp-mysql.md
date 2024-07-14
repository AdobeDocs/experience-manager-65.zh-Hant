---
title: DSRP的MySQL組態
description: 如何連線至MySQL伺服器並建立UGC資料庫
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: eafb60be-2963-4ac9-8618-50fd9bc6fe6c
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 0%

---

# DSRP的MySQL組態 {#mysql-configuration-for-dsrp}

MySQL是關聯式資料庫，可用來儲存使用者產生的內容(UGC)。

這些指示說明如何連線至MySQL伺服器及建立UGC資料庫。

## 要求 {#requirements}

* [最新Communities Feature Pack](deploy-communities.md#latestfeaturepack)
* [MySQL的JDBC驅動程式](deploy-communities.md#jdbc-driver-for-mysql)
* 關聯式資料庫：

   * [MySQL server](https://dev.mysql.com/downloads/mysql/) Community Server 5.6或更新版本

      * 可以在與AEM相同的主機上執行或遠端執行

   * [MySQL Workbench](https://dev.mysql.com/downloads/tools/workbench/)

## 安裝MySQL {#installing-mysql}

[MySQL](https://dev.mysql.com/downloads/mysql/)應該依照目標作業系統的指示下載並安裝。

### 小寫表格名稱 {#lower-case-table-names}

由於SQL不區分大小寫，因此對於區分大小寫的作業系統，必須包含設定以小寫所有資料表名稱。

例如，若要指定Linux作業系統上的所有小寫表格名稱：

* 編輯檔案`/etc/my.cnf`
* 在`[mysqld]`區段中，新增下列行：

  `lower_case_table_names = 1`

### UTF8字元集 {#utf-character-set}

若要提供更好的多語言支援，必須使用UTF8字元集。

變更MySQL以使用UTF8作為其字元集：

* mysql >設定名稱&#39;utf8&#39;；

將MySQL資料庫變更為預設的UTF8：

* 編輯檔案`/etc/my.cnf`
* 在`[client]`區段中，新增下列行：

  `default-character-set=utf8`

* 在`[mysqld]`區段中，新增下列行：

  `character-set-server=utf8`

## 安裝MySQL Workbench {#installing-mysql-workbench}

MySQL Workbench提供UI，用於執行安裝結構描述和初始資料的SQL指令碼。

MySQL Workbench應按照目標作業系統的指示下載及安裝。

## 社群連線 {#communities-connection}

MySQL Workbench初次啟動時，除非已用於其他用途，否則不會顯示任何連線：

![mysqlconnection](assets/mysqlconnection.png)

### 新連線設定 {#new-connection-settings}

1. 選取`MySQL Connections`右側的`+`圖示。
1. 在對話方塊`Setup New Connection`中，輸入適合您平台的值

   為了示範，將作者AEM例項和MySQL放在相同伺服器上：

   * 連線名稱： `Communities`
   * 連線方法： `Standard (TCP/IP)`
   * 主機名稱： `127.0.0.1`
   * 使用者名稱： `root`
   * 密碼： `no password by default`
   * 預設結構描述： `leave blank`

1. 選取`Test Connection`以驗證與執行中MySQL服務的連線

**附註**：

* 預設連線埠為`3306`
* 在[JDBC OSGi組態](#configurejdbcconnections)中，已將選取的連線名稱輸入為資料來源名稱

#### 新社群連線 {#new-communities-connection}

![社群連線](assets/community-connection.png)

## 資料庫設定 {#database-setup}

開啟Communities連線以安裝資料庫。

![安裝資料庫](assets/install-database.png)

### 取得SQL指令碼 {#obtain-the-sql-script}

SQL指令碼是從AEM存放庫取得：

1. 瀏覽至CRXDE Lite

   * 例如，[http://localhost:4502/crx/de](http://localhost:4502/crx/de)

1. 選取/libs/social/config/datastore/dsrp/schema資料夾
1. 下載`init-schema.sql`

   ![database-schema-crxde](assets/database-schema-crxde.png)

下載結構描述的一種方法是：

* 選取SQL檔案的`jcr:content`節點
* 請注意，`jcr:data`屬性的值是一個檢視連結

* 選取檢視連結，將資料儲存至本機檔案

### 建立DSRP資料庫 {#create-the-dsrp-database}

請依照下列步驟安裝資料庫。 資料庫的預設名稱為`communities`。

如果指令碼中的資料庫名稱已變更，請務必也在[JDBC設定](#configurejdbcconnections)中加以變更。

#### 步驟1：開啟SQL檔案 {#step-open-sql-file}

在MySQL Workbench

* 從[檔案]下拉式功能表中，選取&#x200B;**[!UICONTROL 開啟SQL指令碼]**&#x200B;選項
* 選取下載的`init_schema.sql`指令碼

![select-sql-script](assets/select-sql-script.png)

#### 步驟2：執行SQL指令碼 {#step-execute-sql-script}

在步驟1中開啟之檔案的Workbench視窗中，選取`lightening (flash) icon`以執行指令碼。

在下列影像中，`init_schema.sql`檔案已準備就緒可供執行：

![execute-sql-script](assets/execute-sql-script.png)

#### 重新整理 {#refresh}

執行指令碼後，必須重新整理`Navigator`的`SCHEMAS`區段才能檢視新資料庫。 使用「結構描述」右側的重新整理圖示：

![重新整理結構描述](assets/refresh-schema.png)

## 設定JDBC連線 {#configure-jdbc-connection}

**Day Commons JDBC連線集區**&#x200B;的OSGi設定會設定MySQL JDBC驅動程式。

所有發佈與編寫AEM執行個體都應指向相同的MySQL伺服器。

當MySQL在與AEM不同的伺服器上執行時，必須指定伺服器主機名稱，以取代JDBC聯結器中的&#39;localhost&#39;。

* 在每個作者和發佈AEM例項上。
* 以系統管理員許可權登入。
* 存取[網頁主控台](../../help/sites-deploying/configuring-osgi.md)。

   * 例如，[http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)

* 找到`Day Commons JDBC Connections Pool`
* 選取`+`圖示以建立連線設定。

  ![configure-jdbc-connection](assets/configure-jdbc-connection.png)

* 輸入下列值：

   * **[!UICONTROL JDBC驅動程式類別]**： `com.mysql.jdbc.Driver`
   * **[!UICONTROL JDBC連線URI]**： `jdbc:mysql://localhost:3306/communities?characterEncoding=UTF-8`

     如果MySQL伺服器與&#39;this&#39;AEM伺服器&#x200B;*communities*&#x200B;不是預設資料庫（結構描述）名稱，請指定伺服器來取代localhost。

   * **[!UICONTROL 使用者名稱]**： `root`

     或者輸入MySQL伺服器的設定使用者名稱（如果不是&#39;root&#39;）。

   * **[!UICONTROL 密碼]**：

     如果沒有為MySQL設定密碼，請清除此欄位，

     否則請輸入MySQL使用者名稱的設定密碼。

   * **[!UICONTROL 資料來源名稱]**：為[MySQL連線](#new-connection-settings)輸入的名稱，例如，&#39;communities&#39;。

* 選取&#x200B;**[!UICONTROL 儲存]**
