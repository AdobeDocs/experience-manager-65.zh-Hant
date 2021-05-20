---
title: 呈現Forms
seo-title: 呈現Forms
description: 使用Forms服務建立互動式資料擷取用戶端應用程式，以驗證、處理、轉換及傳遞通常在Designer中建立的表單。 表單作者可開發單一表單設計，讓Forms服務在各種瀏覽器環境中以PDF、SWF或HTML格式轉譯。
seo-description: 使用Forms服務建立互動式資料擷取用戶端應用程式，以驗證、處理、轉換及傳遞通常在Designer中建立的表單。 表單作者可開發單一表單設計，讓Forms服務在各種瀏覽器環境中以PDF、SWF或HTML格式轉譯。
uuid: 68d7b7bc-7730-4a83-b7b9-ebe2a29d6c51
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/performing_service_operations_using_apis
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: f8749793-e53f-4812-a093-8278f480e6a8
role: Developer
exl-id: ec9ccf04-7cec-493a-91ab-0e399a905338
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# 呈現Forms {#rendering-forms}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

**關於Forms服務**

Forms服務可讓您建立互動式資料擷取用戶端應用程式，以驗證、處理、轉換及傳遞通常在Designer中建立的表單。 表單作者可開發單一表單設計，讓Forms服務在各種瀏覽器環境中以PDF、SWF或HTML格式轉譯。

當使用者要求表單時，用戶端應用程式會將要求傳送至Forms服務，由服務以適當格式傳回表單。 Forms服務收到請求後，會將資料與表單設計合併，然後以所需格式傳送表單。 表單服務輸出是互動式表單，通常是PDF檔案。 互動式表單可讓使用者填寫表單上的欄位。

根據客戶端應用程式的類型，您可以將表單寫入客戶端Web瀏覽器，或將表單另存為PDF檔案。 基於Web的應用程式可以將表單寫入Web瀏覽器。 案頭應用程式可將表單儲存為PDF檔案。 為了演示如何寫出到Web瀏覽器和PDF檔案，*呈現Forms*&#x200B;部分中的快速入門按以下方式組織：

* Java API強類型化（SOAP模式）範例為Java servlet。
* Web服務(Java Base64)示例為Java servlet。
* Web服務(MTOM)範例是主控台應用程式（並非所有快速入門都有MTOM範例）。

>[!NOTE]
>
>有關建立使用java servlet來調用Forms服務的Web應用程式的資訊，請參閱[建立呈現Forms的Web應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)。

您可以透過下列兩種方式之一，將表單設計（XDP檔案）或PDF檔案傳遞至Forms服務：

* 您可以使用URL值來參考表單設計。 此方法涉及使用`URLSpec`物件。 使用`URLSpec`物件的`setContentRootURI`方法，將內容根傳遞至Forms服務。 表單設計名稱(`formQuery`)會以單獨的參數傳遞。 這兩個值會串連，以取得表單設計的絕對參照。 (位於&#x200B;*轉譯Forms*&#x200B;區段的大部分快速入門都使用此方法。)
* 您可以將包含表單設計的`com.adobe.idp.Document`傳遞至Forms服務。 名為`renderPDFForm2`和`renderHTMLForm2`的兩種新方法接受包含表單設計的`com.adobe.idp.Document`對象。 (請參閱[將檔案傳遞至Forms服務](/help/forms/developing/passing-documents-forms-service.md)

您可以使用Forms服務完成下列工作：

* 轉譯互動式PDF forms。 (請參閱[轉譯互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)。)
* 在用戶端轉譯表單。 (請參閱在用戶端上呈現Forms](/help/forms/developing/rendering-forms-client.md) 。)[
* 根據片段轉譯表單。 (請參閱[根據片段呈現Forms](/help/forms/developing/rendering-forms-based-fragments.md)。)
* 呈現已啟用權限的表單。 (請參閱[呈現啟用權限的Forms](/help/forms/developing/rendering-rights-enabled-forms.md)。)
* 將表單轉譯為HTML。 (請參閱[將Forms呈現為HTML](/help/forms/developing/rendering-forms-html.md)。)
* 使用自訂CSS檔案呈現HTML Forms([使用自訂CSS檔案呈現HTML Forms](/help/forms/developing/rendering-html-forms-using-custom.md))。
* 處理提交的表單。 (請參閱[處理已提交的Forms](/help/forms/developing/handling-submitted-forms.md)。)
* 使用已提交的XML資料建立PDF文檔。 （請參閱[使用已提交的XML資料建立PDF文檔](/help/forms/developing/creating-pdf-documents-submitted-xml.md)。）
* 預先填入表單。 (請參閱[使用可流動配置預填Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md)。)
* 傳遞檔案。 (請參閱[將檔案傳遞至Forms服務](/help/forms/developing/passing-documents-forms-service.md)
* 計算表單資料。 （請參閱[計算表單資料](/help/forms/developing/calculating-form-data.md)。）
* 優化應用程式。 (請參閱[最佳化Forms服務的效能](/help/forms/developing/optimizing-performance-forms-service.md)。)

   ***提示&#x200B;**:Adobe開發人員網站包含以下文章，討論如何建立調用Forms服務並呈現表單的ASP.NET應用程式。請參閱[建立表單呈現ASP.NET應用程式](https://www.adobe.com/devnet/livecycle/articles/asp_net.html)。*
