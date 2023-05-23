---
title: 配置Acrobat Reader DC擴展以捕獲資料
seo-title: Configuring Acrobat Reader DC extensions for data capture
description: 瞭解如何配置Acrobat Reader DC擴展以進行資料捕獲。
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

# 配置Acrobat Reader DC擴展以捕獲資料 {#configuring-acrobat-reader-dc-extensions-for-data-capture}

如果表單安裝AEM的用戶使用Content Services（已棄用）的資料捕獲功能，建議您為這些用戶建立具有只讀訪問權限的角色。

***附註&#x200B;**:Adobe®LiveCycle®內容服務ES（已棄用）是安裝有LiveCycle的內容管理系統。 它使用戶能夠設計、管理、監控和優化以人為中心的流程。 Content Services（已棄用）支援在12/31/2014結束。 請參閱 [Adobe產品生命週期文檔](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html)。*

資料捕獲要求您分配用戶角色以訪問SampleReaderExtensionsCredential。 您可以分配標準的信任管理員角色，但請考慮此角色為一般非管理用戶提供強大的管理員權限，這些權限可以控制PKI信任設定和管理PKI憑據，這可能會危害您在生產環境中安裝表單AEM的安全性。 建議表單系統AEM管理員建立一個僅授予對信任儲存的只讀訪問權限的角色，並將此新角色分配給使用資料捕獲的非管理員用戶。

## 為資料捕獲用戶建立角色 {#create-a-role-for-data-capture-users}

1. 在管理控制台中，按一下「設定」>「用戶管理」>「角色管理」，然後按一下「新建角色」。
1. 在相應欄位中輸入角色名稱（例如，資料捕獲用戶）和說明，然後按一下下一步。
1. 在「角色權限」螢幕上，按一下「查找權限」，然後從可用權限清單中選擇「憑據讀取」。
1. 按一下「OK（確定）」 ，然後按一下「Finish（完成）」。

## 分配資料捕獲角色 {#assign-the-data-capture-role}

1. 在管理控制台中，按一下「設定」>「用戶管理」>「角色管理」，然後按一下「查找」。
1. 按一下您建立的資料捕獲用戶角色。
1. 在「角色用戶/組」頁籤上，按一下「查找用戶/組」。
1. 在「查找用戶和組」螢幕上，按一下「查找」，選擇需要資料捕獲用戶角色的用戶，然後按一下「確定」。
1. 在「編輯角色」螢幕上，按一下「保存」。
