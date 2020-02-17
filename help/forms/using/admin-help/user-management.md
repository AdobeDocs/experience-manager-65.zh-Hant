---
title: 使用者管理
seo-title: 使用者管理
description: 使用者管理可讓您使用SAML，在AEM表單模組和Netegrity SiteMinder保護的應用程式之間啟用SSO。 本檔案提供有關使用者管理的詳細資訊。
seo-description: 使用者管理可讓您使用SAML，在AEM表單模組和Netegrity SiteMinder保護的應用程式之間啟用SSO。 本檔案提供有關使用者管理的詳細資訊。
uuid: f0c8331a-d995-483d-97b7-259df53b1a1a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 10e6177a-8228-4515-aba9-bbe59bede449
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 使用者管理 {#user-management}

使用者管理可讓您使用安全斷言標籤語言(SAML)，在AEM表單模組和Netegrity SiteMinder保護的應用程式之間啟用單一登入(SSO)。 實作SSO時，AEM表單使用者登入頁面不是必要項目，如果使用者已透過公司入口網站進行驗證，則不會顯示。

有關改進DB2的資料庫和目錄同步效能的資訊，請參見 [IBM DB2資料庫：運行命令以定期維護](/help/forms/using/admin-help/ibm-db2-database-running-commands.md#ibm-db2-database-running-commands-for-regular-maintenance)。

## 為啟用SSL的LDAP伺服器配置用戶管理 {#configuring-user-management-for-an-ssl-enabled-ldap-server}

如果您有啟用SSL的LDAP伺服器，請設定「使用者管理」以搭配使用。 (請參 [閱為啟用SSL的LDAP伺服器配置用戶管理](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server)。)

## 設定與Document Security搭配使用的使用者權限 {#setting-user-privileges-for-use-with-document-security}

建立具有建立用戶和組的適當權限的管理員用戶。 如果您的AEM表單環境包含Document Security，請將管理已邀請使用者和本機使用者的權限授予將擔任這些使用者管理員的使用者。 此外，還分配管理控制台用戶角色，以提供用戶對管理控制台的訪問權。 (請參 [閱建立和配置角色](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles)。)

要在策略用戶搜索期間查看選定域中的用戶和組，超級管理員或策略集管理員必須選擇並將域（在「用戶管理」中建立）添加到建立的每個策略集的可見用戶和組清單中。

可見的用戶和組清單對策略集協調器可見，用於限制最終用戶在選擇要添加到策略的用戶或組時可以瀏覽的域。 如果未執行此任務，則策略集協調器將找不到要添加到策略的任何用戶或組。 任何給定的策略集都可以有一個以上的策略集協調器。

>[!NOTE]
>
>必須先建立域，才能建立任何策略。

### 設定可見的使用者和群組 {#set-visible-users-and-groups}

在您安裝並設定AEM表單環境及Document Security後，請在「使用者管理」中設定所有適當的網域。

1. 在管理控制台中，按一下「服務> Document Security>原則」，然後按一下「原則集」標籤。
1. 選擇全局策略集，然後按一下可見用戶和組頁籤。
1. 按一下「新增網域」，並視需要新增現有網域。
1. 導覽至「服務>檔案安全性>設定>我的原則」，然後按一下「可見的使用者和群組」標籤。
1. 按一下「新增網域」，並視需要新增現有網域。

## 管理員使用者限制 {#administrator-user-restrictions}

具有特定管理員權限類型的用戶基於安全原因無法訪問工作區最終用戶網頁。 由於這些網頁可以存在於防火牆之外，因此允許管理層級的任務可能會帶來安全風險。 只有具有「工作區管理員」或「工作區用戶」權限的用戶才能訪問最終用戶網頁。

>[!NOTE]
>
>AEM表單版本不建議使用Flex Workspace。

