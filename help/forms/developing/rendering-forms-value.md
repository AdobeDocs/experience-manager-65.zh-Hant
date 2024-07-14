---
title: 依值呈現Forms
description: 使用Forms API (Java)透過Java API和網站服務API依值轉譯表單。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: a3a6a06d-ec90-4147-a5f0-e776a086ee12
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1822'
ht-degree: 0%

---

# 依值呈現Forms {#rendering-forms-by-value}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

通常，在Designer中建立的表單設計會參考Forms服務傳遞。 表單設計可能很大，因此參考傳遞它們會更有效率，不必依值封送表單設計位元組。 Forms服務也可以快取表單設計，以便在快取時不需要持續讀取表單設計。

如果表單設計包含UUID屬性，則會快取該屬性。 UUID值在所有表單設計中都是獨一無二的，可用來唯一識別表單。 依值呈現表單時，只有在表單重複使用時才應快取表單。 不過，如果表單未重複使用且必須是唯一的，您可以避免使用使用AEM Forms API設定的快取選項來快取表單。

Forms服務也可以解析表單設計內連結內容的位置。 例如，從表單設計內參照的連結影像是相對URL。 系統會一律假設連結內容與表單設計位置相關。 因此，解決連結內容的問題在於透過將相對路徑套用至絕對表單設計位置來決定其位置。

您可以按值傳遞表單設計，而不是以參考傳遞表單設計。 以值傳遞表單設計在動態建立表單設計時很有效；也就是說，當使用者端應用程式在執行階段產生建立表單設計的XML時。 在此情況下，表單設計不會儲存在實體存放庫中，因為它儲存在記憶體中。 在執行階段動態建立表單設計並按值傳遞時，您可以快取表單並改善Forms服務的效能。

**依值傳遞表單的限制**

當表單設計以值傳遞時，以下限制適用：

* 表單設計內沒有相對連結的內容。 所有影像和片段都必須嵌入表單設計內，或絕對參照。
* 轉譯表單後無法執行伺服器端計算。 如果表單提交回Forms服務，系統就會擷取並傳回資料，而不會進行任何伺服器端計算。
* 由於HTML只能在執行階段使用連結的影像，因此無法產生含有內嵌影像的HTML。 這是因為Forms服務可透過從參照的表單設計擷取影像，支援具有HTML的內嵌影像。 由於以值傳遞的表單設計沒有參考位置，因此在顯示HTML頁面時無法擷取內嵌影像。 因此，影像參照必須是絕對路徑，才能以HTML呈現。

