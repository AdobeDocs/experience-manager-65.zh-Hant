---
title: 從工作流啟動文檔服務APIAEM
seo-title: Initiate Document Services APIs from AEM Workflow
description: 瞭解如何在DDX或AEM提供的輸入中調用文檔服務。 另請參閱如何將PDF轉換為PDF/A
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

# 從工作流啟動文檔服務APIAEM  {#initiate-document-services-apis-from-aem-workflow}

## 組合器 {#assembler}

AEM Forms提供自定義工作流以調用以下匯編器服務API:

* **調用**:調用在輸入DDX中指定的對提供的輸入的操作。
* **到PDFA**:將輸入PDF文檔轉換為PDF/A文檔。

### 調用DDX工作流 {#invoke-ddx-workflow}

的 **調用DDX** 工作流調用 `Invoke` 匯編程式服務API，可用於匯編或拆解文檔、向PDF添加水印等。

1. 拖動 **[!UICONTROL 調用DDX]** Forms Workflow頁籤下的工作流步驟。
1. 按兩下添加的工作流步驟以編輯元件。
1. 在「編輯」元件對話框中，配置輸入文檔、環境選項和輸出文檔，然後按一下 **[!UICONTROL 確定]**。

#### 輸入文檔 {#input-documents}

「調用DDX」工作流需要以下輸入文檔：

* **DDX**:它是調用DDX工作流步驟的必需輸入，可通過從DDX輸入下拉清單中選擇以下選項之一來指定。

   * *相對負載*:DDX輸入檔案相對於工作流項的負載資料夾。
   * *使用負載*:工作流項的負載用作輸入DDX文檔。
   * *絕對路徑*:CRX儲存庫中DDX文檔的絕對路徑。

* **從PayLoad建立映射**:選中後，有效負載資料夾下的所有文檔將添加到輸入文檔的映射中 `invoke` 匯編器中的API。 每個文檔的節點名稱用作映射中的鍵。

* **輸入文檔的映射**:指定輸入文檔的映射。 您可以添加任意數量的條目，其中每個條目都指定映射中文檔的鍵和文檔的源。

#### 環境選項 {#environment-options}

「環境選項」頁籤允許您為調用API設定各種處理選項。

* *作業日誌級別*:指定處理日誌的日誌級別。
* *僅驗證*:檢查輸入DDX的有效性。

* *錯誤時失敗*:指定在出現錯誤時對匯編器服務的調用是否應失敗。 預設值為False。

#### 輸出文檔 {#output-documents}

根據輸入DDX，調用API可以生成多個輸出文檔。 「輸出文檔」(Output Documents)頁籤允許您選擇輸出文檔的保存位置。

1. *在負載中保存輸出*:將輸出文檔保存到負載資料夾下，或覆蓋負載（如果負載是檔案）。
1. *輸出文檔的映射*:允許通過為每個輸出文檔添加一個條目來明確指定保存每個輸出文檔的位置。 每個條目都指定文檔及其保存位置。 輸出文檔可以覆蓋負載或保存在負載資料夾下。 當存在多個輸出文檔時，它非常有用。

1. *作業日誌*:指定將作業日誌文檔保存到何處，這有助於排除故障。

### 轉換為PDF/A工作流 {#convert-to-pdf-a-workflow}

「轉換為PDF/A」工作流步驟調用 `toPDFA` 匯編程式服務API。 它用於將PDF文檔轉換為PDF/A相容文檔。

1. 拖動 **[!UICONTROL 轉換為PDFA]** Forms Workflow頁籤下的工作流步驟。

1. 按兩下添加的工作流步驟以編輯元件。
1. 在「編輯」元件對話框中，配置輸入文檔、轉換選項和輸出文檔，然後按一下 **[!UICONTROL 確定]**。

#### 輸入文檔 {#input-documents-1}

通過以下方法之一指定要轉換為PDF/A相容文檔的文檔的源。

* *相對負載*:輸入文檔相對於工作流項的負載資料夾。
* *使用負載*:工作流項的負載用作輸入文檔。
* *絕對路徑*:CRX儲存庫中輸入文檔的絕對路徑。

