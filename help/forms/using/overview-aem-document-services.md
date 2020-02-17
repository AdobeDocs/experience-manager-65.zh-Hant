---
title: AEM檔案服務概觀
seo-title: AEM檔案服務概觀
description: AEM Document services是一組OSGi Services，可用來建立、組合和保護PDF檔案。
seo-description: AEM Document services是一組OSGi Services，可用來建立、組合和保護PDF檔案。
uuid: 439144b7-f805-4819-9ed9-a6e9e374b5ed
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 10d406db-ac10-479b-b08b-d0735116a12b
docset: aem65
translation-type: tm+mt
source-git-commit: 76908a565bf9e6916db39d7db23c04d2d40b3247

---


# AEM檔案服務概觀{#overview-of-aem-document-services}

AEM Document services是一組OSGi Services，可用來建立、組合和保護PDF檔案。 檔案服務包含下列服務：

## 輸出服務 {#output-service}

「輸出」服務可讓您建立不同格式的檔案，包括PDF、雷射印表機格式和標籤印表機格式。 雷射打印機格式為PostScript和打印機控制語言(PCL)。 以下清單指定標籤打印機格式：

* 澤布拉(ZPL)
* Intermec(IPL)
* Datamax(DPL)
* TecToshiba(TPCL)

文檔可以發送到網路打印機、本地打印機或檔案系統上的檔案。 Output服務將XML表單資料與表單設計合併，以生成文檔。 Output服務可以生成文檔，而不將XML表單資料合併到文檔中。 不過，主要的工作流程是將資料合併到檔案中。

>[!NOTE]
>
>表單設計通常是使用設計工具來建立的。 有關為輸出服務建立表單設計的資訊，請參閱設計器幫助。

使用「輸出」服務將XML資料與表單設計合併時，結果會是非互動式PDF檔案。 非互動式PDF檔案不允許使用者在其欄位中輸入資料。 相反地，您可以使用Forms服務來建立互動式PDF表單，讓使用者在其欄位中輸入資料。

可使用下列四個輸出服務操作：

* **generatePDFOuput**:將表單設計與資料合併，以產生PDF檔案
* **generatePrintedOutput**:將表單設計與表單資料合併，以產生要傳送至雷射或標籤網路印表機的檔案

* **generatePDFOutputBatch**:在單次呼叫中合併多個範本與多個資料記錄，以產生一批PDF檔案。 您也可以選擇將所有PDF組合，以產生單一PDF
* **generatePrintedOutputBatch**:在單次呼叫中合併多個範本與多個資料記錄，以產生一批列印檔案(PS、PCL、ZPL、DPL、IPL、TPCL)。 您也可以選擇產生單一列印檔案。

## Assembler Service {#assembler-service}

Assembler服務可讓您合併、重新排列和增強PDF和XDP檔案，並取得PDF檔案的相關資訊。 提交到Assembler服務的每個作業都包括文檔描述XML(DDX)文檔、源文檔和外部資源（字串和圖形）。 DDX文檔提供了有關如何使用源文檔來生成一組合成文檔的說明。

除了上述功能外，Assembler服務：

* 將PDF檔案轉換為PDF/A標準。
* 將PDF表格、XML表格（在Designer中建立）和PDF表格（在Acrobat中建立）轉換為PDF/A-1b、PDF/A-2b和PDFA/A-3b。
* 轉換已簽署或未簽署的PDF檔案（需要數位簽名）。
* 驗證PDF/A檔案是否符合規範，並視需要進行轉換。

### 關於DDX {#about-ddx}

使用Assembler服務時，請使用名為Document Description XML(DDX)的XML語言來描述所需的輸出。 DDX是宣告性標籤語言，其元素代表檔案的建立區塊。 這些建置區塊包括PDF檔案、XDP檔案、XDP表單片段，以及其他元素，例如註解、書籤和樣式化文字。

DDX文檔可以指定具有以下特徵的合成文檔：

* 從多份PDF檔案組合的PDF檔案
* 從單一PDF檔案分割的多份PDF檔案
* PDF資料夾，包含獨立的使用者介面以及多份PDF和非PDF檔案
* 從多個XDP檔案組合的XDP檔案
* XDP檔案，其中包含動態插入XDP檔案的XML片段
* 封裝XDP檔案的PDF檔案
* 報告PDF檔案特性的XML檔案。 報告的特性包括文字、注釋、表單資料、檔案附件、PDF資料夾中使用的檔案、書籤和PDF屬性。 PDF屬性包括表單屬性、頁面旋轉和檔案作者。

