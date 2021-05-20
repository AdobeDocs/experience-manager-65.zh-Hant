---
title: 使用Remoting叫用AEM Forms
seo-title: 使用Remoting叫用AEM Forms
description: 使用「移除」來叫用AEM Forms程式，以叫用在Workbench中建立的程式。 您可以從使用Flex建置的用戶端應用程式叫用AEM Forms程式。
seo-description: 使用「移除」來叫用AEM Forms程式，以叫用在Workbench中建立的程式。 您可以從使用Flex建置的用戶端應用程式叫用AEM Forms程式。
uuid: 592d1519-c38b-4b33-8cf3-61e2bff81501
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 3d8bb2d3-b1f8-49e1-a529-b3e7a28da4bb
role: Developer
exl-id: 94a48776-f537-4b4e-8d71-51b08e463cba
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '4661'
ht-degree: 0%

---

# 使用Remoting {#invoking-aem-forms-using-remoting}叫用AEM Forms

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

在Workbench中建立的程式可透過使用遠端叫用。 也就是說，您可以從使用Flex建置的用戶端應用程式叫用AEM Forms程式。 此功能以資料服務為基礎。

>[!NOTE]
>
>使用Remoting時，建議您叫用在Workbench中建立的程式，而非AEM Forms服務。 但可以直接叫用AEM Forms服務。 (請參閱使用AEM Forms開發人員中心的遠端加密PDF檔案)。

>[!NOTE]
>
>如果AEM Forms服務未設定為允許匿名存取，來自Flex用戶端的請求會導致Web瀏覽器疑難排解。 用戶必須輸入用戶名和密碼憑據。

可使用Remoting調用以下名為`MyApplication/EncryptDocument`的AEM Forms短期進程。 （有關此進程的資訊，如其輸入值和輸出值，請參閱[短期進程示例](/help/forms/developing/aem-forms-processes.md)。）

![iu_iu_encryptdocumentprocess2](assets/iu_iu_encryptdocumentprocess2.png)

>[!NOTE]
>
>若要使用Flex應用程式叫用AEM Forms程式，請確定已啟用遠端端點。 預設情況下，部署進程時將啟用遠程端點。

叫用此程式時，會執行下列動作：

1. 獲取作為輸入值傳遞的不安全PDF文檔。 此操作基於`SetValue`操作。 輸入參數的名稱為`inDoc`，其資料類型為`document`。 （`document`資料類型是Workbench內的可用資料類型。）
1. 使用密碼加密PDF檔案。 此操作基於`PasswordEncryptPDF`操作。 此進程的輸出值的名稱為`outDoc` ，代表密碼加密的PDF文檔。 outDoc的資料類型為`document`。
1. 將密碼加密的PDF文檔另存為PDF檔案到本地檔案系統。 此操作基於`WriteDocument`操作。

>[!NOTE]
>
>`MyApplication/EncryptDocument`程式不以現有的AEM Forms程式為基礎。 若要遵循程式碼範例，請使用Workbench建立名為`MyApplication/EncryptDocument`的程式。

>[!NOTE]
>
>有關使用遠程調用長壽命進程的資訊，請參閱[調用以人為中心的長壽命進程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)。

**另請參閱**

