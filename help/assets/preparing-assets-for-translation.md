---
title: 準備翻譯資產
description: 建立語言根資料夾，以準備要翻譯的資產，以支援多語言資產。
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# 準備翻譯資產 {#preparing-assets-for-translation}

多語言資產是指包含多種語言的二進位檔、中繼資料和標籤的資產。 一般而言，資產的二進位檔、中繼資料和標籤都以一種語言存在，然後會翻譯成其他語言，以用於多語言專案。

在Adobe Experience Manager(AEM)Assets中，多語言資產會包含在檔案夾中，其中每個檔案夾都包含不同語言的資產。

每個語言資料夾都稱為語言副本。 語言副本的根資料夾（稱為語言根目錄）標識語言副本中內容的語言。 例如， ** /content/dam/it是義大利文語言副本的義大利文根目錄。 語言副本必須使用 [正確設定的語言根目錄](preparing-assets-for-translation.md#creating-a-language-root) ，以便在執行來源資產翻譯時定位正確的語言。

您最初新增資產的語言副本是語言主版。 語言主版是翻譯成其他語言的源。 範例資料夾階層包含數個語言根目錄：

```
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

執行下列步驟以準備要翻譯的資產：

1. 建立您語言主版的語言根目錄。 例如，範例檔案夾階層中英文版副本的語言根目錄為 `/content/dam/en`。 確保根據「建立語言根」中的資訊正確配置 [了語言根](preparing-assets-for-translation.md#creating-a-language-root)。

1. 將資產新增至您的語言主版。
1. 建立您需要語言副本的每種目標語言的語言根目錄。

## 建立語言根目錄 {#creating-a-language-root}

要建立語言根目錄，請建立資料夾並使用ISO語言代碼作為「名稱」屬性的值。 建立語言根目錄後，可以在語言根目錄的任何級別建立語言副本。

例如，範例階層的義大利文語言副本的根頁面 `it` 為Name屬性。 Name屬性用作儲存庫中資產節點的名稱，因此確定資產的路徑。(`https://[aem_server]:[port]/assets.html/content/dam/it/`)。

1. 在「資產」主控台中，按一下／點選「 **[!UICONTROL 建立]** 」，然後從 **[!UICONTROL 選單選擇「資料夾]** 」。

   ![建立資料夾](assets/Create-folder.png)

1. 在「名 **[!UICONTROL 稱]** 」欄位中，以格式輸入國家代碼 `<language-code>`。

   ![在資料夾中新增語言代碼](assets/Add-language-code-in-folder.png)

1. 按一下或點選「 **[!UICONTROL 建立]**」。 語言根目錄是在「資產」主控台中建立。

## 檢視語言根 {#viewing-language-roots}

AEM介面提供「 **[!UICONTROL 參考」面板]** ，可顯示已在AEM Assets中建立的語言根目錄清單。

1. 在「資產」主控台中，選取您要建立語言副本的語言主版。
1. 按一下或點選「GlobalNav」圖示，然後選擇「參 **[!UICONTROL 考]** 」以開啟「 [!UICONTROL 參考] 」窗格。

   ![chlimage_1-122](assets/chlimage_1-122.png)

1. 在「參考」窗格中，按一下或點選「語 **[!UICONTROL 言副本」]**。 「語 [!UICONTROL 言復本] 」面板會顯示資產的語言復本。

   ![chlimage_1-123](assets/chlimage_1-123.png)
