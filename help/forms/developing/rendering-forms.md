---
title: 轉換表單
seo-title: 轉換表單
description: 使用Forms服務來建立互動式資料擷取用戶端應用程式，以驗證、處理、轉換和傳送通常在Designer中建立的表單。 表單製作者可以開發單一表單設計，讓Forms服務在各種瀏覽器環境中以PDF、SWF或HTML格式呈現。
seo-description: 使用Forms服務來建立互動式資料擷取用戶端應用程式，以驗證、處理、轉換和傳送通常在Designer中建立的表單。 表單製作者可以開發單一表單設計，讓Forms服務在各種瀏覽器環境中以PDF、SWF或HTML格式呈現。
uuid: 68d7b7bc-7730-4a83-b7b9-ebe2a29d6c51
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/performing_service_operations_using_apis
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: f8749793-e53f-4812-a093-8278f480e6a8
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 0%

---


# 轉換表單{#rendering-forms}

**關於Forms服務**

Forms服務可讓您建立互動式資料擷取用戶端應用程式，以驗證、處理、轉換和傳遞通常在設計工具中建立的表單。 表單製作者可以開發單一表單設計，讓Forms服務在各種瀏覽器環境中以PDF、SWF或HTML格式呈現。

當使用者要求表單時，用戶端應用程式會將要求傳送至Forms服務，而Forms服務會以適當的格式傳回表單。 當Forms服務收到要求時，它會將資料與表單設計合併，然後以所需格式傳送表單。 表單服務輸出是互動式表單，通常是PDF檔案。 互動式表單可讓使用者填寫表單上的欄位。

視用戶端應用程式類型而定，您可將表單寫入用戶端網頁瀏覽器，或將表單儲存為PDF檔案。 網頁應用程式可將表單寫入網頁瀏覽器。 案頭應用程式可將表單儲存為PDF檔案。 為示範如何寫出至網頁瀏覽器和PDF檔案，以下列方式組織了位於&#x200B;*轉換表單*&#x200B;區段中的快速開始：

* Java API強式型別（SOAP模式）範例是Java servlet。
* Web服務(Java Base64)示例是Java servlet。
* web service(MTOM)範例是主控台應用程式（並非所有快速啟動都有MTOM範例）。

>[!NOTE]
>
>有關建立使用Java Servlet調用Forms服務的Web應用程式的資訊，請參閱[建立轉換Forms的Web應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)。

您可以使用下列兩種方式之一，將表單設計（XDP檔案）或PDF檔案傳遞至Forms服務：

* 您可以使用URL值來參考表單設計。 此方法涉及使用`URLSpec`對象。 使用`URLSpec`物件的`setContentRootURI`方法，將內容根目錄傳遞至Forms服務。 表單設計名稱(`formQuery`)會作為單獨的參數傳遞。 這兩個值會串連起來，以取得表單設計的絕對參照。 （位於&#x200B;*演算表單*&#x200B;區段中的大部分快速開始使用此方法。）
* 您可以將包含表單設計的`com.adobe.idp.Document`傳遞至Forms服務。 名為`renderPDFForm2`和`renderHTMLForm2`的兩種新方法接受包含表單設計的`com.adobe.idp.Document`物件。 (請參閱[將檔案傳送至Forms Service](/help/forms/developing/passing-documents-forms-service.md)

您可以使用Forms服務完成下列工作：

* 轉換互動式PDF表單。 （請參閱[轉換互動式PDF表單](/help/forms/developing/rendering-interactive-pdf-forms.md)）。
* 在用戶端上演算表格。 （請參閱用戶端上的[轉換表單。）](/help/forms/developing/rendering-forms-client.md)
* 根據片段來轉換表單。 （請參閱[根據片段呈現表單](/help/forms/developing/rendering-forms-based-fragments.md)）。
* 轉譯啟用權限的表單。 （請參閱[轉換啟用權限的表單](/help/forms/developing/rendering-rights-enabled-forms.md)）。
* 將表單轉換為HTML。 （請參閱[將表單轉換為HTML](/help/forms/developing/rendering-forms-html.md)）。
* 使用自訂CSS檔案轉換HTML表單（[使用自訂CSS檔案轉換HTML表單](/help/forms/developing/rendering-html-forms-using-custom.md)）。
* 處理提交的表單。 （請參閱[處理提交的表單](/help/forms/developing/handling-submitted-forms.md)）。
* 使用已提交的XML資料建立PDF檔案。 （請參閱[使用已提交的XML資料建立PDF檔案](/help/forms/developing/creating-pdf-documents-submitted-xml.md)）。
* 預先填入表格。 （請參閱[使用可排程版面預填表單](/help/forms/developing/prepopulating-forms-flowable-layouts.md)）。
* 傳遞檔案。 (請參閱[將檔案傳送至Forms Service](/help/forms/developing/passing-documents-forms-service.md)
* 計算表單資料。 （請參閱[計算表單資料](/help/forms/developing/calculating-form-data.md)）。
* 最佳化應用程式。 （請參閱[優化Forms Service的效能](/help/forms/developing/optimizing-performance-forms-service.md)。）

   ***提示&#x200B;**:Adobe開發人員網站包含下列文章，討論如何建立叫用Forms服務並轉譯表單的ASP.NET應用程式。請參閱[建立表單渲染ASP.NET應用程式](https://www.adobe.com/devnet/livecycle/articles/asp_net.html)。*

