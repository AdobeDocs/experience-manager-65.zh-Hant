---
title: 登入並登出您的數位資產以進行編輯
description: 瞭解如何取出要編輯的資產，並在變更完成後將其存回。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 07c1a4102539ba4678c55dee3a4882101e39864f

---


# AEM DAM中的登入和登出檔案 {#check-in-and-check-out-files-in-assets}

Adobe Experience Manager(AEM)Assets可讓您取出要編輯的資產，並在完成變更後將其存回。 結帳資產後，只有您可以編輯、註解、發佈、移動或刪除資產。 簽出資產會鎖定資產。 在您將資產存回AEM Assets之前，其他使用者無法對資產執行任何這些作業。 不過，他們仍可變更鎖定資產的中繼資料。

若要能夠登出／登入資產，您需要有其「寫入」存取權。

此功能可協助防止其他使用者覆寫作者所做的變更，讓多位使用者在跨團隊編輯工作流程時共同作業。

## 結帳資產 {#checking-out-assets}

1. 從「資產」使用者介面中，選取您要結帳的資產。 您也可以選取多個資產以結帳。
1. 在工具列中，按一下／點選「 **[!UICONTROL 結帳」]**。
「檢 **[!UICONTROL 出]** 」選項切換 **[!UICONTROL 為「檢入」]**。
若要確認其他使用者是否可以編輯您簽出的資產，請以其他使用者的身分登入。 鎖定符號會顯示在已簽出的資產的縮圖上。

   ![chlimage_1-471](assets/chlimage_1-471.png)

   選取資產。 請注意，工具列不會顯示任何選項，讓您編輯、註解、發佈或刪除資產。

   ![chlimage_1-472](assets/chlimage_1-472.png)

   不過，您可以點選「檢 **[!UICONTROL 視屬性]** 」來編輯鎖定資產的中繼資料。

1. 點選「 **[!UICONTROL 編輯]** 」，在編輯模式中開啟資產。

   ![chlimage_1-473](assets/chlimage_1-473.png)

1. 編輯資產並儲存變更。 例如，裁切影像並儲存。

   ![chlimage_1-474](assets/chlimage_1-474.png)

   您也可以選擇註解或發佈資產。

1. 從「資產」UI中選取已編輯的資產，然後從工具列中點選「 **[!UICONTROL 登入]** 」。 已修改的資產會登入AEM Assets，可供其他使用者編輯。

## 強制登入 {#forced-check-in}

管理員可以簽入由其他用戶簽出的資產。

1. 以管理員身分登入AEM Assets。
1. 從「資產」使用者介面中，選取一或多個已由其他使用者簽出的資產。

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. 在工具列中，點選「 **[!UICONTROL 釋放鎖定」]**。 資產已登入，可供其他使用者編輯。

>[!MORELIKETHIS]
>
>* [瞭解AEM案頭應用程式的登入與登出](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#how-app-works2)
>* [教學課程影片，以瞭解AEM Assets中的存回和存回](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/collaboration/checkin-checkout-technical-video-understand.html)

