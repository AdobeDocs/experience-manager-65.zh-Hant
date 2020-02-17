---
title: AEM Forms Workspace架構
seo-title: AEM Forms Workspace架構
description: LiveCycle AEM Forms工作區架構的概念資訊和概觀。
seo-description: LiveCycle AEM Forms工作區架構的概念資訊和概觀。
uuid: e1a48452-ed44-4ea7-ba38-d961c8faafa5
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c3a312fb-f684-477d-916d-2d3c99aa7607
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# AEM Forms Workspace架構 {#aem-forms-workspace-architecture}

AEM Forms工作區是代管於CRX™的Web應用程式。 在瀏覽器中開啟工作區時，會存取CRX資源，並在瀏覽器中將應用程式轉譯為HTML頁面。

應用程式會存取REST端點上的AEM Forms伺服器，以執行下列動作：

* 獲取用戶任務、進程起點、進程歷史記錄和用戶資訊
* 對任務執行操作
* 資料庫中的查詢任務
* 更新使用者偏好設定等

AEM Forms伺服器可透過JDBC存取AEM Forms資料庫。 資料庫會保留任務、進程及其實例、用戶和相關資訊。

AEM Forms工作區設計為模組化JavaScript™元件，可個別自訂，並在其他Web應用程式中重複使用。 這些元件是以BackBone為基礎，JavaScript程式庫可為Web應用程式提供結構。 這裡是描述元件與BackBone互動的詳細文 [章](/help/forms/using/backbone-interaction.md)。 本文討論了CRX資料夾結構中的元件 [組](/help/forms/using/folder-structure.md) 織。

針對AEM Forms工作區傳送的套件：

* `adobe-lc-workspace-pkg-<version>.zip`:它是CRX包，即，它可以使用包管理器在CRX中部署。
* `adobe-lc-workspace-<version>-src.zip`:此封存包含AEM Forms工作區的完整程式碼和指令碼，以建立部署套件——發運、除錯和開發套件。

**[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)**
