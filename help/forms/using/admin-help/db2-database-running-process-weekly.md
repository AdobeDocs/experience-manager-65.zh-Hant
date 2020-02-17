---
title: '"DB2資料庫：每週運行進程」'
seo-title: '"DB2資料庫：每週運行進程」'
description: 瞭解如何改善AEM表單DB2資料庫的效能。
seo-description: 瞭解如何改善AEM表單DB2資料庫的效能。
uuid: 36070087-c250-41df-a841-aa922e777697
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fc0e8183-5d50-4fc0-997a-5f3168ba0d70
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# DB2資料庫：每週運行流程{#db-database-running-a-process-weekly}

如果您的AEM表單DB2資料庫開始緩慢執行，每週執行下列程式可改善其效能：

1. 啟動DB2控制中心：

   (Windows)選擇「開始」>「程式」>「IBM DB2」>「一般管理工具」>「控制中心」。

   （Linux和UNIX）在命令提示符下，鍵入命 `db2jcc` 令。

1. 在DB2 Control Center對象樹中，按一下所有資料庫。
1. 按一下您為AEM表單建立的資料庫，然後按一下「表格」檔案夾。
1. 在內容窗格中選擇所有資料庫表，按一下右鍵它們，然後選擇運行統計資訊。
1. 轉至「統計資料>索引統計資料」。
1. 選擇收集所有索引的統計資訊，選擇收集具有擴展詳細統計資訊的索引的統計資訊，然後按一下確定。

當程式完成時，將顯示一條消息。 關閉訊息。
