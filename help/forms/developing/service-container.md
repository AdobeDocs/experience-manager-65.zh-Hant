---
title: 服務容器
description: 服務容器中的AEM Forms服務
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding, development-tools
role: Developer
exl-id: 6abf2401-5a87-4f72-9028-74580df5b9de
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---

# 服務容器 {#service-container}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

服務容器中的AEM Forms服務（包括標準服務，例如加密服務、長效和短效處理程式）可以使用各種提供者（例如EJB提供者）來叫用。 EJB提供者可透過RMI/IIOP叫用AEM Forms服務。 Web服務提供者使用SOAP/HTTP和SOAP/JMS等標準，將服務公開為Web服務（WSDL產生）。

下表說明以程式設計方式叫用AEM Forms服務的各種方式。

<table>
 <thead>
  <tr>
   <th><p>引動方法</p></th>
   <th><p>說明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>遠端整合</p></td>
   <td><p>遠端整合可讓Flex使用者端叫用服務作業。 (請參閱 <a href="/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting">使用(AEM表單已棄用) AEM Forms遠端功能叫用AEM Forms</a>.)</p></td>
  </tr>
  <tr>
   <td><p>Java API</p></td>
   <td><p>Java API可以叫用AEM Forms服務。 Java API會整理至使用者端程式庫和Java叫用API。 (請參閱 <a href="/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api">使用Java API叫用AEM Forms</a>.)</p></td>
  </tr>
  <tr>
   <td><p>網站服務</p></td>
   <td><p>AEM Forms支援SOAP/HTTP等Web服務標準。 服務可以公開為Web服務，WSDL遵循W3C定義的Web服務標準。</p><p>您可以從任何Web服務棧疊叫用服務，包括.NET Framework和Sun™ Web Services SDK。 (請參閱 <a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services">使用網站服務叫用AEM Forms</a>.)</p></td>
  </tr>
  <tr>
   <td><p>REST要求</p></td>
   <td><p>AEM Forms支援REST要求。 可以直接從HTML頁面叫用服務。 (請參閱 <a href="/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests">使用REST要求叫用AEM Forms</a>.)</p></td>
  </tr>
 </tbody>
</table>

下圖以視覺化方式呈現以程式設計方式叫用AEM Forms服務的不同方式。

>[!NOTE]
>
>除了使用AEM Forms SDK建立可以叫用AEM Forms服務的使用者端應用程式之外，您也可以建立可以部署至服務容器的元件。 例如，您可以建立包含可用於流程的自訂資料型別的Bank元件。 也就是說，您可以建立資料型別，例如 `com.adobe.idp.BankAccount`. 然後，您可以建立 `com.adobe.idp.BankAccount` 使用者端應用程式中的執行個體。

服務容器提供下列功能：

* 允許使用不同方法叫用AEM Forms服務。 您可以設定端點來設定服務，以便使用所有方法叫用服務：遠端、Java API、網站服務和REST。 (請參閱 [以程式管理端點](/help/forms/developing/programmatically-endpoints.md#programmatically-managing-endpoints).)
* 將訊息轉換為稱為呼叫要求的標準化格式。 從使用者端應用程式（或其他服務）傳送呼叫要求給服務容器中的服務。 叫用要求包含要叫用的服務名稱和執行作業所需的資料值等資訊。 許多服務都需要檔案才能執行作業。 因此，引動請求通常包含檔案，可以是PDF資料、XDP資料、XML資料等。
* 將呼叫要求路由到適當的服務（要呼叫的服務名稱是呼叫要求的一部分）。
* 執行工作，例如判斷呼叫者是否有許可權呼叫指定的服務作業。 叫用要求必須包含有效的AEM表單使用者名稱和密碼。

  有不同的方式可以將呼叫要求傳送至服務。 此外，也有不同的方式可將所需的輸入值傳送至服務。 例如，假設您使用Java API來叫用需要PDF檔案的服務。 對應的Java方法包含接受PDF檔案的引數。 在此情況下，引數的資料型別為 `com.adobe.idp.Document`. (請參閱 [使用Java API傳遞資料至AEM Forms服務](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api).)

  如果您使用watched資料夾叫用服務，則在您將檔案放在設定的watched資料夾中時，會傳送叫用要求。 如果您使用電子郵件叫用服務，當電子郵件訊息到達設定的收件匣時，就會傳送叫用要求給服務。

  執行作業後，服務容器會傳回呼叫回應。 引動回應包含作業結果等資訊。 例如，如果作業修改PDF檔案，則呼叫回應會包含修改過的PDF檔案。 如果操作不成功，則呼叫回應會包含錯誤訊息。

  叫用回應可以與叫用要求的傳送方式一樣擷取。 也就是說，如果呼叫要求是使用Java API傳送，則可以使用Java API擷取呼叫回應。 例如，假設作業會修改PDF檔案。 您可以取得叫用服務的Java方法的傳回值，以擷取修改過的PDF檔案。

  叫用長期處理程式時，叫用回應會包含與叫用要求關聯的識別碼值。 使用此識別碼值，您稍後可以檢查處理序的狀態。 例如，以MortgageLoan長期服務為例。 使用識別碼值，您可以檢查以判斷流程是否成功完成。 (請參閱 [叫用以人為中心的長期流程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).)

  下圖顯示叫用服務的使用者端應用程式（使用Java API）。

  當使用者端應用程式叫用服務時，會發生三個事件：

   1. 使用者端應用程式傳送呼叫要求給服務。
   1. 服務會執行呼叫要求中指定的作業。
   1. 服務容器會將呼叫回應傳回給使用者端應用程式。

**另請參閱**

[瞭解AEM Forms流程](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)

[使用(AEM表單已棄用) AEM Forms遠端功能叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[使用Java API叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[使用網站服務叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)

[叫用以人為中心的長期流程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[使用REST要求叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests)
