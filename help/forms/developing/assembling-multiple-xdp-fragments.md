---
title: 組裝多個XDP片段
seo-title: 組裝多個XDP片段
description: 使用Java API和Web服務API將多個XDP片段組合為單一XDP檔案。
seo-description: 使用Java API和Web服務API將多個XDP片段組合為單一XDP檔案。
uuid: 0e35ff85-ff40-4878-ae31-aa8da75bd3ec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c4706632-02e5-4510-ad9c-4f732d5fbdad
docset: aem65
role: Developer
exl-id: 54d98c69-2b2e-46cb-9f6a-7e9bdbe5c378
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1908'
ht-degree: 0%

---

# 組裝多個XDP片段{#assembling-multiple-xdp-fragments}

您可以將多個XDP片段組合為單一XDP檔案。 例如，假設有XDP片段，其中每個XDP檔案包含一或多個用來建立健全狀態表單的子表單。 下圖顯示大綱視圖（表示&#x200B;*組裝多個XDP片段*&#x200B;快速啟動中使用的tuc018_template_gled.xdp檔案）:

![am_am_forma](assets/am_am_forma.png)

下圖顯示患者區段（代表&#x200B;*組裝多個XDP片段*&#x200B;快速啟動中使用的tuc018_contact.xdp檔案）:

![am_am_formb](assets/am_am_formb.png)

下圖顯示患者健康部分（代表&#x200B;*組合多個XDP片段*&#x200B;快速啟動中使用的tuc018_patient.xdp檔案）:

![am_am_formc](assets/am_am_formc.png)

此片段包含名為&#x200B;*subPatientPhysical*&#x200B;和&#x200B;*subPatientHealth*&#x200B;的兩個子表單。 這兩個子表單都在傳遞到組合器服務的DDX文檔中引用。 使用組合器服務，您可以將所有這些XDP片段合併為單一XDP檔案，如下圖所示。

![am_am_formd](assets/am_am_formd.png)

以下DDX文檔將多個XDP片段組合到XDP文檔中。

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

DDX文檔包含XDP `result`標籤，該標籤指定結果的名稱。 在此情況下，值為`tuc018result.xdp`。 在組合器服務返回結果後，在用於檢索XDP文檔的應用程式邏輯中引用了此值。 例如，請考量下列用於擷取已組合XDP檔案的Java應用程式邏輯（請注意，值會以粗體顯示）:

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

`XDP source`標籤指定表示完整XDP文檔的XDP檔案，該文檔可用作添加XDP片段的容器，或作為按順序附加在一起的多個文檔之一。 在此情況下，XDP文檔僅用作容器（*組裝多個XDP片段*&#x200B;中所示的第一個圖）。 也就是說，其他XDP檔案會放在XDP容器中。

您可以對每個子表單新增`XDPContent`元素（此元素為選用元素）。 在上述範例中，請注意有三個子表單：`subPatientContact`、`subPatientPhysical`和`subPatientHealth`。 `subPatientPhysical`子表單和`subPatientHealth`子表單都位於相同的XDP檔案tuc018_patient.xdp中。 片段元素指定子表單的名稱，如設計器中定義。

