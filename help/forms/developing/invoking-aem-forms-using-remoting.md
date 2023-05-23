---
title: 調用AEM Forms使用遠程處理
seo-title: Invoking AEM Forms using Remoting
description: 使用遠程處理調用AEM Forms流程以調用在Workbench中建立的流程。 您可以從與Flex一起構建的客戶端應用程式調用AEM Forms進程。
seo-description: Use Remoting to invoke an AEM Forms process to invoke processes created in Workbench. You can invoke a AEM Forms process from a client application built with Flex.
uuid: 592d1519-c38b-4b33-8cf3-61e2bff81501
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 3d8bb2d3-b1f8-49e1-a529-b3e7a28da4bb
role: Developer
exl-id: 94a48776-f537-4b4e-8d71-51b08e463cba
source-git-commit: c47b4dcfd2fbdcb0b98ad815f5b04d8f593e4f64
workflow-type: tm+mt
source-wordcount: '4599'
ht-degree: 0%

---

# 調用AEM Forms使用遠程處理 {#invoking-aem-forms-using-remoting}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

可以使用遠程處理來調用在Workbench中建立的流程。 也就是說，您可以從與Flex一起構建的客戶端應用程式調用AEM Forms進程。 此功能基於資料服務。

>[!NOTE]
>
>使用遠程處理時，建議您調用在Workbench中建立的流程，而不是AEM Forms服務。 但是，可以直接援用AEM Forms服務。 (請參閱使用位於AEM Forms開發中心的遠程處理加密PDF文檔。)

>[!NOTE]
>
>如果未將AEM Forms服務配置為允許匿名訪問，則來自Flex客戶端的請求將導致Web瀏覽器出現問題。 用戶必須輸入用戶名和密碼憑據。

以下AEM Forms短命進程，名為 `MyApplication/EncryptDocument`，可使用遠程處理調用。 (有關此流程的資訊，如其輸入值和輸出值，請參見 [短期流程示例](/help/forms/developing/aem-forms-processes.md)。)

![iu_iu_encryptdocumentprocess2](assets/iu_iu_encryptdocumentprocess2.png)

>[!NOTE]
>
>要使用Flex應用程式調用AEM Forms進程，請確保已啟用遠程處理終結點。 預設情況下，在部署進程時啟用遠程處理終結點。

調用此進程時，它執行以下操作：

1. 獲取作為輸入值傳遞的無擔保PDF文檔。 此操作基於 `SetValue` 的下界。 輸入參數的名稱為 `inDoc` 其資料類型為 `document`。 ( `document` 資料類型是Workbench中的可用資料類型。)
1. 使用密碼加密PDF文檔。 此操作基於 `PasswordEncryptPDF` 的下界。 此進程的輸出值的名稱為 `outDoc` 並表示密碼加密的PDF文檔。 outDoc的資料類型為 `document`。
1. 將密碼加密的PDF文檔另存為PDF檔案到本地檔案系統。 此操作基於 `WriteDocument` 的下界。

>[!NOTE]
>
>的 `MyApplication/EncryptDocument` 進程不基於現有的AEM Forms進程。 要跟隨代碼示例，請建立一個名為 `MyApplication/EncryptDocument` 使用Workbench。

>[!NOTE]
>
>有關使用遠程處理調用長期流程的資訊，請參見 [調用以人為中心的長壽命進程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)。

**另請參閱**

