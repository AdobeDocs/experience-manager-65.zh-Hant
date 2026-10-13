---
title: 瞭解檔案夾結構
description: 如何瞭解AEM Forms工作區原始碼的檔案夾結構以自訂。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: a4c1d3d8-477e-4edf-9dde-4ef9c766be5a
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%
---
# 瞭解檔案夾結構 {#understanding-the-folder-structure}

AEM Forms工作區元件是使用Backbone在MVC架構上設計。 每個元件都有一個檔案，用於：

* 模型，包含商業邏輯。
* 範本，即包含介面控制項的HTML檔案。
* 作為範本的Controller類別的檢視。

所有元件的資產都會放置在如下所述的資料夾結構中。 若要存取資產，請登入CRXDE Lite並瀏覽至`/libs/ws/js/runtime/`。

**模型**&#x200B;包含骨幹模型。

**個檢視**&#x200B;包含主幹檢視。

**範本**&#x200B;僅包含元件的HTML範本。

**路由**&#x200B;包含通用路由。 路由內的範本資料夾包含HTML程式碼和元件的參考。

**服務**&#x200B;包含呼叫REST端點上Adobe Experience Manager伺服器API的服務介面。

**util**&#x200B;包含可由多個元件使用的一般公用程式。
