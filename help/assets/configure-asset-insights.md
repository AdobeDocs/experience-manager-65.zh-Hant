---
title: 設定Assets Insights以取得分析。
description: 在 [!DNL Adobe Experience Manager Assets]中設定Assets Insights。
contentOwner: AG
role: Architect, Administrator
feature: 資產分析，資產報表
exl-id: 67be0ae6-5939-40fe-bf8a-b8a2c2f68f15
source-git-commit: 68c36d4e3a14567a4d115ee64a4474bcaf9aa386
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 6%

---

# 設定Assets Insights {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] 從中擷取協力廠商網站所使用數位資產的使用資料 [!DNL Adobe Analytics]。若要啟用Assets Insights以擷取此資料並產生深入分析，請先設定功能以與[!DNL Adobe Analytics]整合。 若要在內部部署安裝中使用此功能，請分別購買[!DNL Adobe Analytics]授權。 [!DNL Managed Services]上的客戶會收到與[!DNL Experience Manager]捆綁的[!DNL Analytics]許可證。 請參閱[Managed Services產品說明](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)。

>[!NOTE]
>
>僅支援並提供影像見解。

1. 在[!DNL Experience Manager]中，按一下&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 資產]**。

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. 按一下「 **[!UICONTROL 前瞻分析設定]** 」資訊卡。
1. 在精靈中，選取資料中心並提供您的認證，包括組織名稱、使用者名稱和共用機密。

   ![在Adobe Analytics中設定Assets InsightsExperience Manager](assets/insights_config2.png)

   *圖：在中 [!DNL Adobe Analytics] 為Assets Insights進行設 [!DNL Experience Manager]定。*

1. 按一下「**[!UICONTROL 驗證]**」。
1. 在[!DNL Experience Manager]驗證您的憑證後，從&#x200B;**[!UICONTROL 報表套裝]**&#x200B;清單中，選擇您要Assets Insights擷取資料的[!DNL Adobe Analytics]報表套裝。 按一下&#x200B;**[!UICONTROL 「新增」]**。
1. 在[!DNL Experience Manager]設定報表套裝後，按一下&#x200B;**[!UICONTROL Done]**。

## 頁面追蹤器{#page-tracker}

設定[!DNL Adobe Analytics]帳戶後，系統會為您產生頁面追蹤器代碼。 若要啟用「資產前瞻分析」以追蹤第三方網站中使用的[!DNL Experience Manager]資產，請在網站程式碼中加入頁面追蹤器程式碼。 使用[!DNL Experience Manager Assets]中的[!UICONTROL 頁面追蹤器]公用程式產生頁面追蹤器程式碼。 如需如何將您的頁面追蹤器程式碼納入第三方網頁的詳細資訊，請參閱[使用頁面追蹤器並在網頁中內嵌程式碼](/help/assets/use-page-tracker.md)。

1. 在[!DNL Experience Manager]中，按一下&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 資產]**。

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. 在導覽頁 **[!UICONTROL 面中]** ，按一下 **** 前瞻分析頁面追蹤器卡片。
1. 按一下&#x200B;**[!UICONTROL 下載]**&#x200B;以下載頁面追蹤器程式碼。
