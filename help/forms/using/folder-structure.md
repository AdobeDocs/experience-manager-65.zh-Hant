---
title: 瞭解資料夾結構
seo-title: 瞭解資料夾結構
description: 如何瞭解要自訂的AEM Forms工作區原始碼的檔案夾結構。
seo-description: 如何瞭解要自訂的AEM Forms工作區原始碼的檔案夾結構。
uuid: ee844f89-887e-4f07-9db3-389859baa374
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 7427858d-8eec-423d-a0a9-444140420620
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# 瞭解資料夾結構{#understanding-the-folder-structure}

AEM Forms工作區元件是使用Backbone，以MVC架構設計。 每個元件都有一個檔案：

* 模型，其中包含商業邏輯。
* 範本，即包含介面控制項的HTML檔案。
* 視圖，它充當模板的控制器類。

所有元件的資產都放在下方所述的檔案夾結構中。 若要存取資產，請登入CRXDE Lite並瀏覽至`/libs/ws/js/runtime/`。

**模** 型包含骨幹模型。

**視** 圖包含骨幹視圖。

**范** 本僅包含元件的HTML範本。

**路** 由包含通用路由。路由內的範本資料夾包含HTML程式碼和元件參考。

**服** 務包含在REST端點上呼叫Adobe Experience Manager伺服器API的服務介面。

**util** 包含可由多個元件使用的通用實用程式。