您可以使用DDX來增強PDF檔案，作為檔案裝配或拆卸的一部分。 您可以指定下列特效的任意組合：

* 在選取的頁面上新增或移除浮水印或背景。
* 新增或移除選取頁面上的頁首和頁尾。
* 移除PDF套件或PDF資料夾的結構和導覽功能。 結果是單一PDF檔案。
* 重新編號頁面標籤。 頁面標籤通常用於頁面編號。
* 從其他來源檔案匯入中繼資料。
* 新增或移除檔案附件、書籤、連結、注釋和JavaScript。
* 設定初始檢視特性並最佳化以在Web上檢視。
* 設定加密PDF的權限。
* 旋轉頁面或旋轉並移動頁面上的內容。
* 變更選取頁面的大小。
* 將資料與以XFA為基礎的PDF合併。

您可以使用簡單的輸入映射來指定源文檔和結果文檔的位置。 您也可以使用下列外部資料URL類型：

* 檔案
* FTP
* HTTP/HTTPS

## 檔案保證服務 {#doc-assurance-service}

Doc Assurance service可協助您加密和解密檔案、以額外的使用權限擴充Adobe Reader的功能，並在檔案中新增數位簽章。 您的使用者可輕鬆與PDF表單和檔案互動，而您的組織可改善安全性、封存和合規性。

Doc Assurance服務包含三項服務：簽名、加密和Reader擴充功能。

### 簽名服務 {#signature-service}

「簽名」服務可讓您在AEM伺服器上處理數位簽章和檔案。 例如，簽名服務通常用於下列情況：

* AEM伺服器會在將表單傳送至使用者以使用Acrobat或Adobe Reader開啟之前，先進行認證。
* AEM伺服器會驗證已使用Acrobat或Adobe Reader新增至表單的簽名。
* AEM伺服器代表公證員簽署表格。

簽章服務會存取儲存在信任商店中的憑證和憑證。

### 加密服務 {#encryption-service}

Encryption服務可讓您加密和解密檔案。 當文檔加密時，其內容將變得不可讀。 您可以加密整份PDF檔案（包括其內容、中繼資料和附件）、除中繼資料以外的所有內容，或僅加密附件。 授權用戶可以解密文檔以獲得對其內容的訪問。 如果PDF檔案使用密碼加密，使用者必須先指定開啟的密碼，才能在Adobe Reader或Acrobat中檢視該檔案。 如果PDF檔案使用憑證加密，使用者必須使用私密金鑰（憑證）解密PDF檔案。 用於解密PDF文檔的私密金鑰必須對應於用於加密的公鑰。

### Reader Extension Service {#reader-extension-service}

Reader Extensions服務可讓貴組織透過擴充Adobe Reader的功能及額外的使用權限，輕鬆分享互動式PDF檔案。 Reader Extensions服務可與Adobe Reader 7.0或更新版本搭配使用。 本服務新增PDF檔案的使用權。 此動作會啟動在使用Adobe reader開啟PDF檔案時通常無法使用的功能，例如新增註解至檔案、填寫表單以及儲存檔案。 協力廠商使用者不需要額外的軟體或增效模組，就能使用具版權的檔案。

當PDF檔案已新增適當的使用權限時，收件者可在Adobe Reader中進行下列活動：

* 線上上或離線完成PDF檔案和表單，讓收件者將復本儲存在本機，以保存新增的資訊
* 將PDF檔案儲存至本機硬碟，以保留原始檔案及任何其他注釋、資料或附件
* 將檔案和媒體剪輯附加至PDF檔案
* 使用業界標準的公用金鑰基礎結構(PKI)技術套用數位簽章，以簽署、認證和驗證PDF檔案
* 以電子方式提交已完成或加上註解的PDF檔案
* 將PDF檔案和表格當做內部資料庫和網站服務的直覺式開發前端
* 與其他人共用PDF檔案，讓審核者可使用直覺式標籤工具來新增注釋。 這些工具包括電子便條紙、印章、反白顯示和文字刪除線。 Acrobat提供的功能相同。
* 支援條碼表單解碼。

當Adobe Reader中開啟具權限的PDF檔案時，這些特殊的使用者功能會自動啟動。 當使用者使用完啟用權限的檔案時，這些功能在Adobe Reader中會再次停用。 在使用者收到另一份具權限的PDF檔案之前，這些檔案會一直停用。

現成可用的DocAssurance服務不可用。 要配置DocAssurance服務，請參 [閱安裝和配置文檔服務](../../forms/using/install-configure-document-services.md)。

## 傳送至印表機服務 {#send-to-printer-service}

Send To Printer service提供API，可將檔案傳送至指定的印表機以進行列印。
