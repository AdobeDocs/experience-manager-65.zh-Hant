---
title: 組合多個XDP片段
seo-title: 組合多個XDP片段
description: 'null'
seo-description: 'null'
uuid: 0e35ff85-ff40-4878-ae31-aa8da75bd3ec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c4706632-02e5-4510-ad9c-4f732d5fbdad
docset: aem65
translation-type: tm+mt
source-git-commit: 9678b4979580bab23dea8ca7493b48b63d5bcfa6

---


# 組合多個XDP片段{#assembling-multiple-xdp-fragments}

您可以將多個XDP片段組合為單一XDP檔案。 例如，請考慮每個XDP檔案包含一個或多個用於建立健康表單的子表單的XDP片段。 下圖顯示大綱視圖(代表「組裝多個XDP片段快速啟動」中使用的tuc018_template_gred.xdp *檔案* ):

![am_am_forma](assets/am_am_forma.png)

下圖顯示病人區段(代表「組裝多個XDP片段快速啟動」中使用的tuc018_contact.xdp *檔案* ):

![am_am_formb](assets/am_am_formb.png)

下圖顯示病人健康區段(代表「組合多個XDP片段快速啟動」中使用的tuc018_patient.xdp *檔案* ):

![am_am_formc](assets/am_am_formc.png)

此片段包含兩個名為 *subPatientPhysical* 和 *subPatientHealth的子表單*。 這兩個子表單都在傳遞給Assembler服務的DDX文檔中引用。 使用Assembler服務，您可以將所有這些XDP片段組合成單一XDP文檔，如下圖所示。

![am_am_formd](assets/am_am_formd.png)

以下DDX檔案會將多個XDP片段組合成XDP檔案。

```as3
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

DDX文檔包含一個XDP `result` 標籤，該標籤指定結果的名稱。 在這種情況下，價值是 `tuc018result.xdp`。 在Assembler服務返回結果後，在用於檢索XDP文檔的應用程式邏輯中引用了此值。 例如，請考慮下列用於檢索已裝配的XDP文檔的Java應用程式邏輯（請注意，值被粗體化）:

```as3
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

標 `XDP source` 記指定代表完整XDP文檔的XDP檔案，該文檔可用作添加XDP片段的容器，或作為按順序附加在一起的多個文檔之一。 在此情況下，XDP檔案只會當做容器使用(如「組合多個XDP片段」中 *的第一個圖例*)。 也就是說，其他XDP檔案會放在XDP容器中。

您可以針對每個子表單新增元 `XDPContent` 素（此元素為選用元素）。 在上述範例中，請注意有三個子表單： `subPatientContact`、 `subPatientPhysical`和 `subPatientHealth`。 子表 `subPatientPhysical` 單和子表 `subPatientHealth` 單都位於相同的XDP檔案tuc018_patient.xdp中。 片段元素指定子表單的名稱，如設計器中所定義。

