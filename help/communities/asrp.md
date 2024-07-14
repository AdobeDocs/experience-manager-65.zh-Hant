---
title: ASRP -Adobe儲存資源提供者
description: 設定AEM Communities以使用關聯式資料庫作為其公用存放區
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 6430ed96-5d96-41b6-866f-90b34ff84f7a
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 0%

---

# ASRP -Adobe儲存資源提供者 {#asrp-adobe-storage-resource-provider}

## 關於ASRP {#about-asrp}

當AEM Communities設定為使用ASRP作為其一般存放區時，使用者產生的內容(UGC)可從所有製作和發佈執行個體存取，而不需要同步或復寫。

另請參閱[SRP選項的特性](/help/communities/working-with-srp.md#characteristics-of-srp-options)和[建議的拓撲](/help/communities/topologies.md)。

## 要求 {#requirements}

使用ASRP需要額外的授權。

若要設定您的AEM Communities網站以使用ASRP進行UGC，請聯絡您的客戶代表：

* 資料中心URL （ASRP端點的位址）
* 消費者金鑰
* 秘密金鑰
* 報表套裝ID

消費者金鑰和機密金鑰會在公司的所有報表套裝間共用。 每個租使用者有一個報告套裝。

## 設定 {#configuration}

### 選取ASRP {#select-asrp}

[儲存設定主控台](/help/communities/srp-config.md)允許選取預設儲存設定，以識別要使用哪個SRP實作。

**在AEM作者執行個體上：**

* 從全域導覽，瀏覽至&#x200B;**[!UICONTROL Tools > Communities > Storage Configuration]**，然後選取&#x200B;**[!UICONTROL Adobe儲存資源提供者(ASRP)]**。

![asrp-default](assets/asrp-default.png)

下列資訊來自布建程式：

* **資料中心URL**：下拉式選單，以選取您的帳戶代表所識別的生產資料中心。
* **預設報表套裝**：輸入預設報表套裝的名稱。
* **消費者金鑰**：輸入消費者金鑰。
* **密碼**：輸入密碼。
* 選取&#x200B;**提交**。

準備發佈執行個體：

* [復寫加密金鑰](#replicate-the-crypto-key)
* [復寫設定](#publishing-the-configuration)

提交設定後，測試連線：

* 選取&#x200B;**測試組態**。

  對於每個製作和發佈執行個體，請測試「儲存設定」控制檯與資料中心的連線。

* 確定設定檔資料的網站URL可透過[外部化連結](#externalize-links)從資料中心路由。

### 復寫加密金鑰 {#replicate-the-crypto-key}

使用者金鑰和秘密金鑰已加密。 為了使金鑰正確加密/解密，所有AEM執行個體上的主要Granite加密金鑰必須相同。

遵循[復寫加密金鑰](/help/communities/deploy-communities.md#replicate-the-crypto-key)的指示。

### 外部化連結 {#externalize-links}

如需正確的設定檔和設定檔影像連結，請確定已正確[設定連結外部化程式](/help/sites-developing/externalizer.md)。

請務必將網域設為可從資料中心URL （ASRP端點）路由的URL。

### 時間同步 {#time-synchronization}

為了成功使用ASRP端點進行驗證，執行您託管AEM Communities的電腦必須時間同步，例如與[網路時間通訊協定(NTP)](https://www.ntp.org/)。

### 發佈設定 {#publishing-the-configuration}

ASRP必須識別為所有製作和發佈執行個體上的共同存放區。

若要在發佈環境中使用相同的設定：

在AEM編寫執行個體上：

* 從主功能表瀏覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 復寫]**
* 選取&#x200B;**啟動樹狀結構**
* **開始路徑**：瀏覽至`/conf/global/settings/communities/srpc/`
* 取消選取&#x200B;**僅修改**
* 選取&#x200B;**啟動**

## 從AEM 6.0升級 {#upgrading-from-aem}

>[!CAUTION]
>
>如果您在已發佈的社群網站上啟用ASRP，則已儲存在[JCR](/help/communities/jsrp.md)中的任何UGC都不再可見，因為內部部署儲存和雲端儲存之間沒有資料同步。

**`AEM Communities Extension`**&#x200B;先前在AEM 6.0 social communities中引入為雲端服務。 自AEM 6.1 Communities起，不需要雲端設定，只要從[儲存設定主控台](/help/communities/srp-config.md)選取ASRP即可。

由於新的儲存結構，從社交社群升級至社群時，必須遵循[升級](/help/communities/upgrade.md#adobe-cloud-storage)指示。

## 管理使用者資料 {#managing-user-data}

如需&#x200B;*使用者*、*使用者設定檔*&#x200B;和&#x200B;*使用者群組*&#x200B;的相關資訊（通常已進入發佈環境），請造訪

* [使用者同步](/help/communities/sync.md)
* [管理使用者和使用者群組](/help/communities/users.md)

## 疑難排解 {#troubleshooting}

### 升級後UGC消失 {#ugc-disappears-after-upgrade}

如果從現有的AEM 6.0社交社群網站升級，請務必遵循[升級指示](/help/communities/upgrade.md#adobe-cloud-storage)，否則會遺失UGC。

### 驗證錯誤 {#authentication-errors}

如果收到資料中心URL的驗證錯誤，且AEM error.log包含有關過時時間戳記的訊息，請驗證時間同步是否正在進行。

使用[網路時間通訊協定(NTP)](https://www.ntp.org/)之類的工具，以時間同步處理所有AEM製作和發佈伺服器。

### 新內容未出現在搜尋中 {#new-content-does-not-appear-in-searches}

Adobe雲端儲存基礎建設使用&#x200B;*最終一致性*&#x200B;來達成其擴充和效能目標。 因此，新內容無法立即使用，且需要幾秒鐘才能顯示在搜尋結果中。

在監視影響最終一致性的間隔時，如果新內容出現在搜尋中需要超過幾秒的時間，請聯絡您的客戶代表。

### ASRP中未顯示UGC {#ugc-not-visible-in-asrp}

檢查儲存選項的組態，確定ASRP已設定為預設提供者。 依預設，儲存資源提供者為JSRP，而非ASRP。

在所有作者和發佈AEM執行個體上，重新造訪儲存設定主控台，或檢查AEM存放庫。

在JCR中，如果[/conf/global/settings/communities](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)：

* 不包含[srpc](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp)節點，這表示儲存提供者是JSRP。
* 如果srpc節點存在且包含[defaultconfiguration](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp/defaultconfiguration)節點，則defaultconfiguration的屬性會將ASRP定義為預設提供者。
