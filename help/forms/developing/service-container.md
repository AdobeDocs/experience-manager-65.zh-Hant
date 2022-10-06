---
title: 服務容器
seo-title: Service container
description: AEM Forms服務位於服務容器中
uuid: 89f2fd3d-63d7-4b70-b335-47314441f3ec
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding, development-tools
discoiquuid: dd9c0ec4-a195-4b78-8992-81d0efcc0a7e
role: Developer
exl-id: 6abf2401-5a87-4f72-9028-74580df5b9de
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# 服務容器 {#service-container}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

位於服務容器中的AEM Forms服務（包括標準服務，如加密服務、長期和短期進程）可以使用各種提供程式（如EJB提供程式）調用。 EJB提供程式允許通過RMI/IIOP調用AEM Forms服務。 Web服務提供程式使用SOAP/HTTP和SOAP/JMS等標準將服務作為Web服務（WSDL生成）公開。

下表說明以程式設計方式叫用AEM Forms服務的不同方式。

<table>
 <thead>
  <tr>
   <th><p>調用方法</p></th>
   <th><p>說明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>遠端整合</p></td>
   <td><p>遠端整合讓Flex用戶端能夠叫用服務操作。 (請參閱 <a href="/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting">使用叫用AEM Forms(AEM表單已淘汰)AEM Forms Remoting</a>.)</p></td>
  </tr>
  <tr>
   <td><p>Java API</p></td>
   <td><p>Java API可叫用AEM Forms服務。 Java API會組織為用戶端程式庫和Java叫用API。 (請參閱 <a href="/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api">使用Java API叫用AEM Forms</a>.)</p></td>
  </tr>
  <tr>
   <td><p>網站服務</p></td>
   <td><p>AEM Forms支援SOAP/HTTP等網站服務標準。 服務可以作為Web服務公開，WSDL符合W3C定義的Web服務標準。</p><p>可從任何Web服務堆棧(包括.NET Framework和Sun™ Web Services SDK)中調用服務。 (請參閱 <a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services">使用Web服務叫用AEM Forms</a>.)</p></td>
  </tr>
  <tr>
   <td><p>REST要求</p></td>
   <td><p>AEM Forms支援REST要求。 可從HTML頁面直接叫用服務。 (請參閱 <a href="/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests">使用REST要求叫用AEM Forms</a>.)</p></td>
  </tr>
 </tbody>
</table>

下圖以視覺化方式呈現以程式設計方式叫用AEM Forms服務的不同方式。

>[!NOTE]
>
>除了使用AEM Forms SDK建立可叫用AEM Forms服務的用戶端應用程式外，您也可以建立可部署至服務容器的元件。 例如，您可以建立包含可用於流程的自訂資料類型的銀行元件。 也就是說，您可以建立資料類型，例如 `com.adobe.idp.BankAccount`. 然後，您可以建立 `com.adobe.idp.BankAccount` 例項。

服務容器提供下列功能：

* 允許使用不同方法叫用AEM Forms服務。 您可以設定端點來設定服務，以便使用所有方法叫用該服務：遠端、Java API、網站服務及REST。 (請參閱 [以寫程式方式管理端點](/help/forms/developing/programmatically-endpoints.md#programmatically-managing-endpoints).)
* 將消息轉換為稱為調用請求的標準化格式。 調用請求從客戶端應用程式（或其他服務）發送到位於服務容器中的服務。 調用請求包含諸如要調用的服務的名稱和執行該操作所需的資料值之類的資訊。 許多服務都需要文檔來執行操作。 因此，調用請求通常包含一個文檔，它可以是PDF資料、XDP資料、XML資料等。
* 將調用請求路由到相應的服務（要調用的服務的名稱是調用請求的一部分）。
* 執行任務，如確定調用者是否具有調用指定服務操作的權限。 調用請求必須包含有效的AEM表單用戶名和密碼。

   向服務發送調用請求有不同的方法。 此外，您也可透過不同方式將必要的輸入值傳送至服務。 例如，假設您使用Java API來叫用需要PDF檔案的服務。 相應的Java方法包含接受PDF文檔的參數。 在此情況下，參數的資料類型為 `com.adobe.idp.Document`. (請參閱 [使用Java API將資料傳遞至AEM Forms服務](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api).)

   如果您使用觀看資料夾叫用服務，則當您將檔案置於已設定的觀看資料夾時，會傳送叫用請求。 如果您使用電子郵件叫用服務，則當電子郵件到達配置的收件箱時，將向服務發送調用請求。

   執行操作後，服務容器會傳回呼叫回應。 調用響應包含諸如操作結果之類的資訊。 例如，如果操作修改PDF文檔，則調用響應包含修改的PDF文檔。 如果操作失敗，則調用響應將包含錯誤消息。

   可以用發送調用請求的相同方式來檢索調用響應。 也就是說，如果使用Java API傳送叫用請求，則可使用Java API擷取叫用回應。 例如，假設操作修改PDF文檔。 通過獲取調用服務的Java方法的返回值，可以檢索修改的PDF文檔。

   當調用長壽命進程時，調用響應包含與調用請求相關聯的標識符值。 使用此識別碼值，您稍後可以檢查程式狀態。 例如，請考慮MortgageLoan長期服務。 使用標識符值，可以檢查以確定該過程是否成功完成。 (請參閱 [調用以人為中心的長壽命過程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).)

   下圖顯示叫用服務的用戶端應用程式（使用Java API）。

   當客戶端應用程式調用服務時，會發生三個事件：

   1. 客戶端應用程式向服務發送調用請求。
   1. 服務執行調用請求中指定的操作。
   1. 服務容器將調用響應返回到客戶端應用程式。

**另請參閱**

[了解AEM Forms程式](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)

[使用叫用AEM Forms(AEM表單已淘汰)AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[使用Java API叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[使用Web服務叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)

[調用以人為中心的長壽命過程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[使用REST要求叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests)
