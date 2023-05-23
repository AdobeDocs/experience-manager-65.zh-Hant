---
title: 導入和導出配置檔案
seo-title: Importing and exporting the configuration file
description: 瞭解如何導入和導出配置檔案以編輯伺服器首選項或配置其AEM他表單產品實例。
seo-description: Learn how to import and export the configuration file in order to edit server preferences or configure another AEM forms product instance.
uuid: 32e8a709-2d7c-4740-9533-d53aa751bc58
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c1636537-f7dc-48d8-a3f0-9052bcd28b62
exl-id: 225dbeb5-a21c-4338-98c7-e10c32973721
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# 導入和導出配置檔案 {#importing-and-exporting-the-configuration-file}

使用「手動配置」頁可以下載XML格式的配置設定副本。 此檔案中的設定控制所有伺服器首選項。 然後，您可以編輯該檔案並將其上載回伺服器。 您還可以使用該檔案配置其AEM他表單產品實例。

為避免安全風險，導出的配置檔案中不包含目錄伺服器的綁定密碼值。 在將檔案導入新系統之前，請更新XML檔案中的密碼。

>[!NOTE]
>
>導入配置檔案AEM會根據檔案中的資訊重新配置表單。 只有系統管理員或熟悉表單產品和XML的專業服AEM務顧問才應考慮修改配置檔案。 他們可能需要編輯配置檔案，例如，以重新配置損壞的設定。

**導出配置資訊**

1. 在管理控制台中，按一下「設定」>「用戶管理」>「配置」>「導入和導出配置檔案」。
1. 按一下「導出」。 如果使用的是MicrosoftInternet Explorer，系統將提示您指定保存檔案的位置。 如果您使用Firefox，則該檔案將保存在您的案頭上。

**導入配置資訊**

1. 在管理控制台中，按一下「設定」>「用戶管理」>「配置」>「導入和導出配置檔案」。
1. 按一下「瀏覽」查找配置檔案，按一下「導入」，然後按一下「確定」。
