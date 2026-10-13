---
title: AEM Forms Workspace架構
description: LiveCycle AEM Forms Workspace架構的概念資訊與概觀。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: c6f216d4-781c-4356-b9f0-3324903a28e7
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: User, Developer
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
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%
---
# AEM Forms Workspace架構 {#aem-forms-workspace-architecture}

AEM Forms工作區是託管於CRX™的網路應用程式。 在瀏覽器中開啟工作區時，會存取CRX資源，並將應用程式呈現為瀏覽器中的HTML頁面。

應用程式存取REST端點上的AEM Forms伺服器以執行下列動作：

* 擷取使用者工作、程式起點、程式歷史記錄和使用者資訊
* 對任務執行動作
* 查詢資料庫中的工作
* 更新使用者偏好設定等

AEM Forms伺服器會透過JDBC存取AEM Forms資料庫。 資料庫會儲存任務、處理作業及其執行個體、使用者和相關資訊。

AEM Forms工作區設計成模組化JavaScript™元件，可個別自訂並重複用於其他網頁應用程式。 這些元件以BackBone為基礎，這是JavaScript資料庫，提供網頁應用程式的結構。 描述元件與BackBone互動的詳細文章為[此處](/help/forms/using/backbone-interaction.md)。 [此](/help/forms/using/folder-structure.md)文章將討論CRX資料夾結構中的元件組織。

為AEM Forms工作區提供的套件：

* `adobe-lc-workspace-pkg-<version>.zip`：它是CRX套件，也就是說，可以使用套件管理員在CRX中部署。
* `adobe-lc-workspace-<version>-src.zip`：此封存包含AEM Forms工作區的完整程式碼以及建立部署套件的指令碼 — 出貨、偵錯和開發套裝。
