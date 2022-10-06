---
title: AEM Forms Workspace架構
seo-title: AEM Forms Workspace Architecture
description: LiveCycleAEM Forms工作區架構的概念資訊和概觀。
seo-description: Conceptual information and overview of the architecture of LiveCycle AEM Forms workspace.
uuid: e1a48452-ed44-4ea7-ba38-d961c8faafa5
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c3a312fb-f684-477d-916d-2d3c99aa7607
exl-id: c6f216d4-781c-4356-b9f0-3324903a28e7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# AEM Forms Workspace架構 {#aem-forms-workspace-architecture}

AEM Forms工作區是在CRX™上托管的網頁應用程式。 在瀏覽器中開啟工作區時，會存取CRX資源，並將應用程式轉譯為瀏覽器中的HTML頁面。

應用程式會在REST端點上存取AEM Forms伺服器，以執行下列作業：

* 獲取用戶任務、進程起始點、進程歷史記錄和用戶資訊
* 對任務執行操作
* 資料庫中的查詢任務
* 更新使用者偏好設定等

AEM Forms伺服器透過JDBC存取AEM Forms資料庫。 資料庫會保存任務、進程及其實例、用戶和相關資訊。

AEM Forms工作區設計為模組化JavaScript™元件，可個別自訂，並在其他Web應用程式中重複使用。 這些元件以BackBone為基礎，BackBone是一個JavaScript程式庫，為Web應用程式提供結構。 本文詳細描述了元件與BackBone的交互 [此處](/help/forms/using/backbone-interaction.md). CRX資料夾結構中的元件組織在 [此](/help/forms/using/folder-structure.md) 文章。

為AEM Forms工作區提供的套件：

* `adobe-lc-workspace-pkg-<version>.zip`:它是CRX套件，即可使用套件管理器在CRX中部署。
* `adobe-lc-workspace-<version>-src.zip`:此封存包含AEM Forms工作區的完整程式碼和建立部署套件（發運、除錯和開發套件）的指令碼。
