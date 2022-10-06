---
title: 使用PDF產生器轉換檔案
seo-title: Converting files using PDF Generator
description: 了解如何使用PDF產生器轉換檔案。
seo-description: Learn how to convert files using PDF Generator.
uuid: 295afb8f-130a-44f5-b0ab-e4c93c0c9e52
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 999ae2be-56ba-48c1-861b-8d4c991a0206
feature: PDF Generator
exl-id: 0e2c12b5-24c8-4aca-8826-cb661051ce4f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1167'
ht-degree: 0%

---

# 使用PDF產生器轉換檔案{#converting-files-using-pdf-generator}

您可以使用PDF產生器網頁來轉換檔案。

## 建立PDF檔案 {#create-a-pdf-file}

1. 在管理控制台中，按一下「服務>PDF產生器>建立PDF」。
1. 按一下「瀏覽」以尋找並選取檔案。

   >[!NOTE]
   >
   >PDF生成器能夠自動檢測.doc、.xls、.ppt和.rtf檔案的檔案類型，即使檔案名缺少副檔名。 此功能無法用於.docx、.xlsx及.pptx檔案。

1. 在「組態設定」下，選取「使用自訂設定」或「上傳設定檔」。

   * 如果您使用自訂設定，請選取Adobe PDF設定、安全性設定和檔案類型設定，並指定逾時。

      Adobe PDF設定僅適用於PS-to-PDF、EPS-to-PDF、PRN-to-PDF、OCR影像 — to-PDF以及本機 — PDF轉換。 逾時設定會指定轉換完成所需的最長時間。 預設為270秒。 在影像對PDF和OpenOffice對PDF轉換期間不會使用這些設定。

   * 如果要上傳設定檔案，請在方塊中輸入其路徑和名稱，或按一下「瀏覽」以尋找並選取檔案。

