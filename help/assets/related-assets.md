---
title: 相關資產
description: 了解如何關聯共用某些共同屬性的數位資產。 也可在數位資產之間建立來源衍生的關係。
contentOwner: AG
role: Business Practitioner
feature: 協作，資產管理
exl-id: ddb69727-74a0-4a4d-a14e-7d3bb5ceea2a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# 相關資產{#related-assets}

[!DNL Adobe Experience Manager Assets] 可讓您使用「相關資產」功能，根據組織的需求手動關聯資產。例如，您可以將授權檔案與類似主題上的資產或影像/視訊產生關聯。 您可以將共用特定共同屬性的資產關聯。 您也可以使用功能建立資產之間的來源/衍生關係。 例如，如果PDF檔案是從INDD檔案生成的，則可將PDF檔案與其源INDD檔案相關。

使用此功能，您可以靈活地與供應商或代理商共用低解析度的PDF檔案或JPG檔案，並且僅應要求提供高解析度的INDD檔案。

>[!NOTE]
>
>只有對資產具有編輯權限的使用者才能與資產產生關聯及解除關聯。

## 相關資產{#relating-assets}

1. 從[!DNL Experience Manager]介面，開啟您要關聯之資產的&#x200B;**[!UICONTROL 屬性]**&#x200B;頁面。

   ![開啟資產的「屬性」頁面以與資產產生關聯](assets/asset-properties-relate-assets.png)

   *圖： [!DNL Assets]  屬性」頁面，以了解相關資產。*

   或者，從清單檢視中選取資產。

   ![chlimage_1-273](assets/chlimage_1-273.png)

   您也可以從集合中選取資產。

   ![chlimage_1-274](assets/chlimage_1-274.png)

1. 若要將另一個資產與您選取的資產產生關聯，請從工具列按一下「**[!UICONTROL 關聯]** ![相關資產](assets/do-not-localize/link-relate.png)」。
1. 執行下列任一操作：

   * 要關聯資產的源檔案，請從清單中選擇&#x200B;**[!UICONTROL 源]**。
   * 要關聯派生檔案，請從清單中選擇&#x200B;**[!UICONTROL Derived]**。
   * 若要建立資產之間的雙向關係，請從清單中選取&#x200B;**[!UICONTROL Others]**。

1. 從&#x200B;**[!UICONTROL 選取資產]**&#x200B;畫面，導覽至您要關聯的資產位置，然後選取它。

   ![chlimage_1-277](assets/chlimage_1-277.png)

1. 按一下&#x200B;**[!UICONTROL 確認]**。
1. 按一下&#x200B;**[!UICONTROL OK]**&#x200B;以關閉對話方塊。 根據您在步驟3中的關係選擇，相關資產會列在&#x200B;**[!UICONTROL Related]**&#x200B;區段中的適當類別下。 例如，如果您相關的資產是當前資產的源檔案，則它會列在&#x200B;**[!UICONTROL Source]**&#x200B;下。

   ![chlimage_1-278](assets/chlimage_1-278.png)

1. 若要取消資產的關聯，請從工具列按一下「取消資產關聯」 **[!UICONTROL 「取消資產關聯」]** ![取消資產關聯](assets/do-not-localize/link-unrelate-icon.png)。

1. 從&#x200B;**[!UICONTROL 移除關係]**&#x200B;對話方塊中，選取您要取消關聯的資產，然後按一下&#x200B;**[!UICONTROL 取消關聯]**。

   ![chlimage_1-280](assets/chlimage_1-280.png)

1. 按一下&#x200B;**[!UICONTROL OK]**&#x200B;以關閉對話方塊。 您移除關係的資產會從&#x200B;**[!UICONTROL Related]**&#x200B;區段下的相關資產清單中刪除。

## 轉換相關資產{#translating-related-assets}

使用相關資產功能建立資產之間的來源/衍生關係在翻譯工作流程中也很實用。 在衍生資產上執行翻譯工作流程時，[!DNL Experience Manager Assets]會自動擷取來源檔案所參考的任何資產，並加入以進行翻譯。 這樣，源資產引用的資產與源資產和派生資產一起翻譯。 例如，假設您的英文副本包含衍生資產及其來源檔案，如所示。

![chlimage_1-281](assets/chlimage_1-281.png)

如果來源檔案與其他資產相關，[!DNL Experience Manager Assets]會擷取參考的資產並加以轉譯。

![「資產屬性」頁面顯示要包括在翻譯中的相關資產的來源檔案](assets/asset-properties-source-asset.png)

*圖：資產之來源資產，以包括於換算。*

1. 依照[建立新翻譯專案](translation-projects.md#create-a-new-translation-project)中的步驟，將來源資料夾中的資產翻譯為目標語言。 例如，在此案例中，將資產翻譯為法文。

1. 從[!UICONTROL 項目]頁開啟翻譯資料夾。

1. 按一下專案圖磚，開啟「詳細資訊」頁面。

   ![chlimage_1-284](assets/chlimage_1-284.png)

1. 按一下翻譯工作卡下方的點以檢視翻譯狀態。

   ![chlimage_1-285](assets/chlimage_1-285.png)

1. 選取資產，然後按一下工具列中的「在資產中顯現&#x200B;****」以檢視資產的轉譯狀態。

   ![chlimage_1-286](assets/chlimage_1-286.png)

1. 要驗證是否已翻譯與源相關的資產，請按一下源資產。

1. 選取與來源相關的資產，然後按一下「**[!UICONTROL 在資產中顯現」]**。 隨即顯示翻譯的相關資產。