[包括AEM FormsFlex圖書館的檔案](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[處理文檔時使用(不建議AEM使用表單)AEM Forms遠程處理](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[通過使用（不建議使用表單）傳遞不安全文檔來調用短AEM時間進程AEM Forms遠程](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[驗證使用Flex構建的客戶端應用程式](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[通過安全文檔調用進程使用遠程處理](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

[使用遠程調用自定義元件服務](invoking-aem-forms-using-remoting.md#invoking-custom-component-services-using-remoting)

[建立使用Flex構建的客戶端應用程式，該應用程式調用以人為中心的長壽命流程](/help/forms/developing/invoking-human-centric-long-lived.md#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process)

[建立使用HTTP令牌執行SSO身份驗證的Flash Builder應用程式](/help/forms/developing/creating-flash-builder-applications-perform.md#creating-flash-builder-applications-that-perform-sso-authentication-using-http-tokens)

<!-- For information on how to display process data in a Flex graph control, see [Displaying AEM Forms process data in Flex graphs](https://www.adobe.com/devnet/livecycle/articles/populating_flexcontrols.html). This URL is 404. No suitable replacement URL was found after a search. Do not make this link live if it is dead! -->

>[!NOTE]
>
>*請確保將crossdomain.xml檔案放在正確的位置。 例如，假定您在JBoss上部署了AEM Forms，請將此檔案放置在以下位置： &lt;install_directory>\Adobe_Experience_Manager_forms\jboss\server\lc_turnkey\deploy\jboss-web.deployer\ROOT.war。*

## 包括AEM FormsFlex圖書館的檔案 {#including-the-aem-forms-flex-library-file}

要使用遠程處理以寫程式方式調用AEM Forms進程，請將adobe-remoting-provider.swc檔案添加到Flex項目的類路徑中。 此SWC檔案位於以下位置：

* *&lt;install_directory>\Adobe_Experience_Manager_forms\sdk\misc\DataServices\Client-Libraries*

   &lt;*安裝目錄*>是安裝AEM Forms的目錄。

**另請參閱**

[調用AEM Forms使用(不建議AEM用於表單)AEM Forms遠程處理](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[處理文檔時使用(不建議AEM使用表單)AEM Forms遠程處理](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[通過使用（不建議使用表單）傳遞不安全文檔來調用短AEM時間進程AEM Forms遠程](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[驗證使用Flex構建的客戶端應用程式](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

## 使用遠程處理處理文檔 {#handling-documents-with-remoting}

在AEM Forms使用的最重要的非原始Java™類型之一是 `com.adobe.idp.Document` 類。 通常需要文檔來調用AEM Forms操作。 它主要是PDF文檔，但可以包含其他文檔類型，如SWF、HTML、XML或DOC檔案。 (請參閱 [使用Java API將資料傳遞到AEM Forms服務](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)。)

使用Flex構建的客戶端應用程式無法直接請求文檔。 例如，您無法啟動Adobe Reader以請求生成PDF檔案的URL。 對文檔類型(如PDF和Microsoft® Word文檔)的請求將返回URL結果。 顯示URL的內容是客戶端的責任。 文檔管理服務有助於生成URL和內容類型資訊。 對XML文檔的請求將返回結果中的完整XML文檔。

### 將文檔作為輸入參數傳遞 {#passing-a-document-as-an-input-parameter}

使用Flex構建的客戶端應用程式無法將文檔直接傳遞給AEM Forms進程。 相反，客戶端應用程式使用 `mx.rpc.livecycle.DocumentReference` ActionScript類，將輸入參數傳遞到需要 `com.adobe.idp.Document` 實例。 Flex客戶端應用程式具有多個用於設定 `DocumentReference` 對象：

* 當文檔位於伺服器上且其檔案位置已知時，將DocumentReference對象的referenceType屬性設定為REF_TYPE_FILE。 將fileRef屬性設定為檔案的位置，如下例所示：

```java
 ... var docRef: DocumentReference = new DocumentReference(); 
 docRef.referenceType = DocumentReference.REF_TYPE_FILE; 
 docRef.fileRef = "C:/install/adobe/cs2/How to Uninstall.pdf"; ...
```

* 當文檔在伺服器上且您知道其URL時，將DocumentReference對象的referenceType屬性設定為REF_TYPE_URL。 將url屬性設定為URL，如下例所示：

```java
... var docRef: DocumentReference = new DocumentReference(); 
docRef.referenceType = DocumentReference.REF_TYPE_URL; 
docRef.url = "https://companyserver:8080/DocumentManager/116/7855"; ...
```

* 要從客戶端應用程式中的文本字串建立DocumentReference對象，請將DocumentReference對象的referenceType屬性設定為REF_TYPE_INLINE。 將text屬性設定為要包括在對象中的文本，如下例所示：

```java
... var docRef: DocumentReference = new DocumentReference(); 
docRef.referenceType = DocumentReference.REF_TYPE_INLINE; 
docRef.text = "Text for my document";  // Optionally, you can override the server's default character set  // if necessary:  // docRef.charsetName=CharacterSetName  ...
```

* 當文檔不在伺服器上時，使用遠程上載servlet將文檔上載到AEM Forms。 AEM Forms的新特點是能夠上傳安全文檔。 上載安全文檔時，必須使用 *文檔上載應用程式用戶* 角色。 沒有此角色，用戶無法上載安全文檔。 建議您使用單一登錄來上載安全文檔。 (請參閱 [通過安全文檔調用進程使用遠程處理](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)。)

>[!NOTE]
如果將AEM Forms配置為允許上載不安全的文檔，則可以使用不具有「文檔上載應用程式用戶」角色的用戶上載文檔。 用戶還可以具有「文檔上載」權限。 但是，如果將AEM Forms配置為僅允許安全文檔，則確保用戶具有「文檔上載應用程式用戶」角色或「文檔上載」權限。 (請參閱 [配置AEM Forms以接受安全文檔和不安全文檔](invoking-aem-forms-using-remoting.md#configuring-aem-forms-to-accept-secure-and-unsecure-documents)。

您為指定的上載URL使用標準Flash上載功能： `https://SERVER:PORT/remoting/lcfileupload`。 然後，您可以使用 `DocumentReference` 對象，無論類型的輸入參數 `Document` 預期
` private function startUpload():void  {  fileRef.addEventListener(Event.SELECT, selectHandler);  fileRef.addEventListener("uploadCompleteData", completeHandler);  try  {   var success:Boolean = fileRef.browse();  }    catch (error:Error)  {   trace("Unable to browse for files.");  }  }      private function selectHandler(event:Event):void {  var request:URLRequest = new  URLRequest("https://SERVER:PORT/remoting/lcfileupload")  try   {   fileRef.upload(request);   }    catch (error:Error)   {   trace("Unable to upload file.");   }  }    private function completeHandler(event:DataEvent):void  {   var params:Object = new Object();   var docRef:DocumentReference = new DocumentReference();   docRef.url = event.data as String;   docRef.referenceType = DocumentReference.REF_TYPE_URL;  }`遠程快速啟動使用遠程上載servlet將PDF檔案傳遞到 `MyApplication/EncryptDocument`處理。 (請參閱 [通過使用（不建議使用表單）傳遞不安全文檔來調用短AEM時間進程AEM Forms遠程](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)。)

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

遠程快速啟動使用遠程上載servlet將PDF檔案傳遞到 `MyApplication/EncryptDocument`處理。 (請參閱 [通過使用（不建議使用表單）傳遞不安全文檔來調用短AEM時間進程AEM Forms遠程](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)。)

### 將文檔傳回客戶端應用程式 {#passing-a-document-back-to-a-client-application}

客戶端應用程式接收類型的對象 `mx.rpc.livecycle.DocumentReference` 返回 `com.adobe.idp.Document` 實例作為輸出參數。 由於客戶端應用程式處理的是ActionScript對象，而不是Java，因此不能將基於Java的文檔對象傳回到Flex客戶端。 相反，伺服器會生成文檔的URL並將該URL傳回客戶端。 的 `DocumentReference` 對象 `referenceType` 屬性指定內容是否位於 `DocumentReference` 或必須從 `DocumentReference.url` 屬性。 的 `DocumentReference.contentType` 屬性指定文檔的類型。

**另請參閱**

[調用AEM Forms使用(不建議AEM用於表單)AEM Forms遠程處理](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[包括AEM FormsFlex圖書館的檔案](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[通過使用（不建議使用表單）傳遞不安全文檔來調用短AEM時間進程AEM Forms遠程](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[驗證使用Flex構建的客戶端應用程式](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[通過安全文檔調用進程使用遠程處理](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

## 通過使用遠程處理傳遞不安全文檔來調用短期流程 {#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting}

要從與Flex一起構建的應用程式調用AEM Forms進程，請執行以下任務：

1. 建立 `mx:RemoteObject` 實例。
1. 建立 `ChannelSet` 實例。
1. 傳遞所需輸入值。
1. 處理返回值。

>[!NOTE]
本節討論如何在將AEM Forms配置為上載不安全的文檔時調用和上載文檔。 有關如何調用AEM Forms進程和上載安全文檔以及如何配置AEM Forms以接受安全和不安全文檔的資訊，請參見 [通過安全文檔調用進程使用遠程處理](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)。

**建立mx:RemoteObject實例**

建立 `mx:RemoteObject` 實例，以調用在Workbench中建立的AEM Forms流程。 建立 `mx:RemoteObject` 實例，指定以下值：

* **id:** 名稱 `mx:RemoteObject` 表示要調用的進程的實例。
* **目標：** 要調用的AEM Forms進程的名稱。 例如，要調用 `MyApplication/EncryptDocument` 進程，指定 `MyApplication/EncryptDocument`。
* **結果：** 處理結果的Flex方法的名稱。

在 `mx:RemoteObject` 標籤，指定 `<mx:method>` 指定進程調用方法名稱的標籤。 通常，Forms調用方法的名稱為 `invoke`。

下面的代碼示例建立 `mx:RemoteObject` 調用實例 `MyApplication/EncryptDocument` 處理。

```java
 <mx:RemoteObject id="EncryptDocument" destination="MyApplication/EncryptDocument" result="resultHandler(event);">
          <mx:method name="invoke" result="handleExecuteInvoke(event)"/>
      </mx:RemoteObject>
```

**建立通往AEM Forms的渠道**

客戶端應用程式可通過在或ActionScript中指MXML定通道來調用AEM Forms，如下面的ActionScript示例所示。 通道必須是 `AMFChannel`。 `SecureAMFChannel`。 `HTTPChannel`或 `SecureHTTPChannel`。

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

分配 `ChannelSet` 實例 `mx:RemoteObject` 實例 `channelSet` 欄位（如上一個代碼示例所示）。 通常，在調用導入語句時，可以在導入語句中導入通道類，而不是指定完全限定的名稱 `ChannelSet.addChannel` 的雙曲餘切值。

**傳遞輸入值**

在Workbench中建立的流程可以採用零個或多個輸入參數，並返回一個輸出值。 客戶端應用程式在 `ActionScript` 對象包含與屬於AEM Forms進程的參數對應的欄位。 這個短命的過程 `MyApplication/EncryptDocument`，需要一個名為 `inDoc`。 進程所暴露的操作的名稱為 `invoke` （短時間進程的預設名稱）。 (請參閱 [調用AEM Forms使用(不建議AEM用於表單)AEM Forms遠程處理](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)。)

以下代碼示例將PDF文檔傳遞給 `MyApplication/EncryptDocument` 進程：

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

在此代碼示例中， `pdfDocument` 是 `DocumentReference` 包含不安全PDF文檔的實例。 有關 `DocumentReference`，請參閱 [處理文檔時使用(不建議AEM使用表單)AEM Forms遠程處理](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)。

**調用服務的特定版本**

您可以使用 `_version` 調用的參數映射中的參數。 例如，要調用 `MyApplication/EncryptDocument` 服務：

```java
 var params:Object = new Object();
 params["inDoc"] = pdfDocument;
 params["_version"] = "1.2"
 var token:AsyncToken = echoService.echoString(params);
```

的 `version` 參數必須是包含單個句點的字串。 句點的左、主版本和右、次版本的值必須是整數。 如果未指定此參數，則調用頭活動版本。

**處理返回值**

AEM Forms進程輸出參數被反序列化為ActionScript對象，客戶端應用程式從中按名稱提取特定參數，如下例所示。 (輸出值 `MyApplication/EncryptDocument` 進程命名 `outDoc`。)

```java
     ...
     var res:Object = event.result;
     var docRef:DocumentReference = res["outDoc"] as DocumentReference;
     ...
```

**調用MyApplication/EncryptDocument進程**

您可以調用 `MyApplication/EncryptDocument` 執行以下步驟：

1. 建立 `mx:RemoteObject` 實例通過ActionScript或MXML。 請參閱建立mx:RemoteObject實例。
1. 設定 `ChannelSet` 實例與AEM Forms通信，並將其與 `mx:RemoteObject` 實例。 請參閱建立到AEM Forms的渠道。
1. 調用ChannelSet `login` 方法或服務 `setCredentials` 方法，指定用戶標識符值和口令。 (請參閱 [使用單一登錄](invoking-aem-forms-using-remoting.md#using-single-sign-on)。)
1. 填充 `mx.rpc.livecycle.DocumentReference` 包含未加保護的PDF文檔的實例 `MyApplication/EncryptDocument` 處理。 (請參閱 [將文檔作為輸入參數傳遞](invoking-aem-forms-using-remoting.md#passing-a-document-as-an-input-parameter)。)
1. 通過調用PDF文檔 `mx:RemoteObject` 實例 `invoke` 的雙曲餘切值。 通過 `Object` 包含輸入參數(即不安全的PDF文檔)。 請參閱傳遞輸入值。
1. 檢索從進程返回的密碼加密PDF文檔。 請參閱處理返回值。

[快速啟動：通過使用（不建議使用表單）傳遞不安全文檔來調用短AEM時間進程AEM Forms遠程](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-by-passing-an-unsecure-document-using-deprecated-for-aem-forms-aem-forms-remoting)

## 驗證使用Flex構建的客戶端應用程式 {#authenticating-client-applications-built-with-flex}

有幾種方法可AEM以使用戶管理器對來自Flex應用程式的遠程處理請求進行身份驗證，包括通過中央登錄服務進行AEM Forms單一登錄、基本身份驗證和自定義身份驗證。 如果未啟用單一登錄和匿名訪問，遠程處理請求將導致基本身份驗證（預設）或自定義身份驗證。

基本身份驗證依賴於Web應用程式容器中的標準J2EE基本身份驗證。 對於基本身份驗證，HTTP 401錯誤會導致瀏覽器質詢。 這意味著，當您嘗試使用RemoteObject連接到Forms應用程式，但尚未從Flex應用程式登錄時，瀏覽器會提示您輸入用戶名和密碼。

對於自定義身份驗證，伺服器會向客戶端發送故障，以指示需要身份驗證。

>[!NOTE]
有關使用HTTP令牌執行身份驗證的資訊，請參見 [建立使用HTTP令牌執行SSO身份驗證的Flash Builder應用程式](/help/forms/developing/creating-flash-builder-applications-perform.md#creating-flash-builder-applications-that-perform-sso-authentication-using-http-tokens)。

### 使用自定義身份驗證 {#using-custom-authentication}

通過在遠程處理終結點上將身份驗證方法從「基本」更改為「自定義」，可以在管理控制台中啟用自定義身份驗證。 如果使用自定義身份驗證，則客戶端應用程式將調用 `ChannelSet.login` 登錄方法和 `ChannelSet.logout` 方法註銷。

>[!NOTE]
在上一版AEM Forms中，您通過調用 `RemoteObject.setCredentials` 的雙曲餘切值。 的 `setCredentials` 直到元件第一次嘗試連接到伺服器時，方法才實際將憑據傳遞到伺服器。 因此，如果元件發出故障事件，則無法確定是由於身份驗證錯誤還是出於其他原因而發生故障。 的 `ChannelSet.login` 方法在調用時連接到伺服器，以便您可以立即處理驗證問題。 儘管您可以繼續使用 `setCredentials` 方法，建議您使用 `ChannelSet.login` 的雙曲餘切值。

由於多個目標可以使用相同的通道和相應的ChannelSet對象，因此登錄到一個目標會將用戶登錄到使用相同通道或通道的任何其他目標。 如果兩個元件將不同的憑據應用於同一ChannelSet對象，則使用最後應用的憑據。 如果多個元件使用相同的經過驗證的ChannelSet對象，則調用 `logout` 方法將所有元件從目標中註銷。

以下示例使用 `ChannelSet.login` 和 `ChannelSet.logout` 方法。 此應用程式執行以下操作：

* 建立 `ChannelSet` 對象 `creationComplete` 表示由 `RemoteObject` 元件
* 通過調用 `ROLogin` 響應按鈕按一下事件
* 使用RemoteObject元件將字串發送到伺服器以響應Button按一下事件。 伺服器將相同的字串返回到RemoteObject元件
* 使用RemoteObject元件的結果事件在TextArea控制項中顯示字串
* 通過調用 `ROLogout` 響應按鈕按一下事件

```java
 <?xml version="1.0"?>
 <!-- security/SecurityConstraintCustom.mxml -->
 <mx:Application xmlns:mx="https://www.adobe.com/2006/mxml" width="100%"
     height="100%" creationComplete="creationCompleteHandler();">
 
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
                     token = cs.login("sampleuser", "samplepassword");
                     // Add result and fault handlers.
                     token.addResponder(new AsyncResponder(LoginResultEvent,
                     LoginFaultEvent));
                 }
             }
 
             // Handle successful login.
             private function LoginResultEvent(event:ResultEvent,
                 token:Object=null):void  {
                     switch(event.result) {
                         case "success":
                             authenticatedCB.selected = true;
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
                             case "success":
                                 authenticatedCB.selected = false;
                                 break;
                                 default:
                     }
                 }
 
                 // Handle logout failure.
                 private function LogoutFaultEvent(event:FaultEvent,
                     token:Object=null):void {
                         Alert.show("Logout failure: " + event.fault.faultString);
                 }
                 // Handle message recevied by RemoteObject component.
                 private function resultHandler(event:ResultEvent):void {
                     ta.text += "Server responded: "+ event.result + "\n";
                 }
 
                 // Handle fault from RemoteObject component.
                 private function faultHandler(event:FaultEvent):void {
                     ta.text += "Received fault: " + event.fault + "\n";
                 }
             ]]>
     </mx:Script>
     <mx:HBox>
         <mx:Label text="Enter a text for the server to echo"/>
         <mx:TextInput id="ti" text="Hello World!"/>
         <mx:Button label="Login"
             click="ROLogin();"/>
         <mx:Button label="Echo"
             enabled="{authenticatedCB.selected}"
             click="remoteObject.echo(ti.text);"/>
         <mx:Button label="Logout"
             click="ROLogout();"/>
         <mx:CheckBox id="authenticatedCB"
             label="Authenticated?"
             enabled="false"/>
     </mx:HBox>
     <mx:TextArea id="ta" width="100%" height="100%"/>
 
     <mx:RemoteObject id="remoteObject"
         destination="myDest"
         result="resultHandler(event);"
         fault="faultHandler(event);"/>
 </mx:Application>
```

的 `login` 和 `logout` 方法返回AsyncToken對象。 將事件處理程式分配給AsyncToken對象，以處理成功調用的結果事件，以及將錯誤事件分配給處理失敗的結果事件。

### 使用單一登錄 {#using-single-sign-on}

表AEM單用戶可以連接到多個AEM FormsWeb應用程式以執行任務。 當用戶從一個Web應用程式移動到另一個應用程式時，要求他們分別登錄到每個Web應用程式是不高效的。 AEM Forms單點登錄機制允許用戶一次登錄，然後訪問任何AEM FormsWeb應用程式。 因為AEM Forms的開發人員可以建立客戶端應用程式供AEM Forms使用，所以他們還必須能夠利用單一登錄機制。

每個AEM FormsWeb應用程式都打包在其自己的Web存檔(WAR)檔案中，然後將其打包為企業存檔(EAR)檔案的一部分。 由於應用程式伺服器不允許跨不同Web應用程式共用會話資料，AEM Forms使用HTTP Cookie來儲存驗證資訊。 驗證cookie使用戶能夠登錄到Forms應用程式，然後連接到其他AEM FormsWeb應用程式。 此技術稱為單點登錄。

AEM Forms開發人員編寫客戶端應用程式以擴展表單指南（不建議使用）的功能並自定義Workspace。 例如，Workspace應用程式可以啟動進程。 然後客戶端應用程式使用遠程端點從Forms服務檢索資料。

當使用（不建議使用表單）AEMAEM Forms遠程調用AEM Forms服務時，客戶端應用程式將作為請求的一部分傳遞身份驗證cookie。 由於用戶已經過身份驗證，因此無需再登錄即可從客戶端應用程式連接到AEM Forms服務。

>[!NOTE]
如果Cookie無效或丟失，則不會隱式重定向到登錄頁。 所以，你仍然可以叫匿名服務。

您可以通過編寫一個客戶端應用程式來繞過AEM Forms單一登錄機制，該應用程式可以自行登錄和註銷。 如果繞過單點登錄機制，則可以對應用程式使用基本或自定義身份驗證。

由於此機制不使用AEM Forms單點登錄機制，因此不會將身份驗證cookie寫入客戶端。 登錄憑據儲存在 `ChannelSet` 遠程通道的對象。 因此， `RemoteObject` 你打的電話 `ChannelSet` 是在這些全權證書的範圍內進行的。

### 在AEM Forms設定單一登錄 {#setting-up-single-sign-on-in-aem-forms}

要在AEM Forms使用單點登錄，請安裝表單工作流元件，其中包括集中登錄服務。 用戶成功登錄後，集中式登錄服務將驗證cookie返回給用戶。 每次後續對FormsWeb應用程式的請求都包含cookie。 如果cookie有效，則用戶將被視為已經過身份驗證，因此不必再次登錄。

### 編寫使用單一登錄的客戶端應用程式 {#writing-a-client-application-that-uses-single-sign-on}

使用單一登錄機制時，您希望用戶在啟動客戶端應用程式之前使用集中登錄服務登錄。 即，客戶端應用程式不會通過瀏覽器或通過調用 `ChannelSet.login` 的雙曲餘切值。

如果使用AEM Forms單點登錄機制，請將遠程處理終結點配置為使用自定義身份驗證，而不是基本身份驗證。 否則，在使用基本身份驗證時，身份驗證錯誤會導致瀏覽器質詢，您不希望用戶看到。 相反，您的應用程式會檢測到驗證錯誤，然後顯示一條消息，指示用戶使用集中登錄服務登錄。

客戶端應用程式通過使用 `RemoteObject` 元件，如下例所示。

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

**在Flex應用程式仍在運行時以新用戶身份登錄**

與Flex一起構建的應用程式套件括每次向AEM Forms服務請求時都包含身份驗證cookie。 出於效能原因，AEM Forms不會在每次請求時驗證cookie。 但是，AEM Forms確實會檢測何時將身份驗證cookie替換為另一個身份驗證cookie。

例如，您啟動客戶端應用程式，當應用程式處於活動狀態時，您可以使用集中登錄服務註銷。 接下來，您可以以其他用戶身份登錄。 以其他用戶身份登錄時，會用新用戶的驗證cookie替換現有的驗證cookie。

在客戶端應用程式的下一個請求中，AEM Forms檢測到cookie已更改，並註銷用戶。 因此，Cookie更改後的第一個請求失敗。 所有後續請求都在新cookie的上下文中發出，並且成功。

**註銷**

若要註銷AEM Forms並使會話失效，必須從客戶端的電腦中刪除身份驗證cookie。 由於一次登錄的目的是允許用戶一次登錄，因此您不希望客戶端應用程式刪除cookie。 此操作有效註銷用戶。

因此， `RemoteObject.logout` 客戶端應用程式中的方法在客戶端上生成一條錯誤消息，該錯誤消息指定會話未註銷。 相反，用戶可以使用集中式登錄服務註銷和刪除驗證cookie。

**在Flex應用程式仍在運行時註銷**

您可以啟動與Flex一起構建的客戶端應用程式，並使用集中登錄服務註銷。 作為註銷過程的一部分，驗證cookie被刪除。 如果遠程處理請求沒有cookie或cookie無效，則用戶會話無效。 此操作實際上是註銷。 下次客戶端應用程式嘗試連接到AEM Forms服務時，將請求用戶登錄。

**另請參閱**

[調用AEM Forms使用(不建議AEM用於表單)AEM Forms遠程處理](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[處理文檔時使用(不建議AEM使用表單)AEM Forms遠程處理](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[包括AEM FormsFlex圖書館的檔案](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[通過使用（不建議使用表單）傳遞不安全文檔來調用短AEM時間進程AEM Forms遠程](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[通過安全文檔調用進程使用遠程處理](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

## 通過安全文檔調用進程使用遠程處理 {#passing-secure-documents-to-invoke-processes-using-remoting}

調用需要一個或多個文檔的進程時，可以將安全文檔傳遞給AEM Forms。 通過傳遞安全文檔，您將保護業務資訊和機密文檔。 在這種情況下，文檔可以引用PDF文檔、XML文檔、Word文檔等。 如果將AEM Forms配置為允許安全文檔，則需要將安全文檔從寫入Flex的客戶端應用程式傳遞給AEM Forms。 (請參閱 [配置AEM Forms以接受安全文檔和不安全文檔](invoking-aem-forms-using-remoting.md#configuring-aem-forms-to-accept-secure-and-unsecure-documents)。)

傳遞安全文檔時，請使用單一登錄並指AEM定具有 *文檔上載應用程式用戶* 角色。 沒有此角色，用戶無法上載安全文檔。 可以以寫程式方式將角色分配給用戶。 (請參閱 [管理角色和權限](/help/forms/developing/users.md#managing-roles-and-permissions)。)

>[!NOTE]
建立新角色並希望該角色的成員上載安全文檔時，請確保指定「文檔上載」權限。

AEM Forms支援名為 `getFileUploadToken` 返回傳遞給上載servlet的令牌。 的 `DocumentReference.constructRequestForUpload` 方法需要指向AEM Forms的URL以及由 `LC.FileUploadAuthenticator.getFileUploadToken` 的雙曲餘切值。 此方法返回 `URLRequest` 在對上載servlet的調用中使用的對象。 以下代碼演示此應用程式邏輯。

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

### 配置AEM Forms以接受安全文檔和不安全文檔 {#configuring-aem-forms-to-accept-secure-and-unsecure-documents}

您可以使用管理控制台指定將文檔從Flex客戶端應用程式傳送到AEM Forms進程時文檔是否安全。 預設情況下，AEM Forms配置為接受安全文檔。 您可以通過執行以下步驟將AEM Forms配置為接受安全文檔：

1. 登錄到管理控制台。
1. 按一下 **設定**。
1. 按一下 **核心繫統設定。**
1. 按一下「Configurations（配置）」。
1. 確保未選中「允許從Flex應用程式上傳非安全文檔」選項。

>[!NOTE]
要配置AEM Forms以接受不安全文檔，請選擇允許從Flex應用程式上傳非安全文檔選項。 然後重新啟動應用程式或服務以確保設定生效。

### 快速啟動：通過使用遠程處理傳遞安全文檔來調用短期流程 {#quick-start-invoking-a-short-lived-process-by-passing-a-secure-document-using-remoting}

以下代碼示例調用 `MyApplication/EncryptDocument.`用戶必須登錄才能按一下「選擇檔案」按鈕，該按鈕用於上載PDF檔案並調用進程。 即，一旦用戶經過身份驗證，「選擇檔案」按鈕將啟用。 下圖顯示了用戶經過身份驗證後的Flex客戶端應用程式。 請注意，已啟用「已驗證」複選框。

![iu_iu_secureremotelogin](assets/iu_iu_secureremotelogin.png)

如果AEM Forms配置為僅允許上載安全文檔，而用戶沒有 *文檔上載應用程式用戶* 角色，然後引發異常。 如果用戶確實具有此角色，則上載檔案並調用該進程。

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
 
        // Set the docRef's url and referenceType parameters
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

[調用AEM Forms使用(不建議AEM用於表單)AEM Forms遠程處理](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[處理文檔時使用(不建議AEM使用表單)AEM Forms遠程處理](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[包括AEM FormsFlex圖書館的檔案](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[通過使用（不建議使用表單）傳遞不安全文檔來調用短AEM時間進程AEM Forms遠程](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[驗證使用Flex構建的客戶端應用程式](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

## 使用遠程調用自定義元件服務 {#invoking-custom-component-services-using-remoting}

可以使用遠程處理調用位於自定義元件中的服務。 例如，考慮包含客戶服務的銀行元件。 您可以使用寫入Flex的客戶端應用程式調用屬於客戶服務的操作。 在執行與此部分關聯的快速啟動之前，必須建立銀行自定義元件。

客戶服務公開名為 `createCustomer`。 本討論介紹如何建立調用客戶服務並建立客戶的Flex客戶端應用程式。 此操作需要複雜的類型對象 `com.adobe.livecycle.sample.customer.Customer` 代表新客戶。 下圖顯示了調用客戶服務並建立新客戶的客戶端應用程式。 的 `createCustomer` operation返回客戶標識符值。 標識符值顯示在「客戶標識符」文本框中。

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
   <td><p>指定客戶的名。 </p></td>
  </tr>
  <tr>
   <td><p>txt上次</p></td>
   <td><p>指定客戶的姓。 </p></td>
  </tr>
  <tr>
   <td><p>txtPhone</p></td>
   <td><p>指定客戶的電話號碼。</p></td>
  </tr>
  <tr>
   <td><p>txt街</p></td>
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
   <td><p>指定新帳戶所屬的客戶標識符值。 此文本框由客戶服務的返回值填充 <code>createCustomer</code> 的下界。 </p></td>
  </tr>
 </tbody>
</table>

### 映射AEM Forms複雜資料類型 {#mapping-aem-forms-complex-data-types}

一些AEM Forms操作需要複雜的資料類型作為輸入值。 這些複雜資料類型定義操作使用的運行時值。 例如，客戶服務 `createCustomer` 操作需要 `Customer` 包含服務所需的運行時值的實例。 如果沒有複雜類型，客戶服務將引發異常並不執行該操作。

調用AEM Forms服務時，建立映射到所需AEM Forms複雜類型的ActionScript對象。 對於操作所需的每個複雜資料類型，建立一個單獨的ActionScript對象。

在ActionScript類中，使用 `RemoteClass` 映射到AEM Forms複雜類型的元資料標籤。 例如，在調用客戶服務 `createCustomer` 操作，建立映射到的ActionScript類 `com.adobe.livecycle.sample.customer.Customer` 資料類型。

以下名為Customer的ActionScript類顯示如何映射到AEM Forms資料類型 `com.adobe.livecycle.sample.customer.Customer`。

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

將AEM Forms複雜類型的完全限定資料類型分配給別名標籤。

ActionScript類的欄位與屬於AEM Forms複雜類型的欄位匹配。 「客戶ActionScript」分類中的六個欄位與屬於 `com.adobe.livecycle.sample.customer.Customer`。

>[!NOTE]
確定屬於Forms複雜類型的欄位名稱的一個好方法是在Web瀏覽器中查看服務的WSDL。 WSDL指定服務的複雜類型和相應的資料成員。 以下WSDL用於客戶服務： `https://[yourServer]:[yourPort]/soap/services/CustomerService?wsdl.`

客戶ActionScript類屬於名為customer的包。 建議將映射到複雜AEM Forms資料類型的所有ActionScript類都放在它們自己的包中。 在Flex項目的src資料夾中建立一個資料夾，並將ActionScript檔案放在資料夾中，如下圖所示。

![iu_iu_customeras](assets/iu_iu_customeras.png)

### 快速啟動：使用遠程處理調用客戶自定義服務 {#quick-start-invoking-the-customer-custom-service-using-remoting}

下面的代碼示例調用客戶服務並建立客戶。 運行此代碼示例時，請確保填寫所有文本框。 另外，確保建立映射到 `com.adobe.livecycle.sample.customer.Customer`。

>[!NOTE]
在執行此快速啟動之前，必須建立和部署銀行自定義元件。

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

此快速入門包含名為 *bank.css*。 以下代碼表示使用的樣式表。

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

[調用AEM Forms使用(不建議AEM用於表單)AEM Forms遠程處理](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[處理文檔時使用(不建議AEM使用表單)AEM Forms遠程處理](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[包括AEM FormsFlex圖書館的檔案](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[通過使用（不建議使用表單）傳遞不安全文檔來調用短AEM時間進程AEM Forms遠程](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[驗證使用Flex構建的客戶端應用程式](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[通過安全文檔調用進程使用遠程處理](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)
