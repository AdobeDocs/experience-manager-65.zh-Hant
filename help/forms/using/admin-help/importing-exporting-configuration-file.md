---
title: 導入和導出配置檔案
seo-title: 導入和導出配置檔案
description: 瞭解如何匯入和匯出設定檔，以編輯伺服器偏好設定或設定其他AEM表單產品例項。
seo-description: 瞭解如何匯入和匯出設定檔，以編輯伺服器偏好設定或設定其他AEM表單產品例項。
uuid: 32e8a709-2d7c-4740-9533-d53aa751bc58
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c1636537-f7dc-48d8-a3f0-9052bcd28b62
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 導入和導出配置檔案 {#importing-and-exporting-the-configuration-file}

使用「手動配置」頁可以下載XML格式的配置設定副本。 此檔案中的設定控制所有伺服器首選項。 然後，您可以編輯檔案並將其上傳回伺服器。 您也可以使用檔案來設定其他AEM表單產品例項。

為避免安全風險，導出的配置檔案中不包括目錄伺服器的綁定密碼值。 在將檔案導入新系統之前，請更新XML檔案中的密碼。

>[!NOTE]
>
>匯入設定檔案會根據檔案中的資訊重新設定AEM表單。 只有熟悉AEM表單產品和XML的系統管理員或專業服務顧問才應考慮修改設定檔。 例如，他們可能需要編輯配置檔案以重新配置損壞的設定。

**匯出設定資訊**

1. 在「管理控制台」中，按一下「設定>使用者管理>設定>匯入和匯出設定檔案」。
1. 按一下「匯出」。 如果您使用Microsoft Internet Explorer，系統會提示您指定儲存檔案的位置。 如果您使用Firefox，檔案會儲存在您的案頭上。

**匯入設定資訊**

1. 在「管理控制台」中，按一下「設定>使用者管理>設定>匯入和匯出設定檔案」。
1. 按一下瀏覽查找配置檔案，按一下導入，然後按一下確定。

