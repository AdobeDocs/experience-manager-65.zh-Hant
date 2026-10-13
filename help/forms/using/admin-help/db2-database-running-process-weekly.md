---
title: DB2&reg； database：每週執行處理作業
description: 瞭解如何改善AEM Forms DB2&reg；資料庫的效能。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: ca2cfe35-b602-4ef8-b4e3-af846105d4de
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%
---
# DB2®資料庫：每週執行處理作業{#db-database-running-a-process-weekly}

如果您的AEM Forms DB2®資料庫開始執行速度很慢，每週執行下列程式可以改善其效能：

1. 啟動DB2®控制中心：

   (Windows)選取「開始>程式> ® DB2® >一般管理工具>控制中心」。

   （Linux®和UNIX®）在命令提示字元中，輸入`db2jcc`命令。

1. 在DB2® Control Center物件樹狀結構中，按一下所有資料庫。
1. 按一下您為AEM Forms建立的資料庫，然後按一下「表格」資料夾。
1. 選取內容窗格中的所有資料庫表格，用滑鼠右鍵按一下這些表格，然後選取執行統計資料。
1. 移至「統計資料>索引統計資料」。
1. 選取收集所有索引的統計值，選取收集具有延伸詳細統計值的索引的統計值，然後按一下確定。

當程式完成時，會顯示一則訊息。 關閉訊息。
