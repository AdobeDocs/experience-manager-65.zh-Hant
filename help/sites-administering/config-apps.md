---
title: 為AEM應用程式設定
seo-title: 為AEM應用程式設定
description: 瞭解如何設定AEM應用程式。
seo-description: 瞭解如何設定AEM應用程式。
uuid: ab9acd93-da7f-4bb7-8d26-224044899068
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 34f24837-f5e2-41f0-a359-fdb695e1b8f2
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7

---


# 為AEM應用程式設定{#configuring-for-aem-apps}

Adobe Experience Manager Apps提供透過Air(OTA)更新應用程式內容的功能。 更新的內容會儲存在發佈例項上。 若要允許裝置上的應用程式連線至發佈例項並檢查更新，必須將發佈例項設定為允許空的反向連結標題。

## 設定空的反向連結標題 {#configuring-empty-referrer-header}

若要設定反向連結篩選服務：

* 開啟Apache Felix主控台(**設定**):
* https://&lt;server>:&lt;port_number>/system/console/configMgr
* 以管理員身分登入。
* 在「配 **置** 」菜單中，選擇： *Apache Sling Referrer Filter*
* 勾選「允許空白」欄位，以允許空白／遺失反向連結標題。
* 按一 **下「儲存** 」以儲存變更。

![chlimage_1-58](assets/chlimage_1-58a.png)

如需詳細 [資訊，請參閱OSGI設定](/help/sites-deploying/osgi-configuration-settings.md)[與安全性檢查清單——跨網站偽造要求的問題](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) 。