>[!NOTE]
>
>雖然您可以依值呈現不同型別的表單(例如，包含使用許可權的HTML表單或表單)，本節將討論呈現互動式PDF forms。

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步驟摘要 {#summary-of-steps}

若要依值呈現表單，請執行下列步驟：

1. 包含專案檔案。
1. 建立Forms使用者端API物件。
1. 參考表單設計。
1. 依值轉譯表單。
1. 將表單資料流寫入使用者端網頁瀏覽器。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，則請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立Forms使用者端API物件**

您必須先建立資料整合服務使用者端，才能以程式設計方式將資料從使用者端API匯入PDF。 建立服務使用者端時，您可以定義呼叫服務所需的連線設定。

**參考表單設計**

依值呈現表單時，您必須建立包含要呈現之表單設計的`com.adobe.idp.Document`物件。 您可以參考現有的XDP檔案，也可以在執行階段動態建立表單設計，並將該資料填入`com.adobe.idp.Document`。

>[!NOTE]
>
>此區段和對應的快速入門會參考現有的XDP檔案。

**依據值演算表單**

若要依值轉譯表單，請將包含表單設計的`com.adobe.idp.Document`執行個體傳遞給轉譯方法的`inDataDoc`引數（可以是`FormsServiceClient`物件的任何轉譯方法，例如`renderPDFForm`、`(Deprecated) renderHTMLForm`等）。 此引數值通常會保留給合併至表單的資料。 同樣地，將空字串值傳遞至`formQuery`引數。 通常，此引數需要字串值，用以指定表單設計的名稱。

>[!NOTE]
>
>如果您想要在表單中顯示資料，必須在`xfa:datasets`元素中指定資料。 如需XFA架構的相關資訊，請前往[https://www.pdfa.org/norm-refs/XFA-3_3.pdf](https://www.pdfa.org/norm-refs/XFA-3_3.pdf)。

**將表單資料流寫入使用者端網頁瀏覽器**

當Forms服務依值轉譯表單時，會傳回您必須寫入使用者端網頁瀏覽器的表單資料流。 寫入使用者端網頁瀏覽器時，使用者可看見表單。

**另請參閱**

[使用Java API依值轉譯表單](#render-a-form-by-value-using-the-java-api)

[使用網站服務API依值轉譯表單](#render-a-form-by-value-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[將檔案傳遞至Forms服務](/help/forms/developing/passing-documents-forms-service.md)

[建立轉譯Forms的網頁應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API依值轉譯表單 {#render-a-form-by-value-using-the-java-api}

使用Forms API (Java)依值轉譯表單：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms使用者端API物件

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`FormsServiceClient`物件。

1. 參考表單設計

   * 使用表單設計的建構函式，並傳遞指定XDP檔案位置的字串值，建立代表要呈現之表單設計的`java.io.FileInputStream`物件。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 依值演算表單

   叫用`FormsServiceClient`物件的`renderPDFForm`方法，並傳遞下列值：

   * 空字串值。 （此引數通常需要字串值，用以指定表單設計的名稱。）
   * 包含表單設計的`com.adobe.idp.Document`物件。 通常，此引數值會保留給合併至表單的資料。
   * 儲存執行階段選項的`PDFFormRenderSpec`物件。 這是選用引數，如果您不想指定執行階段選項，可以指定`null`。
   * 包含Forms服務所需URI值的`URLSpec`物件。
   * 儲存檔案附件的`java.util.HashMap`物件。 這是選用引數，如果您不想將檔案附加至表單，可以指定`null`。

   `renderPDFForm`方法傳回`FormsResult`物件，其中包含可寫入使用者端網頁瀏覽器的表單資料流。

1. 將表單資料流寫入使用者端網頁瀏覽器

   * 呼叫`FormsResult`物件的`getOutputContent`方法，以建立`com.adobe.idp.Document`物件。
   * 透過叫用物件的`getContentType`方法，取得`com.adobe.idp.Document`物件的內容型別。
   * 透過叫用其`setContentType`方法並傳遞`com.adobe.idp.Document`物件的內容型別來設定`javax.servlet.http.HttpServletResponse`物件的內容型別。
   * 呼叫`javax.servlet.http.HttpServletResponse`物件的`getOutputStream`方法，建立用來將表單資料流寫入使用者端網頁瀏覽器的`javax.servlet.ServletOutputStream`物件。
   * 呼叫`com.adobe.idp.Document`物件的`getInputStream`方法，以建立`java.io.InputStream`物件。
   * 建立位元組陣列並配置`InputStream`物件的大小。 叫用`InputStream`物件的`available`方法以取得`InputStream`物件的大小。
   * 叫用`InputStream`物件的`read`方法，並將位元組陣列作為引數傳遞，以表單資料串流填入位元組陣列。
   * 叫用`javax.servlet.ServletOutputStream`物件的`write`方法，將表單資料流傳送至使用者端網頁瀏覽器。 將位元組陣列傳遞至`write`方法。

**另請參閱**

[依值呈現Forms](/help/forms/developing/rendering-forms.md)

[快速入門(SOAP模式)：使用Java API依值轉譯](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用網站服務API依值轉譯表單 {#render-a-form-by-value-using-the-web-service-api}

使用Forms API （Web服務）依值轉譯表單：

1. 包含專案檔案

   * 建立使用Forms服務WSDL的Java Proxy類別。
   * 將Java Proxy類別納入您的類別路徑中。

1. 建立Forms使用者端API物件

   建立`FormsService`物件並設定驗證值。

1. 參考表單設計

   * 使用物件的建構函式建立`java.io.FileInputStream`物件。 傳遞字串值，指定XDP檔案的位置。
   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存以密碼加密的PDF檔案。
   * 建立位元組陣列以儲存`java.io.FileInputStream`物件的內容。 您可以使用其`available`方法取得`java.io.FileInputStream`物件的大小，以決定位元組陣列的大小。
   * 呼叫`java.io.FileInputStream`物件的`read`方法並傳遞位元組陣列，以串流資料填入位元組陣列。
   * 叫用物件的`setBinaryData`方法並傳遞位元組陣列以填入`BLOB`物件。

1. 依值演算表單

   叫用`FormsService`物件的`renderPDFForm`方法，並傳遞下列值：

   * 空字串值。 （此引數通常需要字串值，用以指定表單設計的名稱。）
   * 包含表單設計的`BLOB`物件。 通常，此引數值會保留給合併至表單的資料。
   * 儲存執行階段選項的`PDFFormRenderSpec`物件。 這是選用引數，如果您不想指定執行階段選項，可以指定`null`。
   * 包含Forms服務所需URI值的`URLSpec`物件。
   * 儲存檔案附件的`java.util.HashMap`物件。 這是選用引數，如果您不想將檔案附加至表單，可以指定`null`。
   * 方法填入的空白`com.adobe.idp.services.holders.BLOBHolder`物件。 這可用來儲存轉譯的PDF表單。
   * 方法填入的空白`javax.xml.rpc.holders.LongHolder`物件。 （此引數會以表單儲存頁數。）
   * 方法填入的空白`javax.xml.rpc.holders.StringHolder`物件。 （此引數會儲存地區設定值。）
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

[依值呈現Forms](#rendering-forms-by-value)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
