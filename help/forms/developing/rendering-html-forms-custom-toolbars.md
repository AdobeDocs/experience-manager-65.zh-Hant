---
title: 使用CustomToolbars呈現HTMLForms
seo-title: Rendering HTML Forms with CustomToolbars
description: 使用Forms服務自定義使用HTML表單呈現的工具欄。 可以使用Java API和Web服務API使用自定義工具欄呈現HTML表單。
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

# 使用CustomToolbars呈現HTMLForms {#rendering-html-forms-with-customtoolbars}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

## 使用自定義工具欄呈現HTMLForms {#rendering-html-forms-with-custom-toolbars}

使用Forms服務，可以自定義使用HTML窗體呈現的工具欄。 可以自定義工具欄，以通過覆蓋預設CSS樣式來改變其外觀，並通過覆蓋Java指令碼來添加動態行為。 使用名為fscmenu.xml的XML檔案自定義工具欄。 預設情況下，Forms服務從內部指定的URI位置檢索此檔案。

>[!NOTE]
>
>此URI位置位於adobe-forms-core.jar檔案中，該檔案位於adobe-forms-dsc.jar檔案中。 adobe-forms-dsc.jar檔案位於C:\Adobe\Adobe_Experience_Manager_forms\ folder (C:\ is the installation directory)中。 可以使用檔案提取工具（如Win RAR）開啟Adobe。

您可以從此位置複製fscmenu.xml，修改它以滿足您的要求，然後將其放在自定義URI位置。 接下來，使用Forms服務API設定運行時選項，這些選項使用指定位置的fscmenu.xml檔案生成Forms服務。 這些操作導致Forms服務呈現具有自定義工具欄的HTML表單。

除了fscmenu.xml檔案外，還需要獲取以下檔案：

* fscmenu.js
* fscattachments.js
* fscmenu.css
* fscmenu-v.css
* fscmenu-ie.css
* fscdialog.css

fscJS是與每個節點關聯的Java指令碼。 必須為 `div#fscmenu` 節點和 `ul#fscmenuItem` 節點。 JS檔案實現核心工具欄功能，而預設檔案可工作。

fscCSS是與特定節點關聯的樣式表。 CSS檔案中的樣式指定工具欄外觀。 *fscVCSS* 是垂直工具欄的樣式表，它顯示在渲染的HTML窗體的左側。 *fscIECSS* 是用於在Internet Explorer中呈現的HTML表單的樣式表。

確保fscmenu.xml檔案中引用了上述所有檔案。 即，在fscmenu.xml檔案中，指定URI位置以指向這些檔案，以便Forms服務可以找到這些檔案。 預設情況下，這些檔案在以內部關鍵字開頭的URI位置可用 `FSWebRoot` 或 `ApplicationWebRoot`。

要自定義工具欄，請使用外部關鍵字替換關鍵字 `FSToolBarURI`。 此關鍵字表示在運行時傳遞給Forms服務的URI（本節稍後將顯示此方法）。

您還可以指定這些JS和CSS檔案的絕對位置，如https://www.mycompany.com/scripts/misc/fscmenu.js。 在這種情況下，您不需要 `FSToolBarURI` 的雙曲餘切值。

>[!NOTE]
>
>建議不要混合引用這些檔案的方式。 即，所有URI都應使用 `FSToolBarURI` 或絕對位置。

您可以通過開啟adobe表單來獲取JS和CSS檔案。&lt;appserver>.ear檔案。 在此檔案中，開啟adobe-forms-res.war。 所有這些檔案都位於WAR檔案中。 土坯表單。&lt;appserver>.ear檔案位於表單安AEM裝資料夾(C:\ is the installation directory)中。 您可以開啟Adobe表單。&lt;appserver>.ear使用檔案提取工具（如WinRAR）。

以下XML語法顯示了一個fscmenu.xml檔案示例。

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
>粗體文本表示必須引用的CSS和JS檔案的URI。

以下項目介紹如何自定義工具欄：

