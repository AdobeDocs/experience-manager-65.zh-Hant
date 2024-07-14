---
title: 簽入及簽出 [!DNL Assets]中的檔案
description: 瞭解如何簽出資產進行編輯，並在變更完成後重新簽入。
contentOwner: AG
role: User
feature: Asset Management
exl-id: 544ef73c-4e4b-433f-a173-fdf1c8f45d8e
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 5%

---

# 在[!DNL Experience Manager] DAM中籤入和簽出檔案 {#check-in-and-check-out-files-in-assets}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/check-out-and-submit-assets.html?lang=en) |
| AEM 6.5 | 本文章 |

[!DNL Adobe Experience Manager Assets]可讓您簽出要編輯的資產，並在完成變更後重新簽入。 出庫資產後，只有您可以編輯、註釋、發佈、移動或刪除資產。 取出資產會鎖定資產。 在您將該資產簽回[!DNL Assets]之前，其他使用者無法對該資產執行任何這些操作。 但是，他們仍可變更已鎖定資產的中繼資料。

若要能夠簽出/簽入資產，您需要這些資產的寫入許可權。

此功能可防止其他使用者覆寫作者所做的變更，也就是讓多位使用者共同編輯跨團隊的工作流程。

## 簽出資產 {#checking-out-assets}

1. 從[!DNL Assets]使用者介面中，選取您要簽出的資產。 您也可以選取多個要簽出的資產。
1. 在工具列中按一下&#x200B;**[!UICONTROL 簽出]**。 **[!UICONTROL 簽出]**&#x200B;選項會切換至&#x200B;**[!UICONTROL 簽入]**。
若要確認其他使用者是否可編輯您取出的資產，請以其他使用者的身分登入。 在您出庫的資產縮圖上會顯示鎖定符號。

   ![chlimage_1-471](assets/chlimage_1-471.png)

   選取資產。 請注意，工具列不會顯示任何可讓您編輯、註釋、發佈或刪除資產的選項。

   ![chlimage_1-472](assets/chlimage_1-472.png)

   若要編輯已鎖定資產的中繼資料，請按一下&#x200B;**[!UICONTROL 檢視屬性]**。

1. 按一下&#x200B;**[!UICONTROL 編輯]**&#x200B;以編輯模式開啟資產。

   ![chlimage_1-473](assets/chlimage_1-473.png)

1. 編輯資產並儲存變更。 例如，裁切影像並儲存。

   ![chlimage_1-474](assets/chlimage_1-474.png)

   您也可以選擇為資產加上註解或發佈。

1. 從[!DNL Assets]介面選取已編輯的資產，然後按一下工具列中的&#x200B;**[!UICONTROL 簽入]**。 已修改的資產已簽入[!DNL Assets]，可供其他使用者編輯。

## 強制籤入 {#forced-check-in}

管理員可以簽入由其他使用者簽出的資產。

1. 以系統管理員身分登入[!DNL Assets]。
1. 從[!DNL Assets]使用者介面中，選取一或多個已由其他使用者簽出的資產。

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. 從工具列中按一下&#x200B;**[!UICONTROL 解除鎖定]**。 資產會重新入庫，以供其他使用者編輯。

## 最佳作法和限制 {#tips-limitations}

* 可以刪除包含已取出資產檔案的&#x200B;*資料夾*。 刪除資料夾之前，請確定使用者未簽出任何數位資產。

>[!MORELIKETHIS]
>
>* [了解籤入和簽出 [!DNL Experience Manager] 案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#how-app-works2)
>* [視訊教學課程，以了解籤入和簽出 [!DNL Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/collaboration/check-in-and-check-out.html)
