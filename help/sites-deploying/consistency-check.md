---
title: 一致性和遍歷檢查
seo-title: Consistency and Traversal Checks
description: 瞭解如何執行一致性和遍歷檢查。
seo-description: Learn how to perform consistency and traversal checks.
uuid: 0304e378-7c60-4bf5-9052-d01149d2a6df
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: af9a3e9d-194a-42e5-be28-b238e0c1e55e
feature: Configuring
exl-id: 10dde29b-5dc7-4d4e-80ae-3d4fd0397f7e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# 一致性和遍歷檢查{#consistency-and-traversal-checks}

升級時，可能由於工作區不一致而出現問題。 您可以運行test升級，以查看這是否是問題，也可以將一致性檢查作為預防性操作運行。

如果運行由於工作區不一致而失敗的test升級，您將在crx-quickstart/logs/crx/error.log中看到類似以下內容的條目：

```xml
*ERROR* TarPersistenceManager: No bundle found for uuid 'deadbeef-cafe-babe-cafe-babecafebabe'
 ...
*ERROR* RepositoryImpl: Failed to initialize workspace 'crx.default'
javax.jcr.RepositoryException: Error indexing workspace: Error indexing workspace: Error indexing workspace
...
```

## 執行一致性檢查 {#perform-a-consistency-check}

要執行一致性檢查，請導航到JMX Mbean** com.adobe.granite（儲存庫）**的管理頁。 從主屏AEM幕，轉到：

**「工具」>「Web控制台」>「主」（在菜單欄上）>「JMX」>com.adobe.granite（儲存庫）**

在預設安裝中，可在以下位置找到：  **[|顯示我|](http://localhost:4502/system/console/jmx/com.adobe.granite%3Atype%3DRepository)**

在 **操作** 找到以下兩種方法： **`traversalCheck`** 和 **`consistencyCheck`**。 要執行檢查，請按一下操作並輸入所需參數。

![chlimage_1-117](assets/chlimage_1-117.png)
