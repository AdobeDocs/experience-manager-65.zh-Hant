---
title: 單一登入和逾時處理常式
seo-title: 單一登入和逾時處理常式
description: 如何設定AEM Forms工作區的工作階段逾時值。
seo-description: 如何設定AEM Forms工作區的工作階段逾時值。
uuid: 17583fd5-6453-41d3-bb63-a639983fbea9
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 698990a2-dd3f-480f-9d15-d87563860297
exl-id: 4f824d80-f3f8-4010-9583-5a9ab1151a7b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---

# 單一登入和逾時處理常式{#single-sign-on-and-timeout-handlers}

AEM Forms工作區已啟用SSO。 如果使用者已登入Forms Manager或PDF產生器等AEM Forms應用程式，並在相同的瀏覽器工作階段中存取AEM Forms工作區，則使用者會登入AEM Forms工作區，反之亦然。

## 處理AEM Forms工作區{#handling-server-timeout-in-nbsp-aem-forms-workspace}中的伺服器逾時

可在管理控制台中設定使用者的工作階段逾時。

若要設定逾時，請登入`https://'[server]:[port]'/adminui`，導覽至&#x200B;**設定>使用者管理>設定>設定進階系統屬性**，並進行所需的設定。

在AEM Forms工作區中，逾時的處理方式為：

* 用戶的會話持續時間可用於響應初始化用戶會話的`initialize`調用。
* 彈出式對話方塊會通知使用者工作階段即將到期，也就是工作階段到期的15秒。

在此快顯對話方塊中：

* 按一下「確定」結束用戶會話。
* 按一下取消以重新初始化用戶會話。

>[!NOTE]
>
>若未採取任何動作，系統會在工作階段過期前三秒自動將使用者登出AEM Forms工作區。