>[!NOTE]
>
>有關組合器服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參閱[組合器服務和DDX引用](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟{#summary-of-steps}的摘要

若要組合多個XDP片段，請執行下列工作：

1. 包含專案檔案。
1. 建立PDF組合器客戶端。
1. 參考現有的DDX文檔。
1. 參考XDP檔案。
1. 設定運行時選項。
1. 組合多個XDP檔案。
1. 檢索已裝配的XDP文檔。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

**建立PDF組合器客戶端**

在以寫程式方式執行組合器操作之前，請建立組合器服務客戶端。

**參考現有的DDX文檔**

必須參考DDX檔案才能組合多個XDP檔案。 此DDX文檔必須包含`XDP result`、`XDP source`和`XDPContent`元素。

**參考XDP檔案**

要組合多個XDP文檔，請參考用於組合結果XDP文檔的所有XDP檔案。 確保在`fragment`屬性中指定`source`屬性引用的XDP文檔中包含的子表單的名稱。 子表單在設計器中定義。 例如，請考慮下列XML。

```xml
 <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
```

名為&#x200B;*subPatientContact*&#x200B;的子表單必須位於名為&#x200B;*tuc018_contact.xdp*&#x200B;的XDP檔案中。

**設定運行時選項**

您可以設定運行時選項，以控制組合器服務在執行作業時的行為。 例如，您可以設定一個選項，指示組合器服務在遇到錯誤時繼續處理作業。

**組合多個XDP檔案**

要組合多個XDP檔案，請調用`invokeDDX`操作。 組合器服務返回集合對象中已裝配的XDP文檔。

**檢索已裝配的XDP文檔**

集合對象內返回組合的XDP文檔。 逐一查看收集物件，並將XDP檔案儲存為XDP檔案。 您也可以將XDP檔案傳遞至其他AEM Forms服務，例如Output。

**另請參閱**

[使用Java API組合多個XDP片段](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-java-api)

[使用Web服務API組合多個XDP片段](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)

[使用片段建立PDF檔案](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)

## 使用Java API {#assemble-multiple-xdp-fragments-using-the-java-api}組合多個XDP片段

使用組合器服務API(Java)組合多個XDP片段：

1. 包含專案檔案。

   在Java項目的類路徑中包含客戶端JAR檔案，如adobe-assembler-client.jar。

1. 建立PDF組合器客戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`AssemblerServiceClient`物件。

1. 參考現有的DDX文檔。

   * 使用DDX文檔的建構子並傳遞指定DDX檔案位置的字串值，建立代表DDX文檔的`java.io.FileInputStream`對象。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 參考XDP檔案。

   * 使用`HashMap`建構子建立用於儲存輸入XDP文檔的`java.util.Map`對象。
   * 建立`com.adobe.idp.Document`物件並傳遞包含輸入XDP檔案的`java.io.FileInputStream`物件（對每個XDP檔案重複此工作）。
   * 調用`put`方法並傳遞以下參數，將條目添加到`java.util.Map`對象中：

      * 代表索引鍵名稱的字串值。 此值必須與DDX文檔中指定的`source`元素值匹配（對每個XDP檔案重複此任務）。
      * 包含與`source`元素對應的XDP文檔的`com.adobe.idp.Document`對象（對每個XDP檔案重複此任務）。

1. 設定執行時間選項。

   * 使用其建構子建立`AssemblerOptionSpec`物件，以儲存執行時選項。
   * 通過調用屬於`AssemblerOptionSpec`對象的方法來設定運行時選項以滿足您的業務要求。 例如，要指示組合器服務在發生錯誤時繼續處理作業，請調用`AssemblerOptionSpec`對象的`setFailOnError`方法並傳遞`false`。

1. 組合多個XDP檔案。

   調用`AssemblerServiceClient`對象的`invokeDDX`方法並傳遞以下必需值：

   * 表示要使用的DDX文檔的`com.adobe.idp.Document`對象
   * 包含輸入XDP檔案的`java.util.Map`對象
   * `com.adobe.livecycle.assembler.client.AssemblerOptionSpec`對象，它指定運行時選項，包括預設字型和作業日誌級別

   `invokeDDX`方法返回包含已裝配XDP文檔的`com.adobe.livecycle.assembler.client.AssemblerResult`對象。

1. 檢索已裝配的XDP文檔。

   要獲取已裝配的XDP文檔，請執行以下操作：

   * 調用`AssemblerResult`對象的`getDocuments`方法。 此方法會傳回`java.util.Map`物件。
   * 對`java.util.Map`對象進行迭代，直到找到結果`com.adobe.idp.Document`對象。
   * 調用`com.adobe.idp.Document`對象的`copyToFile`方法以提取已裝配的XDP文檔。

**另請參閱**

[組裝多個XDP](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[片段快速啟動（SOAP模式）:使用Java API組裝多個XDP片段包括](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-multiple-xdp-fragments-using-the-java-api)
[AEM Forms Java庫檔](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[案設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API {#assemble-multiple-xdp-fragments-using-the-web-service-api}組合多個XDP片段

使用組合器服務API（Web服務）組合多個XDP片段：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET項目。 在設定服務引用時，請確保使用以下WSDL定義：

   ```java
    https://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立PDF組合器客戶端。

   * 使用其預設建構子建立`AssemblerServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`AssemblerServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務，如`https://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 您不需要使用`lc_version`屬性。 建立服務參考時，會使用此屬性。
   * 獲取`AssemblerServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派至`AssemblerServiceClient.ClientCredentials.UserName.UserName`欄位。
      * 將相應的密碼值分配給`AssemblerServiceClient.ClientCredentials.UserName.Password`欄位。
      * 將`HttpClientCredentialType.Basic`常數值指派給`BasicHttpBindingSecurity.Transport.ClientCredentialType`欄位。
      * 將`BasicHttpSecurityMode.TransportCredentialOnly`常數值指派給`BasicHttpBindingSecurity.Security.Mode`欄位。

1. 參考現有的DDX文檔。

   * 使用其建構子建立`BLOB`物件。 `BLOB`對象用於儲存DDX文檔。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示DDX文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 叫用`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞位元組陣列、起始位置和資料流長度以讀取。
   * 為`MTOM`物件指派包含位元組陣列內容的屬性，以填入`BLOB`物件。

1. 參考XDP檔案。

   * 對於每個輸入的XDP檔案，使用其建構子建立`BLOB`對象。 `BLOB`對象用於儲存輸入檔案。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示輸入檔案的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 叫用`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞位元組陣列、起始位置和資料流長度以讀取。
   * 為`MTOM`欄位指定位元組陣列的內容，以填入`BLOB`物件。
   * 建立`MyMapOf_xsd_string_To_xsd_anyType`物件。 此收集對象用於儲存建立組合XDP文檔所需的輸入檔案。
   * 對於每個輸入檔案，建立`MyMapOf_xsd_string_To_xsd_anyType_Item`對象。
   * 為`MyMapOf_xsd_string_To_xsd_anyType_Item`對象的`key`欄位分配表示鍵名的字串值。 此值必須與DDX文檔中指定的元素的值匹配。 （對每個輸入XDP檔案執行此任務。）
   * 將儲存輸入檔案的`BLOB`物件指派至`MyMapOf_xsd_string_To_xsd_anyType_Item`物件的`value`欄位。 （對每個輸入XDP檔案執行此任務。）
   * 將`MyMapOf_xsd_string_To_xsd_anyType_Item`物件新增至`MyMapOf_xsd_string_To_xsd_anyType`物件。 調用`MyMapOf_xsd_string_To_xsd_anyType`對象的`Add`方法並傳遞`MyMapOf_xsd_string_To_xsd_anyType`對象。 （對每個輸入的XDP文檔執行此任務。）

1. 設定運行時選項。

   * 使用其建構子建立`AssemblerOptionSpec`物件，以儲存執行時選項。
   * 為屬於`AssemblerOptionSpec`對象的資料成員分配值，以設定運行時選項以滿足您的業務要求。 例如，要指示組合器服務在發生錯誤時繼續處理作業，請將`false`分配給`AssemblerOptionSpec`對象的`failOnError`資料成員。

1. 組合多個XDP檔案。

   調用`AssemblerServiceClient`對象的`invokeDDX`方法並傳遞以下值：

   * 代表DDX文檔的`BLOB`對象
   * 包含所需檔案的`MyMapOf_xsd_string_To_xsd_anyType`對象
   * 指定運行時選項的`AssemblerOptionSpec`對象

   `invokeDDX`方法返回一個`AssemblerResult`對象，該對象包含作業的結果和發生的任何異常。

1. 檢索已裝配的XDP文檔。

   要獲取新建立的XDP文檔，請執行以下操作：

   * 訪問`AssemblerResult`對象的`documents`欄位，該欄位是包含結果PDF文檔的`Map`對象。
   * 逐一查看`Map`對象，以獲取每個結果文檔。 然後，將該陣列成員的`value`轉換為`BLOB`。
   * 通過訪問其`BLOB`對象的`MTOM`屬性來提取表示PDF文檔的二進位資料。 這會傳回一個位元組陣列，您可將其寫出至XDP檔案。

**另請參閱**

[組裝多個XDP片](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[段使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
