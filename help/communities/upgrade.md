---
title: 升級至AEM 6.5 Communities
seo-title: 升級至AEM 6.5 Communities
description: 如何從舊版升級至AEM 6.5 Communities
seo-description: 如何從舊版升級至AEM 6.5 Communities
uuid: 929c3892-1b3b-46a7-8e70-fa6864125911
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: abe5a998-bbe3-4a2b-bcf7-b490a8275219
docset: aem65
exl-id: ea41d35c-967c-4606-b4ec-377e817902e4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 1%

---

# 升級至AEM 6.5 Communities {#upgrading-to-aem-communities}

視每個網站的拓撲和功能而定，升級至AEM Communities 6.5或安裝最新的Feature Pack時，可能需要執行下列動作。

本節針對Communities，並補充[升級至AEM 6.5](/help/sites-deploying/upgrade.md)（平台）中提供的資訊。

## 從AEM 6.1或更新版本{#upgrading-from-aem-or-later}升級

### 重新索引Solr {#reindex-solr}

在使用MSRP設定的部署上安裝新的Communities功能套件時，必須：

1. 安裝[最新的Feature Pack](/help/communities/deploy-communities.md#latestfeaturepack)。
1. 安裝[最新Solr配置檔案](/help/communities/msrp.md#upgrading)。
1. 重新索引MSRP
請參閱[MSRP重新索引工具](/help/communities/msrp.md#msrp-reindex-tool)一節。

### 啟用2.0 {#enablement}

自AEM 6.3起，啟用功能不再將報表資訊儲存在MySQL中。 MySQL相依性僅用於追蹤SCORM內容。

請聯絡[客戶服務](https://helpx.adobe.com/tw/marketing-cloud/contact-support.html)以取得從啟用1.0移轉內容的協助。

## 從AEM 6.0 {#upgrading-from-aem}升級

如果需要保留預先存在的UGC，則執行此操作的方法取決於儲存的部署UGC [內部部署](#on-premise-storage)還是[Adobe雲](#adobe-cloud-storage)中。

### Adobe雲儲存{#adobe-cloud-storage}

如果升級的網站設定為使用Adobe雲端儲存空間，則可能會顯示（不正確），好像所有UGC都已遺失，因為SRP方法將無法在舊位置找到原先現有的UGC。

因此，能夠指示ASRP使用`AEM 6.0 compatability-mode`訪問UGC。

對於所有AEM 6.3製作和發佈例項：

* 以管理員權限登入。
* 配置[ASRP](/help/communities/asrp.md)。
* 請依照下列步驟，使預先存在的UGC可見：

   * 瀏覽至Web主控台：

      * 例如， [https://&lt;host>:&lt;port>/system/console/configMgr](https://localhost:4502/system/console/configMgr)

      * 找到&#x200B;**AEM Communities實用程式**&#x200B;配置。
      * 選取以展開設定面板：

         * *取消選中* `Cloud Storage`

         * 選擇&#x200B;**保存**

      ![實用程式](assets/utilities.png)


### 內部部署儲存{#on-premise-storage}

如果升級的網站未使用雲端儲存空間，則必須轉換任何原先現有的UGC，以符合AEM 6.1 Communities中推出的新結構，以支援通用儲存空間。

為此，GitHub提供開放原始碼移轉工具：
[AEM Communities UGC移轉工具](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### Java API {#java-apis}

從AEM 6.0社交社群升級至AEM 6.3社群時，請注意，許多API已重新組織為不同的套件。 使用IDE定制Communities功能時，應輕鬆解決大多數問題。

如需已棄用SocialUtils套件的詳細資訊，請造訪[SocialUtils重構](/help/communities/socialutils.md)。

另請參閱[使用Maven for Communities](/help/communities/maven.md)。

### 無JSP元件模板{#no-jsp-component-templates}

[社交元件架構](/help/communities/scf.md)(SCF)使用[HandlebarsJS](https://www.handlebarsjs.com/)(HBS)範本語言，取代AEM 6.0之前使用的Java伺服器頁面(JSP)。

在AEM 6.0中，JSP元件會保留在相同位置的新HBS架構元件旁，而HBS元件通常位於名為「hbs」的子資料夾中。

自AEM 6.1起，JSP元件已完全移除。 對於Communities，建議用SCF元件取代JSP元件的所有使用。

## AEM Communities UGC遷移工具{#aem-communities-ugc-migration-tool}

[AEM Communities UGC移轉工具](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)是開放原始碼移轉工具，可在GitHub上使用，可自訂以從舊版AEM社群匯出UGC，並匯入至AEM Communities 6.1或更新版本。

除了從舊版移動UGC外，還可使用工具將UGC從一個[SRP](/help/communities/working-with-srp.md)移至另一個，例如從MSRP移至DSRP。

## 從AEM 5.6.1或舊版{#upgrading-from-aem-or-earlier}升級

概念上，共有三代社群元件：

**第1代**:大約CQ 5.4到AEM 5.6.0，這些是 **** collabcomponents，將UGC儲存在本機存放庫中，使用復寫作為跨平台同步UGC的工具。其他差異包括使用Java Server Pages(JSP)來實作，以及僅在製作環境中製作部落格的功能。

**第2代**:從AEM 5.6.1到AEM 6.1，這是collaband socialcomponents的 **** 組 **** 合。AEM 6.0推出了新的[social元件框架](/help/communities/scf.md)(SCF),AEM 6.2引入了[通用UGC儲存](/help/communities/working-with-srp.md)，其中UGC是使用[儲存資源提供者](/help/communities/srp.md)(SRP)來存取的。

**第3代**:從AEM 6.2開始，只有 **** socialcomponents，以Handlebars(HBS)元件的形式實作，需要為UGC選擇SRP。
