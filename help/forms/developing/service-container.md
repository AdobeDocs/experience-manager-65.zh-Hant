---
title: 服務容器
seo-title: 服務容器
description: AEM Forms服務位於服務容器中
uuid: 89f2fd3d-63d7-4b70-b335-47314441f3ec
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding, development-tools
discoiquuid: dd9c0ec4-a195-4b78-8992-81d0efcc0a7e
role: 開發人員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 0%

---


# 服務容器{#service-container}

**本文中的範例和範例僅適用於AEM Forms的JEE環境。**

位於服務容器中的AEM Forms服務（包括標準服務，如加密服務、長壽命和短壽命進程）可使用各種提供者（如EJB提供者）來呼叫。 EJB提供程式允許通過RMI/IIOP調用AEM Forms服務。 Web服務提供者使用標準（例如SOAP/HTTP和SOAP/JMS），將服務公開為Web服務（WSDL產生）。

下表說明您以程式設計方式叫用AEM Forms服務的不同方式。

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
   <td><p>遠程整合使Flex客戶機能夠調用服務操作。 (請參閱<a href="/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting">使用(表單不建議使用AEM)AEM Forms·里莫廷叫用AEM Forms。)</a></p></td>
  </tr>
  <tr>
   <td><p>Java API</p></td>
   <td><p>Java API可以叫用AEM Forms服務。 Java API會組織為用戶端程式庫和Java呼叫API。 (請參閱<a href="/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api">使用Java API叫用AEM Forms。)</a></p></td>
  </tr>
  <tr>
   <td><p>網站服務</p></td>
   <td><p>AEM Forms支援Web服務標準，例如SOAP/HTTP。 服務可以公開為Web服務，而WSDL符合W3C所定義的Web服務標準。</p><p>可以從任何Web服務堆棧（包括。NET Framework和Sun™ Web Services SDK）調用服務。 (請參閱<a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services">使用Web Services叫用AEM Forms</a>。)</p></td>
  </tr>
  <tr>
   <td><p>REST請求</p></td>
   <td><p>AEM Forms支援REST請求。 您可以直接從HTML頁面呼叫服務。 (請參閱<a href="/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests">使用REST請求調用AEM Forms。)</a></p></td>
  </tr>
 </tbody>
</table>

下圖以視覺化方式呈現以程式設計方式叫用AEM Forms服務的不同方式。

>[!NOTE]
>
>除了使用AEM FormsSDK建立可叫用AEM Forms服務的用戶端應用程式外，您也可以建立可部署至服務容器的元件。 例如，您可以建立包含可用於流程的自訂資料類型的Bank元件。 也就是說，您可以建立資料類型，例如`com.adobe.idp.BankAccount`。 然後，您可以在客戶端應用程式中建立`com.adobe.idp.BankAccount`實例。

服務容器提供下列功能：

* 允許使用不同的方法調用AEM Forms服務。 您可以通過設定端點來配置服務，以便使用所有方法調用該服務：遠端、Java API、web services和REST。 （請參閱[以程式設計方式管理端點](/help/forms/developing/programmatically-endpoints.md#programmatically-managing-endpoints)）。
* 將消息轉換為稱為調用請求的標準化格式。 調用請求從客戶端應用程式（或其他服務）發送到位於服務容器中的服務。 調用請求包含諸如要調用的服務的名稱和執行該操作所需的資料值之類的資訊。 許多服務都需要檔案來執行操作。 因此，呼叫請求通常包含檔案，檔案可以是PDF資料、XDP資料、XML資料等。
* 將調用請求路由到適當的服務（要調用的服務的名稱是調用請求的一部分）。
* 執行任務，例如確定呼叫者是否具有調用指定服務操作的權限。 調用請求必須包含有效AEM的表單用戶名和口令。

   向服務發送調用請求有不同的方法。 此外，傳送所需輸入值至服務的方式也不同。 例如，假設您使用Java API來叫用需要PDF檔案的服務。 對應的Java方法包含接受PDF檔案的參數。 在這種情況下，參數的資料類型為`com.adobe.idp.Document`。 (請參閱[使用Java API](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)將資料傳遞至AEM Forms服務。)

   如果您使用監視資料夾調用服務，則在將檔案放置到已配置的監視資料夾中時，將發送調用請求。 如果您使用電子郵件叫用服務，則當電子郵件訊息送達已設定的收件匣時，會將呼叫請求傳送至服務。

   一旦執行操作，服務容器就發回調用響應。 調用響應包含操作結果等資訊。 例如，如果操作修改PDF文檔，則調用響應將包含修改的PDF文檔。 如果操作失敗，則調用響應包含錯誤消息。

   可以以發送調用請求的相同方式檢索調用響應。 也就是說，如果調用請求是使用Java API發送的，則可以使用Java API檢索調用響應。 例如，假設某個操作修改了PDF文檔。 您可以取得呼叫服務之Java方法的傳回值，以擷取已修改的PDF檔案。

   當調用長壽命進程時，調用響應包含與調用請求相關聯的標識符值。 使用此標識符值，您可以稍後檢查進程的狀態。 例如，請考慮MortgageLoan長期服務。 使用標識符值，可以檢查以確定流程是否成功完成。 （請參閱[叫用以人為中心的長壽命進程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)。）

   下圖顯示調用服務的客戶端應用程式（使用Java API）。

   當用戶端應用程式叫用服務時，會發生三個事件：

   1. 客戶端應用程式向服務發送調用請求。
   1. 服務執行調用請求中指定的操作。
   1. 服務容器返回對客戶端應用程式的調用響應。

**另請參閱**

[瞭解AEM Forms進程](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)

[使用(表單不建議使AEM用)AEM FormsRemoting調用](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[使用Java API叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[使用Web Services叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)

[調用以人為中心的長壽命進程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[使用REST請求調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests)
