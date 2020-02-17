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
translation-type: tm+mt
source-git-commit: aa2c75e061e00ba74d54843a5f35bb7d82d12a92

---


# JSRP - JCR儲存資源提供商 {#jsrp-jcr-storage-resource-provider}

## 關於JSRP {#about-jsrp}

當AEM Communities使用JSRP做為儲存選項（預設值）時，社群內容會儲存在JCR中，而使用者產生的內容(UGC)只能從發佈內容的作者或發佈例項存取。

由於部署簡單，JSRP通常最適合用於一個發佈實例和一個作者實例的演示或開發環境。

另請參 [閱SRP選項和建議的](working-with-srp.md#characteristics-of-srp-options)[拓撲特性](topologies.md)。

## 設定 {#configuration}

### 選擇JSRP {#select-jsrp}

預設情況下，JSRP是UGC的儲存選項。

存 [儲配置控制台](srp-config.md) (Storage Configuration Console)允許選擇預設儲存配置，該配置標識要使用的SRP實施。

在作者環境中，要訪問儲存配置控制台

* 從全域導覽：「工 **[!UICONTROL 具>社群>儲存設定」]**

![chlimage_1-234](assets/chlimage_1-234.png)

* Select **[!UICONTROL JCR Storage Resource Provider (JSRP)]**
* 選擇「提 **[!UICONTROL 交」]**

### 發佈設定 {#publishing-the-configuration}

雖然JSRP是預設設定，但若要確保在發佈環境中設定相同的設定：

* 作者：

   * 從全域導覽：工 **[!UICONTROL 具>部署>複製]**
   * 選擇 **[!UICONTROL 激活樹]**
   * **[!UICONTROL 開始路徑]**:

      * 瀏覽至 `/conf/global/settings/community/srpc/`
   * 選取「啟 **[!UICONTROL 動」]**


## 管理使用者資料 {#managing-user-data}

如需使用者 *、使用者****、使用者*&#x200B;設定檔和使用者群組的相關資訊，請造訪

* [用戶同步](sync.md)
* [管理使用者和使用者群組](users.md)

## 疑難排解 {#troubleshooting}

### UGC在JCR中不可見 {#ugc-not-visible-in-jcr}

通過檢查儲存選項的配置，確保JSRP已配置為預設提供程式。 預設情況下，儲存資源提供方是JSRP。

在所有作者和發佈AEM例項上，請重新造訪「儲存組態控制台」或檢查AEM存放庫：

* 在JCR中，如果 [/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * 不包含srpc節 [點](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc) ，這表示儲存提供程式是JSRP
   * 如果srpc節點存在並包含節點 [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration)，則defaultconfiguration的屬性應將JSRP定義為預設提供程式

### UGC在作者例項上不可見 {#ugc-not-visible-on-author-instance}

這不是錯誤。 JSRP的特點是，在發佈環境中輸入的社群內容只能在發佈環境中顯示。

### UGC在發佈例項上不可見 {#ugc-not-visible-on-publish-instance}

如果單個發佈實例或已部署發佈群集，請遵循「 [UGC Not Visible in JCR」(在JCR中不可見](#ugc-not-visible-in-jcr)UGC)的說明。

如果部署了發佈群，JSRP的一個特點是，社群內容只會顯示在發佈實例上。

UGC若要從任何發佈例項中顯示，則需要發佈叢集。
