---
title: 設定任務管理員端點
description: 瞭解如何設定Task Manager端點以叫用服務。 設定Task Manager端點需要不同的設定。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 8495a3d7-6ac9-41f5-b1f9-31decaba118a
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# 設定任務管理員端點 {#configuring-task-manager-endpoints}

Task Manager端點可讓Workspace使用者呼叫服務。

**任務管理員端點設定**

使用下列設定來設定工作管理員端點。

**名稱：** （必要）識別端點。 名稱會顯示在工作區中的卡片檢視中。 請勿包含&lt;字元，因為這會截斷工作區中顯示的名稱。 如果您輸入URL作為端點的名稱，請確保其符合RFC1738中指定的語法規則。

**說明：** 端點的說明。 請勿包含&lt;字元，因為這會截斷Workspace中顯示的說明。

**工作指示：** 啟動此工作流程的使用者指示。

**程式擁有者：** 負責處理序的人員名稱。

**使用者可以轉送工作：** 允許使用者轉送初始任務。

**顯示附件視窗：** 允許使用者檢視附件視窗。

**允許新增附件：** 允許使用者新增附件和附註。

**最初鎖定的工作：** 鎖定初始任務。

**新增共用佇列的ACL：** 初始任務是以共用佇列使用者的ACL來建立。

**分類：** （必要）使用者會在工作區中看到表單的類別。 從清單中選取類別，或選取「新增類別」以新增類別。

**作業名稱：** （必要）可指派給端點的作業清單。
