---
title: 設定帳戶鎖定設定
description: 使用[啟用帳戶鎖定]選項，可在指定的連續驗證失敗次數之後鎖定使用者帳戶。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: eb8c748d-51d9-4684-97c5-e982ad84ba9f
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 6%

---

# 設定帳戶鎖定設定 {#configure-account-locking-settings}

當您新增網域時，請指定是否啟用帳戶鎖定。 當選取啟用帳戶鎖定選項時，使用者帳戶會在指定次數的連續驗證失敗後鎖定。 在指定的時間長度後，使用者可以嘗試再次驗證。 此功能可防止使用者嘗試各種認證組合來存取系統。

使用「網域管理」頁面中的設定來指定驗證失敗的最大數目以及鎖定帳號的時間長度。 這些設定適用於所有已啟用帳戶鎖定的網域。

1. 在管理控制檯中，按一下 **[!UICONTROL 設定>使用者管理>網域管理]**.
1. 在最大連續驗證失敗數方塊中，輸入在鎖定帳戶之前，使用者連續嘗試登入失敗的次數。 預設值為 20。
1. 在「解除鎖定帳戶之後（分鐘）」方塊中，輸入使用者帳戶被鎖定的分鐘數。 在指定的分鐘數後，使用者可以嘗試再次登入。 預設值為 30。
1. 按一下「**[!UICONTROL 儲存]**」。
