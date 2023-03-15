---
title: 設定Assets Insights以取得分析。
description: 在中設定Assets Insights [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Architect, Admin
feature: Asset Insights,Asset Reports
exl-id: 67be0ae6-5939-40fe-bf8a-b8a2c2f68f15
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 7%

---

# 設定Assets Insights {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] 從擷取協力廠商網站所使用數位資產的使用資料 [!DNL Adobe Analytics]. 若要讓Assets Insights擷取此資料並產生深入分析，請先設定功能以與 [!DNL Adobe Analytics]. 若要在內部部署中使用此功能，請購買 [!DNL Adobe Analytics] 單獨授權。 客戶 [!DNL Managed Services] 接收 [!DNL Analytics] 隨附 [!DNL Experience Manager]. 請參閱 [Managed Services產品說明](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html).

>[!NOTE]
>
>僅支援並提供影像見解。

1. 在 [!DNL Experience Manager]，按一下 **[!UICONTROL 工具]** > **[!UICONTROL 資產]**.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. 按一下「 **[!UICONTROL 前瞻分析設定]** 」資訊卡。
1. 在精靈中，選取資料中心並提供您的認證，包括組織名稱、使用者名稱和共用機密。

   ![在Adobe Analytics中設定Assets InsightsExperience Manager](assets/insights_config2.png)

   *圖：設定 [!DNL Adobe Analytics] （針對中的資產分析） [!DNL Experience Manager].*

1. 按一下 **[!UICONTROL 驗證]**.
1. 之後 [!DNL Experience Manager] 驗證您的憑證，從 **[!UICONTROL 報表套裝]** 清單，選擇 [!DNL Adobe Analytics] 您想要Assets Insights擷取資料的報表套裝。 按一下&#x200B;**[!UICONTROL 「新增」]**。
1. 之後 [!DNL Experience Manager] 設定您的報表套裝，按一下 **[!UICONTROL 完成]**.

## 頁面追蹤器 {#page-tracker}

在您設定 [!DNL Adobe Analytics] 帳戶時，系統會為您產生頁面追蹤器程式碼。 啟用Assets Insights以追蹤 [!DNL Experience Manager] 協力廠商網站中使用的資產，請在網站程式碼中加入頁面追蹤器程式碼。 使用 [!UICONTROL 頁面追蹤器] 實用程式 [!DNL Experience Manager Assets] 來產生頁面追蹤器程式碼。 如需如何在協力廠商網頁中加入頁面追蹤器程式碼的詳細資訊，請參閱 [使用頁面追蹤器並在網頁中內嵌程式碼](/help/assets/use-page-tracker.md).

1. 在 [!DNL Experience Manager]，按一下 **[!UICONTROL 工具]** > **[!UICONTROL 資產]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. 在導覽頁 **[!UICONTROL 面中]** ，按一下 **** 前瞻分析頁面追蹤器卡片。
1. 按一下 **[!UICONTROL 下載]** 下載頁面追蹤器程式碼。
