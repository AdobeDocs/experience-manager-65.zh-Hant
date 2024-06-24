---
title: AEM檔案服務概觀
description: AEM Document Services是一組OSGi服務，用於建立、彙編和保護PDF檔案。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
docset: aem65
feature: Document Services,Reader Extensions, Forms Service,PDF Generator
exl-id: 4c8a3877-1a3c-410d-ad1f-69c73ba4fcc1
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 1%

---

# AEM檔案服務概觀{#overview-of-aem-document-services}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html) |
| AEM 6.5 | 本文章 |


AEM Document Services是一組OSGi服務，用於建立、彙編和保護PDF檔案。 檔案服務包含下列服務：

## 輸出服務 {#output-service}

「輸出」服務可讓您建立不同格式的檔案，包括PDF、雷射印表機格式及標籤印表機格式。 雷射印表機格式為PostScript和Printer Control Language (PCL)。 下列清單指定標籤印表機格式：

* 斑馬(ZPL)
* Intermec (IPL)
* Datamax (DPL)
* 東芝科技(TPCL)

檔案可以傳送到網路印表機、本機印表機或檔案系統上的檔案。 Output服務會合併XML表單資料與表單設計以產生檔案。 Output服務可以產生檔案，而無需將XML表單資料合併到檔案中。 不過，主要工作流程是將資料合併至檔案。

>[!NOTE]
>
>表單設計通常使用Designer來建立。 如需有關為Output服務建立表單設計的資訊，請參閱Designer說明。

使用Output服務將XML資料與表單設計合併時，結果會產生非互動式PDF檔案。 非互動式PDF檔案不允許使用者在其欄位中輸入資料。 相反地，您可以使用Forms服務建立互動式PDF表單，讓使用者在其欄位中輸入資料。

下列四個Output服務作業可供使用：

* **generatePDFOuput**：合併表單設計與資料以產生PDF檔案
* **generatePrintedOutput**：將表單設計與表單資料合併，以產生檔案以傳送至雷射或標籤網路印表機

* **generatePDFOutputBatch**：以單一叫用合併具有多個資料記錄的多個範本，以產生一批PDF檔案。 您也可以選擇合併所有PDF，以產生單一PDF
* **generatePrintedOutputBatch**：在單一叫用中將多個範本與多個資料記錄合併，以產生一批列印檔案(PS、PCL、ZPL、DPL、IPL、TPCL)。 也可以選擇產生單一列印檔案。

## 組合器服務 {#assembler-service}

組合器服務可讓您組合、重新排列和增加PDF和XDP檔案，並取得有關PDF檔案的資訊。 提交至組合器服務的每個工作都包含檔案描述XML (DDX)檔案、來原始檔及外部資源（字串與圖形）。 DDX檔案提供如何使用來原始檔來產生一組結果檔案的指示。

除了上述功能以外，組裝程式服務也提供：

* 將PDF檔案轉換為PDF/A標準。
* 將PDF forms、XML表單(在Designer中建立)和PDF forms(在Acrobat中建立)轉換為PDF/A-1b、PDF/A-2b和PDFA/A-3b。
* 轉換已簽署或未簽署的PDF檔案（需要數位簽名）。
* 驗證PDF/A檔案的合規性，並視需要轉換它。

### 關於DDX {#about-ddx}

使用「組合器」服務時，請使用名為「檔案描述XML (DDX)」的XML語言來描述您想要的輸出。 DDX是一種宣告式標籤語言，其元素代表檔案的建置組塊。 這些建置區塊包括PDF檔案、XDP檔案、XDP表單片段和其他元素，例如註解、書籤和樣式化文字。

DDX檔案可以指定具有以下特性的結果檔案：

* 從多個PDF檔案組裝的PDF檔案
* 與單一PDF檔案分開的多個PDF檔案
* 包含獨立使用者介面以及多個PDF和非PDF檔案的PDFPortfolio
* 從多個XDP檔案組合的XDP檔案
* 包含動態插入XDP檔案之XML片段的XDP檔案
* 封裝XDP檔案的PDF檔案
* 報告PDF檔案特性的XML檔案。 報告的特性包括文字、註釋、表單資料、檔案附件、PDFPortfolio中使用的檔案、書籤和PDF屬性。 PDF屬性包括表單屬性、頁面旋轉和檔案作者。

您可以使用DDX來增加PDF檔案，作為檔案元件或拆解的一部分。 您可以指定下列效果的任意組合：

