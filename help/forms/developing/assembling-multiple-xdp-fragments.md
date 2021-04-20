---
title: 組合多個XDP片段
seo-title: 組合多個XDP片段
description: 使用Java API和Web Service API，將多個XDP片段組合為單一XDP檔案。
seo-description: 使用Java API和Web Service API，將多個XDP片段組合為單一XDP檔案。
uuid: 0e35ff85-ff40-4878-ae31-aa8da75bd3ec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c4706632-02e5-4510-ad9c-4f732d5fbdad
docset: aem65
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1909'
ht-degree: 0%

---


# 組合多個XDP片段{#assembling-multiple-xdp-fragments}

您可以將多個XDP片段組合為單一XDP檔案。 例如，請考慮每個XDP檔案包含一個或多個用於建立健康表單的子表單的XDP片段。 下圖顯示大綱視圖（代表&#x200B;*組合多個XDP片段*&#x200B;快速啟動中使用的tuc018_template_gred.xdp檔案）:

![am_am_forma](assets/am_am_forma.png)

下圖顯示病人區段（代表&#x200B;*組合多個XDP片段*&#x200B;快速啟動中使用的tuc018_contact.xdp檔案）:

![am_am_formb](assets/am_am_formb.png)

下圖顯示病人健康區段（代表&#x200B;*組合多個XDP片段*&#x200B;快速啟動中使用的tuc018_patient.xdp檔案）:

![am_am_formc](assets/am_am_formc.png)

此片段包含兩個名為&#x200B;*subPatientPhysical*&#x200B;和&#x200B;*subPatientHealth*&#x200B;的子表單。 這兩個子表單都在傳遞給Assembler服務的DDX文檔中引用。 使用Assembler服務，您可以將所有這些XDP片段組合成單一XDP文檔，如下圖所示。

![am_am_formd](assets/am_am_formd.png)

以下DDX檔案會將多個XDP片段組合成XDP檔案。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <XDP result="tuc018result.xdp">
            <XDP source="tuc018_template_flowed.xdp">
             <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
               <XDPContent insertionPoint="ddx_fragment" source="tuc018_patient.xdp" fragment="subPatientPhysical" required="false"/>
               <XDPContent insertionPoint="ddx_fragment" source="tuc018_patient.xdp" fragment="subPatientHealth" required="false"/>
            </XDP>
         </XDP>
 </DDX>
```

DDX文檔包含XDP `result`標籤，該標籤指定結果的名稱。 在這種情況下，值為`tuc018result.xdp`。 在Assembler服務返回結果後，在用於檢索XDP文檔的應用程式邏輯中引用了此值。 例如，請考慮下列用於檢索已裝配的XDP文檔的Java應用程式邏輯（請注意，值被粗體化）:

```java
 //Iterate through the map object to retrieve the result XDP document
 for (Iterator i = allDocs.entrySet().iterator(); i.hasNext();) {
     // Retrieve the Map object’s value
     Map.Entry e = (Map.Entry)i.next();
     //Get the key name as specified in the
     //DDX document
     String keyName = (String)e.getKey();
     if (keyName.equalsIgnoreCase("tuc018result.xdp"))
                 {
         Object o = e.getValue();
         outDoc = (Document)o;
         //Save the result PDF file
         File myOutFile = new File("C:\\AssemblerResultXDP.xdp");
         outDoc.copyToFile(myOutFile);
     }
 }
```

`XDP source`標籤指定代表完整XDP文檔的XDP檔案，該檔案可用作添加XDP片段的容器，或作為按順序附加的多個文檔之一。 在這種情況下，XDP文檔僅用作容器（*組合多個XDP片段*&#x200B;中的第一個圖示）。 也就是說，其他XDP檔案會放在XDP容器中。

對於每個子表單，您可以新增`XDPContent`元素（此元素為選用元素）。 在上述範例中，請注意有三個子表單：`subPatientContact`、`subPatientPhysical`和`subPatientHealth`。 `subPatientPhysical`子表單和`subPatientHealth`子表單都位於相同的XDP檔案tuc018_patient.xdp中。 片段元素指定子表單的名稱，如設計器中所定義。

>[!NOTE]
>
>有關Assembler服務的詳細資訊，請參見[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參閱[匯編器服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟{#summary-of-steps}摘要

要組合多個XDP片段，請執行以下任務：

1. 包含專案檔案。
1. 建立PDF匯寫程式式用戶端。
1. 參考現有的DDX檔案。
1. 參考XDP檔案。
1. 設定執行時期選項。
1. 組合多個XDP檔案。
1. 檢索已裝配的XDP文檔。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將下列JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

**建立PDF匯寫程式式用戶端**

在以寫程式方式執行匯編器操作之前，請建立匯編器服務客戶端。

**參考現有的DDX檔案**

必須引用DDX文檔才能組合多個XDP文檔。 此DDX文檔必須包含`XDP result`、`XDP source`和`XDPContent`元素。

**參考XDP檔案**

要組合多個XDP文檔，請參考用於組合結果XDP文檔的所有XDP檔案。 確保在`fragment`屬性中指定了`source`屬性所引用的XDP文檔中包含的子表單的名稱。 子表單是在設計器中定義的。 例如，請考慮以下XML。

```xml
 <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
