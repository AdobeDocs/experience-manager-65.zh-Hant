---
title: 為AEM應用程式進行配置
seo-title: 為AEM應用程式進行配置
description: 了解如何設定AEM應用程式。
seo-description: 了解如何設定AEM應用程式。
uuid: ab9acd93-da7f-4bb7-8d26-224044899068
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 34f24837-f5e2-41f0-a359-fdb695e1b8f2
exl-id: f7aa5ac0-3d03-4c04-b9c2-1bda427b0588
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---

# 為AEM應用程式進行配置{#configuring-for-aem-apps}

Adobe Experience Manager應用程式可透過空中(OTA)更新應用程式的內容。 更新的內容會儲存在發佈執行個體上。 若要允許裝置上的應用程式連線至發佈執行個體並檢查是否有更新，必須將發佈執行個體設定為允許空的反向連結標題。

## 設定空的反向連結標題{#configuring-empty-referrer-header}

若要設定反向連結篩選服務：

* 開啟Apache Felix主控台(**Configurations**)，網址為：
* https://&lt;server>:&lt;port_number>/system/console/configMgr
* 以管理員身分登入。
* 在&#x200B;**Configurations**&#x200B;菜單中，選擇：*Apache Sling Referrer Filter*
* 勾選「允許空白」欄位，以允許空白/遺失的反向連結標題。
* 按一下&#x200B;**儲存**&#x200B;以儲存變更。

![chlimage_1-58](assets/chlimage_1-58a.png)

如需詳細資訊，請參閱[OSGI組態設定](/help/sites-deploying/osgi-configuration-settings.md)和[安全性檢查清單 — 跨網站請求偽造問題](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) 。
