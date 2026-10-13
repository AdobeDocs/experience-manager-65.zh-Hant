---
title: 設定系統資訊服務
description: 瞭解如何設定系統資訊服務。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/system_information_service
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 734ed463-2441-49fc-bacb-deb40851af42
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
source-wordcount: '114'
ht-degree: 0%
---
# 設定系統資訊服務 {#set-up-the-system-information-service}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

系統資訊服務提供用於擷取資訊的REST API。 若要使用系統資訊服務，請從管理控制檯啟用REST端點。 執行以下步驟來啟用REST端點：

1. 登入管理主控台。 管理主控台的預設URL為`https://[hostname]:'port'/adminui.`
1. 導覽至「服務>應用程式及服務>服務管理」。
1. 在[服務管理]頁面上，按一下&#x200B;**SystemInfo**&#x200B;服務。
1. 在[端點]索引標籤上的清單中，選取[REST]，然後按一下[**新增**]。
1. 在[新增REST端點]畫面上，按一下[新增&#x200B;**&#x200B;**]。
