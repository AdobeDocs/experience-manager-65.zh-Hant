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
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 單一登入和逾時處理常式 {#single-sign-on-and-timeout-handlers}

AEM Forms工作區已啟用SSO。 如果使用者已登入AEM Forms應用程式（例如Forms Manager或PDF Generator）使用者介面，並在相同的瀏覽器作業階段存取AEM Forms工作區，則使用者會登入AEM Forms工作區，反之亦然。

## 在AEM Forms工作區中處理伺服器逾時 {#handling-server-timeout-in-nbsp-aem-forms-workspace}

可在管理控制台中設定使用者的作業逾時。

若要設定逾時，請登入至 `https://[server]:[port]/adminui`，導覽至「 **設定>使用者管理>設定>設定進階系統屬性**」，然後進行所需的設定。

在AEM Forms工作區中，逾時的處理方式為：

* 用戶的會話持續時間可用於響應初始化用 `initialize` 戶會話的調用。
* 彈出式對話方塊會通知使用者作業即將過期（在作業過期前15秒）。

在此彈出式對話方塊中：

* 按一下「確定」結束用戶會話。
* 按一下「取消」以重新初始化使用者作業。

>[!NOTE]
>
>如果未執行任何動作，使用者會在作業過期前三秒自動登出AEM Forms工作區。

**[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)**
