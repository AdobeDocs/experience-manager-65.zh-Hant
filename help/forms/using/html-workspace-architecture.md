---
title: AEM Forms工作區體系結構
seo-title: AEM Forms Workspace Architecture
description: 概念資訊和LiveCycleAEM Forms工作區體系結構概述。
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

# AEM Forms工作區體系結構 {#aem-forms-workspace-architecture}

AEM Forms工作區是CRX™上托管的Web應用程式。 在瀏覽器中開啟工作區時，會訪問CRX資源，並在瀏覽器中將應用程式呈現為HTML頁。

應用程式訪問REST端點上的AEM Forms伺服器以執行以下操作：

* 獲取用戶任務、進程起始點、進程歷史記錄和用戶資訊
* 對任務執行操作
* 查詢資料庫中的任務
* 更新用戶首選項及更多

AEM Forms伺服器通過JDBC訪問AEM Forms資料庫。 資料庫會保留任務、進程及其實例、用戶和相關資訊。

AEM Forms工作區設計為模組化JavaScript™元件，可單獨定制並在其他Web應用程式中重新使用。 這些元件基於BackBone,JavaScript庫為Web應用程式提供結構。 詳細描述了BackBone與元件間的相互作用 [這裡](/help/forms/using/backbone-interaction.md)。 有關CRX資料夾結構中元件的組織，請參見 [這個](/help/forms/using/folder-structure.md) 文章。

為AEM Forms工作區提供的包：

* `adobe-lc-workspace-pkg-<version>.zip`:它是CRX包，也就是說，它可以使用包管理器在CRX中部署。
* `adobe-lc-workspace-<version>-src.zip`:它是一個存檔，包含AEM Forms工作區的完整代碼和用於建立部署包的指令碼 — 發運、調試和開發包。
