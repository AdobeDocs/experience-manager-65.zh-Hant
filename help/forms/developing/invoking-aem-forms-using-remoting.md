---
title: 使用Remoting叫用AEM Forms
seo-title: 使用Remoting叫用AEM Forms
description: 'null'
seo-description: 'null'
uuid: 592d1519-c38b-4b33-8cf3-61e2bff81501
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 3d8bb2d3-b1f8-49e1-a529-b3e7a28da4bb
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '4593'
ht-degree: 0%

---


# 使用Remoting {#invoking-aem-forms-using-remoting}叫用AEM Forms

在Workbench中建立的流程可通過使用Remoting調用。 也就是說，您可以從使用Flex建立的用戶端應用程式叫用AEM Forms程式。 這項功能以資料服務為基礎。

>[!NOTE]
>
>使用Remoting時，建議您叫用在Workbench中建立的程式，而非AEM Forms服務。 不過，您可以直接叫用AEM Forms服務。 （請參閱「使用AEM Forms開發人員中心上的遠端加密PDF檔案」）。

>[!NOTE]
>
>如果AEM Forms服務未設定為允許匿名存取，則來自Flex用戶端的要求會造成網頁瀏覽器的挑戰。 用戶必須輸入用戶名和密碼憑據。

下列AEM Forms短期處理程式（名為`MyApplication/EncryptDocument`）可使用Remoting來呼叫。 (有關此進程的資訊（如其輸入和輸出值），請參見[短壽命進程示例](/help/forms/developing/aem-forms-processes.md)。)

![iu_iu_encryptdocumentprocess2](assets/iu_iu_encryptdocumentprocess2.png)

>[!NOTE]
>
>若要使用Flex應用程式叫用AEM Forms程式，請確定已啟用遠端端點。 預設情況下，在部署進程時將啟用遠程端點。

調用此進程時，它執行以下操作：

1. 取得以輸入值傳遞的不安全PDF檔案。 此操作基於`SetValue`操作。 輸入參數的名稱為`inDoc`，其資料類型為`document`。 （`document`資料類型是Workbench內的可用資料類型。）
1. 使用密碼加密PDF檔案。 此操作基於`PasswordEncryptPDF`操作。 此程式的輸出值名稱為`outDoc`，代表密碼加密的PDF檔案。 outDoc的資料類型為`document`。
1. 將密碼加密的PDF檔案儲存為PDF檔案至本機檔案系統。 此操作基於`WriteDocument`操作。

>[!NOTE]
>
>`MyApplication/EncryptDocument`程式不以現有的AEM Forms程式為基礎。 要跟隨代碼示例，請使用Workbench建立名為`MyApplication/EncryptDocument`的流程。

>[!NOTE]
>
>有關使用Remoting調用長壽命進程的資訊，請參閱[調用以人為中心的長壽命進程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)。

**另請參閱**

