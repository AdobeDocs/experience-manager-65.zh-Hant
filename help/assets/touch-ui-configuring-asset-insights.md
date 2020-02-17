---
title: 設定資產分析
description: 在AEM資產中設定資產分析。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 6d4f79c126a3c44666e2a42b2246c964813d24ab

---


# 設定資產分析 {#configure-asset-insights}

Adobe Experience Manager(AEM)Assets會從Adobe Analytics擷取協力廠商網站所使用之AEM資產的使用資料。 若要讓「資產前瞻分析」擷取此資料並產生前瞻分析，請先設定功能以與Adobe Analytics整合。

>[!NOTE]
>
>只有影像才支援並提供見解。

1. 在AEM中，按一下「 **[!UICONTROL 工具]** > **[!UICONTROL 資產]**」。

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. 按一下「 **[!UICONTROL 前瞻分析設定]** 」資訊卡。
1. 在精靈中，選取資料中心並提供您的認證，包括您的組織名稱、使用者名稱和共用密碼。

   ![在AEM中設定Adobe Analytics的資產見解](assets/insights_config2.png)


   *圖：在AEM中設定Adobe Analytics的資產見解*

1. 按一下／點選「 **[!UICONTROL 驗證]**」。
1. 在AEM驗證您的認證後，從「報表套裝」清單 **[!UICONTROL 中]** ，選擇Adobe Analytics報表套裝，讓您從中擷取資產分析。 按一下&#x200B;**[!UICONTROL 「新增」]**。
1. AEM設定您的報表套裝後，按一下／點選「完 **[!UICONTROL 成]**」。

## 頁面追蹤器 {#page-tracker}

在您設定Adobe Analytics帳戶後，就會產生頁面追蹤器代碼。 若要啟用「資產前瞻分析」來追蹤協力廠商網站中使用的AEM資產，請在網站程式碼中加入頁面追蹤器程式碼。 使用AEM Assets中的「頁面追蹤器」公用程式來產生頁面追蹤器代碼。 如需如何將頁面追蹤器程式碼包含在協力廠商網頁中的詳細資訊，請參閱「使 [用頁面追蹤器並在網頁中內嵌程式碼」](/help/assets/touch-ui-using-page-tracker.md)。

1. 在AEM中，按一下「 **[!UICONTROL 工具]** > **[!UICONTROL 資產]**」。

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. 在導覽頁 **[!UICONTROL 面中]** ，按一下 **** 前瞻分析頁面追蹤器卡片。
1. 按一 **[!UICONTROL 下「下載]** 」以下載頁面追蹤器代碼。
