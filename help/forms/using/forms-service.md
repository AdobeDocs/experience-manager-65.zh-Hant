---
title: 表單服務
seo-title: 表單服務
description: 文章說明Forms服務以及您可使用Forms服務執行的表單相關工作。
seo-description: 文章說明Forms服務以及您可使用Forms服務執行的表單相關工作。
uuid: 3258d3c2-8755-4815-8c97-b2cfb9a9dfd4
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: a9695d10-43ec-40eb-942f-7720abaa0973
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 表單服務 {#forms-service}

## 概覽 {#overview}

Forms服務可讓您建立互動式資料擷取用戶端應用程式，以驗證、處理、轉換和傳送通常在設計人員中建立的表單。 Forms服務會將您開發的任何表單設計轉換為PDF檔案。

Forms服務也可讓組織將電子錶單部署為Adobe PDF，以擴充其智慧型資料擷取程式。 您也可以使用服務，分別將資料匯入和匯出至現有的PDF表單。

使用Forms服務可執行下列作業：

* 根據範本和XML資料來轉換PDF表格。
* 啟用表單資料整合，將資料匯入PDF表單並從中擷取資料。
* 根據片段來轉換表單。

## 建立PDF表格 {#creating-pdf-forms-nbsp}

使用表單服務建立PDF表單以擷取資料。 通常，您會從AEM Forms Designer範本開始。 使用Forms `renderPDFForm` 服務的（Javadoc連結）操作將此模板轉換為PDF表單。

操作的第一個參 `renderPDFForm` 數是模板檔案的名稱(例如 `ExpenseClaim.xdp`)。 您可以將範本檔案儲存在本機檔案系統、CRX儲存庫或HTTP或FTP位置。 通過在操作參數中設定內容根，可以指定模板文 `PDFFormRenderOptions` 件的位 `renderPDFForm` 置。 有關可為參數指定的其它選項的詳細資訊，請參見Javadoc `PDFFormRenderOptions` 。

操 `renderPDFForm` 作也可以接受XML資料。 在建立PDF表單時，XML資料會與範本合併，讓產生的PDF表單包含指定的資料。 操作的第二個參 `renderPDFForm` 數可以接受包含XML資料的Document(Javadoc)對象。

## 從PDF表單擷取資料 {#extracting-data-from-pdf-forms-nbsp}

使用Forms `exportData` 服務的(Javadoc)操作從PDF表單中提取資料XML。 此操作接受文檔作為其第一個參數。 您可以將資料匯出為XDP檔案或XML檔案。 如果將資料導出為XML檔案，則導出的資料將刪除XDP封套並返回純XML檔案。 您可以使用第二個參數指定此安排。

## 將資料匯入PDF表單 {#importing-data-into-pdf-forms}

Forms服務也可讓您合併使用AEM Forms Designer或XML資料作業所建立 `renderPDFForm` 的PDF表格。 Forms服 `importData` 務的(Javadoc)操作接受PDF表單和XML資料，並返回帶有資料XML的PDF表單。

## 根據片段轉換表單 {#rendering-forms-based-on-fragments}

Forms服務可以根據您使用AEM Forms Designer建立的片段來轉換表單。 片段是表單中可重複使用的部分。 它會儲存為可插入多個表單設計的個別XDP檔案。 例如，片段可以包含地址塊或合法文字。

使用片段可簡化並加速建立和維護大量表單。 在建立表單時，插入對所需片段的引用，以使片段顯示在表單中。 片段參考包含指向物理XDP檔案的子表單。

以下是使用片段的優點：

* **內容重複使用**:您可以在多種表單設計中重複使用內容。 若要在多個表單中快速重複使用相同內容的部分，請建立片段。 複製或重新建立內容需要較長的時間。 使用片段也可確保表格設計中常用的部分在所有參照表格中具有一致的內容和外觀。
* **全域更新**:您只能在檔案中對多個表單進行一次全域變更。 您可以變更片段中的內容、指令碼物件、資料系結、版面或樣式。 所有參照片段的XDP表單都會反映變更。
* **共用表單建立**:您可以在多個資源間共用表單建立功能。 具備AEM Forms Designer指令碼或其他進階功能的表單開發人員，可開發並共用使用指令碼和動態屬性的片段。 表單設計人員可使用片段來設計表單。 此外，他們可以使用片段來確保表單的所有部分在多個表單上具有一致的外觀和功能。

