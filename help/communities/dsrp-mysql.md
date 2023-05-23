---
title: 用於DSRP的MySQL配置
seo-title: MySQL Configuration for DSRP
description: 如何連接到MySQL伺服器並建立UGC資料庫
seo-description: How to connect to the MySQL server and establish the UGC database
uuid: c058cc88-7ca2-4aed-9a36-b080e603f886
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: edc3043c-7ec4-4e4a-b008-95f1784f012e
role: Admin
exl-id: eafb60be-2963-4ac9-8618-50fd9bc6fe6c
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 0%

---

# 用於DSRP的MySQL配置 {#mysql-configuration-for-dsrp}

MySQL是一個關係資料庫，可用於儲存用戶生成的內容(UGC)。

這些說明描述了如何連接到MySQL伺服器和建立UGC資料庫。

## 要求 {#requirements}

* [最新社區功能包](deploy-communities.md#latestfeaturepack)
* [MySQL的JDBC驅動程式](deploy-communities.md#jdbc-driver-for-mysql)
* 關係資料庫：

   * [MySQL伺服器](https://dev.mysql.com/downloads/mysql/) 社區伺服器5.6版或更高版本

      * 可以在與同一主機上運行，也AEM可以遠程運行
   * [MySQL工作台](https://dev.mysql.com/downloads/tools/workbench/)


## 安裝MySQL {#installing-mysql}

[MySQL](https://dev.mysql.com/downloads/mysql/) 應按照目標作業系統的說明下載並安裝。

### 小寫表名 {#lower-case-table-names}

由於SQL不區分大小寫，因此對於區分大小寫的作業系統，必須包含一個設定，以便將所有表名都小寫。

例如，要指定Linux OS上所有小寫表名：

* 編輯檔案 `/etc/my.cnf`
* 在 `[mysqld]` ，添加以下行：

   `lower_case_table_names = 1`

### UTF8字元集 {#utf-character-set}

要提供更好的多語言支援，必須使用UTF8字元集。

將MySQL更改為將UTF8作為其字元集：

* mysql > SET NAMES &#39;utf8&#39;;

將MySQL資料庫更改為預設UTF8:

* 編輯檔案 `/etc/my.cnf`
* 在 `[client]` ，添加以下行：

   `default-character-set=utf8`

* 在 `[mysqld]` ，添加以下行：

   `character-set-server=utf8`

## 安裝MySQL Workbench {#installing-mysql-workbench}

MySQL Workbench提供了用於執行安裝架構和初始資料的SQL指令碼的UI。

MySQL Workbench應按照目標OS的說明下載和安裝。

## 社區連接 {#communities-connection}

當MySQL Workbench首次啟動時，除非已用於其他目的，否則它尚不顯示任何連接：

![mysqlconnection](assets/mysqlconnection.png)

### 新建連接設定 {#new-connection-settings}

1. 選擇 `+` 表徵圖 `MySQL Connections`。
1. 在對話框中 `Setup New Connection`，輸入適合您的平台的值

   為了進行演示，將作者實AEM例和MySQL放在同一伺服器上：

   * 連接名稱： `Communities`
   * 連接方法： `Standard (TCP/IP)`
   * 主機名： `127.0.0.1`
   * 使用者名稱: `root`
   * 密碼: `no password by default`
   * 預設架構： `leave blank`

1. 選擇 `Test Connection` 驗證與正在運行的MySQL服務的連接

**附註**:

* 預設埠為 `3306`
* 選擇的連接名稱將作為資料源名稱輸入 [JDBC OSGi配置](#configurejdbcconnections)

#### 新建社區連接 {#new-communities-connection}

![社區連接](assets/community-connection.png)

## 資料庫設定 {#database-setup}

開啟社區連接以安裝資料庫。

![安裝資料庫](assets/install-database.png)

### 獲取SQL指令碼 {#obtain-the-sql-script}

SQL指令碼是從儲存庫獲取AEM的：

1. 瀏覽到CRXDE Lite

   * 比如說， [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

1. 選擇/libs/social/config/datastore/dsrp/schema資料夾
1. 下載 `init-schema.sql`

   ![資料庫模式 — crxde](assets/database-schema-crxde.png)

下載架構的一種方法是：

* 選擇 `jcr:content` sql檔案的節點
* 注意 `jcr:data` 屬性是視圖連結

* 選擇視圖連結以將資料保存到本地檔案

### 建立DSRP資料庫 {#create-the-dsrp-database}

按照以下步驟安裝資料庫。 資料庫的預設名稱為 `communities`。

如果在指令碼中更改了資料庫名稱，請確保在 [JDBC配置](#configurejdbcconnections)。

#### 步驟1:開啟SQL檔案 {#step-open-sql-file}

在MySQL工作台中

* 從「檔案」下拉菜單中，選擇 **[!UICONTROL 開啟SQL指令碼]** 選項
* 選擇下載的 `init_schema.sql` 指令碼

![select-sql-script](assets/select-sql-script.png)

#### 步驟2:執行SQL指令碼 {#step-execute-sql-script}

在步驟1中開啟的檔案的「工作台」窗口中，選擇 `lightening (flash) icon` 執行指令碼。

在下圖中， `init_schema.sql` 檔案已準備好執行：

![execute-sql-script](assets/execute-sql-script.png)

#### 重新整理 {#refresh}

執行指令碼後，必須刷新 `SCHEMAS` 的下界 `Navigator` 來查看新資料庫。 使用「SCHEMAS」右側的刷新表徵圖：

![刷新模式](assets/refresh-schema.png)

## 配置JDBC連接 {#configure-jdbc-connection}

OSGi配置 **日公共JDBC連接池** 配置MySQL JDBC驅動程式。

所有發佈和作AEM者實例都應指向同一MySQL伺服器。

當MySQL在與之不同的伺服器上運行AEM時，必須指定伺服器主機名，而不是JDBC連接器中的「localhost」。

* 每個作者和發佈AEM實例。
* 以管理員權限登錄。
* 訪問 [Web控制台](../../help/sites-deploying/configuring-osgi.md)。

   * 比如說， [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)

* 查找 `Day Commons JDBC Connections Pool`
* 選擇 `+` 表徵圖以建立新連接配置。

   ![配置 — jdbc — 連接](assets/configure-jdbc-connection.png)

* 輸入以下值：

   * **[!UICONTROL JDBC驅動程式類]**: `com.mysql.jdbc.Driver`
   * **[!UICONTROL JDBC連接URI]**: `jdbc:mysql://localhost:3306/communities?characterEncoding=UTF-8`

      如果MySQL伺服器與「this」伺服器不相同，則指定伺服器代替localhost AEM *社區* 是預設資料庫（架構）名稱。

   * **[!UICONTROL 用戶名]**: `root`

      或者輸入MySQL伺服器的配置用戶名（如果不是「root」）。

   * **[!UICONTROL 密碼]**:

      如果沒有為MySQL設定密碼，請清除此欄位

      否則，輸入MySQL用戶名的配置密碼。

   * **[!UICONTROL 資料源名稱]**:輸入的名稱 [MySQL連接](#new-connection-settings)，例如「communities」。

* 選擇 **[!UICONTROL 保存]**
