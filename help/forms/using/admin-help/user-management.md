---
title: 使用者管理
seo-title: User Management
description: 使用者管理可讓您使用SAML，在AEM表單模組和受Netegrity SiteMinder保護的應用程式之間啟用SSO。 本檔案提供有關「使用者管理」的詳細資訊。
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

使用者管理，您可以使用安全斷言標籤語言(SAML)，在AEM表單模組和受Netegrity SiteMinder保護的應用程式之間啟用單一登入(SSO)。 實作SSO時，若使用者已透過公司入口網站驗證，則不需要AEM表單使用者登入頁面，也不會顯示。

有關提高DB2的資料庫和目錄同步效能的資訊，請參見 [IBM DB2資料庫：運行命令以進行定期維護](/help/forms/using/admin-help/ibm-db2-database-running-commands.md#ibm-db2-database-running-commands-for-regular-maintenance).

## 為啟用SSL的LDAP伺服器配置用戶管理 {#configuring-user-management-for-an-ssl-enabled-ldap-server}

如果您有啟用SSL的LDAP伺服器，請配置「用戶管理」以使用它。 (請參閱 [為啟用SSL的LDAP伺服器配置用戶管理](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server).)

## 設定與Document Security一起使用的用戶權限 {#setting-user-privileges-for-use-with-document-security}

建立具有建立用戶和組的適當權限的管理員用戶。 如果您的AEM表單環境包含檔案安全性，請將管理受邀和本機使用者的權限授予將擔任這些使用者管理員的使用者。 也分配管理控制台用戶角色，為用戶提供管理控制台的訪問權限。 (請參閱 [建立和配置角色](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)

要在策略用戶搜索期間查看選定域中的用戶和組，超級管理員或策略集管理員必須選擇域，並為每個已建立的策略集將域（在用戶管理中建立）添加到可見的用戶和組清單中。

可見的用戶和組清單對策略集協調器可見，用於限制最終用戶在選擇要添加到策略的用戶或組時可以瀏覽的域。 如果未執行此任務，則策略集協調器將找不到要添加到策略的任何用戶或組。 任何給定的策略集都可以有多個策略集協調器。

>[!NOTE]
>
>必須先建立域，然後才能建立任何策略。

### 設定可見的使用者和群組 {#set-visible-users-and-groups}

使用檔案安全性安裝及設定AEM表單環境後，請在「使用者管理」中設定所有適當的網域。

1. 在管理控制台中，按一下「服務」>「文檔安全」>「策略」，然後按一下「策略集」頁簽。
1. 選擇「全局策略集」，然後按一下「可見用戶和組」頁簽。
1. 按一下「新增網域」 ，然後視需要新增現有網域。
1. 導覽至「服務>檔案安全性>設定>我的原則」 ，然後按一下「可見的使用者和群組」標籤。
1. 按一下「新增網域」 ，然後視需要新增現有網域。

## 管理員用戶限制 {#administrator-user-restrictions}

具有特定管理員權限類型的使用者基於安全原因無法存取Workspace一般使用者網頁。 因為這些網頁可能存在於防火牆之外，因此允許管理層級的任務可能會帶來安全風險。 只有具有工作區管理員或工作區用戶權限的用戶才能訪問最終用戶網頁。

>[!NOTE]
>
>AEM Forms版本已不再使用Flex Workspace。
