---
title: 設定Acrobat Reader DC擴充功能以擷取資料
seo-title: 設定Acrobat Reader DC擴充功能以擷取資料
description: 瞭解如何設定Acrobat Reader DC擴充功能以擷取資料。
seo-description: 瞭解如何設定Acrobat Reader DC擴充功能以擷取資料。
uuid: af6b3c72-601e-4f54-8343-a323eeee5906
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8f8367fe-a8e9-46ee-a980-1633be02932d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 設定Acrobat Reader DC擴充功能以擷取資料 {#configuring-acrobat-reader-dc-extensions-for-data-capture}

如果您AEM表單安裝的使用者使用Content Services（已過時）的資料擷取功能，建議您為這些使用者建立具有唯讀存取權的角色。

***注意&#x200B;**:Adobe® LiveCycle® Content Services ES（已過時）是與LiveCycle一起安裝的內容管理系統。 它可讓使用者設計、管理、監控和最佳化以人為中心的流程。 內容服務（已過時）支援將於2014年12月31日截止。 請參閱[Adobe產品生命週期檔案](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html)。 如需有關設定Content Services（已過時）的資訊，請參[閱管理Content Services](https://help.adobe.com/en_US/livecycle/9.0/admin_contentservices.pdf)。*

資料擷取需要您指派使用者角色來存取SampleReaderExtensionsCredential。 您可以指派標準的信任管理員角色，但請考慮此角色為一般的非管理使用者提供強大的管理員權限，以控制PKI信任設定並管理PKI認證，這可能會危及您在生產環境中安裝AEM表單的安全性。 建議AEM Forms系統管理員建立僅授與信任商店唯讀存取權的角色，並將此新角色指派給使用資料擷取的非管理員使用者。

## 為資料擷取使用者建立角色 {#create-a-role-for-data-capture-users}

1. 在管理控制台中，按一下「設定>使用者管理>角色管理」，然後按一下「新增角色」。
1. 在相應欄位中輸入角色名稱（例如，Data Capture User）和說明，然後按一下「下一步」。
1. 在「角色權限」螢幕上，按一下「查找權限」，然後從可用權限清單中選擇「憑據讀取」。
1. 按一下「確定」，然後按一下「完成」。

## 指派資料擷取角色 {#assign-the-data-capture-role}

1. 在管理控制台中，按一下「設定>使用者管理>角色管理」，然後按一下「尋找」。
1. 按一下您建立的資料擷取使用者角色。
1. 在「角色使用者／群組」標籤上，按一下「尋找使用者／群組」。
1. 在「尋找使用者和群組」畫面中，按一下「尋找」，選取需要資料擷取使用者角色的使用者，然後按一下「確定」。
1. 在「編輯角色」畫面上，按一下「儲存」。

