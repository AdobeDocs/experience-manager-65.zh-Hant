---
title: 設定帳戶鎖定設定
seo-title: 設定帳戶鎖定設定
description: 使用「啟用帳戶鎖定」選項，在指定數量的連續驗證失敗後鎖定使用者帳戶。
seo-description: 使用「啟用帳戶鎖定」選項，在指定數量的連續驗證失敗後鎖定使用者帳戶。
uuid: 5ff3fb76-8b11-4818-9a75-40ed8e121da5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d4409c6b-f4ef-499c-8daa-e93a163ff8ab
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 設定帳戶鎖定設定 {#configure-account-locking-settings}

新增網域時，請指定是否啟用帳戶鎖定。 選取「啟用帳戶鎖定」選項時，在指定數量的連續驗證失敗後，使用者帳戶會被鎖定。 在指定的時間長度後，使用者可嘗試再次驗證。 此功能可防止使用者嘗試各種憑證組合來存取系統。

使用「域管理」頁上的設定來指定驗證失敗的最大數目和帳戶鎖定的時間長度。 這些設定會套用至所有已啟用帳戶鎖定的網域。

1. 在管理控制台中，按一 **[!UICONTROL 下「設定>使用者管理>網域管理]**」。
1. 在「最大連續驗證失敗數」方塊中，輸入使用者在帳戶鎖定之前，嘗試登入失敗的連續次數。 預設值為20。
1. 在「解除鎖定帳戶後（分鐘）」方塊中，輸入使用者帳戶被鎖定的分鐘數。 在指定的分鐘數後，使用者可嘗試再次登入。 預設值為30。
1. 按一下&#x200B;**[!UICONTROL 「儲存」]**。

