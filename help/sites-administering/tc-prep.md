---
title: 準備翻譯內容
description: 瞭解如何準備內容以在Adobe Experience Manager中翻譯。
contentOwner: Guillaume Carlino
feature: Language Copy
exl-id: 81978733-89a6-4436-bcf1-4bde962ed54f
source-git-commit: eaffc71c23c18d26ec5cbb2bbb7524790c4826fe
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 1%

---

# 準備翻譯內容{#preparing-content-for-translation}

多語言網站通常以多種語言提供一定數量的內容。 網站是以一種語言撰寫，然後翻譯成其他語言。 通常，多語言網站是由頁面分支組成，每個分支都包含不同語言的網站頁面。

範例Geometrixx示範網站包含數個語言分支，並使用下列結構：

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

網站的每個語言分支都稱為語言副本。 語言副本的根頁面（稱為語言根）可識別語言副本中的內容語言。 例如， `/content/geometrixx/fr` 是法語副本的語言根。 語言副本必須使用 [已正確設定的語言根目錄](/help/sites-administering/tc-prep.md#creating-a-language-root) 以便在翻譯來源網站時鎖定正確的語言。

您最初為其創作網站內容的語言副本是語言主要版本。 語言母版是翻譯成其他語言的來源。

使用下列步驟來準備您的網站以進行翻譯：

1. 建立語言主版的語言根。 例如，英文Geometrixx示範網站的語言根為/content/geometrixx/en。 請確定已根據中的資訊正確設定語言根 [建立語言根目錄](/help/sites-administering/tc-prep.md#creating-a-language-root).
1. 編寫語言主版的內容。
1. 建立網站每個語言副本的語言根。 例如，Geometrixx範例網站的法文副本為/content/geometrixx/fr。

準備要翻譯的內容後，您可以在語言副本和相關翻譯專案中自動建立遺失的頁面。 (請參閱 [建立翻譯專案](/help/sites-administering/tc-manage.md).) 如需AEM內容翻譯流程的概觀，請參閱 [翻譯多語言網站的內容](/help/sites-administering/translation.md).

## 建立語言根目錄 {#creating-a-language-root}

建立語言根作為識別內容語言的語言副本的根頁面。 建立語言根之後，您可以建立包含語言副本的翻譯專案。

若要建立語言根，請建立頁面並使用ISO語言代碼作為Name屬性的值。 語言程式碼必須是下列其中一種格式：

* `<language-code>`支援的語言代碼是由ISO-639-1定義的兩字母代碼，例如 `en`.

* `<language-code>_<country-code>` 或 `<language-code>-<country-code>`支援的國家/地區代碼是由ISO 3166定義的小寫或大寫兩字母代碼，例如 `en_US`， `en_us`， `en_GB`， `en-gb`.

根據您為全域網站選擇的結構，您可以使用任一格式。  例如，Geometrixx網站法文副本的根頁面有 `fr` 作為Name屬性。 請注意，Name屬性會用作存放庫中頁面節點的名稱，從而決定頁面的路徑。 (http://localhost:4502/content/geometrixx/fr.html)

下列程式使用觸控最佳化UI來建立網站的語言副本。 如需使用傳統UI的說明，請參閱 [使用Classic UI建立語言根](/help/sites-administering/tc-lroot-classic.md).

1. 導覽至「網站」。
1. 按一下或點選您要建立語言副本的網站。

   例如，若要建立Geometrixx Outdoors網站的語言副本，您可以按一下或點選「Geometrixx Outdoors網站」。

1. 按一下或點選「建立」，然後按一下或點選「建立頁面」。

   ![chlimage_1-21](assets/chlimage_1-21a.png)

1. 選取頁面範本，然後按一下或點選「下一步」。
1. 在「名稱」欄位中，輸入國家/地區代碼，格式為 `<language-code>` 或 `<language-code>_<country-code>`，例如 `en`， `en_US`， `en_us`， `en_GB`， `en_gb`. 輸入頁面的標題。

   ![chlimage_1-22](assets/chlimage_1-22a.png)

1. 按一下或點選「建立」。 在確認對話方塊中，按一下或點選 **完成** 返回Sites主控台，或 **開啟** 以開啟語言副本。

## 檢視語言根的狀態 {#seeing-the-status-of-language-roots}

觸控最佳化的UI提供「參考」面板，顯示已建立的語言根清單。

![chlimage_1-23](assets/chlimage_1-23a.png)

下列程式會使用觸控最佳化UI來開啟頁面的「參考」面板。

1. 在網站主控台上，選取網站的頁面，然後按一下或點選 **引用**.

   ![chlimage_1-24](assets/chlimage_1-24a.png)

1. 在參照面板中，按一下或點選 **語言副本**. 「語言副本」面板會顯示網站的語言副本。
