---
title: 為應用配AEM置
seo-title: Configuring for AEM Apps
description: 瞭解如何配置應AEM用。
seo-description: Learn how to configure AEM Apps.
uuid: ab9acd93-da7f-4bb7-8d26-224044899068
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 34f24837-f5e2-41f0-a359-fdb695e1b8f2
exl-id: f7aa5ac0-3d03-4c04-b9c2-1bda427b0588
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# 為應用配AEM置{#configuring-for-aem-apps}

Adobe Experience Manager應用提供了通過空中(OTA)更新應用程式內容的功能。 更新的內容儲存在發佈實例上。 若要允許設備上的應用程式連接到發佈實例並檢查更新，需要將發佈實例配置為允許空的引用者標頭。

## 配置空引用者標頭 {#configuring-empty-referrer-header}

要配置引用程式篩選器服務，請執行以下操作：

* 開啟Apache Felix控制台(**配置**):
* https://&lt;server>:&lt;port_number>/system/console/configMgr
* 以管理員身份登錄。
* 在 **配置** ，選擇 *Apache Sling引用篩選器*
* 選中「允許空」欄位，以允許空/缺少引用器標頭。
* 按一下 **保存** 的子菜單。

![chlimage_1-58](assets/chlimage_1-58a.png)

查看 [OSGI配置設定](/help/sites-deploying/osgi-configuration-settings.md) 和 [安全檢查表 — 跨站點請求偽造問題](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) 的上界。
