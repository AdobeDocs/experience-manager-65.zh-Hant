---
title: 設定您的使用者和使用者群組
seo-title: 設定您的使用者和使用者群組
description: 請依照本頁瞭解使用者角色以及如何設定您的使用者和群組，以支援製作和管理行動應用程式。
seo-description: 請依照本頁瞭解使用者角色以及如何設定您的使用者和群組，以支援製作和管理行動應用程式。
uuid: 55cea2b3-d7e6-4174-92b3-ee97e46b59c4
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 167f3bd9-7dbc-4e6b-9868-3ee53935641b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 設定您的使用者和使用者群組 {#configure-your-users-and-user-groups}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉換的專案使用SPA編輯器（例如React）。 [了解更多](/help/sites-developing/spa-overview.md).

本章說明使用者角色以及如何設定您的使用者和群組，以支援製作和管理行動應用程式。

## AEM mobile應用程式使用者和群組管理 {#aem-mobile-application-users-and-group-administration}

若要協助組織和管理AEM應用程式的權限模型，請提供下列兩個群組：

* 應用程式管理員
* 應用程式作者的應用程式作者

### AEM mobile應用程式內容作者（應用程式作者群組） {#aem-mobile-application-content-authors-app-author-group}

應用程式作者群組成員負責製作AEM mobile應用程式內容，包括頁面、文字、影像和視訊。

#### 群組設定——應用程式作者 {#group-configuration-app-authors}

1. 建立名為&#39;app-authors&#39;的新使用者群組：

   導覽至「使用者管理控制台」: [http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   在使用者群組控制台中，選取「+」按鈕以建立群組。

   將此群組的ID設為&#39;app-authors&#39;，表示它是AEM內特定於製作行動應用程式的特定類型的作者使用者群組。

1. 將成員添加到組：作者

   ![chlimage_1-18](assets/chlimage_1-18.png)

   新增應用程式作者至「作者」群組

1. 現在您已建立應用程式作者使用者群組，您可以透過使用者管理控制台，將個別團隊成員新 [增至此群組](http://localhost:4502/libs/granite/security/content/useradmin.md)。

   ![chlimage_1-19](assets/chlimage_1-19.png)

   編輯使用者群組

1. 導覽至「權 [限」主控台](http://localhost:4502/useradmin) ，並新增管理CloudServices的權限

   * （讀取）/etc/cloudservices
   >[!NOTE]
   >
   >「應用程式作者」從AEM延伸預設的內容作者（作者）群組，進而繼承在/content/phonegap下建立內容的功能

### AEM Mobile應用程式管理員群組（應用程式管理員群組） {#aem-mobile-application-administrators-group-app-admins-group}

應用程式管理員群組成員可以使用應用程式作者隨附的相同權限來製作應用程式內容 **AND** ，此外還負責：

* 在AEM中設定PhoneGap Build和Adobe Mobile Services雲端服務
* 測試、發佈和清除應用程式內容同步OTA更新

>[!NOTE]
>
>權限會決定AEM App Command Center中某些使用者動作的可用性。
>
>您會注意到，有些選項不適用於應用程式管理員可用的應用程式作者。

#### 群組設定——應用程式管理員 {#group-configuration-app-admins}

1. 建立新群組，稱為應用程式管理員。
1. 將下列群組新增至新的應用程式管理員群組：

   * 內容作者
   * workflow-users
   ![chlimage_1-20](assets/chlimage_1-20.png)

1. 導覽至「權 [限」主控台](http://localhost:4502/useradmin) ，並新增管理CloudServices的權限

   * （讀取、修改、建立、刪除、複製）/etc/cloudservices/mobileservices
   * （讀取、修改、建立、刪除、複製）/etc/cloudservices/phonegap-build

1. 在相同的「權限」主控台上，新增舞台、發佈和清除應用程式內容更新的權限

   * （讀取、修改、建立、刪除、複製）/etc/packages/mobileapp
   * （讀取）於/var/contentsync
   >[!NOTE]
   >
   >套件複製可用來從作者例項發佈應用程式更新至發佈例項

   >[!CAUTION]
   >
   >/var/contentsync存取被拒絕OOTB。
   >
   >省略READ權限會導致生成和複製空的更新包。

1. 視需要新增成員至此群組

## 控制面板圖格權限 {#dashboard-tile-permissions}

控制面板圖格可能會根據使用者擁有的權限而顯示不同的動作。 以下說明每個圖格可使用哪些動作。

除了這些權限外，還可根據目前應用程式的設定方式顯示／隱藏動作。 例如，如果尚未將PhoneGap雲端設定指派給應用程式，則公開「遠端建置」動作沒有意義。 這些將列在「配置條&#x200B;**件**」部分下。

### 管理應用程式圖格 {#manage-app-tile}

圖格目前沒有需要權限的動作，但是應用程式的詳細資料頁面有下列動作：

* *Edit* for app-author and app-admin(UI Trigger - jcr:write - on /content/phonegap/{suffix})
* *下載* app-author和app-admin（UI觸發器——在/content/phonegap/{suffix}上）

下圖顯示應用程式的「下載」和「編輯」選項：

![chlimage_1-21](assets/chlimage_1-21.png)

