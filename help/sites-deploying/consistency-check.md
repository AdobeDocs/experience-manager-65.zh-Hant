---
title: 一致性和周遊檢查
description: 瞭解如何執行一致性和周遊檢查。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
feature: Configuring
exl-id: 10dde29b-5dc7-4d4e-80ae-3d4fd0397f7e
source-git-commit: b66ec42c35b5b60804015d340b8194bbd6ef3e28
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

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

若要執行一致性檢查，請瀏覽至JMX Mbean的管理頁面 **com.adobe.granite （存放庫）**. 從AEM主畫面，前往：

**工具> Web主控台> Main （位於功能表列上） > JMX > com.adobe.granite （存放庫）**

預設安裝時，可在此處找到：  **[|顯示給我|](http://localhost:4502/system/console/jmx/com.adobe.granite%3Atype%3DRepository)**

在 **作業** 區段，您可以找到兩種方法： **`traversalCheck`** 和 **`consistencyCheck`**. 若要執行檢查，請按一下操作並輸入所需的引數。

![chlimage_1-117](assets/chlimage_1-117.png)
