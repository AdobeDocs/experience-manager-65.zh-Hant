---
title: 設定資產前瞻分析以取得分析。
description: 在 [!DNL Adobe Experience Manager Assets]中設定資產前瞻分析。
contentOwner: AG
role: Architect, Administrator
feature: 資產分析，資產報表
exl-id: 67be0ae6-5939-40fe-bf8a-b8a2c2f68f15
source-git-commit: c07467feb96c25a4bac1916f88f04fdb37979ee1
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 6%

---

# 設定資產分析{#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] 從中擷取協力廠商網站使用之數位資產的使用資料 [!DNL Adobe Analytics]。若要讓「資產前瞻分析」擷取此資料並產生前瞻分析，請先設定功能以與[!DNL Adobe Analytics]整合。 若要使用此功能，請個別購買[!DNL Adobe Analytics]授權。 [!DNL Managed Services]的客戶會收到與[!DNL Experience Manager]搭售的[!DNL Analytics]授權。 請參閱[Managed Services產品說明](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)。

>[!NOTE]
>
>只有影像才支援並提供見解。

1. 在[!DNL Experience Manager]中，按一下&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 資產]**。

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. 按一下「 **[!UICONTROL 前瞻分析設定]** 」資訊卡。
1. 在精靈中，選取資料中心並提供您的認證，包括您的組織名稱、使用者名稱和共用密碼。

   ![配置Adobe Analytics的Experience Manager資產見解](assets/insights_config2.png)

   *圖：在中 [!DNL Adobe Analytics] 設定資產見解 [!DNL Experience Manager]。*

1. 按一下&#x200B;**[!UICONTROL Authenticate]**。
1. 在[!DNL Experience Manager]驗證您的認證後，從&#x200B;**[!UICONTROL 報表套裝]**&#x200B;清單中，選擇[!DNL Adobe Analytics]報表套裝，讓資產前瞻分析擷取資料。 按一下&#x200B;**[!UICONTROL 「新增」]**。
1. 在[!DNL Experience Manager]設定報表套裝後，按一下&#x200B;**[!UICONTROL Done]**。

## 頁面追蹤器{#page-tracker}

設定[!DNL Adobe Analytics]帳戶後，會為您產生頁面追蹤器代碼。 若要啟用「資產前瞻分析」來追蹤第三方網站中使用的[!DNL Experience Manager]資產，請在網站程式碼中加入頁面追蹤器程式碼。 使用[!DNL Experience Manager Assets]中的[!UICONTROL 頁面追蹤器]公用程式來產生頁面追蹤器程式碼。 如需如何在協力廠商網頁中加入頁面追蹤器代碼的詳細資訊，請參閱[使用頁面追蹤器並在網頁中內嵌代碼](/help/assets/use-page-tracker.md)。

1. 在[!DNL Experience Manager]中，按一下&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 資產]**。

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. 在導覽頁 **[!UICONTROL 面中]** ，按一下 **** 前瞻分析頁面追蹤器卡片。
1. 按一下&#x200B;**[!UICONTROL 下載]**&#x200B;以下載頁面追蹤器代碼。
