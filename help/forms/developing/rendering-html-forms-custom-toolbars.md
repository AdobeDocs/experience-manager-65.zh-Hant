---
title: 使用自訂工具列呈現HTMLForms
seo-title: Rendering HTML Forms with CustomToolbars
description: 使用Forms服務來自訂以HTML表單呈現的工具列。 您可以使用Java API和網站服務API，使用自訂工具列呈現HTML表單。
seo-description: Use the Forms service to customize a toolbar that is rendered with an HTML form. You can render an HTML Form with a custom toolbar using the Java API and a Web Service API.
uuid: b9c9464e-ff19-4051-a39b-4ec71c512d10
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 7eb0e8a8-d76a-43f7-a012-c21157b14cd4
role: Developer
exl-id: 0b992b1c-3878-447a-bccc-7034aa3e98bc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2345'
ht-degree: 0%

---

# 使用自訂工具列呈現HTMLForms {#rendering-html-forms-with-customtoolbars}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

## 使用自訂工具列呈現HTMLForms {#rendering-html-forms-with-custom-toolbars}

Forms服務可讓您自訂以HTML表單轉譯的工具列。 工具列可以自訂，透過覆寫預設CSS樣式來改變其外觀，並透過覆寫Java指令碼來新增動態行為。 使用名為fscmenu.xml的XML檔案自定義工具欄。 依預設，Forms服務會從內部指定的URI位置擷取此檔案。

>[!NOTE]
>
>此URI位置位於adobe-forms-core.jar檔案中，該檔案位於adobe-forms-dsc.jar檔案中。 adobe-forms-dsc.jar檔案位於C:\Adobe\Adobe_Experience_Manager_forms\ folder (C:\ is the installation directory)。 您可以使用檔案擷取工具（例如Win RAR）來開啟adobe。

您可以從此位置複製fscmenu.xml，修改它以滿足您的要求，然後將它放置在自定義URI位置。 接下來，使用Forms服務API，設定執行時選項，使用指定位置的fscmenu.xml檔案產生Forms服務。 這些動作會導致Forms服務轉譯具有自訂工具列的HTML表單。

除了fscmenu.xml檔案外，您還需要獲取以下檔案：

* fscmenu.js
* fscattachments.js
* fscmenu.css
* fscmenu-v.css
* fscmenu-ie.css
* fscdialog.css

fscJS是與每個節點相關聯的Java指令碼。 必須為 `div#fscmenu` 節點和 `ul#fscmenuItem` 節點。 JS檔案實作核心工具列功能，而預設檔案可運作。

fscCSS是與特定節點相關聯的樣式表。 CSS檔案中的樣式指定工具欄外觀。 *fscVCSS* 是垂直工具欄的樣式表，它顯示在已呈現的HTML表單的左側。 *fscIECSS* 是用於在Internet Explorer中呈現的HTML表單的樣式表。

請確定fscmenu.xml檔案中引用了上述所有檔案。 也就是說，在fscmenu.xml檔案中，指定指向這些檔案的URI位置，以便Forms服務能夠找到它們。 預設情況下，這些檔案可在以內部關鍵字開頭的URI位置中使用 `FSWebRoot` 或 `ApplicationWebRoot`.

若要自訂工具列，請使用外部關鍵字來取代關鍵字 `FSToolBarURI`. 此關鍵字代表在執行時傳遞至Forms服務的URI（此方法將在本節稍後顯示）。

您也可以指定這些JS和CSS檔案的絕對位置，例如https://www.mycompany.com/scripts/misc/fscmenu.js。 在此情況下，您不需要使用 `FSToolBarURI` 關鍵字。

>[!NOTE]
>
>不建議您混合參照這些檔案的方式。 也就是說，所有URI都應使用 `FSToolBarURI` 關鍵字或絕對位置。

您可以開啟adobe-forms-&lt;appserver>.ear檔案。 在此檔案中，開啟adobe-forms-res.war。 所有這些檔案都位於WAR檔案中。 Adobe-forms -&lt;appserver>.ear檔案位於AEM forms安裝資料夾(C:\ is the installation directory)中。 您可以開啟adobe-forms -&lt;appserver>.ear使用檔案擷取工具（例如WinRAR）。

