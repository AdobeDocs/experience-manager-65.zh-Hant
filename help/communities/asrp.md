---
title: ASRP - Adobe儲存資源供應商
seo-title: ASRP - Adobe儲存資源供應商
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
source-git-commit: 3202866bd38779a9784e44ab470152df61c585f5
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---


# ASRP - Adobe儲存資源供應商{#asrp-adobe-storage-resource-provider}

## 關於ASRP {#about-asrp}

當AEM Communities設定為使用ASRP做為其公用儲存時，使用者產生的內容(UGC)可從所有作者和發佈例項存取，而不需同步或複製。

另請參見[SRP選項的特性](/help/communities/working-with-srp.md#characteristics-of-srp-options)和[建議拓撲](/help/communities/topologies.md)。

## 要求{#requirements}

使用ASRP需要額外的授權。

若要設定您的AEM Communities網站以使用UGC的ASRP，請連絡您的帳戶代表，以取得：

* 資料中心URL（ASRP端點的位址）
* 消費者金鑰
* 機密金鑰
* 報表套裝ID

消費者和機密金鑰會在公司的所有報表套裝中共用。 每個租用戶有一個報表套裝。

## 設定 {#configuration}

### 選擇ASRP {#select-asrp}

[儲存配置控制台](/help/communities/srp-config.md)允許選擇預設儲存配置，該配置標識要使用的SRP實施。

**在AEM Author例項上：**

* 在全局導航中，導航至&#x200B;**[!UICONTROL 工具>社區>儲存配置]**&#x200B;並選擇&#x200B;**[!UICONTROL Adobe儲存資源提供程式(ASRP)]**。

![asrp-default](assets/asrp-default.png)

以下資訊來自設定過程：

* **資料中心URL**:下拉式清單，以選擇由您的帳戶代表所識別的生產資料中心。
* **預設報表套裝**:輸入預設報表套裝的名稱。
* **消費者金鑰**:輸入消費者金鑰。
* **秘密**:輸入密碼。
* 選擇&#x200B;**提交**。

準備發佈例項：

* [複製加密密鑰](#replicate-the-crypto-key)
* [複製配置](#publishing-the-configuration)

提交配置後，測試連接：

* 選擇&#x200B;**測試配置**。

   對於每個作者和發佈實例，請從「儲存配置」控制台測試與資料中心的連接。

* 請確定設定檔資料的網站URL可透過[外部化連結](#externalize-links)從資料中心路由。

### 複製加密密鑰{#replicate-the-crypto-key}

消費者金鑰和機密金鑰會加密。 為了正確加密／解密密鑰，所有AEM實例上的主Granite Crypto密鑰必須相同。

按照[複製加密密鑰](/help/communities/deploy-communities.md#replicate-the-crypto-key)中的說明操作。

### 將連結外部化{#externalize-links}

如需正確的描述檔和描述檔影像連結，請務必正確[設定連結外部化器](/help/sites-developing/externalizer.md)。

請務必將網域設定為可從資料中心URL（ASRP端點）路由的URL。

### 時間同步{#time-synchronization}

為了成功與ASRP端點進行驗證，您所代管的AEM Communities的執行機器必須進行時間同步，例如與[網路時間通訊協定(NTP)](https://www.ntp.org/)同步。

### 發佈配置{#publishing-the-configuration}

ASRP必須被識別為所有作者和發佈實例上的公用商店。

要使相同的配置在發佈環境中可用，請執行以下操作：

在AEM Author例項上：

* 從主菜單導航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 複製]**
* 選擇&#x200B;**激活樹**
* **開始路徑**:瀏覽至  `/conf/global/settings/communities/srpc/`
* 取消選擇&#x200B;**僅已修改**
* 選擇&#x200B;**激活**

## 從AEM 6.0 {#upgrading-from-aem}升級

>[!CAUTION]
>
>如果您在發佈的社群網站上啟用ASRP，則已儲存在[JCR](/help/communities/jsrp.md)中的任何UGC將不再顯示，因為內部部署儲存空間與雲端儲存空間之間的資料不會同步。

**`AEM Communities Extension`** 之前在AEM 6.0社交社群中以雲端服務的形式推出。自AEM 6.1 Communities起，您不需要雲端設定，只需從[儲存組態控制台](/help/communities/srp-config.md)中選取ASRP。

由於新的儲存結構，從社交社區升級到社區時，必須遵循[upgrade](/help/communities/upgrade.md#adobe-cloud-storage)說明。

## 管理用戶資料{#managing-user-data}

有關通常在發佈環境中輸入的&#x200B;*用戶*、*用戶配置檔案*&#x200B;和&#x200B;*用戶組*&#x200B;的資訊，請訪問

* [用戶同步](/help/communities/sync.md)
* [管理使用者和使用者群組](/help/communities/users.md)

## 疑難排解 {#troubleshooting}

### 升級{#ugc-disappears-after-upgrade}後UGC消失

如果從現有的AEM 6.0社交社群網站升級，請務必依照[升級指示](/help/communities/upgrade.md#adobe-cloud-storage)進行，否則UGC會遺失。

### 驗證錯誤{#authentication-errors}

如果收到Data Center URL的驗證錯誤，而AEM error.log包含有關過時時間戳記的訊息，請確認時間同步正在進行。

使用[網路時間通訊協定(NTP)](https://www.ntp.org/)等工具，將所有AEM作者和發佈伺服器的時間同步化。

### 搜尋{#new-content-does-not-appear-in-searches}中未顯示新內容

Adobe雲端儲存基礎架構使用&#x200B;*最終的一致性*&#x200B;來達成其擴充和效能目標。 因此，新內容無法立即使用，而且需要數秒鐘的時間才會顯示在搜尋結果中。

當監控影響最終一致性的間隔時，如果搜尋中出現新內容所花的時間超過幾秒，請連絡您的帳戶代表。

### ASRP {#ugc-not-visible-in-asrp}中不顯示UGC

通過檢查儲存選項的配置，確保ASRP已配置為預設提供程式。 預設情況下，儲存資源提供方是JSRP，而不是ASRP。

在所有作者和發佈AEM例項上，請重新造訪「儲存設定控制台」，或檢查AEM存放庫。

在JCR中，如果[/conf/global/settings/communities](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/):

* 不包含[srpc](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp)節點，這表示儲存提供程式是JSRP。
* 如果srpc節點存在並包含[defaultconfiguration](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp/defaultconfiguration)節點，則defaultconfiguration的屬性將ASRP定義為預設提供程式。

