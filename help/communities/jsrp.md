---
title: JSRP - JCR儲存資源提供程式
seo-title: JSRP - JCR Storage Resource Provider
description: JSRP通常最適合於一個發佈實例和一個作者實例的演示或開發環境
seo-description: JSRP is generally best suited for demonstration or development environments of one publish instance and one author instance
uuid: 358a43c1-4137-4300-8443-c0d7166968ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: f5316a73-84e2-4a18-98c1-a384eeaa77cf
role: Admin
exl-id: 873e013c-a2da-4b37-b0e3-56bdf240004a
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# JSRP - JCR儲存資源提供程式 {#jsrp-jcr-storage-resource-provider}

## 關於JSRP {#about-jsrp}

當AEM Communities使用JSRP作為其儲存選項（預設）時，社區內容儲存在JCR中，用戶生成的內容(UGC)只能從發佈到它的作者或發佈實例訪問。

由於部署簡單，JSRP通常最適合於一個發佈實例和一個作者實例的演示或開發環境。

另請參閱 [SRP選項的特點](working-with-srp.md#characteristics-of-srp-options) 和 [推薦的拓撲](topologies.md)。

## 設定 {#configuration}

### 選擇JSRP {#select-jsrp}

預設情況下， JSRP是UGC的儲存選項。

的 [儲存配置控制台](srp-config.md) 允許選擇預設儲存配置，該配置可標識要使用的SRP實現。

在作者環境中，要訪問儲存配置控制台

* 從全局導航： **[!UICONTROL 工具]** > **[!UICONTROL 社區]** > **[!UICONTROL 儲存配置]**

* 選擇 **[!UICONTROL JCR儲存資源提供程式(JSRP)]**

* 選擇 **[!UICONTROL 提交]**

![jsrp配置](assets/jsrp-configuration.png)

### 發佈配置 {#publishing-the-configuration}

雖然JSRP是預設配置，但要確保在發佈環境中設定相同的配置：

* 從全局導航： **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 複製]**
* 選擇 **[!UICONTROL 激活樹]** > **[!UICONTROL 起始路徑]**:

   * 瀏覽到 `/conf/global/settings/community/srpc/`

* 選擇 **[!UICONTROL 激活]**

## 管理用戶資料 {#managing-user-data}

有關 *用戶*。 *用戶配置檔案* 和 *用戶組*，通常輸入到發佈環境中，訪問：

* [用戶同步](sync.md)
* [管理用戶和用戶組](users.md)

## 疑難排解 {#troubleshooting}

### UGC在JCR中不可見 {#ugc-not-visible-in-jcr}

通過檢查儲存選項的配置，確保JSRP已配置為預設提供程式。 預設情況下，儲存資源提供程式是JSRP。

在所有作者和發佈AEM實例上，重新訪問儲存配置控制台或檢AEM查儲存庫：

* 在JCR中，如果 [/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * 不包含 [srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc) 節點，表示儲存提供程式是JSRP。
   * 如果srpc節點存在並包含節點 [預設配置](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration)，預設配置的屬性應將JSRP定義為預設提供程式。

### UGC在作者實例上不可見 {#ugc-not-visible-on-author-instance}

這不是錯誤。 JSRP的一個特點是，在發佈環境中輸入的社區內容只在發佈環境中可見。

### UGC在發佈實例上不可見 {#ugc-not-visible-on-publish-instance}

如果單個發佈實例或部署了發佈群集，請按照 [UGC在JCR中不可見](#ugc-not-visible-in-jcr)。

如果部署了發佈場，則JSRP的一個特點是社區內容將僅在發佈到的發佈實例上可見。

要使UGC在任何發佈實例中都可見，需要發佈群集。
