---
title: 使用者管理
seo-title: User Management
description: 用戶管理允許您使用SAML在表單AEM模組和受Netegrity SiteMinder保護的應用程式之間啟用SSO。 此文檔提供有關用戶管理的詳細資訊。
seo-description: User Management allows you to enable SSO between AEM forms modules and Netegrity SiteMinder-protected applications by using SAML. This document provides more information about User Management.
uuid: f0c8331a-d995-483d-97b7-259df53b1a1a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 10e6177a-8228-4515-aba9-bbe59bede449
exl-id: 1da1f6de-ac0d-4e0d-b8bb-956420e42699
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---

# 使用者管理 {#user-management}

用戶管理允許您使用安全斷言標籤語言(SAML)AEM在表單模組和受Netegrity SiteMinder保護的應用程式之間啟用單一登錄(SSO)。 在實施SSO時，AEM表單用戶登錄頁不是必需的，如果用戶已通過公司門戶進行身份驗證，則不顯示。

有關提高DB2的資料庫和目錄同步效能的資訊，請參見 [IBMDB2資料庫：運行用於定期維護的命令](/help/forms/using/admin-help/ibm-db2-database-running-commands.md#ibm-db2-database-running-commands-for-regular-maintenance)。

## 為啟用SSL的LDAP伺服器配置用戶管理 {#configuring-user-management-for-an-ssl-enabled-ldap-server}

如果您有啟用了SSL的LDAP伺服器，請配置「用戶管理」以使用它。 (請參閱 [為啟用SSL的LDAP伺服器配置用戶管理](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server)。)

## 設定與文檔安全性一起使用的用戶權限 {#setting-user-privileges-for-use-with-document-security}

建立具有建立用戶和組相應權限的管理員用戶。 如果您的AEM表單環境包括「文檔安全性」，請將管理已邀請和本地用戶的權限授予將成為這些用戶管理員的用戶。 還分配管理控制台用戶角色，使用戶能夠訪問管理控制台。 (請參閱 [建立和配置角色](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles)。)

要在策略用戶搜索期間查看選定域中的用戶和組，超級管理員或策略集管理員必須為建立的每個策略集選擇域並將其添加到可見用戶和組清單中（在用戶管理中建立）。

可見用戶和組清單對策略集協調器可見，用於限制最終用戶在選擇要添加到策略的用戶或組時可以瀏覽的域。 如果未執行此任務，則策略集協調器將找不到要添加到策略的任何用戶或組。 任何給定策略集都可以有多個策略集協調器。

>[!NOTE]
>
>必須先建立域，然後才能建立任何策略。

### 設定可見用戶和組 {#set-visible-users-and-groups}

在使用「文檔安全」AEM安裝和配置表單環境後，請在「用戶管理」中設定所有相應的域。

1. 在管理控制台中，按一下「服務」>「文檔安全性」>「策略」，然後按一下「策略集」頁籤。
1. 選擇全局策略集，然後按一下可見用戶和組頁籤。
1. 按一下「添加域」(Add Domain)，然後根據需要添加現有域。
1. 導航到「服務」>「文檔安全性」>「配置」>「我的策略」，然後按一下「可見用戶和組」頁籤。
1. 按一下「添加域」(Add Domain)，然後根據需要添加現有域。

## 管理員用戶限制 {#administrator-user-restrictions}

出於安全原因，具有某些類型管理員權限的用戶無法訪問Workspace最終用戶網頁。 由於這些網頁可以存在於防火牆之外，因此允許管理級別的任務可能會帶來安全風險。 只有具有「工作區管理員」或「工作區用戶」權限的用戶才能訪問最終用戶網頁。

>[!NOTE]
>
>不建議使用Flex工AEM作空間。
