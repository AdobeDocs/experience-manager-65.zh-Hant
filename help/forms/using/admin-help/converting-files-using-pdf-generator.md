---
title: 使用PDF產生器轉換檔案
seo-title: 使用PDF產生器轉換檔案
description: 瞭解如何使用PDF Generator轉換檔案。
seo-description: 瞭解如何使用PDF Generator轉換檔案。
uuid: 295afb8f-130a-44f5-b0ab-e4c93c0c9e52
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 999ae2be-56ba-48c1-861b-8d4c991a0206
translation-type: tm+mt
source-git-commit: d3719a9ce2fbb066f99445475af8e1f1e7476f4e

---


# 使用PDF產生器轉換檔案{#converting-files-using-pdf-generator}

您可以使用PDF產生器網頁來轉換檔案。

## 建立PDF檔案 {#create-a-pdf-file}

1. 在管理控制台中，按一下「服務> PDF產生器>建立PDF」。
1. 按一下「瀏覽」以尋找並選取檔案。

   >[!NOTE]
   >
   >PDF產生器可自動偵測。doc、.xls、.ppt和。rtf檔案的檔案類型，即使檔案名稱遺失副檔名亦然。 此功能無法用於。docx、.xlsx和。pptx檔案。

1. 在「設定設定」下方，選取「使用自訂設定」或「上傳設定檔」。

   * 如果您使用自訂設定，請選取Adobe PDF設定、安全性設定和檔案類型設定，並指定逾時。

      Adobe PDF設定僅適用於PS-to-PDF、EPS-to-PDF、PRN-to-PDF、使用OCR的影像-PDF，以及原生-PDF轉換。 逾時設定會指定轉換完成所需的最長時間。 預設值為270秒。 這些設定不會在影像轉PDF和OpenOffice轉PDF時使用。

   * 如果您要上傳設定檔案，請在方塊中輸入其路徑和名稱，或按一下「瀏覽」尋找並選取檔案。

