---
title: Forms 服務
seo-title: Forms Service
description: 文章介紹了Forms服務以及您可以使用Forms服務執行的與表單相關的任務。
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

通過Forms服務，您可以建立互動式資料捕獲客戶端應用程式，這些應用程式可驗證、處理、轉換和傳遞通常在設計器中建立的表單。 Forms服務將您開發的任何表單設計作為PDF文檔呈現。

Forms服務還使企業能夠通過部署電子錶單作為AdobePDF來擴展其智慧資料捕獲流程。 您還可以使用服務分別將資料導入和導出到現有PDF forms。

使用Forms服務執行以下操作：

* 基於模板和XML資料呈現PDF forms。
* 啟用表單資料整合以將資料導入PDF forms並從其中提取資料。
* 基於片段呈現表單。

## 建立PDF forms  {#creating-pdf-forms-nbsp}

使用Form服務為資料捕獲建立PDF forms。 通常，您從AEM Forms設計器模板開始。 使用 `renderPDFForm` （連結到Javadoc）Forms服務的操作，以將此模板轉換為PDF表單。

的第一個參數 `renderPDFForm` operation是模板檔案的名稱(例如， `ExpenseClaim.xdp`)。 可以將模板檔案儲存在本地檔案系統、CRX儲存庫中，或儲存在HTTP或FTP位置。 通過在 `PDFFormRenderOptions` 參數 `renderPDFForm` 的下界。 有關可為指定的其他選項的詳細資訊，請參閱Javadoc `PDFFormRenderOptions` 的下界。

的 `renderPDFForm` 操作也可以接受XML資料。 在建立PDF表單時，XML資料與模板合併，以便生成的PDF表單包含指定的資料。 的第二個參數 `renderPDFForm` 操作可以接受包含XML資料的文檔(Javadoc)對象。

## 從PDF forms中提取資料  {#extracting-data-from-pdf-forms-nbsp}

使用 `exportData` (Javadoc)Forms服務的操作，以從PDF表單中提取資料XML。 此操作將文檔作為其第一個參數。 可以將資料導出為XDP文檔或XML檔案。 如果將資料導出為XML檔案，則導出的資料將刪除XDP包絡並返回純XML檔案。 可以使用第二個參數指定此配置。

## 將資料導入PDF forms {#importing-data-into-pdf-forms}

Forms服務還允許您合併使用AEM Forms設計器或 `renderPDFForm` 操作。 的 `importData` Forms服務的(Javadoc)操作接受PDF表單和XML資料，並返回帶有資料XML的PDF表單。

## 基於片段的呈現形式 {#rendering-forms-based-on-fragments}

Forms服務可以根據您使用AEM Forms設計器建立的片段來呈現表單。 片段是形式的可重用部分。 它被保存為可插入到多個窗體設計中的單獨XDP檔案。 例如，片段可以包括地址塊或合法文本。

使用碎片簡化並加速了大量形式的建立和維護。 在建立表單時，插入對要在表單中顯示的片段所需片段的引用。 片段引用包含指向物理XDP檔案的子窗體。

以下是使用片段的優點：

* **內容重用**:您可以在多個窗體設計中重複使用內容。 要在多個表單中快速重複使用同一內容的部分，請建立一個片段。 複製或重新建立內容需要較長的時間。 使用片段還確保表單設計中經常使用的部分在所有引用表單中具有一致的內容和外觀。
* **全局更新**:您只能對一個檔案中的多個表單進行一次全局更改。 您可以更改片段中的內容、指令碼對象、資料綁定、佈局或樣式。 引用片段的所有XDP表單都反映更改。
* **共用表單建立**:您可以在多個資源之間共用表單的建立。 具有AEM Forms設計器指令碼或其他高級功能的表單開發人員可以開發和共用使用指令碼和動態屬性的片段。 表單設計者可以使用片段來設計表單。 此外，他們可以使用碎片來確保表單的所有部分在多個表單上具有一致的外觀和功能。
