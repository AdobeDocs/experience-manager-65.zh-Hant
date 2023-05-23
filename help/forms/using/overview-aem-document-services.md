---
title: 文檔服AEM務概述
seo-title: Overview of AEM Document Services
description: 文AEM檔服務是一組OSGi服務，用於建立、匯編和保護PDF文檔。
seo-description: AEM Document Services are a set of OSGi Services for creating, assembling, and securing PDF Documents.
uuid: 439144b7-f805-4819-9ed9-a6e9e374b5ed
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 10d406db-ac10-479b-b08b-d0735116a12b
docset: aem65
exl-id: 4c8a3877-1a3c-410d-ad1f-69c73ba4fcc1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 0%

---

# 文檔服AEM務概述{#overview-of-aem-document-services}

文AEM檔服務是一組OSGi服務，用於建立、匯編和保護PDF文檔。 文檔服務包含以下服務：

## 輸出服務 {#output-service}

「輸出」服務允許您以不同格式建立文檔，包括PDF、雷射打印機格式和標籤打印機格式。 雷射打印機格式為PostScript和打印機控制語言(PCL)。 以下清單指定標籤打印機格式：

* 斑馬
* Intermec(IPL)
* Datamax(DPL)
* TecToshiba(TPCL)

文檔可以發送到網路打印機、本地打印機或檔案系統上的檔案。 輸出服務將XML表單資料與表單設計合併，以生成文檔。 輸出服務可以生成文檔，而不將XML表單資料合併到文檔中。 但是，主工作流正在將資料合併到文檔中。

>[!NOTE]
>
>通常使用設計器建立表單設計。 有關為輸出服務建立窗體設計的資訊，請參閱設計器幫助。

當使用輸出服務將XML資料與表單設計合併時，結果是非互動式PDF文檔。 非互動式PDF文檔不允許用戶在其欄位中輸入資料。 相反，您可以使用Forms服務建立互動式PDF表單，讓用戶在其欄位中輸入資料。

以下四個輸出服務操作可供使用：

* **生成PDFOuput**:將表單設計與資料合併以生成PDF文檔
* **generatePrintedOutput**:將表單設計與表單資料合併以生成要發送到雷射打印機或標籤網路打印機的文檔

* **generatePDFOutputBatch**:將多個模板與單個調用中的多個資料記錄合併，以生成一批PDF檔案。 還可以通過組合所有PDF來生成單個PDF
* **generatePrintedOutputBatch**:將多個模板與單個調用中的多個資料記錄合併，以生成一批打印文檔(PS、PCL、ZPL、DPL、IPL、TPCL)。 還可以選擇生成單個打印文檔。

## 組合器服務 {#assembler-service}

「匯編器」服務允許您組合、重新排列和增加PDF和XDP文檔，並獲取有關PDF文檔的資訊。 提交到匯編器服務的每個作業都包括文檔說明XML(DDX)文檔、源文檔和外部資源（字串和圖形）。 DDX文檔提供了有關如何使用源文檔生成一組結果文檔的說明。

除上述功能外，匯編器服務：

* 將PDF文檔轉換為PDF/A標準。
* 將PDF forms、XML表單（在設計器中建立）和PDF forms(在Acrobat建立)轉換為PDF/A-1b、PDF/A-2b和PDFA/A-3b。
* 轉換已簽名或未簽名的PDF文檔（需要數字簽名）。
* 驗證PDF/A檔案的符合性，並在必要時轉換它。

### 關於DDX {#about-ddx}

使用匯編器服務時，使用名為「文檔說明XML」(DDX)的基於XML的語言來描述所需的輸出。 DDX是一種聲明性標籤語言，其元素表示文檔的構件。 這些構造塊包括PDF文檔、XDP文檔、XDP表單片段和諸如注釋、書籤和樣式文本等其他元素。

DDX文檔可指定具有以下特徵的結果文檔：

* PDF文檔，該文檔由多個PDF文檔組裝
* 多個PDF文檔與單個PDF文檔分離
* PDFPortfolio，包括自包含的用戶介面和多個PDF和非PDF文檔
* 從多個XDP文檔組裝的XDP文檔
* 包含動態插入到XDP文檔中的XML片段的XDP文檔
* PDF包裝XDP文檔的文檔
* 報告PDF文檔特徵的XML檔案。 報告的特徵包括文本、注釋、表單資料、檔案附件、在PDFPortfolio、書籤和PDF屬性中使用的檔案。 PDF屬性包括表單屬性、頁面輪替和文檔作者。

可以使用DDX將PDF文檔作為文檔裝配或拆卸的一部分進行擴展。 您可以指定以下效果的任意組合：

