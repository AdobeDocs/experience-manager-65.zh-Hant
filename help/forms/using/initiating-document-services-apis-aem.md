---
title: 從AEM工作流程起始檔案服務API
seo-title: Initiate Document Services APIs from AEM Workflow
description: 了解如何在DDX或提供的輸入中叫用AEM檔案服務。 另請參閱如何將PDF轉換為PDF/A
seo-description: Learn how to invoke AEM Document services on DDX or supplied inputs. Also see hwo to convert PDF to PDF/A
uuid: aacec2df-1ad6-4ff2-a99d-ef206efcdc09
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 8b85bdc7-3864-49c9-81b0-cf15b8e986d9
exl-id: 123087a2-9d09-4579-9185-2ccd7d25bf8d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1171'
ht-degree: 0%

---

# 從AEM工作流程起始檔案服務API  {#initiate-document-services-apis-from-aem-workflow}

## 組合器 {#assembler}

AEM Forms提供自訂工作流程，以叫用下列組合器服務API:

* **調用**:調用輸入DDX中指定的對提供的輸入的操作。
* **toPDFA**:將輸入PDF文檔轉換為PDF/A文檔。

### 叫用DDX工作流程 {#invoke-ddx-workflow}

此 **調用DDX** 工作流調用 `Invoke` 組合器服務API，可用於組合或拆卸文檔、向PDF添加水印等。

1. 拖曳 **[!UICONTROL 調用DDX]** 工作流程步驟(在Sidekick中的「Forms Workflow」標籤下)。
1. 按兩下新增的工作流程步驟以編輯元件。
1. 在「編輯元件」對話框中，配置輸入文檔、環境選項和輸出文檔，然後按一下 **[!UICONTROL 確定]**.

#### 輸入文檔 {#input-documents}

調用DDX工作流需要以下輸入文檔：

* **DDX**:它是「調用DDX」工作流步驟的強制輸入，可通過從DDX輸入下拉清單中選擇以下選項之一來指定。

   * *相對於裝載*:DDX輸入檔案相對於工作流程項目的裝載資料夾。
   * *使用裝載*:工作流項的裝載用作輸入DDX文檔。
   * *絕對路徑*:CRX儲存庫中DDX文檔的絕對路徑。

* **從PayLoad建立地圖**:選取後，裝載資料夾下的所有檔案會新增至 `invoke` 組合器中的API。 每個文檔的節點名稱用作映射中的鍵。

* **輸入文檔的映射**:指定輸入文檔的映射。 可以添加任意數量的條目，其中每個條目都在映射和文檔源中指定文檔的鍵。

#### 環境選項 {#environment-options}

「環境選項」索引標籤可讓您為叫用API設定各種處理選項。

* *作業日誌級別*:指定處理記錄的記錄層級。
* *僅驗證*:檢查輸入DDX的有效性。

* *錯誤時失敗*:指定在發生錯誤時，對組合器服務的調用是否應失敗。 預設值為False。

#### 輸出文檔 {#output-documents}

根據輸入DDX，調用API可產生多個輸出文檔。 「輸出文檔」(Output Documents)頁簽允許您選擇輸出文檔的保存位置。

1. *在裝載中儲存輸出*:將輸出檔案儲存在裝載資料夾下，或覆寫裝載（如果裝載是檔案）。
1. *輸出文檔的映射*:允許通過為每個輸出文檔添加一個條目來顯式指定保存每個輸出文檔的位置。 每個條目都指定文檔以及保存文檔的位置。 輸出檔案可以覆寫裝載，或儲存在裝載資料夾下。 當有多個輸出文檔時，它很有用。

1. *作業日誌*:指定保存作業日誌文檔的位置，這有助於故障診斷。

### 轉換為PDF/工作流程 {#convert-to-pdf-a-workflow}

轉換為PDF/工作流步驟調用 `toPDFA` 組合器服務API。 它用於將PDF文檔轉換為PDF/A相容文檔。

1. 拖曳 **[!UICONTROL ConvertToPDFA]** 工作流程步驟(在Sidekick中的「Forms Workflow」標籤下)。

1. 按兩下新增的工作流程步驟以編輯元件。
1. 在「編輯元件」對話框中，配置輸入文檔、轉換選項和輸出文檔，然後按一下 **[!UICONTROL 確定]**.

#### 輸入文檔 {#input-documents-1}

