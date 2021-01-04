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
translation-type: tm+mt
source-git-commit: 612d102b5925704ce459ad818554e487ec0d5355
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 1%

---


# 升級至AEM 6.5 Communities {#upgrading-to-aem-communities}

視每個網站的拓撲和功能而定，在升級至AEM Communities 6.5或安裝最新功能套件時，可能需要執行下列動作。

本節針對社群，並補充[升級至AEM 6.5](/help/sites-deploying/upgrade.md)（平台）中提供的資訊。

## 從AEM 6.1或更新版本{#upgrading-from-aem-or-later}升級

### 重新索引Solr {#reindex-solr}

在配置有MSRP的部署上安裝新的Communities功能包時，必須：

1. 安裝[最新的功能套件](/help/communities/deploy-communities.md#latestfeaturepack)。
1. 安裝[最新的Solr配置檔案](/help/communities/msrp.md#upgrading)。
1. 重新索引MSRP
請參閱[節MSRP重新索引工具](/help/communities/msrp.md#msrp-reindex-tool)。

### 啟用2.0 {#enablement}

自AEM 6.3起，啟用功能將不再將報告資訊儲存在MySQL中。 MySQL相依性僅用於跟蹤SCORM內容。

請聯絡[客戶服務](https://helpx.adobe.com/tw/marketing-cloud/contact-support.html)，以取得從Enablement 1.0移轉內容的協助。

## 從AEM 6.0 {#upgrading-from-aem}升級

如果需要保留預先存在的UGC，則執行此動作的方式取決於部署儲存在[on-premise](#on-premise-storage)或[Adobe雲端](#adobe-cloud-storage)中。

### Adobe雲端儲存空間{#adobe-cloud-storage}

如果已升級的網站設定為使用Adobe雲端儲存空間，則可能會（不正確）顯示，好像所有UGC都已遺失，因為SRP方法將無法在舊位置找到預先存在的UGC。

因此，能夠指示ASRP使用`AEM 6.0 compatability-mode`訪問UGC。

針對所有AEM 6.3作者和發佈例項：

* 以管理員權限登入。
* 配置[ASRP](/help/communities/asrp.md)。
* 請依照下列步驟，讓預先存在的UGC可見：

   * 瀏覽至Web主控台：

      * 例如，[https://&lt;host>:&lt;port>/system/console/configMgr](https://localhost:4502/system/console/configMgr)

      * 找到&#x200B;**AEM Communities Utilities**&#x200B;組態。
      * 選擇以展開配置面板：

         * *取消選中* `Cloud Storage`

         * 選擇&#x200B;**保存**

      ![實用程式](assets/utilities.png)


### 內部部署儲存{#on-premise-storage}

如果升級的網站未使用雲端儲存空間，則必須轉換任何預先存在的UGC，以符合AEM 6.1 Communities中引進的新結構，以支援共用儲存空間。

為此，GitHub上提供開放原始碼移轉工具：
[AEM Communities UGC移轉工具](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### Java API {#java-apis}

從AEM 6.0社交社群升級至AEM 6.3社群時，請注意，許多API已重新組織為不同的套件。 在使用IDE自訂社群功能時，大多數問題都應輕鬆解決。

如需已過時SocialUtils套件的詳細資訊，請造訪[SocialUtils Reforcation](/help/communities/socialutils.md)。

另請參見[使用Maven for Communities](/help/communities/maven.md)。

### 無JSP元件模板{#no-jsp-component-templates}

[social元件架構](/help/communities/scf.md)(SCF)使用[HandlebarsJS](https://www.handlebarsjs.com/)(HBS)範本語言來取代AEM 6.0之前使用的Java Server Pages(JSP)。

在AEM 6.0中，JSP元件會保留在新HBS架構元件旁邊的相同位置，而HBS元件通常位於名為&quot;hbs&quot;的子檔案夾中。

自AEM 6.1起，JSP元件已完全移除。 對於Communities，建議使用SCF元件替換所有JSP元件的使用。

## AEM Communities UGC移轉工具{#aem-communities-ugc-migration-tool}

[AEM Communities UGC Migration Tool](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)是開放原始碼移轉工具，可在GitHub上使用，可自訂以從舊版AEM Social社群匯出UGC，並匯入AEM Communities 6.1或更新版本。

除了從舊版移動UGC外，還可使用該工具將UGC從一個[SRP](/help/communities/working-with-srp.md)移至另一個，如從MSRP移至DSRP。

## 從AEM 5.6.1或舊版{#upgrading-from-aem-or-earlier}升級

從概念上講，有三代社群組成：

**第1代**:大約CQ 5.4到AEM 5.6.0，這些是 **** collabcomponents，將UGC儲存在本機儲存庫中，將復製作為跨平台同步UGC的方式。其他差異包括使用Java Server Pages(JSP)的實作，以及部落格功能，其中僅包含在作者環境中編寫。

**第2代**:從AEM 5.6.1到AEM 6.1，這是collaband  **** socialcomponents的 **** 混合。AEM 6.0推出新的[社交元件架構](/help/communities/scf.md)(SCF),AEM 6.2推出了[通用UGC商店](/help/communities/working-with-srp.md)，其中UGC是使用[儲存資源提供者](/help/communities/srp.md)(SRP)存取。

**第3代**:從AEM 6.2開始，只有 **** socialcomponents，在SCF中實作為Handlebars(HBS)元件，需要針對UGC選擇SRP。
