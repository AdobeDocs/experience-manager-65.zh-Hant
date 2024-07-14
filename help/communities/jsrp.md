---
title: JSRP - JCR儲存資源提供者
description: JSRP最適合用於一個Publish執行個體和一個作者執行個體的示範或開發環境
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 873e013c-a2da-4b37-b0e3-56bdf240004a
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# JSRP - JCR儲存資源提供者 {#jsrp-jcr-storage-resource-provider}

## 關於JSRP {#about-jsrp}

當AEM Communities使用JSRP作為其儲存選項（預設）時，社群內容儲存在JCR中，並且使用者產生的內容(UGC)只能從張貼該內容的作者或發佈執行個體存取。

由於部署的簡單性，JSRP最適合用於一個Publish執行個體和一個作者執行個體的示範或開發環境。

另請參閱[SRP選項的特性](working-with-srp.md#characteristics-of-srp-options)和[建議的拓撲](topologies.md)。

## 設定 {#configuration}

### 選取JSRP {#select-jsrp}

依預設，JSRP是UGC的儲存選項。

[儲存設定主控台](srp-config.md)允許選取預設儲存設定，以識別要使用哪個SRP實作。

在製作環境中，前往儲存設定主控台

* 從全域導覽： **[!UICONTROL 工具]** > **[!UICONTROL 社群]** > **[!UICONTROL 儲存設定]**

* 選取&#x200B;**[!UICONTROL JCR儲存資源提供者(JSRP)]**

* 選取&#x200B;**[!UICONTROL 提交]**

![jsrp-configuration](assets/jsrp-configuration.png)

### 發佈設定 {#publishing-the-configuration}

雖然JSRP是預設設定，但要確保在發佈環境中設定了相同的設定：

* 從全域導覽： **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 復寫]**
* 選取&#x200B;**[!UICONTROL 啟動樹狀結構]** > **[!UICONTROL 開始路徑]**：

   * 瀏覽至`/conf/global/settings/community/srpc/`

* 選取&#x200B;**[!UICONTROL 啟動]**

## 管理使用者資料 {#managing-user-data}

如需&#x200B;*使用者*、*使用者設定檔*&#x200B;和&#x200B;*使用者群組*&#x200B;的相關資訊（通常已進入發佈環境），請造訪：

* [使用者同步](sync.md)
* [管理使用者和使用者群組](users.md)

## 疑難排解 {#troubleshooting}

### UGC在JCR中不可見 {#ugc-not-visible-in-jcr}

請確定已透過檢查儲存選項的設定，將JSRP設定為預設提供者。 依預設，儲存資源提供者為JSRP。

在所有Author和Publish AEM執行個體上，重新造訪「儲存設定」主控台，或檢查AEM存放庫：

* 在JCR中，若為[/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * 它不包含[srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc)節點，這表示儲存提供者是JSRP。
   * 如果srpc節點存在且包含節點[defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration)，則defaultconfiguration的屬性應該將JSRP定義為預設提供者。

### UGC在作者執行個體上不可見 {#ugc-not-visible-on-author-instance}

這不是錯誤。 JSRP的特點是只可在Publish環境中看到發佈環境中輸入的社群內容。

### UGC在Publish執行個體上不可見 {#ugc-not-visible-on-publish-instance}

如果單一Publish執行個體或已部署發佈叢集，請依照[UGC在JCR](#ugc-not-visible-in-jcr)中不可見的指示操作。

如果部署了發佈陣列，JSRP的特徵是社群內容只會顯示在其張貼到的Publish執行個體上。

若要讓任何Publish執行個體都能看見UGC，則需要發佈叢集。
