---
title: 升級至AEM 6.5 Communities
seo-title: 升級至AEM 6.5 Communities
description: 如何從舊版升級至AEM 6.4 Communities
seo-description: 如何從舊版升級至AEM 6.4 Communities
uuid: 929c3892-1b3b-46a7-8e70-fa6864125911
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: abe5a998-bbe3-4a2b-bcf7-b490a8275219
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 升級至AEM 6.5 Communities{#upgrading-to-aem-communities}

視每個網站的拓撲和功能而定，在升級至AEM Communities 6.5或安裝最新功能套件時，可能需要執行下列動作。

本節針對「社群」，並補充「升級 [至AEM 6.5](/help/sites-deploying/upgrade.md) （平台）」中提供的資訊。

## 從AEM 6.1或更新版本升級 {#upgrading-from-aem-or-later}

### 重新索引Solr {#reindex-solr}

在使用MSRP設定的部署上安裝新的社群功能套件時，必須

1. 安裝最 [新功能包](/help/communities/deploy-communities.md#latestfeaturepack)
1. 安裝最 [新的Solr配置檔案](/help/communities/msrp.md#upgrading)
1. 重新索引MSRP請參閱「 [MSRP重新索引工具」一節](/help/communities/msrp.md#msrp-reindex-tool)

### Enablement 2.0 {#enablement}

自AEM 6.3起，啟用功能將不再將報告資訊儲存在MySQL中。 MySQL相依性僅用於跟蹤SCORM內容。

請聯絡客 [戶服務](https://helpx.adobe.com/marketing-cloud/contact-support.html) ，以取得從Enablement 1.0移轉內容的協助。

## 從AEM 6.0升級 {#upgrading-from-aem}

如果需要保留先前存在的UGC，則要保留的方式取決於部署是在內部部署 [UGC](#on-premise-storage) ，還是 [Adobe雲端中](#adobe-cloud-storage)。

### Adobe雲端儲存空間 {#adobe-cloud-storage}

如果已升級的網站設定為使用Adobe雲端儲存空間，則可能會（不正確）顯示，好像所有UGC都已遺失，因為SRP方法將無法在舊位置找到預先存在的UGC。

因此，可以指示ASRP使用UGC `AEM 6.0 compatability-mode` 訪問UGC。

針對所有AEM 6.3作者和發佈例項

* 以管理員權限登入
* 配置 [ASRP](/help/communities/asrp.md)
* 請遵循下列步驟，讓預先存在的UGC可見：

   * 瀏覽至Web主控台

      * 例如， [https://&lt;host>:&lt;port>/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * 找出 **AEM Communities公用程式設定**
   * 選擇展開配置面板

      * *取消選中***`Cloud Storage`**

      * 選擇保 **存**


![chlimage_1-176](assets/chlimage_1-176.png)

### 現場儲存 {#on-premise-storage}

如果升級的網站未使用雲端儲存空間，則必須轉換任何預先存在的UGC，以符合AEM 6.1 Communities中引進的新結構，以支援共用儲存空間。

為此，GitHub上提供開放原始碼移轉工具：[AEM Communities UGC移轉工具](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### Java API {#java-apis}

從AEM 6.0社交社群升級至AEM 6.3社群時，請注意，許多API已重新組織為不同的套件。 在使用IDE自訂社群功能時，大多數問題都應輕鬆解決。

如需已過時SocialUtils套件的詳細資訊，請造 [訪SocialUtils重構](/help/communities/socialutils.md)。

另請參 [閱使用Maven for Communities](/help/communities/maven.md)。

### 無JSP元件模板 {#no-jsp-component-templates}

社 [交元件架構](/help/communities/scf.md) (SCF)使用 [HandlebarsJS](https://www.handlebarsjs.com/) (HBS)範本語言來取代AEM 6.0之前使用的Java Server Pages(JSP)。

在AEM 6.0中，JSP元件會保留在新HBS架構元件旁邊的相同位置，而HBS元件通常位於名為&quot;hbs&quot;的子檔案夾中。

自AEM 6.1起，JSP元件已完全移除。 對於Communities，建議使用SCF元件替換所有JSP元件的使用。

## AEM Communities UGC移轉工具 {#aem-communities-ugc-migration-tool}

[AEM Communities UGC Migration Tool](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration) （AEM Communities UGC移轉工具）是開放原始碼移轉工具，可在GitHub上使用，可自訂以從舊版AEM社群匯出UGC，並匯入AEM Communities 6.1或更新版本。

除了將UGC從舊版移動外，還可使用此工具將UGC從一個 [SRP](/help/communities/working-with-srp.md) （如從MSRP）移至另一個（如從DSRP）。

## 從AEM 5.6.1或舊版升級 {#upgrading-from-aem-or-earlier}

從概念上講，有三代社群組成：

**第1代** :大約CQ 5.4到AEM 5.6.0 —— 這些是 **collab** components，它們將UGC儲存在本機儲存庫中，並使用複製來同步跨平台的UGC。 其他差異包括使用Java Server Pages(JSP)的實作，以及部落格功能，其中僅包含在作者環境中編寫。

**第2代** :從AEM 5.6.1到AEM 6.1 —— 這是Collab和Social元 **件****的混合** 。 AEM 6.0推出新的 [Social元件架構](/help/communities/scf.md) (SCF),AEM 6.2推出通用的 [UGC商店](/help/communities/working-with-srp.md) ，可使用儲存資源提供者 [](/help/communities/srp.md) (SRP)存取UGC。

**第3代** :從AEM 6.2轉發，只有 **social** components，以SCF建置為Handlebars(HBS)元件，需要針對UGC選擇SRP。
