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
role: 管理員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 4%

---


# 儲存設定 {#storage-configuration}

儲存配置是標識為社區內容選擇的儲存的方法，也稱為用戶生成內容(UGC)。

此設定通知AEM Communities代碼，在訪問UGC時將使用哪個儲存資源提供程式(SRP)的實施，並且必須反映部署時建立AEM的拓撲。

有關儲存選項和部署拓撲的討論，請訪問：

* [社群內容商店](working-with-srp.md)
* [建議的拓撲](topologies.md)

## 儲存配置控制台{#storage-configuration-console}

![jsrp-configuration](assets/jsrp-configuration.png)

在作者環境中，要訪問儲存配置控制台。

* 在全局導航中，選擇&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 社區]** > **[!UICONTROL 儲存配置]**

要選擇預設JCR以外的儲存選項：

* 選擇選項
* 正確配置

   * 請參閱[選擇MSRP](msrp.md#select-msrp)的詳細資訊
   * 請參閱[選擇DSRP](dsrp.md#select-dsrp)的詳細資訊
   * 請參閱[選擇ASRP](asrp.md#select-asrp)的詳細資訊

* 選擇&#x200B;**[!UICONTROL 提交]**。

### 關於JCR儲存{#about-jcr-storage}

請注意，如果未進行任何選擇，則預設值為AEM儲存庫JCR。

JCR是&#x200B;*not*&#x200B;作者和發佈環境共用的公用商店。 社群內容只會從建立社群內容的作者或發佈環境中看到。

請造訪[JCR Store](jsrp.md)以取得其他資訊。

>[!NOTE]
>
>`/etc/socialconfig`下沒有節點`srpc`表示預設[JCR store](jsrp.md)。
