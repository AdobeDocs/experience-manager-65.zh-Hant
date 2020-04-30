---
title: 設定資產前瞻分析，以取得數位資產使用分析。
description: 在[!DNL Adobe Experience Manager Assets]中設定資產見解。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# 設定資產分析 {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] 從中擷取協力廠商網站使用之數位資產的使用資料 [!DNL Adobe Analytics]。 若要讓「資產前瞻分析」擷取此資料並產生前瞻分析，請先設定功能以與Adobe Analytics整合。

>[!NOTE]
>
>只有影像才支援並提供見解。

1. In [!DNL Experience Manager], click **[!UICONTROL Tools]** > **[!UICONTROL Assets]**.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. 按一下「 **[!UICONTROL 前瞻分析設定]** 」資訊卡。
1. 在精靈中，選取資料中心並提供您的認證，包括您的組織名稱、使用者名稱和共用密碼。

   ![在Experience Manager中設定Adobe Analytics的資產見解](assets/insights_config2.png)

   *圖：在中[!DNL Adobe Analytics]設定資產分析[!DNL Experience Manager]。*

1. 按一 **[!UICONTROL 下驗證]**。
1. 驗證 [!DNL Experience Manager] 您的認證後，從「報表套裝」 **[!UICONTROL 清單中]**[!DNL Adobe Analytics] ，選擇您要從中擷取資產分析的報表套裝。 按一下&#x200B;**[!UICONTROL 「新增」]**。
1. 設 [!DNL Experience Manager] 定報表套裝後，按一下 **[!UICONTROL 完成]**。

## 頁面追蹤器 {#page-tracker}

在您設定帳戶 [!DNL Adobe Analytics] 後，會為您產生頁面追蹤器代碼。 若要啟用「資產前瞻分析」 [!DNL Experience Manager] 來追蹤第三方網站中使用的資產，請在網站程式碼中加入頁面追蹤器程式碼。 使用中 [!UICONTROL 的「頁面追蹤] 」公用 [!DNL Experience Manager Assets] 程式來產生頁面追蹤程式碼。 如需如何將頁面追蹤器程式碼包含在協力廠商網頁中的詳細資訊，請參閱「使 [用頁面追蹤器並在網頁中內嵌程式碼」](/help/assets/touch-ui-using-page-tracker.md)。

1. In [!DNL Experience Manager], click **[!UICONTROL Tools]** > **[!UICONTROL Assets]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. 在導覽頁 **[!UICONTROL 面中]** ，按一下 **** 前瞻分析頁面追蹤器卡片。
1. 按一 **[!UICONTROL 下「下載]** 」以下載頁面追蹤器代碼。
