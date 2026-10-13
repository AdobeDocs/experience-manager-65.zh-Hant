---
title: 單一登入和逾時處理常式
description: 如何設定AEM Forms工作區的工作階段逾時值。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 4f824d80-f3f8-4010-9583-5a9ab1151a7b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
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
source-wordcount: '192'
ht-degree: 0%
---
# 單一登入和逾時處理常式 {#single-sign-on-and-timeout-handlers}

AEM Forms工作區已啟用SSO。 如果使用者已登入AEM Forms應用程式（如Forms Manager或PDF Generator使用者介面）並在相同的瀏覽器工作階段中存取AEM Forms工作區，則使用者會登入AEM Forms工作區反之。

## 在AEM Forms工作區中處理伺服器逾時 {#handling-server-timeout-in-nbsp-aem-forms-workspace}

您可以在管理控制檯中設定使用者的工作階段逾時。

若要設定逾時，請登入`https://'[server]:[port]'/adminui`，瀏覽至&#x200B;**設定>使用者管理>設定>設定進階系統屬性**，並進行所需的設定。

在AEM Forms中，工作區逾時的處理方式為：

* 在回應`initialize`初始化使用者工作階段的呼叫時，可以使用使用者的工作階段持續時間。
* 快顯對話方塊會通知使用者工作階段即將到期（在工作階段到期前15秒）。

在此快顯對話方塊上：

* 按一下「確定」結束使用者作業階段。
* 按一下取消以重新初始化使用者工作階段。

>[!NOTE]
>
>如果未採取任何動作，系統會在工作階段到期前3秒自動將使用者登出AEM Forms工作區。
