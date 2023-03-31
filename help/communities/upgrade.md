---
title: 升級至AEM 6.5 Communities
seo-title: Upgrading to AEM 6.5 Communities
description: 如何從舊版升級至AEM 6.5 Communities
seo-description: How to upgrade from an earlier version to AEM 6.5 Communities
uuid: 929c3892-1b3b-46a7-8e70-fa6864125911
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: abe5a998-bbe3-4a2b-bcf7-b490a8275219
docset: aem65
exl-id: ea41d35c-967c-4606-b4ec-377e817902e4
source-git-commit: 066a61a332aa620078740d36bd7f8689282fbf14
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 0%

---

# 升級至AEM 6.5 Communities {#upgrading-to-aem-communities}

視每個網站的拓撲和功能而定，升級至AEM Communities 6.5或安裝最新的Feature Pack時，可能需要執行下列動作。

本節專供社區，並補充 [升級至AEM 6.5](/help/sites-deploying/upgrade.md) （平台）。

## 從AEM 6.1或更新版本升級 {#upgrading-from-aem-or-later}

### 重新索引Solr {#reindex-solr}

在使用MSRP設定的部署上安裝新的Communities功能套件時，必須：

1. 安裝 [最新功能套件](/help/communities/deploy-communities.md#latestfeaturepack).
1. 安裝 [最新Solr配置檔案](/help/communities/msrp.md#upgrading).
1. 重新索引MSRP，請參閱一節 [MSRP重新索引工具](/help/communities/msrp.md#msrp-reindex-tool).

## 從AEM 6.0升級 {#upgrading-from-aem}

如果需要保留預先存在的UGC，則執行此操作的方法取決於儲存的部署UGC [內部部署](#on-premise-storage) 或 [Adobe雲](#adobe-cloud-storage).

### Adobe雲端儲存空間 {#adobe-cloud-storage}

如果升級的網站設定為使用Adobe雲端儲存空間，則可能會顯示（不正確），好像所有UGC都已遺失，因為SRP方法將無法在舊位置找到原先現有的UGC。

因此，有能力指示ASRP使用 `AEM 6.0 compatability-mode` 來存取UGC。

對於所有AEM 6.3製作和發佈例項：

* 以管理員權限登入。
* 設定 [ASRP](/help/communities/asrp.md).
* 請依照下列步驟，使預先存在的UGC可見：

   * 瀏覽至Web主控台：

      * 例如， [https://&lt;host>:&lt;port>/system/console/configMgr](https://localhost:4502/system/console/configMgr)

      * 找出 **AEM Communities公用程式** 設定。
      * 選取以展開設定面板：

         * *取消選中* `Cloud Storage`

         * 選擇 **儲存**

      ![實用程式](assets/utilities.png)


### 內部部署儲存 {#on-premise-storage}

如果升級的網站未使用雲端儲存空間，則必須轉換任何原先現有的UGC，以符合AEM 6.1 Communities中推出的新結構，以支援通用儲存空間。

為此，GitHub提供開放原始碼移轉工具：
[AEM Communities UGC移轉工具](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### Java API {#java-apis}

從AEM 6.0社交社群升級至AEM 6.3社群時，請注意，許多API已重新組織為不同的套件。 使用IDE定制Communities功能時，應輕鬆解決大多數問題。

如需已棄用SocialUtils套件的詳細資訊，請造訪 [SocialUtils重構](/help/communities/socialutils.md).

另請參閱 [使用Maven for Communities](/help/communities/maven.md).

### 無JSP元件模板 {#no-jsp-component-templates}

此 [社會構成框架](/help/communities/scf.md) (SCF)使用 [HandlebarsJS](https://handlebarsjs.com/) (HBS)範本語言取代AEM 6.0之前使用的Java Server Pages(JSP)。

在AEM 6.0中，JSP元件會保留在相同位置的新HBS架構元件旁，而HBS元件通常位於名為「hbs」的子資料夾中。

自AEM 6.1起，JSP元件已完全移除。 對於Communities，建議用SCF元件取代JSP元件的所有使用。

## AEM Communities UGC移轉工具 {#aem-communities-ugc-migration-tool}

此 [AEM Communities UGC移轉工具](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration) 是開放原始碼移轉工具，可在GitHub上使用，可自訂以從舊版AEM social社群匯出UGC，並匯入至AEM Communities 6.1或更新版本。

除了從舊版移動UGC外，還可以使用工具將UGC從舊版移動 [SRP](/help/communities/working-with-srp.md) 從MSRP到DSRP等。

## 從AEM 5.6.1或更舊版本升級 {#upgrading-from-aem-or-earlier}

概念上，共有三代社群元件：

**第1代**:大約CQ 5.4到AEM 5.6.0，以下是 **collab** 將UGC儲存在本機存放庫的元件，使用復寫作為跨平台同步UGC的手段。 其他差異包括使用Java Server Pages(JSP)來實作，以及僅在製作環境中製作部落格的功能。

**第2代**:從AEM 5.6.1到AEM 6.1, **collab** 和 **社交** 元件。 AEM 6.0推出 [社會構成框架](/help/communities/scf.md) (SCF)和AEM 6.2引入 [通用UGC儲存](/help/communities/working-with-srp.md) 其中UGC是使用 [儲存資源提供程式](/help/communities/srp.md) (SRP)。

**第3代**:從AEM 6.2開始，只有 **社交** 元件，在SCF中實作為Handlebars(HBS)元件，需要為UGC選擇SRP。