>[!NOTE]
>
>如需Assembler服務的詳細資訊，請參閱「AEM Forms的 [服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參 [閱Assembler Service和DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟摘要 {#summary-of-steps}

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
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

**建立PDF匯寫程式式用戶端**

在以寫程式方式執行匯編器操作之前，請建立匯編器服務客戶端。

**參考現有的DDX檔案**

必須引用DDX文檔才能組合多個XDP文檔。 此DDX檔案必 `XDP result`須包含 `XDP source`、和 `XDPContent` 元素。

**參考XDP檔案**

要組合多個XDP文檔，請參考用於組合結果XDP文檔的所有XDP檔案。 確保在屬性中指定了屬性引用的XDP文檔中包含 `source` 的子表單的名 `fragment` 稱。 子表單是在設計器中定義的。 例如，請考慮以下XML。

```as3
 <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
```

名為subPatientContact的子 *表單必須位於名為* tuc018_contact.xdp的XDP檔案中 **。

**設定執行時期選項**

您可以設定運行時選項，以控制Assembler服務在執行作業時的行為。 例如，您可以設定一個選項，指示Assembler服務在遇到錯誤時繼續處理作業。

**組合多個XDP檔案**

要組合多個XDP檔案，請調用該 `invokeDDX` 操作。 Assembler服務返回集合對象中已裝配的XDP文檔。

**檢索已裝配的XDP文檔**

在集合對象中返回已組合的XDP文檔。 重複收集物件，並將XDP檔案儲存為XDP檔案。 您也可以將XDP檔案傳遞至其他AEM Forms服務，例如「輸出」。

**另請參閱**

[使用Java API組合多個XDP片段](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-java-api)

[使用web service API組合多個XDP片段](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)

[使用片段建立PDF檔案](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)

## 使用Java API組合多個XDP片段 {#assemble-multiple-xdp-fragments-using-the-java-api}

使用Assembler Service API(Java)組合多個XDP片段：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-assembler-client.jar。

1. 建立PDF匯寫程式式用戶端。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `AssemblerServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 參考現有的DDX檔案。

   * 使用 `java.io.FileInputStream` 其建構子並傳遞指定DDX檔案位置的字串值，建立表示DDX文檔的對象。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 參考XDP檔案。

   * 使用 `java.util.Map` 建構函式建立用來儲存輸入XDP檔案的物 `HashMap` 件。
   * 建立對 `com.adobe.idp.Document` 像並傳遞包 `java.io.FileInputStream` 含輸入XDP檔案的對象（對每個XDP檔案重複此任務）。
   * 通過調用對象的方 `java.util.Map` 法並傳遞以 `put` 下參數，向對象添加條目：

      * 代表索引鍵名稱的字串值。 此值必須與DDX文 `source` 檔中指定的元素值匹配（對每個XDP檔案重複此任務）。
      * 包 `com.adobe.idp.Document` 含與元素對應的XDP文檔的對象(對每個XDP文 `source` 件重複此任務)。

1. 設定執行時期選項。

   * 使用 `AssemblerOptionSpec` 其建構函式建立儲存執行時期選項的物件。
   * 調用屬於該對象的方法，以設定運行時選項以滿足您的業務 `AssemblerOptionSpec` 要求。 例如，若要指示Assembler服務在發生錯誤時繼續處理作業，請叫用 `AssemblerOptionSpec` 物件的方 `setFailOnError` 法並傳遞 `false`。

1. 組合多個XDP檔案。

   叫用物 `AssemblerServiceClient` 件的方 `invokeDDX` 法並傳遞下列必要值：

   * 表 `com.adobe.idp.Document` 示要使用的DDX文檔的對象
   * 包 `java.util.Map` 含輸入XDP檔案的對象
   * 指定 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 運行時選項（包括預設字型和作業日誌級別）的對象
   該方 `invokeDDX` 法返回包 `com.adobe.livecycle.assembler.client.AssemblerResult` 含已裝配的XDP文檔的對象。

1. 檢索已裝配的XDP文檔。

   要獲取已裝配的XDP文檔，請執行以下操作：

   * 叫用 `AssemblerResult` 物件的方 `getDocuments` 法。 此方法返回對 `java.util.Map` 像。
   * 重複該對 `java.util.Map` 像，直到找到結果對 `com.adobe.idp.Document` 像。
   * 叫用物 `com.adobe.idp.Document` 件的方 `copyToFile` 法，以擷取組合的XDP檔案。

**另請參閱**

[組合多個XDP片段](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)[快速啟動（SOAP模式）:使用Java API組合多個XDP片段](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-multiple-xdp-fragments-using-the-java-api)[包括AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用web service API組合多個XDP片段 {#assemble-multiple-xdp-fragments-using-the-web-service-api}

使用Assembler Service API(web service)組合多個XDP片段：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 在設定服務引用時，請確保使用以下WSDL定義：

   ```as3
    https://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立PDF匯寫程式式用戶端。

   * 使用其 `AssemblerServiceClient` 預設建構函式建立物件。
   * 使用建 `AssemblerServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務，例如 `https://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `AssemblerServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給 `AssemblerServiceClient.ClientCredentials.UserName.UserName` 欄位。
      * 為欄位分配相應的密 `AssemblerServiceClient.ClientCredentials.UserName.Password`碼值。
      * 將常 `HttpClientCredentialType.Basic` 數值指派給欄 `BasicHttpBindingSecurity.Transport.ClientCredentialType`位。
      * 將常 `BasicHttpSecurityMode.TransportCredentialOnly` 數值指派給欄 `BasicHttpBindingSecurity.Security.Mode`位。

1. 參考現有的DDX檔案。

   * 使用其 `BLOB` 建構函式建立物件。 對 `BLOB` 像用於儲存DDX文檔。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示DDX文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法，以串流資料填 `System.IO.FileStream` 入位元組 `Read` 陣列。 傳遞要讀取的位元組陣列、起始位置和串流長度。
   * 為對象 `BLOB` 賦值其屬性， `MTOM` 使其包含位元組陣列的內容。

1. 參考XDP檔案。

   * 對於每個輸入的XDP檔案，請使用 `BLOB` 其建構子建立對象。 對 `BLOB` 像用於儲存輸入檔案。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示輸入檔案的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法，以串流資料填 `System.IO.FileStream` 入位元組 `Read` 陣列。 傳遞要讀取的位元組陣列、起始位置和串流長度。
   * 為對象 `BLOB` 分配欄位時， `MTOM` 請使用位元組陣列的內容來填充該對象。
   * 建立對 `MyMapOf_xsd_string_To_xsd_anyType` 像。 此收集對象用於儲存建立組合XDP文檔所需的輸入檔案。
   * 對於每個輸入檔案，建立一個 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象。
   * 為對象欄位指定代表鍵名 `MyMapOf_xsd_string_To_xsd_anyType_Item` 的字串 `key` 值。 此值必須與DDX文檔中指定的元素值匹配。 （對每個輸入的XDP檔案執行此任務。）
   * 將儲存 `BLOB` 輸入檔案的對象指派給對 `MyMapOf_xsd_string_To_xsd_anyType_Item` 像的字 `value` 段。 （對每個輸入的XDP檔案執行此任務。）
   * 將對象 `MyMapOf_xsd_string_To_xsd_anyType_Item` 添加到對 `MyMapOf_xsd_string_To_xsd_anyType` 像。 調用對 `MyMapOf_xsd_string_To_xsd_anyType` 像的方 `Add` 法並傳遞對 `MyMapOf_xsd_string_To_xsd_anyType` 像。 （對每個輸入的XDP文檔執行此任務。）

1. 設定執行時期選項。

   * 使用 `AssemblerOptionSpec` 其建構函式建立儲存執行時期選項的物件。
   * 通過為屬於該對象的資料成員分配值，設定運行時選項以滿足您的業務需 `AssemblerOptionSpec` 求。 例如，若要指示Assembler服務在發生錯誤時繼續處理作業，請指 `false` 派給 `AssemblerOptionSpec` 物件的資料 `failOnError` 成員。

1. 組合多個XDP檔案。

   叫用物 `AssemblerServiceClient` 件的方 `invokeDDX` 法並傳遞下列值：

   * 代 `BLOB` 表DDX文檔的對象
   * 包 `MyMapOf_xsd_string_To_xsd_anyType` 含所需檔案的對象
   * 指定 `AssemblerOptionSpec` 運行時選項的對象
   該方 `invokeDDX` 法返回 `AssemblerResult` 一個對象，該對象包含作業結果和所發生的任何異常。

1. 檢索已裝配的XDP文檔。

   要獲取新建立的XDP文檔，請執行以下操作：

   * 存取物 `AssemblerResult` 件的欄 `documents` 位，此欄位是包含 `Map` 結果PDF檔案的物件。
   * 重複該對 `Map` 像，以獲得每個結果文檔。 然後，將該陣列成員轉 `value` 換為 `BLOB`。
   * 存取PDF檔案的物件屬性，以擷取代表PDF文 `BLOB` 件的二進位 `MTOM` 資料。 這會傳回可寫出至XDP檔案的位元組陣列。

**另請參閱**

[使用MTOM組合多個XDP](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)[片段叫用AEM表單](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)