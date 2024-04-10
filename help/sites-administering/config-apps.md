---
title: 為AEM應用程式進行設定
description: 瞭解如何使用Adobe Experience Manager應用程式來更新應用程式OTA的內容（透過Air）。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: f7aa5ac0-3d03-4c04-b9c2-1bda427b0588
solution: Experience Manager, Experience Manager Sites
feature: Configuring
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 1%

---

# 為AEM應用程式進行設定{#configuring-for-aem-apps}

Adobe Experience Manager應用程式可讓您更新應用程式OTA的內容（透過Air）。 更新的內容會儲存在發佈執行個體上。 若要允許裝置上的應用程式連線至發佈執行個體並檢查更新，必須將發佈執行個體設定為允許空的反向連結標題。

## 設定空的反向連結標題 {#configuring-empty-referrer-header}

若要設定反向連結篩選服務：

* 開啟Apache Felix主控台(**設定**)於：
* https://&lt;server>：&lt;port_number>/system/console/configMgr
* 以管理員身分登入。
* 在 **設定** 功能表，選取： *Apache Sling查閱者篩選器*
* 勾選「允許空白」欄位，以便您可以允許空白/遺失反向連結標題。
* 按一下 **儲存** 以儲存變更。

![chlimage_1-58](assets/chlimage_1-58a.png)

請參閱 [OSGI組態設定](/help/sites-deploying/osgi-configuration-settings.md) 和 [安全性檢查清單 — 跨網站請求偽造問題](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) 以取得更多詳細資料。
