---
title: 從AEM工作流程啟動Document Services API
description: 瞭解如何在DDX或提供的輸入上叫用AEM檔案服務。 另請參閱如何將PDF轉換為PDF/A
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
exl-id: 123087a2-9d09-4579-9185-2ccd7d25bf8d
solution: Experience Manager, Experience Manager Forms
feature: Interactive Communication
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1167'
ht-degree: 0%

---

# 從AEM工作流程啟動Document Services API  {#initiate-document-services-apis-from-aem-workflow}

## 組合器 {#assembler}

AEM Forms提供自訂工作流程，可叫用下列Assembler服務API：

* **invoke**：在提供的輸入上叫用輸入DDX中指定的作業。
* **toPDFA**：將輸入PDF檔案轉換為PDF/A檔案。

### 叫用DDX工作流程 {#invoke-ddx-workflow}

**叫用DDX**&#x200B;工作流程會叫用`Invoke`組合器服務API，您可以用它來組合或分解檔案、為PDF新增浮水印等等。

1. 將&#x200B;**[!UICONTROL 叫用DDX]**&#x200B;工作流程步驟拖曳至Sidekick中「Forms Workflow」標籤下。
1. 連按兩下新增的工作流程步驟以編輯元件。
1. 在[編輯元件]對話方塊中，設定輸入檔案、環境選項和輸出檔案，然後按一下[確定]。**&#x200B;**

#### 輸入檔案 {#input-documents}

啟動DDX工作流程需要下列輸入檔案：

* **DDX**：這是「呼叫DDX」工作流程步驟的必要輸入，可以從DDX輸入下拉式清單中選取下列其中一個選項來指定。

   * *相對於承載*： DDX輸入檔案相對於工作流程專案的承載資料夾。
   * *使用承載*：工作流程專案的承載已用作輸入DDX檔案。
   * *絕對路徑*： CRX存放庫中DDX檔案的絕對路徑。

* **從PayLoad建立對應**：選取時，裝載資料夾下的所有檔案都會新增到組合器中`invoke` API的輸入檔案對應。 每個檔案的節點名稱都會作為對應中的索引鍵。

* **輸入檔案的對映**：指定輸入檔案的對映。 您可以新增任意數目的專案，每個專案在地圖中指定檔案的索引鍵，以及檔案的來源。

#### 環境選項 {#environment-options}

「環境選項」索引標籤可讓您為叫用API設定各種處理選項。

* *工作記錄層級*：指定處理記錄的記錄層級。
* *僅驗證*：檢查輸入DDX的有效性。

* *發生錯誤時失敗*：指定如果發生錯誤，對組合器服務的呼叫是否應失敗。 預設值為False。

#### 輸出檔案 {#output-documents}

根據輸入DDX，叫用API可以產生多個輸出檔案。 「輸出檔案」索引標籤可讓您選取將儲存輸出檔案的位置。

1. *將輸出儲存在承載中*：將輸出檔案儲存在承載資料夾下，或覆寫承載（如果承載是檔案）。
1. *輸出檔案的地圖*：可讓您為每個輸出檔案新增一個專案，明確指定儲存每個輸出檔案的位置。 每個專案都會指定檔案以及儲存的位置。 輸出檔案可能會覆寫承載或儲存在承載資料夾下。 有多個輸出檔案時，此功能會很有用。

1. *工作記錄檔*：指定工作記錄檔檔案的儲存位置，這有助於疑難排解失敗。

### 轉換為PDF/工作流程 {#convert-to-pdf-a-workflow}

轉換成PDF/工作流程步驟會叫用`toPDFA`組合器服務API。 它用於將PDF檔案轉換為PDF/A相容檔案。

1. 將&#x200B;**[!UICONTROL ConvertToPDFA]**&#x200B;工作流程步驟拖曳至Sidekick中「Forms Workflow」標籤下。

1. 連按兩下新增的工作流程步驟以編輯元件。
1. 在[編輯元件]對話方塊中，設定輸入檔案、轉換選項和輸出檔案，然後按一下[確定]。**&#x200B;**

#### 輸入檔案 {#input-documents-1}

以下列其中一種方式，指定要轉換為PDF/A相容檔案的檔案來源。

