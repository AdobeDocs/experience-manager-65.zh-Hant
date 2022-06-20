---
title: 共用資產的專用資料夾
description: 瞭解如何在 [!DNL Adobe Experience Manager Assets] 與其他用戶共用，並為其分配各種權限。
contentOwner: AG
role: User
feature: Collaboration
exl-id: c1aece06-7c1c-43a0-bea0-6f11ecda7e68
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 2%

---

# 中的專用資料夾 [!DNL Adobe Experience Manager Assets] {#private-folder}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/private-folder.html?lang=en) |
| AEM 6.5 | 本文 |
| AEM 6.4 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-64/assets/managing/private-folder.html?lang=en) |

您可以在 [!DNL Adobe Experience Manager Assets] 只供您使用的用戶介面。 您可以將此專用資料夾共用給其他用戶，並為其分配各種權限。 根據您分配的權限級別，用戶可以對資料夾執行各種任務，例如查看資料夾內的資產或編輯資產。

>[!NOTE]
>
>專用資料夾至少有一個具有所有者角色的成員。

## 專用資料夾建立和共用 {#create-share-private-folder}

要建立和共用專用資料夾：

1. 在 [!DNL Assets] 控制台，按一下 **[!UICONTROL 建立]** ，然後選擇 **[!UICONTROL 資料夾]** 的子菜單。

   ![建立資產資料夾](assets/Create-folder.png)

1. 在 **[!UICONTROL 建立資料夾]** 對話框，輸入資料夾的標題和名稱（可選），然後選擇 **[!UICONTROL 私人]** 的雙曲餘切值。

1. 按一下&#x200B;**[!UICONTROL 建立]**。建立專用資料夾。

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. 要與其他用戶共用資料夾並為其分配權限，請選擇該資料夾，然後按一下 **[!UICONTROL 屬性]** 的子菜單。

   ![資訊選項](assets/do-not-localize/info-circle-icon.png)

   >[!NOTE]
   >
   >在您共用該資料夾之前，該資料夾對任何其他用戶都不可見。

1. 在 **[!UICONTROL 資料夾屬性]** 頁，從 **[!UICONTROL 添加用戶]** 清單，將角色分配給您的個人資料夾上的用戶，然後按一下 **[!UICONTROL 添加]**。

   ![chlimage_1-415](assets/chlimage_1-415.png)

   >[!NOTE]
   >
   >可以指定各種角色，如 `Editor`。 `Owner`或 `Viewer` 與您共用資料夾的用戶。 如果分配 `Owner` 角色，用戶 `Editor` 資料夾的權限。 此外，用戶還可以與他人共用該資料夾。 如果分配 `Editor` 角色，用戶可以編輯您的專用資料夾中的資產。 如果您分配了查看者角色，則用戶只能查看您的專用資料夾中的資產。

   >[!NOTE]
   >
   >專用資料夾至少包含一個成員 `Owner` 角色。 因此，管理員無法從專用資料夾中刪除所有所有者成員。 但是，要從專用資料夾中刪除現有所有者（和管理員本身），管理員必須將其他用戶添加為所有者。

1. 按一下「**[!UICONTROL 儲存]**」。根據您分配的角色，用戶在登錄到時會為您的專用資料夾分配一組權限 [!DNL Assets]。
1. 按一下 **[!UICONTROL 確定]** 關閉確認消息。
1. 與您共用資料夾的用戶會收到共用通知。 登錄到 [!DNL Assets] 用戶的憑據查看通知。

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. 按一下 [!UICONTROL 通知] 開啟通知清單。

   ![通知清單](assets/Assets-Notification.png)

1. 按一下管理員共用的專用資料夾條目以開啟該資料夾。

>[!NOTE]
>
>要建立專用資料夾，需要「讀取」和「修改」 [訪問控制權限](/help/sites-administering/security.md#permissions-in-aem) 在要建立專用資料夾的父資料夾上。 如果您不是管理員，則預設情況下，這些權限不會為您啟用 `/content/dam`。 在這種情況下，首先獲取用戶ID/組的這些權限，然後嘗試建立專用資料夾。

## 刪除專用資料夾 {#delete-private-folder}

通過選擇資料夾並選擇 [!UICONTROL 刪除] 選項，或使用鍵盤上的Backspace鍵。

![「刪除」選項在頂部菜單中](assets/delete-option.png)

>[!CAUTION]
>
>如果從CRXDE Lite中刪除專用資料夾，則儲存庫中將保留冗餘用戶組。

>[!NOTE]
>
>如果使用上述方法從用戶介面中刪除資料夾，則還會刪除關聯的用戶組。
>
>但是，現有的冗餘、未使用和自動生成的用戶組可以使用 `clean` JMX中的方法(`http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`)。
