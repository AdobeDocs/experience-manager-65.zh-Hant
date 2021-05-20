---
title: AEM檔案服務概觀
seo-title: AEM檔案服務概觀
description: AEM檔案服務是一組OSGi服務，用於建立、組裝和保護PDF檔案。
seo-description: AEM檔案服務是一組OSGi服務，用於建立、組裝和保護PDF檔案。
uuid: 439144b7-f805-4819-9ed9-a6e9e374b5ed
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 10d406db-ac10-479b-b08b-d0735116a12b
docset: aem65
exl-id: 4c8a3877-1a3c-410d-ad1f-69c73ba4fcc1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1423'
ht-degree: 0%

---

# AEM Document Services概述{#overview-of-aem-document-services}

AEM檔案服務是一組OSGi服務，用於建立、組裝和保護PDF檔案。 文檔服務包含以下服務：

## 輸出服務 {#output-service}

「輸出」服務可讓您以不同格式建立文檔，包括PDF、雷射打印機格式和標籤打印機格式。 雷射打印機格式為PostScript和打印機控制語言(PCL)。 以下清單指定標籤打印機格式：

* 澤布拉(ZPL)
* Intermec(IPL)
* Datamax(DPL)
* TecToshiba(TPCL)

文檔可以發送到網路打印機、本地打印機或檔案系統上的檔案。 輸出服務將XML表單資料與表單設計合併，以生成文檔。 輸出服務可以生成文檔，而無需將XML表單資料合併到文檔中。 但是，主要工作流正在將資料合併到文檔中。

>[!NOTE]
>
>表單設計通常由設計工具建立。 有關為輸出服務建立表單設計的資訊，請參閱設計器幫助。

使用輸出服務將XML資料與表單設計合併時，結果會是非互動式PDF檔案。 非互動式PDF檔案不會讓使用者在其欄位中輸入資料。 相反地，您可以使用Forms服務建立互動式PDF表單，讓使用者在其欄位中輸入資料。

以下四個輸出服務操作可供使用：

* **generatePDFOuput**:將表單設計與資料合併，以產生PDF檔案
* **generatePrintedOutput**:將表單設計與表單資料合併，生成要發送到雷射打印機或標籤網路打印機的文檔

* **generatePDFOutputBatch**:在單一叫用中合併多個範本和多個資料記錄，以產生一批PDF檔案。您也可以選擇合併所有PDF，以產生單一PDF
* **generatePrintedOutputBatch**:在一個調用中合併多個模板和多個資料記錄，以生成一批打印文檔(PS、PCL、ZPL、DPL、IPL、TPCL)。還可以選擇生成單個打印文檔。

## 組合器服務 {#assembler-service}

組合器服務可讓您組合、重新排列和擴展PDF和XDP文檔，並獲取有關PDF文檔的資訊。 提交到組合器服務的每個作業都包括文檔描述XML(DDX)文檔、源文檔和外部資源（字串和圖形）。 DDX文檔提供了如何使用源文檔生成一組生成的文檔的說明。

除了上述功能外，組合器服務：

* 將PDF文檔轉換為PDF/A標準。
* 將PDF forms、XML表單（在Designer中建立）和PDF forms(在Acrobat中建立)轉換為PDF/A-1b、PDF/A-2b和PDFA/A-3b。
* 轉換已簽名或未簽名的PDF文檔（需要數字簽名）。
* 驗證PDF/A檔案的合規性，並視需要轉換。

### 關於DDX {#about-ddx}

使用組合器服務時，使用基於XML的語言(稱為Document Description XML(DDX))來描述要的輸出。 DDX是一種聲明性標注語言，其元素表示文檔的構成塊。 這些建置區塊包括PDF檔案、XDP檔案、XDP表單片段，以及其他元素，例如註解、書籤和已設定樣式的文字。

DDX文檔可以指定具有以下特徵的生成文檔：

* 從多個PDF文檔組合的PDF文檔
* 從單一PDF檔案分割的多個PDF檔案
* PDFPortfolio，包含自成一體的使用者介面以及多個PDF和非PDF檔案
* 從多個XDP文檔組合的XDP文檔
* 包含動態插入XDP檔案之XML片段的XDP檔案
* 封裝XDP檔案的PDF檔案
* 報告PDF文檔特性的XML檔案。 報告的特性包括文本、注釋、表單資料、檔案附件、PDFPortfolio中使用的檔案、書籤和PDF屬性。 PDF屬性包括表單屬性、頁面旋轉和檔案作者。

可以使用DDX將PDF文檔擴展為文檔裝配或拆卸的一部分。 您可以指定下列效果的任何組合：

