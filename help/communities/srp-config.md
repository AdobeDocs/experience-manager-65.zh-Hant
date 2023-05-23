---
title: 儲存設定
seo-title: Storage Configuration
description: 如何訪問儲存配置控制台
seo-description: How to access the Storage Configuration Console
uuid: 6a5a71d5-6aaa-4635-8852-4dae33c497a9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 71fac7e9-814a-48b5-b816-9bdcb2a05190
role: Admin
exl-id: 67de7e26-3f93-4034-9e3a-5c127f7447bc
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 3%

---

# 儲存設定 {#storage-configuration}

儲存配置是標識為社區內容選擇的儲存的方法，也稱為用戶生成的內容(UGC)。

此設定通知AEM Communities代碼，在訪問UGC時將使用儲存資源提供程式(SRP)的實現，並且必須反映部署時建立AEM的拓撲。

有關儲存選項和部署拓撲的討論，請訪問：

* [社區內容儲存](working-with-srp.md)
* [推薦的拓撲](topologies.md)

## 儲存配置控制台 {#storage-configuration-console}

![jsrp配置](assets/jsrp-configuration.png)

在作者環境中，訪問儲存配置控制台。

* 從全局導航中，選擇 **[!UICONTROL 工具]** > **[!UICONTROL 社區]** > **[!UICONTROL 儲存配置]**

要選擇預設JCR以外的儲存選項：

* 選擇選項
* 適當配置

   * 查看詳細資訊 [選擇MSRP](msrp.md#select-msrp)
   * 查看詳細資訊 [選擇DSRP](dsrp.md#select-dsrp)
   * 查看詳細資訊 [選擇ASRP](asrp.md#select-asrp)

* 選擇 **[!UICONTROL 提交]**。

### 關於JCR儲存 {#about-jcr-storage}

請注意，如果未進行任何選擇，則預設為AEM儲存庫JCR。

JCR為 *不* 由作者和發佈環境共用的公用儲存。 社區內容將僅從建立社區內容的作者或發佈環境中可見。

訪問 [JCR儲存](jsrp.md) 的雙曲餘切值。

>[!NOTE]
>
>節點的缺失 `srpc` 在 `/etc/socialconfig` 指示預設值 [JCR儲存](jsrp.md)。
