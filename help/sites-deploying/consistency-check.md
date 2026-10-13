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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 523b1ccd-901e-5e3b-9fa7-f3dfd82463d5
    internal-label: Configuring
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '156'
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
