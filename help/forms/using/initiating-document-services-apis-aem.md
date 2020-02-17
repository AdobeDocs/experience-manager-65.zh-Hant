---
title: 從AEM Workflow啟動檔案服務API
seo-title: 從AEM Workflow啟動檔案服務API
description: 瞭解如何在DDX上叫用AEM檔案服務或提供的輸入。 另請參閱如何將PDF轉換為PDF/A
seo-description: 瞭解如何在DDX上叫用AEM檔案服務或提供的輸入。 另請參閱如何將PDF轉換為PDF/A
uuid: aacec2df-1ad6-4ff2-a99d-ef206efcdc09
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 8b85bdc7-3864-49c9-81b0-cf15b8e986d9
translation-type: tm+mt
source-git-commit: 7caf09f7020c066072eac04a349a19b144dfeb7b

---


# 從AEM Workflow啟動檔案服務API {#initiate-document-services-apis-from-aem-workflow}

## 匯編器 {#assembler}

AEM Forms提供自訂工作流程，以叫用下列Assembler服務API:

* **叫用**:調用在輸入DDX中指定的操作（對提供的輸入）。
* **toPDFA**:將輸入的PDF檔案轉換為PDF/A檔案。

### 叫用DDX工作流程 {#invoke-ddx-workflow}

「叫 **用DDX** 」工作流程會叫用 `Invoke` Assembler服務API，您可使用它來組合或反匯編檔案、在PDF中加入浮水印等。

1. 將「叫 **[!UICONTROL 用DDX]** 」工作流程步驟拖曳至Sidekick中「表單工作流程」標籤下。
1. 連按兩下新增的工作流程步驟以編輯元件。
1. 在「編輯元件」對話框中，配置輸入文檔、環境選項和輸出文檔，然後按一下「確 **[!UICONTROL 定」]**。

#### Input documents {#input-documents}

「叫用DDX」工作流程需要下列輸入檔案：

* **DDX**:它是「叫用DDX」工作流程步驟的必要輸入，可從DDX輸入下拉式清單中選取下列其中一個選項來指定。

   * *相對於負載*:DDX輸入檔案相對於工作流項的裝載資料夾。
   * *使用裝載*:工作流程項目的裝載將用作輸入DDX文檔。
   * *絕對路徑*:CRX儲存庫中DDX文檔的絕對路徑。

* **從PayLoad建立地圖**:選中後，裝載資料夾下的所有文檔都將添加到Assembler中API的「輸入文檔的 `invoke` 映射」中。 每個文檔的節點名稱用作映射中的鍵。

* **輸入文檔的映射**:指定輸入文檔的映射。 您可以添加任意數量的條目，其中每個條目都在映射中指定文檔的鍵和文檔的源。

#### Environment options {#environment-options}

「環境選項」頁籤允許您為調用API設定各種處理選項。

* *作業日誌級別*:指定處理日誌的日誌級別。
* *僅驗證*:檢查輸入DDX的有效性。

* *錯誤時失敗*:指定在發生錯誤時對Assembler服務的調用是否應失敗。 預設值為False。

#### Output documents {#output-documents}

根據輸入DDX，調用API可產生多個輸出檔案。 「輸出文檔」(Output Documents)頁籤允許您選擇輸出文檔的保存位置。

1. *在裝載中保存輸出*:將輸出檔案儲存在裝載檔案夾下，或覆寫裝載（如果裝載為檔案）。
1. *輸出文檔的映射*:允許通過為每個輸出文檔添加一個條目來明確指定保存每個輸出文檔的位置。 每個條目都指定文檔及其保存位置。 輸出文檔可以覆蓋裝載或保存在裝載資料夾下。 當有多個輸出檔案時，此功能很實用。

1. *作業日誌*:指定將作業日誌文檔保存到何處，這有助於排除故障。

### Convert to PDF/A workflow {#convert-to-pdf-a-workflow}

「轉換為PDF/A」工作流程步驟會叫用 `toPDFA` Assembler服務API。 它用於將PDF檔案轉換為PDF/A相容檔案。

1. 將ConvertToPDFA工 **[!UICONTROL 作流程步驟拖曳至]** Sidekick中「表單工作流程」標籤下方。

1. 連按兩下新增的工作流程步驟以編輯元件。
1. 在「編輯元件」對話方塊中，設定輸入檔案、轉換選項和輸出檔案，然後按一下「確 **[!UICONTROL 定」]**。

