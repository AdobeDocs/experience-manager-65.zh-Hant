---
title: ASRP - adobe儲存資源供應商
seo-title: ASRP - adobe儲存資源供應商
description: 設定AEM Communities，以使用關聯式資料庫做為其公用儲存
seo-description: 設定AEM Communities，以使用關聯式資料庫做為其公用儲存
uuid: abe47ad9-9f72-4dad-a5e9-6d621a9722d4
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 3e81b519-57ca-4ee1-94bd-7adac4605407
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# ASRP - adobe儲存資源供應商{#asrp-adobe-storage-resource-provider}

## 關於ASRP {#about-asrp}

當AEM Communities設定為使用ASRP做為其公用儲存時，使用者產生的內容(UGC)可從所有作者和發佈例項存取，而不需同步或複製。

另請參 [閱SRP選項和建議的](/help/communities/working-with-srp.md#characteristics-of-srp-options)[拓撲特性](/help/communities/topologies.md)。

## 需求 {#requirements}

使用ASRP需要額外的授權。

若要設定您的AEM Communities網站以使用UGC的ASRP，請連絡您的帳戶代表，以取得：

* 資料中心URL（ASRP端點的位址）
* 消費者金鑰
* 機密金鑰
* 報表套裝ID

消費者和機密金鑰會在公司的所有報表套裝中共用。 每個租用戶有一個報表套裝。

## 設定 {#configuration}

### 選擇ASRP {#select-asrp}

存 [儲配置控制台](/help/communities/srp-config.md) (Storage Configuration Console)允許選擇預設儲存配置，該配置標識要使用的SRP實施。

**在AEM Author例項上：**

* 從全局導航（工具、社區、儲存配置）中，選擇** Adobe儲存資源提供商(ASRP)。**

![chlimage_1-30](assets/chlimage_1-30.png)

以下資訊來自設定過程：

* **資料中心 URL. **下拉式清單，以選取您的帳戶代表所識別的生產資料中心。
* **預設報表套裝. **輸入預設報表套裝的名稱。
* **消費者金鑰**. 輸入消費者金鑰。
* **機密. **輸入機密。
* 選擇 **提交。**

準備發佈例項：

* [複製加密密鑰](#replicate-the-crypto-key)
* [複製配置](#publishing-the-configuration)

提交配置後，測試連接：

* 選擇 **測試配置**。 對於每個作者和發佈實例，請從「儲存配置」控制台測試與資料中心的連接。

* 透過外部化連結，確保描述檔資料的網站URL可從資料中 [心路由](#externalize-links)。

### 複製加密密鑰 {#replicate-the-crypto-key}

消費者金鑰和機密金鑰會加密。 為了正確加密／解密密鑰，主Granite Crypto密鑰在所有AEM實例上必須相同。

按照複製加密密 [鑰中的說明操作](/help/communities/deploy-communities.md#replicate-the-crypto-key)。

### 外部化連結 {#externalize-links}

如需正確的描述檔和描述檔影像連結，請務必正確 [設定連結外部化](/help/sites-developing/externalizer.md)。

請務必將網域設定為可從資料中心URL（ASRP端點）路由的URL。

### 時間同步 {#time-synchronization}

為了成功與ASRP端點進行驗證，您所代管的AEM Communities的執行機器必須進行時間同步化，例如與 [Network Time Protocol(NTP)](https://www.ntp.org/)。

### 發佈設定 {#publishing-the-configuration}

ASRP必須被識別為所有作者和發佈實例上的公用商店。

要使相同的配置在發佈環境中可用，請執行以下操作：

在AEM Author例項上：

* 從主功能表導覽至 `Tools > Operations > Replication.`
* 選擇「 **激活樹」。**
* **開始路徑：**瀏覽至/etc/socialconfig/srpc/
* 取消選 **擇「僅修改」。**
* 選擇「 **啟動」。**

## 從AEM 6.0升級 {#upgrading-from-aem}

>[!CAUTION]
>
>如果您在已發佈的社群網站上啟用ASRP，則已儲存在 [](/help/communities/jsrp.md)JCR中的任何UGC都不再可見，因為內部部署儲存空間和雲端儲存空間之間的資料不會同步。

**`AEM Communities Extension`**之前在AEM 6.0社交社群中以雲端服務的形式推出。 自AEM 6.1 Communities起，您不需要雲端設定，只需從儲存組態主控台 [選取ASRP](/help/communities/srp-config.md)。

由於新的儲存結構，從社交社群升級至社群時，必 [須依](/help/communities/upgrade.md#adobe-cloud-storage) 照升級指示進行。

## 管理使用者資料 {#managing-user-data}

如需使用者 *、使用者****、使用者*&#x200B;設定檔和使用者群組的相關資訊，請造訪

* [用戶同步](/help/communities/sync.md)
* [管理使用者和使用者群組](/help/communities/users.md)

## 疑難排解 {#troubleshooting}

### 升級後UGC消失 {#ugc-disappears-after-upgrade}

如果從現有的AEM 6.0社群網站進行升級，請務必依照升級 [指示](/help/communities/upgrade.md#adobe-cloud-storage)，否則UGC會遺失。

### 驗證錯誤 {#authentication-errors}

如果收到Data Center URL的驗證錯誤，而AEM error.log包含有關過時時間戳記的訊息，請確認時間同步正在進行。

使用網路時間通訊協定( [Network Time Protocol, NTP)](https://www.ntp.org/) 等工具，將所有AEM作者和發佈伺服器的時間同步化。

### 搜尋中不會顯示新內容 {#new-content-does-not-appear-in-searches}

Adobe雲端儲存基礎架構使用最 *終的一致性* ，來達成其擴充和效能目標。 因此，新內容無法立即使用，而且需要數秒鐘的時間才會顯示在搜尋結果中。

當監控影響最終一致性的間隔時，如果搜尋中出現新內容所花的時間超過幾秒，請連絡您的帳戶代表。

### UGC在ASRP中不可見 {#ugc-not-visible-in-asrp}

通過檢查儲存選項的配置，確保ASRP已配置為預設提供程式。 預設情況下，儲存資源提供方是JSRP，而不是ASRP。

在所有作者和發佈AEM例項上，請重新造訪「儲存設定控制台」，或檢查AEM存放庫。

在JCR中，如 [果/etc/socialconfig](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/):

* 不包含 [srpc節點](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) ，這表示儲存提供程式是JSRP。
* 如果srpc節點存在並包含節點 [defaultconfiguration](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)，則defaultconfiguration的屬性會將ASRP定義為預設提供程式。

