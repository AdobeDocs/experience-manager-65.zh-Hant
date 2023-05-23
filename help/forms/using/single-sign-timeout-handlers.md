---
title: 單一登錄和超時處理程式
seo-title: Single Sign On and timeout handlers
description: How-to為AEM Forms工作區設定會話超時值。
seo-description: How-to set the session timeout value for AEM Forms workspace.
uuid: 17583fd5-6453-41d3-bb63-a639983fbea9
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 698990a2-dd3f-480f-9d15-d87563860297
exl-id: 4f824d80-f3f8-4010-9583-5a9ab1151a7b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# 單一登錄和超時處理程式 {#single-sign-on-and-timeout-handlers}

AEM Forms工作區已啟用SSO。 如果用戶已登錄到AEM Forms應用程式(如Forms管理器或PDF生成器用戶介面)，並在同一瀏覽器會話中訪問AEM Forms工作區，則用戶將登錄到AEM Forms工作區，反之亦然。

## 在AEM Forms工作區中處理伺服器超時 {#handling-server-timeout-in-nbsp-aem-forms-workspace}

可以在管理控制台中配置用戶的會話超時。

要設定超時，請登錄到 `https://'[server]:[port]'/adminui`，導航 **設定>用戶管理>配置>配置高級系統屬性**，並進行所需設定。

在AEM Forms工作區中，超時處理為：

* 用戶的會話持續時間可用於響應 `initialize` 初始化用戶會話的調用。
* 彈出對話框將通知用戶會話即將過期，在會話到期前15秒。

在此彈出對話框中：

* 按一下「確定」結束用戶會話。
* 按一下取消重新初始化用戶會話。

>[!NOTE]
>
>如果未採取任何操作，則在會話到期前三秒鐘，用戶將自動從AEM Forms工作區註銷。