以下XML語法顯示了fscmenu.xml檔案的示例。

```html
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
>粗體文字代表必須參考的CSS和JS檔案的URI。

下列項目說明如何自訂工具列：

* 變更 `fscJS`, `fscCSS`, `fscVCSS`, `fscIECSS` 屬性（在fscmenu.xml檔案中），以透過使用本節所述的其中一種方法來反映引用檔案的自定義位置(例如， `fscJS="FSToolBarURI/scripts/fscmenu.js"`)。
* 必須指定所有CSS和JS檔案。 如果未修改任何檔案，請在自訂位置提供預設檔案。 您可以開啟各種檔案，如本節所述，以取得預設檔案。
* 允許為任何檔案提供絕對參照(例如，https://www.example.com/scripts/custom-vertical-fscmenu.css)。
* JS和CSS檔案， `div#fscmenu` 節點要求是工具列功能的必要條件。 個人 `ul#fscmenuItem` 節點可能有或沒有支援的JS或CSS檔案。

**變更本機值**

在自定義工具欄時，可以更改工具欄的區域設定值。 也就是說，你可以用另一種語言來顯示。 下圖顯示以法文顯示的自訂工具列。

>[!NOTE]
>
>無法以多種語言建立自訂工具列。 工具欄不能根據區域設定使用不同的XML檔案。

要更改工具欄的區域設定值，請確保fscmenu.xml檔案包含要顯示的語言。 以下XML語法顯示用於顯示法文工具欄的fscmenu.xml檔案。

```html
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
>與此部分關聯的快速入門使用此XML檔案顯示法文自定義工具欄，如上圖所示。

另外，通過調用 `HTMLRenderSpec` 物件 `setLocale` 方法，並傳遞指定區域設定的字串值。 例如，傳遞 `fr_FR` 指定法文。 Forms服務與本地化工具列搭配。

>[!NOTE]
>
>呈現使用自訂工具列的HTML表單之前，您必須知道HTML表單的呈現方式。 (請參閱 [將Forms轉譯為HTML](/help/forms/developing/rendering-forms-html.md).)

如需Forms服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary-of-steps}

要呈現包含自定義工具欄的HTML表單，請執行以下任務：

1. 包含專案檔案。
1. 建立Forms Java API物件。
1. 參考自定義fscmenu XML檔案。
1. 轉譯HTML表單。
1. 將表單資料流寫入客戶端Web瀏覽器。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請包含代理檔案。

**建立Forms Java API物件**

您必須先建立Forms用戶端物件，才能以程式設計方式執行Forms服務支援的操作。

**參考自定義fscmenu XML檔案**

要呈現包含自定義工具欄的HTML表單，請參考描述工具欄的fscmenu XML檔案。 （本節提供fscmenu XML檔案的兩個示例。） 另外，請確保fscmenu.xml檔案正確指定所有引用檔案的位置。 如本節前面所述，請確定所有檔案皆由 `FSToolBarURI` 關鍵字或其絕對位置。

**轉譯HTML表單**

要呈現HTML表單，請指定在Designer中建立並另存為XDP檔案的表單設計。 也選取HTML轉換類型。 例如，您可以指定HTML轉換類型，用於為Internet Explorer 5.0或更新版本轉譯動態HTML。

呈現HTML表單還需要URI值（例如，用於呈現其他表單類型的URI值）。

**將表單資料流寫入客戶端Web瀏覽器**

Forms服務轉譯HTML表單時，會傳回表單資料流，您必須將此資料流寫入用戶端網頁瀏覽器，使使用者能看到HTML表單。

**另請參閱**

[使用Java API使用自訂工具列呈現HTML表單](#render-an-html-form-with-a-custom-toolbar-using-the-java-api)

[使用網站服務API使用自訂工具列轉譯HTML表單](#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[轉譯互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[將Forms轉譯為HTML](/help/forms/developing/rendering-forms-html.md)

[建立可轉譯Forms的網頁應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API使用自訂工具列呈現HTML表單 {#render-an-html-form-with-a-custom-toolbar-using-the-java-api}

使用Forms服務API(Java)呈現包含自訂工具列的HTML表單：

1. 包含項目檔案

   在Java專案的類別路徑中加入用戶端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms Java API物件

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `FormsServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 參考自定義fscmenu XML檔案

   * 建立 `HTMLRenderSpec` 物件，使用其建構子。
   * 要使用工具欄呈現HTML表單，請調用 `HTMLRenderSpec` 物件 `setHTMLToolbar` 方法和傳遞 `HTMLToolbar` 列舉值。 例如，要顯示垂直HTML工具欄，請通過 `HTMLToolbar.Vertical`.
   * 通過調用 `HTMLRenderSpec` 物件 `setToolbarURI` 方法，並傳遞指定XML檔案的URI位置的字串值。
   * 如果適用，請通過調用 `HTMLRenderSpec` 物件 `setLocale` 方法，並傳遞指定區域設定值的字串值。 預設值為英文。

   >[!NOTE]
   >
   >與此部分關聯的快速入門將此值設定為 `fr_FR`*.*

