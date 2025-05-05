---
title: 相關資產
description: 瞭解如何關聯共用某些通用屬性的數位資產。 也可在數位資產之間建立來源衍生的關係。
contentOwner: AG
role: User
feature: Collaboration,Asset Management
exl-id: ddb69727-74a0-4a4d-a14e-7d3bb5ceea2a
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 3%

---

# 相關資產 {#related-assets}

[!DNL Adobe Experience Manager Assets]可讓您使用相關資產功能，根據貴組織的需求手動建立資產關聯。 例如，您可以將授權檔案與類似主題的資產或影像/影片建立關聯。 您可以將共用特定通用屬性的資產建立關聯。 您也可以使用功能來建立資產之間的來源/衍生關係。 例如，如果您有一個從INDD檔案產生的PDF檔案，則可以將PDF檔案與其來源INDD檔案相關聯。

使用此功能，您可以彈性地與廠商或機構共用低解析度的PDF檔案或JPG檔案，並僅在提出要求時提供高解析度的INDD檔案。

>[!NOTE]
>
>只有對資產具有編輯許可權的使用者才能建立資產的相關性和取消資產的相關性。

## 相關資產 {#relating-assets}

1. 從[!DNL Experience Manager]介面，開啟要建立關聯之資產的&#x200B;**[!UICONTROL 屬性]**&#x200B;頁面。

   ![開啟資產的屬性頁面以關聯資產](assets/asset-properties-relate-assets.png)

   *圖： [!DNL Assets] [!UICONTROL 屬性]頁面以關聯資產。*

   或者，從清單檢視中選取資產。

   ![chlimage_1-273](assets/chlimage_1-273.png)

   您也可以從集合中選取資產。

   ![chlimage_1-274](assets/chlimage_1-274.png)

1. 若要將另一個資產與您選取的資產建立關聯，請從工具列按一下&#x200B;**[!UICONTROL 關聯]** ![關聯資產](assets/do-not-localize/link-relate.png)。
1. 執行下列任一項作業：

   * 若要關聯資產的來源檔案，請從清單中選取&#x200B;**[!UICONTROL Source]**。
   * 若要關聯衍生檔案，請從清單中選取&#x200B;**[!UICONTROL 衍生]**。
   * 若要在資產之間建立雙向關係，請從清單中選取&#x200B;**[!UICONTROL 其他]**。

1. 從&#x200B;**[!UICONTROL 選取資產]**&#x200B;畫面中，導覽至您要建立關聯的資產位置，然後選取該資產。

   ![chlimage_1-277](assets/chlimage_1-277.png)

1. 按一下&#x200B;**[!UICONTROL 確認]**。
1. 按一下&#x200B;**[!UICONTROL 確定]**&#x200B;關閉對話方塊。 根據您在步驟3中選擇的關係，相關資產會列在&#x200B;**[!UICONTROL 相關]**&#x200B;區段的適當類別下。 例如，如果您相關的資產是目前資產的來源檔案，則會列在&#x200B;**[!UICONTROL Source]**&#x200B;下。

   ![chlimage_1-278](assets/chlimage_1-278.png)

1. 若要取消關聯資產，請從工具列按一下&#x200B;**[!UICONTROL 取消關聯]** ![取消關聯資產](assets/do-not-localize/link-unrelate-icon.png)。

1. 從&#x200B;**[!UICONTROL 移除關係]**&#x200B;對話方塊中選取您要取消關聯的資產，然後按一下&#x200B;**[!UICONTROL 取消關聯]**。

   ![chlimage_1-280](assets/chlimage_1-280.png)

1. 按一下&#x200B;**[!UICONTROL 確定]**&#x200B;關閉對話方塊。 您移除關係的資產會從&#x200B;**[!UICONTROL 相關]**&#x200B;區段下的相關資產清單中刪除。

## 翻譯相關資產 {#translating-related-assets}

使用相關資產功能在資產之間建立來源/衍生關係，在翻譯工作流程中也很有幫助。 當您在衍生資產上執行翻譯工作流程時，[!DNL Experience Manager Assets]會自動擷取來源檔案參考的任何資產，並將其納入以進行翻譯。 如此一來，來源資產所參考的資產會與來源和衍生資產一併轉譯。 例如，假設您的英文副本包含衍生資產及其來源檔案（如圖所示）。

![chlimage_1-281](assets/chlimage_1-281.png)

如果來源檔案與另一個資產相關，[!DNL Experience Manager Assets]會擷取參照的資產並包含它以進行翻譯。

![資產屬性頁面會顯示要納入翻譯之相關資產的來源檔案](assets/asset-properties-source-asset.png)

*圖：要納入翻譯之相關資產的Source資產。*

1. 依照[建立翻譯專案](translation-projects.md#create-a-new-translation-project)中的步驟，將來源資料夾中的資產翻譯成目標語言。 例如，在此案例中，請將您的資產翻譯為法文。

1. 從[!UICONTROL 專案]頁面，開啟翻譯資料夾。

1. 按一下專案拼貼以開啟詳細資訊頁面。

   ![chlimage_1-284](assets/chlimage_1-284.png)

1. 按一下翻譯工作卡片下方的省略符號以檢視翻譯狀態。

   ![chlimage_1-285](assets/chlimage_1-285.png)

1. 選取資產，然後從工具列按一下&#x200B;**[!UICONTROL 在Assets中顯示]**&#x200B;以檢視資產的翻譯狀態。

   ![chlimage_1-286](assets/chlimage_1-286.png)

1. 若要驗證與來源相關的資產是否已翻譯，請按一下來源資產。

1. 選取與來源相關的資產，然後按一下[在Assets中顯示] **&#x200B;**。 隨即顯示翻譯的相關資產。