* *相對於承載*：輸入檔案相對於工作流程專案的承載資料夾。
* *使用承載*：工作流程專案的承載已用作輸入檔案。
* *絕對路徑*： CRX存放庫中輸入檔案的絕對路徑。

#### 轉換選項 {#conversion-options}

「轉換選項」可讓您指定變更PDF/A轉換流程的選項。

* *法規遵循* ：指定輸出PDF/A必須符合的PDF/A標準。
* *結果層級* ：指定用於PDF/A轉換記錄的記錄層級。
* *簽章* ：指定轉換期間必須如何處理輸入檔案中的簽章。
* *色域* ：指定要用於輸出PDF/A檔案的預先定義色域。
* *驗證*&#x200B;轉換：指定轉換後的PDF/A檔案在轉換後是否應驗證PDF/A相容性。
* *工作記錄層級* ：指定要用於處理記錄的記錄層級。

* *中繼資料延伸結構描述* ：指定在PDF檔案的中繼資料中用於XMP屬性的中繼資料延伸結構描述路徑。

#### 輸出檔案 {#output-documents-1}

「輸出檔案」標籤可讓您指定輸出檔案的目的地

* *PDFA Document*：指定轉換PDF/A檔案的儲存位置。 它可以覆寫裝載檔案或儲存在裝載資料夾下。
* *轉換記錄檔*：指定轉換記錄檔的儲存位置。 它可以覆寫裝載檔案，或儲存在裝載資料夾下。

## 表單 {#forms}

「轉譯PDF表單」工作流程是`renderPDFForm` Forms服務API的包裝函式，可使用XDP範本和資料xml建立PDF表單。

### 呈現PDF表單工作流程 {#render-pdf-form-workflow}

1. 在「Sidekick」中，將「呈現PDF表單」工作流程步驟拖曳至「Forms Workflow」標籤下。
1. 連按兩下新增的工作流程步驟以編輯元件。
1. 在[編輯元件]對話方塊中，設定輸入檔案、輸出檔案和其他引數，然後按一下[確定]。**&#x200B;**

#### 輸入檔案 {#input-documents-2}

* *範本檔案*：指定XDP範本的位置。 這是必填欄位。

* *資料檔案*：指定需要與範本合併的資料xml的位置。

#### 輸出檔案 {#output-documents-2}

* *輸出檔案*： — 指定產生的PDF表單的名稱。

#### 其他引數 {#additional-parameters}

* *內容根*：指定儲存於輸入XDP範本中所用片段或影像之存放庫中的資料夾路徑。
* *提交URL*：指定所產生PDF表單的預設提交URL。
* *地區*：指定產生的PDF表單的預設地區。
* *Acrobat版本*：為產生的PDF表單指定目標Acrobat版本。
* *已標籤的PDF*：指定是否要讓產生的PDF可供存取。
* *XCI檔案*：指定XCI檔案的路徑。

## 輸出 {#output}

產生非互動式PDF工作流程是`generatePDFOutput`輸出服務API的包裝函式。 它可用來從XDP範本和資料xml產生非互動式PDF檔案。

### 產生非互動式PDF輸出工作流程   {#generate-non-interactive-pdf-output-workflow-nbsp}

1. 將「產生非互動式PDF輸出」工作流程拖曳至「Sidekick」中「Forms Workflow」標籤下。
1. 連按兩下新增的工作流程步驟以編輯元件。
1. 在[編輯元件]對話方塊中，設定輸入檔案、輸出檔案和其他引數，然後按一下[確定]。**&#x200B;**

#### 輸入檔案 {#input-documents-3}

* *範本檔案*：指定XDP範本的位置。 這是必填欄位。

* *資料檔案*：指定需要與範本合併的資料xml的位置。

#### 輸出檔案 {#output-document}

*輸出檔案*：指定產生的PDF表單的名稱。

#### 其他引數 {#additional-parameters-1}

* *內容根*：指定儲存於輸入XDP範本中所用片段或影像之存放庫中的資料夾路徑。
* *地區*：指定產生的PDF表單的預設地區。
* *Acrobat版本*：為產生的PDF表單指定目標Acrobat版本。
* 線性PDF：指定是否要最佳化產生的PDF以供網頁檢視。
* *已標籤的PDF*：指定是否要讓產生的PDF可供存取。
* *XCI檔案*：指定XCI檔案的路徑。