通過以下方式之一指定要轉換為PDF/A相容文檔的文檔源。

* *相對於裝載*:輸入文檔相對於工作流項的裝載資料夾。
* *使用裝載*:工作流程項目的裝載將用作輸入文檔。
* *絕對路徑*:CRX儲存庫中輸入文檔的絕對路徑。

#### 轉換選項 {#conversion-options}

「轉換選項」可讓您指定可改變PDF/A轉換程式的選項。

* *合規性* :指定輸出PDF/A必須符合的PDF/A標準。
* *結果級別* :指定用於PDF/轉換記錄的記錄層級。
* *簽名* :指定在轉換過程中必須如何處理輸入文檔中的簽名。
* *色域* :指定用於輸出PDF/A文檔的預定義顏色空間。
* *驗證* 轉換：指定轉換後是否應驗證轉換的PDF/A文檔以符合PDF/A規範。
* *作業日誌級別* :指定用於處理日誌的日誌級別。

* *中繼資料擴充功能結構* :指定要用於PDF文檔元資料中的XMP屬性的元資料擴展架構的路徑。

#### 輸出文檔 {#output-documents-1}

「輸出文檔」(Output Documents)頁簽允許您指定輸出文檔的目標

* *PDFA檔案*:指定轉換的PDF/A文檔的保存位置。 它可以覆寫裝載檔案或儲存在裝載資料夾下。
* *轉換記錄*:指定轉換記錄檔的儲存位置。 它可以覆寫裝載檔案，或儲存在裝載資料夾下。

## Forms {#forms}

「轉譯PDF表單」工作流程是周圍的包裝函式 `renderPDFForm` Forms服務API，可使用XDP範本和資料xml建立PDF表單。

### 呈現PDF表單工作流 {#render-pdf-form-workflow}

1. 將「呈現PDF表單」工作流步驟拖曳至Sidekick的「Forms Workflow」標籤下。
1. 按兩下新增的工作流程步驟以編輯元件。
1. 在「編輯」元件對話框中，配置輸入文檔、輸出文檔和其他參數，然後按一下 **[!UICONTROL 確定]**.

#### 輸入文檔 {#input-documents-2}

* *範本檔案*:指定XDP範本的位置。 這是必填欄位。

* *資料檔案*:指定需要與模板合併的資料xml的位置。

#### 輸出文檔 {#output-documents-2}

* *輸出文檔*: — 指定生成的PDF表單的名稱。

#### 其他參數 {#additional-parameters}

* *內容根*:指定儲存庫中資料夾的路徑，儲存輸入XDP範本中使用的片段或影像。
* *提交Url*:指定生成的PDF表單的預設提交URL。
* *地區*:指定生成的PDF表單的預設區域設定。
* *Acrobat版本*:指定所產生Acrobat表單的目標PDF版本。
* *標籤PDF*:指定是否讓產生的PDF可供存取。
* *XCI檔案*:指定XCI檔案的路徑。

## 輸出 {#output}

「產生非互動式PDF」工作流程是 `generatePDFOutput` 輸出服務API。 它用於從XDP範本和資料xml產生非互動式PDF檔案。

### 生成非互動式PDF輸出工作流   {#generate-non-interactive-pdf-output-workflow-nbsp}

1. 將「產生非互動式PDF輸出」工作流程拖曳至Sidekick的「Forms Workflow」標籤下。
1. 按兩下新增的工作流程步驟以編輯元件。
1. 在「編輯」元件對話框中，配置輸入文檔、輸出文檔和其他參數，然後按一下 **[!UICONTROL 確定]**.

#### 輸入文檔 {#input-documents-3}

* *範本檔案*:指定XDP範本的位置。 這是必填欄位。

* *資料檔案*:指定需要與模板合併的資料xml的位置。

#### 輸出文檔 {#output-document}

*輸出文檔*:指定生成的PDF表單的名稱。

#### 其他參數 {#additional-parameters-1}

* *內容根*:指定儲存庫中資料夾的路徑，儲存輸入XDP範本中使用的片段或影像。
* *地區*:指定生成的PDF表單的預設區域。
* *Acrobat版本*:指定所產生Acrobat表單的目標PDF版本。
* 線性化PDF:指定是否要最佳化為Web檢視產生的PDF。
* *標籤PDF*:指定是否讓產生的PDF可供存取。
* *XCI檔案*:指定XCI檔案的路徑。
