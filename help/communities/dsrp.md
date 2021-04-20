---
title: DSRP —— 關係資料庫儲存資源提供程式
seo-title: DSRP —— 關係資料庫儲存資源提供程式
description: 設定AEM Communities以使用關係資料庫作為其公共儲存
seo-description: 設定AEM Communities以使用關係資料庫作為其公共儲存
uuid: f364e7da-ee54-4ab2-a630-7ec9239005ac
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d23acb18-6761-4290-9e7a-a434582791bd
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 2%

---


# DSRP —— 關係資料庫儲存資源提供程式{#dsrp-relational-database-storage-resource-provider}

## 關於DSRP {#about-dsrp}

將AEM Communities配置為使用關係資料庫作為其公共儲存時，用戶生成的內容(UGC)可從所有作者和發佈實例中訪問，而無需同步或複製。

另請參見[SRP選項的特性](working-with-srp.md#characteristics-of-srp-options)和[建議拓撲](topologies.md)。

## 要求{#requirements}

* [MySQL](#mysql-configuration)，關係型資料庫。
* [Apache Solr](#solr-configuration)，搜尋平台。

>[!NOTE]
>
>預設儲存配置現在儲存在conf路徑(`/conf/global/settings/community/srpc/defaultconfiguration`)中，而不是etc路徑(`/etc/socialconfig/srpc/defaultconfiguration`)中。 建議您按照[遷移步驟](#zerodt-migration-steps)進行預設srp工作。

## 關係資料庫配置{#relational-database-configuration}

### MySQL配置{#mysql-configuration}

MySQL安裝可通過使用不同的資料庫（模式）名稱和不同的連接（伺服器：埠）在相同連接池中的啟用功能和公共儲存(DSRP)之間共用。

有關安裝和配置詳細資訊，請參見[MySQL Configuration for DSRP](dsrp-mysql.md)。

### Solr 設定 {#solr-configuration}

Solr安裝可以通過使用不同的集合在節點儲存(Oak)和公共儲存(SRP)之間共用。

如果Oak和SRP系列都被大量使用，則可基於效能原因安裝第二個Solr。

對於生產環境，SolrCloud模式比獨立模式（單一本機Solr設定）提供更佳的效能。

有關安裝和配置詳細資訊，請參見[ SRP的Solr配置](solr.md)。

### 選擇DSRP {#select-dsrp}

[儲存配置控制台](srp-config.md)允許選擇預設儲存配置，該配置標識要使用的SRP實施。

在作者中，要訪問儲存配置控制台

* 以管理員權限登入
* 從&#x200B;**主菜單**

   * 選擇&#x200B;**[!UICONTROL 工具]**（從左窗格）
   * 選擇&#x200B;**[!UICONTROL 社區]**
   * 選擇&#x200B;**[!UICONTROL 儲存配置]**

      * 例如，產生的位置是：[http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)
      >[!NOTE]
      >
      >預設儲存配置現在儲存在conf路徑(`/conf/global/settings/community/srpc/defaultconfiguration`)中      而非etc路徑(`/etc/socialconfig/srpc/defaultconfiguration`)。 建議您按照[遷移步驟](#zerodt-migration-steps)進行預設srp工作。
   ![dsrp-config](assets/dsrp-config.png)

* 選擇&#x200B;**[!UICONTROL 資料庫儲存資源提供程式(DSRP)]**
* **資料庫設定**

   * **[!UICONTROL JDBC 資料來源名稱]**

      給定給MySQL連接的名稱必須與在[JDBC OSGi configuration](dsrp-mysql.md#configurejdbcconnections)中輸入的名稱相同

      *預設*:社區

   * **[!UICONTROL 資料庫名稱]**

      [init_schema.sql](dsrp-mysql.md#obtain-the-sql-script)指令碼中給定給架構的名稱

      *預設*:社區

* **SolrConfiguration**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Zookeeper Host**

      如果使用內部ZooKeeper執行Solr，請將此值留空。 否則，在與外部ZooKeeper一起運行的[SolrCloud模式](solr.md#solrcloud-mode)中，將此值設定為ZooKeeper的URI，例如&#x200B;*my.server.com:80*

      *預設*:  *&lt;blank>*

   * **[!UICONTROL Solr URL]**

      *預設*:https://127.0.0.1:8983/solr/

   * **[!UICONTROL Solr 集合]**

      *預設*:collection1

* 選擇&#x200B;**[!UICONTROL 提交]**。

### 預設srp {#zerodt-migration-steps}的零停機時間遷移步驟

請依照下列步驟來確保預設srp頁面[http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)如預期般運作：

1. 將位於`/etc/socialconfig`的路徑重新命名為`/etc/socialconfig_old`，以便系統配置返回jsrp（預設）。
1. 前往預設srp頁面[http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)，其中已設定jsrp。 按一下&#x200B;**[!UICONTROL submit]**&#x200B;按鈕，以便在`/conf/global/settings/community/srpc`建立新的預設配置節點。
1. 刪除已建立的預設配置`/conf/global/settings/community/srpc/defaultconfiguration`。
1. 複製舊配置`/etc/socialconfig_old/srpc/defaultconfiguration`以取代上一步中刪除的節點(`/conf/global/settings/community/srpc/defaultconfiguration`)。
1. 刪除舊的etc節點`/etc/socialconfig_old`。

## 發佈配置{#publishing-the-configuration}

DSRP必須被識別為所有作者和發佈例項上的通用商店。

要使相同的配置在發佈環境中可用，請執行以下操作：

* 作者：

   * 從主菜單導航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 複製]**
   * 按兩下&#x200B;**[!UICONTROL 激活樹]**
   * **開始路徑**:

      * 瀏覽至`/etc/socialconfig/srpc/`
   * 確保未選擇`Only Modified`。
   * 選擇&#x200B;**[!UICONTROL 激活]**。


## 管理用戶資料{#managing-user-data}

有關&#x200B;*用戶*、*用戶概要檔案*&#x200B;和&#x200B;*用戶組*&#x200B;的資訊，請訪問：

* [用戶同步](sync.md)
* [管理使用者和使用者群組](users.md)

## 為DSRP {#reindexing-solr-for-dsrp}重新索引Solr

要重新索引DSRP Solr，請遵循[重新索引MSRP](msrp.md#msrp-reindex-tool)的檔案，但是，在為DSRP重新索引時，請改用此URL:**/services/social/datastore/rdb/reindex**

例如，重新索引DSRP的curl命令如下所示：

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```