#### 轉換選項 {#conversion-options}

「轉換選項」(Conversion Options)允許您指定可改變PDF/A轉換過程的選項。

* *合規性* :指定輸出PDF/A必須符合的PDF/A標準。
* *結果級別* :指定用於PDF/A轉換日誌的日誌級別。
* *簽名* :指定在轉換過程中必須如何處理輸入文檔中的簽名。
* *顏色空間* :指定用於輸出PDF/A文檔的預定義顏色空間。
* *驗證* 轉換：指定是否應在轉換後驗證轉換的PDF/A文檔是否符合PDF/A。
* *作業日誌級別* :指定用於處理日誌的日誌級別。

* *元資料擴展架構* :指定用於PDF文檔元資料中屬XMP性的元資料擴展架構的路徑。

#### 輸出文檔 {#output-documents-1}

「輸出文檔」(Output Documents)頁籤允許您指定輸出文檔的目標

* *PDFA文檔*:指定保存轉換的PDF/A文檔的位置。 它可以覆蓋負載文檔或保存在負載資料夾下。
* *轉換日誌*:指定保存轉換日誌的位置。 它可以覆蓋負載文檔，也可以保存在負載資料夾下。

## Forms {#forms}

「呈現PDF表單」工作流是圍繞的包裝 `renderPDFForm` Forms服務API，用於使用XDP模板和資料xml建立PDF表單。

### 呈現PDF表單工作流 {#render-pdf-form-workflow}

1. 將「渲染PDF表單」工作流步驟拖到「邊」(Sidek)中的「Forms Workflow」(Render)頁籤下。
1. 按兩下添加的工作流步驟以編輯元件。
1. 在「編輯」元件對話框中，配置輸入文檔、輸出文檔和其他參數，然後按一下 **[!UICONTROL 確定]**。

#### 輸入文檔 {#input-documents-2}

* *模板檔案*:指定XDP模板的位置。 這是一個強制欄位。

* *資料文檔*:指定需要與模板合併的資料xml的位置。

#### 輸出文檔 {#output-documents-2}

* *輸出文檔*: — 指定生成的PDF窗體的名稱。

#### 其他參數 {#additional-parameters}

* *內容根*:指定儲存輸入XDP模板中使用的片段或影像的儲存庫中資料夾的路徑。
* *提交URL*:指定生成的PDF表單的預設提交URL。
* *區域設定*:指定生成的PDF窗體的預設區域設定。
* *Acrobat版*:指定生成的Acrobat表單的目標PDF版本。
* *標籤PDF*:指定是否使生成的PDF可訪問。
* *XCI文檔*:指定XCI檔案的路徑。

## 輸出 {#output}

「生成非交互PDF工作流」是圍繞的包裝 `generatePDFOutput` 輸出服務API。 它用於從XDP模板和資料xml生成非交互PDF文檔。

### 生成非互動式PDF輸出工作流   {#generate-non-interactive-pdf-output-workflow-nbsp}

1. 將「生成非交互PDF輸出」工作流拖到Sidek中的「Forms Workflow」頁籤下。
1. 按兩下添加的工作流步驟以編輯元件。
1. 在「編輯」元件對話框中，配置輸入文檔、輸出文檔和其他參數，然後按一下 **[!UICONTROL 確定]**。

#### 輸入文檔 {#input-documents-3}

* *模板檔案*:指定XDP模板的位置。 這是一個強制欄位。

* *資料文檔*:指定需要與模板合併的資料xml的位置。

#### 輸出文檔 {#output-document}

*輸出文檔*:指定生成的PDF窗體的名稱。

#### 其他參數 {#additional-parameters-1}

* *內容根*:指定儲存輸入XDP模板中使用的片段或影像的儲存庫中資料夾的路徑。
* *區域設定*:指定生成的PDF窗體的預設區域設定。
* *Acrobat版*:指定生成的Acrobat表單的目標PDF版本。
* 線性化PDF:指定是否優化生成的Web查看PDF。
* *標籤PDF*:指定是否使生成的PDF可訪問。
* *XCI文檔*:指定XCI檔案的路徑。