* 添加或刪除所選頁面上的水印或背景。
* 添加或刪除所選頁面上的頁眉和頁腳。
* 刪除PDF包或PDFPortfolio的結構和導航功能。 結果是單個PDF檔案。
* 重新編號頁面標籤。 頁面標籤通常用於頁面編號。
* 從其他源文檔導入元資料。
* 添加或刪除檔案附件、書籤、連結、注釋和JavaScript。
* 設定初始視圖特徵並優化以在Web上查看。
* 設定加密PDF的權限。
* 旋轉頁面或旋轉並移動頁面上的內容。
* 更改所選頁面的大小。
* 將資料與基於XFA的PDF合併。

可以使用簡單的輸入映射來指定源文檔和結果文檔的位置。 您還可以使用以下外部資料URL類型：

* 檔案
* FTP
* HTTP/HTTPS

## 文檔保障服務 {#doc-assurance-service}

文檔保障服務可幫助您加密和解密文檔、擴展具有其他使用權限的Adobe Reader的功能，以及向文檔添加數字簽名。 您的用戶可以輕鬆地與PDF forms和文檔交互，而您的組織可以提高安全性、歸檔和法規遵從性。

Doc Assurance服務包含三項服務：簽名、加密和讀取器擴展。

### 簽名服務 {#signature-service}

通過簽名服務，您可以在伺服器上使用數字簽名和AEM文檔。 例如，簽名服務通常用於以下情況：

* 伺服器AEM在將表單發送給用戶以使用Acrobat或Adobe Reader開啟之前對表單進行認證。
* 服AEM務器驗證已通過使用Acrobat或Adobe Reader添加到表單的簽名。
* 服AEM務器代表公證員簽署表格。

簽名服務訪問儲存在信任儲存中的證書和憑據。

### 加密服務 {#encryption-service}

加密服務使您能夠加密和解密文檔。 當文檔被加密時，其內容將變得不可讀。 您可以加密整個PDF文檔（包括其內容、元資料和附件）、除其元資料之外的所有內容，或僅加密附件。 授權用戶可以解密文檔以獲得對其內容的訪問。 如果PDF文檔使用密碼進行加密，則用戶必須指定開啟的密碼，然後才能在Adobe Reader或Acrobat查看該文檔。 如果PDF文檔用證書加密，則用戶必須用私鑰（證書）解密PDF文檔。 用於解密PDF文檔的私鑰必須與用於加密文檔的公鑰相對應。

### Reader分機服務 {#reader-extension-service}

Reader擴展服務通過擴展Adobe Reader的功能並附加使用權限，使您的組織能夠輕鬆共用互動式PDF文檔。 Reader分機服務與Adobe Reader7.0或更高版本配合使用。 該服務將使用權限添加到PDF文檔。 此操作將激活在使用Adobe Reader開啟PDF文檔時通常不可用的功能，如向文檔添加註釋、填寫表單和保存文檔。 第三方用戶不需要使用其他軟體或插件來處理啟用權限的文檔。

當PDF文檔添加了相應的使用權限時，收件人可以從Adobe Reader內進行以下活動：

* 完成線上或離線PDF文檔和表單，允許收件人將副本保存到本地以記錄，同時仍保留添加的資訊
* 將PDF文檔保存到本地硬碟，以保留原始文檔和任何附加註釋、資料或附件
* 將檔案和媒體剪輯附加到PDF文檔
* 使用行業標準公鑰基礎架構(PKI)技術應用數字簽名來簽署、認證和驗證PDF文檔
* 以電子方式提交已完成或已注釋的PDF文檔
* 將PDF文檔和表單用作內部資料庫和Web服務的直觀開發前端
* 與他人共用PDF文檔，以便審閱人可以使用直觀的標籤工具添加註釋。 這些工具包括電子便箋、郵票、高光和文本刪除。 Acrobat也提供同樣的功能。
* 支援條形碼格式解碼。

當在Adobe Reader內開啟啟用權限的PDF文檔時，會自動激活這些特殊用戶功能。 當用戶完成使用啟用權限的文檔時，這些功能在Adobe Reader再次被禁用。 在用戶收到另一個啟用權限的PDF文檔之前，這些文檔將保持禁用狀態。

開箱後，DocAssurance服務不可用。 要配置DocAssurance服務，請參見 [安裝和配置配置文檔服務](../../forms/using/install-configure-document-services.md)。

## 發送到打印機服務 {#send-to-printer-service}

「發送到打印機服務」提供API，用於將文檔發送到指定的打印機以進行打印。
