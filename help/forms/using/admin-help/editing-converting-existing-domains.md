---
title: 編輯和轉換現有域
seo-title: Editing and converting existing domains
description: 瞭解如何從「域管理」頁更改現有域的設定。 將現有企業域轉換為混合域，反之亦然。
seo-description: Learn how to change the settings for existing domains from the Domain Management page. Convert an existing enterprise domain to a hybrid domain or vice versa.
uuid: 4cc9547e-b4ec-4588-b1cf-18720f06149a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 44dec184-3ef7-4ba6-a87f-ad171d3cb188
exl-id: 34ac5f8b-f209-4f99-ad71-4df6f2c88c1e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---

# 編輯和轉換現有域{#editing-and-converting-existing-domains}

可以從「域管理」頁更改現有域的設定。 您還可以將現有企業域轉換為混合域。

## 編輯現有域 {#edit-an-existing-domain}

1. 在管理控制台中，按一下「設定」>「用戶管理」>「域管理」。
1. 按一下要編輯的域名。
1. 要更改域名，請更改「名稱」框中的文本。
1. 要更改企業域或混合域的驗證資訊，請按一下頁面底部的相應驗證名稱。 在「編輯驗證」頁上，根據需要更改設定。 (請參閱 [驗證設定](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings)。)
1. 要更改企業域的目錄資訊，請按一下頁面底部的相應目錄名。 在「編輯目錄」頁上，根據需要更改設定。 (請參閱 [添加目錄或自定義SPI](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis)。)
1. 完成更改後，按一下「確定」。

## 將企業域轉換為混合域 {#convert-an-enterprise-domain-to-a-hybrid-domain}

1. 在管理控制台中，按一下「設定」>「用戶管理」>「域管理」。
1. 按一下要轉換的企業域的名稱。
1. 按一下「轉換為混合域」。
1. 查看顯示的有關用戶和組資料和用戶身份驗證的資訊，然後按一下確定。
1. 編輯混合域的設定，然後按一下「確定」。

>[!NOTE]
>
>如果要轉換的企業域不包含目錄設定，則任何LDAP身份驗證設定都將丟失。

## 將混合域轉換為企業域 {#convert-a-hybrid-domain-to-an-enterprise-domain}

1. 在管理控制台中，按一下「設定」>「用戶管理」>「域管理」。
1. 按一下要轉換的混合域的名稱。
1. 按一下「轉換為企業域」。
1. 查看顯示的有關用戶和組資料和用戶身份驗證的資訊，然後按一下確定。
1. 按一下「添加目錄」並配置所需的目錄資訊。 (請參閱 [添加目錄或自定義SPI](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis)。)