1. （可選）在XMP中繼資料檔案下，輸入XMP檔案的路徑和名稱，或按一下瀏覽以尋找並選取檔案。 XMP檔案可用來包含標準中繼資料資訊。 (請參閱 [關於XMP檔案](converting-files-using-pdf-generator.md#about-xmp-files).)
1. 按一下建立。建立檔案時，會顯示指向該檔案的連結。 如果轉換期間發生錯誤，則會顯示警告。 如果要建立Postscript檔案，警告也包含指向日誌檔案的連結。
1. 按一下PDF檔案的連結。 檔案會在Acrobat中開啟。

### 關於XMP檔案 {#about-xmp-files}

PDF產生器在Acrobat 5.0或更新版本中建立的文檔包含XML格式的文檔元資料。 *中繼資料* 包括有關文檔及其內容的資訊，如作者的名稱、關鍵字以及搜索實用程式可以使用的版權資訊。

文檔元資料包含（但不限於）也顯示在Acrobat中「文檔屬性」對話框的「說明」頁簽上的資訊。 在「說明」頁簽上所做的更改將反映在文檔元資料中。 使用第三方產品可以擴展和修改文檔元資料。

Adobe可擴充中繼資料平台(XMP)為Adobe應用程式提供通用的XML架構，該架構可標準化跨發佈工作流程的檔案中繼資料的建立、處理和交換。 您可以以XMP格式保存和導入文檔元資料XML原始碼，以便在各種文檔之間共用元資料。 如需XMP檔案的詳細資訊，請參閱 [可擴充中繼資料平台(XMP)](https://www.adobe.com/products/xmp/) 和 [AdobeXMP開發人員中心](https://www.adobe.com/devnet/xmp.html).

您可以在Acrobat中建立XMP檔案。

## 將HTML檔案或ZIP檔案轉換為PDF {#convert-an-html-file-or-zip-file-to-pdf}

您可以使用「PDF產生器」，將下列類型的檔案轉換為Adobe PDF:

* HTML檔案，您可以透過上傳HTML檔案或指定網頁或網站的URL來轉換。
* 封存檔(ZIP)，可包含HTML檔案、影像檔案或兩者。

如果ZIP檔案在其資料夾層次結構的最底層包含多個HTML檔案，則ZIP檔案還必須包含index.htm或index.html檔案。

>[!NOTE]
>
>* 要PDF的HTML功能需要系統字型目錄中的某些字型。 在Linux、Solaris和AIX系統上，系統字型目錄必須包含Courier字型。 在Windows系統上，系統字型目錄必須包含Times New Roman。
>
>* （僅限UNIX系統）AEM Forms伺服器上應提供下列日文字型之一，以將日文字型的網頁轉換為PDF檔案。
>
>  * &quot;薩扎納米哥特&quot;
>  * &quot;Kozuka Gothic Pro-VI&quot;
>  * &quot;Kozuka Mincho Pro-VI&quot;
>  * &quot;薩扎納米哥特&quot;
>  * &quot;Kozuka Mincho Pr6N&quot;
>  * 《三草佐佐奈美》
>  * &quot;AdobeHeiti Std&quot;
>  * 「Adobe Song Std」
>
>* 若要從本機檔案系統上傳檔案，請使用「HTML至PDF」頁面上的「上傳檔案」選項。


1. 在管理控制台中，按一下「服務>PDF產生器>HTML以PDF」。
1. 執行下列任一作業，指定要轉換的檔案：

   * 在「上傳檔案」中，鍵入HTML檔案或ZIP檔案的路徑和檔案名，或按一下「瀏覽」以查找並選擇它。
   * 在「指定URL」方塊中，輸入要轉換的頁面或網站的URL。

   >[!NOTE]
   >
   >您要轉換的檔案副檔名必須為.html、.htm或.zip。

1. 指定配置設定：

   * 若要使用自訂設定，請選取「使用自訂設定」、指定安全性和檔案類型設定，並指定逾時值。 預設值為270秒。
   >[!NOTE]
   >
   >如果將「生成PDF」服務配置為使用Acrobat WebCapture，則在此頁上選擇的「檔案類型設定」不會影響生成的PDF。 請改為適當變更伺服器上安裝的Acrobat版本。

   * 若要使用現有設定檔案，請選取「上傳設定檔案」 ，然後按一下「瀏覽」以前往檔案位置。


1. 若要上傳XMP檔案，請按一下「瀏覽」並前往檔案位置。 XMP檔案可用來包含標準中繼資料資訊。 (請參閱 [關於XMP檔案](converting-files-using-pdf-generator.md#about-xmp-files).)
1. 按一下建立。建立檔案時，會顯示PDF檔案的連結。
1. 按一下連結以檢視Acrobat中的PDF檔案。

## 將PDF檔案導出為其他檔案格式（僅限Windows） {#export-a-pdf-file-to-another-file-format-windows-only}

您可以將PDF檔案匯出為各種檔案格式，如以下章節中的產生PDF服務一節所述： [服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

1. 在管理控制台中，按一下「服務>PDF產生器>Export PDF」。
1. 按一下「瀏覽」以尋找要匯出的PDF檔案。
1. 在要列出的Export PDF檔案中，選擇要導出PDF檔案的格式。
1. 在指定逾時方塊中，輸入應用程式逾時前的等待時間。 預設值為270秒。

   轉換檔案時顯示的轉換時間可能大於您在此指定的值。 「轉換時間」包括等待執行緒或進程所花費的時間、轉換檔案所花費的時間，以及後援轉換器所花費的時間（如果適用）。 次. 指定逾時值是轉換檔案所花費的時間。

1. （選用）在 **指定自訂預檢設定檔** 選項，按一下「瀏覽」，然後選擇 [自訂預檢設定檔](https://helpx.adobe.com/acrobat/using/preflight-profiles-acrobat-pro.html). 僅在將文檔轉換為PDF歸檔(PDF/A)格式時使用印前檢查配置檔案。
1. 按一下「匯出」。 轉換完成時，會顯示匯出檔案的連結。
1. 按一下連結即可檢視轉換的檔案。

## 最佳化PDF（僅限Windows） {#optimize-a-pdf}

PDF產生器支援縮減PDF檔案的大小。

>[!NOTE]
>
>優化數字簽名的文檔會刪除並使數字簽名失效。

1. 在管理控制台中，按一下「服務>PDF產生器>Optimize PDF」。
1. 按一下「瀏覽」以尋找要最佳化的PDF檔案。
1. 指定配置設定：

   * 若要使用自訂設定，請選取「使用自訂設定」、指定檔案類型設定，並指定逾時值。 預設值為270秒。
   * 若要使用現有設定檔案，請選取「上傳設定檔案」 ，然後按一下「瀏覽」以前往檔案位置。

1. 按一下建立。
