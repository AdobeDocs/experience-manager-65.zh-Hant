---
title: JSRP - JCR儲存資源提供商
seo-title: JSRP - JCR Storage Resource Provider
description: JSRP通常最適合一個發佈例項和一個製作例項的示範或開發環境
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

# JSRP - JCR儲存資源提供商 {#jsrp-jcr-storage-resource-provider}

## 關於JSRP {#about-jsrp}

當AEM Communities使用JSRP作為其儲存選項（預設值）時，社群內容會儲存在JCR中，而使用者產生的內容(UGC)只能從張貼到的製作或發佈執行個體存取。

由於部署簡單，JSRP通常最適合一個發佈執行個體和一個製作執行個體的示範或開發環境。

另請參閱 [SRP選項的特點](working-with-srp.md#characteristics-of-srp-options) 和 [建議的拓撲](topologies.md).

## 設定 {#configuration}

### 選擇JSRP {#select-jsrp}

依預設，JSRP是UGC的儲存選項。

此 [儲存配置控制台](srp-config.md) 允許選擇預設儲存配置，以確定要使用的SRP實施。

在製作環境中，前往儲存設定主控台

* 從全局導航： **[!UICONTROL 工具]** > **[!UICONTROL 社群]** > **[!UICONTROL 儲存配置]**

* 選擇 **[!UICONTROL JCR儲存資源提供商(JSRP)]**

* 選擇 **[!UICONTROL 提交]**

![jsrp-configuration](assets/jsrp-configuration.png)

### 發佈設定 {#publishing-the-configuration}

雖然JSRP是預設設定，但為了確保在發佈環境中設定相同的設定：

* 從全局導航： **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 復寫]**
* 選擇 **[!UICONTROL 激活樹]** > **[!UICONTROL 起始路徑]**:

   * 瀏覽至 `/conf/global/settings/community/srpc/`

* 選擇 **[!UICONTROL 啟動]**

## 管理使用者資料 {#managing-user-data}

如需 *使用者*, *使用者設定檔* 和 *使用者群組*，通常會在發佈環境中輸入，請造訪：

* [使用者同步](sync.md)
* [管理使用者和使用者群組](users.md)

## 疑難排解 {#troubleshooting}

### UGC在JCR中不可見 {#ugc-not-visible-in-jcr}

檢查儲存選項的設定，確認JSRP已設為預設提供者。 依預設，儲存資源提供者為JSRP。

在所有製作和發佈AEM例項上，重新造訪儲存設定主控台或檢查AEM存放庫：

* 在JCR中，如果 [/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * 不包含 [srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc) 節點，表示儲存提供者為JSRP。
   * 如果srpc節點存在且包含節點 [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration),defaultconfiguration的屬性應將JSRP定義為預設提供者。

### UGC在製作執行個體上不可見 {#ugc-not-visible-on-author-instance}

這不是錯誤。 JSRP的一項特點，是在發佈環境中輸入的社群內容只會顯示在發佈環境中。

### UGC在發佈執行個體上不可見 {#ugc-not-visible-on-publish-instance}

如果單一發佈執行個體或部署了發佈叢集，請依照 [UGC在JCR中不可見](#ugc-not-visible-in-jcr).

如果已部署發佈伺服器陣列，JSRP的一個特點是，社群內容只會顯示在發佈執行個體上。

若要從任何發佈執行個體顯示UGC，需要發佈叢集。