1. 轉譯HTML表單

   叫用 `FormsServiceClient` 物件 `renderHTMLForm` 方法，並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案名副檔名。 如果您參考屬於Forms應用程式一部分的表單設計，請務必指定完整路徑，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` 指定HTML首選項類型的枚舉值。 例如，要呈現與Internet Explorer 5.0或更新版本的動態HTML相容的HTML表單，請指定 `TransformTo.MSDHTML`.
   * A `com.adobe.idp.Document` 包含要與表單合併資料的物件。 如果您不想合併資料，請傳遞空白 `com.adobe.idp.Document` 物件。
   * 此 `HTMLRenderSpec` 儲存HTML運行時選項的對象。
   * 指定 `HTTP_USER_AGENT` 標題值，例如 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * A `URLSpec` 用於儲存呈現HTML表單所需的URI值的對象。
   * A `java.util.HashMap` 儲存檔案附件的物件。 這是選用參數，您可以指定 `null` 如果您不想將檔案附加到表單。

   此 `renderHTMLForm` 方法傳回 `FormsResult` 包含必須寫入客戶端web瀏覽器的表單資料流的對象。

1. 將表單資料流寫入客戶端Web瀏覽器

   * 建立 `com.adobe.idp.Document` 對象，方法是調用 `FormsResult` 物件s `getOutputContent` 方法。
   * 取得 `com.adobe.idp.Document` 對象 `getContentType` 方法。
   * 設定 `javax.servlet.http.HttpServletResponse` 對象的內容類型，方法是調用 `setContentType` 方法，並傳遞 `com.adobe.idp.Document` 物件。
   * 建立 `javax.servlet.ServletOutputStream` 通過調用 `javax.servlet.http.HttpServletResponse` 物件 `getOutputStream` 方法。
   * 建立 `java.io.InputStream` 對象，方法是調用 `com.adobe.idp.Document` 物件 `getInputStream` 方法。
   * 建立位元組陣列，並叫用 `InputStream` 物件 `read` 方法，並將位元組陣列傳遞為引數。
   * 叫用 `javax.servlet.ServletOutputStream` 物件 `write` 將表單資料流傳送至用戶端網頁瀏覽器的方法。 將位元組陣列傳遞至 `write` 方法。

**另請參閱**

[快速入門（SOAP模式）:使用Java API使用自訂工具列轉譯HTML表單](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API使用自訂工具列轉譯HTML表單 {#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api}

使用Forms服務API（網站服務）轉譯包含自訂工具列的HTML表單：

1. 包含項目檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 在類路徑中包含Java代理類。

1. 建立Forms Java API物件

   建立 `FormsService` 對象和設定驗證值。

1. 參考自定義fscmenu XML檔案

   * 建立 `HTMLRenderSpec` 物件，使用其建構子。
   * 要使用工具欄呈現HTML表單，請調用 `HTMLRenderSpec` 物件 `setHTMLToolbar` 方法和傳遞 `HTMLToolbar` 列舉值。 例如，要顯示垂直HTML工具欄，請通過 `HTMLToolbar.Vertical`.
   * 通過調用 `HTMLRenderSpec` 物件 `setToolbarURI` 方法，並傳遞指定XML檔案的URI位置的字串值。
   * 如果適用，請通過調用 `HTMLRenderSpec` 物件 `setLocale` 方法，並傳遞指定區域設定的字串值。 預設值為英文。

   >[!NOTE]
   >
   >與此部分關聯的快速入門將此值設定為 `fr_FR`*.*

1. 轉譯HTML表單

   叫用 `FormsService` 物件 `renderHTMLForm` 方法，並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案名副檔名。 如果您參考屬於Forms應用程式一部分的表單設計，請務必指定完整路徑，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` 指定HTML首選項類型的枚舉值。 例如，要呈現與Internet Explorer 5.0或更新版本的動態HTML相容的HTML表單，請指定 `TransformTo.MSDHTML`.
   * A `BLOB` 包含要與表單合併資料的物件。 如果您不想合併資料，請傳遞 `null`.
   * 此 `HTMLRenderSpec` 儲存HTML運行時選項的對象。
   * 指定 `HTTP_USER_AGENT` 標題值，例如 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322`)。 如果您不想設定此值，可以傳遞空白字串。
   * A `URLSpec` 用於儲存呈現HTML表單所需的URI值的對象。
   * A `java.util.HashMap` 儲存檔案附件的物件。 此參數為選用參數，您可以指定 `null` 如果您不想將檔案附加到表單。
   * 空白 `com.adobe.idp.services.holders.BLOBHolder` 由填入的物件 `renderHTMLForm` 方法。 此參數值儲存呈現的表單。
   * 空白 `com.adobe.idp.services.holders.BLOBHolder` 由填入的物件 `renderHTMLForm` 方法。 此參數儲存輸出XML資料。
   * 空白 `javax.xml.rpc.holders.LongHolder` 由填入的物件 `renderHTMLForm` 方法。 此引數會儲存表單中的頁數。
   * 空白 `javax.xml.rpc.holders.StringHolder` 由填入的物件 `renderHTMLForm` 方法。 此參數儲存地區設定值。
   * 空白 `javax.xml.rpc.holders.StringHolder` 由填入的物件 `renderHTMLForm` 方法。 此引數會儲存所使用的HTML呈現值。
   * 空白 `com.adobe.idp.services.holders.FormsResultHolder` 包含此操作結果的對象。

   此 `renderHTMLForm` 方法填入 `com.adobe.idp.services.holders.FormsResultHolder` 作為最後一個引數值傳遞的物件，具有必須寫入用戶端網頁瀏覽器的表單資料流。

1. 將表單資料流寫入客戶端Web瀏覽器

   * 建立 `FormResult` 物件，方法是取得 `com.adobe.idp.services.holders.FormsResultHolder` 物件 `value` 資料成員。
   * 建立 `BLOB` 包含表單資料的物件，方法是叫用 `FormsResult` 物件 `getOutputContent` 方法。
   * 取得 `BLOB` 對象 `getContentType` 方法。
   * 設定 `javax.servlet.http.HttpServletResponse` 對象的內容類型，方法是調用 `setContentType` 方法，並傳遞 `BLOB` 物件。
   * 建立 `javax.servlet.ServletOutputStream` 通過調用 `javax.servlet.http.HttpServletResponse` 物件 `getOutputStream` 方法。
   * 建立位元組陣列，並叫用 `BLOB` 物件 `getBinaryData` 方法。 此任務分配 `FormsResult` 位元組陣列的物件。
   * 叫用 `javax.servlet.http.HttpServletResponse` 物件 `write` 將表單資料流傳送至用戶端網頁瀏覽器的方法。 將位元組陣列傳遞至 `write` 方法。

**另請參閱**

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
