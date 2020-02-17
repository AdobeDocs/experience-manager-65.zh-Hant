---
title: 使用CustomToolbars轉換HTML表格
seo-title: 使用CustomToolbars轉換HTML表格
description: 'null'
seo-description: 'null'
uuid: b9c9464e-ff19-4051-a39b-4ec71c512d10
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 7eb0e8a8-d76a-43f7-a012-c21157b14cd4
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 使用CustomToolbars轉換HTML表格 {#rendering-html-forms-with-customtoolbars}

## 使用自訂工具列來轉換HTML表格 {#rendering-html-forms-with-custom-toolbars}

Forms服務可讓您自訂使用HTML表格轉譯的工具列。 您可自訂工具列，以覆寫預設的CSS樣式來改變其外觀，並借由覆寫Java指令碼來新增動態行為。 使用名為fscmenu.xml的XML檔案自定義工具欄。 預設情況下，Forms服務從內部指定的URI位置檢索此檔案。

>[!NOTE]
>
>此URI位置位於adobe-forms-core.jar檔案中，此檔案位於adobe-forms-dsc.jar檔案中。 adobe-forms-dsc.jar檔案位於C:\Adobe\Adobe_Experience_Manager_forms\ folder (C:\ is the installation directory)。 您可以使用檔案擷取工具（例如Win RAR）來開啟adobe。

您可以從此位置複製fscmenu.xml、修改它以符合您的需求，然後將它放置在自訂URI位置。 接著，使用Forms Service API，從指定位置使用fscmenu.xml檔案來設定導致Forms服務的執行時期選項。 這些動作會導致Forms服務轉換具有自訂工具列的HTML表格。

除了fscmenu.xml檔案外，您還需要取得下列檔案：

* fscmenu.js
* fscattachments.js
* fscmenu.css
* fscmenu-v.css
* fscmenu-ie.css
* fscdialog.css

fscJS是與每個節點相關聯的Java指令碼。 必須為節點提供一個，並 `div#fscmenu` 可選地為節點 `ul#fscmenuItem` 提供。 JS檔案會實作核心工具列功能，而預設檔案也能運作。

fscCSS是與特定節點關聯的樣式表。 CSS檔案中的樣式會指定工具列外觀。 *fscVCSS* 是垂直工具列的樣式表，顯示在轉譯的HTML表格左側。 *fscIECSS* 是用於在Internet explorer中呈現的HTML表單的樣式表。

請確定fscmenu.xml檔案中已參考上述所有檔案。 也就是說，在fscmenu.xml檔案中，指定指向這些檔案的URI位置，讓Forms服務找到這些檔案。 依預設，這些檔案可在URI位置使用，從內部關鍵字 `FSWebRoot` 開始 `ApplicationWebRoot`。

若要自訂工具列，請使用外部關鍵字來取代關鍵字 `FSToolBarURI`。 此關鍵字代表在執行時期傳遞至Forms服務的URI（本節稍後會顯示此方法）。

您也可以指定這些JS和CSS檔案的絕對位置，例如https://www.mycompany.com/scripts/misc/fscmenu.js。 在這種情況下，您不需要使用關鍵 `FSToolBarURI` 字。

>[!NOTE]
>
>不建議您混用這些檔案的參考方式。 也就是說，所有URI都應使用關鍵字或絕 `FSToolBarURI` 對位置來參考。

您可以開啟adobe-forms-&lt;appserver>.ear檔案，以取得JS和CSS檔案。 在此檔案中，開啟adobe-forms-res.war。 這些檔案都位於WAR檔案中。 adobe-forms-&lt;appserver>.ear檔案位於AEM forms安裝資料夾(C:\ is the installation directory)中。 您可以使用檔案擷取工具（例如WinRAR）開啟adobe-forms-&lt;appserver>.ear。

以下XML語法顯示了fscmenu.xml檔案示例。

```as3
 <div id="fscmenu" fscJS="FSToolBarURI/scripts/fscmenu.js" fscCSS="FSToolBarURI/fscmenu.css" fscVCSS="FSToolBarURI/fscmenu-v.css" fscIECSS="FSToolBarURI/fscmenu-ie.css">
         <ul class="fscmenuItem" id="Home">
             <li>
                 <a href="#" fscTarget="_top" tabindex="1">Home</a>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Upload" fscJS="FSToolBarURI/scripts/fscattachments.js" fscCSS="FSToolBarURI/fscdialog.css">
             <li>
                 <a tabindex="2">Upload Attachments</a>
                 <ul class="fscmenuPopup" id="fscUploadAttachments">
                     <li>
                         <a href="javascript:doUploadDialog();" tabindex="3">Add ...</a>
                     </li>
                     <li>
                         <a href="javascript:doDeleteDialog();" tabindex="4">Delete ...</a>
                     </li>
                 </ul>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Download">
             <li>
                 <a tabindex="100">Download Attachments</a>
                 <ul class="fscmenuPopup">
                     <li>
                         <a tabindex="101">None available</a>
                     </li>
                 </ul>
             </li>
         </ul>
     </div>
```

>[!NOTE]
>
>粗體文字代表必須參考之CSS和JS檔案的URI。

下列項目說明如何自訂工具列：

* 使用本節中 `fscJS`介紹的方法之一（例如，），更改、、 `fscCSS``fscVCSS``fscIECSS``fscJS="FSToolBarURI/scripts/fscmenu.js"`、屬性的值（在fscmenu.xml檔案中），以反映所引用檔案的自定義位置。
* 必須指定所有CSS和JS檔案。 如果未修改任何檔案，請在自訂位置提供預設檔案。 您可以按本節所述開啟各種檔案，以取得預設檔案。
* 允許為任何檔案提供絕對參考(例如https://www.example.com/scripts/custom-vertical-fscmenu.css)。
* 節點需要的JS和CSS檔 `div#fscmenu` 案是工具列功能的必備工具。 個別 `ul#fscmenuItem` 節點可能或可能不具備支援的JS或CSS檔案。

**變更本機值**

在自訂工具列時，您可以變更工具列的地區設定值。 就是說，你可以用另一種語言來顯示。 下圖顯示以法文顯示的自訂工具列。

>[!NOTE]
>
>無法以多種語言建立自訂工具列。 工具欄不能根據區域設定使用不同的XML檔案。

若要變更工具列的地區設定值，請確定fscmenu.xml檔案包含您要顯示的語言。 以下XML語法顯示用於顯示法文工具欄的fscmenu.xml檔案。

```as3
 <div id="fscmenu" fscJS="FSToolBarURI/scripts/fscmenu.js" fscCSS="FSToolBarURI/fscmenu.css" fscVCSS="FSToolBarURI/fscmenu-v.css" fscIECSS="FSToolBarURI/fscmenu-ie.css">
         <ul class="fscmenuItem" id="Home">
             <li>
                 <a href="#" fscTarget="_top" tabindex="1">Accueil</a>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Upload" fscJS="FSToolBarURI/scripts/fscattachments.js" fscCSS="FSToolBarURI/fscdialog.css">
             <li>
                 <a tabindex="2">Télécharger les pièces jointes</a>
                 <ul class="fscmenuPopup" id="fscUploadAttachments">
                     <li>
                         <a href="javascript:doUploadDialog();" tabindex="3">Ajouter...</a>
                     </li>
                     <li>
                         <a href="javascript:doDeleteDialog();" tabindex="4">Supprimer...</a>
                     </li>
                 </ul>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Download">
             <li>
                 <a tabindex="100">Télécharger les pièces jointes</a>
                 <ul class="fscmenuPopup">
                     <li>
                         <a tabindex="101">Aucune disponible</a>
                     </li>
                 </ul>
             </li>
         </ul>
     </div>
```

>[!NOTE]
>
>與此部分關聯的「快速入門」使用此XML檔案顯示法文自定義工具欄，如上圖所示。

此外，您也可以叫用物件的方法，並傳 `HTMLRenderSpec` 遞指定地區 `setLocale` 值的字串值，以指定有效的地區值。 例如，通過指 `fr_FR` 定法文。 Forms服務與本地化工具列搭售。

>[!NOTE]
>
>在您演算使用自訂工具列的HTML表格之前，您必須瞭解HTML表格的轉換方式。 (請參 [閱「將表單轉換為HTML](/help/forms/developing/rendering-forms-html.md)」)。

如需Forms服務的詳細資訊，請參閱「AEM Forms [的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

若要轉換包含自訂工具列的HTML表格，請執行下列工作：

1. 包含專案檔案。
1. 建立Forms Java API物件。
1. 參考自訂fscmenu XML檔案。
1. 演算HTML表格。
1. 將表單資料流寫入用戶端網頁瀏覽器。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請加入proxy檔案。

**建立Forms Java API物件**

您必須先建立Forms用戶端物件，才能以程式設計方式執行Forms服務支援的作業。

**參考自訂fscmenu XML檔案**

要渲染包含自定義工具欄的HTML表單，請參考描述該工具欄的fscmenu XML檔案。 （本節提供fscmenu XML檔案的兩個示例。）此外，請確定fscmenu.xml檔案會正確指定所有參照檔案的位置。 如本節稍早所述，請確定所有檔案皆由關鍵字或其絕 `FSToolBarURI` 對位置參考。

**轉換HTML表格**

要渲染HTML表單，請指定在Designer中建立並另存為XDP檔案的表單設計。 也選擇HTML轉換類型。 例如，您可以指定轉換Internet Explorer 5.0或更新版本動態HTML的HTML轉換類型。

轉換HTML表單也需要值，例如轉換其他表單類型的URI值。

**將表單資料串流寫入用戶端網頁瀏覽器**

當Forms服務轉譯HTML表單時，它會傳回您必須寫入用戶端網頁瀏覽器的表單資料串流，讓使用者可以看見HTML表單。

**另請參閱**

[使用Java API，使用自訂工具列來轉換HTML表格](#render-an-html-form-with-a-custom-toolbar-using-the-java-api)

[使用web service API，使用自訂工具列轉譯HTML表格](#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[轉換互動式PDF表單](/help/forms/developing/rendering-interactive-pdf-forms.md)

[將表單轉換為HTML](/help/forms/developing/rendering-forms-html.md)

[建立轉譯表單的Web應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API，使用自訂工具列來轉換HTML表格 {#render-an-html-form-with-a-custom-toolbar-using-the-java-api}

使用Forms Service API(Java)演算包含自訂工具列的HTML表單：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms Java API物件

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `FormsServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 參考自訂fscmenu XML檔案

   * 使用其 `HTMLRenderSpec` 建構函式建立物件。
   * 若要使用工具列來轉換HTML表格，請叫 `HTMLRenderSpec` 用物件的方 `setHTMLToolbar` 法並傳遞 `HTMLToolbar` 列舉值。 例如，若要顯示垂直HTML工具列，請傳遞 `HTMLToolbar.Vertical`。
   * 調用物件的方法並傳遞指定XML檔 `HTMLRenderSpec` 案URI位 `setToolbarURI` 置的字串值，以指定fscmenu XML檔案的位置。
   * 如果適用，請調用物件的方法並傳 `HTMLRenderSpec` 遞指定地區值 `setLocale` 的字串值，以設定地區值。 預設值為英文。
   >[!NOTE]
   >
   >與此部分關聯的快速啟動將此值設定為 `fr_FR`*。*

1. 轉換HTML表格

   叫用物 `FormsServiceClient` 件的方 `renderHTMLForm` 法並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案副檔名。 如果您參照屬於Forms應用程式一部分的表單設計，請確定您指定完整路徑，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 指定 `TransformTo` HTML首選項類型的枚舉值。 例如，若要轉譯與Internet Explorer 5.0或更新版本的動態HTML相容的HTML表格，請指定 `TransformTo.MSDHTML`。
   * 包 `com.adobe.idp.Document` 含要與表單合併的資料的對象。 如果您不想合併資料，請傳遞空 `com.adobe.idp.Document` 物件。
   * 儲存 `HTMLRenderSpec` HTML執行時期選項的物件。
   * 指定標題值的字 `HTTP_USER_AGENT` 串值，例如 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
   * 存 `URLSpec` 儲呈現HTML表單所需URI值的對象。
   * 儲存 `java.util.HashMap` 檔案附件的對象。 這是可選參數，您可以指 `null` 定是否不要將檔案附加到表單。
   該方 `renderHTMLForm` 法返回包 `FormsResult` 含必須寫入客戶端Web瀏覽器的表單資料流的對象。

1. 將表單資料串流寫入用戶端網頁瀏覽器

   * 通過調 `com.adobe.idp.Document` 用對象的方法 `FormsResult` 建立對 `getOutputContent` 像。
   * 通過調用對象的方 `com.adobe.idp.Document` 法來獲取對象的內 `getContentType` 容類型。
   * 調用 `javax.servlet.http.HttpServletResponse` 物件的方法並傳遞物件的內 `setContentType` 容類型，以設定物件的內容 `com.adobe.idp.Document` 類型。
   * 建立 `javax.servlet.ServletOutputStream` 物件，以呼叫物件的方法，將表單資料串流寫入用戶端Web `javax.servlet.http.HttpServletResponse` 瀏覽器 `getOutputStream` 中。
   * 調用 `java.io.InputStream` 物件的方 `com.adobe.idp.Document` 法以建立物 `getInputStream` 件。
   * 建立位元組陣列，並借由調用物件的方法並將 `InputStream` 位元組陣列 `read` 傳入為引數，以表單資料流填入。
   * 叫用物 `javax.servlet.ServletOutputStream` 件的方 `write` 法，將表單資料串流傳送至用戶端網頁瀏覽器。 將位元組陣列傳遞至 `write` 方法。

**另請參閱**

[快速入門（SOAP模式）:使用Java API使用自訂工具列來轉換HTML表格](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API，使用自訂工具列轉譯HTML表格 {#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api}

使用Forms Service API(web service)演算包含自訂工具列的HTML表格：

1. 包含專案檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 在類路徑中包含Java代理類。

1. 建立Forms Java API物件

   建立對 `FormsService` 像並設定驗證值。

1. 參考自訂fscmenu XML檔案

   * 使用其 `HTMLRenderSpec` 建構函式建立物件。
   * 若要使用工具列來轉換HTML表格，請叫 `HTMLRenderSpec` 用物件的方 `setHTMLToolbar` 法並傳遞 `HTMLToolbar` 列舉值。 例如，若要顯示垂直HTML工具列，請傳遞 `HTMLToolbar.Vertical`。
   * 調用物件的方法並傳遞指定XML檔 `HTMLRenderSpec` 案URI位 `setToolbarURI` 置的字串值，以指定fscmenu XML檔案的位置。
   * 如果適用，請調用物件的方法並傳 `HTMLRenderSpec` 遞指定地區值 `setLocale` 的字串值，以設定地區值。 預設值為英文。
   >[!NOTE]
   >
   >與此部分關聯的快速啟動將此值設定為 `fr_FR`*。*

1. 轉換HTML表格

   叫用物 `FormsService` 件的方 `renderHTMLForm` 法並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案副檔名。 如果您參照屬於Forms應用程式一部分的表單設計，請確定您指定完整路徑，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 指定 `TransformTo` HTML首選項類型的枚舉值。 例如，若要轉譯與Internet Explorer 5.0或更新版本的動態HTML相容的HTML表格，請指定 `TransformTo.MSDHTML`。
   * 包 `BLOB` 含要與表單合併的資料的對象。 如果您不想合併資料，請傳遞 `null`。
   * 儲存 `HTMLRenderSpec` HTML執行時期選項的物件。
   * 指定標題值( `HTTP_USER_AGENT` 如)的字串 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322`值。 如果您不想設定此值，可以傳遞空字串。
   * 存 `URLSpec` 儲呈現HTML表單所需URI值的對象。
   * 儲存 `java.util.HashMap` 檔案附件的對象。 此參數為可選參數，您可以指 `null` 定是否不想將檔案附加到表單。
   * 由方 `com.adobe.idp.services.holders.BLOBHolder` 法填入的空對 `renderHTMLForm` 像。 此參數值儲存渲染的表單。
   * 由方 `com.adobe.idp.services.holders.BLOBHolder` 法填入的空對 `renderHTMLForm` 像。 此參數儲存輸出XML資料。
   * 由方 `javax.xml.rpc.holders.LongHolder` 法填入的空對 `renderHTMLForm` 像。 此引數會儲存表單中的頁數。
   * 由方 `javax.xml.rpc.holders.StringHolder` 法填入的空對 `renderHTMLForm` 像。 此引數儲存地區值。
   * 由方 `javax.xml.rpc.holders.StringHolder` 法填入的空對 `renderHTMLForm` 像。 此引數儲存所使用的HTML轉換值。
   * 包含 `com.adobe.idp.services.holders.FormsResultHolder` 此操作結果的空對象。
   該方 `renderHTMLForm` 法用必 `com.adobe.idp.services.holders.FormsResultHolder` 須寫入客戶端Web瀏覽器的表單資料流填充作為最後一個參數值傳遞的對象。

1. 將表單資料串流寫入用戶端網頁瀏覽器

   * 獲取 `FormResult` 對象資料成員的 `com.adobe.idp.services.holders.FormsResultHolder` 值以建立 `value` 對象。
   * 呼叫 `BLOB` 物件的方法，以建立包含表 `FormsResult` 單資料的物 `getOutputContent` 件。
   * 通過調用對象的方 `BLOB` 法來獲取對象的內 `getContentType` 容類型。
   * 調用 `javax.servlet.http.HttpServletResponse` 物件的方法並傳遞物件的內 `setContentType` 容類型，以設定物件的內容 `BLOB` 類型。
   * 建立 `javax.servlet.ServletOutputStream` 物件，以呼叫物件的方法，將表單資料串流寫入用戶端Web `javax.servlet.http.HttpServletResponse` 瀏覽器 `getOutputStream` 中。
   * 建立位元組陣列，並透過叫用物件的方 `BLOB` 法來填入該 `getBinaryData` 陣列。 此任務將對象的內 `FormsResult` 容分配給位元組陣列。
   * 叫用物 `javax.servlet.http.HttpServletResponse` 件的方 `write` 法，將表單資料串流傳送至用戶端網頁瀏覽器。 將位元組陣列傳遞至 `write` 方法。

**另請參閱**

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
