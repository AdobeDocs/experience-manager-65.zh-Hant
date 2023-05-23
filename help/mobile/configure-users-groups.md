---
title: 配置用戶和組
description: 按照此頁瞭解用戶角色以及如何配置用戶和組以支援您的移動應用程式的創作和管理。
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

# 配置用戶和用戶組 {#configure-your-users-and-user-groups}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

本章介紹用戶角色以及如何配置用戶和組以支援您的移動應用程式的創作和管理。

## AEM Mobile應用程式用戶和組管理 {#aem-mobile-application-users-and-group-administration}

要幫助組織和管理應用程式的權AEM限模型，可使用以下兩個組：

* 應用管理員的應用管理員
* 應用程式作者

### AEM Mobile應用程式內容作者（應用程式作者組） {#aem-mobile-application-content-authors-app-author-group}

應用程式作者組的成員負責編寫移動應AEM用程式內容，包括頁面、文本、影像和視頻。

#### 組配置 — 應用程式作者 {#group-configuration-app-authors}

1. 建立名為「app-authors」的新用戶組：

   定位至「用戶」Admin Console: [http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   在用戶組控制台中，選擇「+」按鈕以建立組。

   將此組的ID設定為「app-authors」，以表示它是特定類型的作者用戶組，特定於在中創作移動應AEM用。

1. 將成員添加到組：作者

   ![chlimage_1-18](assets/chlimage_1-18.png)

   將應用程式作者添加到作者組

1. 現在，您已建立了應用程式作者用戶組，您可以通過 [用戶管理控制台](http://localhost:4502/libs/granite/security/content/useradmin.md)。

   ![chlimage_1-19](assets/chlimage_1-19.png)

   編輯用戶組

1. 導航到 [權限控制台](http://localhost:4502/useradmin) 添加管理cloudservices的權限

   * /etc/cloudservices上（已讀）
   >[!NOTE]
   >
   >應用作者將預設的內容作者（作者）組從AEM中擴展，從而繼承了在/content/phonegap下建立內容的能力

### AEM Mobile應用程式管理員組（app-admins組） {#aem-mobile-application-administrators-group-app-admins-group}

app-admins組的成員可以使用應用程式作者附帶的相同權限來創作應用程式內容 **和** 此外，還負責：

* 在中配置PhoneGap Build和Adobe移動服務雲服AEM務
* 暫存、發佈和清除應用程式內容同步OTA更新

>[!NOTE]
>
>權限決定應用命令中心中某些用戶AEM操作的可用性。
>
>您會注意到，有些選項對應用程式作者不可用，而應用程式管理員則可用。

#### 組配置 — 應用管理員 {#group-configuration-app-admins}

1. 建立名為app-admins的新組。
1. 將以下組添加到新的app-admins組：

   * 內容作者
   * 工作流用戶

   ![chlimage_1-20](assets/chlimage_1-20.png)

1. 導航到 [權限控制台](http://localhost:4502/useradmin) 添加管理cloudservices的權限

   * （讀取、修改、建立、刪除、複製）/etc/cloudservices/mobilesservices
   * （讀取、修改、建立、刪除、複製）/etc/cloudservices/phonegap-build

1. 在同一「權限」控制台上，將權限添加到舞台、發佈和清除應用程式內容更新

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

## 儀表板磁貼權限 {#dashboard-tile-permissions}

儀表板磁貼可以根據用戶擁有的權限顯示不同的操作。 下面介紹了每個磁貼可用的操作。

除了這些權限外，還可以根據當前應用的配置方式顯示/隱藏操作。 例如，如果尚未將PhoneGap雲配置分配給應用，則顯示「遠程生成」操作沒有意義。 這些將列在下面的「 」**配置條件**&#39;節。

### 管理應用程式磁貼 {#manage-app-tile}

磁貼當前沒有需要權限的操作，但應用程式的詳細資訊頁面具有以下操作：

* *編輯* 對於app-author和app-admin（UI觸發器 — jcr:write - on /content/phonegap/{suffix}）
* *下載* 用於app-author和app-admin（UI觸發器 — 在/content/phonegap/{suffix}上）

下圖顯示了應用的「下載」和「編輯」選項：

![chlimage_1-21](assets/chlimage_1-21.png)
