---
title: 準備要翻譯的資產
description: 建立語言根資料夾以準備要翻譯的資產以支援多語言資產。
contentOwner: AG
role: User, Admin
feature: Projects
exl-id: eee768e3-3eb4-46fa-b9ae-9ef8764a3a94
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 1%

---

# 準備要翻譯的資產 {#preparing-assets-for-translation}

多語言資產是指具有多語言二進位檔案、中繼資料和標籤的資產。 一般而言，資產的二進位檔案、中繼資料和標籤會以一種語言存在，然後會翻譯成其他語言以用於多語言專案。

在[!DNL Adobe Experience Manager Assets]中，多語言資產包含在資料夾中，其中每個資料夾都包含不同語言的資產。

每個語言資料夾都稱為語言副本。 語言副本的根資料夾（稱為語言根）可識別語言副本中內容的語言。 例如，*/content/dam/it*&#x200B;是義大利文語言副本的義大利文語言根。 語言復本必須使用[正確設定的語言根](preparing-assets-for-translation.md#creating-a-language-root)，以便在翻譯來源資產時鎖定正確的語言。

您最初新增資產的語言副本是主要語言。 主要語言是翻譯成其他語言的來源。 範例資料夾階層包含數個語言根：

```shell
/content
    /- dam
        |- en
        |- fr
        |- de
        |- es
        |- it
        |- ja
        |- zh
```

執行以下步驟來準備要翻譯的資產：

1. 建立主要語言的語言根。 例如，範例資料夾階層中英文副本的語言根為`/content/dam/en`。 請確定已根據[建立語言根](preparing-assets-for-translation.md#creating-a-language-root)中的資訊正確設定語言根。

1. 將資產新增至您的主要語言。
1. 針對您需要語言副本的每個目標語言建立語言根。

## 建立語言根 {#creating-a-language-root}

若要建立語言根，請建立資料夾並使用ISO語言代碼作為Name屬性的值。 建立語言根後，您可以在語言根內的任何層級建立語言副本。

例如，範例階層的義大利文語言副本的根頁面以`it`作為Name屬性。 Name屬性會用作存放庫中資產節點的名稱，從而決定資產的路徑。(`https://[aem_server]:[port]/assets.html/content/dam/it/`)。

1. 從[!DNL Assets]主控台，按一下&#x200B;**[!UICONTROL 建立]**，然後從功能表選擇&#x200B;**[!UICONTROL 資料夾]**。

   ![建立資料夾](assets/Create-folder.png)

1. 在&#x200B;**[!UICONTROL 名稱]**&#x200B;欄位中，以`<language-code>`的格式輸入國家/地區代碼。

   ![在資料夾中新增語言代碼](assets/Add-language-code-in-folder.png)

1. 按一下「**[!UICONTROL 建立]**」。語言根目錄是在[!DNL Assets]主控台中建立。

## 檢視語言根 {#viewing-language-roots}

[!DNL Experience Manager]介面提供&#x200B;**[!UICONTROL 參考]**&#x200B;面板，顯示已在[!DNL Assets]中建立的語言根清單。

1. 在[!DNL Assets]主控台中，選取您要建立語言副本的主要語言。
1. 從左側邊欄中，選取&#x200B;**[!UICONTROL 參考]**&#x200B;選項以開啟[!UICONTROL 參考]窗格。

   ![chlimage_1-122](assets/chlimage_1-122.png)

1. 在[參考]窗格中，按一下[語言復本]。**** [!UICONTROL 語言副本]面板會顯示資產的語言副本。

   ![語言副本](assets/lang-copy2.png)