#### Input documents {#input-documents-1}

指定要轉換為PDF/A相容檔案的檔案來源，方法如下：

* *相對於負載*:輸入文檔相對於工作流項的裝載資料夾。
* *使用裝載*:工作流項目的裝載將用作輸入文檔。
* *絕對路徑*:CRX儲存庫中輸入文檔的絕對路徑。

#### Conversion options {#conversion-options}

「轉換選項」可讓您指定可改變PDF/A轉換程式的選項。

* *符合性* :指定輸出PDF/A必須符合的PDF/A標準。
* *結果層級* :指定用於PDF/A轉換記錄的記錄檔層級。
* *簽名* :指定在轉換期間必須如何處理輸入文檔中的簽名。
* *色域* :指定用於輸出PDF/A文檔的預定義顏色空間。
* *驗證轉換* :指定轉換後是否應驗證轉換的PDF/A檔案是否符合PDF/A規範。
* *作業日誌級別* :指定用於處理日誌的日誌級別。

* *中繼資料擴充功能架構* :指定PDF檔案中繼資料中XMP屬性的中繼資料延伸架構路徑。

#### Output documents {#output-documents-1}

「輸出文檔」(Output Documents)頁籤允許您指定輸出文檔的目標

* *PDFA檔案*:指定轉換的PDF/A文檔的保存位置。 它可以覆寫裝載檔案或儲存在裝載資料夾下。
* *轉換記錄*:指定轉換記錄檔的儲存位置。 它可以覆寫裝載檔案，也可以儲存在裝載檔案夾下。

## 表單 {#forms}

Render PDF Form Workflow是 `renderPDFForm` Forms服務API的包裝函式，可使用XDP範本和資料xml來建立PDF表單。

### 轉換PDF表單工作流程 {#render-pdf-form-workflow}

1. 將「Render PDF Form」工作流程步驟拖曳至Sidekick的「Forms Workflow」（表單工作流程）標籤下。
1. 連按兩下新增的工作流程步驟以編輯元件。
1. 在「編輯元件」對話方塊中，設定輸入檔案、輸出檔案及其他參數，然後按一下「確 **[!UICONTROL 定」]**。

#### Input documents {#input-documents-2}

* *範本檔案*:指定XDP模板的位置。 這是一個強制欄位。

* *資料檔案*:指定需要與模板合併的資料xml的位置。

#### Output documents {#output-documents-2}

* *輸出檔案*:-指定生成的PDF表單的名稱。

#### 其他參數 {#additional-parameters}

* *內容根*:指定儲存庫中儲存輸入XDP模板中使用的片段或影像的資料夾路徑。
* *提交Url*:指定產生的PDF表單的預設提交URL。
* *地區*:指定所生成PDF表單的預設區域設定。
* *Acrobat版本*:指定所產生PDF表單的目標Acrobat版本。
* *標籤的PDF*:指定是否讓產生的PDF可供存取。
* *XCI檔案*:指定XCI檔案的路徑。

## 輸出 {#output}

「產生非互動式PDF工作流程」是 `generatePDFOutput` Output service API的包裝函式。 它用來從XDP範本和資料xml產生非互動式PDF檔案。

### 產生非互動式PDF輸出工作流程 {#generate-non-interactive-pdf-output-workflow-nbsp}

1. 將「產生非互動式PDF輸出」工作流程拖曳至Sidekick的「表單工作流程」標籤下。
1. 連按兩下新增的工作流程步驟以編輯元件。
1. 在「編輯元件」對話方塊中，設定輸入檔案、輸出檔案及其他參數，然後按一下「確 **[!UICONTROL 定」]**。

#### Input documents {#input-documents-3}

* *範本檔案*:指定XDP模板的位置。 這是一個強制欄位。

* *資料檔案*:指定需要與模板合併的資料xml的位置。

#### Output document {#output-document}

*輸出檔案*:指定所生成PDF表單的名稱。

#### 其他參數 {#additional-parameters-1}

* *內容根*:指定儲存庫中儲存輸入XDP模板中使用的片段或影像的資料夾路徑。
* *地區*:指定所生成PDF表單的預設地區。
* *Acrobat版本*:指定所產生PDF表單的目標Acrobat版本。
* 線性化PDF:指定是否最佳化產生的PDF以供網頁檢視。
* *標籤的PDF*:指定是否讓產生的PDF可供存取。
* *XCI檔案*:指定XCI檔案的路徑。

