---
title: Assets Insights
description: 了解「資產前瞻分析」功能如何讓您追蹤第三方網站、行銷活動和Adobe創意解決方案中使用的影像的使用者評等和使用統計資料。
contentOwner: AG
role: User, Admin
feature: Asset Insights,Asset Reports
exl-id: 0130ac40-a72b-4caf-a10f-3c7d76eaa1e6
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 7%

---

# Assets Insights {#asset-insights}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/assets-insights.html?lang=en) |
| AEM 6.5 | 本文 |

「資產前瞻分析」功能可讓您追蹤使用者評等，以及第三方網站、行銷活動和Adobe創意解決方案所使用影像的使用統計資料。 有助於深入了解其效能和受歡迎程度。

[!DNL Assets] 前瞻分析會擷取使用者活動詳細資料，例如影像的分級、點按次數和曝光次數（影像在網站上載入的次數）。 它會根據這些統計資料來指派分數給影像。 您可以使用分數和效能統計資料來選取要納入目錄、行銷活動等的熱門影像。 您甚至可以根據這些統計資料制定存檔和許可證更新策略。

針對 [!DNL Assets] 用於從網站擷取影像使用統計資料的前瞻分析，您必須在網站程式碼中包含影像的內嵌程式碼。

若要讓Assets Insights顯示資產的使用量統計資料，請先設定從Adobe Analytics擷取報表資料的功能。 如需詳細資訊，請參閱 [設定Assets Insights](/help/assets/configure-asset-insights.md). 若要在內部部署中使用此功能，請購買 [!DNL Adobe Analytics] 單獨授權。 客戶 [!DNL Managed Services] 接收 [!DNL Analytics] 隨附 [!DNL Experience Manager]. 請參閱 [Managed Services產品說明](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html).

>[!NOTE]
>
>僅支援並提供影像見解。

## 查看影像的統計資訊 {#viewing-statistics-for-an-image}

您可以從中繼資料頁面檢視「資產前瞻分析」分數。

1. 從 [!DNL Assets] 使用者介面(UI)，選取影像，然後按一下 **[!UICONTROL 屬性]** 的上界。
1. 在「屬性」頁面中，按一下 **[!UICONTROL 前瞻分析]** 標籤。
1. 檢閱 **[!UICONTROL 前瞻分析]** 標籤。 此 **[!UICONTROL 分數]** 一節說明資產的資產使用總量和效能分數。

   使用分數說明資產在各種解決方案中的使用次數。

   此 **[!UICONTROL 曝光數]** score是網站上載入資產的次數。 顯示在 **[!UICONTROL 點按次數]** 是資產的點按次數。

1. 檢閱 **[!UICONTROL 使用情況統計資料]** 區段來了解資產所屬的實體，以及最近使用哪些創意解決方案。 使用率越高，資產在使用者中受歡迎的機率就越大。 使用資料顯示在以下標題下：

   * **資產**:資產屬於集合或複合資產的次數
   * **網頁與行動**:資產加入網站和應用程式的次數
   * **社交**:資產用於解決方案(例如Adobe Social和Adobe Campaign)的次數
   * **電子郵件**:資產用於電子郵件促銷活動的次數

   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >由於「資產前瞻分析」功能通常會定期從Adobe Analytics擷取解決方案資料，因此「解決方案」區段可能不會顯示最新資料。 顯示資料的時段取決於Assets Insights執行擷取Analytics資料的擷取作業排程。

1. 要以圖形方式查看某個時段內資產的效能統計資訊，請在「效能統計資訊」部分中 **[!UICONTROL 選擇該時段]** 。詳細資訊 (包括點按次數和印象) 會顯示為圖形的趨勢線。

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >與「解決方案」區段中的資料不同，「效能統計資料」區段會顯示最新的資料。

1. 若要取得您納入網站之資產的內嵌程式碼，以取得效能資料，請按一下 **[!UICONTROL 取得內嵌程式碼]** 在資產縮圖下方。 如需如何將內嵌程式碼包含在協力廠商網頁的詳細資訊，請參閱 [使用頁面追蹤器並在網頁中內嵌程式碼](/help/assets/use-page-tracker.md).

   ![chlimage_1-98](assets/chlimage_1-303.png)

## 查看映像的聚合統計資訊 {#viewing-aggregate-statistics-for-images}

您可以使用前瞻分析檢視同時檢視資料夾內所有資產 **[!UICONTROL 的分數]**。

1. 在 [!DNL Assets] 使用者介面，導覽至包含您要檢視前瞻分析之資產的資料夾。
1. 按一下工具列中的「配置」，然後選擇 **[!UICONTROL 前瞻分析檢視]**.
1. 頁面會顯示資產的使用分數。 比較各種資產的評等並得出深入分析。

## 排程背景工作 {#scheduling-background-job}

Assets Insights會定期從Adobe Analytics報表套裝擷取資產的使用資料。 根據預設，Assets Insights會每24小時在凌晨2:00執行背景工作，以擷取資料。 不過，您可以借由設定 **[!UICONTROL Adobe CQ DAM資產效能報表同步作業]** 服務。

1. 按一下 [!DNL Experience Manager] 標誌，然後 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web主控台]**.
1. 開啟 **[!UICONTROL Adobe CQ DAM資產效能報表同步作業]** 服務設定。

   ![chlimage_1-99](assets/chlimage_1-304.png)

1. 在屬性調度器表達式中指定作業所需的調度器頻率和開始時間。 儲存變更。
