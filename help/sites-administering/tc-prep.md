---
title: 準備翻譯內容
seo-title: Preparing Content for Translation
description: 瞭解如何準備翻譯內容。
seo-description: Learn how to prepare content for translation.
uuid: 369630a8-2ed7-48db-973e-bd8213231d49
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 8bd67d71-bcb7-4ca0-9751-3ff3ee054011
feature: Language Copy
exl-id: 81978733-89a6-4436-bcf1-4bde962ed54f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 1%

---

# 準備翻譯內容{#preparing-content-for-translation}

多語言網站通常以多種語言提供一定數量的內容。 網站以一種語言編寫，然後翻譯成其他語言。 通常，多語言站點由頁面的分支組成，其中每個分支包含以不同語言表示的站點頁面。

示例Geometrixx演示站點包括幾個語言分支，並使用以下結構：

```xml
/content
    |- geometrixx
             |- en
             |- fr
             |- de
             |- es
             |- it
             |- ja
             |- zh
```

站點的每個語言分支都稱為語言副本。 語言副本的根頁（稱為語言根）標識語言副本中內容的語言。 比如說， `/content/geometrixx/fr` 是法文語言副本的語言根。 語言副本必須使用 [正確配置的語言根](/help/sites-administering/tc-prep.md#creating-a-language-root) 這樣，當執行源站點的翻譯時，就會針對正確的語言。

您最初為其創作網站內容的語言副本是語言母版。 語言母版是翻譯成其他語言的源。

使用以下步驟準備您的站點進行翻譯：

1. 建立語言母版的語言根。 例如，英語Geometrixx演示站點的語言根為/content/geometrixx/en。 確保根據中的資訊正確配置語言根 [建立語言根](/help/sites-administering/tc-prep.md#creating-a-language-root)。
1. 編寫您的語言母版的內容。
1. 為站點建立每種語言副本的語言根。 例如，Geometrixx示例站點的法語語言副本是/content/geometrixx/fr。

在準備翻譯內容後，您可以在語言副本和相關翻譯項目中自動建立丟失的頁面。 (請參閱 [建立翻譯項目](/help/sites-administering/tc-manage.md)。) 有關中的內容翻譯過程的概AEM述，請參見 [翻譯多語言網站的內容](/help/sites-administering/translation.md)。

## 建立語言根 {#creating-a-language-root}

建立語言根作為標識內容語言的語言副本的根頁。 建立語言根後，可以建立包含語言副本的翻譯項目。

要建立語言根，請建立一個頁面，並使用ISO語言代碼作為「名稱」屬性的值。 語言代碼必須採用以下格式之一：

* `<language-code>`支援的語言代碼是ISO-639-1定義的雙字母代碼，例如 `en`。

* `<language-code>_<country-code>` 或 `<language-code>-<country-code>`支援的國家代碼是ISO 3166定義的小寫或大寫雙字母代碼，例如 `en_US`。 `en_us`。 `en_GB`。 `en-gb`。

您可以根據為全局站點選擇的結構使用兩種格式。  例如，Geometrixx站點的法語語言副本的根頁具有 `fr` 名稱屬性。 請注意，「名稱」屬性用作儲存庫中頁面節點的名稱，因此確定了頁面的路徑。 (http://localhost:4502/content/geometrixx/fr.html)

以下過程使用觸控優化的UI建立網站的語言副本。 有關使用Classic UI的說明，請參見 [使用標準用戶介面建立語言根](/help/sites-administering/tc-lroot-classic.md)。

1. 導航到站點。
1. 按一下或點擊要為其建立語言副本的站點。

   例如，要建立Geometrixx Outdoors站點的語言副本，可按一下或點擊Geometrixx Outdoors站點。

1. 按一下或點擊「建立」，然後按一下或點擊「建立頁面」。

   ![chlimage_1-21](assets/chlimage_1-21a.png)

1. 選擇頁面模板，然後按一下或點擊「下一步」。
1. 在「名稱」欄位中，鍵入國家/地區代碼，格式為 `<language-code>` 或 `<language-code>_<country-code>`，例如 `en`。 `en_US`。 `en_us`。 `en_GB`。 `en_gb`。 鍵入頁面標題。

   ![chlimage_1-22](assets/chlimage_1-22a.png)

1. 按一下或點擊「建立」。 在確認對話框中，按一下或點擊 **完成** 返回到站點控制台，或 **開啟** 開啟語言副本。

## 語言根的地位 {#seeing-the-status-of-language-roots}

觸控優化的UI提供「參考」面板，該面板顯示已建立的語言根的清單。

![chlimage_1-23](assets/chlimage_1-23a.png)

以下過程使用觸控優化的UI開啟頁面的「引用」面板。

1. 在「站點」控制台上，選擇站點的頁面，然後按一下或點擊 **引用**。

   ![chlimage_1-24](assets/chlimage_1-24a.png)

1. 在「參照」(references)面板中，按一下或點擊 **語言副本**。 「語言副本」面板顯示網站的語言副本。
