---
title: 呈現Forms
seo-title: Rendering Forms
description: 使用Forms服務建立互動式資料擷取用戶端應用程式，以驗證、處理、轉換及傳遞通常在Designer中建立的表單。 表單作者可開發單一表單設計，讓Forms服務在各種瀏覽器環境中轉譯為PDF、SWF或HTML。
seo-description: Use the Forms service to create interactive data capture client applications that validate, process, transform, and deliver forms typically created in Designer. Form authors can develop a single form design that the Forms service renders in PDF, SWF, or HTML in various browser environments.
uuid: 68d7b7bc-7730-4a83-b7b9-ebe2a29d6c51
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/performing_service_operations_using_apis
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: f8749793-e53f-4812-a093-8278f480e6a8
role: Developer
exl-id: ec9ccf04-7cec-493a-91ab-0e399a905338
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---

# 呈現Forms {#rendering-forms}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

**關於Forms服務**

Forms服務可讓您建立互動式資料擷取用戶端應用程式，以驗證、處理、轉換及傳遞通常在Designer中建立的表單。 表單作者可開發單一表單設計，讓Forms服務在各種瀏覽器環境中轉譯為PDF、SWF或HTML。

當使用者要求表單時，用戶端應用程式會將要求傳送至Forms服務，由服務以適當格式傳回表單。 Forms服務收到請求後，會將資料與表單設計合併，然後以所需格式傳送表單。 表單服務輸出是互動式表單，通常是PDF檔案。 互動式表單可讓使用者填寫表單上的欄位。

根據客戶端應用程式的類型，您可以將表單寫入客戶端Web瀏覽器，或將表單另存為PDF檔案。 基於Web的應用程式可以將表單寫入Web瀏覽器。 案頭應用程式可將表單儲存為PDF檔案。 若要示範如何寫出至網頁瀏覽器和PDF檔案，請快速入門 *呈現Forms* 區段的組織方式如下：

* Java API強類型化（SOAP模式）範例為Java servlet。
* Web服務(Java Base64)示例為Java servlet。
* Web服務(MTOM)範例是主控台應用程式（並非所有快速入門都有MTOM範例）。

>[!NOTE]
>
>如需建立使用java servlet來叫用Forms服務的Web應用程式的相關資訊，請參閱 [建立可轉譯Forms的網頁應用程式](/help/forms/developing/creating-web-applications-renders-forms.md).

您可以透過下列兩種方式之一，將表單設計（XDP檔案）或PDF檔案傳遞至Forms服務：

* 您可以使用URL值來參考表單設計。 此方法包括使用 `URLSpec` 物件。 內容根會使用 `URLSpec` 物件 `setContentRootURI` 方法。 表單設計名稱( `formQuery`)會以個別參數的形式傳遞。 這兩個值會串連，以取得表單設計的絕對參照。 (大部分快速入門位於 *呈現Forms* 小節使用此方法。)
* 您可以傳遞 `com.adobe.idp.Document` 包含Forms服務的表單設計。 兩種新方法已命名 `renderPDFForm2` 和 `renderHTMLForm2` 接受 `com.adobe.idp.Document` 包含表單設計的物件。 (請參閱 [將檔案傳遞至Forms服務](/help/forms/developing/passing-documents-forms-service.md)

您可以使用Forms服務完成下列工作：

* 轉譯互動式PDF forms。 (請參閱 [轉譯互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md).)
* 在用戶端轉譯表單。 (請參閱 [在用戶端呈現Forms](/help/forms/developing/rendering-forms-client.md).)
* 根據片段轉譯表單。 (請參閱 [根據片段轉譯Forms](/help/forms/developing/rendering-forms-based-fragments.md).)
* 呈現已啟用權限的表單。 (請參閱 [呈現已啟用權限的Forms](/help/forms/developing/rendering-rights-enabled-forms.md).)
* 將表單轉譯為HTML。 (請參閱 [將Forms轉譯為HTML](/help/forms/developing/rendering-forms-html.md).)
* 使用自訂CSS檔案呈現HTMLForms([使用自訂CSS檔案呈現HTMLForms](/help/forms/developing/rendering-html-forms-using-custom.md).)
* 處理提交的表單。 (請參閱 [處理已提交的Forms](/help/forms/developing/handling-submitted-forms.md).)
* 使用已提交的XML資料建立PDF文檔。 (請參閱 [使用已提交的XML資料建立PDF文檔](/help/forms/developing/creating-pdf-documents-submitted-xml.md).)
* 預先填入表單。 (請參閱 [使用可流式配置預填Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
* 傳遞檔案。 (請參閱 [將檔案傳遞至Forms服務](/help/forms/developing/passing-documents-forms-service.md)
* 計算表單資料。 (請參閱 [計算表單資料](/help/forms/developing/calculating-form-data.md).)
* 優化應用程式。 (請參閱 [最佳化Forms服務的效能](/help/forms/developing/optimizing-performance-forms-service.md).)
