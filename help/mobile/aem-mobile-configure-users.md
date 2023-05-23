---
title: 配置用戶和用戶組
description: 按照此頁瞭解用戶角色以及如何配置用戶和組以支援移動按需服務應用的創作和管理。
uuid: 461e1725-41dd-4883-92b9-a7e175660401
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: c3c73e67-7f85-4308-b4cd-1b42d4f3f2d9
exl-id: 58b7d1b9-a851-442a-9d02-212cad8abbed
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 1%

---

# 配置用戶和用戶組 {#configure-your-users-and-user-groups}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

本章介紹用戶角色以及如何配置用戶和組以支援您的移動應用程式的創作和管理。

## AEM Mobile應用程式用戶和組管理 {#aem-mobile-application-users-and-group-administration}

### AEM Mobile應用程式內容作者（應用程式作者組） {#aem-mobile-application-content-authors-app-author-group}

應用程式作者組的成員負責編寫移動應AEM用程式內容，包括頁面、文本、影像和視頻。

#### 組配置 — 應用程式作者 {#group-configuration-app-authors}

1. 建立名為「app-authors」的新用戶組：

   定位至「用戶」Admin Console: [http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   在用戶組控制台中，選擇「+」按鈕以建立組。

   將此組的ID設定為「app-authors」，以表示它是特定類型的作者用戶組，特定於在中創作移動應AEM用。

1. 將成員添加到組：作者

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. 現在，您已建立了應用程式作者用戶組，您可以通過 [用戶管理控制台](http://localhost:4502/libs/granite/security/content/useradmin.md)。

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. 下面允許您添加到內容作AEM者組：

   （閱讀）

   * /app
   * /etc/clientlibs
   * /etc/designs
   * /etc/cloudservices/dps2015

### AEM Mobile應用程式管理員組（app-admins組） {#aem-mobile-application-administrators-group-app-admins-group}

app-admins組的成員可以使用應用程式作者附帶的相同權限來創作應用程式內容 **和** 此外，還負責：

* 暫存、發佈和清除應用程式ContentSync OTA更新

>[!NOTE]
>
>權限決定應用命令中心中某些用戶AEM操作的可用性。
>
>您會注意到，有些選項對應用程式作者不可用，而應用程式管理員則可用。

### 組配置 — 應用管理員 {#group-configuration-app-admins}

1. 建立名為app-admins的新組。
1. 將以下組添加到新的app-admins組：

   * 內容作者
   * 工作流用戶

   ![chlimage_1-169](assets/chlimage_1-169.png)

   >[!NOTE]
   >
   >工作流用戶需要使用PhoneGap Build服務遠程生成

1. 導航到 [權限控制台](http://localhost:4502/useradmin) 添加管理cloudservices的權限

   * （讀取、修改、建立、刪除、複製）/etc/cloudservices/mobilesservices

1. 在同一「權限」控制台上，向存放、發佈和清除應用程式內容更新添加權限；

   * （讀取、修改、建立、刪除、複製）/etc/packages/mobileapp
   * /var/contentsync上（讀取）

   >[!NOTE]
   >
   >包複製用於將應用更新從作者實例發佈到發佈實例

   >[!CAUTION]
   >
   >/var/contentsync訪問被拒絕OOTB。
   >
   >忽略READ權限可能會導致生成和複製空的更新包。

1. 根據需要將成員添加到此組
1. 導出內容或上載

   * 在/etc/contentsync上（讀取）訪問導出模板
   * 在/var上（讀取）到，用於讀取的路徑遍歷
   * （讀、寫、修改、刪除）/var/contentsync上的內容，以寫、讀和清除ContentSync快取的導出內容

### 其他資源 {#additional-resources}

要詳細瞭解建立AEM Mobile On-demand Services應用程式的其他兩個角色和職責，請參閱以下資源：

* [開發AEMAEM Mobile On-demand Services內容](/help/mobile/aem-mobile-on-demand.md)
* [AEM Mobile On-demand ServicesAEM應用的創作內容](/help/mobile/mobile-apps-ondemand.md)
