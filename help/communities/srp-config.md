---
title: 儲存體設定
description: 瞭解儲存設定主控台，用於識別為社群內容（也稱為使用者產生的內容）選擇的儲存空間。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 67de7e26-3f93-4034-9e3a-5c127f7447bc
solution: Experience Manager
feature: Communities
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 3%
---
# 儲存體設定 {#storage-configuration}

儲存體設定是識別為社群內容（也稱為使用者產生的內容，UGC）選擇的儲存體的方法。

此設定會通知AEM Communities程式碼，當存取UGC時，使用哪個儲存資源提供者(SRP)實作。 它必須反映部署Adobe Experience Manager (AEM)時建立的拓撲。

有關儲存選項和部署拓撲的討論，請造訪：

* [社群內容存放區](working-with-srp.md)
* [建議的拓撲](topologies.md)

## 儲存設定主控台 {#storage-configuration-console}

![jsrp-configuration](assets/jsrp-configuration.png)

在Author環境中，存取儲存設定主控台。

* 從全域導覽中，選取&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 社群]** > **[!UICONTROL 儲存設定]**

若要選取預設JCR以外的儲存選項：

* 選取一個選項
* 正確設定

  * 檢視[選取MSRP](msrp.md#select-msrp)的詳細資料
  * 檢視[選取DSRP](dsrp.md#select-dsrp)的詳細資料
  * 檢視[選取ASRP](asrp.md#select-asrp)的詳細資料

* 選取&#x200B;**[!UICONTROL 提交]**。

### 關於JCR儲存 {#about-jcr-storage}

如果未選取任何專案，預設為AEM存放庫JCR。

JCR是&#x200B;*不是*&#x200B;作者和發佈環境共用的公用存放區。 社群內容只會從建立該社群內容的作者或發佈環境中顯示。

如需其他資訊，請造訪[JCR存放區](jsrp.md)。

>[!NOTE]
>
>`/etc/socialconfig`下缺少節點`srpc`表示預設的[JCR存放區](jsrp.md)。
