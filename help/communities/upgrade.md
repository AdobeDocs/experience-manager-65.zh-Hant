---
title: 升級AEM到6.5個社區
seo-title: Upgrading to AEM 6.5 Communities
description: 如何從早期版本升級AEM到6.5社區
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

# 升級AEM到6.5個社區 {#upgrading-to-aem-communities}

根據每個站點的拓撲和功能，升級到AEM Communities6.5或安裝最新功能包時可能需要執行以下操作。

本節針對社區，並補充了 [升級AEM到6.5](/help/sites-deploying/upgrade.md) （平台）。

## 從6AEM.1或更高版本升級 {#upgrading-from-aem-or-later}

### 重新索引索爾 {#reindex-solr}

在配置了MSRP的部署上安裝新的社區功能包時，必須：

1. 安裝 [最新功能包](/help/communities/deploy-communities.md#latestfeaturepack)。
1. 安裝 [最新的Solr配置檔案](/help/communities/msrp.md#upgrading)。
1. 重新索引MSRP，請參閱一節 [MSRP重新索引工具](/help/communities/msrp.md#msrp-reindex-tool)。

## 從AEM6.0升級 {#upgrading-from-aem}

如果需要保留預先存在的UGC，則執行此操作的方法取決於部署是否儲存了UGC [現場](#on-premise-storage) 或 [Adobe雲](#adobe-cloud-storage)。

### Adobe雲儲存 {#adobe-cloud-storage}

如果已升級的站點配置為使用Adobe雲儲存，則可能會顯示（不正確），好像所有UGC都已丟失，因為SRP方法將無法找到舊位置中的預先存在的UGC。

因此，有能力指示ASRP使用 `AEM 6.0 compatability-mode` 訪問UGC。

對於所AEM有6.3作者和發佈實例：

* 使用管理員權限登錄。
* 配置 [ASRP](/help/communities/asrp.md)。
* 按照以下步驟使預先存在的UGC可見：

   * 瀏覽到Web控制台：

      * 比如說， [https://&lt;host>:&lt;port>/system/console/configMgr](https://localhost:4502/system/console/configMgr)

      * 定位 **AEM Communities公用事業** 配置。
      * 選擇以展開配置面板：

         * *取消選中* `Cloud Storage`

         * 選擇 **保存**

      ![實用程式](assets/utilities.png)


### 本地儲存 {#on-premise-storage}

如果升級的站點未使用雲儲存，則必須轉換任何預先存在的UGC，以符合在AEM6.1社區中引入的新結構，以支援公共儲存。

為此，GitHub上提供了一個開源遷移工具：
[AEM CommunitiesUGC遷移工具](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### Java API {#java-apis}

在從AEM6.0社區升級到AEM6.3社區時，請注意，許多API已重新組織為不同的包。 在使用IDE定制社區功能時，應輕鬆解決大多數問題。

有關已棄用的SocialUtils包的詳細資訊，請訪問 [SocialUtils重構](/help/communities/socialutils.md)。

另請參閱 [將Maven用於社區](/help/communities/maven.md)。

### 無JSP元件模板 {#no-jsp-component-templates}

的 [社會構成框架](/help/communities/scf.md) (SCF)使用 [車把JS](https://handlebarsjs.com/) (HBS)模板語言代替6.0之前使用的Java Server Pages(JSP)AEM。

在AEM6.0中，JSP元件保留在同一位置的新HBS框架元件旁邊，HBS元件通常位於名為「hbs」的子資料夾中。

截至AEM6.1,JSP元件已完全刪除。 對於社區，建議將JSP元件的所有使用替換為SCF元件。

## AEM CommunitiesUGC遷移工具 {#aem-communities-ugc-migration-tool}

的 [AEM CommunitiesUGC遷移工具](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration) 是GitHub上提供的開放原始碼遷移工具，可自定義以從早期版本的社AEM區導出UGC並導入AEM Communities6.1或更高版本。

除了將UGC從早期版本移動外，還可以使用工具將UGC從一個版本移動 [SRP](/help/communities/working-with-srp.md) 從MSRP到DSRP。

## 從AEM5.6.1或更早版本升級 {#upgrading-from-aem-or-earlier}

從概念上講，有三代社區組成：

**第1代**:大約在5.4到AEM5.6.0之間， **合作** 將UGC儲存在本地儲存庫中的元件，使用復製作為跨平台同步UGC的手段。 其他差異包括使用Java Server Pages(JSP)實現，以及僅在作者環境中創作的部落格功能。

**第2代**:從AEM5.6.1到AEM6.1 **合作** 和 **社會** 元件。 AEM6.0引入了 [社會構成框架](/help/communities/scf.md) (SCF)和AEM6.2 [通用UGC儲存](/help/communities/working-with-srp.md) 其中，UGC使用 [儲存資源提供程式](/help/communities/srp.md) (SRP)。

**第3代**:從AEM6.2開始，只有 **社會** 元件，在SCF中實現為Handlebar(HBS)元件，需要為UGC選擇SRP。
