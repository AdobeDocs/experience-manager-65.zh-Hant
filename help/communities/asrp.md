---
title: ASRP -Adobe儲存資源提供程式
seo-title: ASRP - Adobe Storage Resource Provider
description: 設定AEM Communities以將關係資料庫用作其公用儲存
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

當AEM Communities配置為使用ASRP作為其公共儲存時，用戶生成的內容(UGC)可以從所有作者和發佈實例中訪問，而無需同步或複製。

另請參閱 [SRP選項的特點](/help/communities/working-with-srp.md#characteristics-of-srp-options) 和 [推薦的拓撲](/help/communities/topologies.md)。

## 要求 {#requirements}

使用ASRP需要額外的許可證。

要將AEM Communities站點配置為將ASRP用於UGC，請聯繫您的客戶代表：

* 資料中心URL（ASRP終結點的地址）
* 消費者金鑰
* 機密金鑰
* 報表套件ID

消費者密鑰和密鑰在公司的所有報告套件中共用。 每個租戶有一個報告套件。

## 設定 {#configuration}

### 選擇ASRP {#select-asrp}

的 [儲存配置控制台](/help/communities/srp-config.md) 允許選擇預設儲存配置，該配置可標識要使用的SRP實現。

**在AEM作者實例上：**

* 從全局導航，導航到 **[!UICONTROL 工具>社區>儲存配置]** 選擇 **[!UICONTROL Adobe儲存資源提供程式(ASRP)]**。

![asrp預設](assets/asrp-default.png)

以下資訊來自預配過程：

* **資料中心URL**:下拉式，選擇由客戶代表標識的生產資料中心。
* **預設報表套件**:輸入預設報表套件的名稱。
* **使用者密鑰**:輸入使用者密鑰。
* **秘密**:輸入密碼。
* 選擇 **提交**。

準備發佈實例：

* [複製加密密鑰](#replicate-the-crypto-key)
* [複製配置](#publishing-the-configuration)

提交配置後，test連接：

* 選擇 **Test配置**。

   對於每個作者和發佈實例，從「儲存配置」控制台test到資料中心的連接。

* 確保配置檔案資料的站點URL可通過資料中心路由 [外部化連結](#externalize-links)。

### 複製加密密鑰 {#replicate-the-crypto-key}

用戶密鑰和密鑰被加密。 為了正確加密/解密密鑰，所有實例上的主Granite加密密鑰必須相AEM同。

按照以下說明執行操作： [複製加密密鑰](/help/communities/deploy-communities.md#replicate-the-crypto-key)。

### 外部化連結 {#externalize-links}

要獲得正確的配置檔案和配置檔案映像連結，請確保正確 [配置連結外部化程式](/help/sites-developing/externalizer.md)。

請確保將域設定為可從資料中心URL（ASRP終結點）路由的URL。

### 時間同步 {#time-synchronization}

為了使用ASRP終結點進行身份驗證成功，運行托管AEM Communities的電腦必須進行時間同步，例如與 [網路時間協定(NTP)](https://www.ntp.org/)。

### 發佈配置 {#publishing-the-configuration}

ASRP必須標識為所有作者和發佈實例上的公用儲存。

要在發佈環境中使相同的配置可用：

在AEM作者實例上：

* 從主菜單導航到 **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 複製]**
* 選擇 **激活樹**
* **起始路徑**:瀏覽 `/conf/global/settings/communities/srpc/`
* 取消選擇 **僅修改**
* 選擇 **激活**

## 從AEM6.0升級 {#upgrading-from-aem}

>[!CAUTION]
>
>如果在已發佈的社區站點上啟用ASRP，則已儲存在 [JCR](/help/communities/jsrp.md) 不再可見，因為本地儲存和雲儲存之間沒有資料同步。

**`AEM Communities Extension`** 此前在6.AEM0社區引入雲服務。 截至AEM6.1社區，無需雲配置，只需從 [儲存配置控制台](/help/communities/srp-config.md)。

由於新的儲存結構，因此必須遵循 [升級](/help/communities/upgrade.md#adobe-cloud-storage) 從社區升級到社區時的說明。

## 管理用戶資料 {#managing-user-data}

有關 *用戶*。 *用戶配置檔案* 和 *用戶組*，通常輸入到發佈環境中，訪問

* [用戶同步](/help/communities/sync.md)
* [管理用戶和用戶組](/help/communities/users.md)

## 疑難排解 {#troubleshooting}

### 升級後UGC消失 {#ugc-disappears-after-upgrade}

如果從現有的AEM6.0社區站點升級，請確保 [升級說明](/help/communities/upgrade.md#adobe-cloud-storage)，否則UGC將丟失。

### 驗證錯誤 {#authentication-errors}

如果接收到針對資料中心URL的驗證錯誤，AEM且error.log包含有關過時時間戳的消息，則驗證是否正在進行時間同步。

使用工具，如 [網路時間協定(NTP)](https://www.ntp.org/) 以時間同步所AEM有作者和發佈伺服器。

### 搜索中未顯示新內容 {#new-content-does-not-appear-in-searches}

Adobe雲儲存基礎架構使用 *最終一致性* 實現其擴展和效能目標。 因此，新內容不會立即可用，而要在搜索結果中顯示，需要幾秒鐘。

在監視影響最終一致性的間隔時，如果搜索中顯示新內容需要超過幾秒鐘，請與您的客戶代表聯繫。

### UGC在ASRP中不可見 {#ugc-not-visible-in-asrp}

通過檢查儲存選項的配置，確保已將ASRP配置為預設提供程式。 預設情況下，儲存資源提供程式是JSRP，而不是ASRP。

在所有作者和發佈AEM實例上，重新訪問儲存配置控制台或檢AEM查儲存庫。

在JCR中，如果 [/conf/global/settings/communities](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/):

* 不包含 [srpc](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp) 節點，表示儲存提供程式是JSRP。
* 如果srpc節點存在並包含 [預設配置](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp/defaultconfiguration) 節點，預設配置的屬性將ASRP定義為預設提供程式。
