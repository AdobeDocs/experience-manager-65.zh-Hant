---
title: 在Adobe Experience Manager中建立和共用私人資料夾。
description: 瞭解如何在Adobe Experience Manager Assets中建立私人資料夾，並與其他使用者共用資料夾，以及為他們指派各種權限。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 91caca39b0b6c5c0c98b58be02f518901a3d90e3
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 0%

---


# 私人資料夾共用 {#private-folder-sharing}

您可以在Adobe Experience Manager Assets使用者介面中建立專屬於您的私人資料夾。 您可以將此私人資料夾共用給其他使用者，並為其指派各種權限。 根據您指派的權限層級，使用者可以對資料夾執行各種工作，例如檢視資料夾內的資產或編輯資產。

>[!NOTE]
>
>私人資料夾至少有一個擁有擁有者角色的成員。

1. 在「資產」主控台中，按一 **[!UICONTROL 下工具列中的]** 「建立」，然後從功能表 **[!UICONTROL 選擇「資料夾]** 」。

   ![建立資產檔案夾](assets/Create-folder.png)

1. 在「創 **[!UICONTROL 建資料夾]** 」對話框中，輸入資料夾的標題和名稱（可選），然後選擇「 **[!UICONTROL 私用」]**。

   ![選中「專用」複選框可將資料夾設定為專用](assets/private-folder.png)

1. 按一下&#x200B;**[!UICONTROL 建立]**。UI中會建立私人資料夾。

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. To share the folder with other users and the assign privileges to them, select the folder, and click **[!UICONTROL Properties]** from the toolbar.

   ![資訊選項](assets/do-not-localize/info-circle-icon.png)

   >[!NOTE]
   >
   >在您共用資料夾之前，該資料夾不會顯示給任何其他使用者。

1. In the **[!UICONTROL Folder Properties]** page, select a user from the **[!UICONTROL Add User]** list, assign a role to the user on your private folder, and click **[!UICONTROL Add]**.

   ![chlimage_1-415](assets/chlimage_1-415.png)

   >[!NOTE]
   >
   >您可以將各種角色（例如編輯者、擁有者或檢視器）指派給您共用資料夾的使用者。 如果您為用戶分配了「所有者」角色，則用戶對資料夾具有編輯者權限。 此外，使用者也可以與其他人共用資料夾。 如果您指派了編輯者角色，使用者可以編輯私人資料夾中的資產。 如果您指派檢視器角色，使用者只能檢視您私人資料夾中的資產。

   >[!NOTE]
   >
   >私人資料夾至少有一個擁有擁有者角色的成員。 因此，管理員無法從專用資料夾中刪除所有所有者成員。 但是，要從專用資料夾中刪除現有所有者（和管理員本身），管理員必須將其他用戶添加為所有者。

1. 按一下&#x200B;**[!UICONTROL 「儲存」]**。根據您指派的角色，當使用者登入「資產」時，會為使用者指派一組權限給您的私人資料夾。
1. 按一下 **[!UICONTROL 確定]** ，關閉確認消息。
1. 與您共用資料夾的使用者會收到共用通知。 使用使用者的認證登入資產以檢視通知。

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. 按一下「通知」以開啟通知清單。

   ![通知清單](assets/Assets-Notification.png)

1. 按一下管理員共用的專用資料夾條目以開啟該資料夾。

>[!NOTE]
>
>要能夠建立專用資料夾，您需要對要建立專用資料夾的父資料夾具有讀取和編輯ACL權限。 如果您不是管理員，則這些權限依預設不會為您啟用 `/content/dam`。 在此情況下，請先取得使用者ID/群組的這些權限，再嘗試建立私人資料夾或檢視資料夾設定。
