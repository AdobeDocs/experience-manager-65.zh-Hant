---
title: 配置Task Manager終結點
seo-title: Configuring Task Manager endpoints
description: 瞭解如何配置Task Manager終結點。
seo-description: Learn how to configure Task Manager endpoints.
uuid: 07604b10-0bd7-4bce-9624-7ebac4754f56
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9c55feb9-23d8-4798-a3c5-70ec736df3ad
exl-id: 8495a3d7-6ac9-41f5-b1f9-31decaba118a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# 配置Task Manager終結點 {#configuring-task-manager-endpoints}

Task Manager終結點使Workspace用戶能夠調用服務。

**任務管理器終結點設定**

使用以下設定配置任務管理器終結點。

**名稱：** （必需）標識終結點。 名稱顯示在Workspace的卡視圖中。 不要包含&lt;字元，因為它將截斷Workspace中顯示的名稱。 如果輸入URL作為終結點的名稱，請確保它符合RFC1738中指定的語法規則。

**描述：** 終結點的說明。 不要包含&lt;字元，因為它將截斷Workspace中顯示的說明。

**任務說明：** 啟動此工作流的用戶的說明。

**進程所有者：** 負責流程的人員的姓名。

**用戶可以轉發任務：** 允許用戶轉發初始任務。

**顯示附件窗口：** 允許用戶查看附件窗口。

**允許添加附件：** 允許用戶添加附件和備注。

**任務初始鎖定：** 鎖定初始任務。

**為共用隊列添加ACL:** 初始任務是使用ACL為共用隊列用戶建立的。

**分類：** （必需）用戶在工作區中將看到表單的類別。 從清單中選擇類別，或選擇「新建類別」以添加類別。

**操作名稱：** （必需）可分配給終結點的操作清單。
