---
title: 設定國際化選項
seo-title: 設定國際化選項
description: 瞭解如何指定用於轉換表單的地區設定，以及如何指定用於編碼輸出串流的字元集。
seo-description: 瞭解如何指定用於轉換表單的地區設定，以及如何指定用於編碼輸出串流的字元集。
uuid: bb77f5f3-634f-4285-9b10-c4dd40085e69
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e845d13f-bef2-442d-af9a-4f92d7616a46
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 設定國際化選項{#setting-internationalization-options}

## 指定用於轉換表單的地區 {#specify-the-locale-used-to-render-forms}

您可以指定在轉譯PDF表單時使用的地區設定。 PDF表格上的欄位使用指定的地區設定來顯示資料。 例如，如果地區設定為德文，表單會使用德文小數分隔符號來表示數值。 語言環境也用於傳送驗證訊息給用戶端裝置，例如網頁瀏覽器，做為HTML轉換的一部分。

1. 在管理控制台中，按一下「服務>表單」。
1. 在「國際化」的「語言」清單中，選擇用於渲染表單的語言環境。 預設值為英文（美國）。
1. 按一下「儲存」。

## 指定用於編碼輸出流的字元集 {#specify-the-character-set-used-to-encode-the-output-stream}

1. 在「國際化」下的「字元集」清單中，選擇一個字元集。 此設定取決於所使用的API，即renderHTMLForm或renderPDFForm。 要指定列出的字元集以外的字元集，請選擇「自定義」並在顯示的框中指定編碼值。

   對於HTML轉換，AEM表單支援由套件定義的字元編碼 `java.nio.charset` 值。 如果sFormPreference是PDFForm，則僅支援特定字元集。 字元集必須是有效的標準名稱。 預設值為ISO-8859-1。

1. 按一下「儲存」。

