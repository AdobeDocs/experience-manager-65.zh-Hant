---
title: 使用標準用戶介面建立語言根
seo-title: Creating a Language Root Using the Classic UI
description: 瞭解如何使用Classic UI建立語言根。
seo-description: Learn how to create a language root using the Classic UI.
uuid: 62e40d39-2868-4d3d-9af7-c60a1a658be0
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: b88edad4-2a2e-429b-86a2-cc68ba69697e
docset: aem65
feature: Language Copy
exl-id: 1ae21d80-0683-4ab9-afaa-4d733ff47720
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# 使用標準用戶介面建立語言根{#creating-a-language-root-using-the-classic-ui}

以下過程使用經典UI建立站點的語言根。 有關詳細資訊，請參見 [建立語言根](/help/sites-administering/tc-prep.md#creating-a-language-root)。

1. 在「網站」控制台的「網站」樹中，選擇網站的根頁。 ([http://localhost:4502/siteadmin#](http://localhost:4502/siteadmin#))
1. 添加新的子頁面，該頁面表示站點的語言版本：

   1. 按一下「新建」>「新建頁面」。
   1. 在對話框中，指定標題和名稱。 名稱的格式應為 `<language-code>` 或 `<language-code>_<country-code>`，例如en、en_US、en_us、en_GB、en_gb。

      * 支援的語言代碼是ISO-639-1定義的小寫、雙字母代碼
      * 受支援的國家/地區代碼是ISO 3166定義的小寫或大寫兩字母代碼
   1. 選擇模板，然後按一下建立。

   ![新頁](assets/newpagefr.png)

1. 在「網站」控制台的「網站」樹中，選擇網站的根頁。
1. 在「工具」菜單中，選擇「語言複製」。

   ![工具語言副本](assets/toolslanguagecopy.png)

   「語言複製」對話框顯示可用語言版本和網頁的矩陣。 語言列中的x表示該頁可用於該語言。

   ![語言](assets/languagecopydialog.png)

1. 要將現有頁面或頁面樹複製到語言版本，請在語言列中為該頁面選擇單元格。 按一下箭頭，然後選擇要建立的複製類型。

   在以下示例中，設備/太陽鏡/irian頁面正被複製到法語版本。

   ![隱翅目](assets/languagecopydilogdropdown.png)

   | 語言副本的類型 | 說明 |
   |---|---|
   | auto | 使用父頁中的行為 |
   | 忽略 | 不建立此頁及其子頁的副本 |
   | `<language>+` （如法語+） | 從該語言複製頁面及其所有子代 |
   | `<language>` （如法語） | 僅複製該語言中的頁面 |

1. 按一下「確定」關閉對話框。
1. 在下一個對話框中，按一下「是」確認複製。
