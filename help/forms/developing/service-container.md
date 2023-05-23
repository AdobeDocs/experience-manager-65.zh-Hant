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

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

位於服務容器中的AEM Forms服務（包括標準服務，如加密服務、長壽命和短壽命進程）可使用各種提供程式（如EJB提供程式）調用。 EJB提供程式允許通過RMI/IIOP調用AEM Forms服務。 Web服務提供程式使用SOAP/HTTP和SOAP/JMS等標準將服務作為Web服務（WSDL生成）公開。

下表介紹了以寫程式方式調用AEM Forms服務的不同方法。

<table>
 <thead>
  <tr>
   <th><p>調用方法</p></th>
   <th><p>說明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>遠程整合</p></td>
   <td><p>遠程整合使Flex客戶機能夠調用服務操作。 (請參閱 <a href="/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting">調用AEM Forms使用(不建議AEM用於表單)AEM Forms遠程處理</a>。)</p></td>
  </tr>
  <tr>
   <td><p>Java API</p></td>
   <td><p>Java API可以調用AEM Forms服務。 Java API被組織到客戶端庫和Java調用API中。 (請參閱 <a href="/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api">使用Java API調用AEM Forms</a>。)</p></td>
  </tr>
  <tr>
   <td><p>Web服務</p></td>
   <td><p>AEM Forms支援SOAP/HTTP等Web服務標準。 服務可以作為Web服務公開，WSDL符合W3C定義的Web服務標準。</p><p>可以從任何Web服務堆棧（包括.NET Framework和Sun™ Web服務SDK）調用服務。 (請參閱 <a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services">使用Web服務調用AEM Forms</a>。)</p></td>
  </tr>
  <tr>
   <td><p>REST請求</p></td>
   <td><p>AEM Forms支援REST請求。 可以直接從HTML頁調用服務。 (請參閱 <a href="/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests">使用REST請求調用AEM Forms</a>。)</p></td>
  </tr>
 </tbody>
</table>

下圖提供了以寫程式方式調用AEM Forms服務的不同方式的直觀表示。

>[!NOTE]
>
>除了使用AEM FormsSDK建立可調用AEM Forms服務的客戶端應用程式外，您還可以建立可部署到服務容器的元件。 例如，您可以建立包含可在流程中使用的自定義資料類型的Bank元件。 即，您可以建立資料類型，如 `com.adobe.idp.BankAccount`。 然後可以建立 `com.adobe.idp.BankAccount` 客戶端應用程式中的實例。

服務容器提供以下功能：

* 允許使用不同方法調用AEM Forms服務。 可以通過設定端點來配置服務，以便可以使用所有方法調用該服務：遠程處理、Java API、Web服務和REST。 (請參閱 [以寫程式方式管理端點](/help/forms/developing/programmatically-endpoints.md#programmatically-managing-endpoints)。)
* 將消息轉換為稱為調用請求的標準化格式。 從客戶端應用程式（或另一服務）向位於服務容器中的服務發送調用請求。 調用請求包含諸如要調用的服務的名稱和執行該操作所需的資料值之類的資訊。 許多服務都需要文檔才能執行操作。 因此，調用請求通常包含一個文檔，可以是PDF資料、XDP資料、XML資料等。
* 將調用請求路由到適當的服務（要調用的服務的名稱是調用請求的一部分）。
* 執行任務，如確定呼叫者是否有權調用指定的服務操作。 調用請求必須包含有效AEM的表單用戶名和密碼。

   向服務發送調用請求有不同的方法。 此外，還有不同的方法將所需輸入值發送到服務。 例如，假定您使用Java API調用需要PDF文檔的服務。 相應的Java方法包含接受PDF文檔的參數。 在這種情況下，參數的資料類型為 `com.adobe.idp.Document`。 (請參閱 [使用Java API將資料傳遞到AEM Forms服務](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)。)

   如果使用監視資料夾調用服務，則在將檔案放置在已配置的監視資料夾中時會發送調用請求。 如果您使用電子郵件調用服務，則當電子郵件到達配置的收件箱時，將向服務發送調用請求。

   一旦執行操作，服務容器就返回調用響應。 調用響應包含諸如操作結果之類的資訊。 例如，如果操作修改PDF文檔，則調用響應包含修改的PDF文檔。 如果操作未成功，則調用響應包含錯誤消息。

   可以以發送調用請求的相同方式檢索調用響應。 即，如果調用請求是使用Java API發送的，則可以使用Java API檢索調用響應。 例如，假定操作修改PDF文檔。 通過獲取調用該服務的Java方法的返回值，可以檢索修改的PDF文檔。

   當調用長壽命進程時，調用響應包含與調用請求相關聯的標識符值。 使用此標識符值，您可以稍後檢查進程的狀態。 例如，請考慮MortgageLoan的長期服務。 使用標識符值，可以檢查以確定該進程是否成功完成。 (請參閱 [調用以人為中心的長壽命進程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)。)

   下圖顯示了使用Java API調用服務的客戶端應用程式。

   當客戶端應用程式調用服務時，會發生三個事件：

   1. 客戶端應用程式向服務發送調用請求。
   1. 服務執行在調用請求中指定的操作。
   1. 服務容器返回對客戶端應用程式的調用響應。

**另請參閱**

[瞭解AEM Forms進程](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)

[調用AEM Forms使用(不建議AEM用於表單)AEM Forms遠程處理](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[使用Java API調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[使用Web服務調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)

[調用以人為中心的長壽命進程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[使用REST請求調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests)
