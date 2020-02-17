---
title: DSRP的MySQL配置
seo-title: DSRP的MySQL配置
description: 如何連接到MySQL伺服器並建立UGC資料庫
seo-description: 如何連接到MySQL伺服器並建立UGC資料庫
uuid: c058cc88-7ca2-4aed-9a36-b080e603f886
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: edc3043c-7ec4-4e4a-b008-95f1784f012e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# DSRP的MySQL配置 {#mysql-configuration-for-dsrp}

MySQL是關係型資料庫，可用來儲存使用者產生的內容(UGC)。

以下說明如何連接到MySQL伺服器並建立UGC資料庫。

## 需求 {#requirements}

* [最新社群功能套件](deploy-communities.md#latestfeaturepack)
* [MySQL的JDBC驅動程式](deploy-communities.md#jdbc-driver-for-mysql)
* 關係資料庫：

   * [MySQL Server](https://dev.mysql.com/downloads/mysql/) Community Server 5.6版或更新版本

      * 可能與AEM在相同的主機上執行，或遠端執行
   * [MySQL工作台](https://dev.mysql.com/downloads/tools/workbench/)


## 安裝MySQL {#installing-mysql}

[MySQL](https://dev.mysql.com/downloads/mysql/) 應按照目標OS的說明下載並安裝。

### 小寫表名 {#lower-case-table-names}

由於SQL不區分大小寫，因此對於區分大小寫的作業系統，必須包含將所有表名都小寫的設定。

例如，要在Linux OS上指定所有小寫表名：

* 編輯檔案 `/etc/my.cnf`
* 在區 `[mysqld]` 段中，新增下列行：

   `lower_case_table_names = 1`

### UTF8字元集 {#utf-character-set}

為提供更佳的多語言支援，必須使用UTF8字元集。

將MySQL更改為以UTF8作為其字元集：

* mysql> SET NAMES &#39;utf8&#39;;

將MySQL資料庫變更為預設為UTF8:

* 編輯檔案 `/etc/my.cnf`
* 在區 `[client]` 段中，新增下列行：

   `default-character-set=utf8`

* 在區 `[mysqld]` 段中，新增下列行：

   `character-set-server=utf8`

## 安裝MySQL Workbench {#installing-mysql-workbench}

MySQL Workbench提供了一個UI，用於執行安裝模式和初始資料的SQL指令碼。

MySQL Workbench應按照目標OS的說明下載並安裝。

## Communities Connection {#communities-connection}

當MySQL工作台首次啟動時（除非已用於其他用途），它將不顯示任何連接：

![chlimage_1-104](assets/chlimage_1-104.png)

### 新連線設定 {#new-connection-settings}

1. 選擇 `+` 右側的表徵圖 `MySQL Connections`。
1. 在對話方 `Setup New Connection`塊中，輸入適合您平台的值

   為了展示目的，將作者AEM例項和MySQL放在相同的伺服器上：

   * 連接名稱： `Communities`
   * 連接方法： `Standard (TCP/IP)`
   * Hostname: `127.0.0.1`
   * 使用者名稱: `root`
   * 密碼: `no password by default`
   * 預設方案： `leave blank`

1. 選 `Test Connection` 擇以驗證到正在運行的MySQL服務的連接

**附註**:

* 預設埠為 `3306`
* 在 [JDBC OSGi配置中，選擇的連接名作為資料源名輸入](#configurejdbcconnections)

#### 新社群連線 {#new-communities-connection}

![chlimage_1-105](assets/chlimage_1-105.png)

## 資料庫設定 {#database-setup}

開啟Communities連接以安裝資料庫。

![chlimage_1-106](assets/chlimage_1-106.png)

### 獲取SQL指令碼 {#obtain-the-sql-script}

SQL指令碼是從AEM資料庫取得：

1. 瀏覽至CRXDE Lite

   * 例如， [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

1. 選擇/libs/social/config/datastore/dsrp/schema資料夾
1. 下載 `init-schema.sql`

![chlimage_1-107](assets/chlimage_1-107.png)

下載架構的方法之一是

* 為sql文 `jcr:content`件選擇節點
* 請注意，屬性的 `jcr:data`值是檢視連結

* 選取檢視連結，將資料儲存至本機檔案

### 建立DSRP資料庫 {#create-the-dsrp-database}

請遵循以下步驟安裝資料庫。 資料庫的預設名稱為 `communities`。

如果指令碼中更改了資料庫名稱，請務必在 [JDBC配置中更改該名稱](#configurejdbcconnections)。

#### 步驟1:開啟SQL檔案 {#step-open-sql-file}

在MySQL工作台中

* 從「檔案」下拉菜單
* 選擇下載的 `init_schema.sql`

![chlimage_1-108](assets/chlimage_1-108.png)

#### 步驟2:執行SQL指令碼 {#step-execute-sql-script}

在步驟1中開啟之檔案的「工作台」視窗中，選取要 `lightening (flash) icon` 執行指令碼的檔案。

在以下映像中，文 `init_schema.sql` 件已準備好執行：

![chlimage_1-109](assets/chlimage_1-109.png)

#### 重新整理 {#refresh}

執行指令碼後，必須刷新該 `SCHEMAS`部分以 `Navigator` 查看新資料庫。 使用「方案」右側的刷新表徵圖：

![chlimage_1-110](assets/chlimage_1-110.png)

## 配置JDBC連接 {#configure-jdbc-connection}

Day Commons JDBC連接池的OSGi **配置** ，配置MySQL JDBC驅動程式。

所有發佈和作者AEM例項都應指向相同的MySQL伺服器。

當MySQL在與AEM不同的伺服器上執行時，必須在JDBC連接器中指定伺服器主機名稱，以取代&#39;localhost&#39;。

* 在每個作者上並發佈AEM例項
* 以管理員權限登入
* 存取網 [路主控台](../../help/sites-deploying/configuring-osgi.md)

   * 例如， [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)

* 找到 `Day Commons JDBC Connections Pool`
* 選擇圖 `+` 標以建立新連接配置

![chlimage_1-111](assets/chlimage_1-111.png)

* 輸入下列值：

   * **[!UICONTROL JDBC驅動程式類]**: `com.mysql.jdbc.Driver`
   * **[!UICONTROL JDBC連接URI]**: `jdbc:mysql://localhost:3306/communities?characterEncoding=UTF-8`

      如果MySQL伺服器與&#39;this&#39; AEM伺服器不相同，請指定伺服器取代localhost

      *communities* is the default database(schema)name

   * **[!UICONTROL 使用者名稱]**: `root`

      或者，如果不是「root」，請輸入MySQL伺服器的配置用戶名

   * **[!UICONTROL 密碼]**:

      如果沒有為MySQL設定口令，請清除此欄位，

      else enter configured password for the mySQL Username
   * **[!UICONTROL 資料來源名稱]**:為 [MySQL連接輸入的名稱](#new-connection-settings)，例如&#39;communities&#39;

* 選擇保 **[!UICONTROL 存]**