* 更改 `fscJS`。 `fscCSS`。 `fscVCSS`。 `fscIECSS` 屬性（在fscmenu.xml檔案中），通過使用本節中介紹的方法之一來反映引用檔案的自定義位置(例如， `fscJS="FSToolBarURI/scripts/fscmenu.js"`)。
* 必須指定所有CSS和JS檔案。 如果未修改任何檔案，請在自定義位置提供預設檔案。 可以按本節所述開啟各種檔案來獲取預設檔案。
* 允許為任何檔案提供絕對引用(例如，https://www.example.com/scripts/custom-vertical-fscmenu.css)。
* JS和CSS檔案 `div#fscmenu` 節點對工具欄功能至關重要。 個人 `ul#fscmenuItem` 節點可能或不具有支援的JS或CSS檔案。

**更改本地值**

作為自定義工具欄的一部分，您可以更改工具欄的區域設定值。 就是說，你可以用另外一種語言來顯示。 下圖顯示了以法語顯示的自定義工具欄。

>[!NOTE]
>
>無法以多種語言建立自定義工具欄。 工具欄不能根據區域設定使用不同的XML檔案。

要更改工具欄的區域設定值，請確保fscmenu.xml檔案包含要顯示的語言。 以下XML語法顯示用於顯示法語工具欄的fscmenu.xml檔案。

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
>與此部分關聯的快速啟動使用此XML檔案顯示法文自定義工具欄，如上圖所示。

另外，通過調用 `HTMLRenderSpec` 對象 `setLocale` 方法，並傳遞指定區域設定值的字串值。 例如，通過 `fr_FR` 的子菜單。 Forms服務與本地化工具欄捆綁在一起。

>[!NOTE]
>
>在呈現使用自定義工具欄的HTML表單之前，必須知道HTML表單的呈現方式。 (請參閱 [讓Forms成為HTML](/help/forms/developing/rendering-forms-html.md)。)

有關Forms服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

要呈現包含自定義工具欄的HTML表單，請執行以下任務：

1. 包括項目檔案。
1. 建立FormsJava API對象。
1. 引用自定義fscmenu XML檔案。
1. 呈現HTML窗體。
1. 將表單資料流寫入客戶端Web瀏覽器。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請包括代理檔案。

**建立FormsJava API對象**

在以寫程式方式執行Forms服務支援的操作之前，必須建立Forms客戶端對象。

**引用自定義fscmenu XML檔案**

要呈現包含自定義工具欄的HTML表單，請引用描述工具欄的fscmenu XML檔案。 （本節提供了fscmenu XML檔案的兩個示例。） 另外，確保fscmenu.xml檔案正確指定所有引用檔案的位置。 如本節前面所述，確保所有檔案都由 `FSToolBarURI` 或其絕對位置。

**呈現HTML窗體**

要呈現HTML窗體，請指定在設計器中建立並另存為XDP檔案的窗體設計。 另選HTML轉換類型。 例如，可以指定為Internet Explorer 5.0或更高版本呈現動態HTML的HTML轉換類型。

呈現HTML表單還需要值，如用於呈現其他表單類型的URI值。

**將表單資料流寫入客戶端Web瀏覽器**

當Forms服務呈現HTML表單時，它將返回您必須寫入客戶端Web瀏覽器的表單資料流，以使HTML表單對用戶可見。

**另請參閱**

[使用Java API使用自定義工具欄呈現HTML窗體](#render-an-html-form-with-a-custom-toolbar-using-the-java-api)

[使用Web服務API使用自定義工具欄呈現HTML窗體](#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速啟動](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[呈現互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[讓Forms成為HTML](/help/forms/developing/rendering-forms-html.md)

[建立呈現Forms的Web應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API使用自定義工具欄呈現HTML窗體 {#render-an-html-form-with-a-custom-toolbar-using-the-java-api}

使用Forms服務API(Java)呈現包含自定義工具欄的HTML表單：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-forms-client.jar。

1. 建立FormsJava API對象

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `FormsServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 引用自定義fscmenu XML檔案

   * 建立 `HTMLRenderSpec` 對象。
   * 要使用工具欄呈現HTML窗體，請調用 `HTMLRenderSpec` 對象 `setHTMLToolbar` 方法和通過 `HTMLToolbar` 枚舉值。 例如，要顯示垂直HTML工具欄，請通過 `HTMLToolbar.Vertical`。
   * 通過調用 `HTMLRenderSpec` 對象 `setToolbarURI` 方法並傳遞一個字串值，該字串值指定XML檔案的URI位置。
   * 如果適用，通過調用 `HTMLRenderSpec` 對象 `setLocale` 方法，並傳遞指定區域設定值的字串值。 預設值為英語。

   >[!NOTE]
   >
   >與此部分關聯的快速啟動將此值設定為 `fr_FR`*。*

1. 呈現HTML窗體

   調用 `FormsServiceClient` 對象 `renderHTMLForm` 方法並傳遞以下值：

   * 一個字串值，它指定表單設計名稱，包括檔案副檔名。 如果引用屬於Forms應用程式的表單設計，請確保指定完整路徑，如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * A `TransformTo` 指定HTML首選項類型的枚舉值。 例如，要呈現與Internet Explorer 5.0或更高版本的動態HTML相容的HTML表單，請指定 `TransformTo.MSDHTML`。
   * A `com.adobe.idp.Document` 包含要與窗體合併的資料的對象。 如果不想合併資料，請傳遞一個空 `com.adobe.idp.Document` 的雙曲餘切值。
   * 的 `HTMLRenderSpec` 儲存HTML運行時選項的對象。
   * 一個字串值，它指定 `HTTP_USER_AGENT` 標題值，如 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
   * A `URLSpec` 儲存呈現HTML窗體所需的URI值的對象。
   * A `java.util.HashMap` 儲存檔案附件的對象。 這是可選參數，您可以指定 `null` 的子菜單。

   的 `renderHTMLForm` 方法返回 `FormsResult` 包含必須寫入客戶端web瀏覽器的表單資料流的對象。

1. 將表單資料流寫入客戶端Web瀏覽器

   * 建立 `com.adobe.idp.Document` 通過調用 `FormsResult` 對象s `getOutputContent` 的雙曲餘切值。
   * 獲取的內容類型 `com.adobe.idp.Document` 通過調用對象 `getContentType` 的雙曲餘切值。
   * 設定 `javax.servlet.http.HttpServletResponse` 通過調用對象的內容類型 `setContentType` 方法和傳遞 `com.adobe.idp.Document` 的雙曲餘切值。
   * 建立 `javax.servlet.ServletOutputStream` 用於通過調用Web瀏覽器將表單資料流寫入客戶端的對象 `javax.servlet.http.HttpServletResponse` 對象 `getOutputStream` 的雙曲餘切值。
   * 建立 `java.io.InputStream` 通過調用 `com.adobe.idp.Document` 對象 `getInputStream` 的雙曲餘切值。
   * 通過調用 `InputStream` 對象 `read` 方法，並將位元組陣列作為參數傳遞。
   * 調用 `javax.servlet.ServletOutputStream` 對象 `write` 一種將表單資料流發送到客戶端web瀏覽器的方法。 將位元組陣列傳遞到 `write` 的雙曲餘切值。

**另請參閱**

[快速啟動（SOAP模式）:使用Java API使用自定義工具欄呈現HTML窗體](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API使用自定義工具欄呈現HTML窗體 {#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api}

使用Forms服務API（Web服務）呈現包含自定義工具欄的HTML表單：

1. 包括項目檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 在類路徑中包括Java代理類。

1. 建立FormsJava API對象

   建立 `FormsService` 對象和設定驗證值。

1. 引用自定義fscmenu XML檔案

   * 建立 `HTMLRenderSpec` 對象。
   * 要使用工具欄呈現HTML窗體，請調用 `HTMLRenderSpec` 對象 `setHTMLToolbar` 方法和通過 `HTMLToolbar` 枚舉值。 例如，要顯示垂直HTML工具欄，請通過 `HTMLToolbar.Vertical`。
   * 通過調用 `HTMLRenderSpec` 對象 `setToolbarURI` 方法並傳遞一個字串值，該字串值指定XML檔案的URI位置。
   * 如果適用，通過調用 `HTMLRenderSpec` 對象 `setLocale` 方法，並傳遞指定區域設定值的字串值。 預設值為英語。

   >[!NOTE]
   >
   >與此部分關聯的快速啟動將此值設定為 `fr_FR`*。*

1. 呈現HTML窗體

   調用 `FormsService` 對象 `renderHTMLForm` 方法並傳遞以下值：

   * 一個字串值，它指定表單設計名稱，包括檔案副檔名。 如果引用屬於Forms應用程式的表單設計，請確保指定完整路徑，如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * A `TransformTo` 指定HTML首選項類型的枚舉值。 例如，要呈現與Internet Explorer 5.0或更高版本的動態HTML相容的HTML表單，請指定 `TransformTo.MSDHTML`。
   * A `BLOB` 包含要與窗體合併的資料的對象。 如果不想合併資料，請傳遞 `null`。
   * 的 `HTMLRenderSpec` 儲存HTML運行時選項的對象。
   * 一個字串值，它指定 `HTTP_USER_AGENT` 標題值，如 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322`)。 如果不想設定此值，可以傳遞空字串。
   * A `URLSpec` 儲存呈現HTML窗體所需的URI值的對象。
   * A `java.util.HashMap` 儲存檔案附件的對象。 此參數是可選的，您可以指定 `null` 的子菜單。
   * 空 `com.adobe.idp.services.holders.BLOBHolder` 填充的對象 `renderHTMLForm` 的雙曲餘切值。 此參數值儲存渲染的表單。
   * 空 `com.adobe.idp.services.holders.BLOBHolder` 填充的對象 `renderHTMLForm` 的雙曲餘切值。 此參數儲存輸出XML資料。
   * 空 `javax.xml.rpc.holders.LongHolder` 填充的對象 `renderHTMLForm` 的雙曲餘切值。 此參數儲存窗體中的頁數。
   * 空 `javax.xml.rpc.holders.StringHolder` 填充的對象 `renderHTMLForm` 的雙曲餘切值。 此參數儲存區域設定值。
   * 空 `javax.xml.rpc.holders.StringHolder` 填充的對象 `renderHTMLForm` 的雙曲餘切值。 此參數儲存所使用的HTML呈現值。
   * 空 `com.adobe.idp.services.holders.FormsResultHolder` 包含此操作結果的對象。

   的 `renderHTMLForm` 方法填充 `com.adobe.idp.services.holders.FormsResultHolder` 作為最後一個參數值傳遞的對象，其表單資料流必須寫入客戶端web瀏覽器。

1. 將表單資料流寫入客戶端Web瀏覽器

   * 建立 `FormResult` 通過獲取 `com.adobe.idp.services.holders.FormsResultHolder` 對象 `value` 資料成員。
   * 建立 `BLOB` 通過調用包含表單資料的對象 `FormsResult` 對象 `getOutputContent` 的雙曲餘切值。
   * 獲取的內容類型 `BLOB` 通過調用對象 `getContentType` 的雙曲餘切值。
   * 設定 `javax.servlet.http.HttpServletResponse` 通過調用對象的內容類型 `setContentType` 方法和傳遞 `BLOB` 的雙曲餘切值。
   * 建立 `javax.servlet.ServletOutputStream` 用於通過調用Web瀏覽器將表單資料流寫入客戶端的對象 `javax.servlet.http.HttpServletResponse` 對象 `getOutputStream` 的雙曲餘切值。
   * 建立位元組陣列，並通過調用 `BLOB` 對象 `getBinaryData` 的雙曲餘切值。 此任務分配 `FormsResult` 對象。
   * 調用 `javax.servlet.http.HttpServletResponse` 對象 `write` 一種將表單資料流發送到客戶端web瀏覽器的方法。 將位元組陣列傳遞到 `write` 的雙曲餘切值。

**另請參閱**

[使用Base64編碼調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
