---
title: 設定Acrobat Reader DC擴充功能以擷取資料
seo-title: Configuring Acrobat Reader DC extensions for data capture
description: 了解如何設定Acrobat Reader DC擴充功能以擷取資料。
seo-description: Learn how to configure Acrobat Reader DC extensions for data capture.
uuid: af6b3c72-601e-4f54-8343-a323eeee5906
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8f8367fe-a8e9-46ee-a980-1633be02932d
exl-id: 0f8e1e46-4fc5-43f6-abb1-19a3f20e1f1d
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---

# 設定Acrobat Reader DC擴充功能以擷取資料 {#configuring-acrobat-reader-dc-extensions-for-data-capture}

如果AEM表單安裝的使用者使用內容服務的資料擷取功能（已淘汰），建議您為這些使用者建立具有唯讀存取權的角色。

***附註&#x200B;**:Adobe®LiveCycle® Content Services ES（已過時）是隨LiveCycle安裝的內容管理系統。 它使用戶能夠設計、管理、監控和優化以人為中心的流程。 內容服務（已過時）支援將於12/31/2014終止。 請參閱 [Adobe產品生命週期檔案](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html).*

資料捕獲要求您分配用戶角色以訪問SampleReaderExtensionsCredential。 您可以分配標準的信任管理員角色，但請考慮，此角色為一般的非管理用戶提供了強大的管理員權限，這些權限可以控制PKI信任設定和管理PKI憑據，這可能會危及在生產環境中安裝AEM表單的安全。 建議AEM Forms系統管理員建立僅授予信任儲存區唯讀存取權的角色，並將此新角色指派給使用資料擷取的非管理員使用者。

## 為資料捕獲用戶建立角色 {#create-a-role-for-data-capture-users}

1. 在管理控制台中，按一下「設定>使用者管理>角色管理」，然後按一下「新增角色」。
1. 在相應欄位中輸入角色名稱（例如，資料捕獲用戶）和說明，然後按一下下一步。
1. 在「角色權限」螢幕上，按一下「查找權限」，然後從可用權限清單中選擇「憑據讀取」。
1. 按一下「確定」，然後按一下「完成」。

## 分配資料捕獲角色 {#assign-the-data-capture-role}

1. 在管理控制台中，按一下「設定>使用者管理>角色管理」，然後按一下「尋找」。
1. 按一下您建立的資料擷取使用者角色。
1. 在「角色使用者/群組」標籤上，按一下「尋找使用者/群組」 。
1. 在「查找用戶和組」螢幕上，按一下「查找」，選擇需要資料捕獲用戶角色的用戶，然後按一下「確定」。
1. 在「編輯角色」螢幕上，按一下「保存」。
