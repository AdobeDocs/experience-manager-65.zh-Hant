---
title: 使用PDF Generator轉換檔案
description: PDF Generator服務會將原生檔案格式轉換為PDF。 它也會將PDF轉換為其他檔案格式，並最佳化PDF檔案的大小。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: 0e2c12b5-24c8-4aca-8826-cb661051ce4f
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '1185'
ht-degree: 0%

---

# 使用PDF Generator轉換檔案{#converting-files-using-pdf-generator}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

您可以使用PDF Generator網頁來轉換檔案。

## 建立PDF檔案 {#create-a-pdf-file}

1. 在Administration Console中，按一下「服務>PDF Generator>建立PDF」。
1. 按一下「瀏覽」以尋找並選取檔案。

   >[!NOTE]
   >
   >PDF Generator能夠自動偵測.doc、.xls、.ppt和.rtf等檔案型別，即使檔案名稱遺失副檔名亦然。 此功能不適用於.docx、.xlsx和.pptx檔案。

1. 在「組態設定」下，選取「使用自訂設定」或「上傳設定檔案」。

   * 如果您使用自訂設定，請選取Adobe PDF設定、安全性設定和檔案型別設定，並指定逾時。

     Adobe PDF設定僅適用於PS對PDF、EPS對PDF、PRN對PDF、開啟OCR的影像對PDF，以及原生對PDF的轉換。 逾時設定會指定完成轉換所需的最長時間。 預設值為270秒。 影像到PDF和OpenOffice到PDF轉換期間不會使用這些設定。

   * 如果您要上傳設定檔案，請在方塊中輸入其路徑和名稱，或按一下「瀏覽」以尋找並選取檔案。

