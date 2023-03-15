---
title: Forms 服務
seo-title: Forms Service
description: 本文說明Forms服務，以及您可使用Forms服務執行的表單相關工作。
seo-description: The article describes Forms service and the form-related tasks you can perform using Forms service.
uuid: 3258d3c2-8755-4815-8c97-b2cfb9a9dfd4
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: a9695d10-43ec-40eb-942f-7720abaa0973
exl-id: bd1216e4-2248-484b-a3c1-c209da4ff94f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 0%

---

# Forms 服務 {#forms-service}

## 概觀 {#overview}

Forms服務可讓您建立互動式資料擷取用戶端應用程式，以驗證、處理、轉換及傳遞通常在Designer中建立的表單。 Forms服務會以PDF檔案的形式呈現，記錄您開發的任何表單設計。

Forms服務也可讓組織將電子錶單部署為AdobePDF，以延伸其智慧型資料擷取程式。 您也可以使用服務，將資料分別匯入和匯出至現有PDF forms。

使用Forms服務執行下列作業：

* 根據範本和XML資料呈現PDF forms。
* 啟用表單資料整合，將資料匯入PDF forms並從中擷取資料。
* 根據片段轉譯表單。

## 建立PDF forms  {#creating-pdf-forms-nbsp}

使用表單服務建立資料捕獲的PDF forms。 通常從AEM Forms設計工具範本開始。 使用 `renderPDFForm` (連結到Forms)操作，將此模板轉換為PDF表單。

的第一個參數 `renderPDFForm` operation是範本檔案的名稱(例如 `ExpenseClaim.xdp`)。 您可以將範本檔案儲存在本機檔案系統、CRX存放庫，或儲存在HTTP或FTP位置。 您可以在 `PDFFormRenderOptions` 參數 `renderPDFForm` 操作。 有關可為 `PDFFormRenderOptions` 參數。

此 `renderPDFForm` 操作也可以接受XML資料。 建立PDF表單時，XML資料會與模板合併，以便生成的PDF表單包含指定的資料。 的第二個參數 `renderPDFForm` 操作可以接受包含XML資料的文檔(Javadoc)對象。

## 從PDF forms擷取資料  {#extracting-data-from-pdf-forms-nbsp}

使用 `exportData` (Javadoc)從Forms表單中提取資料XML的PDF服務的操作。 此操作接受文檔作為其第一個參數。 您可以將資料匯出為XDP檔案或XML檔案。 如果將資料導出為XML檔案，則導出的資料將刪除XDP信封並返回純XML檔案。 您可以使用第二個參數指定此排列。

## 將資料匯入PDF forms {#importing-data-into-pdf-forms}

Forms服務也可讓您合併使用AEM Forms Designer或 `renderPDFForm` 操作XML資料。 此 `importData` (Javadoc)Forms服務的操作接受PDF表單和XML資料，並返回帶有資料XML的PDF表單。

## 根據片段轉譯表單 {#rendering-forms-based-on-fragments}

Forms服務可根據您使用AEM Forms Designer建立的片段來轉譯表單。 片段是表單中可重複使用的部分。 它會儲存為個別的XDP檔案，可插入至多個表單設計中。 例如，片段可以包含地址塊或法律文字。

使用片段可簡化及加速大量表單的建立與維護。 建立表單時，插入所需片段的參考，以讓片段在表單中顯示。 片段參考包含指向物理XDP檔案的子表單。

以下是使用片段的優點：

* **內容重複使用**:您可以在多個表單設計中重複使用內容。 若要在多個表單中快速重複使用相同內容的部分，請建立片段。 複製或重新建立內容需要較長的時間。 使用片段也可確保經常使用的表單設計部分在所有參考表單中具有一致的內容和外觀。
* **全域更新**:您只能對檔案中的多個表單進行一次全域變更。 您可以變更片段中的內容、指令碼物件、資料系結、版面或樣式。 所有參考片段的XDP表單都會反映變更。
* **共用表單建立**:您可以在多個資源之間共用表單建立作業。 具備指令碼或AEM Forms Designer其他進階功能的表單開發人員可開發及共用使用指令碼和動態屬性的片段。 表單設計人員可以使用片段來設計表單。 此外，他們可以使用片段，確保表單的所有部分在多個表單中具有一致的外觀和功能。
