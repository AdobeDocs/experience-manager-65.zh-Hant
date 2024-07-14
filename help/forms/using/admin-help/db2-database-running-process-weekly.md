---
title: 「DB2&amp；reg；資料庫：每週執行處理序」
description: 瞭解如何改善AEM Forms DB2&amp； reg；資料庫的效能。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: ca2cfe35-b602-4ef8-b4e3-af846105d4de
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---

# DB2®資料庫：每週執行處理作業{#db-database-running-a-process-weekly}

如果您的AEM Forms DB2®資料庫開始執行速度很慢，每週執行下列程式可以改善其效能：

1. 啟動DB2®控制中心：

   (Windows)選取「開始>程式> IBM® DB2® >一般管理工具>控制中心」。

   (Linux®和UNIX®)在命令提示字元中，輸入`db2jcc`命令。

1. 在DB2® Control Center物件樹狀結構中，按一下所有資料庫。
1. 按一下您為AEM Forms建立的資料庫，然後按一下「表格」資料夾。
1. 選取內容窗格中的所有資料庫表格，用滑鼠右鍵按一下這些表格，然後選取執行統計資料。
1. 移至「統計資料>索引統計資料」。
1. 選取收集所有索引的統計值，選取收集具有延伸詳細統計值的索引的統計值，然後按一下確定。

當程式完成時，會顯示一則訊息。 關閉訊息。
