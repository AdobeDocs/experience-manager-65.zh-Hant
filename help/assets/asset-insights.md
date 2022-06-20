---
title: 資產透視
description: 瞭解Assets Insights功能如何讓您跟蹤在第三方網站、市場營銷活動和Adobe的創造性解決方案中使用的影像的用戶評級和使用統計資訊。
contentOwner: AG
role: User, Admin
feature: Asset Insights,Asset Reports
exl-id: 0130ac40-a72b-4caf-a10f-3c7d76eaa1e6
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 7%

---

# 資產透視 {#asset-insights}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/assets-insights.html?lang=en) |
| AEM 6.5 | 本文 |
| AEM 6.4 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-64/assets/managing/touch-ui-configuring-asset-insights.html?lang=en) |

Assets Insights功能使您能夠跟蹤用戶評級和在第三方網站、市場營銷活動和Adobe的創意解決方案中使用的影像的使用統計。 它有助於人們瞭解他們的表現和受歡迎程度。

[!DNL Assets] Insights可捕獲用戶活動詳細資訊，如對影像進行分級、按一下和印象的次數（將影像載入到網站上的次數）。 它根據這些統計資料給影像分配分數。 您可以使用分數和業績統計資訊來選擇要包含在目錄、市場營銷活動等中的流行影像。 您甚至可以根據這些統計資料制定存檔和許可證續訂策略。

對於 [!DNL Assets] 要從網站捕獲影像的使用統計資訊的見解，必須在網站代碼中包含影像的嵌入代碼。

要讓Assets Insights顯示資產的使用情況統計資訊，請首先配置功能以從Adobe Analytics獲取報告資料。 有關詳細資訊，請參閱 [配置資產透視](/help/assets/configure-asset-insights.md)。 要在內部安裝中使用此功能，請購買 [!DNL Adobe Analytics] 單獨許可。 客戶 [!DNL Managed Services] 接收 [!DNL Analytics] 與 [!DNL Experience Manager]。 請參閱 [Managed Services產品說明](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)。

>[!NOTE]
>
>只支援和提供影像的見解。

## 查看影像的統計資訊 {#viewing-statistics-for-an-image}

您可以從元資料頁面查看Assets Insights得分。

1. 從 [!DNL Assets] 用戶介面(UI)，選擇影像，然後按一下 **[!UICONTROL 屬性]** 的子菜單。
1. 在「屬性」頁中，按一下 **[!UICONTROL 洞察力]** 頁籤。
1. 複查中資產的使用詳細資訊 **[!UICONTROL 洞察力]** 頁籤。 的 **[!UICONTROL 得分]** 節描述資產的資產使用總量和效能分類。

   使用情況分數描述了資產在各種解決方案中使用的次數。

   的 **[!UICONTROL 印象]** score是在網站上載入資產的次數。 顯示在下面的編號 **[!UICONTROL 按一下]** 是按一下資產的次數。

1. 查看 **[!UICONTROL 使用情況統計]** 瞭解資產是哪些實體的一部分，以及最近使用了哪些創造性解決方案。 使用率越高，該資產在用戶中受歡迎的可能性就越大。 使用資料顯示在以下標題下：

   * **資產**:資產作為集合或複合資產一部分的次數
   * **Web和移動**:資產加入網站和應用的次數
   * **社會**:在解決方案(如Adobe Social和Adobe Campaign)中使用該資產的次數
   * **電子郵件**:資產在電子郵件市場活動中使用的次數

   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >由於Assets Insights功能通常定期從Adobe Analytics獲取解決方案資料，因此解決方案部分可能不顯示最新資料。 顯示資料的時段取決於Assets Insights為檢索分析資料而運行的提取操作的計畫。

1. 要以圖形方式查看某個時段內資產的效能統計資訊，請在「效能統計資訊」部分中 **[!UICONTROL 選擇該時段]** 。詳細資訊 (包括點按次數和印象) 會顯示為圖形的趨勢線。

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >與「解決方案」部分中的資料不同，「效能統計」部分顯示最新資料。

1. 要獲取包含在網站中的資產的嵌入代碼以獲取效能資料，請按一下 **[!UICONTROL 獲取嵌入代碼]** 資產縮覽圖下方。 有關如何在第三方網頁中包含嵌入代碼的詳細資訊，請參閱 [使用頁面跟蹤器並在網頁中嵌入代碼](/help/assets/use-page-tracker.md)。

   ![chlimage_1-98](assets/chlimage_1-303.png)

## 查看影像的聚合統計資訊 {#viewing-aggregate-statistics-for-images}

您可以使用前瞻分析檢視同時檢視資料夾內所有資產 **[!UICONTROL 的分數]**。

1. 在 [!DNL Assets] 用戶介面，導航到包含要查看其透視的資產的資料夾。
1. 從工具欄中按一下「佈局」，然後選擇 **[!UICONTROL 透視視圖]**。
1. 該頁顯示資產的使用分數。 比較各種資產的評級並得出見解。

## 計畫後台作業 {#scheduling-background-job}

Assets Insights定期從Adobe Analytics報告套件中獲取資產的使用資料。 預設情況下，Assets Insights每24小時運行一次後台作業，在凌晨2點運行一次獲取資料。 但是，可以通過配置 **[!UICONTROL Adobe CQDAM資產效能報告同步作業]** 從Web控制台獲取服務。

1. 按一下 [!DNL Experience Manager] 徽標，然後轉到 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。
1. 開啟 **[!UICONTROL Adobe CQDAM資產效能報告同步作業]** 服務配置。

   ![chlimage_1-99](assets/chlimage_1-304.png)

1. 在屬性調度器表達式中指定作業所需的調度器頻率和開始時間。 儲存變更。
