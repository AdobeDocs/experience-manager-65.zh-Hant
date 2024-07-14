---
title: 根據片段轉譯Forms
description: 使用Forms服務來轉譯以使用Designer建立的片段為基礎的表單。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: febf5350-3fc5-48c0-8bc5-198daff15936
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2189'
ht-degree: 0%

---

# 根據片段轉譯Forms {#rendering-forms-based-on-fragments}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

## 根據片段轉譯Forms {#rendering-forms-based-on-fragments-inner}

Forms服務可以轉譯以您使用Designer建立的片段為基礎的表單。 *片段*&#x200B;是可重複使用的表單部分，並儲存為可插入多個表單設計的個別XDP檔案。 例如，片段可以包含位址區塊或合法文字。

使用片段可簡化並加速大量表單的建立與維護。 建立表單時，插入所需片段的參考，片段就會顯示在表單中。 片段參考包含指向實體XDP檔案的子表單。 如需有關根據片段建立表單設計的資訊，請參閱[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)

片段可以包含數個包在選擇子表單集中的子表單。 選擇子表單集根據資料連線的資料流程控制子表單的顯示。 您可以使用條件陳述式來決定集合中哪個子表單會出現在傳遞的表單中。 例如，集合中的每個子表單可以包含特定地理位置的資訊，而顯示的子表單可以根據使用者的位置來決定。

*指令碼片段*&#x200B;包含可重複使用的JavaScript函式或與任何特定物件（例如日期剖析器或Web服務引動）分開儲存的值。 這些片段包含單一指令碼物件，會在「階層」浮動視窗中顯示為變數的子項。 無法從其他物件的屬性指令碼（例如驗證、計算或初始化等事件指令碼）建立片段。

使用片段的優點如下：

* **內容重複使用**：您可以使用片段在多個表單設計中重複使用內容。 當您需要以多個表單使用某些相同內容時，使用片段會比複製或重新建立內容更快更簡單。 使用片段也可確保表單設計中經常使用的部分在所有參考表單中都具有一致的內容和外觀。
* **全域更新**：您可以使用片段在一個檔案中對多個表單進行一次全域變更。 您可以變更片段中的內容、指令碼物件、資料繫結、版面或樣式，而所有參考片段的XDP表單都會反映變更。
* 例如，許多表單的共同元素可能是包含國家/地區下拉式清單物件的位址區塊。 如果您需要更新下拉式清單物件的值，則必須開啟許多表單以進行變更。 如果您將位址區塊納入片段中，則只需開啟一個片段檔案即可進行變更。
* 若要更新PDF表單中的片段，您必須在Designer中重新儲存表單。
* **共用表單建立**：您可以使用片段在數個資源間共用表單的建立。 具備指令碼或Designer其他進階功能專業知識的表單開發人員可開發和共用片段，以運用指令碼和動態屬性。 表單設計人員可以使用這些片段來配置表單設計，並確保表單的所有部分在多人設計的多個表單中都具有一致的外觀和功能。

### 組裝使用片段組裝的表單設計 {#assembling-a-form-design-assembled-using-fragments}

您可以組合表單設計，以根據多個片段傳遞至Forms服務。 若要組裝多個片段，請使用Assembler服務。 若要檢視使用組合服務建立其他Forms服務（輸出服務）使用的表單設計的範例，請參閱[使用片段建立PDF檔案](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)。 您可以使用Forms服務執行相同的工作流程，而不使用輸出服務。

使用Assembler服務時，您傳遞的是使用片段組裝的表單設計。 已建立的表單設計未參考其他片段。 相較之下，本主題將討論傳送參照其他片段至Forms服務的表單設計。 不過，組合器並未組裝表單設計。 它是在Designer中建立的。

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>如需有關建立轉譯片段表單的網頁式應用程式的資訊，請參閱[建立轉譯Forms的網頁應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)。

### 步驟摘要 {#summary-of-steps}

若要根據片段轉譯表單，請執行以下工作：

1. 包含專案檔案。
1. 建立Forms使用者端API物件。
1. 指定URI值。
1. 演算表單。
1. 將表單資料流寫入使用者端網頁瀏覽器。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Forms使用者端API物件**

您必須先建立Forms服務使用者端，才能以程式設計方式執行Forms服務使用者端API作業。

**指定URI值**