```

名為&#x200B;*subPatientContact*&#x200B;的子表單必須位於名為&#x200B;*tuc018_contact.xdp*&#x200B;的XDP檔案中。

**設定執行時期選項**

您可以設定運行時選項，以控制Assembler服務在執行作業時的行為。 例如，您可以設定一個選項，指示Assembler服務在遇到錯誤時繼續處理作業。

**組合多個XDP檔案**

要組合多個XDP檔案，請調用`invokeDDX`操作。 Assembler服務返回集合對象中已裝配的XDP文檔。

**檢索已裝配的XDP文檔**

在集合對象中返回已組合的XDP文檔。 重複收集物件，並將XDP檔案儲存為XDP檔案。 您也可以將XDP檔案傳遞至其他AEM Forms服務，例如輸出。

**另請參閱**

[使用Java API組合多個XDP片段](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-java-api)

[使用web service API組合多個XDP片段](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-web-service-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)

[使用片段建立PDF檔案](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)

## 使用Java API {#assemble-multiple-xdp-fragments-using-the-java-api}組合多個XDP片段

使用Assembler Service API(Java)組合多個XDP片段：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-assembler-client.jar。

1. 建立PDF匯寫程式式用戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`AssemblerServiceClient`對象。

1. 參考現有的DDX檔案。

   * 使用DDX文檔的建構子並傳遞指定DDX檔案位置的字串值，建立代表DDX文檔的`java.io.FileInputStream`對象。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 參考XDP檔案。

   * 使用`HashMap`建構函式建立`java.util.Map`物件，用來儲存輸入的XDP檔案。
   * 建立`com.adobe.idp.Document`對象並傳遞包含輸入XDP檔案的`java.io.FileInputStream`對象（對每個XDP檔案重複此任務）。
   * 通過調用`put`方法並傳遞以下參數，將條目添加到`java.util.Map`對象：

      * 代表索引鍵名稱的字串值。 此值必須與DDX文檔中指定的`source`元素值匹配（對每個XDP檔案重複此任務）。
      * 包含與`source`元素對應的XDP文檔的`com.adobe.idp.Document`對象（對每個XDP檔案重複此任務）。

1. 設定執行時期選項。

   * 使用其建構子建立一個`AssemblerOptionSpec`對象，該對象儲存運行時選項。
   * 通過調用屬於`AssemblerOptionSpec`對象的方法，設定運行時選項以滿足您的業務要求。 例如，若要指示Assembler服務在發生錯誤時繼續處理作業，請叫用`AssemblerOptionSpec`物件的`setFailOnError`方法並傳遞`false`。

1. 組合多個XDP檔案。

   叫用`AssemblerServiceClient`物件的`invokeDDX`方法並傳遞下列必要值：

   * `com.adobe.idp.Document`物件，代表要使用的DDX檔案
   * 包含輸入XDP檔案的`java.util.Map`對象
   * `com.adobe.livecycle.assembler.client.AssemblerOptionSpec`物件，指定執行時間選項，包括預設字型和工作記錄層級

   `invokeDDX`方法返回包含已裝配的XDP文檔的`com.adobe.livecycle.assembler.client.AssemblerResult`對象。

1. 檢索已裝配的XDP文檔。

   要獲取已裝配的XDP文檔，請執行以下操作：

   * 叫用`AssemblerResult`物件的`getDocuments`方法。 此方法返回`java.util.Map`對象。
   * 重複`java.util.Map`物件，直到找到結果`com.adobe.idp.Document`物件。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法，擷取已組合的XDP檔案。

**另請參閱**

[組合多個XDP片](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[段快速啟動（SOAP模式）:使用Java ](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-multiple-xdp-fragments-using-the-java-api)
[API組合多個XDP片段(包括AEM FormsJava庫檔案)](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用web service API {#assemble-multiple-xdp-fragments-using-the-web-service-api}組合多個XDP片段

使用Assembler Service API(web service)組合多個XDP片段：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 在設定服務引用時，請確保使用以下WSDL定義：

   ```java
    https://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms的伺服器的IP位址。

