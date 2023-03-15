---
title: DSRP — 關係資料庫儲存資源提供程式
seo-title: DSRP - Relational Database Storage Resource Provider
description: 設定AEM Communities以使用關係資料庫作為其公用儲存
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

當AEM Communities設定為使用關係資料庫作為其公用存放區時，使用者產生的內容(UGC)可從所有製作和發佈執行個體存取，而無須同步或復寫。

另請參閱 [SRP選項的特點](working-with-srp.md#characteristics-of-srp-options) 和 [建議的拓撲](topologies.md).

## 要求 {#requirements}

* [MySQL](#mysql-configuration)，關係資料庫。
* [阿帕奇索爾](#solr-configuration)，即搜尋平台。

>[!NOTE]
>
>預設儲存配置現在儲存在「conf path(`/conf/global/settings/community/srpc/defaultconfiguration`)而非etc路徑(`/etc/socialconfig/srpc/defaultconfiguration`)。 建議您遵循 [移轉步驟](#zerodt-migration-steps) 讓defaultsrp正常運作。

## 關係資料庫配置 {#relational-database-configuration}

### MySQL配置 {#mysql-configuration}

MySQL安裝可通過使用不同的資料庫（架構）名稱以及不同的連接(server:port)在同一連接池中啟用功能和公共儲存(DSRP)之間共用。

有關安裝和配置的詳細資訊，請參見 [DSRP的MySQL配置](dsrp-mysql.md).

### Solr 設定 {#solr-configuration}

Solr安裝可透過使用不同集合在節點存放區(Oak)和公用存放區(SRP)之間共用。

如果Oak和SRP集合都大量使用，可能會基於效能原因安裝第二個Solr。

對於生產環境，SolrCloud模式比獨立模式（單一本地Solr設定）提供了更高的效能。

有關安裝和配置的詳細資訊，請參見 [SRP的Solr配置](solr.md).

### 選擇DSRP {#select-dsrp}

此 [儲存配置控制台](srp-config.md) 允許選擇預設儲存配置，以確定要使用的SRP實施。

在作者上，存取儲存設定主控台

* 以管理員權限登入
* 從 **主菜單**

   * 選擇 **[!UICONTROL 工具]** （從左窗格）
   * 選擇 **[!UICONTROL 社群]**
   * 選擇 **[!UICONTROL 儲存配置]**

      * 例如，產生的位置是： [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)
      >[!NOTE]
      >
      >預設儲存配置現在儲存在「conf path(`/conf/global/settings/community/srpc/defaultconfiguration`)而非etc路徑(`/etc/socialconfig/srpc/defaultconfiguration`)。 建議您遵循 [移轉步驟](#zerodt-migration-steps) 讓defaultsrp正常運作。
   ![dsrp-config](assets/dsrp-config.png)

* 選擇 **[!UICONTROL 資料庫儲存資源提供程式(DSRP)]**
* **資料庫設定**

   * **[!UICONTROL JDBC 資料來源名稱]**

      為MySQL連接指定的名稱必須與中輸入的名稱相同 [JDBC OSGi配置](dsrp-mysql.md#configurejdbcconnections)

      *預設*:社群

   * **[!UICONTROL 資料庫名稱]**

      為中的架構指定的名稱 [init_schema.sql](dsrp-mysql.md#obtain-the-sql-script) 指令碼

      *預設*:社群

* **SolrConfiguration**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Zookeeper Host**

      如果使用內部ZooKeeper運行Solr，請將此值留空。 否則，當執行 [SolrCloud模式](solr.md#solrcloud-mode) 使用外部ZooKeeper，將此值設定為ZooKeeper的URI，例如 *my.server.com:80*

      *預設*: *&lt;blank>*

   * **[!UICONTROL Solr URL]**

      *預設*:https://127.0.0.1:8983/solr/

   * **[!UICONTROL Solr 集合]**

      *預設*:集合1

* 選擇 **[!UICONTROL 提交]**.

### 預設srp的零停機遷移步驟 {#zerodt-migration-steps}

請依照下列步驟，確保預設項目頁面 [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp) 如預期般運作：

1. 在重新命名路徑 `/etc/socialconfig` to `/etc/socialconfig_old`，使系統配置回復為jsrp（預設）。
1. 前往defaultsrp頁面 [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)，其中已設定jsrp。 按一下 **[!UICONTROL 提交]** 按鈕，以便在建立新的預設配置節點 `/conf/global/settings/community/srpc`.
1. 刪除已建立的預設配置 `/conf/global/settings/community/srpc/defaultconfiguration`.
1. 複製舊配置 `/etc/socialconfig_old/srpc/defaultconfiguration` 取代已刪除節點(`/conf/global/settings/community/srpc/defaultconfiguration`)。
1. 刪除舊等節點 `/etc/socialconfig_old`.

## 發佈設定 {#publishing-the-configuration}

DSRP必須識別為所有製作和發佈執行個體上的通用商店。

若要讓相同的設定可在發佈環境中使用：

* 在作者上：

   * 從主功能表導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 復寫]**
   * 按兩下 **[!UICONTROL 激活樹]**
   * **開始路徑**:

      * 瀏覽至 `/etc/socialconfig/srpc/`
   * 確保 `Only Modified` 未選取。
   * 選擇 **[!UICONTROL 啟動]**.


## 管理使用者資料 {#managing-user-data}

如需 *使用者*, *使用者設定檔* 和 *使用者群組*，通常會在發佈環境中輸入，請造訪：

* [使用者同步](sync.md)
* [管理使用者和使用者群組](users.md)

## DSRP的重新索引解決方案 {#reindexing-solr-for-dsrp}

要重新索引DSRP Solr，請遵循 [重新索引MSRP](msrp.md#msrp-reindex-tool)，不過在為DSRP重新建立索引時，請改用此URL: **/services/social/datastore/rdb/reindex**

例如，重新索引DSRP的curl命令如下所示：

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```
