---
title: 渲染Forms
seo-title: Rendering Forms
description: 使用Forms服務可建立互動式資料捕獲客戶端應用程式，以驗證、處理、轉換和傳遞通常在設計器中建立的表單。 表單作者可以開發Forms服務在各種瀏覽器環境中以PDF、SWF或HTML方式呈現的單一表單設計。
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

# 渲染Forms {#rendering-forms}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

**關於Forms**

通過Forms服務，您可以建立互動式資料捕獲客戶端應用程式，這些應用程式可驗證、處理、轉換和傳遞通常在設計器中建立的表單。 表單作者可以開發Forms服務在各種瀏覽器環境中以PDF、SWF或HTML方式呈現的單一表單設計。

當最終用戶請求表單時，客戶端應用程式將請求發送到Forms服務，該服務以適當的格式返回表單。 一旦Forms服務收到請求，它就會將資料與表單設計合併，然後以所需格式遞送表單。 表單服務輸出是互動式表單，通常是PDF文檔。 互動式表單使用戶能夠填寫表單上的欄位。

根據客戶端應用程式的類型，您可以將表單寫入客戶端Web瀏覽器或將表單另存為PDF檔案。 基於Web的應用程式可以將表單寫入Web瀏覽器。 案頭應用程式可以將表單另存為PDF檔案。 要演示如何寫出到Web瀏覽器和PDF檔案，請快速啟動 *渲染Forms* 組成：

* Java API強類型（SOAP模式）示例是Java Servlet。
* Web服務(Java Base64)示例是Java Servlet。
* Web服務(MTOM)示例是控制台應用程式（並非所有快速啟動都有MTOM示例）。

>[!NOTE]
>
>有關建立使用java servlet調用Forms服務的Web應用程式的資訊，請參見 [建立呈現Forms的Web應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)。

您可以通過以下兩種方式之一將表單設計（XDP檔案）或PDF文檔傳遞給Forms服務：

* 可以使用URL值引用表單設計。 此方法涉及使用 `URLSpec` 的雙曲餘切值。 內容根目錄將通過 `URLSpec` 對象 `setContentRootURI` 的雙曲餘切值。 窗體設計名稱( `formQuery`)作為單獨的參數傳遞。 將這兩個值連接起來，以獲得對表單設計的絕對參照。 (大多數快速啟動位於 *渲染Forms* 部分使用此方法。)
* 你可以通過 `com.adobe.idp.Document` 包含Forms服務的表格設計。 兩種新方法名為 `renderPDFForm2` 和 `renderHTMLForm2` 接受 `com.adobe.idp.Document` 包含窗體設計的對象。 (請參閱 [將檔案轉給Forms](/help/forms/developing/passing-documents-forms-service.md)

您可以使用Forms服務完成以下任務：

* 呈現互動式PDF forms。 (請參閱 [呈現互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)。)
* 在客戶端上呈現表單。 (請參閱 [在客戶端呈現Forms](/help/forms/developing/rendering-forms-client.md)。)
* 基於片段呈現表單。 (請參閱 [基於片段呈現Forms](/help/forms/developing/rendering-forms-based-fragments.md)。)
* 呈現啟用權限的表單。 (請參閱 [啟用版權的呈現Forms](/help/forms/developing/rendering-rights-enabled-forms.md)。)
* 將表單渲染為HTML。 (請參閱 [讓Forms成為HTML](/help/forms/developing/rendering-forms-html.md)。)
* 使用自定義CSS檔案呈現HTMLForms([使用自定義CSS檔案呈現HTMLForms](/help/forms/developing/rendering-html-forms-using-custom.md)。)
* 處理提交的表單。 (請參閱 [處理已提交的Forms](/help/forms/developing/handling-submitted-forms.md)。)
* 使用已提交的XML資料建立PDF文檔。 (請參閱 [使用已提交的XML資料建立PDF文檔](/help/forms/developing/creating-pdf-documents-submitted-xml.md)。)
* 預填充表單。 (請參閱 [用可流式佈局預填充Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md)。)
* 傳遞文檔。 (請參閱 [將檔案轉給Forms](/help/forms/developing/passing-documents-forms-service.md)
* 計算表單資料。 (請參閱 [計算表單資料](/help/forms/developing/calculating-form-data.md)。)
* 優化應用程式。 (請參閱 [優化Forms服務的效能](/help/forms/developing/optimizing-performance-forms-service.md)。)
