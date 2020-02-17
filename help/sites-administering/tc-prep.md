---
title: 準備翻譯內容
seo-title: 準備翻譯內容
description: 瞭解如何準備翻譯內容。
seo-description: 瞭解如何準備翻譯內容。
uuid: 369630a8-2ed7-48db-973e-bd8213231d49
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 8bd67d71-bcb7-4ca0-9751-3ff3ee054011
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# 準備翻譯內容{#preparing-content-for-translation}

多語言網站通常提供多種語言的內容。 網站以一種語言編寫，然後翻譯成其他語言。 通常，多語言網站由頁面分支組成，其中每個分支包含不同語言的網站頁面。

範例Geometrixx Demo Site包含數種語言分支，並使用下列結構：

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

網站的每個語言分支都稱為語言副本。 語言副本的根頁面（稱為語言根目錄）可識別語言副本中內容的語言。 例如， `/content/geometrixx/fr` 是法文語言副本的語言根目錄。 語言副本必須使用 [正確配置的語言根目錄](/help/sites-administering/tc-prep.md#creating-a-language-root) ，以便在執行源站點翻譯時定位正確的語言。

您最初為其製作網站內容的語言副本是語言主版。 語言主版是翻譯成其他語言的源。

使用下列步驟來準備您的網站進行翻譯：

1. 建立您語言主版的語言根目錄。 例如，英文Geometrixx示範網站的語言根目錄為/content/geometrixx/tw。 確保根據建立語言根目錄中的資訊正確配置 [了語言根目錄](/help/sites-administering/tc-prep.md#creating-a-language-root)。
1. 編寫您的語言大師的內容。
1. 為您的網站建立每個語言副本的語言根目錄。 例如，Geometrixx範例網站的法文語言副本為/content/geometrixx/fr。

在準備翻譯內容後，您可以自動在語言副本和相關的翻譯項目中建立缺少的頁面。 (請參 [閱建立翻譯項目](/help/sites-administering/tc-manage.md)。)如需AEM中內容轉譯程式的概觀，請參閱「多語 [言網站的轉譯內容」](/help/sites-administering/translation.md)。

## 建立語言根 {#creating-a-language-root}

建立語言根目錄作為識別內容語言的語言副本的根頁面。 建立語言根目錄後，可以建立包含語言副本的翻譯項目。

要建立語言根目錄，請建立一個頁面，並使用ISO語言代碼作為「名稱」屬性的值。 語言代碼必須採用下列格式之一：

* `<language-code>`例如，支援的語言程式碼是由ISO-639-1所定義的雙字母程式碼 `en`。

* `<language-code>_<country-code>` 或 `<language-code>-<country-code>`者，支援的國家／地區代碼是ISO 3166定義的小寫或大寫雙字母代碼 `en_US`, `en_us`例如， `en_GB`、 `en-gb`。

您可以根據您為全域網站選擇的結構，使用任一格式。  例如，Geometrixx網站的法文語言副本的根頁面 `fr` 為Name屬性。 請注意，Name屬性用作儲存庫中頁節點的名稱，因此確定了頁的路徑。 (http://localhost:4502/content/geometrixx/fr.html)

下列程式使用觸控最佳化的UI來建立網站的語言副本。 如需使用Classic UI的指示，請參 [閱使用Classic UI建立語言根目錄](/help/sites-administering/tc-lroot-classic.md)。

1. 導覽至網站。
1. 按一下或點選您要建立語言副本的網站。

   例如，若要建立Geometrixx Outdoors網站的語言副本，您可按一下或點選Geometrixx Outdoors網站。

1. 按一下或點選「建立」，然後按一下或點選「建立頁面」。

   ![chlimage_1-21](assets/chlimage_1-21a.png)

1. 選取頁面範本，然後按一下或點選「下一步」。
1. 在「名稱」欄位中，以或格式 `<language-code>` 輸入國 `<language-code>_<country-code>`家代碼， `en`例如， `en_US`、 `en_us`、 `en_GB`、 `en_gb`。 輸入頁面的標題。

   ![chlimage_1-22](assets/chlimage_1-22a.png)

1. 按一下或點選「建立」。 在確認對話方塊中，按一下或點選 **Done** （完成）以返回Sites主控台，或點選 **Open** （開啟）以開啟語言副本。

## 語言根的地位 {#seeing-the-status-of-language-roots}

觸控最佳化UI提供「參考」面板，顯示已建立的語言根目錄清單。

![chlimage_1-23](assets/chlimage_1-23a.png)

下列程式使用觸控最佳化的UI來開啟頁面的「參考」面板。

1. 在「網站」主控台上，選取網站的頁面，然後按一下或點選「參 **考」**。

   ![chlimage_1-24](assets/chlimage_1-24a.png)

1. 在參照面板中，按一下或點選「語 **言副本」**。 「語言副本」面板顯示網站的語言副本。

