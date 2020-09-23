---
title: 私人資料夾位於 [!DNL Adobe Experience Manager Assets]
description: 瞭解如何在中建立私人資料 [!DNL Adobe Experience Manager Assets] 夾，並與其他使用者共用資料夾，以及為他們指派各種權限。
contentOwner: AG
translation-type: tm+mt
source-git-commit: be97ef4f3bb6b904dabcfcd44025a4898bcf4dee
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 0%

---


# 私人資料夾位於 [!DNL Adobe Experience Manager Assets] {#private-folder}

您可以在使用者介面中建立 [!DNL Adobe Experience Manager Assets] 專屬於您的私人資料夾。 您可以將此私人資料夾共用給其他使用者，並為其指派各種權限。 根據您指派的權限層級，使用者可以對資料夾執行各種工作，例如檢視資料夾內的資產或編輯資產。

>[!NOTE]
>
>私人資料夾至少有一個擁有擁有者角色的成員。

## 私人資料夾建立與共用 {#create-share-private-folder}

要建立和共用專用資料夾：

1. 在控制 [!DNL Assets] 台中，按一下工 **[!UICONTROL 具列中的「建立]** 」，然後從選單中選 **[!UICONTROL 擇「資料夾]** 」。

   ![建立資產檔案夾](assets/Create-folder.png)

1. 在「創 **[!UICONTROL 建資料夾]** 」對話框中，輸入資料夾的標題和名稱（可選），然後選擇「 **[!UICONTROL 私用]** 」選項。

1. 按一下&#x200B;**[!UICONTROL 建立]**。建立專用資料夾。

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

1. 按一下&#x200B;**[!UICONTROL 「儲存」]**。根據您指派的角色，當使用者登入時，會為使用者指派一組權限給您的私人資料夾 [!DNL Assets]。
1. 按一下 **[!UICONTROL 確定]** ，關閉確認消息。
1. 與您共用資料夾的使用者會收到共用通知。 使用用 [!DNL Assets] 者的認證登入以檢視通知。

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. 按一下「通知」以開啟通知清單。

   ![通知清單](assets/Assets-Notification.png)

1. 按一下管理員共用的專用資料夾條目以開啟該資料夾。

>[!NOTE]
>
>要建立專用資料夾，您需要對要建立專用資料夾的父 [資料夾](/help/sites-administering/security.md#permissions-in-aem) ，具有「讀取」和「修改」訪問控制權限。 如果您不是管理員，則這些權限依預設不會為您啟用 `/content/dam`。 在這種情況下，請先取得使用者ID/群組的這些權限，再嘗試建立私人資料夾。

## 刪除專用資料夾 {#delete-private-folder}

您可以通過選擇資料夾並從頂部菜單中選擇「刪 [!UICONTROL 除] 」選項，或使用鍵盤上的Backspace鍵刪除資料夾。

![頂部菜單中的刪除選項](assets/delete-option.png)

>[!CAUTION]
>
>如果從CRXDE Lite刪除專用資料夾，則儲存庫中將保留冗餘用戶組。

>[!NOTE]
>
>如果您使用上述方法從使用者介面刪除資料夾，則相關的使用者群組也會隨之刪除。
不過，使用 [JMX可以從資料庫清理現有的冗餘、未使用和自動生成的用戶組](#group-clean-up-jmx)。

### 使用JMX來清除未使用的使用者群組 {#group-clean-up-jmx}

要清除未使用用戶組的儲存庫，請執行以下操作：

1. 開啟JMX以清除您作者例項中「資產」的 [!DNL Experience Manager] 冗餘群組 `http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`。
For example, `http://no1010042068039.corp.adobe.com:4502/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`.

1. 從此JMX `clean` 調用方法。

您可以看到，所有冗餘用戶組或自動生成的組（建立名稱與先前刪除的組相同的資料夾時建立的組）都將從路徑中刪除 `/home/groups/mac/default/<user_name>/<folder_name>`。
