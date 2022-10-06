---
title: 配置帳戶鎖定設定
seo-title: Configure account-locking settings
description: 使用「啟用帳戶鎖定」選項，在指定數量的連續身份驗證失敗後鎖定用戶帳戶。
seo-description: Use the Enable Account Locking option to lock user accounts after a specified number of consecutive authentication failures.
uuid: 5ff3fb76-8b11-4818-9a75-40ed8e121da5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d4409c6b-f4ef-499c-8daa-e93a163ff8ab
exl-id: eb8c748d-51d9-4684-97c5-e982ad84ba9f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 5%

---

# 配置帳戶鎖定設定 {#configure-account-locking-settings}

新增網域時，請指定是否要啟用帳戶鎖定。 選擇「啟用帳戶鎖定」選項後，在指定數量的連續身份驗證失敗後鎖定用戶帳戶。 在指定的時間長度後，用戶可以再次嘗試驗證。 此功能可防止用戶嘗試各種憑據組合來訪問系統。

使用「域管理」頁上的設定來指定身份驗證失敗的最大數量和帳戶被鎖定的時間長度。 這些設定適用於已啟用帳戶鎖定的所有網域。

1. 在管理控制台中，按一下 **[!UICONTROL 設定>使用者管理>網域管理]**.
1. 在「最大連續身份驗證失敗數」框中，輸入用戶在其帳戶被鎖定前嘗試登錄失敗的連續次數。 預設值為 20。
1. 在Unlock The Account After(Minutes)框中，輸入用戶帳戶被鎖定的分鐘數。 在指定的分鐘數後，用戶可以嘗試重新登錄。 預設值為 30。
1. 按一下「**[!UICONTROL 儲存]**」。
