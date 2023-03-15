---
title: 共用資產的私人資料夾
description: 了解如何在 [!DNL Adobe Experience Manager Assets] 並與其他使用者共用，並為其指派各種權限。
contentOwner: AG
role: User
feature: Collaboration
exl-id: c1aece06-7c1c-43a0-bea0-6f11ecda7e68
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 3%

---

# 中的專用資料夾 [!DNL Adobe Experience Manager Assets] {#private-folder}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/private-folder.html?lang=en) |
| AEM 6.5 | 本文 |
| AEM 6.4 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-64/assets/managing/private-folder.html?lang=en) |

您可以在 [!DNL Adobe Experience Manager Assets] 專供您使用的使用者介面。 您可以將此私人資料夾共用給其他使用者，並為其指派各種權限。 根據您指派的權限層級，使用者可以對資料夾執行各種工作，例如在資料夾內檢視資產或編輯資產。

>[!NOTE]
>
>私人資料夾至少有一個具有「所有者」角色的成員。

## 建立和共用私人資料夾 {#create-share-private-folder}

要建立和共用私人資料夾：

1. 在 [!DNL Assets] 主控台，按一下 **[!UICONTROL 建立]** 從工具列，然後選擇 **[!UICONTROL 資料夾]** 的上界。

   ![建立資產資料夾](assets/Create-folder.png)

1. 在 **[!UICONTROL 建立資料夾]** 對話框，輸入資料夾的標題和名稱（可選），然後選擇 **[!UICONTROL 私人]** 選項。

1. 按一下&#x200B;**[!UICONTROL 建立]**。已建立私人資料夾。

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. 要與其他用戶共用資料夾以及為其分配權限，請選擇該資料夾，然後按一下 **[!UICONTROL 屬性]** 的上界。

   ![資訊選項](assets/do-not-localize/info-circle-icon.png)

   >[!NOTE]
   >
   >在您共用資料夾之前，該資料夾不會顯示給任何其他使用者。

1. 在 **[!UICONTROL 資料夾屬性]** 頁面中，從 **[!UICONTROL 添加用戶]** 清單，將角色指派給私人資料夾上的使用者，然後按一下 **[!UICONTROL 新增]**.

   ![chlimage_1-415](assets/chlimage_1-415.png)

   >[!NOTE]
   >
   >您可以指派各種角色，例如 `Editor`, `Owner`，或 `Viewer` 共用資料夾的使用者。 若您指派 `Owner` 角色給使用者，使用者具有 `Editor` 資料夾的權限。 此外，使用者可與其他人共用資料夾。 若您指派 `Editor` 角色，則使用者可以編輯您私人資料夾中的資產。 如果您指派檢視器角色，使用者只能檢視您私人資料夾中的資產。

   >[!NOTE]
   >
   >私人資料夾中至少有一個成員具有 `Owner` 角色。 因此，管理員無法從專用資料夾中刪除所有所有者成員。 但是，要從專用資料夾中刪除現有所有者（和管理員本身），管理員必須將其他用戶添加為所有者。

1. 按一下「**[!UICONTROL 儲存]**」。根據您指派的角色，當使用者登入時，系統會為使用者指派一組權限給您的私人資料夾 [!DNL Assets].
1. 按一下 **[!UICONTROL 確定]** 以關閉確認訊息。
1. 您與其共用資料夾的使用者會收到共用通知。 登入 [!DNL Assets] 以使用者的憑證來檢視通知。

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. 按一下 [!UICONTROL 通知] 以開啟通知清單。

   ![通知清單](assets/Assets-Notification.png)

1. 按一下管理員共用的專用資料夾的條目以開啟該資料夾。

>[!NOTE]
>
>要建立專用資料夾，需要「讀取」和「修改」 [存取控制權限](/help/sites-administering/security.md#permissions-in-aem) 在要建立私人資料夾的父資料夾上。 如果您不是管理員，預設不會為您啟用這些權限 `/content/dam`. 在此情況下，請先取得使用者ID/群組的這些權限，再嘗試建立私人資料夾。

## 刪除私人資料夾 {#delete-private-folder}

您可以選取資料夾並選取「 」，以刪除資料夾 [!UICONTROL 刪除] 選項，或使用鍵盤上的空格鍵。

![「刪除」選項（在頂端功能表中）](assets/delete-option.png)

>[!CAUTION]
>
>如果您從CRXDE Lite中刪除私人資料夾，則存放庫中會保留多餘的使用者群組。

>[!NOTE]
>
>如果您使用上述方法從使用者介面中刪除資料夾，則也會刪除相關的使用者群組。
>
>不過，您可以使用從存放庫中移除現有的備援、未使用和自動產生的使用者群組 `clean` 方法（在Author例項中）`http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`)。
