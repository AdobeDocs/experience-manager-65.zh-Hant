---
title: 共用資產的私人資料夾
description: 瞭解如何在 [!DNL Adobe Experience Manager Assets] 中建立專用資料夾，並與其他用戶共用該資料夾，並為其分配各種權限。
contentOwner: AG
role: Business Practitioner
feature: Collaboration
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 1%

---


# [!DNL Adobe Experience Manager Assets] {#private-folder}中的專用資料夾

您可以在[!DNL Adobe Experience Manager Assets]使用者介面中建立專供您使用的私人資料夾。 您可以將此私人資料夾共用給其他使用者，並為其指派各種權限。 根據您指派的權限層級，使用者可以對資料夾執行各種工作，例如檢視資料夾內的資產或編輯資產。

>[!NOTE]
>
>私人資料夾至少有一個擁有擁有者角色的成員。

## 建立和共用{#create-share-private-folder}專用資料夾

要建立和共用專用資料夾：

1. 在[!DNL Assets]控制台中，從工具欄按一下&#x200B;**[!UICONTROL 建立]**，然後從菜單中選擇&#x200B;**[!UICONTROL 資料夾]**。

   ![建立資產檔案夾](assets/Create-folder.png)

1. 在&#x200B;**[!UICONTROL 建立資料夾]**&#x200B;對話框中，輸入資料夾的標題和名稱（可選），然後選擇&#x200B;**[!UICONTROL 專用]**&#x200B;選項。

1. 按一下&#x200B;**[!UICONTROL 建立]**。建立專用資料夾。

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. 要與其他用戶共用資料夾以及為其分配權限，請選擇該資料夾，然後從工具欄中按一下「屬性」。****

   ![資訊選項](assets/do-not-localize/info-circle-icon.png)

   >[!NOTE]
   >
   >在您共用資料夾之前，該資料夾不會顯示給任何其他使用者。

1. 在&#x200B;**[!UICONTROL 資料夾屬性]**&#x200B;頁面中，從&#x200B;**[!UICONTROL 添加用戶]**&#x200B;清單中選擇用戶，在私人資料夾中為用戶分配角色，然後按一下&#x200B;**[!UICONTROL 添加]**。

   ![chlimage_1-415](assets/chlimage_1-415.png)

   >[!NOTE]
   >
   >您可以將各種角色（例如`Editor`、`Owner`或`Viewer`）指派給與您共用資料夾的使用者。 如果您指派`Owner`角色給使用者，則使用者對資料夾具有`Editor`權限。 此外，使用者也可以與其他人共用資料夾。 如果您指派`Editor`角色，使用者可以編輯私人資料夾中的資產。 如果您指派檢視器角色，使用者只能檢視您私人資料夾中的資產。

   >[!NOTE]
   >
   >專用資料夾至少有一個`Owner`角色的成員。 因此，管理員無法從專用資料夾中刪除所有所有者成員。 但是，要從專用資料夾中刪除現有所有者（和管理員本身），管理員必須將其他用戶添加為所有者。

1. 按一下「**[!UICONTROL 儲存]**」。根據您指派的角色，當使用者登入[!DNL Assets]時，會為使用者指派一組權限給您的私人資料夾。
1. 按一下&#x200B;**[!UICONTROL 確定]**&#x200B;以關閉確認消息。
1. 與您共用資料夾的使用者會收到共用通知。 使用用戶的憑據登錄[!DNL Assets]以查看通知。

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. 按一下[!UICONTROL 通知]以開啟通知清單。

   ![通知清單](assets/Assets-Notification.png)

1. 按一下管理員共用的專用資料夾條目以開啟該資料夾。

>[!NOTE]
>
>要建立專用資料夾，需要在要建立專用資料夾的父資料夾上讀取並修改[訪問控制權限](/help/sites-administering/security.md#permissions-in-aem)。 如果您不是管理員，則在`/content/dam`上預設不會為您啟用這些權限。 在這種情況下，請先取得使用者ID/群組的這些權限，再嘗試建立私人資料夾。

## 刪除專用資料夾{#delete-private-folder}

您可以通過選擇資料夾並從頂部菜單中選擇[!UICONTROL Delete]選項，或使用鍵盤上的Backspace鍵來刪除資料夾。

![頂部菜單中的刪除選項](assets/delete-option.png)

>[!CAUTION]
>
>如果從CRXDE Lite中刪除專用資料夾，則儲存庫中將保留冗餘用戶組。

>[!NOTE]
>
>如果您使用上述方法從使用者介面刪除資料夾，則相關的使用者群組也會隨之刪除。
>
>但是，使用作者實例(`http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`)中JMX的`clean`方法，可從儲存庫中刪除現有的冗餘、未使用和自動生成的用戶組。