* 在選定頁面上添加或刪除水印或背景。
* 在選取的頁面上新增或移除頁首與頁尾。
* 移除PDF套件或PDFPortfolio的結構和導覽功能。 結果會是單一PDF檔案。
* 重新編號頁面標籤。 頁面標籤通常用於頁面編號。
* 從其他源文檔導入元資料。
* 新增或移除檔案附件、書籤、連結、註解和JavaScript。
* 設定初始檢視特性並最佳化以在網路上檢視。
* 設定加密PDF的權限。
* 旋轉頁面或旋轉並移動頁面上的內容。
* 變更選取頁面的大小。
* 將資料與XFA型PDF合併。

可以使用簡單的輸入映射來指定源文檔和結果文檔的位置。 您也可以使用下列外部資料URL類型：

* 檔案
* FTP
* HTTP/HTTPS

## 文檔保障服務{#doc-assurance-service}

檔案保證服務可協助您加密及解密檔案、以其他使用權限擴充Adobe Reader的功能，以及為檔案新增數位簽名。 您的用戶可以輕鬆地與PDF forms和文檔交互，而您的組織可以改進安全性、歸檔和法規遵從性。

Doc Assurance服務包含三項服務：簽名、加密和讀取器擴展。

### 簽名服務{#signature-service}

簽名服務可讓您在AEM伺服器上使用數位簽名和文檔。 例如，簽名服務通常用於以下情況：

* AEM伺服器會先驗證表單，再傳送給使用者，供使用Acrobat或Adobe Reader開啟。
* AEM伺服器會使用Acrobat或Adobe Reader驗證已新增至表單的簽名。
* AEM伺服器代表公證人簽署表格。

簽名服務訪問儲存在信任儲存中的證書和憑據。

### 加密服務 {#encryption-service}

加密服務使您能夠加密和解密文檔。 文檔被加密後，其內容將變得不可讀。 您可以加密整個PDF文檔（包括其內容、元資料和附件）、除元資料外的所有內容，或僅加密附件。 授權用戶可以解密該文檔以獲得對其內容的訪問。 如果PDF檔案使用密碼加密，使用者必須先指定開啟的密碼，才能在Adobe Reader或Acrobat中檢視該檔案。 如果PDF檔案使用憑證加密，使用者必須以私密金鑰（憑證）解密PDF檔案。 用於解密PDF檔案的私密金鑰必須對應至用於加密檔案的公開金鑰。

### Reader擴展服務{#reader-extension-service}

Reader延伸模組服務可讓您的組織透過擴充Adobe Reader的功能與其他使用權限，輕鬆共用互動式PDF檔案。 Reader擴充功能服務適用於Adobe Reader 7.0或更新版本。 此服務將使用權限新增至PDF檔案。 此操作會激活在使用Adobe Reader開啟PDF文檔時通常不可用的功能，例如向文檔添加註釋、填寫表單和保存文檔。 協力廠商使用者不需要其他軟體或外掛程式，即可使用啟用權限的檔案。

新增PDF檔案的適當使用權限後，收件者可從Adobe Reader中進行下列活動：

* 線上或離線完成PDF檔案和表單，讓收件者可將副本儲存在本機，以備記錄之用，並仍保留新增的資訊不變
* 將PDF檔案儲存至本機硬碟，以保留原始檔案和任何其他註解、資料或附件
* 將檔案和媒體剪輯附加到PDF文檔
* 使用業界標準的公開金鑰基礎結構(PKI)技術應用數位簽名，對PDF文檔進行簽名、認證和驗證
* 以電子方式提交完整或加上註解的PDF檔案
* 將PDF檔案和表單作為內部資料庫和網站服務的直觀開發前端
* 與他人共用PDF文檔，使審閱者可以使用直觀的標注工具添加註釋。 這些工具包括電子便箋、郵票、醒目提示和文字刪除。 Acrobat提供相同的功能。
* 支援條碼式表單解碼。

在Adobe Reader中開啟啟用權限的PDF檔案時，系統會自動啟用這些特殊使用者功能。 當使用者完成使用已啟用權限的檔案時，這些函式在Adobe Reader中會再次停用。 在使用者收到其他已啟用權限的PDF檔案前，這些檔案仍會停用。

DocAssurance服務現成無法使用。 要配置DocAssurance服務，請參閱[安裝和配置文檔服務](../../forms/using/install-configure-document-services.md)。

## 發送到打印機服務{#send-to-printer-service}

「發送到打印機服務」提供API，用於將文檔發送到指定的打印機以進行打印。
