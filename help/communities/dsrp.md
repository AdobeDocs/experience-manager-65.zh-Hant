---
title: DSRP —— 關係資料庫儲存資源提供程式
seo-title: DSRP —— 關係資料庫儲存資源提供程式
description: 設定AEM Communities，以使用關聯式資料庫做為其公用儲存
seo-description: 設定AEM Communities，以使用關聯式資料庫做為其公用儲存
uuid: f364e7da-ee54-4ab2-a630-7ec9239005ac
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d23acb18-6761-4290-9e7a-a434582791bd
translation-type: tm+mt
source-git-commit: b7c790681034e9950aa43738310f7af8b1dd0085

---


# DSRP —— 關係資料庫儲存資源提供程式 {#dsrp-relational-database-storage-resource-provider}

## 關於DSRP {#about-dsrp}

當AEM Communities設定為使用關係式資料庫做為其公用儲存時，使用者產生的內容(UGC)可從所有作者和發佈執行個體存取，而不需同步或複製。

另請參 [閱SRP選項和建議的](working-with-srp.md#characteristics-of-srp-options)[拓撲特性](topologies.md)。

## 需求 {#requirements}

* [MySQL](#mysql-configuration)，關係資料庫
* [Apache Solr](#solr-configuration)，搜尋平台

>[!NOTE]
>
>預設儲存配置現在儲存在conf路徑(`/conf/global/settings/community/srpc/defaultconfiguration`)中，而不是etc路徑(`/etc/socialconfig/srpc/defaultconfiguration`)中。 建議您依照移轉步 [驟](#zerodt-migration-steps) ，讓預設srp如預期般運作。


## 關係資料庫配置 {#relational-database-configuration}

### MySQL配置 {#mysql-configuration}

MySQL安裝可通過使用不同的資料庫（模式）名稱和不同的連接（伺服器：埠）在相同連接池中的啟用功能和公共儲存(DSRP)之間共用。

有關安裝和配置詳細資訊，請參 [閱MySQL Configuration for DSRP](dsrp-mysql.md)。

### Solr 設定 {#solr-configuration}

Solr安裝可以通過使用不同的集合在節點儲存(Oak)和公共儲存(SRP)之間共用。

如果Oak和SRP系列都被大量使用，則可基於效能原因安裝第二個Solr。

對於生產環境，SolrCloud模式比獨立模式（單一本機Solr設定）提供更佳的效能。

有關安裝和配置詳細資訊，請參 [閱Solr Configuration for SRP](solr.md)。

### 選擇DSRP {#select-dsrp}

存 [儲配置控制台](srp-config.md) (Storage Configuration Console)允許選擇預設儲存配置，該配置標識要使用的SRP實施。

在作者中，要訪問儲存配置控制台

* 以管理員權限登入
* 從主功 **能表**

   * 選擇 **[!UICONTROL 工具]** （從左窗格）
   * 選擇社 **[!UICONTROL 群]**
   * 選擇 **[!UICONTROL 儲存配置]**

      * 例如，產生的位置是： [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)
      >[!NOTE]
      >
      >預設儲存配置現在儲存在conf路徑(`/conf/global/settings/community/srpc/defaultconfiguration`)中，而不是etc路徑(`/etc/socialconfig/srpc/defaultconfiguration`)中。 建議您依照移轉步 [驟](#zerodt-migration-steps) ，讓預設srp如預期般運作。

![chlimage_1-128](assets/chlimage_1-128.png)

* Select **[!UICONTROL Database Storage Resource Provider (DSRP)]**
* **資料庫設定**

   * **[!UICONTROL JDBC 資料來源名稱]**

      給定給MySQL連接的名稱必須與在 [JDBC OSGi配置中輸入的名稱相同](dsrp-mysql.md#configurejdbcconnections)

      *預設*:社區

   * **[!UICONTROL 資料庫名稱]**

      為 [init_schema.sql指令碼中的架構指定的名稱](dsrp-mysql.md#obtain-the-sql-script)

      *預設*:社區

* **SolrConfiguration**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Zookeeper Host **

      如果使用內部ZooKeeper執行Solr，請將此值留空。 否則，在 [SolrCloud模式下與外部ZooKeeper一起運行時](solr.md#solrcloud-mode) ，將此值設定為ZooKeeper的URI，如 *my.server.com:80*

      *預設*: *&lt;blank>*

   * **[!UICONTROL Solr URL]**

      *預設*:https://127.0.0.1:8983/solr/

   * **[!UICONTROL Solr 集合]**

      *預設*:collection1

* 選擇 **[!UICONTROL 提交]**。

### 預設SRP的零停機遷移步驟 {#zerodt-migration-steps}

請依照下列步驟，確保預設srp頁面 [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp) 如預期般運作：

1. 將路徑重新命 `/etc/socialconfig` 名為， `/etc/socialconfig_old`以便系統配置返回jsrp（預設）。
1. 前往預設srp頁 [面http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)，其中已設定jsrp。 按一下「 **[!UICONTROL submit]** （提交）」按鈕，以便在中建立新的預設配置節點 `/conf/global/settings/community/srpc`。
1. 刪除已建立的預設配置 `/conf/global/settings/community/srpc/defaultconfiguration`。
1. 在上一步中 `/etc/socialconfig_old/srpc/defaultconfiguration` 複製舊配置以取代已刪`/conf/global/settings/community/srpc/defaultconfiguration`除節點()。
1. 刪除舊的等節點 `/etc/socialconfig_old`。

## 發佈設定 {#publishing-the-configuration}

DSRP必須被識別為所有作者和發佈例項上的通用商店。

要使相同的配置在發佈環境中可用，請執行以下操作：

* 作者：

   * 從主菜單導航到「工 **[!UICONTROL 具」>「操作」>「複製」]**
   * 按兩下「激活 **樹」**
   * **開始路徑:**

      * 瀏覽至 `/etc/socialconfig/srpc/`
   * 請確 `Only Modified` 定未選取。
   * 選取「啟 **[!UICONTROL 動」]**


## 管理使用者資料 {#managing-user-data}

如需使用者 *、使用者****、使用者*&#x200B;設定檔和使用者群組的相關資訊，請造訪

* [用戶同步](sync.md)
* [管理使用者和使用者群組](users.md)

## DSRP的重新索引解決方案 {#reindexing-solr-for-dsrp}

要重新索引DSRP Solr，請按照文檔對MSRP [重新編製索引](msrp.md#msrp-reindex-tool)，但是，在為DSRP重新編製索引時，請改用此URL: **/services/social/datastore/rdb/reindex**

例如，重新索引DSRP的curl命令如下所示：

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```

