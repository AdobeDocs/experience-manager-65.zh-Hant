---
title: 了解資料夾結構
seo-title: 了解資料夾結構
description: 如何了解要自訂的AEM Forms工作區原始碼的資料夾結構。
seo-description: 如何了解要自訂的AEM Forms工作區原始碼的資料夾結構。
uuid: ee844f89-887e-4f07-9db3-389859baa374
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 7427858d-8eec-423d-a0a9-444140420620
exl-id: a4c1d3d8-477e-4edf-9dde-4ef9c766be5a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# 了解資料夾結構{#understanding-the-folder-structure}

AEM Forms工作區元件是使用骨幹架構以MVC架構設計。 每個元件都有一個檔案，用於：

* 模型，包含商業邏輯。
* 範本，即包含介面控制項的HTML檔案。
* 視圖，它作為模板的控制器類。

所有元件的資產會置於下述的資料夾結構中。 若要存取資產，請登入CRXDE Lite並瀏覽至`/libs/ws/js/runtime/`。

**** models包含骨幹模型。

**** views包含骨幹檢視。

**** 範本僅包含元件的HTML範本。

**** routes包含通用路由。路由內的範本資料夾包含HTML程式碼和元件的參考。

**** servicesContains服務介面，用於在REST端點上呼叫Adobe Experience Manager伺服器API。

**** utilContains可由多個元件使用的通用實用程式。
