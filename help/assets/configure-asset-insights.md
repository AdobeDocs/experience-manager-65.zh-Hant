---
title: 設定Assets Insights以取得分析。
description: 在 [!DNL Adobe Experience Manager Assets]中設定Assets Insights。
contentOwner: AG
role: Architect, Admin
feature: Asset Insights,Asset Reports
exl-id: 67be0ae6-5939-40fe-bf8a-b8a2c2f68f15
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 7%

---

# 設定Assets深入分析 {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets]會從[!DNL Adobe Analytics]擷取協力廠商網站使用之數位資產的使用資料。 若要啟用Assets Insights以擷取此資料並產生深入分析，請先設定此功能以與[!DNL Adobe Analytics]整合。 若要在內部部署安裝中使用此功能，請另外購買[!DNL Adobe Analytics]授權。 [!DNL Managed Services]的客戶會收到與[!DNL Experience Manager]繫結的[!DNL Analytics]授權。 請參閱[Managed Services產品說明](https://helpx.adobe.com/tw/legal/product-descriptions/adobe-experience-manager-managed-services.html)。

>[!NOTE]
>
>僅支援並為影像提供深入分析。

1. 在[!DNL Experience Manager]中，按一下&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]**。

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. 按一下「 **[!UICONTROL 前瞻分析設定]** 」資訊卡。
1. 在精靈中，選取資料中心並提供您的認證，包括組織名稱、使用者名稱和共用機密。

   ![在Experience Manager中設定Adobe Analytics以進行Assets Insights](assets/insights_config2.png)

   *圖：在[!DNL Experience Manager].*&#x200B;中設定Assets Insights的[!DNL Adobe Analytics]

1. 按一下&#x200B;**[!UICONTROL 驗證]**。
1. [!DNL Experience Manager]驗證您的認證後，從&#x200B;**[!UICONTROL 報表套裝]**&#x200B;清單中，選擇您希望Assets分析擷取資料的[!DNL Adobe Analytics]報表套裝。 按一下&#x200B;**[!UICONTROL 新增]**。
1. 在[!DNL Experience Manager]設定您的報表套裝後，按一下&#x200B;**[!UICONTROL 完成]**。

## 頁面追蹤器 {#page-tracker}

在您設定[!DNL Adobe Analytics]帳戶後，系統就會為您產生頁面追蹤器程式碼。 若要啟用Assets Insights以追蹤第三方網站中使用的[!DNL Experience Manager]資產，請在網站程式碼中包含頁面追蹤器程式碼。 使用[!DNL Experience Manager Assets]中的[!UICONTROL 頁面追蹤器]公用程式來產生頁面追蹤器代碼。 如需如何將頁面追蹤器程式碼包含在協力廠商網頁中的詳細資訊，請參閱[在網頁中使用頁面追蹤器和內嵌程式碼](/help/assets/use-page-tracker.md)。

1. 在[!DNL Experience Manager]中，按一下&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]**。

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. 在導覽頁 **[!UICONTROL 面中]** ，按一下 **&#x200B;**&#x200B;前瞻分析頁面追蹤器卡片。
1. 按一下&#x200B;**[!UICONTROL 下載]**&#x200B;以下載頁面追蹤程式碼。