[包含AEM Forms Flex程式庫檔案](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[使用(AEM表單已淘汰)AEM Forms Remoting處理檔案](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[使用(AEM表單已過時)AEM Forms Remoting傳遞不安全的檔案，以叫用短期處理程式](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[驗證使用Flex建置的用戶端應用程式](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[使用遠程功能傳遞安全文檔以調用進程](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

[使用遠程調用自定義元件服務](invoking-aem-forms-using-remoting.md#invoking-custom-component-services-using-remoting)

[建立使用Flex構建的客戶端應用程式，該應用程式調用以人為中心的長期流程](/help/forms/developing/invoking-human-centric-long-lived.md#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process)

[使用HTTP Token建立執行SSO驗證的Flash Builder應用程式](/help/forms/developing/creating-flash-builder-applications-perform.md#creating-flash-builder-applications-that-perform-sso-authentication-using-http-tokens)

如需如何在Flex圖表控制項中顯示處理資料的資訊，請參閱在Flex圖表](https://www.adobe.com/devnet/livecycle/articles/populating_flexcontrols.html)中顯示AEM Forms處理資料。[

>[!NOTE]
>
>*請務必將crossdomain.xml檔案放置在正確位置。例如，假設您在JBoss上部署了AEM Forms，請將此檔案放置在下列位置：&lt;install_directory>\Adobe_Experience_Manager_forms\jboss\server\lc_turnkey\deploy\jboss-web.deployer\ROOT.war*

## 包含AEM Forms Flex程式庫檔案{#including-the-aem-forms-flex-library-file}

若要使用Remoting以程式設計方式叫用AEM Forms程式，請將adobe-remoting-provider.swc檔案新增至您Flex專案的類別路徑。 此SWC檔案位於以下位置：

* *&lt;install_directory>\Adobe_Experience_Manager_forms\sdk\misc\DataServices\Client-Libraries*

   其中， &lt;*install_directory*>是安裝AEM Forms的目錄。

**另請參閱**

[使用叫用AEM Forms(AEM表單已淘汰)AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[使用(AEM表單已淘汰)AEM Forms Remoting處理檔案](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[使用(AEM表單已過時)AEM Forms Remoting傳遞不安全的檔案，以叫用短期處理程式](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[驗證使用Flex建置的用戶端應用程式](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

## 使用Remoting {#handling-documents-with-remoting}處理文檔

AEM Forms中使用的最重要的非原始Java類型之一是`com.adobe.idp.Document`類。 調用AEM Forms操作通常需要文檔。 它主要是PDF文檔，但可包含其他文檔類型，如SWF、HTML、XML或DOC檔案。 (請參閱[使用Java API](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)將資料傳遞至AEM Forms服務。)

以Flex建置的用戶端應用程式無法直接要求檔案。 例如，您無法啟動Adobe Reader來要求產生PDF檔案的URL。 對文檔類型（如PDF和Microsoft Word文檔）的請求將返回結果為URL。 用戶端有責任顯示URL的內容。 文檔管理服務有助於生成URL和內容類型資訊。 對XML文檔的請求將返回結果中的完整XML文檔。

### 將文檔作為輸入參數{#passing-a-document-as-an-input-parameter}傳遞

以Flex建置的用戶端應用程式無法將檔案直接傳遞至AEM Forms程式。 相反，客戶端應用程式使用`mx.rpc.livecycle.DocumentReference`ActionScript類的實例，將輸入參數傳遞到需要`com.adobe.idp.Document`實例的操作。 Flex用戶端應用程式有幾個設定`DocumentReference`物件的選項：

* 當文檔位於伺服器上且其檔案位置已知時，將DocumentReference對象的referenceType屬性設定為REF_TYPE_FILE。 將fileRef屬性設定為檔案的位置，如下例所示：

```java
 ... var docRef: DocumentReference = new DocumentReference(); 
 docRef.referenceType = DocumentReference.REF_TYPE_FILE; 
 docRef.fileRef = "C:/install/adobe/cs2/How to Uninstall.pdf"; ...
```

* 當文檔位於伺服器上且您知道其URL時，請將DocumentReference對象的referenceType屬性設定為REF_TYPE_URL。 將url屬性設為URL，如下列範例所示：

```java
... var docRef: DocumentReference = new DocumentReference(); 
docRef.referenceType = DocumentReference.REF_TYPE_URL; 
docRef.url = "https://companyserver:8080/DocumentManager/116/7855"; ...
```

* 要從客戶端應用程式中的文本字串建立DocumentReference對象，請將DocumentReference對象的referenceType屬性設定為REF_TYPE_INLINE。 將text屬性設定為要包含在物件中的文字，如下列範例所示：

```java
... var docRef: DocumentReference = new DocumentReference(); 
docRef.referenceType = DocumentReference.REF_TYPE_INLINE; 
docRef.text = "Text for my document";  // Optionally, you can override the server’s default character set  // if necessary:  // docRef.charsetName=CharacterSetName  ...
```

* 當檔案不在伺服器上時，請使用「遠端上傳servlet」將檔案上傳至AEM Forms。 AEM Forms的新功能是上傳安全檔案。 上傳安全文檔時，必須使用&#x200B;*文檔上載應用程式用戶*&#x200B;角色的用戶。 沒有此角色，用戶無法上載安全文檔。 建議您使用單一登入來上傳安全檔案。 （請參閱[使用Remoting](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)傳遞安全文檔以調用進程。）

>[!NOTE]
如果將AEM Forms設定為允許上載不安全的文檔，則可以使用沒有「文檔上載應用程式用戶」角色的用戶來上載文檔。 用戶也可以具有「文檔上載」權限。 不過，如果將AEM Forms設定為僅允許安全文檔，請確保用戶具有「文檔上載應用程式用戶」角色或「文檔上載」權限。 (請參閱[將AEM Forms設定為接受安全和不安全的檔案](invoking-aem-forms-using-remoting.md#configuring-aem-forms-to-accept-secure-and-unsecure-documents)。

您對指定的上傳URL使用標準Flash上傳功能：`https://SERVER:PORT/remoting/lcfileupload`。 然後，只要`Document`類型的輸入參數為預期值，就可以使用`DocumentReference`對象
` private function startUpload():void  {  fileRef.addEventListener(Event.SELECT, selectHandler);  fileRef.addEventListener("uploadCompleteData", completeHandler);  try  {   var success:Boolean = fileRef.browse();  }    catch (error:Error)  {   trace("Unable to browse for files.");  }  }      private function selectHandler(event:Event):void {  var request:URLRequest = new  URLRequest("https://SERVER:PORT/remoting/lcfileupload")  try   {   fileRef.upload(request);   }    catch (error:Error)   {   trace("Unable to upload file.");   }  }    private function completeHandler(event:DataEvent):void  {   var params:Object = new Object();   var docRef:DocumentReference = new DocumentReference();   docRef.url = event.data as String;   docRef.referenceType = DocumentReference.REF_TYPE_URL;  }`遠程快速入門使用遠程上載servlet將PDF檔案傳遞到`MyApplication/EncryptDocument`進程。 (請參閱[使用(AEM表單已過時)AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)傳遞不安全的檔案，以叫用短期處理程式。)

```java
 
private
function startUpload(): void  { 
 fileRef.addEventListener(Event.SELECT, selectHandler); 
 fileRef.addEventListener("uploadCompleteData", completeHandler); 
 try  { 
  var success: Boolean = fileRef.browse(); 
 }  
 catch (error: Error)  { 
  trace("Unable to browse for files."); 
 } 
}   
private
function selectHandler(event: Event): void { 
 var request: URLRequest = new  URLRequest("https://SERVER:PORT/remoting/lcfileupload")  try  { 
  fileRef.upload(request); 
 }  
 catch (error: Error)  { 
  trace("Unable to upload file."); 
 } 
}  
private
function completeHandler(event: DataEvent): void  { 
 var params: Object = new Object(); 
 var docRef: DocumentReference = new DocumentReference(); 
 docRef.url = event.data as String; 
 docRef.referenceType = DocumentReference.REF_TYPE_URL; 
}
```

「遠程快速入門」使用「遠程上傳servlet」將PDF檔案傳遞到`MyApplication/EncryptDocument`進程。 (請參閱[使用(AEM表單已過時)AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)傳遞不安全的檔案，以叫用短期處理程式。)

### 將文檔傳回客戶端應用程式{#passing-a-document-back-to-a-client-application}

客戶端應用程式接收類型為`mx.rpc.livecycle.DocumentReference`的對象，用於返回`com.adobe.idp.Document`實例作為輸出參數的服務操作。 由於客戶端應用程式處理的是ActionScript對象而非Java，因此您無法將基於Java的文檔對象傳回到Flex客戶端。 伺服器會為檔案產生URL，並將URL傳回用戶端。 `DocumentReference`對象的`referenceType`屬性指定內容是位於`DocumentReference`對象中，還是必須從`DocumentReference.url`屬性中的URL中檢索。 `DocumentReference.contentType`屬性指定文檔的類型。

**另請參閱**

[使用叫用AEM Forms(AEM表單已淘汰)AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[包含AEM Forms Flex程式庫檔案](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[使用(AEM表單已過時)AEM Forms Remoting傳遞不安全的檔案，以叫用短期處理程式](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[驗證使用Flex建置的用戶端應用程式](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[使用遠程功能傳遞安全文檔以調用進程](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

## 通過使用Remoting {#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting}傳遞不安全文檔來調用短期進程

若要從使用Flex建置的應用程式叫用AEM Forms程式，請執行下列工作：

1. 建立`mx:RemoteObject`實例。
1. 建立`ChannelSet`實例。
1. 傳遞所需的輸入值。
1. 處理傳回值。

>[!NOTE]
本節探討當AEM Forms設定為上傳不安全的檔案時，如何叫用AEM Forms程式和上傳檔案。 有關如何調用AEM Forms進程和上傳安全文檔以及如何配置AEM Forms以接受安全和不安全文檔的資訊，請參閱[使用Remoting](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)傳遞安全文檔以調用進程。

**建立mx:RemoteObject實例**

您可以建立`mx:RemoteObject`例項，以叫用在Workbench中建立的AEM Forms程式。 若要建立`mx:RemoteObject`例項，請指定以下值：

* **id:** 代表要叫 `mx:RemoteObject` 用的程式的例項名稱。
* **目的地：** 要叫用的AEM Forms程式名稱。例如，要調用`MyApplication/EncryptDocument`進程，請指定`MyApplication/EncryptDocument`。
* **結果：** 處理結果的Flex方法的名稱。

在`mx:RemoteObject`標籤中，指定`<mx:method>`標籤，該標籤指定進程調用方法的名稱。 通常，Forms調用方法的名稱為`invoke`。

以下代碼示例建立調用`MyApplication/EncryptDocument`進程的`mx:RemoteObject`實例。

```java
 <mx:RemoteObject id="EncryptDocument" destination="MyApplication/EncryptDocument" result="resultHandler(event);">
          <mx:method name="invoke" result="handleExecuteInvoke(event)"/>
      </mx:RemoteObject>
```

**建立通道至AEM Forms**

用戶端應用程式可在MXML或ActionScript中指定通道以叫用AEM Forms，如下列ActionScript範例所示。 通道必須是`AMFChannel`、`SecureAMFChannel`、`HTTPChannel`或`SecureHTTPChannel`。

```java
     ...
     private function refresh():void{
         var cs:ChannelSet= new ChannelSet();
         cs.addChannel(new AMFChannel("my-amf",
             "https://yourlcserver:8080/remoting/messagebroker/amf"));
         EncryptDocument.setCredentials("administrator", "password");
         EncryptDocument.channelSet = cs;
     }
     ...
```

將`ChannelSet`例項指派給`mx:RemoteObject`例項的`channelSet`欄位（如上一個程式碼範例所示）。 通常，在調用`ChannelSet.addChannel`方法時，您會在導入語句中導入通道類，而不是指定完全限定的名稱。

**傳遞輸入值**

在Workbench中建立的程式可取用零個或多個輸入參數，並傳回輸出值。 客戶端應用程式在`ActionScript`對象內傳遞輸入參數，其欄位與屬於AEM Forms進程的參數相對應。 名為`MyApplication/EncryptDocument`的短期進程需要一個名為`inDoc`的輸入參數。 進程公開的操作名稱為`invoke`（短期進程的預設名稱）。 (請參閱[使用叫用AEM Forms(AEM表單已淘汰)AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)。)

以下代碼示例將PDF文檔傳遞至`MyApplication/EncryptDocument`進程：

```java
     ...
     var params:Object = new Object();
 
     //Document is an instance of DocumentReference
     //that store an unsecured PDF document
     params["inDoc"] = pdfDocument;
 
     // Invoke an operation synchronously:
     EncryptDocument.invoke(params);
     ...
```

在此程式碼範例中，`pdfDocument`是包含不安全PDF檔案的`DocumentReference`例項。 有關`DocumentReference`的資訊，請參閱[使用(AEM表單已過時)AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)處理文檔。

**叫用服務的特定版本**

您可以在呼叫的參數映射中使用`_version`參數來叫用特定版本的Forms服務。 例如，要調用`MyApplication/EncryptDocument`服務的1.2版：

```java
 var params:Object = new Object();
 params["inDoc"] = pdfDocument;
 params["_version"] = "1.2"
 var token:AsyncToken = echoService.echoString(params);
```

`version`參數必須是包含單一句號的字串。 句點的左、主、右、次版本的值必須是整數。 如果未指定此參數，則調用頭活動版本。

**處理傳回值**

AEM Forms進程輸出參數被反序列化為ActionScript對象，客戶機應用程式從這些對象中按名稱提取特定參數，如以下示例所示。 （`MyApplication/EncryptDocument`進程的輸出值名為`outDoc`。）

```java
     ...
     var res:Object = event.result;
     var docRef:DocumentReference = res["outDoc"] as DocumentReference;
     ...
```

**調用MyApplication/EncryptDocument進程**

您可以執行下列步驟來叫用`MyApplication/EncryptDocument`程式：

1. 透過ActionScript或MXML建立`mx:RemoteObject`例項。 請參閱建立mx:RemoteObject實例。
1. 設定`ChannelSet`例項以與AEM Forms通訊，並將其與`mx:RemoteObject`例項建立關聯。 請參閱建立管道至AEM Forms。
1. 調用ChannelSet的`login`方法或服務的`setCredentials`方法以指定用戶標識符值和口令。 （請參閱[使用單一登入](invoking-aem-forms-using-remoting.md#using-single-sign-on)。）
1. 將不安全的PDF檔案填入`mx.rpc.livecycle.DocumentReference`執行個體，以傳遞至`MyApplication/EncryptDocument`程式。 （請參閱[將文檔作為輸入參數傳遞](invoking-aem-forms-using-remoting.md#passing-a-document-as-an-input-parameter)。）
1. 呼叫`mx:RemoteObject`執行個體的`invoke`方法，以加密PDF檔案。 傳遞包含輸入參數（不安全的PDF檔案）的`Object`。 請參閱傳遞輸入值。
1. 擷取從程式傳回的密碼加密PDF檔案。 請參閱處理傳回值。

[快速入門：使用(AEM表單已過時)AEM Forms Remoting傳遞不安全的檔案，以叫用短期處理程式](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-by-passing-an-unsecure-document-using-deprecated-for-aem-forms-aem-forms-remoting)

## 驗證使用Flex {#authenticating-client-applications-built-with-flex}建立的客戶端應用程式

AEM Forms使用者管理員可透過數種方式驗證來自Flex應用程式的遠端請求，包括透過中央登入服務、基本驗證和自訂驗證執行AEM Forms單一登入。 當未啟用單一登入或匿名存取時，Remoting請求會導致基本驗證（預設值）或自訂驗證。

基本驗證依賴於來自Web應用程式容器的標準J2EE基本驗證。 對於基本驗證，HTTP 401錯誤會造成瀏覽器疑難問題。 這表示當您嘗試使用RemoteObject連線至Forms應用程式，但尚未從Flex應用程式登入時，瀏覽器會提示您輸入使用者名稱和密碼。

對於自定義身份驗證，伺服器向客戶端發送一個錯誤，以指示需要身份驗證。

>[!NOTE]
有關使用HTTP令牌執行身份驗證的資訊，請參閱[建立使用HTTP令牌執行SSO身份驗證的Flash Builder應用程式](/help/forms/developing/creating-flash-builder-applications-perform.md#creating-flash-builder-applications-that-perform-sso-authentication-using-http-tokens)。

### 使用自定義身份驗證{#using-custom-authentication}

通過在遠程端點上將身份驗證方法從「基本」更改為「自定義」，可在管理控制台中啟用自定義身份驗證。 如果使用自定義身份驗證，則您的客戶端應用程式將調用`ChannelSet.login`方法以登錄，調用`ChannelSet.logout`方法以註銷。

>[!NOTE]
在舊版AEM Forms中，您會呼叫`RemoteObject.setCredentials`方法，將憑證傳送至目的地。 在元件首次嘗試連接到伺服器之前，`setCredentials`方法實際上並未將憑據傳遞到伺服器。 因此，如果元件發出了故障事件，則無法確定是由於身份驗證錯誤還是其他原因而發生故障。 當您呼叫`ChannelSet.login`方法時，會連線至伺服器，以便您能立即處理驗證問題。 雖然您可以繼續使用`setCredentials`方法，但建議您使用`ChannelSet.login`方法。

由於多個目的地可以使用相同的通道和相應的ChannelSet對象，因此登錄到一個目的地會將用戶登錄到使用相同通道或通道的任何其他目的地。 如果兩個元件將不同的憑據應用於同一ChannelSet對象，則使用最後應用的憑據。 如果多個元件使用相同的已驗證ChannelSet對象，則調用`logout`方法會將所有元件記錄出目標。

以下示例將`ChannelSet.login`和`ChannelSet.logout`方法與RemoteObject控制項一起使用。 此應用程式會執行下列動作：

* 在`creationComplete`處理程式中建立`ChannelSet`對象，該對象表示`RemoteObject`元件使用的通道
* 響應按鈕點擊事件，呼叫`ROLogin`函式，將憑證傳遞至伺服器
* 使用RemoteObject元件將字串發送到伺服器以響應按鈕點擊事件。 伺服器將相同的字串返回到RemoteObject元件
* 使用RemoteObject元件的結果事件在TextArea控制項中顯示字串
* 響應按鈕點擊事件，呼叫`ROLogout`函式以註銷伺服器

```java
 <?xml version=”1.0”?>
 <!-- security/SecurityConstraintCustom.mxml -->
 <mx:Application xmlns:mx=”https://www.adobe.com/2006/mxml” width=”100%”
     height=”100%” creationComplete=”creationCompleteHandler();”>
 
     <mx:Script>
         <![CDATA[
             import mx.controls.Alert;
             import mx.messaging.config.ServerConfig;
             import mx.rpc.AsyncToken;
             import mx.rpc.AsyncResponder;
             import mx.rpc.events.FaultEvent;
             import mx.rpc.events.ResultEvent;
             import mx.messaging.ChannelSet;
 
             // Define a ChannelSet object.
             public var cs:ChannelSet;
 
             // Define an AsyncToken object.
             public var token:AsyncToken;
 
             // Initialize ChannelSet object based on the
             // destination of the RemoteObject component.
             private function creationCompleteHandler():void {
                 if (cs == null)
                 cs = ServerConfig.getChannelSet(remoteObject.destination);
             }
 
             // Login and handle authentication success or failure.
             private function ROLogin():void {
                 // Make sure that the user is not already logged in.
                 if (cs.authenticated == false) {
                     token = cs.login(“sampleuser”, “samplepassword”);
                     // Add result and fault handlers.
                     token.addResponder(new AsyncResponder(LoginResultEvent,
                     LoginFaultEvent));
                 }
             }
 
             // Handle successful login.
             private function LoginResultEvent(event:ResultEvent,
                 token:Object=null):void  {
                     switch(event.result) {
                         case “success”:
                             authenticatedCB.selected = true;
                             break;
                             default:
                     }
                 }
 
                 // Handle login failure.
                 private function LoginFaultEvent(event:FaultEvent,
                     token:Object=null):void {
                         switch(event.fault.faultCode) {
                             case “Client.Authentication”:
                                 default:
                                 authenticatedCB.selected = false;
                                 Alert.show(“Login failure: “ + event.fault.faultString);
                     }
                 }
 
                 // Logout and handle success or failure.
                 private function ROLogout():void {
                     // Add result and fault handlers.
                     token = cs.logout();
                     token.addResponder(new
                         AsyncResponder(LogoutResultEvent,LogoutFaultEvent));
                 }
 
                 // Handle successful logout.
                 private function LogoutResultEvent(event:ResultEvent,
                     token:Object=null):void {
                         switch (event.result) {
                             case “success”:
                                 authenticatedCB.selected = false;
                                 break;
                                 default:
                     }
                 }
 
                 // Handle logout failure.
                 private function LogoutFaultEvent(event:FaultEvent,
                     token:Object=null):void {
                         Alert.show(“Logout failure: “ + event.fault.faultString);
                 }
                 // Handle message recevied by RemoteObject component.
                 private function resultHandler(event:ResultEvent):void {
                     ta.text += “Server responded: “+ event.result + “\n”;
                 }
 
                 // Handle fault from RemoteObject component.
                 private function faultHandler(event:FaultEvent):void {
                     ta.text += “Received fault: “ + event.fault + “\n”;
                 }
             ]]>
     </mx:Script>
     <mx:HBox>
         <mx:Label text=”Enter a text for the server to echo”/>
         <mx:TextInput id=”ti” text=”Hello World!”/>
         <mx:Button label=”Login”
             click=”ROLogin();”/>
         <mx:Button label=”Echo”
             enabled=”{authenticatedCB.selected}”
             click=”remoteObject.echo(ti.text);”/>
         <mx:Button label=”Logout”
             click=”ROLogout();”/>
         <mx:CheckBox id=”authenticatedCB”
             label=”Authenticated?”
             enabled=”false”/>
     </mx:HBox>
     <mx:TextArea id=”ta” width=”100%” height=”100%”/>
 
     <mx:RemoteObject id=”remoteObject”
         destination=”myDest”
         result=”resultHandler(event);”
         fault=”faultHandler(event);”/>
 </mx:Application>
```

`login`和`logout`方法會傳回AsyncToken物件。 將事件處理常式指派給AsyncToken物件，讓結果事件處理成功的呼叫，並讓錯誤事件處理失敗。

### 使用單一登入{#using-single-sign-on}

AEM forms使用者可以連線至多個AEM Forms網頁應用程式來執行工作。 當使用者從一個Web應用程式移至另一個應用程式時，要求他們個別登入每個Web應用程式並不有效。 AEM Forms單一登入機制可讓使用者登入一次，然後存取任何AEM Forms Web應用程式。 由於AEM Forms開發人員可建立用於AEM Forms的用戶端應用程式，因此他們也必須能夠運用單一登入機制。

每個AEM Forms Web應用程式都會封裝在其自己的Web Archive(WAR)檔案中，然後封裝為Enterprise Archive(EAR)檔案的一部分。 由於應用程式伺服器不允許在不同的Web應用程式間共用工作階段資料，AEM Forms會使用HTTP Cookie來儲存驗證資訊。 驗證Cookie可讓使用者登入Forms應用程式，然後連線至其他AEM Forms網頁應用程式。 此技術稱為單一登入。

AEM Forms開發人員撰寫用戶端應用程式以擴充「表單指南」的功能（已淘汰）及自訂工作區。 例如，工作區應用程式可以啟動程式。 然後，用戶端應用程式會使用遠端端點來從Forms服務中擷取資料。

使用(AEM表單已淘汰)AEM Forms Remoting叫用AEM Forms服務時，用戶端應用程式會隨著請求傳遞驗證Cookie。 由於使用者已通過驗證，因此從用戶端應用程式連線至AEM Forms服務不需要額外登入。

>[!NOTE]
如果Cookie無效或遺失，登入頁面就不會有隱式重新導向。 因此，您仍可以呼叫匿名服務。

您可以撰寫自行登入和登出的用戶端應用程式，以略過AEM Forms單一登入機制。 如果您略過單一登入機制，便可對您的應用程式使用基本或自訂驗證。

由於此機制未使用AEM Forms單一登入機制，因此不會將驗證Cookie寫入用戶端。 登錄憑據儲存在遠程通道的`ChannelSet`對象中。 因此，您對相同`ChannelSet`發出的任何`RemoteObject`呼叫，都會在這些憑證的內容中進行。

### 在AEM Forms中設定單一登入{#setting-up-single-sign-on-in-aem-forms}

若要在AEM Forms中使用單一登入，請安裝表單工作流程元件（包括集中登入服務）。 使用者成功登入後，集中式登入服務會傳回驗證Cookie給使用者。 後續對Forms Web應用程式提出的每個請求都包含Cookie。 如果Cookie有效，系統會將使用者視為已驗證，不需要再次登入。

### 編寫使用單一登錄{#writing-a-client-application-that-uses-single-sign-on}的客戶端應用程式

當您利用單一登入機制時，您會希望使用者在啟動用戶端應用程式之前，使用集中式登入服務登入。 也就是說，客戶端應用程式不會通過瀏覽器登錄，也不會通過調用`ChannelSet.login`方法登錄。

如果您使用AEM Forms單一登入機制，請將「遠端」端點設定為使用自訂驗證，而非基本驗證。 否則，使用基本驗證時，驗證錯誤會造成瀏覽器挑戰，您不希望使用者看到。 反之，您的應用程式會偵測驗證錯誤，然後顯示訊息，指示使用者使用集中登入服務登入。

客戶端應用程式使用`RemoteObject`元件通過遠程端點訪問AEM Forms，如以下示例所示。

```java
 <?xml version="1.0"?>
 <mx:Application
        backgroundColor="#FFFFFF">
 
       <mx:Script>
          <![CDATA[
 
            import mx.controls.Alert;
            import mx.rpc.events.FaultEvent;
 
            // Prompt user to login on a fault.
            private function faultHandler(event:FaultEvent):void
            {
             if(event.fault.faultCode=="Client.Authentication")
             {
                 Alert.show(
                     event.fault.faultString + "\n" +
                     event.fault.faultCode + "\n" +
                     "Please login to continue.");
             }
         }
          ]]>
       </mx:Script>
 
       <mx:RemoteObject id="srv"
           destination="product"
           fault="faultHandler(event);"/>
 
       <mx:DataGrid
           width="100%" height="100%"
           dataProvider="{srv.getProducts.lastResult}"/>
 
       <mx:Button label="Get Data"
           click="srv.getProducts();"/>
 
 </mx:Application>
```

**在Flex應用程式仍在執行時以新使用者身分登入**

以Flex建置的應用程式包含驗證Cookie，且包含對AEM Forms服務的每個要求。 基於效能原因，AEM Forms不會在每個請求上驗證Cookie。 不過，AEM Forms會偵測何時將驗證Cookie取代為其他驗證Cookie。

例如，您啟動了客戶端應用程式，當應用程式處於活動狀態時，您可以使用集中式登錄服務來註銷。 接下來，您可以以其他使用者的身分登入。 以其他使用者身分登入，會將現有的驗證Cookie以新使用者的驗證Cookie取代。

在來自用戶端應用程式的下一個要求時，AEM Forms會偵測Cookie已變更，並將使用者登出。 因此，Cookie變更後的第一個要求會失敗。 所有後續請求都會在新Cookie的內容中提出，且會成功。

**登出**

若要登出AEM Forms並使工作階段無效，必須從用戶端的電腦刪除驗證Cookie。 由於單一登入的目的是讓使用者只登入一次，因此您不希望用戶端應用程式刪除Cookie。 此動作會有效登出使用者。

因此，調用客戶端應用程式中的`RemoteObject.logout`方法會在客戶端上生成一條錯誤消息，指定會話未註銷。 使用者可改為使用集中登入服務來登出及刪除驗證Cookie。

**在Flex應用程式仍在執行時登出**

您可以啟動以Flex建置的用戶端應用程式，並使用集中登入服務來登出。 在登出程式中，會刪除驗證Cookie。 如果提出的遠端請求沒有Cookie或Cookie無效，則使用者工作階段會失效。 此動作實際上是登出。 下次客戶端應用程式嘗試連接到AEM Forms服務時，將請求用戶登錄。

**另請參閱**

[使用叫用AEM Forms(AEM表單已淘汰)AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[使用(AEM表單已淘汰)AEM Forms Remoting處理檔案](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[包含AEM Forms Flex程式庫檔案](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[使用(AEM表單已過時)AEM Forms Remoting傳遞不安全的檔案，以叫用短期處理程式](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[使用遠程功能傳遞安全文檔以調用進程](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

## 使用Remoting {#passing-secure-documents-to-invoke-processes-using-remoting}傳遞安全文檔以調用進程

叫用需要一或多個檔案的程式時，您可以將安全檔案傳遞至AEM Forms。 通過傳遞安全文檔，您可以保護業務資訊和機密文檔。 在這種情況下，文檔可以指PDF文檔、XML文檔、Word文檔等。 將AEM Forms設為允許安全檔案時，必須將安全檔案從寫入Flex的用戶端應用程式傳遞至AEM Forms。 (請參閱[將AEM Forms設定為接受安全和不安全的檔案](invoking-aem-forms-using-remoting.md#configuring-aem-forms-to-accept-secure-and-unsecure-documents)。)

傳遞安全檔案時，請使用單一登入，並指定具有&#x200B;*檔案上傳應用程式使用者*&#x200B;角色的AEM表單使用者。 沒有此角色，用戶無法上載安全文檔。 您可以以程式設計方式將角色指派給使用者。 （請參閱[管理角色和權限](/help/forms/developing/users.md#managing-roles-and-permissions)。）

>[!NOTE]
建立新角色並希望該角色的成員上載安全文檔時，請確保指定「文檔上載」權限。

AEM Forms支援名為`getFileUploadToken`的操作，該操作會傳回傳遞至上傳servlet的Token。 `DocumentReference.constructRequestForUpload`方法需要連同`LC.FileUploadAuthenticator.getFileUploadToken`方法傳回的代號的URL來存取AEM Forms。 此方法會傳回`URLRequest`物件，用於呼叫上傳servlet。 下列程式碼會示範此應用程式邏輯。

```java
     ...
         private function startUpload():void
         {
             fileRef.addEventListener(Event.SELECT, selectHandler);
             fileRef.addEventListener("uploadCompleteData", completeHandler);
             try
             {
         var success:Boolean = fileRef.browse();
             }
             catch (error:Error)
             {
                 trace("Unable to browse for files.");
             }
 
         }
 
          private function selectHandler(event:Event):void
             {
             var authTokenService:RemoteObject = new RemoteObject("LC.FileUploadAuthenticator");
             authTokenService.addEventListener("result", authTokenReceived);
             authTokenService.channelSet = cs;
             authTokenService.getFileUploadToken();
             }
 
         private function authTokenReceived(event:ResultEvent):void
             {
             var token:String = event.result as String;
             var request:URLRequest = DocumentReference.constructRequestForUpload("http://localhost:8080", token);
 
             try
             {
           fileRef.upload(request);
             }
             catch (error:Error)
             {
             trace("Unable to upload file.");
             }
             }
 
         private function completeHandler(event:DataEvent):void
         {
 
             var params:Object = new Object();
             var docRef:DocumentReference = new DocumentReference();
             docRef.url = event.data as String;
             docRef.referenceType = DocumentReference.REF_TYPE_URL;
         }
         ...
```

)

### 將AEM Forms設定為接受安全和不安全的檔案{#configuring-aem-forms-to-accept-secure-and-unsecure-documents}

您可以使用管理控制台來指定將檔案從Flex用戶端應用程式傳遞至AEM Forms程式時，檔案是否安全。 依預設，AEM Forms會設定為接受安全檔案。 您可以執行下列步驟，將AEM Forms設定為接受安全檔案：

1. 登入管理控制台。
1. 按一下「**設定**」。
1. 按一下「**核心繫統設定」。**
1. 按一下「設定」。
1. 確保未選取「允許從Flex應用程式上傳非安全檔案」選項。

>[!NOTE]
若要設定AEM Forms以接受不安全的檔案，請選取「允許從Flex應用程式上傳非安全的檔案」選項。 然後重新啟動應用程式或服務，以確保設定生效。

### 快速入門：使用Remoting {#quick-start-invoking-a-short-lived-process-by-passing-a-secure-document-using-remoting}傳遞安全文檔以調用短期進程

以下代碼示例調用`MyApplication/EncryptDocument.`用戶必須登錄才能按一下「選擇檔案」按鈕，該按鈕用於上載PDF檔案並調用該進程。 也就是說，一旦用戶通過驗證，就會啟用「選擇檔案」按鈕。 下圖顯示使用者通過驗證後的Flex用戶端應用程式。 請注意已驗證核取方塊已啟用。

![iu_iu_secureremotelogin](assets/iu_iu_secureremotelogin.png)

如果AEM Forms設定為僅允許上傳安全檔案，且使用者沒有&#x200B;*檔案上傳應用程式使用者*&#x200B;角色，則會擲回例外狀況。 如果使用者擁有此角色，則會上傳檔案並叫用程式。

```java
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Application  xmlns="*"
      creationComplete="initializeChannelSet();">
        <mx:Script>
        <![CDATA[
      import mx.rpc.livecycle.DocumentReference;
      import flash.net.FileReference;
      import flash.net.URLRequest;
      import flash.events.Event;
      import flash.events.DataEvent;
      import mx.messaging.ChannelSet;
      import mx.messaging.channels.AMFChannel;
      import mx.rpc.events.ResultEvent;
      import mx.collections.ArrayCollection;
      import mx.rpc.AsyncToken;
      import mx.controls.Alert;
      import mx.rpc.events.FaultEvent;
      import mx.rpc.AsyncResponder;
 
      // Classes used in file retrieval
      private var fileRef:FileReference = new FileReference();
      private var docRef:DocumentReference = new DocumentReference();
      private var parentResourcePath:String = "/";
      private var now1:Date;
      private var serverPort:String = "hiro-xp:8080";
 
      // Define a ChannelSet object.
      public var cs:ChannelSet;
 
      // Define an AsyncToken object.
      public var token:AsyncToken;
 
       // Holds information returned from AEM Forms
      [Bindable]
      public var progressList:ArrayCollection = new ArrayCollection();
 
 
      // Handles a successful login
     private function LoginResultEvent(event:ResultEvent,
         token:Object=null):void  {
             switch(event.result) {
                 case "success":
                     authenticatedCB.selected = true;
                     btnFile.enabled = true;
                     btnLogout.enabled = true;
                     btnLogin.enabled = false;
                         break;
                     default:
                 }
             }
 
 
 // Handle login failure.
 private function LoginFaultEvent(event:FaultEvent,
     token:Object=null):void {
     switch(event.fault.faultCode) {
                 case "Client.Authentication":
                         default:
                         authenticatedCB.selected = false;
                         Alert.show("Login failure: " + event.fault.faultString);
                 }
             }
 
 
      // Set up channel set to invoke AEM Forms
      private function initializeChannelSet():void {
        cs = new ChannelSet();
        cs.addChannel(new AMFChannel("remoting-amf", "https://" + serverPort + "/remoting/messagebroker/amf"));
        EncryptDocument2.channelSet = cs;
      }
 
     // Call this method to upload the file.
      // This creates a file picker and lets the user select a PDF file to pass to the EncryptDocument process.
      private function uploadFile():void {
        fileRef.addEventListener(Event.SELECT, selectHandler);
        fileRef.addEventListener(DataEvent.UPLOAD_COMPLETE_DATA,completeHandler);
        fileRef.browse();
      }
 
      // Gets called for selected file. Does the actual upload via the file upload servlet.
      private function selectHandler(event:Event):void {
              var authTokenService:RemoteObject = new RemoteObject("LC.FileUploadAuthenticator");
         authTokenService.addEventListener("result", authTokenReceived);
         authTokenService.channelSet = cs;
         authTokenService.getFileUploadToken();
      }
 
     private function authTokenReceived(event:ResultEvent):void
     {
     var token:String = event.result as String;
     var request:URLRequest = DocumentReference.constructRequestForUpload("https://hiro-xp:8080", token);
 
     try
     {
           fileRef.upload(request);
     }
     catch (error:Error)
     {
         trace("Unable to upload file.");
     }
 }
 
      // Called once the file is completely uploaded.
      private function completeHandler(event:DataEvent):void {
 
        // Set the docRef’s url and referenceType parameters
        docRef.url = event.data as String;
        docRef.referenceType=DocumentReference.REF_TYPE_URL;
        executeInvokeProcess();
      }
 
     //This method invokes the EncryptDocument process
      public function executeInvokeProcess():void {
         //Create an Object to store the input value for the EncryptDocument process
           now1 = new Date();
 
         var params:Object = new Object();
         params["inDoc"]=docRef;
 
         // Invoke the EncryptDocument process
         var token:AsyncToken;
         token = EncryptDocument2.invoke(params);
         token.name = name;
      }
 
      // AEM Forms  login method
      private function ROLogin():void {
         // Make sure that the user is not already logged in.
 
         //Get the User and Password
         var userName:String = txtUser.text;
         var pass:String = txtPassword.text;
 
        if (cs.authenticated == false) {
             token = cs.login(userName, pass);
 
         // Add result and fault handlers.
         token.addResponder(new AsyncResponder(LoginResultEvent,    LoginFaultEvent));
                 }
             }
 
      // This method handles a successful process invocation
      public function handleResult(event:ResultEvent):void
      {
            //Retrieve information returned from the service invocation
          var token:AsyncToken = event.token;
          var res:Object = event.result;
          var dr:DocumentReference = res["outDoc"] as DocumentReference;
          var now2:Date = new Date();
 
           // These fields map to columns in the DataGrid
          var progObject:Object = new Object();
          progObject.filename = token.name;
          progObject.timing = (now2.time - now1.time).toString();
          progObject.state = "Success";
          progObject.link = "<a href='" + dr.url + "'> open </a>";
          progressList.addItem(progObject);
      }
 
      // Prompt user to login on a fault.
       private function faultHandler(event:FaultEvent):void
            {
             if(event.fault.faultCode=="Client.Authentication")
             {
                 Alert.show(
                     event.fault.faultString + "\n" +
                     event.fault.faultCode + "\n" +
                     "Please login to continue.");
             }
            }
 
       // AEM Forms  logout method
     private function ROLogout():void {
         // Add result and fault handlers.
         token = cs.logout();
         token.addResponder(new AsyncResponder(LogoutResultEvent,LogoutFaultEvent));
     }
 
     // Handle successful logout.
     private function LogoutResultEvent(event:ResultEvent,
         token:Object=null):void {
         switch (event.result) {
         case "success":
                 authenticatedCB.selected = false;
                 btnFile.enabled = false;
                 btnLogout.enabled = false;
                 btnLogin.enabled = true;
                 break;
                 default:
             }
     }
 
     // Handle logout failure.
     private function LogoutFaultEvent(event:FaultEvent,
             token:Object=null):void {
             Alert.show("Logout failure: " + event.fault.faultString);
     }
 
          private function resultHandler(event:ResultEvent):void {
          // Do anything else here.
          }
        ]]>
 
      </mx:Script>
      <mx:RemoteObject id="EncryptDocument" destination="MyApplication/EncryptDocument" result="resultHandler(event);">
          <mx:method name="invoke" result="handleResult(event)"/>
      </mx:RemoteObject>
 
       <!--//This consists of what is displayed on the webpage-->
      <mx:Panel id="lcPanel" title="EncryptDocument  (Deprecated for AEM forms) AEM Forms Remoting Example"
           height="25%" width="25%" paddingTop="10" paddingLeft="10" paddingRight="10"
           paddingBottom="10">
         <mx:Label width="100%" color="blue"
                text="Select a PDF file to pass to the EncryptDocument process"/>
        <mx:DataGrid x="10" y="0" width="500" id="idProgress" editable="false"
           dataProvider="{progressList}" height="231" selectable="false" >
          <mx:columns>
            <mx:DataGridColumn headerText="Filename" width="200" dataField="filename" editable="false"/>
            <mx:DataGridColumn headerText="State" width="75" dataField="state" editable="false"/>
            <mx:DataGridColumn headerText="Timing" width="75" dataField="timing" editable="false"/>
            <mx:DataGridColumn headerText="Click to Open" dataField="link" editable="false" >
             <mx:itemRenderer>
                <mx:Component>
                   <mx:Text x="0" y="0" width="100%" htmlText="{data.link}"/>
                </mx:Component>
             </mx:itemRenderer>
            </mx:DataGridColumn>
          </mx:columns>
        </mx:DataGrid>
        <mx:Button label="Select File" click="uploadFile()"  id="btnFile" enabled="false"/>
        <mx:Button label="Login" click="ROLogin();" id="btnLogin"/>
        <mx:Button label="LogOut" click="ROLogout();" enabled="false" id="btnLogout"/>
        <mx:HBox>
         <mx:Label text="User:"/>
         <mx:TextInput id="txtUser" text=""/>
         <mx:Label text="Password:"/>
         <mx:TextInput id="txtPassword" text="" displayAsPassword="true"/>
         <mx:CheckBox id="authenticatedCB"
             label="Authenticated?"
             enabled="false"/>
     </mx:HBox>
      </mx:Panel>
 </mx:Application>
```

**另請參閱**

[使用叫用AEM Forms(AEM表單已淘汰)AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[使用(AEM表單已淘汰)AEM Forms Remoting處理檔案](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[包含AEM Forms Flex程式庫檔案](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[使用(AEM表單已過時)AEM Forms Remoting傳遞不安全的檔案，以叫用短期處理程式](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[驗證使用Flex建置的用戶端應用程式](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

## 使用Remoting {#invoking-custom-component-services-using-remoting}調用自定義元件服務

您可以使用Remoting叫用自訂元件中的服務。 例如，請考慮包含客戶服務的銀行元件。 您可以使用寫入Flex的用戶端應用程式，叫用屬於客戶服務的作業。 您必須先建立銀行自定義元件，才能執行與此部分關聯的快速啟動。

客戶服務公開名為`createCustomer`的操作。 本討論介紹如何建立調用客戶服務並建立客戶的Flex客戶端應用程式。 此操作需要一個代表新客戶的`com.adobe.livecycle.sample.customer.Customer`類型的複雜對象。 下圖顯示了調用客戶服務並建立新客戶的客戶端應用程式。 `createCustomer`操作返回客戶標識符值。 識別碼值會顯示在「客戶識別碼」文字方塊中。

![iu_iu_flexnewcust](assets/iu_iu_flexnewcust.png)

下表列出了屬於此客戶端應用程式的控制項。

<table>
 <thead>
  <tr>
   <th><p>控制項名稱</p></th>
   <th><p>說明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>txtFirst</p></td>
   <td><p>指定客戶的名字。 </p></td>
  </tr>
  <tr>
   <td><p>txtLast</p></td>
   <td><p>指定客戶的姓氏。 </p></td>
  </tr>
  <tr>
   <td><p>txtPhone</p></td>
   <td><p>指定客戶的電話號碼。</p></td>
  </tr>
  <tr>
   <td><p>txtStreet</p></td>
   <td><p>指定客戶的街道名稱。</p></td>
  </tr>
  <tr>
   <td><p>txtState</p></td>
   <td><p>指定客戶的狀態。 </p></td>
  </tr>
  <tr>
   <td><p>txtZIP</p></td>
   <td><p>指定客戶的郵遞區號。 </p></td>
  </tr>
  <tr>
   <td><p>txtCity</p></td>
   <td><p>指定客戶的城市。</p></td>
  </tr>
  <tr>
   <td><p>txtCustId</p></td>
   <td><p>指定新帳戶所屬的客戶識別碼值。 此文本框由客戶服務<code>createCustomer</code>操作的返回值填充。 </p></td>
  </tr>
 </tbody>
</table>

### 映射AEM Forms複雜資料類型{#mapping-aem-forms-complex-data-types}

有些AEM Forms作業需要複雜的資料類型作為輸入值。 這些複雜的資料類型定義了操作使用的運行時值。 例如，客戶服務的`createCustomer`操作需要`Customer`實例，該實例包含服務所需的運行時值。 若沒有複雜類型，客戶服務會擲回例外狀況，而不執行操作。

叫用AEM Forms服務時，建立對應至必要AEM Forms複雜類型的ActionScript物件。 對於操作需要的每種複雜資料類型，建立一個單獨的ActionScript對象。

在ActionScript類別中，使用`RemoteClass`中繼資料標籤來對應至AEM Forms複雜類型。 例如，在調用客戶服務的`createCustomer`操作時，建立映射到`com.adobe.livecycle.sample.customer.Customer`資料類型的ActionScript類。

以下名為Customer的ActionScript類說明如何映射到AEM Forms資料類型`com.adobe.livecycle.sample.customer.Customer`。

```java
 package customer
 
 {
     [RemoteClass(alias="com.adobe.livecycle.sample.customer.Customer")]
     public class Customer
     {
            public var name:String;
            public var street:String;
            public var city:String;
            public var state:String;
            public var phone:String;
            public var zip:int;
        }
 }
```

AEM Forms複雜類型的完全限定資料類型將分配給別名標籤。

ActionScript類的欄位與屬於AEM Forms複雜類型的欄位匹配。 客戶ActionScript類中的六個欄位與屬於`com.adobe.livecycle.sample.customer.Customer`的欄位匹配。

>[!NOTE]
要確定屬於Forms複雜類型的欄位名稱，最好在Web瀏覽器中查看服務的WSDL。 WSDL指定服務的複雜類型和相應的資料成員。 以下WSDL用於客戶服務：`https://[yourServer]:[yourPort]/soap/services/CustomerService?wsdl.`

客戶ActionScript類屬於名為customer的包。 建議您將對應至複雜AEM Forms資料類型的所有ActionScript類別放入自己的套件中。 在Flex專案的src資料夾中建立資料夾，並將ActionScript檔案置於資料夾中，如下圖所示。

![iu_iu_customeras](assets/iu_iu_customeras.png)

### 快速入門：使用Remoting {#quick-start-invoking-the-customer-custom-service-using-remoting}調用客戶自定義服務

以下代碼示例調用客戶服務並建立新客戶。 執行此程式碼範例時，請務必填寫所有文字方塊。 同時，請確定您建立對應至`com.adobe.livecycle.sample.customer.Customer`的Customer.as檔案。

>[!NOTE]
在執行此快速啟動之前，您必須建立並部署銀行自定義元件。

```java
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Application  layout="absolute" backgroundColor="#B1ABAB">
 
 <mx:Script>
            <![CDATA[
 
      import flash.net.FileReference;
      import flash.net.URLRequest;
      import flash.events.Event;
      import flash.events.DataEvent;
      import mx.messaging.ChannelSet;
      import mx.messaging.channels.AMFChannel;
      import mx.rpc.events.ResultEvent;
      import mx.collections.ArrayCollection;
      import mx.rpc.AsyncToken;
      import mx.managers.CursorManager;
      import mx.rpc.remoting.mxml.RemoteObject;
 
 
      // Custom class that corresponds to an input to the
      // AEM Forms encryption method
      import customer.Customer;
 
      // Classes used in file retrieval
      private var fileRef:FileReference = new FileReference();
      private var parentResourcePath:String = "/";
      private var serverPort:String = "hiro-xp:8080";
      private var now1:Date;
      private var fileName:String;
 
      // Prepares parameters for encryptPDFUsingPassword method call
      public function executeCreateCustomer():void
      {
 
        var cs:ChannelSet= new ChannelSet();
     cs.addChannel(new AMFChannel("remoting-amf", "https://" + serverPort + "/remoting/messagebroker/amf"));
 
     customerService.setCredentials("administrator", "password");
     customerService.channelSet = cs;
 
     //Create a Customer object required to invoke the Customer service's
     //createCustomer operation
     var myCust:Customer = new Customer();
 
     //Get values from the user of the Flex application
     var fullName:String = txtFirst.text +" "+txtLast.text ;
     var Phone:String = txtPhone.text;
     var Street:String = txtStreet.text;
     var State:String = txtState.text;
     var Zip:int = parseInt(txtZIP.text);
     var City:String = txtCity.text;
 
     //Populate Customer fields
     myCust.name = fullName;
     myCust.phone = Phone;
     myCust.street= Street;
     myCust.state= State;
     myCust.zip = Zip;
     myCust.city = City;
 
     //Invoke the Customer service's createCustomer operation
     var params:Object = new Object();
        params["inCustomer"]=myCust;
     var token:AsyncToken;
        token = customerService.createCustomer(params);
        token.name = name;
      }
 
      private function handleResult(event:ResultEvent):void
      {
          // Retrieve the information returned from the service invocation
          var token:AsyncToken = event.token;
          var res:Object = event.result;
          var custId:String = res["CustomerId"] as String;
 
          //Assign to the custId to the text box
          txtCustId.text = custId;
      }
 
 
      private function resultHandler(event:ResultEvent):void
      {
 
      }
            ]]>
 </mx:Script>
 <mx:RemoteObject id="customerService" destination="CustomerService" result="resultHandler(event);">
 <mx:method name="createCustomer" result="handleResult(event)"/>
 </mx:RemoteObject>
 
 
 <mx:Style source="../bank.css"/>
     <mx:Grid>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="New Customer" fontSize="16" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="First Name:" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtFirst"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:Button label="Create Customer" id="btnCreateCustomer" click="executeCreateCustomer()"/>
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="Last Name" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtLast"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="Phone" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtPhone"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="Street" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtStreet"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="State" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtState"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="ZIP" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtZIP"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="City" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtCity"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                             <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="Customer Identifier" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtCustId" editable="false"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                 </mx:Grid>
 </mx:Application>
 
```

**樣式表**

此快速入門包含名為&#x200B;*bank.css*&#x200B;的樣式表。 以下代碼表示使用的樣式表。

```css
 /* CSS file */
 global
 {
          backgroundGradientAlphas: 1.0, 1.0;
          backgroundGradientColors: #525152,#525152;
          borderColor: #424444;
          verticalAlign: middle;
          color: #FFFFFF;
          font-size:12;
          font-weight:normal;
 }
 
 ApplicationControlBar
 {
          fillAlphas: 1.0, 1.0;
          fillColors: #393839, #393839;
 }
 
 .textField
 {
          backgroundColor: #393839;
          background-disabled-color: #636563;
 }
 
 
 .button
 {
          fillColors: #636563, #424242;
 }
 
 .dropdownMenu
 {
          backgroundColor: #DDDDDD;
          fillColors: #636563, #393839;
          alternatingItemColors: #888888, #999999;
 }
 
 .questionLabel
 {
 
 }
 
 ToolTip
 {
        backgroundColor: black;
        backgroundAlpha: 1.0;
        cornerRadius: 0;
        color: white;
 }
 
 DateChooser
 {
        cornerRadius: 0; /* pixels */
        headerColors: black, black;
        borderColor: black;
        themeColor: black;
        todayColor: red;
        todayStyleName: myTodayStyleName;
        headerStyleName: myHeaderStyleName;
        weekDayStyleName: myWeekDayStyleName;
        dropShadowEnabled: true;
 }
 
 .myTodayStyleName
 {
        color: white;
 }
 
 .myWeekDayStyleName
 {
        fontWeight: normal;
 }
 
 .myHeaderStyleName
 {
        color: red;
        fontSize: 16;
        fontWeight: bold;
 }
```

**另請參閱**

[使用叫用AEM Forms(AEM表單已淘汰)AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[使用(AEM表單已淘汰)AEM Forms Remoting處理檔案](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[包含AEM Forms Flex程式庫檔案](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[使用(AEM表單已過時)AEM Forms Remoting傳遞不安全的檔案，以叫用短期處理程式](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[驗證使用Flex建置的用戶端應用程式](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[使用遠程功能傳遞安全文檔以調用進程](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)
