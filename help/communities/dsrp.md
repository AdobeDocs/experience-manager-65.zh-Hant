---
title: DSRP — 關係資料庫儲存資源提供程式
seo-title: DSRP — 關係資料庫儲存資源提供程式
description: 設定AEM Communities以使用關係資料庫作為其公用儲存
seo-description: 設定AEM Communities以使用關係資料庫作為其公用儲存
uuid: f364e7da-ee54-4ab2-a630-7ec9239005ac
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d23acb18-6761-4290-9e7a-a434582791bd
role: Administrator
exl-id: 15b3a594-efde-4702-9233-232ba1c7e5b0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 2%

---

# DSRP — 關係資料庫儲存資源提供程式{#dsrp-relational-database-storage-resource-provider}

## 關於DSRP {#about-dsrp}

當AEM Communities設定為使用關係資料庫作為其公用存放區時，使用者產生的內容(UGC)可從所有製作和發佈執行個體存取，而無須同步或復寫。

另請參閱[SRP選項的特性](working-with-srp.md#characteristics-of-srp-options)和[建議拓撲](topologies.md)。

## 需求 {#requirements}

* [MySQL](#mysql-configuration)，關係資料庫。
* [Apache Solr](#solr-configuration)，一個搜索平台。

>[!NOTE]
>
>預設儲存配置現在儲存在「conf path(`/conf/global/settings/community/srpc/defaultconfiguration`)」中，而非etc路徑(`/etc/socialconfig/srpc/defaultconfiguration`)中。 建議您遵循[移轉步驟](#zerodt-migration-steps)，使defaultsrp如預期般運作。

## 關係資料庫配置{#relational-database-configuration}

### MySQL配置{#mysql-configuration}

MySQL安裝可通過使用不同的資料庫（架構）名稱以及不同的連接(server:port)在同一連接池中啟用功能和公共儲存(DSRP)之間共用。

有關安裝和配置的詳細資訊，請參閱[DSRP](dsrp-mysql.md)的MySQL配置。

### Solr 設定 {#solr-configuration}

Solr安裝可透過使用不同集合在節點存放區(Oak)和公用存放區(SRP)之間共用。

如果Oak和SRP集合都大量使用，可能會基於效能原因安裝第二個Solr。

對於生產環境，SolrCloud模式比獨立模式（單一本地Solr設定）提供了更高的效能。

有關安裝和配置的詳細資訊，請參閱[SRP](solr.md)的Solr配置。

### 選擇DSRP {#select-dsrp}

[儲存配置控制台](srp-config.md)允許選擇預設儲存配置，以確定要使用的SRP實施。

在作者上，存取儲存設定主控台

* 以管理員權限登入
* 從&#x200B;**主菜單**

   * 選擇&#x200B;**[!UICONTROL 工具]**（從左窗格）
   * 選擇&#x200B;**[!UICONTROL Communities]**
   * 選擇&#x200B;**[!UICONTROL 儲存配置]**

      * 例如，產生的位置是：[http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)
      >[!NOTE]
      >
      >預設儲存配置現在儲存在「conf path(`/conf/global/settings/community/srpc/defaultconfiguration`)」中      而非etc路徑(`/etc/socialconfig/srpc/defaultconfiguration`)。 建議您遵循[移轉步驟](#zerodt-migration-steps)，使defaultsrp如預期般運作。
   ![dsrp-config](assets/dsrp-config.png)

* 選擇&#x200B;**[!UICONTROL 資料庫儲存資源提供程式(DSRP)]**
* **資料庫設定**

   * **[!UICONTROL JDBC 資料來源名稱]**

      為MySQL連接指定的名稱必須與[JDBC OSGi配置](dsrp-mysql.md#configurejdbcconnections)中輸入的名稱相同

      *預設*:社群

   * **[!UICONTROL 資料庫名稱]**

      在[init_schema.sql](dsrp-mysql.md#obtain-the-sql-script)指令碼中為架構指定的名稱

      *預設*:社群

* **SolrConfiguration**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Zookeeper Host**

      如果使用內部ZooKeeper運行Solr，請將此值留空。 否則，當使用外部ZooKeeper在[SolrCloud模式](solr.md#solrcloud-mode)中運行時，將此值設定為ZooKeeper的URI，如&#x200B;*my.server.com:80*

      *預設*:  *&lt;blank>*

   * **[!UICONTROL Solr URL]**

      *預設*:https://127.0.0.1:8983/solr/

   * **[!UICONTROL Solr 集合]**

      *預設*:集合1

* 選擇&#x200B;**[!UICONTROL Submit]**。

### 預設srp {#zerodt-migration-steps}的零停機遷移步驟

請依照下列步驟，確保defaultsrp頁面[http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)如預期般運作：

1. 將位於`/etc/socialconfig`的路徑重新命名為`/etc/socialconfig_old`，以便系統配置回復為jsrp（預設）。
1. 前往已設定jsrp的defaultsrp頁面[http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)。 按一下&#x200B;**[!UICONTROL submit]**&#x200B;按鈕，在`/conf/global/settings/community/srpc`建立新的預設配置節點。
1. 刪除已建立的預設配置`/conf/global/settings/community/srpc/defaultconfiguration`。
1. 複製舊配置`/etc/socialconfig_old/srpc/defaultconfiguration`，以取代上一步中已刪除的節點(`/conf/global/settings/community/srpc/defaultconfiguration`)。
1. 刪除舊的etc節點`/etc/socialconfig_old`。

## 發佈配置{#publishing-the-configuration}

DSRP必須識別為所有製作和發佈執行個體上的通用商店。

若要讓相同的設定可在發佈環境中使用：

* 在作者上：

   * 從主菜單導航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 複製]**
   * 按兩下&#x200B;**[!UICONTROL 激活樹]**
   * **開始路徑**:

      * 瀏覽至`/etc/socialconfig/srpc/`
   * 確保未選擇`Only Modified`。
   * 選擇&#x200B;**[!UICONTROL 激活]**。


## 管理用戶資料{#managing-user-data}

有關&#x200B;*users*、*user profiles*&#x200B;和&#x200B;*user groups*&#x200B;的資訊，通常在發佈環境中輸入，請訪問：

* [使用者同步](sync.md)
* [管理使用者和使用者群組](users.md)

## DSRP {#reindexing-solr-for-dsrp}的索爾重新索引

若要重新索引DSRP Solr，請依照[重新索引MSRP](msrp.md#msrp-reindex-tool)的檔案操作，但為DSRP重新索引時，請改用此URL:**/services/social/datastore/rdb/reindex**

例如，重新索引DSRP的curl命令如下所示：

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```
