---
title: Configure Asset Insights to get digial asset usage analytics.
description: Configure Asset Insights in [!DNL Adobe Experience Manager Assets].
contentOwner: AG
translation-type: tm+mt
source-git-commit: b59f7471ab9f3c5e6eb3365122262b592c8e6244
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 7%

---


# 設定資產分析 {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] fetches usage data around digital assets used by third-party websites from [!DNL Adobe Analytics]. To enable Asset Insights to retrieve this data and generate insights, first configure the feature to integrate with Adobe Analytics.

>[!NOTE]
>
>Insights are only supported and provided for images.

1. In [!DNL Experience Manager], click **[!UICONTROL Tools]** > **[!UICONTROL Assets]**.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. 按一下「 **[!UICONTROL 前瞻分析設定]** 」資訊卡。
1. In the wizard, select a data center and provide your credentials including the name of your organization, user name, and Shared Secret.

   ![在Experience Manager中設定Adobe Analytics的資產見解](assets/insights_config2.png)

   *Figure: Configure[!DNL Adobe Analytics]for Assets Insights in[!DNL Experience Manager].*

1. 按一 **[!UICONTROL 下驗證]**。
1. 驗證 [!DNL Experience Manager] 您的認證後，從「報表套裝」 **[!UICONTROL 清單中]**[!DNL Adobe Analytics] ，選擇您要從中擷取資產分析的報表套裝。 按一下&#x200B;**[!UICONTROL 「新增」]**。
1. 設 [!DNL Experience Manager] 定報表套裝後，按一下 **[!UICONTROL 完成]**。

## 頁面追蹤器 {#page-tracker}

在您設定帳戶 [!DNL Adobe Analytics] 後，會為您產生頁面追蹤器代碼。 若要啟用「資產前瞻分析」 [!DNL Experience Manager] 來追蹤第三方網站中使用的資產，請在網站程式碼中加入頁面追蹤器程式碼。 使用中 [!UICONTROL 的「頁面追蹤] 」公用 [!DNL Experience Manager Assets] 程式來產生頁面追蹤程式碼。 如需如何將頁面追蹤器程式碼包含在協力廠商網頁中的詳細資訊，請參閱「使 [用頁面追蹤器並在網頁中內嵌程式碼」](/help/assets/touch-ui-using-page-tracker.md)。

1. In [!DNL Experience Manager], click **[!UICONTROL Tools]** > **[!UICONTROL Assets]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. 在導覽頁 **[!UICONTROL 面中]** ，按一下 **** 前瞻分析頁面追蹤器卡片。
1. Click **[!UICONTROL Download]** to download the page tracker code.