若要成功根據片段轉譯表單，您必須確保Forms服務同時找到表單和表單設計參考的片段（XDP檔案）。 例如，假設表單名為PO.xdp，此表單使用名為FooterUS.xdp和FooterCanada.xdp的兩個片段。 在這種情況下，Forms服務必須能夠找到所有三個XDP檔案。

您可以將表單放在某個位置，並將片段放在另一個位置，以組織表單及其片段，或將所有XDP檔案放在同一個位置。 就本節而言，假設所有XDP檔案都在AEM Forms存放庫中。 如需有關將XDP檔案放入AEM Forms存放庫的資訊，請參閱[寫入資源](/help/forms/developing/aem-forms-repository.md#writing-resources)。

根據片段呈現表單時，您必須僅參考表單本身，而非片段。 例如，您必須參考PO.xdp，而非FooterUS.xdp或FooterCanada.xdp。 請確定您將片段放置在Forms服務可找到它們的位置。

**轉譯表單**

以片段為基礎的表單能以與非片段表單相同的方式轉譯。 也就是說，您可以將表單轉譯為PDF、HTML或表單參考線（已棄用）。 本節中的範例將以片段為基礎的表單轉譯為互動式PDF表單。 (請參閱[呈現互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)。)

**將表單資料流寫入使用者端網頁瀏覽器**

Forms服務轉譯表單時，會傳回您必須寫入使用者端網頁瀏覽器的表單資料流。 寫入使用者端網頁瀏覽器時，使用者可看見表單。

**另請參閱**

[使用Java API根據片段轉譯表單](#render-forms-based-on-fragments-using-the-java-api)

[使用網站服務API根據片段轉譯表單](#render-forms-based-on-fragments-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[呈現互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[建立轉譯Forms的網頁應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API根據片段轉譯表單 {#render-forms-based-on-fragments-using-the-java-api}

使用Forms API (Java)根據片段轉譯表單：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms使用者端API物件

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`FormsServiceClient`物件。

1. 指定URI值

   * 使用它的建構函式建立儲存URI值的`URLSpec`物件。
   * 叫用`URLSpec`物件的`setApplicationWebRoot`方法，並傳遞代表應用程式網頁根目錄的字串值。
   * 叫用`URLSpec`物件的`setContentRootURI`方法，並傳遞指定內容根URI值的字串值。 確認表單設計和片段位於內容根URI中。 否則，Forms服務會擲回例外狀況。 若要參考存放庫，請指定`repository://`。
   * 叫用`URLSpec`物件的`setTargetURL`方法，並傳遞字串值，該值指定要將表單資料張貼到的目標URL值。 如果您在表單設計中定義目標URL，您可以傳遞空字串。 您也可以指定傳送表單以執行計算的URL。

1. 演算表單

   叫用`FormsServiceClient`物件的`renderPDFForm`方法，並傳遞下列值：

   * 字串值，指定表單設計名稱，包括副檔名。 如果您參照的表單設計屬於Forms應用程式的一部分，請確定您指定完整路徑，例如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 包含要與表單合併之資料的`com.adobe.idp.Document`物件。 如果您不想合併資料，請傳遞空的`com.adobe.idp.Document`物件。
   * 儲存執行階段選項的`PDFFormRenderSpec`物件。
   * `URLSpec`物件包含Forms服務根據片段轉譯表單所需的URI值。
   * 儲存檔案附件的`java.util.HashMap`物件。 這是選用引數，如果您不想將檔案附加至表單，可以指定`null`。

   `renderPDFForm`方法傳回`FormsResult`物件，其中包含必須寫入使用者端網頁瀏覽器的表單資料流。

1. 將表單資料流寫入使用者端網頁瀏覽器

   * 呼叫`FormsResult`物件的`getOutputContent`方法，以建立`com.adobe.idp.Document`物件。
   * 透過叫用物件的`getContentType`方法，取得`com.adobe.idp.Document`物件的內容型別。
   * 透過叫用其`setContentType`方法並傳遞`com.adobe.idp.Document`物件的內容型別來設定`javax.servlet.http.HttpServletResponse`物件的內容型別。
   * 呼叫`javax.servlet.http.HttpServletResponse`物件的`getOutputStream`方法，建立用來將表單資料流寫入使用者端網頁瀏覽器的`javax.servlet.ServletOutputStream`物件。
   * 呼叫`com.adobe.idp.Document`物件的`getInputStream`方法，以建立`java.io.InputStream`物件。
   * 呼叫`InputStream`物件的`read`方法，並將位元組陣列作為引數傳遞，以表單資料流填入位元組陣列。
   * 叫用`javax.servlet.ServletOutputStream`物件的`write`方法，將表單資料流傳送至使用者端網頁瀏覽器。 將位元組陣列傳遞至`write`方法。

**另請參閱**

[根據片段轉譯Forms](#rendering-forms-based-on-fragments)

[快速入門(SOAP模式)：使用Java API根據片段轉譯表單](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-based-on-fragments-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API根據片段轉譯表單 {#render-forms-based-on-fragments-using-the-web-service-api}

使用Forms API （Web服務）根據片段轉譯表單：

1. 包含專案檔案

   * 建立使用Forms服務WSDL的Java Proxy類別。
   * 將Java Proxy類別納入您的類別路徑中。

1. 建立Forms使用者端API物件

   建立`FormsService`物件並設定驗證值。

1. 指定URI值

   * 使用建構函式建立儲存URI值的`URLSpec`物件。
   * 叫用`URLSpec`物件的`setApplicationWebRoot`方法，並傳遞代表應用程式網頁根目錄的字串值。
   * 叫用`URLSpec`物件的`setContentRootURI`方法，並傳遞指定內容根URI值的字串值。 確認表單設計位於內容根URI中。 否則，Forms服務會擲回例外狀況。 若要參考存放庫，請指定`repository://`。
   * 叫用`URLSpec`物件的`setTargetURL`方法，並傳遞字串值，該值指定要將表單資料張貼到的目標URL值。 如果您在表單設計中定義目標URL，您可以傳遞空字串。 您也可以指定傳送表單以執行計算的URL。

1. 演算表單

   叫用`FormsService`物件的`renderPDFForm`方法，並傳遞下列值：

   * 字串值，指定表單設計名稱，包括副檔名。 如果您參照的表單設計屬於Forms應用程式的一部分，請確定您指定完整路徑，例如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 包含要與表單合併之資料的`BLOB`物件。 如果您不想合併資料，請傳遞`null`。
   * 儲存執行階段選項的`PDFFormRenderSpec`物件。 如果輸入檔案是PDF檔案，則無法設定標籤的PDF選項。 如果輸入檔案是XDP檔案，則可以設定標籤的PDF選項。
   * 包含Forms服務所需URI值的`URLSpec`物件。
   * 儲存檔案附件的`java.util.HashMap`物件。 這是選用引數，如果您不想將檔案附加至表單，可以指定`null`。
   * 方法填入的空白`com.adobe.idp.services.holders.BLOBHolder`物件。 此引數用於儲存演算後的表單。
   * 方法填入的空白`javax.xml.rpc.holders.LongHolder`物件。 此引數會儲存表單中的頁數。
   * 方法填入的空白`javax.xml.rpc.holders.StringHolder`物件。 此引數將會儲存地區設定值。
   * 包含此作業結果的空白`com.adobe.idp.services.holders.FormsResultHolder`物件。

   `renderPDFForm`方法會將必須寫入使用者端網頁瀏覽器的表單資料流，填入作為最後一個引數值傳遞的`com.adobe.idp.services.holders.FormsResultHolder`物件。

1. 將表單資料流寫入使用者端網頁瀏覽器

   * 取得`com.adobe.idp.services.holders.FormsResultHolder`物件之`value`資料成員的值，以建立`FormResult`物件。
   * 呼叫`FormsResult`物件的`getOutputContent`方法，建立包含表單資料的`BLOB`物件。
   * 透過叫用物件的`getContentType`方法，取得`BLOB`物件的內容型別。
   * 透過叫用其`setContentType`方法並傳遞`BLOB`物件的內容型別來設定`javax.servlet.http.HttpServletResponse`物件的內容型別。
   * 呼叫`javax.servlet.http.HttpServletResponse`物件的`getOutputStream`方法，建立用來將表單資料流寫入使用者端網頁瀏覽器的`javax.servlet.ServletOutputStream`物件。
   * 建立位元組陣列，並透過叫用`BLOB`物件的`getBinaryData`方法來填入該陣列。 此工作會將`FormsResult`物件的內容指派給位元組陣列。
   * 叫用`javax.servlet.http.HttpServletResponse`物件的`write`方法，將表單資料流傳送至使用者端網頁瀏覽器。 將位元組陣列傳遞至`write`方法。

**另請參閱**

[根據片段轉譯Forms](#rendering-forms-based-on-fragments)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
