---
title: 準備資產以進行翻譯
description: 建立語言根資料夾以準備翻譯資產以支援多語言資產。
contentOwner: AG
role: User, Admin
feature: Projects
exl-id: eee768e3-3eb4-46fa-b9ae-9ef8764a3a94
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 1%

---

# 準備資產以進行翻譯 {#preparing-assets-for-translation}

多語言資產是指使用多種語言的二進位檔案、元資料和標籤的資產。 通常，資產的二進位檔案、元資料和標籤以一種語言存在，然後翻譯成其他語言以用於多語言項目。

在 [!DNL Adobe Experience Manager Assets]，多語言資產包含在資料夾中，其中每個資料夾包含不同語言的資產。

每個語言資料夾都稱為語言副本。 語言副本的根資料夾（稱為語言根）標識語言副本中內容的語言。 比如說， */content/dam/it* 是義大利語副本的義大利語根。 語言副本必須使用 [正確配置的語言根](preparing-assets-for-translation.md#creating-a-language-root) 這樣，在執行源資產的翻譯時，就能找到正確的語言。

您最初為其添加資產的語言副本是語言主要。 主要語言是翻譯成其他語言的源。 一個示例資料夾層次結構包括多個語言根：

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

執行以下步驟以準備資產以進行翻譯：

1. 建立語言主語的語言根。 例如，示例資料夾層次結構中英文副本的語言根為 `/content/dam/en`。 確保根據中的資訊正確配置語言根 [建立語言根](preparing-assets-for-translation.md#creating-a-language-root)。

1. 將資源添加到您的語言主語。
1. 建立需要語言副本的每個目標語言的語言根。

## 建立語言根 {#creating-a-language-root}

要建立語言根，請建立一個資料夾，並使用ISO語言代碼作為「名稱」屬性的值。 在建立語言根目錄後，可以在語言根目錄的任何級別建立語言副本。

例如，示例層次結構的義大利語語言副本的根頁具有 `it` 名稱屬性。 「名稱」屬性用作儲存庫中資產節點的名稱，因此確定資產的路徑。(`https://[aem_server]:[port]/assets.html/content/dam/it/`)。

1. 從 [!DNL Assets] 控制台，按一下 **[!UICONTROL 建立]** 選擇 **[!UICONTROL 資料夾]** 的子菜單。

   ![建立資料夾](assets/Create-folder.png)

1. 在 **[!UICONTROL 名稱]** 欄位鍵入格式為 `<language-code>`。

   ![在資料夾中添加語言代碼](assets/Add-language-code-in-folder.png)

1. 按一下&#x200B;**[!UICONTROL 建立]**。語言根在 [!DNL Assets] 控制台。

## 查看語言根 {#viewing-language-roots}

[!DNL Experience Manager] 介面提供 **[!UICONTROL 引用]** 顯示在中建立的語言根清單的面板 [!DNL Assets]。

1. 在 [!DNL Assets] 控制台，選擇要為其建立語言副本的語言主要版本。
1. 從左滑軌中，選擇 **[!UICONTROL 引用]** 選項 [!UICONTROL 引用] 的子菜單。

   ![chlimage_1-122](assets/chlimage_1-122.png)

1. 在「引用」窗格中，按一下 **[!UICONTROL 語言副本]**。 的 [!UICONTROL 語言副本] 面板顯示資產的語言副本。

   ![語言副本](assets/lang-copy2.png)
