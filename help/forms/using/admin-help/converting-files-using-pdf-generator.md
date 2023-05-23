---
title: 使用PDF生成器轉換檔案
seo-title: Converting files using PDF Generator
description: 瞭解如何使用PDF生成器轉換檔案。
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

# 使用PDF生成器轉換檔案{#converting-files-using-pdf-generator}

可以使用「PDF生成器」網頁轉換檔案。

## 建立PDF檔案 {#create-a-pdf-file}

1. 在管理控制台中，按一下「服務」>「PDF生成器」>「建立PDF」。
1. 按一下「瀏覽」(Browse)查找並選擇檔案。

   >[!NOTE]
   >
   >PDF生成器能夠自動檢測.doc、.xls、.ppt和.rtf檔案的檔案類型，即使檔案名缺少檔案副檔名也是如此。 此功能不適用於.docx、.xlsx和.pptx檔案。

1. 在「配置設定」下，選擇「使用自定義設定」或「上載設定檔案」。

   * 如果使用自定義設定，請選擇Adobe PDF設定、安全設定和檔案類型設定並指定超時。

      Adobe PDF設定僅適用於PS到PDF、EPS到PDF、PRN到PDF、使用OCR開啟的影像到PDF以及本地到PDF轉換。 超時設定指定轉換完成所花費的最大時間。 預設值為270秒。 這些設定在映像到PDF和OpenOffice到PDF轉換期間不使用。

   * 如果要上載設定檔案，請在框中鍵入其路徑和名稱，或按一下「瀏覽」查找並選擇該檔案。

