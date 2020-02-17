---
title: 儲存設定
seo-title: 儲存設定
description: 如何訪問儲存配置控制台
seo-description: 如何訪問儲存配置控制台
uuid: 6a5a71d5-6aaa-4635-8852-4dae33c497a9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 71fac7e9-814a-48b5-b816-9bdcb2a05190
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 儲存設定 {#storage-configuration}

儲存配置是標識為社區內容選擇的儲存的方法，也稱為用戶生成內容(UGC)。

此設定會通知AEM Communities程式碼，說明在存取UGC時，將使用哪個儲存資源提供者(SRP)實作，且必須反映部署AEM時建立的拓撲。

有關儲存選項和部署拓撲的討論，請訪問

* [社群內容商店](working-with-srp.md)
* [建議的拓撲](topologies.md)

## 儲存配置控制台 {#storage-configuration-console}

![chlimage_1-188](assets/chlimage_1-188.png)

在作者環境中，要訪問儲存配置控制台

* 從全域導覽：「工 **[!UICONTROL 具>社群>儲存設定」]**

要選擇預設JCR以外的儲存選項：

* 選擇選項
* 正確配置

   * 請參閱選擇MSRP的 [詳細資訊](msrp.md#select-msrp)
   * 請參閱選擇DSRP的 [詳細資訊](dsrp.md#select-dsrp)
   * 請參閱選擇ASRP的 [詳細資訊](asrp.md#select-asrp)

* 選擇「提 **[!UICONTROL 交」]**

### 關於JCR儲存 {#about-jcr-storage}

請注意，如果未進行任何選取，預設值為AEM儲存庫JCR。

JCR不是 *作者* 和發佈環境共用的公用商店。 社群內容只會從建立社群內容的作者或發佈環境中看到。

請造 [訪JCR商店](jsrp.md) ，以取得其他資訊。

>[!NOTE]
>
>缺少下面的節 `srpc`點 `/etc/socialconfig` 表示預設 [JCR儲存](jsrp.md)。