* 在選取的頁面上新增或移除浮水印或背景。
* 在選取的頁面上新增或移除頁首與頁尾。
* 移除PDF封裝或PDFPortfolio的結構和導覽功能。 結果會是單一PDF檔案。
* 重新編號頁面標籤。 頁面標籤通常用於頁碼編排。
* 從其他來原始檔匯入中繼資料。
* 新增或移除檔案附件、書籤、連結、註解和JavaScript。
* 設定初始檢視特性並最佳化以利在網頁上檢視。
* 設定加密PDF的許可權。
* 旋轉頁面或在頁面上旋轉和移動內容。
* 變更所選頁面的大小。
* 將資料與XFA型PDF合併。

您可以使用簡單的輸入對映來指定來源和結果檔案的位置。 您也可以使用下列外部資料URL型別：

* 檔案
* FTP
* HTTP/HTTPS

## 檔案保證服務 {#doc-assurance-service}

檔案保證服務可協助您加密和解密檔案、透過其他使用許可權擴充Adobe Reader功能，以及將數位簽名新增至檔案。 您的使用者可以輕鬆與PDF forms和檔案互動，而您的組織則可改善安全性、封存和合規性。

Doc Assurance服務包含三種服務：簽名、加密和讀取器延伸。

### 簽章服務 {#signature-service}

簽名服務可讓您在AEM伺服器上處理數位簽名和檔案。 例如，簽章服務通常用於以下情況：

* AEM伺服器會先認證表單，再將表單傳送給使用者，以使用Acrobat或Adobe Reader開啟。
* AEM伺服器會使用Acrobat或Adobe Reader驗證已新增至表單的簽名。
* AEM伺服器代表公用公證員簽署表格。

簽章服務會存取儲存在信任存放區中的憑證和認證。

### 加密服務 {#encryption-service}

加密服務可讓您加密和解密檔案。 檔案加密後，其內容會變得無法讀取。 您可以加密整個PDF檔案（包括其內容、中繼資料及附件）、其中繼資料以外的所有內容，或僅加密附件。 授權的使用者可以解密檔案以取得其內容的存取權。 如果PDF檔案已使用密碼加密，使用者必須先指定開啟的密碼，才能在Adobe Reader或Acrobat中檢視檔案。 如果使用憑證加密PDF檔案，使用者必須使用私密金鑰（憑證）解密PDF檔案。 用來解密PDF檔案的私密金鑰必須對應到用來加密它的公開金鑰。

### Reader延伸服務 {#reader-extension-service}

Reader擴充功能可透過擴充具有其他使用許可權的Adobe Reader功能，讓您的組織輕鬆共用互動式PDF檔案。 Reader擴充功能服務可與Adobe Reader 7.0或更新版本搭配使用。 此服務會將使用許可權新增至PDF檔案。 此動作會啟動在使用Adobe Reader開啟PDF檔案時通常無法使用的功能，例如新增註釋至檔案、填寫表單和儲存檔案。 協力廠商使用者不需要其他軟體或外掛程式即可使用啟用許可權的檔案。

當PDF檔案新增了適當的使用許可權時，收件者可以在Adobe Reader中執行下列活動：

* 線上上或離線完成PDF檔案和表單，讓收件者可在本機儲存復本以做為記錄，同時仍完整保留新增的資訊
* 將PDF檔案儲存至本機硬碟，以保留原始檔案及任何其他註解、資料或附件
* 將檔案和媒體剪輯附加至PDF檔案
* 使用業界標準的公開金鑰基礎結構(PKI)技術套用數位簽名，簽署、認證和驗證PDF檔案
* 以電子方式提交已完成或附註的PDF檔案
* 使用PDF檔案和表單作為內部資料庫和Web服務的直覺式開發前端
* 與其他人共用PDF檔案，讓檢閱者可以使用直覺式的標籤工具來新增註解。 這些工具包括電子註解、印章、醒目提示和文字刪除線。 Acrobat提供相同功能。
* 支援條碼式表單解碼。

在Adobe Reader中開啟許可權啟用的PDF檔案時，會自動啟用這些特殊使用者功能。 當使用者完成使用已啟用許可權的檔案時，這些功能在Adobe Reader中會再次停用。 除非使用者收到其他已啟用許可權的PDF檔案，否則這些功能會維持停用狀態。

開箱即用的DocAssurance服務無法使用。 若要設定DocAssurance服務，請參閱 [安裝和配置配置檔案服務](../../forms/using/install-configure-document-services.md).

## 傳送至印表機服務 {#send-to-printer-service}

「傳送至印表機服務」提供API，可將檔案傳送至指定的印表機進行列印。