1. 建立PDF匯寫程式式用戶端。

   * 使用其預設建構子建立`AssemblerServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`AssemblerServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞給AEM Forms服務，如`https://localhost:8080/soap/services/AssemblerService?blob=mtom`。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。
   * 獲取`AssemblerServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將表AEM單用戶名分配給`AssemblerServiceClient.ClientCredentials.UserName.UserName`欄位。
      * 為`AssemblerServiceClient.ClientCredentials.UserName.Password`欄位分配相應的口令值。
      * 將`HttpClientCredentialType.Basic`常數值指派給`BasicHttpBindingSecurity.Transport.ClientCredentialType`欄位。
      * 將`BasicHttpSecurityMode.TransportCredentialOnly`常數值指派給`BasicHttpBindingSecurity.Security.Mode`欄位。

1. 參考現有的DDX檔案。

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存DDX檔案。
   * 通過調用`System.IO.FileStream`對象的建構子並傳遞一個字串值來建立對象，該字串值表示DDX文檔的檔案位置和開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞要讀取的位元組陣列、起始位置和串流長度。
   * 通過為`MTOM`對象的屬性指定位元組陣列的內容來填充`BLOB`對象。

1. 參考XDP檔案。

   * 對於每個輸入的XDP檔案，使用其建構子建立`BLOB`對象。 `BLOB`對象用於儲存輸入檔案。
   * 通過調用`System.IO.FileStream`對象的建構子並傳遞一個字串值來建立對象，該字串值表示輸入檔案的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞要讀取的位元組陣列、起始位置和串流長度。
   * 通過為`MTOM`對象的欄位分配位元組陣列的內容來填充`BLOB`對象。
   * 建立`MyMapOf_xsd_string_To_xsd_anyType`對象。 此收集對象用於儲存建立組合XDP文檔所需的輸入檔案。
   * 對於每個輸入檔案，建立一個`MyMapOf_xsd_string_To_xsd_anyType_Item`對象。
   * 為`MyMapOf_xsd_string_To_xsd_anyType_Item`對象的`key`欄位分配代表鍵名的字串值。 此值必須與DDX文檔中指定的元素值匹配。 （對每個輸入的XDP檔案執行此任務。）
   * 將儲存輸入檔案的`BLOB`對象分配給`MyMapOf_xsd_string_To_xsd_anyType_Item`對象的`value`欄位。 （對每個輸入的XDP檔案執行此任務。）
   * 將`MyMapOf_xsd_string_To_xsd_anyType_Item`對象添加到`MyMapOf_xsd_string_To_xsd_anyType`對象。 調用`MyMapOf_xsd_string_To_xsd_anyType`對象的`Add`方法並傳遞`MyMapOf_xsd_string_To_xsd_anyType`對象。 （對每個輸入的XDP文檔執行此任務。）

1. 設定執行時期選項。

   * 使用其建構子建立一個`AssemblerOptionSpec`對象，該對象儲存運行時選項。
   * 通過為屬於`AssemblerOptionSpec`對象的資料成員分配值，設定運行時選項以滿足您的業務要求。 例如，要指示Assembler服務在出現錯誤時繼續處理作業，請將`false`分配給`AssemblerOptionSpec`對象的`failOnError`資料成員。

1. 組合多個XDP檔案。

   叫用`AssemblerServiceClient`物件的`invokeDDX`方法並傳遞下列值：

   * 代表DDX文檔的`BLOB`對象
   * 包含所需檔案的`MyMapOf_xsd_string_To_xsd_anyType`對象
   * 指定運行時選項的`AssemblerOptionSpec`對象

   `invokeDDX`方法返回一個`AssemblerResult`對象，該對象包含作業的結果和發生的任何例外。

1. 檢索已裝配的XDP文檔。

   要獲取新建立的XDP文檔，請執行以下操作：

   * 存取`AssemblerResult`物件的`documents`欄位，此欄位是`Map`物件，包含產生的PDF檔案。
   * 重複`Map`物件，以取得每個結果檔案。 然後，將該陣列成員的`value`轉換為`BLOB`。
   * 存取PDF檔案的`BLOB`物件的`MTOM`屬性，擷取代表PDF檔案的二進位資料。 這會傳回可寫出至XDP檔案的位元組陣列。

**另請參閱**

[組合多個XDP片](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[段使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)