---
title: 設定您的使用者和使用者群組
seo-title: Configure Your Users and User Groups
description: 請依照本頁面了解使用者角色，以及如何設定您的使用者和群組，以支援行動On-Demand服務應用程式的製作和管理。
seo-description: Follow this page to understand the user roles and how to configure your users and groups to support the authoring and mangement of your mobile On-Demand services app.
uuid: 461e1725-41dd-4883-92b9-a7e175660401
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: c3c73e67-7f85-4308-b4cd-1b42d4f3f2d9
exl-id: 58b7d1b9-a851-442a-9d02-212cad8abbed
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# 設定您的使用者和使用者群組 {#configure-your-users-and-user-groups}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

本章說明使用者角色，以及如何設定您的使用者和群組，以支援行動應用程式的製作和管理。

## AEM Mobile應用程式使用者和群組管理 {#aem-mobile-application-users-and-group-administration}

### AEM Mobile應用程式內容作者（應用程式作者群組） {#aem-mobile-application-content-authors-app-author-group}

應用程式製作群組的成員負責製作AEM行動應用程式內容，包括頁面、文字、影像和影片。

#### 群組設定 — 應用程式作者 {#group-configuration-app-authors}

1. 建立名為「應用程式作者」的新使用者群組：

   導覽至使用者Admin Console: [http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   從使用者群組控制台中，選取「+」按鈕以建立群組。

   將此群組的ID設為「應用程式作者」，表示這是特定類型的製作使用者群組，專用於在AEM內編寫行動應用程式。

1. 向組添加成員：作者

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. 現在您已建立應用程式作者使用者群組，您可以透過 [使用者管理控制台](http://localhost:4502/libs/granite/security/content/useradmin.md).

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. 下列項目可讓您新增至AEM內容作者群組：

   （閱讀）

   * /app
   * /etc/clientlibs
   * /etc/designs
   * /etc/cloudservices/dps2015

### AEM Mobile應用程式管理員群組（應用程式管理員群組） {#aem-mobile-application-administrators-group-app-admins-group}

應用程式管理員群組的成員可以使用應用程式作者隨附的相同權限，編寫應用程式內容 **和** 此外，還負責：

* 測試、發佈和清除應用程式ContentSync OTA更新

>[!NOTE]
>
>權限會決定AEM應用程式命令中心中某些使用者動作的可用性。
>
>您會發現，有些選項不適用於應用程式管理員可用的應用程式作者。

### 群組設定 — 應用程式管理員 {#group-configuration-app-admins}

1. 建立名為app-admins的新群組。
1. 將下列群組新增至新的應用程式管理員群組：

   * 內容作者
   * 工作流 — 使用者

   ![chlimage_1-169](assets/chlimage_1-169.png)

   >[!NOTE]
   >
   >使用者需要透過PhoneGap Build服務來遠端建置

1. 導覽至 [權限主控台](http://localhost:4502/useradmin) 和添加管理cloudservices的權限

   * （讀取、修改、建立、刪除、複製）

1. 在相同的權限主控台上，新增權限以存放、發佈及清除應用程式內容更新；

   * （讀取、修改、建立、刪除、復寫）/etc/packages/mobileapp
   * （讀取）/var/contentsync

   >[!NOTE]
   >
   >套件復寫可用來從製作執行個體發佈應用程式更新至發佈執行個體

   >[!CAUTION]
   >
   >/var/contentsync訪問被拒絕OOTB。
   >
   >省略READ權限會導致生成和複製空更新包。

1. 視需要將成員新增至此群組
1. 匯出內容或上傳

   * （讀取）在/etc/contentsync上，以訪問導出模板
   * （讀取）在/var上，為讀取時遍歷路徑
   * （讀、寫、修改、刪除）/var/contentsync上，寫入、讀取和清除ContentSync快取的匯出內容

### 其他資源 {#additional-resources}

若要深入了解建立AEM Mobile On-demand Services應用程式的其他兩個角色和責任，請參閱下列資源：

* [為AEM Mobile On-demand Services開發AEM內容](/help/mobile/aem-mobile-on-demand.md)
* [為AEM Mobile On-demand Services應用程式編寫AEM內容](/help/mobile/mobile-apps-ondemand.md)
