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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 523b1ccd-901e-5e3b-9fa7-f3dfd82463d5
    internal-label: Configuring
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 1%
---
# 為AEM應用程式進行設定{#configuring-for-aem-apps}

Adobe Experience Manager應用程式可讓您更新應用程式OTA的內容（透過Air）。 更新的內容會儲存在發佈執行個體上。 若要允許裝置上的應用程式連線至發佈執行個體並檢查更新，必須將發佈執行個體設定為允許空的反向連結標題。

## 設定空的反向連結標題 {#configuring-empty-referrer-header}

若要設定反向連結篩選服務：

* 在下列位置開啟Apache Felix主控台（**組態**）：
* https://<server>：<port_number>/system/console/configMgr
* 以管理員身分登入。
* 在&#x200B;**設定**&#x200B;功能表中，選取： *Apache Sling反向連結篩選器*
* 勾選「允許空白」欄位，以便您可以允許空白/遺失反向連結標題。
* 按一下[儲存]儲存變更。****

![chlimage_1-58](assets/chlimage_1-58a.png)

如需詳細資訊，請參閱[OSGI組態設定](/help/sites-deploying/osgi-configuration-settings.md)和[安全性檢查清單 — 跨網站請求偽造問題](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery)。
