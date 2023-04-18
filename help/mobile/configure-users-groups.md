---
title: 設定使用者和使用者群組
description: 請依照本頁面了解使用者角色，以及如何設定您的使用者和群組，以支援行動應用程式的製作和管理。
uuid: 55cea2b3-d7e6-4174-92b3-ee97e46b59c4
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 167f3bd9-7dbc-4e6b-9868-3ee53935641b
exl-id: 9f814204-8cd4-4ba9-9e25-3ff1b25c1955
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 0%

---

# 設定您的使用者和使用者群組 {#configure-your-users-and-user-groups}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

本章說明使用者角色，以及如何設定您的使用者和群組，以支援行動應用程式的製作和管理。

## AEM Mobile應用程式使用者和群組管理 {#aem-mobile-application-users-and-group-administration}

為協助組織及管理AEM應用程式的權限模型，可使用下列兩個群組：

* 應用程式管理員
* 應用程式作者適用的應用程式作者

### AEM Mobile應用程式內容作者（應用程式作者群組） {#aem-mobile-application-content-authors-app-author-group}

應用程式製作群組的成員負責製作AEM行動應用程式內容，包括頁面、文字、影像和影片。

#### 群組設定 — 應用程式作者 {#group-configuration-app-authors}

1. 建立名為「應用程式作者」的新使用者群組：

   導覽至使用者Admin Console: [http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   從使用者群組控制台中，選取「+」按鈕以建立群組。

   將此群組的ID設為「應用程式作者」，表示這是特定類型的製作使用者群組，專用於在AEM內編寫行動應用程式。

1. 向組添加成員：作者

   ![chlimage_1-18](assets/chlimage_1-18.png)

   將應用程式作者新增至作者群組

1. 現在您已建立應用程式作者使用者群組，您可以透過 [使用者管理控制台](http://localhost:4502/libs/granite/security/content/useradmin.md).

   ![chlimage_1-19](assets/chlimage_1-19.png)

   編輯使用者群組

1. 導覽至 [權限主控台](http://localhost:4502/useradmin) 和添加管理cloudservices的權限

   * （讀取）/etc/cloudservices
   >[!NOTE]
   >
   >應用程式作者從AEM延伸預設的內容作者（作者）群組，進而繼承在/content/phonegap下建立內容的功能

### AEM Mobile應用程式管理員群組（應用程式管理員群組） {#aem-mobile-application-administrators-group-app-admins-group}

應用程式管理員群組的成員可以使用應用程式作者隨附的相同權限，編寫應用程式內容 **和** 此外，還負責：

* 在AEM中設定PhoneGap Build和AdobeMobile Services雲端服務
* 測試、發佈和清除應用程式內容同步OTA更新

>[!NOTE]
>
>權限會決定AEM應用程式命令中心中某些使用者動作的可用性。
>
>您會發現，有些選項不適用於應用程式管理員可用的應用程式作者。

#### 群組設定 — 應用程式管理員 {#group-configuration-app-admins}

1. 建立名為app-admins的新群組。
1. 將下列群組新增至新的應用程式管理員群組：

   * 內容作者
   * 工作流 — 使用者

   ![chlimage_1-20](assets/chlimage_1-20.png)

1. 導覽至 [權限主控台](http://localhost:4502/useradmin) 和添加管理cloudservices的權限

   * （讀取、修改、建立、刪除、複製）
   * （讀取、修改、建立、刪除、複製）/etc/cloudservices/phonegap-build

1. 在相同的權限主控台上，新增權限以存放、發佈和清除應用程式內容更新

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

## 控制面板圖磚權限 {#dashboard-tile-permissions}

控制面板圖磚可能會根據使用者擁有的權限而公開不同的動作。 以下說明每個圖磚可使用的動作。

除了這些權限之外，您也可以根據目前應用程式的設定方式來顯示/隱藏動作。 例如，如果尚未將PhoneGap雲端設定指派給應用程式，則顯示「遠端建置」動作沒有意義。 這些將列於下方的「**配置條件**「節。

### 管理應用程式圖磚 {#manage-app-tile}

此圖磚目前沒有需要權限的動作，但應用程式的詳細資訊頁面有下列動作：

* *編輯* 適用於app-author和app-admin（UI觸發器 — jcr:write - on /content/phonegap/{suffix}）
* *下載* app-author和app-admin適用（UI觸發器 — 位於/content/phonegap/{suffix}）

下圖顯示應用程式的下載和編輯選項：

![chlimage_1-21](assets/chlimage_1-21.png)