1. （可選）在「XMP中繼資料檔案」下方，輸入XMP檔案的路徑和名稱，或按一下「瀏覽」尋找並選取檔案。 XMP檔案可用來包含標準中繼資料資訊。 (請參 [閱關於XMP檔案](converting-files-using-pdf-generator.md#about-xmp-files)。)
1. 按一下「建立」。建立檔案時，將顯示指向該檔案的連結。 如果轉換期間發生錯誤，會出現警告。 如果您正在建立Postscript檔案，則警告還包含指向日誌檔案的連結。
1. 按一下PDF檔案的連結。 檔案會在Acrobat中開啟。

### 關於XMP檔案 {#about-xmp-files}

PDF產生器在Acrobat 5.0或更新版本中建立的PDF檔案包含XML格式的檔案中繼資料。 *中繼資料* (Metadata)包含有關檔案及其內容的資訊，例如作者的名稱、關鍵字，以及搜尋公用程式可使用的版權資訊。

檔案中繼資料包含（但不限於）也會出現在Acrobat「檔案屬性」對話方塊的「說明」標籤上的資訊。 在「說明」標籤上所做的變更會反映在檔案中繼資料中。 使用協力廠商產品可擴充和修改檔案中繼資料。

Adobe Extensible Metadata Platform(XMP)為Adobe應用程式提供通用的XML架構，可標準化檔案中繼資料在出版工作流程中的建立、處理和交換。 您可以儲存並匯入XMP格式的檔案中繼資料XML原始碼，讓您輕鬆在各種檔案之間共用中繼資料。 如需XMP檔案的詳細資訊，請參 [閱可擴充中繼資料平台(XMP)](https://www.adobe.com/products/xmp/)[和Adobe XMP開發人員中心](https://www.adobe.com/devnet/xmp.html)。

您可以在Acrobat中建立XMP檔案。

## 將HTML檔案或ZIP檔案轉換為PDF {#convert-an-html-file-or-zip-file-to-pdf}

您可以使用PDF產生器，將下列類型的檔案轉換為Adobe PDF:

* HTML檔案，您可以透過上傳HTML檔案或指定網頁或網站的URL來轉換。
* 封存檔案(ZIP)，可包含HTML檔案、影像檔或兩者。

如果ZIP檔案在其檔案夾階層的最低層級包含多個HTML檔案，則ZIP檔案也必須包含index.htm或index.html檔案。

>[!NOTE]
>
>HTML至PDF功能需要系統字型目錄中的特定字型。 在Linux、Solaris和AIX系統上，系統字型目錄必須包含Courier字型。 在Windows系統上，系統字型目錄必須包含Times New Roman。

>[!NOTE]
>
>若要從本機檔案系統上傳檔案，請使用HTML至PDF頁面上的「上傳檔案」選項。

1. 在管理控制台中，按一下「服務> PDF產生器> HTML至PDF」。
1. 執行下列任一任務，指定要轉換的檔案：

   * 在「上傳檔案」中，輸入HTML檔案或ZIP檔案的路徑和檔案名稱，或按一下「瀏覽」以尋找並選取它。
   * 在「指定URL」方塊中，輸入要轉換的頁面或網站的URL。

      ***注意&#x200B;**:您要轉換的檔案必須副檔名為。html、.htm或。zip。*

1. 指定配置設定：

   * 若要使用自訂設定，請選取「使用自訂設定」、指定安全性和檔案類型設定，並指定逾時值。 預設值為270秒。

      **注意**:如果您設定「產生PDF」服務以使用Acrobat webCapture，您在此頁面上選取的「檔案類型設定」不會影響產生的PDF。 請改為對伺服器上安裝的Acrobat版本進行適當變更。

   * 若要使用現有的設定檔案，請選取「上傳設定檔案」，然後按一下「瀏覽」前往檔案位置。

1. 若要上傳XMP檔案，請按一下「瀏覽」並移至檔案位置。 XMP檔案可用來包含標準中繼資料資訊。 (請參 [閱關於XMP檔案](converting-files-using-pdf-generator.md#about-xmp-files)。)
1. 按一下「建立」。建立檔案時，會出現PDF檔案的連結。
1. 按一下連結，在Acrobat中檢視PDF檔案。

## 將PDF檔案匯出為其他檔案格式（僅限Windows） {#export-a-pdf-file-to-another-file-format-windows-only}

您可以將PDF檔案匯出為各種檔案格式，如「服務參考」的「產生PDF服務」一章 [所述](https://www.adobe.com/go/learn_aemforms_services_63)。

1. 在管理控制台中，按一下「服務> PDF產生器>匯出PDF」。
1. 按一下「瀏覽」以找出要匯出的PDF檔案。
1. 在「將PDF檔案匯出至」清單中，選取要將PDF檔案匯出至的格式。
1. 在「指定逾時」方塊中，輸入在應用程式逾時之前等待的時間。 預設值為270秒。

   轉換檔案時顯示的轉換時間可能會大於您在此處指定的值。 「轉換時間」包括等待線程或進程所花費的時間、轉換檔案所花費的時間，以及備援轉換器所花費的時間（如果適用）。 次. 「指定逾時」值只是轉換檔案所花的時間。

1. （可選）在「指定自 **訂預檢設定檔** 」選項中，按一下「瀏覽」，然後選取自 [訂的預檢設定檔](https://helpx.adobe.com/acrobat/using/preflight-profiles-acrobat-pro.html)。 預檢描述檔僅用於將檔案轉換為PDF封存(PDF/A)格式。
1. 按一下「匯出」。 轉換完成時，會出現匯出檔案的連結。
1. 按一下連結以檢視已轉換的檔案。

## 最佳化PDF（僅限Windows） {#optimize-a-pdf}

PDF產生器支援縮減PDF檔案的大小。

>[!NOTE]
>
>最佳化數位簽章檔案會移除數位簽章，並使其無效。

1. 在管理控制台中，按一下「服務> PDF產生器>最佳化PDF」。
1. 按一下「瀏覽」以找出要最佳化的PDF檔案。
1. 指定配置設定：

   * 若要使用自訂設定，請選取「使用自訂設定」、指定檔案類型設定，並指定逾時值。 預設值為270秒。
   * 若要使用現有的設定檔案，請選取「上傳設定檔案」，然後按一下「瀏覽」前往檔案位置。

1. 按一下「建立」。

