---
title: 設定帳戶鎖定設定
description: 使用[啟用帳戶鎖定]選項，可在指定的連續驗證失敗次數之後鎖定使用者帳戶。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: eb8c748d-51d9-4684-97c5-e982ad84ba9f
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
source-wordcount: '210'
ht-degree: 5%
---
# 設定帳戶鎖定設定 {#configure-account-locking-settings}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

當您新增網域時，請指定是否啟用帳戶鎖定。 當選取啟用帳戶鎖定選項時，使用者帳戶會在指定次數的連續驗證失敗後鎖定。 在指定的時間長度後，使用者可以嘗試再次驗證。 此功能可防止使用者嘗試各種認證組合來存取系統。

使用「網域管理」頁面中的設定來指定驗證失敗的最大數目以及鎖定帳號的時間長度。 這些設定適用於所有已啟用帳戶鎖定的網域。

1. 在管理控制檯中，按一下&#x200B;**[!UICONTROL 設定>使用者管理>網域管理]**。
1. 在最大連續驗證失敗數方塊中，輸入在鎖定帳戶之前，使用者連續嘗試登入失敗的次數。 預設值為 20。
1. 在「解除鎖定帳戶之後（分鐘）」方塊中，輸入使用者帳戶被鎖定的分鐘數。 在指定的分鐘數後，使用者可以嘗試再次登入。 預設值為 30。
1. 按一下&#x200B;**[!UICONTROL 儲存]**。
