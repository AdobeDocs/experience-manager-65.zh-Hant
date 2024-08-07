---
title: 一致性和周遊檢查
description: 瞭解如何執行一致性和周遊檢查。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
feature: Configuring
exl-id: 10dde29b-5dc7-4d4e-80ae-3d4fd0397f7e
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 1%

---

# 一致性和周遊檢查{#consistency-and-traversal-checks}

升級時，可能會因為工作區不一致而發生問題。 您可以執行測試升級以檢視這是否為問題，或執行一致性檢查作為預防性動作。

如果您執行因工作區不一致而失敗的測試升級，您會在crx-quickstart/logs/crx/error.log中看到類似下列的專案：

```xml
*ERROR* TarPersistenceManager: No bundle found for uuid 'deadbeef-cafe-babe-cafe-babecafebabe'
 ...
*ERROR* RepositoryImpl: Failed to initialize workspace 'crx.default'
javax.jcr.RepositoryException: Error indexing workspace: Error indexing workspace: Error indexing workspace
...
```

## 執行一致性檢查 {#perform-a-consistency-check}

若要執行一致性檢查，請瀏覽至JMX Mbean **com.adobe.granite （儲存庫）**&#x200B;的管理頁面。 從AEM主畫面，前往：

**工具> Web主控台> Main （在功能表列上） > JMX > com.adobe.granite （存放庫）**

在預設安裝中，它位於此處： **[|顯示我|](http://localhost:4502/system/console/jmx/com.adobe.granite%3Atype%3DRepository)**

在頁面的&#x200B;**作業**&#x200B;區段中，您找到兩個方法： **`traversalCheck`**&#x200B;和&#x200B;**`consistencyCheck`**。 若要執行檢查，請按一下操作並輸入所需的引數。

![chlimage_1-117](assets/chlimage_1-117.png)
