---
title: DSRP — 關係資料庫儲存資源提供程式
seo-title: DSRP - Relational Database Storage Resource Provider
description: 設定AEM Communities以將關係資料庫用作其公用儲存
seo-description: Set up AEM Communities to use a relational database as its common store
uuid: f364e7da-ee54-4ab2-a630-7ec9239005ac
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d23acb18-6761-4290-9e7a-a434582791bd
role: Admin
exl-id: 15b3a594-efde-4702-9233-232ba1c7e5b0
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 2%

---

# DSRP — 關係資料庫儲存資源提供程式 {#dsrp-relational-database-storage-resource-provider}

## 關於DSRP {#about-dsrp}

當AEM Communities配置為使用關係資料庫作為其公共儲存時，用戶生成的內容(UGC)可從所有作者和發佈實例訪問，而無需同步或複製。

另請參閱 [SRP選項的特點](working-with-srp.md#characteristics-of-srp-options) 和 [推薦的拓撲](topologies.md)。

## 要求 {#requirements}

* [MySQL](#mysql-configuration)，關係資料庫。
* [阿帕奇索爾](#solr-configuration)，搜索平台。

>[!NOTE]
>
>預設儲存配置現在儲存在conf path(`/conf/global/settings/community/srpc/defaultconfiguration`)而不是等路徑(`/etc/socialconfig/srpc/defaultconfiguration`)。 建議您按照 [遷移步驟](#zerodt-migration-steps) 使defaultsrp按預期工作。

## 關係資料庫配置 {#relational-database-configuration}

### MySQL配置 {#mysql-configuration}

MySQL安裝可以通過使用不同的資料庫（架構）名稱和不同的連接（伺服器：埠）在同一連接池內在啟用功能和公共儲存(DSRP)之間共用。

有關安裝和配置的詳細資訊，請參見 [用於DSRP的MySQL配置](dsrp-mysql.md)。

### Solr 設定 {#solr-configuration}

通過使用不同集合，節點儲存(Oak)和公共儲存(SRP)之間可以共用Solr安裝。

如果Oak和SRP集合都被集中使用，則可能出於效能原因安裝第二個Solr。

對於生產環境，SolrCloud模式比獨立模式（單個本地Solr設定）提供了更高的效能。

有關安裝和配置的詳細資訊，請參見 [SRP的Solr配置](solr.md)。

### 選擇DSRP {#select-dsrp}

的 [儲存配置控制台](srp-config.md) 允許選擇預設儲存配置，該配置可標識要使用的SRP實現。

作者：訪問儲存配置控制台

* 使用管理員權限登錄
* 從 **主菜單**

   * 選擇 **[!UICONTROL 工具]** （從左窗格）
   * 選擇 **[!UICONTROL 社區]**
   * 選擇 **[!UICONTROL 儲存配置]**

      * 例如，結果位置是： [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)
      >[!NOTE]
      >
      >預設儲存配置現在儲存在conf path(`/conf/global/settings/community/srpc/defaultconfiguration`)而不是等路徑(`/etc/socialconfig/srpc/defaultconfiguration`)。 建議您按照 [遷移步驟](#zerodt-migration-steps) 使defaultsrp按預期工作。
   ![dsrp-config](assets/dsrp-config.png)

* 選擇 **[!UICONTROL 資料庫儲存資源提供程式(DSRP)]**
* **資料庫設定**

   * **[!UICONTROL JDBC 資料來源名稱]**

      給MySQL連接的名稱必須與在中輸入的名稱相同 [JDBC OSGi配置](dsrp-mysql.md#configurejdbcconnections)

      *預設*:社區

   * **[!UICONTROL 資料庫名稱]**

      為中的架構指定的名稱 [init_schema_sql](dsrp-mysql.md#obtain-the-sql-script) 指令碼

      *預設*:社區

* **Solr配置**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Zookeeper Host**

      如果使用內部ZooKeeper運行Solr，請將此值留空。 否則，在 [SolrCloud模式](solr.md#solrcloud-mode) 使用外部ZooKeeper，將此值設定為ZooKeeper的URI，如 *my.server.com:80*

      *預設*: *&lt;blank>*

   * **[!UICONTROL Solr URL]**

      *預設*:https://127.0.0.1:8983/solr/

   * **[!UICONTROL Solr 集合]**

      *預設*:集合1

* 選擇 **[!UICONTROL 提交]**。

### 預設SRP的零停機時間遷移步驟 {#zerodt-migration-steps}

按照以下步驟確保預設SRP頁 [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp) 按預期工作：

1. 更名位於 `/etc/socialconfig` 至 `/etc/socialconfig_old`，以便系統配置返回jsrp（預設）。
1. 轉到defaultsrp頁 [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)，其中配置了jsrp。 按一下 **[!UICONTROL 提交]** 按鈕，以在 `/conf/global/settings/community/srpc`。
1. 刪除建立的預設配置 `/conf/global/settings/community/srpc/defaultconfiguration`。
1. 複製舊配置 `/etc/socialconfig_old/srpc/defaultconfiguration` 代替已刪除的節點(`/conf/global/settings/community/srpc/defaultconfiguration`)。
1. 刪除舊等節點 `/etc/socialconfig_old`。

## 發佈配置 {#publishing-the-configuration}

DSRP必須標識為所有作者和發佈實例上的公用儲存。

要在發佈環境中使相同的配置可用：

* 作者：

   * 從主菜單導航到 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 複製]**
   * 按兩下 **[!UICONTROL 激活樹]**
   * **開始路徑**:

      * 瀏覽到 `/etc/socialconfig/srpc/`
   * 確保 `Only Modified` 的子菜單。
   * 選擇 **[!UICONTROL 激活]**。


## 管理用戶資料 {#managing-user-data}

有關 *用戶*。 *用戶配置檔案* 和 *用戶組*，通常輸入到發佈環境中，訪問：

* [用戶同步](sync.md)
* [管理用戶和用戶組](users.md)

## 為DSRP重新編製索引 {#reindexing-solr-for-dsrp}

要重新索引DSRP Solr，請按照文檔 [重新索引MSRP](msrp.md#msrp-reindex-tool)但是，在為DSRP重新編製索引時，請改用此URL: **/services/social/datastore/rdb/reindex**

例如，重新索引DSRP的curl命令如下所示：

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```
