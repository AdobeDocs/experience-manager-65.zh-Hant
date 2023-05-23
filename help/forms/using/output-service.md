---
title: 輸出服務
seo-title: Output Service
description: 描述作為文檔服務一部分的輸AEM出服務
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

## 概觀 {#overview}

輸出服務是Document Services的一部分的OSGiAEM服務。 輸出服務支援AEM Forms設計器的各種輸出格式和輸出設計功能。 輸出服務可以轉換XFA模板和XML資料，以生成各種格式的打印文檔。

Output 服務可讓您建立以下用途的應用程式：

* 使用 XML 資料填寫範本檔案來產生最終表單文件。
* 以各種格式生成輸出表單，包括非互動式PDF、PostScript、PCL和ZPL打印流。
* 從 XFA 表單 PDF 產生列印 PDF。
* 通過將多組資料與提供的模板合併，批量生成PDF、PostScript、PCL和ZPL文檔。

>[!NOTE]
>
>輸出服務是32位應用程式。 在MicrosoftWindows上，32位應用程式最多可使用2 GB記憶體。 該限制也適用於輸出服務。

## 建立非互動式表單文檔 {#creating-non-interactive-form-documents}

![使用output_modified](assets/usingoutput_modified.png)

通常，您使用AEM Forms設計器建立模板。 的 `generatePDFOutput` 和 `generatePrintedOutput` Output服務的API允許您直接將這些模板轉換為各種格式，包括PDF、PostScript、ZPL和PCL。

的 `generatePDFOutput` 操作生成PDF，而 `generatePrintedOutput` 操作生成PostScript、ZPL和PCL格式。 這兩個操作的第一個參數接受模板檔案的名稱(例如 `ExpenseClaim.xdp`)或包含該模板的Document對象。 指定模板檔案的名稱時，還應指定內容根作為包含模板的資料夾的路徑。 可以使用以下任一選項指定內容根 `PDFOutputOptions` 或 `PrintedOutputOptions` 的下界。 有關可以使用這些參數指定的其他選項的詳細資訊，請參見Javadoc。

第二個參數接受在生成輸出文檔時與模板合併的XML文檔。

的 `generatePDFOutput` 操作還可以接受基於XFA的PDF表單作為輸入，並返回非交互版本的PDF表單作為輸出。

## 生成非互動式表單文檔 {#generating-non-interactive-form-documents}

請考慮一個方案，其中每個模板有一個或多個模板和多個XML資料記錄。

使用 `generatePDFOutputBatch` 和 `generatePrintedOutputBatch` 輸出服務的操作，以為每個記錄生成打印文檔。

您還可以將記錄合併為單個文檔。 這兩個操作都需要四個參數。

第一個參數是映射，該映射包含任意字串作為鍵，模板檔案的名稱作為值。

第二個參數是其值是包含XML資料的Document對象的不同Map。 鍵與為第一個參數指定的鍵相同。

第三個參數 `generatePDFOutputBatch` 或 `generatePrintedOutputBatch` 類型 `PDFOutputOptions` 或 `PrintedOutputOptions` 分別進行。

參數類型與參數的類型相同 `generatePDFOutput` 和 `generatePrintedOutput` 具有相同的效果。

第四個參數的類型 `BatchOptions`，用於指定是否可以為每個記錄生成單獨的檔案。 此參數的預設值為false。

兩者 `generatePrintedOutputBatch` 和 `generatePDFOutputBatch` 返回類型值 `BatchResult`。 該值包含生成的文檔清單。 它還包含XML格式的元資料文檔，該元資料文檔包含與生成的每個文檔相關的資訊。
