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

儲存配置是標識為社區內容選擇的儲存的方法，也稱為用戶生成內容(UGC)。

此設定會通知AEM Communities程式碼，在存取UGC時將使用哪個儲存資源提供者(SRP)實作，且必須反映部署AEM時建立的拓撲。

有關儲存選項和部署拓撲的討論，請訪問：

* [社群內容商店](working-with-srp.md)
* [建議的拓撲](topologies.md)

## 儲存配置控制台 {#storage-configuration-console}

![jsrp-configuration](assets/jsrp-configuration.png)

在製作環境中，存取儲存設定主控台。

* 在全局導航中，選擇 **[!UICONTROL 工具]** > **[!UICONTROL 社群]** > **[!UICONTROL 儲存配置]**

要選擇預設JCR以外的儲存選項：

* 選擇選項
* 適當配置

   * 請參閱 [選擇MSRP](msrp.md#select-msrp)
   * 請參閱 [選擇DSRP](dsrp.md#select-dsrp)
   * 請參閱 [選擇ASRP](asrp.md#select-asrp)

* 選擇 **[!UICONTROL 提交]**.

### 關於JCR儲存 {#about-jcr-storage}

請注意，如果未選取，預設為AEM存放庫JCR。

JCR為 *not* 製作和發佈環境共用的公用存放區。 社群內容只會從建立該內容的製作或發佈環境中顯示。

瀏覽 [JCR商店](jsrp.md) 以取得其他資訊。

>[!NOTE]
>
>節點不存在 `srpc` 在 `/etc/socialconfig` 表示預設值 [JCR商店](jsrp.md).
