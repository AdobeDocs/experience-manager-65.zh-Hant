---
title: 升級至AEM 6.5社群
description: 如何從舊版升級至AEM 6.5 Communities
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
docset: aem65
exl-id: ea41d35c-967c-4606-b4ec-377e817902e4
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 0%

---

# 升級至AEM 6.5社群 {#upgrading-to-aem-communities}

根據每個網站的拓朴和功能，在升級至AEM Communities 6.5或安裝最新功能套件時，可能需要執行下列動作。

本節專屬於Communities，並補充中提供的資訊。 [升級至AEM 6.5](/help/sites-deploying/upgrade.md) （平台）。

## 從AEM 6.1或更新版本升級 {#upgrading-from-aem-or-later}

### 重新索引Solr {#reindex-solr}

在使用MSRP設定的部署上安裝新的Communities Feature Pack時，將需要：

1. 安裝 [最新feature pack](/help/communities/deploy-communities.md#latestfeaturepack).
1. 安裝 [最新的Solr設定檔案](/help/communities/msrp.md#upgrading).
1. 重新索引MSRP請參閱區段 [MSRP重新索引工具](/help/communities/msrp.md#msrp-reindex-tool).

## 從AEM 6.0升級 {#upgrading-from-aem}

如果需要保留之前存在的UGC，那麼保留的方法取決於部署是否儲存UGC [內部部署](#on-premise-storage) 或在 [Adobe雲端](#adobe-cloud-storage).

### Adobe雲端儲存空間 {#adobe-cloud-storage}

如果升級的網站設定為使用Adobe雲端儲存空間，則它可能會出現（不正確的）情況，彷彿所有UGC已遺失，因為SRP方法無法在舊位置找到既存的UGC。

因此，能夠指示ASRP使用 `AEM 6.0 compatability-mode` 以存取UGC。

對於所有AEM 6.3編寫和發佈執行個體：

* 以系統管理員許可權登入。
* 設定 [ASRP](/help/communities/asrp.md).
* 請依照下列步驟，顯示預先存在的UGC：

   * 瀏覽至Web主控台：

      * 例如， [https://&lt;host>：&lt;port>/system/console/configMgr](https://localhost:4502/system/console/configMgr)

      * 尋找 **AEM Communities公用程式** 設定。
      * 選取以展開設定面板：

         * *取消核取* `Cloud Storage`

         * 選取 **儲存**

     ![公用程式](assets/utilities.png)

### 內部部署儲存 {#on-premise-storage}

如果升級後的網站未使用雲端儲存空間，任何預先存在的UGC都必須轉換，以符合AEM 6.1 Communities中為支援通用儲存空間而引入的新結構。

為此，GitHub提供開放原始碼移轉工具：
[AEM Communities UGC移轉工具](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### Java API {#java-apis}

從AEM 6.0社交社群升級為AEM 6.3社群時，許多API已重新整理為不同的套件。 在使用IDE進行Communities功能的自訂時，大多數問題應該都能輕鬆解決。

如需有關已棄用的SocialUtils套件的詳細資訊，請造訪 [SocialUtils重構](/help/communities/socialutils.md).

另請參閱 [使用適用於社群的Maven](/help/communities/maven.md).

### 沒有JSP元件範本 {#no-jsp-component-templates}

此 [社交元件框架](/help/communities/scf.md) (SCF)使用 [HandlebarsJS](https://handlebarsjs.com/) (HBS)範本化語言取代AEM 6.0之前使用的Java Server Pages (JSP)。

在AEM 6.0中，JSP元件會與新HBS架構元件一起保留在相同的位置，而HBS元件通常位於名為「hbs」的子資料夾中。

自AEM 6.1起，JSP元件已完全移除。 對於Communities，建議使用SCF元件取代所有使用的JSP元件。

## AEM Communities UGC移轉工具 {#aem-communities-ugc-migration-tool}

此 [AEM Communities UGC移轉工具](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration) 是開放原始碼移轉工具，可在GitHub上取得，且可自訂以從舊版AEM社交社群匯出UGC，並匯入至AEM Communities 6.1或更新版本。

除了從舊版移動UGC之外，也可以使用此工具將UGC從舊版移動 [SRP](/help/communities/working-with-srp.md) 到另一個，例如從MSRP到DSRP。

## 從AEM 5.6.1或更舊版本升級 {#upgrading-from-aem-or-earlier}

從概念上講，社群元件分為三代：

**第1代**：大概CQ 5.4到AEM 5.6.0，這些是 **合作** 元件使用復寫將UGC儲存在本機存放庫中，作為跨平台同步UGC的方式。 其他差異包括使用Java Server Pages (JSP)實作，以及只在作者環境中編寫的部落格功能。

**第2代**：從AEM 5.6.1到AEM 6.1，這是混合使用 **合作** 和 **社交** 元件。 AEM 6.0推出新功能 [社交元件框架](/help/communities/scf.md) (SCF)和AEM 6.2推出了 [通用UGC存放區](/help/communities/working-with-srp.md) 使用存取UGC的位置 [儲存資源提供者](/help/communities/srp.md) (SRP)。

**第3代**：從AEM 6.2開始，只有 **社交** 元件，在SCF中實作為Handlebars (HBS)元件，需要為UGC選擇SRP。
