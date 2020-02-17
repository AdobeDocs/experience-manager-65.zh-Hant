---
title: 轉換表單
seo-title: 轉換表單
description: 'null'
seo-description: 'null'
uuid: 68d7b7bc-7730-4a83-b7b9-ebe2a29d6c51
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/performing_service_operations_using_apis
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: f8749793-e53f-4812-a093-8278f480e6a8
translation-type: tm+mt
source-git-commit: 687cdacc2868de16a4df968dddedd330ce3317bb

---


# 轉換表單 {#rendering-forms}

**關於Forms服務**

Forms服務可讓您建立互動式資料擷取用戶端應用程式，以驗證、處理、轉換和傳遞通常在設計工具中建立的表單。 表單製作者可以開發單一表單設計，讓Forms服務在各種瀏覽器環境中以PDF、SWF或HTML格式呈現。

當使用者要求表單時，用戶端應用程式會將要求傳送至Forms服務，而Forms服務會以適當的格式傳回表單。 當Forms服務收到要求時，它會將資料與表單設計合併，然後以所需格式傳送表單。 表單服務輸出是互動式表單，通常是PDF檔案。 互動式表單可讓使用者填寫表單上的欄位。

視用戶端應用程式類型而定，您可將表單寫入用戶端網頁瀏覽器，或將表單儲存為PDF檔案。 網頁應用程式可將表單寫入網頁瀏覽器。 案頭應用程式可將表單儲存為PDF檔案。 為示範如何寫出至網頁瀏覽器和PDF檔案，「轉換表單」區段中的快速開始會以下列方式組織： **

* Java API強式型別（SOAP模式）範例是Java servlet。
* Web服務(Java Base64)示例是Java servlet。
* web service(MTOM)範例是主控台應用程式（並非所有快速啟動都有MTOM範例）。

***注意&#x200B;**:有關建立使用java servlet調用Forms服務的Web應用程式的資訊，請參[閱建立轉換表單的Web應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)。*


您可以使用下列兩種方式之一，將表單設計（XDP檔案）或PDF檔案傳遞至Forms服務：

* 您可以使用URL值來參考表單設計。 此方法涉及使用 `URLSpec` 物件。 內容根目錄會使用物件的方法傳 `URLSpec` 遞至Forms服 `setContentRootURI` 務。 表單設計名稱( `formQuery`)會以個別參數傳遞。 這兩個值會串連起來，以取得表單設計的絕對參照。 (「轉換表單」區段中的大部分快 *速開始* ，都採用此方法。)
* 您可以將包含表 `com.adobe.idp.Document` 單設計的表單傳遞至Forms服務。 命名和接受包 `renderPDFForm2` 含表 `renderHTMLForm2` 單設 `com.adobe.idp.Document` 計的物件的兩種新方法。 (請參 [閱將檔案傳送至Forms服務](/help/forms/developing/passing-documents-forms-service.md)

您可以使用Forms服務完成下列工作：

* 轉換互動式PDF表單。 (請參 [閱轉換互動式PDF表單](/help/forms/developing/rendering-interactive-pdf-forms.md)。)
* 在用戶端上演算表格。 (請參 [閱用戶端上的轉譯表單](/help/forms/developing/rendering-forms-client.md)。)
* 根據片段來轉換表單。 (請參 [閱根據片段轉譯表單](/help/forms/developing/rendering-forms-based-fragments.md))。
* 轉譯啟用權限的表單。 (請參 [閱轉換啟用權限的表單](/help/forms/developing/rendering-rights-enabled-forms.md)。)
* 將表單轉換為HTML。 (請參 [閱「將表單轉換為HTML](/help/forms/developing/rendering-forms-html.md)」)。
* 使用自訂CSS檔案轉換HTML表格(使[用自訂CSS檔案轉換HTML表格](/help/forms/developing/rendering-html-forms-using-custom.md))。
* 處理提交的表單。 (請參 [閱處理提交的表單](/help/forms/developing/handling-submitted-forms.md)。)
* 使用已提交的XML資料建立PDF檔案。 (請參 [閱使用提交的XML資料建立PDF檔案](/help/forms/developing/creating-pdf-documents-submitted-xml.md)。)
* 預先填入表格。 (請參 [閱使用可排程版面預填表單](/help/forms/developing/prepopulating-forms-flowable-layouts.md)。)
* 傳遞檔案。 (請參 [閱將檔案傳送至Forms服務](/help/forms/developing/passing-documents-forms-service.md)
* 計算表單資料。 (請參閱 [計算表單資料](/help/forms/developing/calculating-form-data.md)。)
* 最佳化應用程式。 (請參 [閱最佳化Forms服務的效能](/help/forms/developing/optimizing-performance-forms-service.md)。)

   ***提示&#x200B;**:Adobe開發人員網站包含下列文章，討論如何建立叫用Forms服務並轉譯表單的ASP.NET應用程式。 請參[閱建立表單渲染ASP.NET應用程式](https://www.adobe.com/devnet/livecycle/articles/asp_net.html)。*

