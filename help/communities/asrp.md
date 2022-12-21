---
title: ASRP -Adobe儲存資源提供程式
seo-title: ASRP - Adobe Storage Resource Provider
description: 設定AEM Communities以使用關係資料庫作為其公用儲存
seo-description: Set up AEM Communities to use a relational database as its common store
uuid: abe47ad9-9f72-4dad-a5e9-6d621a9722d4
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 3e81b519-57ca-4ee1-94bd-7adac4605407
docset: aem65
role: Admin
exl-id: 6430ed96-5d96-41b6-866f-90b34ff84f7a
source-git-commit: 42feafa381c129117dae5345255702f0b0951a17
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 0%

---

# ASRP -Adobe儲存資源提供程式 {#asrp-adobe-storage-resource-provider}

## 關於ASRP {#about-asrp}

當AEM Communities設定為使用ASRP作為其公用存放區時，使用者產生的內容(UGC)可從所有製作和發佈執行個體存取，而無須同步或復寫。

另請參閱 [SRP選項的特點](/help/communities/working-with-srp.md#characteristics-of-srp-options) 和 [建議的拓撲](/help/communities/topologies.md).

## 要求 {#requirements}

使用ASRP需要額外的許可。

若要設定您的AEM Communities網站以使用ASRP進行UGC，請連絡您的客戶代表，以取得：

* 資料中心URL（ASRP端點的地址）
* 消費者金鑰
* 機密金鑰
* 報表套裝ID

消費者金鑰和機密金鑰會在公司的所有報表套裝間共用。 每個租用戶有一個報表套裝。

## 設定 {#configuration}

### 選擇ASRP {#select-asrp}

此 [儲存配置控制台](/help/communities/srp-config.md) 允許選擇預設儲存配置，以確定要使用的SRP實施。

**在AEM Author例項上：**

* 從全域導覽導覽至 **[!UICONTROL 工具>社區>儲存配置]** 選取 **[!UICONTROL Adobe儲存資源提供程式(ASRP)]**.

![asrp-default](assets/asrp-default.png)

以下資訊來自設定過程：

* **資料中心URL**:從下拉式清單中選取由您的帳戶代表所識別的生產資料中心。
* **預設報表套裝**:輸入預設報表套裝的名稱。
* **使用者金鑰**:輸入使用者金鑰。
* **機密**:輸入密碼。
* 選擇 **提交**.

準備發佈例項：

* [複製加密密鑰](#replicate-the-crypto-key)
* [複製配置](#publishing-the-configuration)

提交配置後，測試連接：

* 選擇 **測試設定**.

   對於每個製作和發佈實例，從儲存配置控制台測試與資料中心的連接。

* 請確定設定檔資料的網站URL可從資料中心路由，方法為 [外部連結](#externalize-links).

### 複製加密密鑰 {#replicate-the-crypto-key}

使用者金鑰和密鑰已加密。 為了正確加密/解密金鑰，所有AEM例項上的主要Granite Crypto金鑰必須相同。

請依照 [複製加密密鑰](/help/communities/deploy-communities.md#replicate-the-crypto-key).

### 將連結外部化 {#externalize-links}

若要取得正確的設定檔和設定檔影像連結，請務必正確 [配置Link Externalizer](/help/sites-developing/externalizer.md).

請務必將網域設定為可從資料中心URL（ASRP端點）路由的URL。

### 時間同步 {#time-synchronization}

為了成功與ASRP端點進行驗證，執行托管AEM Communities的電腦必須同步時間，例如與 [網路時間協定(NTP)](https://www.ntp.org/).

### 發佈設定 {#publishing-the-configuration}

ASRP必須識別為所有製作和發佈執行個體上的通用存放區。

若要讓相同的設定可在發佈環境中使用：

在AEM Author例項上：

* 從主功能表導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 復寫]**
* 選擇 **激活樹**
* **起始路徑**:瀏覽 `/conf/global/settings/communities/srpc/`
* 取消選擇 **僅已修改**
* 選擇 **啟動**

## 從AEM 6.0升級 {#upgrading-from-aem}

>[!CAUTION]
>
>如果您在已發佈的社群網站上啟用ASRP，則任何已儲存在 [JCR](/help/communities/jsrp.md) 不再可見，因為內部部署儲存與雲端儲存之間不會同步資料。

**`AEM Communities Extension`** 先前於AEM 6.0 social communities as a cloud service中推出。 自AEM 6.1 Communities起，不需要雲端設定，只需從 [儲存配置控制台](/help/communities/srp-config.md).

由於新的儲存結構，因此必須遵循 [升級](/help/communities/upgrade.md#adobe-cloud-storage) 從社交社群升級至社群的指示。

## 管理使用者資料 {#managing-user-data}

如需 *使用者*, *使用者設定檔* 和 *使用者群組*，通常會在發佈環境中輸入，請造訪

* [使用者同步](/help/communities/sync.md)
* [管理使用者和使用者群組](/help/communities/users.md)

## 疑難排解 {#troubleshooting}

### 升級後UGC消失 {#ugc-disappears-after-upgrade}

如果從現有的AEM 6.0社交社群網站進行升級，請務必遵循 [升級指示](/help/communities/upgrade.md#adobe-cloud-storage)，否則UGC似乎會遺失。

### 驗證錯誤 {#authentication-errors}

如果收到資料中心URL的驗證錯誤，且AEM error.log包含有關過時時間戳的訊息，請確認正在進行時間同步。

使用工具，例如 [網路時間協定(NTP)](https://www.ntp.org/) 來同步所有AEM製作和發佈伺服器。

### 搜尋中未出現新內容 {#new-content-does-not-appear-in-searches}

Adobe雲儲存基礎架構使用 *最終一致性* 實現其擴展和效能目標。 因此，新內容無法立即使用，而且需要數秒的時間才會顯示在搜尋結果中。

當監控影響最終一致性的間隔時間時，如果新內容出現在搜尋中所花的時間超過幾秒，請連絡您的帳戶代表。

### UGC在ASRP中不可見 {#ugc-not-visible-in-asrp}

檢查儲存選項的配置，確保ASRP已配置為預設提供程式。 預設情況下，儲存資源提供者為JSRP，而非ASRP。

在所有製作和發佈AEM例項上，重新造訪儲存設定主控台，或檢查AEM存放庫。

在JCR中，如果 [/conf/global/settings/communities](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/):

* 不包含 [srpc](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp) 節點，表示儲存提供者為JSRP。
* 如果srpc節點存在且包含 [defaultconfiguration](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp/defaultconfiguration) 節點，預設配置的屬性將ASRP定義為預設提供程式。