1. （選擇性）在「XMP中繼資料檔案」下，輸入XMP檔案的路徑和名稱，或按一下「瀏覽」尋找並選取檔案。 XMP檔案可用來包含標準中繼資料資訊。 (請參閱[關於XMP檔案](converting-files-using-pdf-generator.md#about-xmp-files)。)
1. 按一下「建立」。 建立檔案時，會出現指向該檔案的連結。 如果在轉換期間發生錯誤，則會出現警告。 如果您要建立Postscript檔案，警告也包含記錄檔的連結。
1. 按一下PDF檔案的連結。 檔案會在Acrobat中開啟。

### 關於XMP檔案 {#about-xmp-files}

在Acrobat 5.0或更新版本中PDF Generator建立的PDF檔案包含XML格式的檔案中繼資料。 *中繼資料*&#x200B;包含有關檔案及其內容的資訊，例如搜尋公用程式可以使用的作者名稱、關鍵字和版權資訊。

檔案中繼資料包含（但不限於）也顯示在Acrobat中「檔案內容」對話方塊的「說明」標籤上的資訊。 在「說明」標籤上進行的變更會反映在檔案中繼資料中。 可使用協力廠商產品來擴充及修改檔案中繼資料。

Adobe可延伸中繼資料平台(XMP)為Adobe應用程式提供通用XML架構，可標準化跨發佈工作流程的檔案中繼資料的建立、處理和交換。 您可以以XMP格式儲存和匯入檔案中繼資料XML原始程式碼，以便在不同檔案之間共用中繼資料。 如需XMP檔案的詳細資訊，請參閱[可延伸的中繼資料平台(XMP)](https://www.adobe.com/products/xmp/)和[AdobeXMP開發人員中心](https://www.adobe.com/devnet/xmp.html)。

您可以在Acrobat中建立XMP檔案。

## 將HTML檔案或ZIP檔案轉換為PDF {#convert-an-html-file-or-zip-file-to-pdf}

您可以使用PDF Generator將下列型別的檔案轉換成Adobe PDF：

* HTML檔案，您可以透過上傳HTML檔案或指定網頁或網站的URL來轉換這些檔案。
* 封存的檔案(ZIP)，其中可包含HTML檔案和/或影像檔案。

如果ZIP檔案在其資料夾階層的最低層級包含多個HTML檔案，則ZIP檔案也必須包含index.htm或index.html檔案。

>[!NOTE]
>
>* PDFHTML功能需要系統字型目錄中的特定字型。 在Linux、Solaris和AIX系統上，系統字型目錄必須包含Courier字型。 在Windows系統上，系統字型目錄必須包含Times New Roman。
>
>* （僅適用於UNIX系統）AEM Forms伺服器上應提供下列日文字型之一，以將日文字型的網頁轉換為PDF檔案。
>
>  * 「薩扎奈米哥特語」
>  * 「Kozuka Gothic Pro-VI」
>  * 「Kozuka Mincho Pro-VI」
>  * 「薩扎奈米哥特語」
>  * 「Kozuka Mincho Pr6N」
>  * 「紗波峰澄」
>  * 「Adobe黑地標準時間」
>  * 「Adobe Song標準」
>
>* 若要從本機檔案系統上傳檔案，請使用「HTMLPDF」頁面上的「上傳檔案」選項。

1. 在管理控制檯中，按一下「服務>PDF Generator>HTML以PDF」。
1. 執行下列其中一項作業，指定要轉換的檔案：

   * 在上傳檔案中，輸入HTML檔案或ZIP檔案的路徑和檔案名稱，或按一下「瀏覽」找到並選取它。
   * 在「指定URL」方塊中，輸入要轉換之頁面或網站的URL。

   >[!NOTE]
   >
   >您要轉換的檔案副檔名必須是.html、.htm或.zip。

1. 指定組態設定：

   * 若要使用自訂設定，請選取「使用自訂設定」，指定安全性與檔案型別設定，並指定逾時值。 預設值為270秒。

   >[!NOTE]
   >
   >如果您將「產生PDF」服務設定為使用Acrobat WebCapture，則您在此頁面上選取的「檔案型別設定」不會影響產生的PDF。 請改對安裝在伺服器上的Acrobat版本進行適當的變更。

   * 若要使用現有的設定檔案，請選取「上傳設定檔案」，然後按一下「瀏覽」移至檔案位置。

1. 若要上傳XMP檔案，請按一下「瀏覽」並移至檔案位置。 XMP檔案可用來包含標準中繼資料資訊。 (請參閱[關於XMP檔案](converting-files-using-pdf-generator.md#about-xmp-files)。)
1. 按一下「建立」。 建立檔案時，會顯示PDF檔案的連結。
1. 按一下連結，即可在Acrobat中檢視PDF檔案。

## 將PDF檔案匯出為其他檔案格式（僅限Windows） {#export-a-pdf-file-to-another-file-format-windows-only}

您可以將PDF檔案匯出為各種檔案格式，如[Services Reference](https://www.adobe.com/go/learn_aemforms_services_63)的「產生PDF服務」一章中所述。

1. 在管理控制檯中，按一下「服務>PDF Generator>Export PDF」。
1. 按一下「瀏覽」以找出要匯出的PDF檔案。
1. 在要列出的Export PDF檔案中，選取要將PDF檔案匯出到的格式。
1. 在指定逾時方塊中，輸入應用程式逾時前的等待時間。 預設值為270秒。

   轉換檔案時顯示的轉換時間可能大於您在此指定的值。 「轉換時間」包括等候執行緒或程式所花的時間、轉換檔案所花的時間，以及遞補轉換器所花的時間（如果適用）。 時間。 「指定逾時」值只是轉換檔案所花的時間。

1. （選擇性）在&#x200B;**指定自訂預檢設定檔**&#x200B;選項中，按一下[瀏覽]，然後選取[自訂預檢設定檔](https://helpx.adobe.com/acrobat/using/preflight-profiles-acrobat-pro.html)。 將檔案轉換為PDF封存(PDF/A)格式時，才會使用預檢設定檔。
1. 按一下「匯出」。 轉換完成後，會出現指向匯出檔案的連結。
1. 按一下連結以檢視轉換的檔案。

## 最佳化PDF（僅限Windows） {#optimize-a-pdf}

PDF Generator支援縮減PDF檔案的大小。

>[!NOTE]
>
>最佳化數位簽署的檔案會移除數位簽名並使之失效。

1. 在管理控制檯中，按一下「服務>PDF Generator>Optimize PDF」。
1. 按一下「瀏覽」以找出要最佳化的PDF檔案。
1. 指定組態設定：

   * 若要使用自訂設定，請選取「使用自訂設定」，指定檔案型別設定，並指定逾時值。 預設值為270秒。
   * 若要使用現有的設定檔案，請選取「上傳設定檔案」，然後按一下「瀏覽」移至檔案位置。

1. 按一下「建立」。
