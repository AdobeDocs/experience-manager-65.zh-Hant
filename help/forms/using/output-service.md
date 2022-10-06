---
title: 輸出服務
seo-title: Output Service
description: 說明屬於AEM檔案服務的輸出服務
seo-description: Describes Output Service, which is part of AEM Document Services
uuid: edddef59-b43c-486f-8734-3f97961ecf4d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 51ab91ff-c0c0-4165-ae02-f306e45eea03
docset: aem65
exl-id: 1b62e1c1-428d-4c0f-98a8-486f319fa581
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 6%

---

# 輸出服務{#output-service}

## 總覽 {#overview}

輸出服務是AEM檔案服務的一部分。 輸出服務支援AEM Forms Designer的各種輸出格式和輸出設計功能。 輸出服務可以轉換XFA模板和XML資料，以生成各種格式的打印文檔。

Output 服務可讓您建立以下用途的應用程式：

* 使用 XML 資料填寫範本檔案來產生最終表單文件。
* 以各種格式生成輸出表單，包括非互動式PDF、PostScript、PCL和ZPL打印流。
* 從 XFA 表單 PDF 產生列印 PDF。
* 將多組資料與提供的模板合併，以批量生成PDF、PostScript、PCL和ZPL文檔。

>[!NOTE]
>
>輸出服務是32位應用程式。 在Microsoft Windows上，32位元應用程式最多可使用2 GB記憶體。 此限制也適用於輸出服務。

## 建立非互動式表單檔案 {#creating-non-interactive-form-documents}

![usingoutput_modified](assets/usingoutput_modified.png)

通常，您會使用AEM Forms Designer建立範本。 此 `generatePDFOutput` 和 `generatePrintedOutput` 輸出服務的API可以直接將這些模板轉換為各種格式，包括PDF、PostScript、ZPL和PCL。

此 `generatePDFOutput` 操作會生成PDF，而 `generatePrintedOutput` 操作生成PostScript、ZPL和PCL格式。 這兩個操作的第一個參數接受模板檔案的名稱(例如 `ExpenseClaim.xdp`)或包含範本的檔案物件。 指定範本檔案的名稱時，也請指定內容根作為包含範本之資料夾的路徑。 您可以使用 `PDFOutputOptions` 或 `PrintedOutputOptions` 參數。 有關可以使用這些參數指定的其他選項的詳細資訊，請參閱Javadoc。

第二參數接受在生成輸出文檔時與模板合併的XML文檔。

此 `generatePDFOutput` 操作也可以接受基於XFA的PDF表單作為輸入，並將PDF表單的非互動式版本作為輸出返回。

## 產生非互動式表單檔案 {#generating-non-interactive-form-documents}

假設您有一或多個範本，以及每個範本的多個XML資料記錄。

使用 `generatePDFOutputBatch` 和 `generatePrintedOutputBatch` 輸出服務的操作，以生成每個記錄的打印文檔。

您也可以將記錄合併為單一檔案。 兩個操作都需要四個參數。

第一個參數是地圖，其中包含以任意字串作為索引鍵，而範本檔案的名稱則為值。

第二個參數是不同的映射，其值是包含XML資料的文檔對象。 鍵與您為第一個參數指定的鍵相同。

的第三個參數 `generatePDFOutputBatch` 或 `generatePrintedOutputBatch` 是類型 `PDFOutputOptions` 或 `PrintedOutputOptions` 分別為5個。

參數類型與 `generatePDFOutput` 和 `generatePrintedOutput` 操作，效果相同。

第四個參數為 `BatchOptions`，您可使用此欄位指定是否可為每個記錄產生個別檔案。 此參數的預設值為false。

兩者 `generatePrintedOutputBatch` 和 `generatePDFOutputBatch` 傳回類型的值 `BatchResult`. 值包含生成的文檔清單。 它還包含XML格式的元資料文檔，該文檔包含與生成的每個文檔相關的資訊。
