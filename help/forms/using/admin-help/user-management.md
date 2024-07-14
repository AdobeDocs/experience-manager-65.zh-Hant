---
title: 使用者管理
description: 「使用者管理」可讓您使用SAML在AEM表單模組與Netegrity SiteMinder保護的應用程式之間啟用SSO。 本檔案提供「使用者管理」的詳細資訊。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1da1f6de-ac0d-4e0d-b8bb-956420e42699
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# 使用者管理 {#user-management}

「使用者管理」可讓您使用安全性宣告標籤語言(SAML)，在AEM表單模組與Netegrity SiteMinder保護的應用程式之間啟用單一登入(SSO)。 實作SSO時，AEM Forms使用者登入頁面不是必要頁面，且若使用者已透過公司入口網站驗證，則不顯示。

如需有關改善DB2的資料庫和目錄同步處理效能的資訊，請參閱[IBM DB2資料庫：執行定期維護的命令](/help/forms/using/admin-help/ibm-db2-database-running-commands.md#ibm-db2-database-running-commands-for-regular-maintenance)。

## 為啟用SSL的LDAP伺服器設定使用者管理 {#configuring-user-management-for-an-ssl-enabled-ldap-server}

如果您有啟用SSL的LDAP伺服器，請設定「使用者管理」以搭配使用。 （請參閱[為啟用SSL的LDAP伺服器設定使用者管理](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server)。）

## 設定與Document Security搭配使用的使用者許可權 {#setting-user-privileges-for-use-with-document-security}

建立具有適當許可權可建立使用者和群組的管理員使用者。 如果您的AEM表單環境包含Document Security，請將管理受邀和本機使用者的許可權授予將成為這些使用者管理員的使用者。 同時指派管理主控台使用者角色，讓使用者可以存取管理主控台。 （請參閱[建立和設定角色](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles)。）

若要在原則使用者搜尋期間檢視所選網域中的使用者和群組，超級管理員或原則集管理員必須選取網域（在「使用者管理」中建立），並將網域新增至每個建立之原則集的可見使用者與群組清單。

可見的使用者和群組清單對原則集協調者可見，並用來限制一般使用者選擇要加入原則的使用者或群組時，可以瀏覽的網域。 如果未執行此工作，原則集協調員將無法找到任何使用者或群組來加入原則。 任何指定的原則集都可以有一個以上的原則集協調器。

>[!NOTE]
>
>必須先建立網域，然後才能建立任何原則。

### 設定可見的使用者和群組 {#set-visible-users-and-groups}

使用Document Security安裝和設定AEM表單環境後，請在「使用者管理」中設定所有適當的網域。

1. 在管理控制檯中，按一下「服務」>「Document Security」>「原則」，然後按一下「原則集」標籤。
1. 選取[Global Policy Set]，然後按一下[Visible Users And Groups]索引標籤。
1. 按一下「新增網域」 ，並視需要新增現有網域。
1. 導覽至「服務> Document Security >設定>我的原則」 ，然後按一下「可見的使用者和群組」標籤。
1. 按一下「新增網域」 ，並視需要新增現有網域。

## 管理員使用者限制 {#administrator-user-restrictions}

基於安全理由，具有特定管理員許可權型別的使用者無法存取Workspace一般使用者網頁。 因為這些網頁可能存在於防火牆之外，允許管理層級的工作可能會帶來安全性風險。 只有擁有Workspace管理員或Workspace使用者許可權的使用者才能存取一般使用者網頁。

>[!NOTE]
>
>AEM Forms版本已棄用Flex工作區。
