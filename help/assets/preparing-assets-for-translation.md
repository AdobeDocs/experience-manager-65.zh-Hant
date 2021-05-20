---
title: 準備翻譯資產
description: 建立語言根資料夾以準備要翻譯的資產，以支援多語言資產。
contentOwner: AG
role: Business Practitioner, Administrator
feature: 專案
exl-id: eee768e3-3eb4-46fa-b9ae-9ef8764a3a94
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---

# 準備翻譯資產{#preparing-assets-for-translation}

多語言資產是指具有多種語言的二進位檔、中繼資料和標籤的資產。 資產的二進位檔、中繼資料和標籤通常以一種語言存在，然後轉譯為其他語言，以用於多語言專案。

在[!DNL Adobe Experience Manager Assets]中，多語言資產包含在資料夾中，其中每個資料夾都包含不同語言的資產。

每個語言資料夾都稱為語言副本。 語言副本的根資料夾（稱為語言根）標識語言副本中內容的語言。 例如， */content/dam/it*&#x200B;是義大利文語言副本的義大利文根。 語言副本必須使用[正確配置的語言根](preparing-assets-for-translation.md#creating-a-language-root)，以便在執行源資產翻譯時定位正確的語言。

您最初新增資產的語言副本是語言主要。 語言主要是翻譯成其他語言的源。 範例資料夾階層包含數種語言根：

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

執行下列步驟準備翻譯資產：

1. 建立語言主要的語言根。 例如，範例資料夾階層中英文副本的語言根目錄為`/content/dam/en`。 確保根據[建立語言根](preparing-assets-for-translation.md#creating-a-language-root)中的資訊正確配置語言根。

1. 將資產新增至您的語言主要版本。
1. 建立您需要語言副本的每種目標語言的語言根。

## 建立語言根{#creating-a-language-root}

要建立語言根，請建立資料夾並使用ISO語言代碼作為Name屬性的值。 建立語言根後，您就可以在語言根的任何層級建立語言副本。

例如，範例階層的義大利語言副本的根頁面會以`it`作為Name屬性。 Name屬性會作為存放庫中資產節點的名稱，因此會決定資產的路徑。(`https://[aem_server]:[port]/assets.html/content/dam/it/`)。

1. 在[!DNL Assets]控制台中，按一下&#x200B;**[!UICONTROL Create]**&#x200B;並從菜單中選擇&#x200B;**[!UICONTROL Folder]**。

   ![建立資料夾](assets/Create-folder.png)

1. 在&#x200B;**[!UICONTROL 名稱]**&#x200B;欄位中，以`<language-code>`格式輸入國家/地區代碼。

   ![在資料夾中新增語言程式碼](assets/Add-language-code-in-folder.png)

1. 按一下&#x200B;**[!UICONTROL 建立]**。語言根在[!DNL Assets]控制台中建立。

## 查看語言根{#viewing-language-roots}

[!DNL Experience Manager] 介面提供一 **** 個「參考」面板，該面板顯示已在中建立的語言根 [!DNL Assets]清單。

1. 在[!DNL Assets]控制台中，選擇要為其建立語言副本的語言主要。
1. 從左側邊欄中，選擇&#x200B;**[!UICONTROL References]**&#x200B;選項以開啟[!UICONTROL Reference]窗格。

   ![chlimage_1-122](assets/chlimage_1-122.png)

1. 在「參考」窗格中，按一下「語言副本」****。 [!UICONTROL 語言副本]面板會顯示資產的語言副本。

   ![語言副本](assets/lang-copy2.png)
