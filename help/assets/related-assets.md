---
title: 相關資產
description: 瞭解如何建立共用一些共同屬性的數位資產之間的關聯。 也可建立數位資產之間的來源衍生關係。
contentOwner: AG
role: 業務從業人員
feature: 協作，資產管理
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---


# 相關資產{#related-assets}

[!DNL Adobe Experience Manager Assets] 可讓您使用相關資產功能，根據組織的需求手動建立資產關聯。例如，您可以將授權檔案與類似主題上的資產或影像／視訊建立關聯。 您可以建立與共用特定共同屬性的資產關聯。 您也可以使用此功能來建立資產間的來源／衍生關係。 例如，如果您有PDF檔案是從INDD檔案產生，則可將PDF檔案與其來源INDD檔案建立關聯。

使用此功能，您就可以彈性地與廠商或機構共用低解析度的PDF檔案或JPG檔案，並且只有在要求時才提供高解析度的INDD檔案。

>[!NOTE]
>
>只有對資產具有編輯權限的使用者可以關聯和取消關聯資產。

## 關聯資產{#relating-assets}

1. 在[!DNL Experience Manager]介面中，開啟您要建立關聯之資產的&#x200B;**[!UICONTROL 屬性]**&#x200B;頁面。

   ![開啟資產的「屬性」頁面，以建立資產的關聯](assets/asset-properties-relate-assets.png)

   *圖： [!DNL Assets] [!UICONTROL 「屬] 性」頁，以關聯資產。*

   或者，從清單檢視中選取資產。

   ![chlimage_1-273](assets/chlimage_1-273.png)

   您也可以從系列中選取資產。

   ![chlimage_1-274](assets/chlimage_1-274.png)

1. 若要將其他資產與您選取的資產建立關聯，請按一下工具列中的「建立關聯資產」。****![](assets/do-not-localize/link-relate.png)
1. 執行下列任一項作業：

   * 要關聯資產的源檔案，請從清單中選擇&#x200B;**[!UICONTROL 源]**。
   * 要關聯派生檔案，請從清單中選擇&#x200B;**[!UICONTROL Derived]**。
   * 若要在資產之間建立雙向關係，請從清單中選取&#x200B;**[!UICONTROL Others]**。

1. 從&#x200B;**[!UICONTROL 選擇資產]**&#x200B;畫面，瀏覽至您要建立關聯的資產所在位置，然後選擇它。

   ![chlimage_1-277](assets/chlimage_1-277.png)

1. 按一下&#x200B;**[!UICONTROL 確認]**。
1. 按一下&#x200B;**[!UICONTROL 確定]**&#x200B;關閉對話框。 根據您在步驟3中選擇的關係，相關資產會列在&#x200B;**[!UICONTROL Related]**&#x200B;一節中適當類別下。 例如，如果您相關的資產是目前資產的來源檔案，則會列在&#x200B;**[!UICONTROL Source]**&#x200B;下。

   ![chlimage_1-278](assets/chlimage_1-278.png)

1. 若要解除資產關聯，請從工具列按一下「解除關聯&#x200B;****![解除關聯資產](assets/do-not-localize/link-unrelate-icon.png)」。

1. 從&#x200B;**[!UICONTROL 移除關係]**&#x200B;對話方塊中選取您要解除關聯的資產，然後按一下&#x200B;**[!UICONTROL 解除關聯]**。

   ![chlimage_1-280](assets/chlimage_1-280.png)

1. 按一下&#x200B;**[!UICONTROL 確定]**&#x200B;關閉對話框。 您移除關係的資產會從&#x200B;**[!UICONTROL Related]**&#x200B;區段下的相關資產清單中刪除。

## 翻譯相關資產{#translating-related-assets}

使用相關資產功能建立資產間的來源／衍生關係也有助於翻譯工作流程。 在派生資產上運行翻譯工作流時，[!DNL Experience Manager Assets]會自動提取源檔案引用的任何資產並包括其以供翻譯。 這樣，源資產引用的資產與源資產和衍生資產一起折算。 例如，假設您的英文版副本包含衍生資產及其來源檔案，如所示。

![chlimage_1-281](assets/chlimage_1-281.png)

如果源檔案與另一個資產相關，[!DNL Experience Manager Assets]將讀取引用的資產並包括該資產以供翻譯。

![「資產屬性」頁顯示要包括在轉換中的相關資產的源檔案](assets/asset-properties-source-asset.png)

*圖：相關資產的來源資產，以便進行折算。*

1. 按照[建立新翻譯項目](translation-projects.md#create-a-new-translation-project)中的步驟，將源資料夾中的資產翻譯為目標語言。 例如，在此例中，請將您的資產翻譯為法文。

1. 在[!UICONTROL Projects]頁面中，開啟翻譯資料夾。

1. 按一下專案圖格以開啟詳細資訊頁面。

   ![chlimage_1-284](assets/chlimage_1-284.png)

1. 按一下翻譯工作卡下方的省略號可查看翻譯狀態。

   ![chlimage_1-285](assets/chlimage_1-285.png)

1. 選擇資產，然後從工具列按一下「在資產中顯現」**[!UICONTROL ，以檢視資產的轉換狀態。]**

   ![chlimage_1-286](assets/chlimage_1-286.png)

1. 若要確認是否已轉換與來源相關的資產，請按一下來源資產。

1. 選取與來源相關的資產，然後按一下「在資產中顯現」。 ****&#x200B;會顯示已轉換的相關資產。