[包含AEM Forms Flex程式庫檔案](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[使用（AEM表單不建議使用）AEM Forms Remoting處理檔案](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[使用（AEM表單不建議使用）AEM Forms Remoting傳遞不安全的檔案，以叫用短暫的程式](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[驗證使用Flex建立的用戶端應用程式](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[使用Remoting傳遞安全檔案以叫用程式](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

[使用Remoting叫用自訂元件服務](invoking-aem-forms-using-remoting.md#invoking-custom-component-services-using-remoting)

[建立使用Flex建立的用戶端應用程式，以叫用以人為中心的長壽命程式](/help/forms/developing/invoking-human-centric-long-lived.md#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process)

[建立使用HTTP Token執行SSO驗證的Flash Builder應用程式](/help/forms/developing/creating-flash-builder-applications-perform.md#creating-flash-builder-applications-that-perform-sso-authentication-using-http-tokens)

如需如何在Flex圖形控制項中顯示流程資料的詳細資訊，請參閱[在Flex圖形中顯示AEM Forms流程資料](https://www.adobe.com/devnet/livecycle/articles/populating_flexcontrols.html)。

>[!NOTE]
>
>*請務必將crossdomain.xml檔案放在適當的位置。例如，假設您在JBoss上部署AEM Forms，請將此檔案置於下列位置：&lt;install_directory>\Adobe_Experience_Manager_forms\jboss\server\lc_turnkey\deploy\jboss-web.deployer\ROOT.war.*

## 包含AEM Forms Flex程式庫檔案{#including-the-aem-forms-flex-library-file}

若要使用Remoting以程式設計方式叫用AEM Forms程式，請將adobe-remoting-provider.swc檔案新增至Flex專案的類別路徑。 此SWC檔案位於以下位置：

* *&lt;install_directory>\Adobe_Experience_Manager_forms\sdk\misc\DataServices\Client-Libraries*

   其中， &lt;*install_directory*>是安裝AEM Forms的目錄。

**另請參閱**

[使用（AEM表單不建議使用）AEM Forms Remoting叫用AEM Forms](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[使用（AEM表單不建議使用）AEM Forms Remoting處理檔案](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[使用（AEM表單不建議使用）AEM Forms Remoting傳遞不安全的檔案，以叫用短暫的程式](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[驗證使用Flex建立的用戶端應用程式](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

## 使用Remoting {#handling-documents-with-remoting}處理文檔

AEM Forms中使用的最重要非原始Java類型之一是`com.adobe.idp.Document`類別。 呼叫AEM Forms作業時，通常需要檔案。 它主要是PDF檔案，但可包含其他檔案類型，例如SWF、HTML、XML或DOC檔案。 （請參閱「使用Java API[將資料傳送至AEM Forms服務」）。](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

使用Flex建立的用戶端應用程式無法直接要求檔案。 例如，您無法啟動Adobe Reader以請求產生PDF檔案的URL。 要求檔案類型（例如PDF和Microsoft Word檔案）會傳回URL結果。 客戶有責任顯示URL的內容。 「檔案管理」服務可協助產生URL和內容類型資訊。 對XML檔案的要求會傳回完整的XML檔案。

### 將文檔作為輸入參數{#passing-a-document-as-an-input-parameter}傳遞

使用Flex建立的用戶端應用程式無法將檔案直接傳遞至AEM Forms程式。 客戶端應用程式會使用`mx.rpc.livecycle.DocumentReference` ActionScript類的實例，將輸入參數傳遞到需要`com.adobe.idp.Document`實例的操作。 Flex用戶端應用程式有數個設定`DocumentReference`物件的選項：

* 當文檔位於伺服器上且其檔案位置已知時，將DocumentReference對象的referenceType屬性設定為REF_TYPE_FILE。 將fileRef屬性設定為檔案的位置，如下例所示：

```java
 ... var docRef: DocumentReference = new DocumentReference(); 
 docRef.referenceType = DocumentReference.REF_TYPE_FILE; 
 docRef.fileRef = "C:/install/adobe/cs2/How to Uninstall.pdf"; ...
```

* 當檔案位於伺服器上且您知道其URL時，請將DocumentReference物件的referenceType屬性設為REF_TYPE_URL。 將url屬性設定為URL，如下列範例所示：

```java
... var docRef: DocumentReference = new DocumentReference(); 
docRef.referenceType = DocumentReference.REF_TYPE_URL; 
docRef.url = "https://companyserver:8080/DocumentManager/116/7855"; ...
```

* 要從客戶端應用程式中的文本字串建立DocumentReference對象，請將DocumentReference對象的referenceType屬性設定為REF_TYPE_INLINE。 將text屬性設定為要包括在對象中的文本，如以下示例所示：

```java
... var docRef: DocumentReference = new DocumentReference(); 
docRef.referenceType = DocumentReference.REF_TYPE_INLINE; 
docRef.text = "Text for my document";  // Optionally, you can override the server’s default character set  // if necessary:  // docRef.charsetName=CharacterSetName  ...
```

* 當檔案不在伺服器上時，請使用「遠端上傳servlet」將檔案上傳至AEM Forms。 AEM Forms的新功能是可上傳安全檔案。 上傳安全文檔時，必須使用具有&#x200B;*文檔上載應用程式用戶*&#x200B;角色的用戶。 如果沒有此角色，用戶將無法上傳安全文檔。 建議您使用單一登入來上傳安全檔案。 （請參閱[使用Remoting](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)傳遞安全文檔以調用進程。）

>[!NOTE]
如果AEM Forms已設定為允許上傳不安全的檔案，您可以使用不具備「檔案上傳應用程式使用者」角色的使用者來上傳檔案。 使用者也可以擁有「檔案上傳」權限。 不過，如果AEM Forms已設定為僅允許安全檔案，請確定使用者具有「檔案上傳應用程式使用者」角色或「檔案上傳」權限。 (請參閱[設定AEM Forms以接受安全且不安全的檔案](invoking-aem-forms-using-remoting.md#configuring-aem-forms-to-accept-secure-and-unsecure-documents)。

您可針對指定的上傳URL使用標準的Flash上傳功能：`https://SERVER:PORT/remoting/lcfileupload`。 然後，只要需要輸入類型`Document`的參數，就可以使用`DocumentReference`對象
` private function startUpload():void  {  fileRef.addEventListener(Event.SELECT, selectHandler);  fileRef.addEventListener("uploadCompleteData", completeHandler);  try  {   var success:Boolean = fileRef.browse();  }    catch (error:Error)  {   trace("Unable to browse for files.");  }  }      private function selectHandler(event:Event):void {  var request:URLRequest = new  URLRequest("https://SERVER:PORT/remoting/lcfileupload")  try   {   fileRef.upload(request);   }    catch (error:Error)   {   trace("Unable to upload file.");   }  }    private function completeHandler(event:DataEvent):void  {   var params:Object = new Object();   var docRef:DocumentReference = new DocumentReference();   docRef.url = event.data as String;   docRef.referenceType = DocumentReference.REF_TYPE_URL;  }`遠程快速入門使用遠程上載servlet將PDF檔案傳遞到`MyApplication/EncryptDocument`進程。 (請參閱[使用（AEM表單已過時）AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)傳遞不安全的檔案，以叫用短暫的程式。)

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

「遠程快速入門」使用「遠程上傳servlet」將PDF檔案傳遞到`MyApplication/EncryptDocument`進程。 (請參閱[使用（AEM表單已過時）AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)傳遞不安全的檔案，以叫用短暫的程式。)

### 將文檔傳回客戶端應用程式{#passing-a-document-back-to-a-client-application}

客戶端應用程式接收類型為`mx.rpc.livecycle.DocumentReference`的對象，用於返回作為輸出參數的`com.adobe.idp.Document`實例的服務操作。 由於用戶端應用程式處理的是ActionScript物件，而非Java，因此您無法將以Java為基礎的檔案物件傳回至Flex用戶端。 伺服器會為檔案產生URL，並將URL傳回用戶端。 `DocumentReference`物件的`referenceType`屬性指定內容是位於`DocumentReference`物件中，還是必須從`DocumentReference.url`屬性的URL擷取。 `DocumentReference.contentType`屬性指定文檔類型。

**另請參閱**

[使用（AEM表單不建議使用）AEM Forms Remoting叫用AEM Forms](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[包含AEM Forms Flex程式庫檔案](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[使用（AEM表單不建議使用）AEM Forms Remoting傳遞不安全的檔案，以叫用短暫的程式](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[驗證使用Flex建立的用戶端應用程式](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[使用Remoting傳遞安全檔案以叫用程式](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

## 使用Remoting {#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting}傳遞不安全的檔案，以叫用短暫的進程

若要從使用Flex建立的應用程式叫用AEM Forms程式，請執行下列工作：

1. 建立`mx:RemoteObject`實例。
1. 建立`ChannelSet`實例。
1. 傳遞必要的輸入值。
1. 處理返回值。

>[!NOTE]
本節討論當AEM Forms設定為上傳不安全的檔案時，如何叫用AEM Forms程式並上傳檔案。 如需如何叫用AEM Forms進程和上傳安全檔案，以及如何設定AEM Forms以接受安全且不安全的檔案的詳細資訊，請參閱[使用Remoting](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)傳送安全檔案以叫用程式。

**建立mx:RemoteObject實例**

您可以建立`mx:RemoteObject`例項，以叫用在Workbench中建立的AEM Forms流程。 要建立`mx:RemoteObject`實例，請指定以下值：

* **id:** 表示要調 `mx:RemoteObject` 用的進程的實例名稱。
* **目標：** 要叫用的AEM Forms程式名稱。例如，要調用`MyApplication/EncryptDocument`進程，請指定`MyApplication/EncryptDocument`。
* **結果：** 處理結果的Flex方法名稱。

在`mx:RemoteObject`標籤中，指定`<mx:method>`標籤，以指定進程調用方法的名稱。 通常，Forms調用方法的名稱為`invoke`。

下面的代碼示例建立調用`MyApplication/EncryptDocument`進程的`mx:RemoteObject`實例。

```java
 <mx:RemoteObject id="EncryptDocument" destination="MyApplication/EncryptDocument" result="resultHandler(event);">
          <mx:method name="invoke" result="handleExecuteInvoke(event)"/>
      </mx:RemoteObject>
```

**建立AEM表單的渠道**

用戶端應用程式可在MXML或ActionScript中指定頻道來叫用AEM Forms，如下列ActionScript範例所示。 渠道必須是`AMFChannel`、`SecureAMFChannel`、`HTTPChannel`或`SecureHTTPChannel`。

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

將`ChannelSet`例項指派給`mx:RemoteObject`例項的`channelSet`欄位（如上面的程式碼範例所示）。 通常，在調用`ChannelSet.addChannel`方法時，您會在import語句中導入channel類，而不是指定完全限定的名稱。

**傳遞輸入值**

在Workbench中建立的流程可採用零個或多個輸入參數並返回輸出值。 用戶端應用程式會在`ActionScript`物件內傳送輸入參數，並傳送與屬於AEM Forms程式的參數對應的欄位。 名為`MyApplication/EncryptDocument`的短期進程需要一個名為`inDoc`的輸入參數。 進程公開的操作名稱為`invoke`（短期進程的預設名稱）。 (請參閱[使用（AEM表單已過時）AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)叫用AEM Forms。)

以下代碼示例將PDF文檔傳遞到`MyApplication/EncryptDocument`進程：

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

在此程式碼範例中，`pdfDocument`是`DocumentReference`例項，包含不安全的PDF檔案。 如需`DocumentReference`的詳細資訊，請參閱[處理檔案時使用（AEM表單已過時）AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)。

**叫用服務的特定版本**

您可以使用調用的參數映射中的`_version`參數來調用特定版本的Forms服務。 例如，要調用`MyApplication/EncryptDocument`服務的1.2版：

```java
 var params:Object = new Object();
 params["inDoc"] = pdfDocument;
 params["_version"] = "1.2"
 var token:AsyncToken = echoService.echoString(params);
```

`version`參數必須是包含單一句點的字串。 句點的左、主版和右、次版的值必須是整數。 如果未指定此參數，則會調用頭活動版本。

**處理返回值**

AEM Forms流程輸出參數會反序列化至ActionScript物件，用戶端應用程式會從這些物件依名稱擷取特定參數，如下列範例所示。 （`MyApplication/EncryptDocument`進程的輸出值名為`outDoc`。）

```java
     ...
     var res:Object = event.result;
     var docRef:DocumentReference = res["outDoc"] as DocumentReference;
     ...
```

**調用MyApplication/EncryptDocument進程**

通過執行以下步驟，可以調用`MyApplication/EncryptDocument`進程：

1. 透過ActionScript或MXML建立`mx:RemoteObject`例項。 請參閱建立mx:RemoteObject例項。
1. 設定`ChannelSet`例項以與AEM Forms通訊，並將它與`mx:RemoteObject`例項建立關聯。 請參閱「建立AEM表單的渠道」。
1. 呼叫ChannelSet的`login`方法或服務的`setCredentials`方法，以指定使用者識別碼值和密碼。 （請參閱[使用單一登入](invoking-aem-forms-using-remoting.md#using-single-sign-on)）。
1. 在`mx.rpc.livecycle.DocumentReference`例項中填入不安全的PDF檔案，以傳遞至`MyApplication/EncryptDocument`程式。 （請參閱[將文檔作為輸入參數](invoking-aem-forms-using-remoting.md#passing-a-document-as-an-input-parameter)傳遞。）
1. 呼叫`mx:RemoteObject`例項的`invoke`方法，以加密PDF檔案。 傳遞包含輸入參數的`Object`（此為不安全的PDF檔案）。 請參閱傳遞輸入值。
1. 擷取從程式傳回的密碼加密PDF檔案。 請參閱處理返回值。

[快速入門：使用（AEM表單不建議使用）AEM Forms Remoting傳遞不安全的檔案，以叫用短暫的程式](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-by-passing-an-unsecure-document-using-deprecated-for-aem-forms-aem-forms-remoting)

## 驗證使用Flex {#authenticating-client-applications-built-with-flex}建立的用戶端應用程式

AEM Forms使用者管理員可透過數種方式來驗證來自Flex應用程式的Remoting要求，包括透過中央登入服務、基本驗證和自訂驗證的AEM Forms單一登入。 當未啟用單一登入或匿名存取時，遠端要求會產生基本驗證（預設值）或自訂驗證。

基本驗證需仰賴Web應用程式容器中的標準J2EE基本驗證。 對於基本驗證，HTTP 401錯誤會造成瀏覽器挑戰。 這表示當您嘗試使用RemoteObject連線至Forms應用程式，但尚未從Flex應用程式登入時，瀏覽器會提示您輸入使用者名稱和密碼。

對於自訂驗證，伺服器會傳送錯誤給用戶端，指出需要驗證。

>[!NOTE]
如需使用HTTP Token執行驗證的詳細資訊，請參閱「建立使用HTTP Token執行SSO驗證的Flash Builder應用程式」[。](/help/forms/developing/creating-flash-builder-applications-perform.md#creating-flash-builder-applications-that-perform-sso-authentication-using-http-tokens)

### 使用自訂驗證{#using-custom-authentication}

通過將遠程端點上的驗證方法從「基本」更改為「自定義」，可以在管理控制台中啟用自定義驗證。 如果您使用自訂驗證，您的用戶端應用程式會呼叫`ChannelSet.login`方法以登入，而呼叫`ChannelSet.logout`方法以登出。

>[!NOTE]
在舊版AEM Forms中，您會呼叫`RemoteObject.setCredentials`方法，將認證傳送至目的地。 `setCredentials`方法直到元件第一次嘗試連接到伺服器時才實際將憑據傳遞到伺服器。 因此，如果元件發出故障事件，則無法確定是否由於驗證錯誤或其他原因發生故障。 當您呼叫`ChannelSet.login`方法時，會連線至伺服器，以便您能立即處理驗證問題。 雖然您可以繼續使用`setCredentials`方法，但建議您使用`ChannelSet.login`方法。

由於多個目標可以使用相同的通道和相應的ChannelSet對象，因此登錄到一個目標會將用戶登錄到使用相同通道或通道的任何其他目標。 如果兩個元件將不同的憑據應用到同一ChannelSet對象，則會使用最後應用的憑據。 如果多個元件使用相同的已驗證ChannelSet對象，則調用`logout`方法會將所有元件從目標中記錄出來。

以下示例使用`ChannelSet.login`和`ChannelSet.logout`方法和RemoteObject控制項。 此應用程式執行以下操作：

* 在`creationComplete`處理常式中建立`ChannelSet`物件，代表`RemoteObject`元件使用的頻道
* 響應Button click事件調用`ROLogin`函式，將憑據傳遞給伺服器
* 使用RemoteObject元件向伺服器發送字串以響應Button按一下事件。 伺服器將相同的字串返回RemoteObject元件
* 使用RemoteObject元件的結果事件在TextArea控制項中顯示字串
* 響應Button click事件調用`ROLogout`函式以登出伺服器

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

`login`和`logout`方法會傳回AsyncToken物件。 為結果事件指派事件處理常式至AsyncToken物件，以處理成功的呼叫，並為錯誤事件指派處理常式以處理失敗。

### 使用單一登入{#using-single-sign-on}

AEM Forms使用者可以連線至多個AEM Forms Web應用程式，以執行工作。 當使用者從一個Web應用程式移至另一個Web應用程式時，要求他們個別登入每個Web應用程式並不有效。 AEM Forms單一登入機制可讓使用者登入一次，然後存取任何AEM Forms Web應用程式。 由於AEM Forms開發人員可建立用於AEM Forms的用戶端應用程式，因此他們也必須能夠運用單一登入機制。

每個AEM Forms Web應用程式都會封裝在其專屬的Web Archive(WAR)檔案中，然後封裝為企業檔案(EAR)檔案的一部分。 由於應用程式伺服器不允許在不同網路應用程式間共用工作階段資料，AEM Forms會使用HTTP Cookie來儲存驗證資訊。 驗證Cookie可讓使用者登入Forms應用程式，然後連線至其他AEM Forms網頁應用程式。 此技術稱為單一登入。

AEM Forms開發人員編寫用戶端應用程式，以擴充表單指南（已過時）的功能，並自訂工作區。 例如，工作區應用程式可以啟動程式。 然後，客戶端應用程式使用遠程端點從Forms服務中檢索資料。

當使用（針對AEM表單已過時）AEM Forms Remoting呼叫AEM Forms服務時，用戶端應用程式會將驗證Cookie傳送為請求的一部分。 由於使用者已經通過驗證，因此不需要額外登入，就能將用戶端應用程式連線至AEM Forms服務。

>[!NOTE]
如果Cookie無效或遺失，則沒有內含的重新導向至登入頁面。 因此，您仍可呼叫匿名服務。

您可以透過編寫自行登入和登出的用戶端應用程式，略過AEM Forms單一登入機制。 如果您略過單一登入機制，則可對應用程式使用基本或自訂驗證。

由於此機制不使用AEM Forms單一登入機制，因此不會將驗證Cookie寫入用戶端。 登錄憑據儲存在遠程通道的`ChannelSet`對象中。 因此，您對相同`ChannelSet`進行的任何`RemoteObject`呼叫都是在這些認證的上下文中進行的。

### 在AEM Forms {#setting-up-single-sign-on-in-aem-forms}中設定單一登入

若要在AEM Forms中使用單一登入，請安裝表單工作流程元件，其中包含集中式登入服務。 使用者成功登入後，集中式登入服務會傳回驗證Cookie給使用者。 後續對Forms Web應用程式的每個要求都包含Cookie。 如果Cookie有效，使用者即視為已驗證，不必再登入。

### 編寫使用單一登入{#writing-a-client-application-that-uses-single-sign-on}的用戶端應用程式

當您運用單一登入機制時，您預期使用者在啟動用戶端應用程式之前，應使用集中式登入服務來登入。 也就是說，客戶端應用程式不通過瀏覽器或通過調用`ChannelSet.login`方法登錄。

如果您使用AEM Forms單一登入機制，請設定Remoting端點，使用自訂驗證，而非基本驗證。 否則，當使用基本驗證時，驗證錯誤會導致瀏覽器出現問題，您不希望使用者看到。 您的應用程式會偵測到驗證錯誤，然後顯示訊息，指示使用者使用集中式登入服務登入。

用戶端應用程式會使用`RemoteObject`元件，透過遠端端點存取AEM Forms，如下列範例所示。

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

**在Flex應用程式仍在執行時，以新使用者身分登入**

使用Flex建立的應用程式會包含驗證Cookie，而且每次要求AEM Forms服務時都會用到它。 基於效能原因，AEM Forms不會在每個請求上驗證Cookie。 不過，AEM Forms會偵測到驗證Cookie何時被其他驗證Cookie取代。

例如，您啟動客戶端應用程式，當應用程式處於活動狀態時，您使用集中式登錄服務登出。 接下來，您可以以不同的使用者身分登入。 以不同使用者身分登入時，會以新使用者的驗證Cookie取代現有的驗證Cookie。

在來自用戶端應用程式的下一個要求時，AEM Forms會偵測到Cookie已變更，並登出使用者。 因此，Cookie變更後的第一個請求會失敗。 所有後續請求都會在新Cookie的上下文中提出並成功。

**登出**

若要登出AEM Forms並使作業無效，必須從用戶端的電腦刪除驗證Cookie。 由於單一登入的目的是讓使用者登入一次，因此您不希望用戶端應用程式刪除Cookie。 此動作可有效登出使用者。

因此，在客戶端應用程式中調用`RemoteObject.logout`方法會在客戶端上生成一條錯誤消息，指定會話未註銷。 使用者可以改用集中式登入服務來登出和刪除驗證Cookie。

**在Flex應用程式仍在執行時登出**

您可以啟動以Flex建立的用戶端應用程式，並使用集中式登入服務登出。 在登出程式中，會刪除驗證Cookie。 如果提出移除要求時沒有Cookie，或是使用無效的Cookie，使用者作業會無效。 此操作實際上是註銷。 下次用戶端應用程式嘗試連線至AEM Forms服務時，會要求使用者登入。

**另請參閱**

[使用（AEM表單不建議使用）AEM Forms Remoting叫用AEM Forms](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[使用（AEM表單不建議使用）AEM Forms Remoting處理檔案](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[包含AEM Forms Flex程式庫檔案](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[使用（AEM表單不建議使用）AEM Forms Remoting傳遞不安全的檔案，以叫用短暫的程式](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[使用Remoting傳遞安全檔案以叫用程式](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

## 使用Remoting {#passing-secure-documents-to-invoke-processes-using-remoting}傳遞安全文檔以調用進程

在叫用需要一或多份檔案的程式時，您可以將安全檔案傳遞至AEM Forms。 通過傳遞安全文檔，您可以保護業務資訊和機密文檔。 在這種情況下，檔案可以參照PDF檔案、XML檔案、Word檔案等。 當AEM Forms設定為允許安全檔案時，必須將安全檔案從以Flex編寫的用戶端應用程式傳送至AEM Forms。 （請參閱[設定AEM Forms以接受安全且不安全的檔案](invoking-aem-forms-using-remoting.md#configuring-aem-forms-to-accept-secure-and-unsecure-documents)）。

傳遞安全檔案時，請使用單一登入並指定具有&#x200B;*檔案上傳應用程式使用者*&#x200B;角色的AEM表單使用者。 如果沒有此角色，用戶將無法上傳安全文檔。 您可以以程式設計方式為使用者指派角色。 （請參閱[管理角色和權限](/help/forms/developing/users.md#managing-roles-and-permissions)。）

>[!NOTE]
當您建立新角色並希望該角色的成員上傳安全檔案時，請確定您指定「檔案上傳」權限。

AEM Forms支援名為`getFileUploadToken`的作業，可傳回傳遞至上傳servlet的Token。 `DocumentReference.constructRequestForUpload`方法需要AEM Forms的URL以及`LC.FileUploadAuthenticator.getFileUploadToken`方法傳回的Token。 此方法返回在調用上載servlet時使用的`URLRequest`對象。 下列程式碼會示範此應用程式邏輯。

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

### 設定AEM Forms以接受安全和不安全的檔案{#configuring-aem-forms-to-accept-secure-and-unsecure-documents}

您可以使用管理控制台來指定將檔案從Flex用戶端應用程式傳送至AEM Forms程式時，檔案是否安全。 依預設，AEM Forms會設定為接受安全檔案。 您可以執行下列步驟，將AEM Forms設定為接受安全檔案：

1. 登入管理控制台。
1. 按一下&#x200B;**Settings**。
1. 按一下&#x200B;**核心繫統設定。**
1. 按一下配置。
1. 請確定未選取「允許從Flex應用程式上傳非安全的檔案」選項。

>[!NOTE]
若要設定AEM Forms以接受不安全的檔案，請選取「允許從Flex應用程式上傳非安全的檔案」選項。 然後重新啟動應用程式或服務，以確保設定生效。

### 快速入門：使用Remoting {#quick-start-invoking-a-short-lived-process-by-passing-a-secure-document-using-remoting}傳遞安全文檔，以叫用短期流程

以下代碼示例調用`MyApplication/EncryptDocument.`用戶必須登錄才能按一下用於上傳PDF檔案並調用該過程的「選擇檔案」按鈕。 也就是說，一旦用戶通過驗證，「選擇檔案」按鈕即會啟用。 下圖顯示在使用者經過驗證後的Flex用戶端應用程式。 請注意，已驗證核取方塊已啟用。

![iu_iu_secureremotelogin](assets/iu_iu_secureremotelogin.png)

如果AEM Forms設定為僅允許上傳安全檔案，而使用者沒有&#x200B;*Document Upload Application User*&#x200B;角色，則會擲回例外。 如果使用者確實有此角色，則會上傳檔案並呼叫程式。

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

[使用（AEM表單不建議使用）AEM Forms Remoting叫用AEM Forms](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[使用（AEM表單不建議使用）AEM Forms Remoting處理檔案](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[包含AEM Forms Flex程式庫檔案](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[使用（AEM表單不建議使用）AEM Forms Remoting傳遞不安全的檔案，以叫用短暫的程式](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[驗證使用Flex建立的用戶端應用程式](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

## 使用Remoting {#invoking-custom-component-services-using-remoting}調用自定義元件服務

您可以使用Remoting來叫用自訂元件中的服務。 例如，考慮包含客戶服務的銀行元件。 您可以使用Flex中編寫的用戶端應用程式，來叫用屬於客戶服務的作業。 在執行與此部分關聯的快速啟動之前，您必須建立Bank自定義元件。

客戶服務公開名為`createCustomer`的操作。 本討論說明如何建立叫用客戶服務並建立客戶的Flex用戶端應用程式。 此操作需要一個代表新客戶的`com.adobe.livecycle.sample.customer.Customer`類型的複雜對象。 下圖顯示調用客戶服務並建立新客戶的客戶端應用程式。 `createCustomer`操作返回客戶標識符值。 識別碼值會顯示在「客戶識別碼」文字方塊中。

![iu_iu_flexnewcust](assets/iu_iu_flexnewcust.png)

下表列出屬於此客戶端應用程式的控制項。

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
   <td><p>指定新帳戶所屬的客戶識別碼值。 此文字方塊由客戶服務<code>createCustomer</code>作業的傳回值填入。 </p></td>
  </tr>
 </tbody>
</table>

### 對應AEM Forms複雜的資料類型{#mapping-aem-forms-complex-data-types}

某些AEM Forms作業需要複雜的資料類型作為輸入值。 這些複雜的資料類型定義操作使用的運行時值。 例如，客戶服務的`createCustomer`操作需要包含服務所需運行時值的`Customer`實例。 如果沒有複雜的類型，客戶服務會拋出異常，並且不執行操作。

在叫用AEM Forms服務時，請建立對應至必要AEM Forms複雜類型的ActionScript物件。 針對某個操作需要的每種複雜資料類型，建立一個單獨的ActionScript對象。

在ActionScript類別中，使用`RemoteClass`中繼資料標籤來對應至AEM Forms複雜類型。 例如，在叫用客戶服務的`createCustomer`操作時，請建立映射至`com.adobe.livecycle.sample.customer.Customer`資料類型的ActionScript類別。

下列名為Customer的ActionScript類別顯示如何對應至AEM Forms資料類型`com.adobe.livecycle.sample.customer.Customer`。

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

AEM Forms複雜類型的完全限定資料類型會指派給別名標籤。

ActionScript類別的欄位符合屬於AEM Forms複雜類型的欄位。 位於Customer ActionScript類別中的6個欄位符合屬於`com.adobe.livecycle.sample.customer.Customer`的欄位。

>[!NOTE]
確定屬於Forms複雜類型的欄位名稱的一個好方法是在Web瀏覽器中查看服務的WSDL。 WSDL指定服務的複雜類型和相應的資料成員。 以下WSDL用於客戶服務：`https://[yourServer]:[yourPort]/soap/services/CustomerService?wsdl.`

Customer ActionScript類別屬於名為customer的套件。 建議您將所有對應至複雜AEM Forms資料類型的ActionScript類別置於其專屬的套件中。 在Flex專案的src資料夾中建立資料夾，並將ActionScript檔案置於資料夾中，如下圖所示。

![iu_iu_customeras](assets/iu_iu_customeras.png)

### 快速入門：使用Remoting {#quick-start-invoking-the-customer-custom-service-using-remoting}調用客戶定制服務

以下代碼示例調用客戶服務並建立新客戶。 執行此程式碼範例時，請確定您已填寫所有文字方塊。 此外，請確定您建立對應至`com.adobe.livecycle.sample.customer.Customer`的Customer.as檔案。

>[!NOTE]
您必須先建立並部署Bank自訂元件，才能執行此快速入門。

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

此快速入門包含名為&#x200B;*bank.css*&#x200B;的樣式表。 下列程式碼代表所使用的樣式表。

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

[使用（AEM表單不建議使用）AEM Forms Remoting叫用AEM Forms](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[使用（AEM表單不建議使用）AEM Forms Remoting處理檔案](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[包含AEM Forms Flex程式庫檔案](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[使用（AEM表單不建議使用）AEM Forms Remoting傳遞不安全的檔案，以叫用短暫的程式](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[驗證使用Flex建立的用戶端應用程式](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[使用Remoting傳遞安全檔案以叫用程式](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)
