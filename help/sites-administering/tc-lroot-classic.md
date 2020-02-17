---
title: 使用Classic UI建立語言根目錄
seo-title: 使用Classic UI建立語言根目錄
description: 瞭解如何使用Classic UI建立語言根目錄。
seo-description: 瞭解如何使用Classic UI建立語言根目錄。
uuid: 62e40d39-2868-4d3d-9af7-c60a1a658be0
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: b88edad4-2a2e-429b-86a2-cc68ba69697e
docset: aem65
translation-type: tm+mt
source-git-commit: 8b53e79e3a88f58423e99477db930a4912a1ba09

---


# 使用Classic UI建立語言根目錄{#creating-a-language-root-using-the-classic-ui}

下列程式使用傳統UI來建立網站的語言根目錄。 如需詳細資訊，請 [參閱建立語言根目錄](/help/sites-administering/tc-prep.md#creating-a-language-root)。

1. 在「網站」主控台的「網站」樹狀結構中，選取網站的根頁面。 ([http://localhost:4502/siteadmin#](http://localhost:4502/siteadmin#))
1. 新增代表網站語言版本的子頁面：

   1. 按一下「新增>新增頁面」。
   1. 在對話方塊中，指定「標題」和「名稱」。 名稱的格式必須為 `<language-code>` 或 `<language-code>_<country-code>`，例如en、en_US、en_us、en_GB、en_gb。

      * 支援的語言程式碼為小寫、由ISO-639-1定義的雙字母程式碼
      * 支援的國家／地區代碼為小寫或大寫，由ISO 3166定義的雙字母代碼
   1. 選取範本，然後按一下建立。
   ![newpagefr](assets/newpagefr.png)

1. 在「網站」主控台的「網站」樹狀結構中，選取網站的根頁面。
1. 在「工具」菜單中，選擇「語言副本」。

   ![工具語言副本](assets/toolslanguagecopy.png)

   「語言副本」對話框顯示可用語言版本和網頁的矩陣。 語言欄中的x表示該頁面有該語言版本。

   ![語言隱譯對話](assets/languagecopydialog.png)

1. 若要將現有頁面或頁面樹狀結構複製到語言版本，請在語言欄中選取該頁面的儲存格。 按一下箭頭並選取要建立的復本類型。

   在下例中，設備／太陽鏡/irian頁面被複製到法文版本。

   ![苦蕎麥](assets/languagecopydilogdropdown.png)

   | 語言副本類型 | 說明 |
   |---|---|
   | auto | 使用父頁面的行為 |
   | 忽略 | 不建立此頁及其子頁的副本 |
   | `<language>+` （例如法文+） | 從該語言複製頁面及其所有子系 |
   | `<language>` （例如法文） | 僅複製該語言的頁面 |

1. 按一下「確定」(OK)關閉對話框。
1. 在下一個對話方塊中，按一下「是」以確認復本。

