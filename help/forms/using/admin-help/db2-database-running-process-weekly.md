---
title: '"DB2資料庫：每週運行進程」'
seo-title: "DB2 database: Running a process weekly"
description: 了解如何改進AEM Forms DB2資料庫的效能。
seo-description: See how you can improve the performance of your AEM forms DB2 database.
uuid: 36070087-c250-41df-a841-aa922e777697
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fc0e8183-5d50-4fc0-997a-5f3168ba0d70
exl-id: ca2cfe35-b602-4ef8-b4e3-af846105d4de
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# DB2資料庫：每週運行進程{#db-database-running-a-process-weekly}

如果您的AEM表單DB2資料庫開始緩慢執行，每週執行下列程式可改善其效能：

1. 啟動DB2控制中心：

   (Windows)選擇「開始」>「程式」>「IBM DB2」>「常規管理工具」>「控制中心」。

   （Linux和UNIX）在命令提示符下，鍵入 `db2jcc` 命令。

1. 在DB2控制中心對象樹中，按一下所有資料庫。
1. 按一下為AEM表單建立的資料庫，然後按一下表格資料夾。
1. 選擇「內容」窗格中的所有資料庫表，按一下右鍵並選擇「運行統計資訊」。
1. 轉至「統計>索引統計」。
1. 選擇收集所有索引的統計資訊，選擇收集具有擴展詳細統計資訊的索引的統計資訊，然後按一下確定。

進程完成時，將顯示一條消息。 關閉訊息。
