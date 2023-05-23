---
title: 配置Assets Insights以獲取分析。
description: 在中配置Assets Insights [!DNL Adobe Experience Manager Assets]。
contentOwner: AG
role: Architect, Admin
feature: Asset Insights,Asset Reports
exl-id: 67be0ae6-5939-40fe-bf8a-b8a2c2f68f15
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 6%

---

# 配置資產透視 {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] 從第三方網站獲取有關數字資產的使用資料 [!DNL Adobe Analytics]。 要使Assets Insights能夠檢索此資料並生成見解，請首先配置該功能以與 [!DNL Adobe Analytics]。 要在內部安裝中使用此功能，請購買 [!DNL Adobe Analytics] 單獨許可。 客戶 [!DNL Managed Services] 接收 [!DNL Analytics] 與 [!DNL Experience Manager]。 請參閱 [Managed Services產品說明](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)。

>[!NOTE]
>
>只支援和提供影像的見解。

1. 在 [!DNL Experience Manager]按一下 **[!UICONTROL 工具]** > **[!UICONTROL 資產]**。

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. 按一下「 **[!UICONTROL 前瞻分析設定]** 」資訊卡。
1. 在嚮導中，選擇資料中心並提供您的憑據，包括組織名稱、用戶名和共用密鑰。

   ![配置Adobe Analytics的Experience Manager中的Assets Insights](assets/insights_config2.png)

   *圖：配置 [!DNL Adobe Analytics] 對於中的Assets Insights [!DNL Experience Manager]。*

1. 按一下 **[!UICONTROL 驗證]**。
1. 之後 [!DNL Experience Manager] 驗證您的憑據，從 **[!UICONTROL 報表套件]** 清單，選擇 [!DNL Adobe Analytics] 從Assets Insights獲取資料的報告套件。 按一下 **[!UICONTROL 添加]**。
1. 之後 [!DNL Experience Manager] 設定報告套件，按一下 **[!UICONTROL 完成]**。

## 頁面跟蹤器 {#page-tracker}

配置完 [!DNL Adobe Analytics] 帳戶，將為您生成頁跟蹤器代碼。 要啟用Assets Insights以跟蹤 [!DNL Experience Manager] 用於第三方網站的資產，包括網站代碼中的頁面跟蹤程式碼。 使用 [!UICONTROL 頁面跟蹤器] 實用程式 [!DNL Experience Manager Assets] 生成頁跟蹤器代碼。 有關如何在第三方網頁中包含頁面跟蹤器代碼的詳細資訊，請參閱 [使用頁面跟蹤器並在網頁中嵌入代碼](/help/assets/use-page-tracker.md)。

1. 在 [!DNL Experience Manager]按一下 **[!UICONTROL 工具]** > **[!UICONTROL 資產]**。

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. 在導覽頁 **[!UICONTROL 面中]** ，按一下 **** 前瞻分析頁面追蹤器卡片。
1. 按一下 **[!UICONTROL 下載]** 下載頁面跟蹤器代碼。
