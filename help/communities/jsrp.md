---
title: JSRP - JCR儲存資源提供商
seo-title: JSRP - JCR儲存資源提供商
description: JSRP通常最適合用於一個發佈實例和一個作者實例的演示或開發環境
seo-description: JSRP通常最適合用於一個發佈實例和一個作者實例的演示或開發環境
uuid: 358a43c1-4137-4300-8443-c0d7166968ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: f5316a73-84e2-4a18-98c1-a384eeaa77cf
role: 管理員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---


# JSRP - JCR儲存資源提供程式{#jsrp-jcr-storage-resource-provider}

## 關於JSRP {#about-jsrp}

當AEM Communities使用JSRP作為其儲存選項（預設值）時，社群內容會儲存在JCR中，而且使用者產生的內容(UGC)只能從作者或發佈實例存取。

由於部署簡單，JSRP通常最適合用於一個發佈實例和一個作者實例的演示或開發環境。

另請參見[SRP選項的特性](working-with-srp.md#characteristics-of-srp-options)和[建議拓撲](topologies.md)。

## 設定 {#configuration}

### 選擇JSRP {#select-jsrp}

預設情況下，JSRP是UGC的儲存選項。

[儲存配置控制台](srp-config.md)允許選擇預設儲存配置，該配置標識要使用的SRP實施。

在作者環境中，要訪問儲存配置控制台

* 從全域導覽：**[!UICONTROL 工具]** > **[!UICONTROL 社區]** > **[!UICONTROL 儲存配置]**

* 選擇&#x200B;**[!UICONTROL JCR儲存資源提供程式(JSRP)]**

* 選擇&#x200B;**[!UICONTROL 提交]**

![jsrp-configuration](assets/jsrp-configuration.png)

### 發佈配置{#publishing-the-configuration}

雖然JSRP是預設設定，但若要確保在發佈環境中設定相同的設定：

* 從全域導覽：**[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 複製]**
* 選擇&#x200B;**[!UICONTROL 激活樹]** > **[!UICONTROL 啟動路徑]**:

   * 瀏覽至`/conf/global/settings/community/srpc/`

* 選擇&#x200B;**[!UICONTROL 激活]**

## 管理用戶資料{#managing-user-data}

有關&#x200B;*用戶*、*用戶概要檔案*&#x200B;和&#x200B;*用戶組*&#x200B;的資訊，請訪問：

* [用戶同步](sync.md)
* [管理使用者和使用者群組](users.md)

## 疑難排解 {#troubleshooting}

### UGC在JCR {#ugc-not-visible-in-jcr}中不可見

通過檢查儲存選項的配置，確保JSRP已配置為預設提供程式。 預設情況下，儲存資源提供方是JSRP。

在所有作者和發佈實例AEM上，重新訪問儲存配置控制台或檢查存AEM儲庫：

* 在JCR中，如果[/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * 不包含[srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc)節點，表示儲存提供程式是JSRP。
   * 如果srpc節點存在並包含節點[defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration)，則defaultconfiguration的屬性應將JSRP定義為預設提供程式。

### 作者實例{#ugc-not-visible-on-author-instance}上不顯示UGC

這不是錯誤。 JSRP的特點是，在發佈環境中輸入的社群內容只能在發佈環境中顯示。

### UGC在發佈實例{#ugc-not-visible-on-publish-instance}上不可見

如果單個發佈實例或已部署發佈群集，則按照[UGC Not Visible in JCR](#ugc-not-visible-in-jcr)的說明操作。

如果部署了發佈群，JSRP的一個特點是，社群內容只會顯示在發佈實例上。

UGC若要從任何發佈例項中顯示，則需要發佈叢集。
