---
title: 瞭解資料夾結構
seo-title: Understanding the folder structure
description: 如何理解AEM Forms工作區原始碼的資料夾結構進行自定義。
seo-description: How to understand the folder structure of AEM Forms workspace source code to customize.
uuid: ee844f89-887e-4f07-9db3-389859baa374
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 7427858d-8eec-423d-a0a9-444140420620
exl-id: a4c1d3d8-477e-4edf-9dde-4ef9c766be5a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# 瞭解資料夾結構 {#understanding-the-folder-structure}

AEM Forms工作區元件是使用Backbone在MVC架構上設計的。 每個元件都有一個檔案，用於：

* 模型，包含商業邏輯。
* 模板，即包含介面控制項的HTML檔案。
* 視圖，它充當模板的控制器類。

所有元件的資產都放置在下面描述的資料夾結構中。 要訪問資產，請登錄到CRXDE Lite並瀏覽到 `/libs/ws/js/runtime/`。

**模型** 包含主幹模型。

**視圖** 包含主幹視圖。

**模板** 僅包含元件的HTML模板。

**路由** 包含通用路由。 路由中的模板資料夾包含HTML代碼和對元件的引用。

**服務** 包含在REST終結點上調用Adobe Experience Manager伺服器API的服務介面。

**實用** 包含可由多個元件使用的通用實用程式。