1. （可選）在元數XMP據檔案下，鍵入檔案的路徑和名XMP稱，或按一下瀏覽查找並選擇檔案。 文XMP件可用於包括標準元資料資訊。 (請參閱 [關於文XMP件](converting-files-using-pdf-generator.md#about-xmp-files)。)
1. 按一下建立。建立檔案時，將顯示指向該檔案的連結。 如果轉換過程中出現錯誤，則會出現警告。 如果要建立Postscript檔案，則警告還包含指向日誌檔案的連結。
1. 按一下PDF檔案的連結。 檔案在Acrobat開啟。

### 關於文XMP件 {#about-xmp-files}

PDF生成器在Acrobat 5.0或更高版本中建立的文檔包含XML格式的文檔元資料。 *元資料* 包括有關文檔及其內容的資訊，如作者名稱、關鍵字以及搜索實用程式可以使用的版權資訊。

文檔元資料包含（但不限於）資訊，這些資訊也出現在Acrobat的「文檔屬性」對話框的「說明」頁籤上。 在「說明」(Description)頁籤上所做的更改將反映在文檔元資料中。 可以使用第三方產品來擴展和修改文檔元資料。

Adobe可擴展元資料平台(XMP)為Adobe應用程式提供了通用XML框架，該框架規範了文檔元資料在發佈工作流中的建立、處理和交換。 您可以以格式保存和導入文檔元資料XML源XMP代碼，使各種文檔之間更容易共用元資料。 有關檔案的詳細信XMP息，請參見 [可擴展元資料平XMP台()](https://www.adobe.com/products/xmp/) 和 [Adobe開XMP發中心](https://www.adobe.com/devnet/xmp.html)。

您可以在XMPAcrobat建立檔案。

## 將HTML檔案或ZIP檔案轉換為PDF {#convert-an-html-file-or-zip-file-to-pdf}

可以使用「PDF生成器」將以下類型的檔案轉換為Adobe PDF:

* HTML檔案，可以通過上載HTML檔案或指定網頁或網站的URL來轉換該檔案。
* 已存檔檔案(ZIP)，可包含HTML檔案、映像檔案或兩者。

如果ZIP檔案在其資料夾層次結構的最低級別包含多個HTML檔案，則ZIP檔案還必須包含index.htm或index.html檔案。

>[!NOTE]
>
>* HTML到PDF功能要求系統字型目錄中的某些字型。 在Linux、Solaris和AIX系統上，系統字型目錄必須包含Courier字型。 在Windows系統上，系統字型目錄必須包含Times New Roman。
>
>* （僅基於UNIX的系統）以下日文字型之一應在AEM Forms伺服器上可用，以將帶日文字型的網頁轉換為PDF文檔。
>
>  * &quot;Sazanami哥特&quot;
>  * &quot;Kozuka GothicPRO-VI&quot;
>  * &quot;Kozuka MinchoPRO-VI&quot;
>  * &quot;Sazanami哥特&quot;
>  * 「Kozuka MinchoPr6N」
>  * 《佐佐南民草》
>  * &quot;Adobe海提體育會&quot;
>  * 《Adobe Song性病》
>
>* 要從本地檔案系統上載檔案，請使用「到HTML」頁上的「上載檔案」選項。


1. 在管理控制台中，按一下「服務」>「PDF生成器」>「HTML到PDF」。
1. 通過執行以下任務之一指定要轉換的檔案：

   * 在上載檔案中，鍵入HTML檔案或ZIP檔案的路徑和檔案名，或按一下瀏覽查找並選擇該檔案。
   * 在「指定URL」框中，鍵入要轉換的頁面或網站的URL。

   >[!NOTE]
   >
   >要轉換的檔案的檔案副檔名必須為.html、.htm或.zip。

1. 指定配置設定：

   * 要使用自定義設定，請選擇「使用自定義設定」，指定安全性和檔案類型設定，並指定超時值。 預設值為270秒。
   >[!NOTE]
   >
   >如果將「生成PDF」服務配置為使用AcrobatWebCapture，則您在此頁上選擇的「檔案類型設定」不會影響生成的PDF。 相反，對伺服器上安裝的Acrobat版本進行適當的更改。

   * 要使用現有設定檔案，請選擇「上載設定檔案」，然後按一下「瀏覽」以轉到檔案位置。


1. 要上載文XMP件，請按一下「瀏覽」並轉到檔案位置。 文XMP件可用於包括標準元資料資訊。 (請參閱 [關於文XMP件](converting-files-using-pdf-generator.md#about-xmp-files)。)
1. 按一下建立。建立檔案時，將顯示指向PDF檔案的連結。
1. 按一下連結查看Acrobat的PDF文檔。

## 將PDF檔案導出為其他檔案格式（僅限Windows） {#export-a-pdf-file-to-another-file-format-windows-only}

您可以將PDF檔案導出為各種檔案格式，如的「生成PDF服務」一章中所述 [服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

1. 在管理控制台中，按一下「服務」>「PDF生成器」>「Export PDF」。
1. 按一下「瀏覽」(Browse)以查找要導出的PDF檔案。
1. 在要列出的Export PDF檔案中，選擇要將PDF檔案導出到的格式。
1. 在指定超時框中，輸入應用程式超時之前等待的時間。 預設值為270秒。

   轉換檔案時顯示的「轉換時間」可能大於在此處指定的值。 「轉換時間」包括等待線程或進程所花費的時間、轉換檔案所花的時間以及回退轉換器所花費的時間（如果適用）。 time. 指定超時值只是轉換檔案所花的時間。

1. （可選）在 **指定自定義印前檢查配置檔案** 選項，按一下「瀏覽」，然後選擇 [自定義印前檢查配置檔案](https://helpx.adobe.com/acrobat/using/preflight-profiles-acrobat-pro.html)。 印前檢查配置檔案僅在將文檔轉換為PDF存檔(PDF/A)格式時使用。
1. 按一下「導出」。 轉換完成後，將顯示指嚮導出檔案的連結。
1. 按一下連結查看已轉換的檔案。

## 優化PDF（僅限Windows） {#optimize-a-pdf}

PDF生成器支援減小PDF檔案的大小。

>[!NOTE]
>
>優化數字簽名文檔會刪除並使數字簽名失效。

1. 在管理控制台中，按一下「服務」>「PDF生成器」>「Optimize PDF」。
1. 按一下「瀏覽」(Browse)查找要優化的PDF檔案。
1. 指定配置設定：

   * 要使用自定義設定，請選擇「使用自定義設定」，指定檔案類型設定並指定超時值。 預設值為270秒。
   * 要使用現有設定檔案，請選擇「上載設定檔案」，然後按一下「瀏覽」以轉到檔案位置。

1. 按一下建立。
