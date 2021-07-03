---
title: 共用資產的私人資料夾
description: 了解如何在 [!DNL Adobe Experience Manager Assets] 中建立私人資料夾，並與其他使用者共用資料夾，並為其指派各種權限。
contentOwner: AG
role: User
feature: 協作
exl-id: c1aece06-7c1c-43a0-bea0-6f11ecda7e68
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager Assets]中的專用資料夾 {#private-folder}

您可以在[!DNL Adobe Experience Manager Assets]使用者介面中建立專供您使用的私人資料夾。 您可以將此私人資料夾共用給其他使用者，並為其指派各種權限。 根據您指派的權限層級，使用者可以對資料夾執行各種工作，例如在資料夾內檢視資產或編輯資產。

>[!NOTE]
>
>私人資料夾至少有一個具有「所有者」角色的成員。

## 建立和共用私人資料夾 {#create-share-private-folder}

要建立和共用私人資料夾：

1. 在[!DNL Assets]控制台中，從工具欄按一下&#x200B;**[!UICONTROL Create]**，然後從菜單中選擇&#x200B;**[!UICONTROL Folder]**。

   ![建立資產資料夾](assets/Create-folder.png)

1. 在&#x200B;**[!UICONTROL 建立資料夾]**&#x200B;對話框中，輸入資料夾的標題和名稱（可選），然後選擇&#x200B;**[!UICONTROL Private]**&#x200B;選項。

1. 按一下&#x200B;**[!UICONTROL 建立]**。已建立私人資料夾。

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. 要與其他用戶共用資料夾以及為其分配權限，請選擇該資料夾，然後從工具欄按一下「**[!UICONTROL 屬性]**」。

   ![資訊選項](assets/do-not-localize/info-circle-icon.png)

   >[!NOTE]
   >
   >在您共用資料夾之前，該資料夾不會顯示給任何其他使用者。

1. 在&#x200B;**[!UICONTROL 資料夾屬性]**&#x200B;頁中，從&#x200B;**[!UICONTROL 添加用戶]**&#x200B;清單中選擇用戶，將角色分配給私人資料夾中的用戶，然後按一下&#x200B;**[!UICONTROL 添加]**。

   ![chlimage_1-415](assets/chlimage_1-415.png)

   >[!NOTE]
   >
   >您可以將各種角色（如`Editor`、`Owner`或`Viewer`）指派給您共用資料夾的使用者。 如果您將`Owner`角色指派給使用者，則使用者對資料夾具有`Editor`權限。 此外，使用者可與其他人共用資料夾。 如果您指派`Editor`角色，使用者可以編輯您私人資料夾中的資產。 如果您指派檢視器角色，使用者只能檢視您私人資料夾中的資產。

   >[!NOTE]
   >
   >私人資料夾至少有一個具有`Owner`角色的成員。 因此，管理員無法從專用資料夾中刪除所有所有者成員。 但是，要從專用資料夾中刪除現有所有者（和管理員本身），管理員必須將其他用戶添加為所有者。

1. 按一下「**[!UICONTROL 儲存]**」。根據您指派的角色，當使用者登入[!DNL Assets]時，系統會為使用者指派一組權限給您的私人資料夾。
1. 按一下&#x200B;**[!UICONTROL 確定]**&#x200B;以關閉確認訊息。
1. 您與其共用資料夾的使用者會收到共用通知。 使用用戶憑據登錄[!DNL Assets]以查看通知。

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. 按一下[!UICONTROL Notifications]以開啟通知清單。

   ![通知清單](assets/Assets-Notification.png)

1. 按一下管理員共用的專用資料夾的條目以開啟該資料夾。

>[!NOTE]
>
>要建立專用資料夾，需要在要建立專用資料夾的父資料夾上，讀取並修改[訪問控制權限](/help/sites-administering/security.md#permissions-in-aem)。 如果您不是管理員，預設不會在`/content/dam`上為您啟用這些權限。 在此情況下，請先取得使用者ID/群組的這些權限，再嘗試建立私人資料夾。

## 刪除私人資料夾 {#delete-private-folder}

您可以通過選擇資料夾並從頂部菜單中選擇[!UICONTROL 刪除]選項，或使用鍵盤上的Backspace鍵來刪除資料夾。

![「刪除」選項（在頂端功能表中）](assets/delete-option.png)

>[!CAUTION]
>
>如果您從CRXDE Lite中刪除私人資料夾，則存放庫中會保留多餘的使用者群組。

>[!NOTE]
>
>如果您使用上述方法從使用者介面中刪除資料夾，則也會刪除相關的使用者群組。
>
>不過，在製作例項(`http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`)的JMX中，可使用`clean`方法，從存放庫中移除現有的備援、未使用和自動產生的使用者群組。
