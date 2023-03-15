---
title: 相關資產
description: 了解如何關聯共用某些共同屬性的數位資產。 也可在數位資產之間建立來源衍生的關係。
contentOwner: AG
role: User
feature: Collaboration,Asset Management
exl-id: ddb69727-74a0-4a4d-a14e-7d3bb5ceea2a
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 2%

---

# 相關資產 {#related-assets}

[!DNL Adobe Experience Manager Assets] 可讓您使用「相關資產」功能，根據組織的需求手動關聯資產。 例如，您可以將授權檔案與類似主題上的資產或影像/視訊產生關聯。 您可以將共用特定共同屬性的資產關聯。 您也可以使用功能建立資產之間的來源/衍生關係。 例如，如果您有一個從INDD檔案生成的PDF檔案，則可將PDF檔案與其源INDD檔案相關。

使用此功能，您可以靈活地與供應商或代理商共用低解析度的PDF檔案或JPG檔案，並使高解析度的INDD檔案僅可應要求提供。

>[!NOTE]
>
>只有對資產具有編輯權限的使用者才能與資產產生關聯及解除關聯。

## 相關資產 {#relating-assets}

1. 從 [!DNL Experience Manager] 介面，開啟 **[!UICONTROL 屬性]** 頁面，以查看您要關聯的資產。

   ![開啟資產的「屬性」頁面以與資產產生關聯](assets/asset-properties-relate-assets.png)

   *圖： [!DNL Assets] [!UICONTROL 屬性] 頁面，與資產相關。*

   或者，從清單檢視中選取資產。

   ![chlimage_1-273](assets/chlimage_1-273.png)

   您也可以從集合中選取資產。

   ![chlimage_1-274](assets/chlimage_1-274.png)

1. 若要將另一個資產與您選取的資產產生關聯，請按一下 **[!UICONTROL 相關]** ![相關資產](assets/do-not-localize/link-relate.png) 的上界。
1. 執行下列任一項作業：

   * 要關聯資產的源檔案，請選擇 **[!UICONTROL 來源]** 從清單中。
   * 要關聯派生檔案，請選擇 **[!UICONTROL 衍生]** 從清單中。
   * 若要在資產之間建立雙向關係，請選取 **[!UICONTROL 其他]** 從清單中。

1. 從 **[!UICONTROL 選取資產]** 畫面中，導覽至您要關聯的資產位置，然後選取它。

   ![chlimage_1-277](assets/chlimage_1-277.png)

1. 按一下 **[!UICONTROL 確認]**.
1. 按一下 **[!UICONTROL 確定]** 以關閉對話方塊。 根據您在步驟3中選擇的關係，相關資產會列在 **[!UICONTROL 相關]** 區段。 例如，如果您相關的資產是目前資產的來源檔案，則會列在 **[!UICONTROL 來源]**.

   ![chlimage_1-278](assets/chlimage_1-278.png)

1. 若要取消資產的關聯，請按一下 **[!UICONTROL 不相關]** ![相關資產](assets/do-not-localize/link-unrelate-icon.png) 的上界。

1. 從 **[!UICONTROL 刪除關係]** 對話框，然後按一下 **[!UICONTROL 不相關]**.

   ![chlimage_1-280](assets/chlimage_1-280.png)

1. 按一下 **[!UICONTROL 確定]** 以關閉對話方塊。 您移除關係的資產會從 **[!UICONTROL 相關]** 區段。

## 換算相關資產 {#translating-related-assets}

使用相關資產功能建立資產之間的來源/衍生關係在翻譯工作流程中也很實用。 對衍生資產執行翻譯工作流程時， [!DNL Experience Manager Assets] 自動擷取來源檔案所參考的任何資產，並加以轉譯。 這樣，源資產引用的資產與源資產和派生資產一起翻譯。 例如，假設您的英文副本包含衍生資產及其來源檔案，如所示。

![chlimage_1-281](assets/chlimage_1-281.png)

如果源檔案與另一個資產相關， [!DNL Experience Manager Assets] 擷取參考的資產，並加入以進行翻譯。

![「資產屬性」頁面顯示要包括在翻譯中的相關資產的來源檔案](assets/asset-properties-source-asset.png)

*圖：資產之來源資產，以包括於換算。*

1. 依照 [建立新的翻譯專案](translation-projects.md#create-a-new-translation-project). 例如，在此案例中，將資產翻譯為法文。

1. 從 [!UICONTROL 專案] 頁，開啟翻譯資料夾。

1. 按一下專案圖磚，開啟詳細資訊頁面。

   ![chlimage_1-284](assets/chlimage_1-284.png)

1. 按一下翻譯工作卡下方的點以檢視翻譯狀態。

   ![chlimage_1-285](assets/chlimage_1-285.png)

1. 選取資產，然後按一下 **[!UICONTROL 在資產中顯示]** 從工具列檢視資產的翻譯狀態。

   ![chlimage_1-286](assets/chlimage_1-286.png)

1. 要驗證是否已翻譯與源相關的資產，請按一下源資產。

1. 選取與來源相關的資產，然後按一下 **[!UICONTROL 在資產中顯示]**. 隨即顯示翻譯的相關資產。
